# Kubernetes Core Concepts - Q81-Q90 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q81-Q90

---

### Question 81
[HARD]

A team provisions a PersistentVolume (PV) with `persistentVolumeReclaimPolicy: Retain` and a PersistentVolumeClaim (PVC) binds to it. A developer then deletes the PVC. What is the state of the PV immediately after the PVC deletion, and can a new PVC automatically bind to it?

A) The PV is deleted along with the PVC; the underlying storage is removed
B) The PV enters a `Released` state and a new PVC can automatically bind to it
C) The PV enters a `Released` state but no new PVC can automatically bind to it until an administrator manually reclaims it
D) The PV returns to an `Available` state and is immediately ready for a new PVC to claim

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a PVC bound to a PV with `Retain` reclaim policy is deleted, the PV transitions to the `Released` state rather than `Available`. In the `Released` state, the PV still holds a reference to the previous claim and retains the data on the underlying storage. A new PVC cannot automatically bind to a `Released` PV because Kubernetes considers it as still holding the previous claimant's data. An administrator must manually remove the claimRef from the PV spec (and optionally clean up the data) before it returns to `Available` and can be bound again.

**Source:** https://kubernetes.io/docs/concepts/storage/persistent-volumes/#retain

</details>

---

### Question 82
[HARD]

A cluster administrator creates a StorageClass named `fast-ssd` with `provisioner: kubernetes.io/aws-ebs` and `reclaimPolicy: Delete`. A developer creates a PVC that references this StorageClass. The PVC enters `Bound` status, and a PV appears that was not manually created. Later, the developer deletes the PVC. What happens to the dynamically provisioned PV and the underlying EBS volume?

A) The PV is retained in `Released` state and the EBS volume persists; the administrator must clean up manually
B) The PV is deleted but the underlying EBS volume is retained for manual recovery
C) Both the PV object and the underlying EBS volume are deleted automatically
D) The PV is recycled by wiping the volume data and returned to the `Available` pool

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a StorageClass has `reclaimPolicy: Delete`, deleting the PVC triggers deletion of both the PersistentVolume object in Kubernetes and the underlying storage asset in the external infrastructure (in this case, the AWS EBS volume). This is the default reclaim policy for dynamically provisioned volumes. The `Retain` policy would preserve both, and `Recycle` (deprecated) would scrub the data. Since the StorageClass explicitly set `Delete`, the entire chain of resources is cleaned up automatically upon PVC deletion.

**Source:** https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy

</details>

---

### Question 83
[HARD]

A team needs to deploy a distributed file processing application where multiple Pods across different nodes must simultaneously read and write to the same shared volume. Which access mode must the PersistentVolumeClaim request, and what is a key constraint of this choice?

A) `ReadWriteOnce` -- this allows multiple Pods to read and write as long as they are on the same node
B) `ReadOnlyMany` -- multiple Pods can access the volume across nodes, but write operations require a separate volume
C) `ReadWriteMany` -- multiple Pods across nodes can read and write, but this mode is only supported by certain storage backends such as NFS or CephFS
D) `ReadWriteOncePod` -- this ensures exclusive access for one Pod, which is the safest option for concurrent writes

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** `ReadWriteMany` (RWX) is the only access mode that allows multiple Pods on multiple nodes to simultaneously mount the volume for both reading and writing. However, not all storage backends support RWX -- block storage systems like AWS EBS and GCE Persistent Disk only support `ReadWriteOnce`. Shared file systems like NFS, CephFS, and Azure Files support RWX. `ReadWriteOnce` only guarantees single-node mount for read-write, `ReadOnlyMany` does not permit writes, and `ReadWriteOncePod` restricts access to a single Pod entirely.

**Source:** https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes

</details>

---

### Question 84
[HARD]

A Pod specification includes an `emptyDir` volume shared between an init container and an application container. The init container writes a configuration file to the `emptyDir`, then exits successfully. The application container reads this file on startup. Later, the node running the Pod experiences a kernel panic and the Pod is rescheduled to a different node. What happens to the data in the `emptyDir` volume?

A) The data persists because `emptyDir` volumes are stored in etcd and replicated across the cluster
B) The data is lost because `emptyDir` is tied to the Pod's lifecycle on the original node; the rescheduled Pod gets a fresh empty volume
C) The data is automatically migrated to the new node by the kubelet before the Pod starts
D) The data is preserved in the node's local storage and restored when the Pod is rescheduled back to the original node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An `emptyDir` volume is created when a Pod is assigned to a node and exists for as long as that Pod runs on that specific node. When the Pod is removed from the node for any reason -- including rescheduling after a node failure -- the data in the `emptyDir` is permanently deleted. The rescheduled Pod on the new node receives a completely new, empty `emptyDir` volume. This means the init container will run again on the new node and regenerate the configuration file. `emptyDir` is not replicated, not stored in etcd, and not migrated between nodes.

