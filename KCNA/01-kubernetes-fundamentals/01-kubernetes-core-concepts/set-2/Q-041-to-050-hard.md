# Kubernetes Core Concepts - Q41-Q50 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q41-Q50

---

### Question 41
[HARD]

A platform engineer is building a custom controller that needs to react to changes in ConfigMap objects across all namespaces. The controller must process every change without missing any updates, even if it temporarily loses connection to the API server. The engineer is considering using a standard GET request in a polling loop versus leveraging the Kubernetes watch mechanism. What is the primary advantage of the watch mechanism that makes it suitable for this use case?

A) Watch requests bypass RBAC authorization, allowing the controller to see all ConfigMaps regardless of permissions
B) Watch returns a stream of change notifications using resourceVersion, and if the watch is disconnected, it can resume from the last seen resourceVersion to avoid missing events
C) Watch automatically retries failed requests and guarantees exactly-once delivery of every event to the controller
D) Watch requests are served from the controller-manager's local cache instead of etcd, eliminating API server load entirely

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Kubernetes watch mechanism works by establishing a long-lived HTTP connection that streams change notifications (ADDED, MODIFIED, DELETED events) as they occur. Each event includes a resourceVersion, and if the watch connection is interrupted, the client can re-establish the watch starting from the last observed resourceVersion. This ensures that no events are missed during a temporary disconnection. Watch does not bypass RBAC (option A), does not guarantee exactly-once delivery (option C) since events may need to be reprocessed, and watch requests still go through the API server rather than being served from a controller-manager cache (option D).

**Source:** https://kubernetes.io/docs/reference/using-api/api-concepts/#efficient-detection-of-changes

</details>

---

### Question 42
[HARD]

A team has two CI/CD pipelines that both manage the same Deployment object. Pipeline A uses `kubectl apply` with server-side apply and sets the field manager name to "pipeline-a". Pipeline B also uses server-side apply with the field manager name "pipeline-b". Pipeline A sets `spec.replicas` to 3 in its manifest. Later, Pipeline B submits a manifest that also includes `spec.replicas` but sets it to 5. Neither pipeline uses the `--force-conflicts` flag. What happens when Pipeline B's apply is processed?

A) The API server merges both values and sets replicas to the higher value of 5
B) Pipeline B's apply succeeds and replicas is updated to 5, with ownership silently transferred from pipeline-a to pipeline-b
C) The API server returns a conflict error because the `spec.replicas` field is already owned by the "pipeline-a" field manager
D) The API server ignores Pipeline B's replicas field and keeps the value at 3, only applying non-conflicting fields from Pipeline B

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Server-side apply tracks field ownership using field managers. When Pipeline A applies with its field manager name, it becomes the owner of the `spec.replicas` field. When Pipeline B attempts to apply a different value for the same field, a conflict is detected because Pipeline B does not own that field. Without the `--force-conflicts` flag, the API server rejects the request with a conflict error. To resolve this, Pipeline B would need to use `--force-conflicts` to forcefully take ownership of the field, or the teams would need to coordinate so only one pipeline manages the replicas field. The API server does not merge conflicting values (option A), does not silently transfer ownership (option B), and does not silently ignore fields (option D).

**Source:** https://kubernetes.io/docs/reference/using-api/server-side-apply/#conflicts

</details>

---

### Question 43
[HARD]

A cluster administrator discovers that a third-party tool in their environment is still creating resources using the `extensions/v1beta1` API version for Ingress objects. The administrator knows this API version was removed in Kubernetes v1.22. The cluster is currently running Kubernetes v1.25. What is the expected behavior when the tool attempts to create an Ingress using `extensions/v1beta1`?

