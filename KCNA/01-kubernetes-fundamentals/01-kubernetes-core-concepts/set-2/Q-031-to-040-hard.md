# Kubernetes Core Concepts - Q31-Q40 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q31-Q40

---

### Question 31
[HARD]

A production Kubernetes cluster runs a 3-node etcd cluster behind the control plane. During a network partition, 2 of the 3 etcd nodes become unreachable simultaneously. An engineer attempts to create a new Deployment using `kubectl apply`. What happens?

A) The Deployment is created successfully because the remaining etcd node can still serve writes
B) The Deployment creation fails because etcd has lost quorum and cannot commit new writes
C) The Deployment is queued in the kube-apiserver and applied once the etcd nodes recover
D) The kube-apiserver automatically switches to an in-memory store until etcd recovers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** etcd uses the Raft consensus algorithm, which requires a strict majority (quorum) of nodes to agree before committing any write. For a 3-node cluster, the quorum is 2. When 2 of 3 nodes are unreachable, only 1 node remains, which cannot form a quorum. The kube-apiserver will be unable to persist the Deployment object and will return an error to the client. The API server does not queue writes or fall back to alternative storage -- it relies entirely on etcd for persistence, and without quorum, all mutating operations fail.

**Source:** https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#multi-node-etcd-cluster

</details>

---

### Question 32
[HARD]

A node is under memory pressure and the kubelet must evict Pods. The node is running three Pods: Pod A has both CPU and memory requests and limits set to identical values, Pod B has memory requests set lower than its limits, and Pod C has no resource requests or limits defined at all. In what order will the kubelet evict these Pods?

A) Pod A first, then Pod B, then Pod C -- because Guaranteed Pods consume the most reserved resources
B) Pod C first, then Pod B, then Pod A -- because BestEffort Pods are evicted before Burstable, which are evicted before Guaranteed
C) Pod B first, then Pod C, then Pod A -- because Burstable Pods exceeding requests are evicted first
D) All three Pods are evicted simultaneously since the node is under pressure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes assigns QoS classes based on resource specifications: Guaranteed (all containers have equal requests and limits for both CPU and memory), Burstable (at least one container has a request or limit set but does not qualify as Guaranteed), and BestEffort (no requests or limits at all). Pod A is Guaranteed, Pod B is Burstable, and Pod C is BestEffort. When the kubelet performs eviction under memory pressure, it follows the order BestEffort first, then Burstable, and finally Guaranteed. This protects Pods that have made explicit resource guarantees while sacrificing those that have not.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/#pod-selection-for-kubelet-eviction

</details>

---

### Question 33
[HARD]

An engineer configures a Pod with a PreStop lifecycle hook that runs a shell command taking 15 seconds to complete. The Pod's `terminationGracePeriodSeconds` is set to 5. When Kubernetes sends a termination signal to the Pod, what happens to the PreStop hook?

A) The PreStop hook runs to completion (15 seconds) because lifecycle hooks are exempt from the grace period
B) The PreStop hook is skipped entirely because the grace period is shorter than the hook duration
C) The PreStop hook starts executing but is forcibly terminated after 5 seconds when the grace period expires, and the container is killed with SIGKILL
D) The PreStop hook extends the grace period automatically to 15 seconds to allow completion

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When Kubernetes terminates a Pod, it first executes the PreStop hook (if defined) before sending SIGTERM to the container process. However, the entire graceful shutdown sequence -- including the PreStop hook and the subsequent SIGTERM handling -- must complete within the `terminationGracePeriodSeconds`. If the PreStop hook is still running when the grace period expires, Kubernetes sends SIGKILL to forcibly terminate the container. In this scenario, the 15-second hook cannot finish within the 5-second grace period, so the container is killed after 5 seconds. The grace period is not automatically extended; it acts as a hard deadline for the entire termination sequence.

**Source:** https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#hook-handler-execution

</details>

---

### Question 34
[HARD]

A cluster administrator creates a PriorityClass named `critical-service` with a priority value of 1000000 and `preemptionPolicy: PreemptLowerPriority`. A new Pod using this PriorityClass cannot be scheduled because no node has sufficient resources. Several lower-priority Pods are running across the cluster. What does the scheduler do?