**Source:** https://kubernetes.io/docs/concepts/storage/volumes/#emptydir

</details>

---

### Question 85
[HARD]

A developer configures a Pod to use a `hostPath` volume of type `DirectoryOrCreate` pointing to `/var/app/data` on the node. The Pod is part of a Deployment with 3 replicas. In a multi-node cluster, what are two significant risks of this design?

A) The `hostPath` volume cannot be mounted by more than one container, so only one replica will start; the others will fail with a mount error
B) Each replica may land on a different node and see different data (or empty directories), and any replica has direct read/write access to the host filesystem, creating a security risk
C) The `hostPath` volume type is deprecated and will cause the Pod to enter `CrashLoopBackOff` on Kubernetes 1.25+
D) The `hostPath` volume forces all replicas to be scheduled on the same node, defeating the purpose of multiple replicas for high availability

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `hostPath` mounts a file or directory from the host node's filesystem into the Pod. Since Deployment replicas can be scheduled on different nodes, each replica accesses the local filesystem of its respective node, meaning they see entirely different data -- or freshly created empty directories if `DirectoryOrCreate` is used. Additionally, `hostPath` grants the Pod direct access to the host's filesystem, which is a significant security concern because a compromised container could read or modify sensitive host files. `hostPath` does not force co-location, is not deprecated, and does not restrict mounting to a single container.

**Source:** https://kubernetes.io/docs/concepts/storage/volumes/#hostpath

</details>

---

### Question 86
[HARD]

A team has a ConfigMap named `app-config` containing a key `settings.yaml` with a multi-line YAML configuration. They need the application to see this as a file at `/etc/app/settings.yaml` inside the container. They also want changes to the ConfigMap to be reflected in the running Pod without restarting it. Which approach should they use, and what is a limitation?

A) Use an environment variable from the ConfigMap; environment variables are automatically refreshed when the ConfigMap changes
B) Mount the ConfigMap as a volume at `/etc/app`; the kubelet will eventually update the mounted file when the ConfigMap changes, but there may be a delay of up to the kubelet sync period plus the cache propagation delay
C) Mount the ConfigMap as a volume at `/etc/app`; the file is updated instantaneously with zero delay whenever the ConfigMap changes
D) Use an environment variable with `envFrom` and set `configMapRef` to auto-reload; this is the only method that supports live updates

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a ConfigMap is mounted as a volume, Kubernetes projects the data as files in the specified directory. The kubelet periodically checks for ConfigMap updates and refreshes the mounted files using atomic symlink swaps. However, this update is not instantaneous -- it can take up to the kubelet's sync period (default 60 seconds) plus the time for the API server cache to propagate the change. Environment variables sourced from ConfigMaps, by contrast, are set at container start time and never updated during the container's lifetime, making them unsuitable for live configuration changes. The application must also be capable of detecting and reloading the file.

**Source:** https://kubernetes.io/docs/concepts/configuration/configmap/#mounted-configmaps-are-updated-automatically

</details>

---

### Question 87
[HARD]

A security engineer reviews a Pod specification and notices that a Secret named `db-creds` is mounted as a volume at `/etc/secrets`. They want to understand the security implications of this mount. Which statement accurately describes how Kubernetes handles Secret volume mounts?

A) Secret data is written to the node's local disk in an encrypted file, and the kubelet decrypts it on-the-fly when the container reads the file
B) Secret data is stored on a tmpfs (RAM-backed filesystem) by default, so the data is never written to the node's physical disk, but it is still base64-decoded and readable as plaintext inside the container
C) Secret data is mounted as an encrypted volume that requires the container to supply a decryption key at runtime
D) Secret data is streamed directly from the API server to the container process at read time, never touching the node's filesystem or memory

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Secret is mounted as a volume in a Pod, the kubelet stores the Secret data on a tmpfs (an in-memory filesystem) on the node, which means the data is held in RAM and not written to the node's physical disk. This provides a layer of protection against data recovery from disk. However, the data inside the container is base64-decoded and presented as plaintext files, so any process in the container can read the secret values. Secrets are not encrypted at the volume mount level -- encryption at rest applies only to how Secrets are stored in etcd, not how they are delivered to Pods. This is why additional measures like RBAC, Pod Security Standards, and encryption at rest are recommended.

**Source:** https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-files-from-a-pod

</details>

---

### Question 88
[HARD]