A) The API server automatically converts the request to the current `networking.k8s.io/v1` version and creates the Ingress successfully
B) The API server returns an error because the `extensions/v1beta1` API endpoint no longer exists and cannot serve requests for that version
C) The Ingress is created but stored with a deprecation warning annotation, and the object becomes read-only after 90 days
D) The API server accepts the request but schedules the object for automatic migration to `networking.k8s.io/v1` during the next garbage collection cycle

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When an API version is removed from a Kubernetes release, the corresponding REST endpoint is completely removed from the API server. Any client attempting to use the removed API version will receive an HTTP 404 or similar error because the endpoint simply does not exist. The Kubernetes API deprecation policy requires that API versions be deprecated for a minimum period before removal (typically at least two release cycles for beta APIs), giving users time to migrate. Once removed, there is no automatic conversion (option A), no deprecated-but-functional state (option C), and no deferred migration mechanism (option D). The tool must be updated to use the current `networking.k8s.io/v1` API version.

**Source:** https://kubernetes.io/docs/reference/using-api/deprecation-policy/

</details>

---

### Question 44
[HARD]

A Kubernetes cluster administrator needs to evaluate an alpha-stage feature called `PodSchedulingReadiness` before it becomes generally available. The administrator reads the documentation and learns that this feature is controlled by a feature gate. On a cluster running a standard Kubernetes release, which statement accurately describes how alpha feature gates work?

A) Alpha features are enabled by default but can be disabled through feature gates, and they are considered safe for production workloads
B) Alpha features are disabled by default, must be explicitly enabled via the `--feature-gates` flag on relevant components, and may be removed without notice in future releases
C) Alpha features cannot be enabled through feature gates and are only available in special "alpha" builds of Kubernetes distributed separately
D) Alpha features are automatically enabled once the cluster has been running for 30 days, allowing a stabilization period before activation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes uses feature gates to control the activation of alpha, beta, and GA features. Alpha features are disabled by default and must be explicitly enabled by setting the appropriate feature gate flag (e.g., `--feature-gates=PodSchedulingReadiness=true`) on the relevant Kubernetes components such as the API server, kubelet, or controller manager. Alpha features are considered experimental, may contain bugs, may change their behavior or API without notice, and can even be removed entirely in subsequent releases without a deprecation period. They are not recommended for production clusters. Beta features, by contrast, are enabled by default starting from Kubernetes v1.24 onward (previously they were also enabled by default, but the policy was tightened). GA features are always enabled and their feature gates are eventually removed.

**Source:** https://kubernetes.io/docs/reference/command-line-tools-reference/feature-gates/

</details>

---

### Question 45
[HARD]

A site reliability engineer is troubleshooting intermittent leader election failures in a highly available Kubernetes control plane with three API server replicas. They notice that the `kube-controller-manager` component uses Lease objects in the `kube-system` namespace for leader election. During investigation, they also observe that each node in the cluster has a corresponding Lease object in the `kube-node-lease` namespace. Which statement correctly distinguishes these two uses of Lease objects?

A) Both use cases serve the same purpose: they prevent split-brain scenarios by ensuring only one instance of each component or node is active at any time
B) Lease objects in `kube-system` are used for leader election among replicated control plane components, while Lease objects in `kube-node-lease` serve as lightweight node heartbeats that the kubelet renews to signal the node is alive
C) Lease objects in `kube-node-lease` are used for leader election among kubelets on different nodes, while Lease objects in `kube-system` track API server health check timestamps
D) Lease objects in `kube-system` store control plane component configuration, while Lease objects in `kube-node-lease` store the node's resource capacity and allocatable values

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes Lease objects serve two distinct but important purposes. In the `kube-system` namespace, Lease objects are used for leader election among replicated control plane components such as `kube-controller-manager` and `kube-scheduler`. Only the leader instance actively performs work, and the Lease object records which instance currently holds leadership. In the `kube-node-lease` namespace, each node has a corresponding Lease object that the kubelet periodically renews as a heartbeat signal. This is a more lightweight and scalable mechanism than the previous approach of updating the full Node object's status. The node controller uses these Lease renewals to determine node health. Kubelets do not participate in leader election (option C), and Lease objects do not store component configuration or node capacity data (option D).

**Source:** https://kubernetes.io/docs/concepts/architecture/leases/

</details>

---

### Question 46
[HARD]