A) The high-priority Pod remains Pending indefinitely until a node with sufficient resources becomes available through natural Pod completion
B) The scheduler identifies a node where evicting one or more lower-priority Pods would free enough resources, evicts those Pods, and schedules the high-priority Pod on that node
C) The scheduler scales up the cluster by adding a new node automatically to accommodate the high-priority Pod
D) The scheduler splits the high-priority Pod's resource requests across multiple nodes using Pod topology spread

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a high-priority Pod cannot be scheduled and its PriorityClass has `preemptionPolicy: PreemptLowerPriority` (the default), the scheduler enters its preemption logic. It evaluates each node to determine if evicting one or more lower-priority Pods would make the node feasible for the pending Pod. If such a node is found, the scheduler preempts (evicts) the selected lower-priority Pods by setting their `deletionTimestamp` and giving them a grace period to terminate. Once sufficient resources are freed, the high-priority Pod is scheduled onto that node. The scheduler does not auto-scale clusters or split Pods across nodes -- those are responsibilities of external components like the Cluster Autoscaler.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/#preemption

</details>

---

### Question 35
[HARD]

A developer needs to debug a running Pod that was built from a minimal distro image containing no shell or debugging utilities. The Pod is in a CrashLoopBackOff state, but the developer needs to inspect the process environment and filesystem of the running container. Which Kubernetes feature allows attaching a temporary container with debugging tools to this running Pod without modifying the Pod spec or restarting it?

A) Init containers, which run before the main container and can be used to inject debugging tools into a shared volume
B) Sidecar containers added via a `kubectl edit` command to inject a debug container alongside the main container
C) Ephemeral containers, which can be added to an already-running Pod via `kubectl debug` to provide debugging utilities
D) A DaemonSet running a privileged debug Pod on each node that shares the host PID namespace

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Ephemeral containers are a special type of container that can be added to an existing Pod temporarily for debugging purposes using `kubectl debug`. Unlike regular or init containers, they are not defined in the Pod spec at creation time and cannot be added via `kubectl edit`. They are designed specifically for troubleshooting scenarios where a distroless or minimal container image lacks debugging tools. Ephemeral containers can share process namespaces with other containers in the Pod, allowing inspection of the target container's filesystem and processes. Init containers are not applicable here because they only run before the main container starts and cannot be added after Pod creation.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/

</details>

---

### Question 36
[HARD]

A platform team needs to mount a Pod's ServiceAccount token, a ConfigMap containing application settings, and a Secret containing TLS certificates into a single directory at `/etc/app-config` inside the container. Each source must appear as files in the same mount path. Which volume type achieves this?

A) An emptyDir volume with an init container that copies data from each source into the shared directory
B) A projected volume that combines the ServiceAccount token, ConfigMap, and Secret sources into one volume mount
C) Three separate volume mounts at `/etc/app-config/token`, `/etc/app-config/settings`, and `/etc/app-config/tls` respectively
D) A hostPath volume pointing to a node directory pre-populated with all three data sources

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A projected volume allows combining multiple volume sources -- including Secrets, ConfigMaps, Downward API fields, and ServiceAccount tokens -- into a single directory under one volume mount. This is the only native volume type that can merge heterogeneous sources into a unified file tree at a single mount point. Option C would work but uses three separate mount paths (subdirectories), not a single flat directory as required. Option A is an engineering workaround, not a native Kubernetes feature. Projected volumes were designed precisely for this use case of aggregating multiple configuration sources into one location.

**Source:** https://kubernetes.io/docs/concepts/storage/projected-volumes/

</details>

---

### Question 37
[HARD]

A team is building a monitoring sidecar that needs to dynamically discover its own Pod name, namespace, the node it is running on, and the Pod's assigned IP address at runtime -- without querying the Kubernetes API server. The sidecar needs these values as environment variables. Which Kubernetes mechanism allows exposing this Pod metadata directly to the container?

A) A ConfigMap that the CI/CD pipeline pre-populates with the Pod's expected name and namespace before deployment
B) The Downward API, which can inject Pod and container metadata as environment variables or volume files using `fieldRef` and `resourceFieldRef`
C) A sidecar container that runs `kubectl get pod` on startup and writes the output to a shared volume
D) Annotations on the Pod object that the application reads by querying the API server at startup

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Downward API allows containers to consume information about themselves and their Pod without coupling to the Kubernetes API server. Using `fieldRef` in the Pod spec's `env` section, you can expose fields such as `metadata.name`, `metadata.namespace`, `spec.nodeName`, and `status.podIP` as environment variables. You can also use `resourceFieldRef` to expose container resource requests and limits. This mechanism requires no RBAC permissions or API server access. Option A is fragile and does not work with dynamically generated Pod names. Option C creates unnecessary coupling to kubectl and requires RBAC. Option D requires API server access, which contradicts the requirement.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/downward-api/