A cluster administrator is planning a storage strategy for a production Kubernetes cluster. They have PersistentVolumes that contain sensitive customer data. They want to ensure that when tenants delete their PVCs, the underlying storage is not automatically destroyed, but the PVs are also not immediately available for other tenants to claim. Which reclaim policy meets both requirements, and what manual step must the administrator perform to make the PV available again?

A) `Delete` policy -- the PV is destroyed but the admin can recover data from cloud provider snapshots
B) `Recycle` policy -- the PV data is scrubbed with `rm -rf` and the PV returns to `Available`, preventing other tenants from seeing old data
C) `Retain` policy -- the PV moves to `Released` state preserving data; the admin must manually clean up the data and remove the PV's `claimRef` to make it `Available` again
D) `Archive` policy -- the PV is moved to cold storage automatically and a new PV is created for the next tenant

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `Retain` reclaim policy preserves the PV and its underlying storage when the bound PVC is deleted. The PV transitions to the `Released` state, which prevents any new PVC from automatically binding to it -- this is critical for data isolation between tenants. To reuse the PV, the administrator must take explicit action: verify or clean up the data on the underlying volume, and then edit the PV to remove the `.spec.claimRef` field, which transitions it back to `Available`. The `Delete` policy would destroy the data, `Recycle` is deprecated and would erase data without administrator oversight, and `Archive` is not a valid Kubernetes reclaim policy.

**Source:** https://kubernetes.io/docs/concepts/storage/persistent-volumes/#retain

</details>

---

### Question 89
[HARD]

A platform team is evaluating storage solutions for their Kubernetes cluster. They notice that the Kubernetes core repository no longer accepts new in-tree volume plugins and that existing in-tree plugins are being migrated. What is the primary reason Kubernetes introduced the Container Storage Interface (CSI), and how does it change the relationship between Kubernetes and storage vendors?

A) CSI was introduced to improve storage performance by bypassing the kubelet and allowing direct communication between Pods and storage backends
B) CSI was introduced so that storage vendor code is developed and deployed independently of the Kubernetes core, allowing vendors to release updates on their own schedule without requiring changes to Kubernetes itself
C) CSI was introduced to replace PersistentVolumes entirely with a simpler API that does not require PVCs
D) CSI was introduced to enforce encryption at rest for all volume types, which was not possible with in-tree plugins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Container Storage Interface (CSI) was created as an industry standard to decouple storage plugin development from the Kubernetes core codebase. Before CSI, every storage provider had to contribute in-tree volume plugins directly to the Kubernetes repository, meaning storage bug fixes and features were tied to Kubernetes release cycles. With CSI, storage vendors develop, deploy, and maintain their own CSI driver as separate containerized workloads (typically DaemonSets and Deployments), releasing updates independently. CSI does not bypass the kubelet, does not replace PersistentVolumes, and is not specifically about encryption -- it is fundamentally about extensibility and independent lifecycle management.

**Source:** https://kubernetes.io/blog/2019/01/15/container-storage-interface-ga/

</details>

---

### Question 90
[HARD]

A developer needs a temporary scratch volume for a batch processing Pod that should be provisioned dynamically with specific storage characteristics (e.g., high-IOPS SSD) and automatically cleaned up when the Pod terminates. They do not want the volume to persist beyond the Pod's lifecycle, but they also need more flexibility than what a basic `emptyDir` can provide. Which volume approach should they use?

A) A generic ephemeral volume with an embedded PVC template that references a StorageClass, which dynamically provisions storage scoped to the Pod's lifetime
B) A standard PersistentVolumeClaim with `persistentVolumeReclaimPolicy: Delete`, manually deleted after the Pod completes
C) An `emptyDir` volume with `sizeLimit` set and `medium: Memory`, which provides high-IOPS tmpfs storage
D) A `hostPath` volume pointing to a local SSD, which is automatically cleaned up when the Pod terminates

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Generic ephemeral volumes allow a Pod spec to include an embedded PVC template that creates a PersistentVolumeClaim owned by the Pod. This PVC can reference a StorageClass to dynamically provision storage with specific characteristics (such as high-IOPS SSD). When the Pod terminates, the PVC is garbage collected because the Pod is its owner, and if the StorageClass has a `Delete` reclaim policy, the underlying storage is also cleaned up. This provides the dynamic provisioning flexibility of PVCs with the ephemeral lifecycle of Pod-scoped volumes. An `emptyDir` with `medium: Memory` uses RAM and cannot leverage provisioned disk storage. A `hostPath` volume is not cleaned up automatically and has no dynamic provisioning. A standard PVC would persist beyond the Pod unless manually deleted.

**Source:** https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/#generic-ephemeral-volumes

</details>