A developer is writing an automation script that updates a Deployment and then verifies whether the update resulted in a new rollout. The script reads the Deployment object and examines its metadata. The developer notices two metadata fields: `.metadata.generation` and `.metadata.resourceVersion`. Both are numeric values that seem to increment. After changing only an annotation on the Deployment (without modifying the spec), the developer observes that `resourceVersion` changed but `generation` did not. Which explanation correctly describes the difference between these two fields?

A) `generation` is incremented on every write to the object including metadata changes, while `resourceVersion` is only incremented when the spec changes
B) `generation` represents the version of the desired state (spec) and is incremented only when the spec changes, while `resourceVersion` is an opaque value updated on every write to the object including status and metadata changes
C) `generation` is a cluster-wide counter shared across all objects, while `resourceVersion` is specific to each individual object
D) `generation` is set once at creation and never changes, while `resourceVersion` increments only when the object's status subresource is updated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `.metadata.generation` field represents a sequence number for the desired state of the object. It is incremented by the API server only when the object's spec (the desired state) is modified. Changes to metadata (like annotations or labels) or status do not increment generation. Controllers often compare `.metadata.generation` with `.status.observedGeneration` to determine if the controller has processed the latest spec changes. In contrast, `.metadata.resourceVersion` is an opaque value (typically derived from etcd's modification revision) that changes on every write to the object, regardless of which part (metadata, spec, or status) was modified. It is used for optimistic concurrency control. The resourceVersion is not a cluster-wide counter but is specific to the etcd revision system, and generation is not set only at creation (option D).

**Source:** https://kubernetes.io/docs/reference/using-api/api-concepts/#resource-versions

</details>

---

### Question 47
[HARD]

A team maintains a Kubernetes operator that updates Deployment objects by patching their container images. The operator currently uses a JSON merge patch to update the `spec.template.spec.containers` list. A bug report reveals that when the operator patches a Deployment that has two containers (an application container and a sidecar), the patch replaces the entire containers list with a single container, removing the sidecar. Which patching strategy would solve this problem while allowing the operator to update a specific container by name without affecting other containers in the list?

A) Use a JSON Patch (RFC 6902) operation that always appends new containers to the end of the list regardless of existing entries
B) Use a strategic merge patch, which uses the `name` field as a merge key for the containers list, allowing individual containers to be updated without replacing the entire list
C) Use a server-side apply with `--force-conflicts` to ensure all containers are preserved during the update
D) Use a JSON merge patch with the `$retainKeys` directive to preserve unspecified list items during the merge

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Strategic merge patch is a Kubernetes-specific patch strategy that understands the schema of Kubernetes objects. For lists that have a defined merge key (such as the `name` field for containers), strategic merge patch merges list items by their key rather than replacing the entire list. When the operator sends a strategic merge patch with only the application container specified, Kubernetes matches it by the container name and updates only that container, leaving the sidecar untouched. JSON merge patch (RFC 7396), by contrast, treats lists as atomic values and replaces the entire list with the patch value, which is the root cause of the bug. JSON Patch (option A) operates on specific array indices rather than merge keys, which is fragile. The `$retainKeys` directive (option D) is not a feature of JSON merge patch.

**Source:** https://kubernetes.io/docs/tasks/manage-kubernetes-objects/update-api-object-kubectl-patch/#use-a-strategic-merge-patch-to-update-a-deployment

</details>

---

### Question 48
[HARD]

A junior developer attempts to create a ClusterRole by specifying it within a YAML file that includes `metadata.namespace: production`. They apply the file using `kubectl apply -f clusterrole.yaml`. Separately, another team member tries to create a ResourceQuota without specifying any namespace in the YAML, and their current kubectl context has no default namespace set. Which outcome correctly describes what happens in each case?