</details>

---

### Question 38
[HARD]

An administrator places a Pod manifest file at `/etc/kubernetes/manifests/monitoring-agent.yaml` on a worker node. The kubelet creates the Pod, and it appears in `kubectl get pods` output. However, when the administrator tries to delete the Pod using `kubectl delete pod`, the Pod reappears shortly after. Why does this happen, and what type of Pod is this?

A) It is a DaemonSet-managed Pod, and the DaemonSet controller recreates it after deletion
B) It is a static Pod managed directly by the kubelet; the kubelet monitors the manifest directory and recreates the Pod whenever the file is present
C) It is a regular Pod with a restart policy of Always, which causes the kubelet to restart it after termination
D) It is managed by a ReplicaSet controller that detects the missing Pod and creates a replacement

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static Pods are managed directly by the kubelet on a specific node, without the API server or any controller managing them. The kubelet watches a configured directory (typically `/etc/kubernetes/manifests/`) for Pod manifest files and automatically creates the corresponding Pods. A mirror Pod is created in the API server so the Pod is visible via `kubectl`, but the API server cannot control static Pods. When you delete the mirror Pod via `kubectl`, the kubelet detects that the manifest file still exists and recreates the Pod. The only way to permanently remove a static Pod is to remove or rename the manifest file from the node's filesystem. This is fundamentally different from DaemonSet or ReplicaSet behavior, which operate through controllers on the control plane.

**Source:** https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/

</details>

---

### Question 39
[HARD]

A developer submits a request to create a Pod via `kubectl apply`. The request successfully passes authentication and RBAC authorization. However, the Pod is rejected before it is persisted to etcd. The error message indicates that the Pod does not meet the cluster's security standards. Which stage in the API request flow is most likely responsible for this rejection?

A) Authentication, which verifies the user's identity and can reject requests that do not meet security policies
B) Authorization (RBAC), which evaluates whether the user has permission to create Pods with certain security configurations
C) Admission control, which includes validating and mutating admission webhooks that enforce policies after authorization but before persistence
D) etcd validation, which rejects objects that do not conform to security schemas stored in the database

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The Kubernetes API request flow proceeds through authentication, authorization, and then admission control before the object is persisted to etcd. Admission controllers (both built-in and webhook-based) operate after a request is authenticated and authorized. Validating admission webhooks can enforce policies such as security standards, image registries, resource limits, and label requirements -- rejecting requests that violate organizational policies even when the user has RBAC permission to create the resource. In this scenario, the user passed authentication and authorization, so the rejection must come from the admission control stage. etcd does not perform policy validation; it stores whatever the API server sends it.

**Source:** https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/

</details>

---

### Question 40
[HARD]

A platform team wants to introduce a new resource type called `DatabaseCluster` into their Kubernetes cluster so that developers can declare database instances using `kubectl apply -f dbcluster.yaml`. The resource should be watchable, support CRUD operations through the standard API, and appear in `kubectl get` output. No modifications to the Kubernetes source code are allowed. Which approach should the team use?

A) Create a ConfigMap for each database instance and use labels to distinguish them as DatabaseCluster objects
B) Define a Custom Resource Definition (CRD) that registers the `DatabaseCluster` resource type with the Kubernetes API, then create Custom Resources conforming to that definition
C) Deploy a standalone REST API server outside the cluster that manages database instances and configure kubectl to proxy requests to it
D) Use Annotations on existing Deployment objects to store database configuration metadata, and query them via a custom CLI tool

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Custom Resource Definitions (CRDs) are the standard mechanism for extending the Kubernetes API with new resource types without modifying the Kubernetes source code. Once a CRD is registered, the API server dynamically serves the new resource type, supporting full CRUD operations, watch semantics, RBAC integration, and standard kubectl commands like `get`, `describe`, and `delete`. Custom Resources created from a CRD are stored in etcd alongside native Kubernetes objects and benefit from the same API machinery. Option A abuses ConfigMaps for a purpose they are not designed for and provides no schema validation. Option C works but does not integrate with the native Kubernetes API as required. CRDs are typically paired with custom controllers (operators) to add business logic.

**Source:** https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/

</details>