A) The ClusterRole is created in the `production` namespace, and the ResourceQuota is created in the `kube-system` namespace as a fallback
B) The ClusterRole creation fails because cluster-scoped resources cannot have a namespace field, and the ResourceQuota is created in the `default` namespace
C) The ClusterRole is created and the namespace field is silently ignored because it is cluster-scoped, and the ResourceQuota is created in the `default` namespace because kubectl uses `default` when no namespace is specified
D) Both operations fail: ClusterRole cannot be created with a namespace, and ResourceQuota requires an explicit namespace

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Kubernetes resources are either namespace-scoped or cluster-scoped. ClusterRole is a cluster-scoped resource, meaning it exists outside of any namespace. If a namespace field is specified in the metadata for a cluster-scoped resource, the API server silently ignores it rather than returning an error. ResourceQuota, on the other hand, is a namespace-scoped resource and must belong to a namespace. When no namespace is specified in the YAML manifest and no namespace is set in the current kubectl context, kubectl defaults to the `default` namespace. The API server does not reject cluster-scoped resources that include a namespace field (option B and D are incorrect), and it does not fall back to `kube-system` for namespace-scoped resources (option A is incorrect).

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#not-all-objects-are-in-a-namespace

</details>

---

### Question 49
[HARD]

A DevOps engineer wants to validate a complex Kubernetes manifest before applying it to a production cluster. They want to ensure the manifest passes both client-side schema validation and server-side admission control (including webhooks) without actually persisting any changes. The engineer runs `kubectl apply -f manifest.yaml --dry-run=server`. The command returns successfully with no errors. Which statement accurately describes what was and was not validated during this server-side dry-run?

A) Server-side dry-run only validates YAML syntax and basic schema; it does not invoke admission webhooks or validate resource quotas
B) Server-side dry-run processes the request through the full admission chain including mutating and validating webhooks, but does not persist the object to etcd, so it cannot guarantee that concurrent changes or race conditions won't cause the actual apply to fail
C) Server-side dry-run persists the object temporarily to etcd for validation, then automatically rolls it back, guaranteeing the actual apply will succeed
D) Server-side dry-run validates against the schema only on the client side and sends a lightweight metadata check to the server, skipping all admission controllers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Server-side dry-run (`--dry-run=server`) sends the request to the API server, which processes it through the entire admission chain including mutating admission webhooks, validating admission webhooks, and built-in admission controllers like ResourceQuota. However, the final step of persisting the object to etcd is skipped. This means the dry-run validates nearly everything the real request would encounter, but it cannot account for race conditions such as another user consuming the remaining resource quota between the dry-run and the actual apply, or concurrent modifications to related objects. Client-side dry-run (`--dry-run=client`), by contrast, only performs local schema validation without contacting the API server. Server-side dry-run does not temporarily persist objects (option C) and it does process the full server-side admission chain (options A and D are incorrect).

**Source:** https://kubernetes.io/docs/reference/using-api/api-concepts/#dry-run

</details>

---

### Question 50
[HARD]

A developer creates a Pod with the name `web-server` in the `staging` namespace. After the Pod is running, the developer attempts to change the Pod's `spec.containers[0].name` from `nginx` to `web-app` using `kubectl edit`. The edit is rejected by the API server. The developer also tries to update `metadata.labels` and `spec.containers[0].image`, and both of those changes succeed. Which statement best explains the immutability rules that govern these different outcomes?

A) Container names, container images, and labels are all mutable, but the API server randomly rejects edits during high load to protect etcd performance
B) Container names are immutable because the `spec.containers` list uses the `name` field as its merge key and identity, making it part of the Pod's structural identity, while labels and container images are mutable fields that can be updated after creation
C) All fields under `spec` are immutable after Pod creation, so the image change must have been applied through a Pod replacement rather than an in-place update
D) Container names can only be changed by deleting the container and adding a new one in the same edit operation, while labels and images are freely mutable

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes Pods have strict immutability rules for most of their spec fields, but not all. The container `name` field within `spec.containers` is immutable after Pod creation because it serves as the merge key that uniquely identifies each container within the Pod. Changing a container's name would effectively mean replacing one container with a different one, which is not allowed as an in-place update. By contrast, `metadata.labels` is always mutable for any Kubernetes object, and `spec.containers[*].image` is one of the few spec fields explicitly allowed to be updated on an existing Pod. Other mutable Pod fields include `spec.activeDeadlineSeconds`, `spec.tolerations` (additions only), and certain container resource fields in specific conditions. The claim that all spec fields are immutable (option C) is incorrect, and there is no mechanism to replace a container by name in a single edit (option D).

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/#pod-update-and-replacement

</details>
