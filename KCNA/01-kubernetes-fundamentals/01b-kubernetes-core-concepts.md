# Kubernetes Core Concepts - 100 MCQ Questions (Part B)

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Kubernetes Core Concepts
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

## Pods

### Question 1
[MEDIUM]

How do containers within the same Pod communicate with each other?

A) Through the Kubernetes API
B) Using localhost
C) Via a Service
D) Through environment variables

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Containers within the same Pod share the same network namespace, meaning they can communicate with each other using localhost and different ports. They don't need a Service or external networking to talk to each other.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 2
[MEDIUM-HARD]

Which of the following is NOT a valid Pod restart policy?

A) Always
B) OnFailure
C) Never
D) OnSuccess

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Kubernetes supports three restart policies: `Always` (default), `OnFailure`, and `Never`. There is no `OnSuccess` restart policy. `Always` restarts containers regardless of exit code, `OnFailure` only restarts on non-zero exit codes, and `Never` doesn't restart containers.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 3
[MEDIUM-HARD]

In a multi-container Pod, which resources are shared between containers?

A) CPU and memory limits only
B) Network namespace and storage volumes
C) Process namespace only
D) Nothing is shared between containers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Containers in the same Pod share the network namespace (same IP address, can use localhost) and can mount the same volumes. They do NOT share process namespaces by default (though this can be enabled), and each container has its own filesystem root.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 4
[MEDIUM-HARD]

What is the default restart policy for a Pod if not specified?

A) Never
B) OnFailure
C) Always
D) Unless-stopped

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The default restart policy for Pods is `Always`. This means if you don't explicitly set a restartPolicy, Kubernetes will automatically restart containers whenever they exit, regardless of the exit code.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 5
[MEDIUM-HARD]

What happens if an init container fails?

A) The Pod continues with app containers anyway
B) The init container is restarted until it succeeds (or Pod fails if restartPolicy: Never)
C) The Pod is immediately deleted
D) The failed init container is skipped

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If an init container fails, the kubelet restarts it until it succeeds. App containers don't start until all init containers complete. Exception: if the Pod has `restartPolicy: Never`, the entire Pod is marked as failed. Init containers don't have per-container restart policies—the Pod's policy determines behavior.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

---

### Question 6
[HARD]

What is the difference between resource requests and limits?

A) Requests are for CPU only, limits are for memory only
B) Requests guarantee minimum resources, limits cap maximum usage
C) Requests apply to Pods, limits apply to containers
D) There is no difference, they are aliases

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Resource requests specify the minimum resources a container needs and are used by the scheduler for placement decisions. Limits specify the maximum resources a container can use. If a container exceeds its memory limit, it may be OOM killed. If it exceeds CPU limit, it gets throttled.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 7
[MEDIUM-HARD]

What is the Pod lifecycle phase when all containers have terminated successfully?

A) Running
B) Completed
C) Succeeded
D) Terminated

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When all containers in a Pod have terminated with an exit code of 0 and will not be restarted, the Pod enters the `Succeeded` phase. This typically happens with Jobs or Pods with `restartPolicy: Never` or `OnFailure`.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 8
[MEDIUM-HARD]

What annotation is used to prevent a Pod from being evicted during node maintenance?

A) `pod.kubernetes.io/no-evict: "true"`
B) `scheduler.alpha.kubernetes.io/critical-pod`
C) There is no such annotation; use PodDisruptionBudget instead
D) `kubernetes.io/no-drain: "true"`

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** There is no annotation to prevent Pod eviction. To protect Pods during voluntary disruptions like node drains, you should use PodDisruptionBudgets (PDBs) which specify the minimum number of Pods that must remain available during disruptions.

**Source:** [Disruptions | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/)

</details>

---

### Question 9
[MEDIUM-HARD]

What happens when you delete a Pod managed by a Deployment?

A) The Pod is permanently deleted
B) The Deployment creates a new Pod to maintain the desired replica count
C) The Deployment is also deleted
D) The Pod enters a Terminating state indefinitely

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When you delete a Pod that's managed by a Deployment (via a ReplicaSet), the Deployment controller notices the replica count is below the desired state and creates a new Pod to replace it. This is the self-healing nature of Kubernetes.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 10
[MEDIUM-HARD]

Which field determines which node a Pod is scheduled on based on node labels?

A) `nodeName`
B) `nodeSelector`
C) `affinity`
D) Both B and C can be used

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Both `nodeSelector` and `affinity` can be used to influence Pod scheduling based on node labels. `nodeSelector` is simpler and requires exact label matches. `affinity` provides more expressive rules including soft preferences and anti-affinity.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 11
[HARD]

A Pod has `hostNetwork: true` set. What is the implication?

A) The Pod can only communicate with other Pods on the same node
B) The Pod uses the host's network namespace instead of its own
C) The Pod gets a dedicated network interface
D) Network policies don't apply to this Pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `hostNetwork: true`, the Pod uses the host node's network namespace directly. This means the Pod shares the host's IP address and can bind to host ports. This is useful for system daemons but reduces isolation and can cause port conflicts.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 12
[MEDIUM-HARD]

What is the purpose of a Pod's `serviceAccountName` field?

A) To specify which Service exposes the Pod
B) To define the identity used by the Pod for API authentication
C) To set the DNS name of the Pod
D) To specify resource accounting

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `serviceAccountName` field specifies which ServiceAccount identity the Pod uses for authenticating with the Kubernetes API. This determines what permissions the Pod has when making API calls. Token mounting is controlled by `automountServiceAccountToken` (tokens are now projected volumes, not auto-created Secrets).

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 13
[MEDIUM-HARD]

Which container probe checks if a container is ready to accept traffic?

A) livenessProbe
B) readinessProbe
C) startupProbe
D) healthProbe

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `readinessProbe` determines if a container is ready to accept traffic. When a readiness probe fails, the Pod's IP is removed from Service endpoints, stopping traffic from being routed to it. This is different from livenessProbe which determines if a container should be restarted.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 14
[HARD]

A container has both startupProbe and livenessProbe configured. When does the livenessProbe start running?

A) Immediately when the container starts
B) After the startupProbe succeeds
C) They run concurrently
D) After a fixed 10-second delay

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a startupProbe is configured, Kubernetes disables liveness and readiness probes until the startup probe succeeds. This is useful for slow-starting containers that might fail liveness checks during their initialization phase.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 15
[MEDIUM-HARD]

What is the default behavior when no readinessProbe is configured?

A) The container is never considered ready
B) The container is considered ready as soon as it starts
C) Kubernetes uses a default HTTP check on port 80
D) The container is considered ready after 30 seconds

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Without a readinessProbe, Kubernetes assumes the container is ready as soon as it starts. This means it will immediately receive traffic, which might cause errors if the application takes time to initialize. Always configure readiness probes for production workloads.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 16
[MEDIUM-HARD]

How can you view the events related to a specific Pod?

A) `kubectl events <pod>`
B) `kubectl describe pod <pod>`
C) `kubectl logs <pod> --events`
D) `kubectl get events --pod=<pod>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe pod <pod-name>` shows detailed information about a Pod including recent events at the bottom of the output. Events include scheduling decisions, image pulls, container starts/stops, and probe failures.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 17
[HARD]

Which of the following is true about Pod DNS?

A) Pod DNS records are optional and require DNS add-on configuration
B) Pods can only resolve Service DNS names
C) All Pods automatically get DNS records by default
D) Pods cannot have DNS names, only Services can

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Pod A/AAAA records are not created by default. They require enabling the `pods` option in CoreDNS configuration. When enabled, Pods get DNS records in the form `pod-ip-address.namespace.pod.cluster.local` (with dots replaced by dashes). Services always get DNS records; Pod records are optional.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 18
[MEDIUM]

Which field in the Pod spec sets environment variables for a container?

A) `spec.env`
B) `spec.containers[].env`
C) `spec.environment`
D) `metadata.env`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Environment variables are set in the container spec under `spec.containers[].env`. Each entry has a `name` and either a `value` or a `valueFrom` reference to get the value from a ConfigMap, Secret, or field reference.

**Source:** [Define Environment Variables for a Container | Kubernetes](https://kubernetes.io/docs/tasks/inject-data-application/define-environment-variable-container/)

</details>

---

### Question 19
[MEDIUM-HARD]

How do you force delete a Pod that's stuck in Terminating state?

A) `kubectl delete pod <pod> --force`
B) `kubectl delete pod <pod> --grace-period=0 --force`
C) `kubectl remove pod <pod>`
D) `kubectl terminate pod <pod>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To force delete a stuck Pod, use `kubectl delete pod <pod-name> --grace-period=0 --force`. This immediately removes the Pod from the API server without waiting for graceful termination. Use with caution as it may leave resources in an inconsistent state.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 20
[HARD]

What is a static Pod?

A) A Pod that cannot be scaled
B) A Pod managed directly by the kubelet without the API server
C) A Pod with no resource limits
D) A Pod that runs on all nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static Pods are managed directly by the kubelet on a specific node, without the API server. They're defined in manifest files in a directory watched by the kubelet (usually /etc/kubernetes/manifests). Control plane components like kube-apiserver often run as static Pods.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 21
[MEDIUM-HARD]

What is the purpose of `imagePullPolicy: IfNotPresent`?

A) Always pull the image from the registry
B) Only pull if the image doesn't exist locally
C) Never pull the image
D) Pull only if the image tag has changed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `IfNotPresent` means the kubelet only pulls the image if it's not already present on the node. This is the default for images with specific tags (not `latest`). It speeds up Pod startup when the image is already cached.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 22
[MEDIUM-HARD]

How can you specify that a Pod should only run on nodes with SSD storage?

A) Use a `nodeSelector` matching a label like `disk=ssd`
B) Set `storageType: ssd` in the Pod spec
C) Use a PersistentVolumeClaim with SSD requirements
D) Configure the scheduler with SSD preferences

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Use `nodeSelector` in the Pod spec with a label selector like `disk: ssd`. The nodes must be labeled appropriately (e.g., `kubectl label node <node> disk=ssd`). The scheduler will only place the Pod on nodes matching the selector.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 23
[HARD]

A Pod has `priorityClassName: high-priority` set. What does this affect?

A) CPU scheduling within the node
B) Order of image pulls
C) Pod scheduling order and preemption
D) Network traffic priority

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** PriorityClass affects Pod scheduling order (higher priority Pods are scheduled first) and preemption (higher priority Pods can evict lower priority Pods when resources are scarce). It doesn't affect CPU scheduling or network priority within the cluster.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 24
[HARD]

What is the purpose of `topologySpreadConstraints` in a Pod spec?

A) To define network topology for the Pod
B) To control how Pods are distributed across topology domains
C) To set storage replication topology
D) To configure DNS topology

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `topologySpreadConstraints` control how Pods are spread across topology domains (like zones, nodes, or regions) to achieve high availability. You can specify maximum skew (allowed imbalance) and how to handle unsatisfiable constraints.

**Source:** [Pod Topology Spread Constraints | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)

</details>

---

### Question 25
[HARD]

A Pod has both `nodeName` and `nodeSelector` specified. What happens?

A) `nodeSelector` takes precedence
B) `nodeName` takes precedence, bypassing the scheduler
C) The Pod fails validation
D) Both constraints must be satisfied

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When `nodeName` is specified, it bypasses the scheduler entirely and binds the Pod directly to that node. The `nodeSelector` is effectively ignored because the scheduler isn't involved. The kubelet on the named node will run the Pod if possible.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

## Deployments & ReplicaSets

### Question 26
[MEDIUM]

How does a Deployment manage Pods?

A) Directly creates and manages Pods
B) Creates ReplicaSets which then manage Pods
C) Uses DaemonSets to manage Pods
D) Relies on the scheduler to create Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deployments don't directly manage Pods. Instead, they create and manage ReplicaSets, which in turn create and manage Pods. This layered approach allows Deployments to maintain history (old ReplicaSets) for rollbacks.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 27
[MEDIUM-HARD]

What does `maxSurge` control in a rolling update?

A) Maximum number of Pods that can be unavailable
B) Maximum number of extra Pods that can be created above desired count
C) Maximum time for the update to complete
D) Maximum number of rollback versions kept

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `maxSurge` specifies how many extra Pods (above the desired replica count) can be created during a rolling update. It can be an absolute number or percentage. For example, with 10 replicas and maxSurge=2, up to 12 Pods can exist during the update.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 28
[HARD]

A Deployment has 10 replicas, maxSurge=25%, maxUnavailable=25%. During an update, what's the maximum and minimum number of Pods?

A) Max: 12, Min: 8
B) Max: 13, Min: 7
C) Max: 12, Min: 7
D) Max: 13, Min: 8

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** With 10 replicas: maxSurge=25% rounds up to 3 (max 13 Pods), maxUnavailable=25% rounds down to 2 (min 8 Pods). Kubernetes rounds up surge and rounds down unavailable to ensure availability. So maximum is 13 Pods, minimum is 8 Pods.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 29
[MEDIUM-HARD]

What happens to old ReplicaSets after a successful Deployment update?

A) They are immediately deleted
B) They are scaled to 0 but retained for rollback
C) They continue running alongside new Pods
D) They are archived to etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Old ReplicaSets are scaled to 0 replicas but retained in the cluster. This allows rollbacks to previous versions. The number of retained ReplicaSets is controlled by `revisionHistoryLimit` (default 10).

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 30
[MEDIUM-HARD]

How do you check the status of a Deployment rollout?

A) `kubectl get deployment <name>`
B) `kubectl rollout status deployment <name>`
C) `kubectl describe deployment <name>`
D) All of the above provide rollout information

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** All three commands provide rollout information. `kubectl rollout status` specifically watches the rollout progress. `kubectl get deployment` shows ready/desired replicas. `kubectl describe deployment` shows detailed status including conditions and events.

**Source:** [kubectl rollout | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

</details>

---

### Question 31
[MEDIUM-HARD]

What command pauses a Deployment rollout?

A) `kubectl rollout stop deployment <name>`
B) `kubectl rollout pause deployment <name>`
C) `kubectl deployment pause <name>`
D) `kubectl pause deployment <name>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl rollout pause deployment <name>` pauses the rollout, allowing you to make multiple changes without triggering multiple rollouts. Resume with `kubectl rollout resume deployment <name>`.

**Source:** [kubectl rollout | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

</details>

---

### Question 32
[MEDIUM-HARD]

How does a ReplicaSet identify which Pods it manages?

A) By Pod names
B) By label selectors matching Pod labels
C) By namespace only
D) By IP addresses

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ReplicaSets use label selectors to identify Pods they manage. Pods with labels matching the selector are considered part of the ReplicaSet. This is why changing Pod labels can cause them to be orphaned or adopted by different ReplicaSets.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 33
[MEDIUM-HARD]

What is the relationship between a Deployment's selector and its Pod template labels?

A) They can be completely different
B) The selector must match the Pod template labels
C) The selector automatically copies from Pod template
D) Only the selector matters, Pod labels are ignored

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Deployment's selector must match the Pod template's labels. The API server validates this—if they don't match, the Deployment creation fails. This ensures the Deployment can find and manage the Pods it creates.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 34
[HARD]

What is the `revisionHistoryLimit` field used for?

A) Maximum number of ReplicaSets to retain for rollback
B) Maximum number of rollouts per day
C) Maximum revision number
D) Limit on history stored in etcd

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `revisionHistoryLimit` specifies how many old ReplicaSets to retain for rollback purposes. The default is 10. Setting it to 0 means no rollback history is kept, and old ReplicaSets are garbage collected immediately.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 35
[MEDIUM-HARD]

What does `kubectl rollout history deployment <name>` show?

A) All changes ever made to the Deployment
B) List of revision numbers and change causes
C) Git-like commit history
D) Resource usage history

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl rollout history` shows revision numbers for the Deployment along with the `CHANGE-CAUSE` annotation if set. To see details of a specific revision, add `--revision=<number>`. This helps identify which version to roll back to.

**Source:** [kubectl rollout | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

</details>

---

### Question 36
[MEDIUM-HARD]

What is the Recreate deployment strategy?

A) Gradually replaces Pods one at a time
B) Terminates all existing Pods before creating new ones
C) Creates new Pods in a separate namespace
D) Maintains two full sets of Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `Recreate` strategy terminates all existing Pods before creating any new ones. This causes downtime but ensures the old and new versions never run simultaneously. Use this when your application can't handle multiple versions running concurrently.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 37
[HARD]

A Deployment has `.spec.selector` that matches Pods created by another Deployment. What happens?

A) Both Deployments share the Pods
B) The second Deployment fails to create
C) Both Deployments fight over the Pods, causing instability
D) The API server rejects one Deployment

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** If two Deployments have overlapping selectors, they'll both try to manage the same Pods, causing unpredictable behavior. Each will scale up/down based on its desired state, potentially causing Pods to be constantly created and deleted. Always use unique selectors.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 38
[HARD]

What happens during a failed rollout when `progressDeadlineSeconds` is exceeded?

A) The Deployment automatically rolls back
B) The Deployment is marked failed; no auto-rollback; manual intervention required
C) All Pods are terminated
D) The Deployment is deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When `progressDeadlineSeconds` is exceeded, the Deployment's condition is set to `Progressing=False` with reason `ProgressDeadlineExceeded`. Kubernetes takes no further action—it does NOT automatically roll back. The stalled state persists until you intervene by fixing the issue, rolling back manually, or updating the spec to trigger a new rollout.

**Source:** [Deployments - Progress Deadline | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#progress-deadline-seconds)

</details>

---

### Question 39
[MEDIUM-HARD]

What is the purpose of a ReplicaSet's `replicas` field?

A) Maximum number of Pods allowed
B) Exact number of Pod replicas desired
C) Minimum number of Pods required
D) Number of nodes to schedule on

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `replicas` field specifies the exact number of Pod replicas the ReplicaSet should maintain. The ReplicaSet controller continuously reconciles the actual number of Pods with this desired count, creating or deleting Pods as needed.

**Source:** [ReplicaSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

</details>

---

### Question 40
[MEDIUM-HARD]

What happens when you delete a Deployment?

A) Only the Deployment object is deleted
B) The Deployment and its ReplicaSets are deleted, but not Pods
C) The Deployment, its ReplicaSets, and their Pods are all deleted
D) Nothing is deleted until you confirm

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Deleting a Deployment cascades to delete its ReplicaSets, which in turn delete their Pods. This is the default cascade delete behavior. Use `--cascade=orphan` to delete only the Deployment while keeping ReplicaSets and Pods.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 41
[MEDIUM-HARD]

What command restarts all Pods in a Deployment without changing the container image?

A) `kubectl restart deployment <name>`
B) `kubectl rollout restart deployment <name>`
C) `kubectl delete pods` with selector
D) `kubectl apply --force`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl rollout restart` triggers a rolling restart by patching the Pod template with a restart annotation. This restarts all Pods without changing the container image. Note: it does modify the Deployment spec (adds an annotation), but the application configuration remains unchanged.

**Source:** [kubectl rollout | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

</details>

---

### Question 42
[HARD]

You have a Deployment with 3 replicas. After updating, you notice 4 ReplicaSets. Why?

A) An error occurred during rollout
B) You performed 3 updates, and revisionHistoryLimit allows keeping old ReplicaSets
C) The Deployment was paused mid-update
D) There's always one extra ReplicaSet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Each update creates a new ReplicaSet (or reuses one if identical to a previous version). With 3 updates from the initial state, you'd have 4 ReplicaSets: the original plus 3 updates. Old ReplicaSets are scaled to 0 but retained for rollback.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 43
[HARD]

What's the difference between scaling a Deployment and updating its replica count in the manifest?

A) No difference
B) Scaling is temporary, manifest changes are permanent
C) Both change the same field, but manifest changes may be tracked in version control
D) Scaling triggers a rollout, manifest changes don't

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Both `kubectl scale` and editing the manifest update `.spec.replicas`. The difference is operational—manifest changes in version control provide an audit trail and can be applied declaratively. Neither triggers a rollout since scaling doesn't change the Pod template.

**Source:** [kubectl scale | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/)

</details>

---

### Question 44
[MEDIUM-HARD]

What is the purpose of `.spec.selector.matchExpressions` in a ReplicaSet?

A) To select nodes for scheduling
B) To define complex Pod selection criteria with operators
C) To match container images
D) To express resource requirements

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `matchExpressions` allows complex label selection using operators like `In`, `NotIn`, `Exists`, and `DoesNotExist`. This is more flexible than `matchLabels` which only supports equality. For example: select Pods where `env` is either `prod` or `staging`.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 45
[MEDIUM-HARD]

How do you check which ReplicaSet is currently active for a Deployment?

A) The one with non-zero replicas
B) The one with the highest revision number
C) Check `kubectl describe deployment`
D) All of the above

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** All these methods work. The active ReplicaSet has non-zero replicas and the highest revision number. `kubectl describe deployment` shows the current ReplicaSet under "NewReplicaSet". Old ReplicaSets are scaled to 0 but may still exist.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 46
[MEDIUM-HARD]

What is the significance of the `generation` field in a Deployment?

A) The total number of Pods created
B) A counter that increments when the spec changes
C) The Kubernetes API version
D) The age of the Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `generation` field in metadata increments whenever the Deployment's spec changes. This is used by controllers and tools to detect changes. The `observedGeneration` in status shows the last generation the controller acted on.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 47
[HARD]

What is proportional scaling in Deployments?

A) Scaling Pods proportionally across nodes
B) Distributing additional replicas across old and new ReplicaSets during rollout
C) Scaling based on CPU utilization
D) Keeping Pod sizes proportional

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** During a rolling update, if you scale the Deployment, Kubernetes distributes the additional replicas proportionally across active ReplicaSets. This maintains the rollout ratio rather than adding all new replicas to just the old or new ReplicaSet.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 48
[HARD]

A Deployment shows `AVAILABLE: 3` but `READY: 3/5`. What does this indicate?

A) 3 Pods are available and ready out of 5 desired
B) 3 Pods have passed minReadySeconds, 3 Pods are passing readiness probe
C) The numbers should always match; this indicates an error
D) 3 Pods are available, 5 were attempted

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `READY` shows how many Pods are passing their readiness probe out of the desired count. `AVAILABLE` shows Pods that have been ready for at least `minReadySeconds`. During rollouts or with failing Pods, these numbers can differ.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 49
[HARD]

You want exactly 5 Pods running at all times during a rollout. What should you set?

A) `maxSurge: 0, maxUnavailable: 0` (invalid)
B) `maxSurge: 5, maxUnavailable: 0`
C) `maxSurge: 0, maxUnavailable: 5`
D) `replicas: 5, minAvailable: 5`

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Setting both `maxSurge: 0` and `maxUnavailable: 0` is invalid—it would prevent any change. To always have exactly 5 Pods, you'd need `maxSurge: 0, maxUnavailable: 0` which is rejected. The closest option is `maxSurge: 1+, maxUnavailable: 0` allowing temporary increase.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 50
[HARD]

Why does Kubernetes add the `pod-template-hash` label automatically?

A) For metrics collection
B) To prevent different ReplicaSets from adopting each other's Pods
C) For logging purposes
D) To enable horizontal pod autoscaling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `pod-template-hash` ensures ReplicaSets don't accidentally adopt Pods from other ReplicaSets (even within the same Deployment). Without it, ReplicaSets with the same selector could fight over Pods. The hash makes each ReplicaSet's selector unique.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

## Services

### Question 51
[MEDIUM]

Which Service type is only accessible from within the cluster?

A) NodePort
B) LoadBalancer
C) ClusterIP
D) ExternalName

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** ClusterIP (the default type) creates an internal IP that's only reachable from within the cluster. NodePort and LoadBalancer expose Services externally. ExternalName provides DNS aliasing without creating a cluster IP.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 52
[MEDIUM-HARD]

How does a Service discover which Pods to route traffic to?

A) By Pod names
B) By Pod IP addresses
C) By label selectors matching Pod labels
D) By namespace only

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Services use label selectors to identify backend Pods. Pods with labels matching the Service's selector become endpoints. The Endpoints object (automatically managed) contains the IPs of all matching Pods.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 53
[HARD]

What is a headless Service?

A) A Service without a selector
B) A Service with `clusterIP: None`
C) A Service without any Pods
D) A Service that doesn't use DNS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A headless Service has `clusterIP: None`. Instead of load-balancing through a single IP, DNS queries return the IPs of all individual Pods. This is useful for stateful applications where clients need to connect to specific Pods or discover all endpoints.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#headless-services)

</details>

---

### Question 54
[MEDIUM-HARD]

What is the DNS name format for a Service in Kubernetes?

A) `<service>.<namespace>`
B) `<service>.<namespace>.svc.cluster.local`
C) `<service>.cluster.local`
D) `<namespace>.<service>.svc`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The full DNS name is `<service-name>.<namespace>.svc.cluster.local`. Within the same namespace, you can use just `<service-name>`. Across namespaces, use `<service-name>.<namespace>` or the full name.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 55
[MEDIUM-HARD]

What happens when all Pods matching a Service selector become unavailable?

A) The Service is automatically deleted
B) The Service returns errors to clients
C) Traffic is queued until Pods return
D) The Endpoints object becomes empty, connections fail

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** When no Pods match the selector, the Endpoints object becomes empty. New connection attempts fail (connection refused or timeout). The Service itself remains; it just has no backends to route to. Existing connections may hang until timeout.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 56
[HARD]

What is the purpose of ExternalName Service type?

A) To expose internal services externally
B) To create a DNS CNAME alias to an external service
C) To assign external IPs to Pods
D) To load balance external traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ExternalName Services don't proxy traffic or select Pods. Instead, they create a DNS CNAME record pointing to an external hostname. When you resolve `myservice.namespace.svc.cluster.local`, you get the external hostname back.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 57
[MEDIUM-HARD]

What is the Endpoints object in Kubernetes?

A) A way to define API endpoints
B) An object containing IP addresses of Pods selected by a Service
C) Network policy endpoints
D) External service endpoints only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Endpoints is an object that lists the IP addresses and ports of Pods selected by a Service. It's automatically created and managed when a Service has a selector. For Services without selectors, you can manually create Endpoints to point to external services.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 58
[MEDIUM-HARD]

What happens when you create a LoadBalancer Service in a cluster without cloud provider integration?

A) The Service is rejected by the API server
B) The Service stays in Pending state for EXTERNAL-IP
C) It automatically falls back to NodePort only
D) An error is logged and the Service is deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Without a cloud provider or load balancer controller (like MetalLB), LoadBalancer Services remain in Pending state indefinitely—the EXTERNAL-IP never gets assigned. The Service still works as a NodePort/ClusterIP, but no external load balancer is provisioned.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

</details>

---

### Question 59
[HARD]

What happens with `externalTrafficPolicy: Local` if a node has no matching Pods?

A) Traffic is forwarded to another node
B) Traffic is dropped (connection refused)
C) The node is removed from the load balancer
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** With `externalTrafficPolicy: Local`, nodes without matching Pods fail the load balancer health check and are removed from rotation. If traffic somehow reaches such a node, it's dropped. This is important to consider for Pod distribution.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 60
[MEDIUM-HARD]

What is the purpose of `publishNotReadyAddresses: true` in a Service?

A) To publish the Service before it's ready
B) To include unready Pod IPs in Endpoints (and thus headless Service DNS)
C) To expose unready nodes
D) To disable readiness checks

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `publishNotReadyAddresses: true`, unready Pod IPs are included in Endpoints/EndpointSlices even if readiness probes fail. For headless Services, this means DNS records include unready Pods. This is useful for StatefulSets where Pods need to discover each other during initialization before they're fully ready.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 61
[MEDIUM-HARD]

How can a Pod discover a Service's ClusterIP?

A) Through environment variables injected by Kubernetes
B) Through DNS resolution
C) Through the Kubernetes API
D) All of the above

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Services can be discovered via: (1) environment variables like `<SERVICE>_SERVICE_HOST` and `<SERVICE>_SERVICE_PORT` (injected at Pod start), (2) DNS lookup of `<service>.<namespace>`, or (3) API queries. DNS is most common and flexible.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 62
[MEDIUM-HARD]

What protocol does a Service use by default?

A) HTTP
B) TCP
C) UDP
D) HTTPS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Services default to TCP protocol. To use UDP, set `spec.ports[].protocol: UDP`. Services can have multiple ports with different protocols. gRPC and HTTP work over TCP at the Service level.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 63
[HARD]

How do you create a Service that load balances across Pods in multiple namespaces?

A) Use cross-namespace selectors
B) Create a Service without selector and manually manage Endpoints
C) It's not possible, Services are namespace-scoped
D) Use a Federation Service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Services can't select Pods across namespaces. To achieve cross-namespace load balancing, create a selector-less Service and manually create/manage Endpoints pointing to Pod IPs in other namespaces. Or use an Ingress or service mesh.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 64
[HARD]

What is EndpointSlice and why was it introduced?

A) A way to slice network traffic
B) A scalable replacement for Endpoints with better performance
C) A method to distribute endpoints across zones
D) A security feature for endpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** EndpointSlices are a more scalable way to track network endpoints. Unlike Endpoints (single object per Service), EndpointSlices split endpoints across multiple smaller objects. This improves performance for Services with many endpoints by reducing etcd and network overhead.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 65
[HARD]

What is the difference between iptables and IPVS mode for kube-proxy?

A) IPVS only works on Linux
B) IPVS offers better performance and more load balancing algorithms
C) iptables supports UDP, IPVS doesn't
D) They're identical in functionality

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** IPVS mode offers better performance for clusters with many Services (O(1) vs O(n) for iptables rule matching). It also provides more load balancing algorithms (round-robin, least-connections, etc.). iptables mode uses random distribution.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 66
[HARD]

A Service has `internalTrafficPolicy: Local`. What does this mean?

A) External traffic uses local routing
B) Internal cluster traffic only routes to Pods on the same node
C) The Service is only accessible locally
D) Traffic stays within the same zone

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `internalTrafficPolicy: Local` makes internal traffic (from within the cluster) route only to Pods on the same node as the client. This can reduce latency and cross-node traffic. If no local Pods exist, the request fails.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 67
[MEDIUM-HARD]

When must Service ports have names?

A) Always
B) When there are multiple ports defined
C) Never, names are optional
D) Only for NodePort Services

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Port names are optional when a Service has only one port. When multiple ports are defined, each must have a unique name. These names are also used by EndpointSlices and are required for some features like service meshes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 68
[MEDIUM-HARD]

What is the topology-aware routing feature in Services?

A) Routing based on network topology hints
B) Preferring endpoints in the same zone to reduce latency
C) DNS-based geographic routing
D) Both A and B

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Topology-aware routing (topology hints) enables Services to prefer endpoints in the same zone as the client. This reduces cross-zone traffic and latency.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 69
[MEDIUM-HARD]

How do you test Service connectivity from within the cluster?

A) Use a test Pod to curl or wget the Service
B) Check Service endpoints with kubectl
C) Use `kubectl port-forward` from your local machine
D) Run `kubectl describe service`

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** To test actual in-cluster connectivity, make a network request from inside the cluster using a test Pod (e.g., `kubectl run tmp --rm -it --image=busybox -- wget <service>`). Checking endpoints or describing Services only verifies configuration, not actual network connectivity. `kubectl port-forward` tunnels via the API server—useful for local debugging but doesn't test in-cluster networking.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 70
[HARD]

You want traffic to only go to Pods that have been running for at least 30 seconds. How do you achieve this?

A) Set `minReadySeconds: 30` on the Service
B) Set `minReadySeconds: 30` on the Deployment
C) Use a readiness probe with `initialDelaySeconds: 30`
D) Both B and C work

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Services route traffic based solely on readiness probe status—not `minReadySeconds`. The `minReadySeconds` field on Deployments controls when a Pod is counted as "available" for rollout purposes, not Service traffic. To delay Service traffic, use a readiness probe with `initialDelaySeconds: 30` so the Pod isn't marked ready until the delay passes.

**Source:** [Deployment | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

## ConfigMaps & Secrets

### Question 71
[MEDIUM]

How can a Pod consume data from a ConfigMap?

A) As environment variables
B) As files in a mounted volume
C) As command-line arguments
D) All of the above

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** ConfigMaps can be consumed as: (1) environment variables via `envFrom` or `env.valueFrom`, (2) files by mounting as a volume, or (3) command arguments by referencing environment variables set from the ConfigMap.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 72
[MEDIUM-HARD]

How do you create a ConfigMap from a file?

A) `kubectl create configmap my-config --from-file=config.properties`
B) `kubectl apply -f config.properties`
C) `kubectl import configmap config.properties`
D) `kubectl create configmap my-config < config.properties`

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Use `kubectl create configmap <name> --from-file=<path>` to create a ConfigMap from a file. The filename becomes the key, file contents become the value. Use `--from-file=<key>=<path>` to specify a custom key name.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 73
[HARD]

Why might ConfigMap updates not be reflected when using `subPath` mount?

A) `subPath` is read-only
B) `subPath` mounts a snapshot, not a symbolic link
C) `subPath` doesn't support ConfigMaps
D) It's a bug

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When using `subPath`, Kubernetes mounts the file directly rather than using symbolic links. This means the Pod sees a snapshot at mount time, and updates to the ConfigMap aren't reflected. Use full volume mounts for automatic updates.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 74
[MEDIUM-HARD]

How do ServiceAccounts obtain tokens in Kubernetes 1.24+?

A) Secrets are automatically created with long-lived tokens
B) Via TokenRequest API and projected volumes (no auto-created Secret)
C) Manual token creation is required
D) Tokens are stored in ConfigMaps

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Since Kubernetes 1.24, ServiceAccount tokens are no longer automatically created as Secrets. Instead, bound tokens are obtained via the TokenRequest API and mounted as projected volumes. These tokens are short-lived and automatically rotated. Legacy `kubernetes.io/service-account-token` Secrets can still be manually created if needed.

**Source:** [Service Account Token Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#service-account-token-secrets)

</details>

---

### Question 75
[MEDIUM-HARD]

How do you decode a base64-encoded value from a Secret?

A) `kubectl get secret <name> -o jsonpath='{.data.key}' | base64 -d`
B) `kubectl describe secret <name>`
C) `kubectl get secret <name> --decode`
D) Secrets are automatically decoded when retrieved

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Secret data is stored base64-encoded. Use `kubectl get secret <name> -o jsonpath='{.data.<key>}' | base64 -d` to decode. Or use `-o go-template='{{.data.<key> | base64decode}}'`. `kubectl describe` shows keys but not values.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 76
[HARD]

What happens when a Pod references a non-existent ConfigMap?

A) The Pod starts with empty values
B) The Pod fails to start with an error
C) Depends on whether the reference is `optional`
D) The ConfigMap is automatically created

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** By default, referencing a non-existent ConfigMap causes Pod startup to fail. You can set `optional: true` in `configMapRef` or `configMapKeyRef` to allow the Pod to start anyway, treating the reference as empty.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 77
[MEDIUM-HARD]

What is the difference between `envFrom` and `env` with `valueFrom`?

A) No difference
B) `envFrom` imports all keys, `env` with `valueFrom` imports specific keys
C) `envFrom` is for Secrets only
D) `env` with `valueFrom` is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `envFrom` imports all keys from a ConfigMap or Secret as environment variables. `env` with `valueFrom` lets you select specific keys and optionally rename them. Use `envFrom` for bulk import, `env` for selective import.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 78
[MEDIUM-HARD]

How do you mount only specific keys from a ConfigMap?

A) Use `items` in the volume configuration
B) Use `keys` selector
C) Create separate ConfigMaps
D) It's not possible

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Use the `items` field in the ConfigMap volume to specify which keys to mount and their paths. Each item specifies a `key` from the ConfigMap and a `path` where it should appear in the volume.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 79
[MEDIUM-HARD]

What type of Secret is used for Docker registry credentials?

A) `Opaque`
B) `kubernetes.io/dockerconfigjson`
C) `kubernetes.io/tls`
D) `kubernetes.io/basic-auth`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubernetes.io/dockerconfigjson` Secrets store Docker registry credentials. Create with `kubectl create secret docker-registry <name> --docker-server=<url> --docker-username=<user> --docker-password=<pass>`. Reference in `imagePullSecrets`.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 80
[HARD]

What is the difference between `stringData` and `data` in a Secret manifest?

A) `stringData` is for strings, `data` is for binary
B) `stringData` accepts plain text, `data` requires base64
C) They're aliases
D) `stringData` is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `stringData` accepts plain text values (convenient for manifests), `data` requires base64-encoded values. When you apply a manifest with `stringData`, Kubernetes converts it to base64 and stores in `data`. You can use both in the same manifest.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 81
[HARD]

A Pod uses `envFrom` to load a ConfigMap. The ConfigMap has a key with an invalid environment variable name (e.g., `my-key`). What happens?

A) The Pod fails to start
B) The key is skipped with a warning event
C) The key is renamed automatically
D) The Pod starts but crashes at runtime

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Keys that can't be used as environment variable names (containing hyphens, starting with digits, etc.) are skipped, and a warning event is generated. The Pod starts successfully with the valid keys. Use `env` with `valueFrom` to explicitly map invalid keys to valid environment variable names.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 82
[HARD]

You want to trigger a Pod restart when a ConfigMap changes. What's a common approach?

A) Kubernetes automatically restarts Pods
B) Use a hash of ConfigMap content in Pod annotations
C) Set `restartOnConfigChange: true`
D) This is not possible

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes doesn't auto-restart Pods on ConfigMap changes. A common pattern is adding an annotation with a hash of ConfigMap content (e.g., `checksum/config: <sha256>`). Tools like Helm support this. When ConfigMap changes, the annotation changes, triggering a rollout.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 83
[HARD]

What is the recommended practice for managing Secrets in production?

A) Store them in Git alongside other manifests
B) Use external secret management (Vault, AWS Secrets Manager) with operators
C) Encode them in base64 for security
D) Store them as ConfigMaps since they're not really different

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Best practice is using external secret management systems (HashiCorp Vault, AWS Secrets Manager, etc.) with Kubernetes operators or CSI drivers. Never store secrets in Git. Base64 is encoding, not encryption. Enable encryption at rest and RBAC.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 84
[HARD]

What is a projected volume, and how does it relate to ConfigMaps?

A) A volume that projects multiple sources (ConfigMaps, Secrets, etc.) into one directory
B) A read-only ConfigMap volume
C) A volume that projects to multiple Pods
D) A temporary ConfigMap storage

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Projected volumes combine multiple volume sources (ConfigMaps, Secrets, ServiceAccount tokens, downwardAPI) into a single mount point. This is useful when you need data from multiple sources in the same directory without multiple mounts.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 85
[HARD]

What happens when you delete a ConfigMap that's in use by a running Pod?

A) The Pod is terminated
B) The Pod continues running but loses the ConfigMap data immediately
C) Env vars remain; volume-mounted files are eventually removed after kubelet sync
D) The delete is blocked

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Deleting a ConfigMap doesn't terminate running Pods. Environment variables were copied at Pod start and remain unchanged. Volume-mounted ConfigMap data is eventually updated (emptied) when the kubelet syncs—this isn't immediate but happens after a sync delay. New Pods trying to use the deleted ConfigMap will fail to start.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

## Namespaces, Labels & Selectors

### Question 86
[MEDIUM]

Which resources are NOT namespaced in Kubernetes?

A) Pods and Services
B) Nodes and PersistentVolumes
C) ConfigMaps and Secrets
D) Deployments and ReplicaSets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Nodes, PersistentVolumes, Namespaces themselves, ClusterRoles, and ClusterRoleBindings are cluster-scoped (not namespaced). Most other resources (Pods, Services, ConfigMaps, Deployments, etc.) are namespaced.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 87
[MEDIUM-HARD]

What happens when you deploy a resource without specifying a namespace?

A) The deployment fails
B) It goes to the `default` namespace
C) It creates a new namespace
D) It becomes cluster-scoped

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Resources deployed without an explicit namespace go to `default`. You can change the default namespace for kubectl with `kubectl config set-context --current --namespace=<name>` or specify `-n <namespace>` per command.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 88
[MEDIUM-HARD]

What is the purpose of labels in Kubernetes?

A) To name resources
B) To attach identifying metadata for organization and selection
C) To set resource limits
D) To enable logging

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Labels are key-value pairs attached to objects for identification and grouping. They're used by selectors (in Services, Deployments, etc.) to find matching resources. Unlike annotations, labels are meant to be used for selection and filtering.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 89
[MEDIUM-HARD]

Which selector type uses operators like `In`, `NotIn`, `Exists`?

A) Equality-based selectors
B) Set-based selectors
C) Both types support these operators
D) Field selectors

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Set-based selectors use operators: `In`, `NotIn`, `Exists`, `DoesNotExist`. They're more expressive than equality-based selectors (which only use `=`, `==`, `!=`). Use `matchExpressions` for set-based selection in resources like Deployments.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 90
[HARD]

What does the selector `app notin (test, dev)` match?

A) Pods where app is either test or dev
B) Pods where app is neither test nor dev (including Pods without the app label)
C) Pods where app exists and is neither test nor dev
D) It's invalid syntax

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** `NotIn` requires the label key to exist—it matches resources where the key exists AND the value is not in the specified set. Pods without the `app` label are NOT matched. To include resources without the key, use `DoesNotExist` or combine selectors.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#set-based-requirement)

</details>

---

### Question 91
[MEDIUM-HARD]

What is a recommended label for identifying the application name?

A) `name`
B) `app.kubernetes.io/name`
C) `application`
D) `app`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes recommends using labels from the `app.kubernetes.io/` prefix for standardization. `app.kubernetes.io/name` is for the application name. Others include `app.kubernetes.io/instance`, `app.kubernetes.io/version`, `app.kubernetes.io/component`, etc.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 92
[MEDIUM-HARD]

How do you delete all Pods with a specific label?

A) `kubectl delete pods --all -l app=test`
B) `kubectl delete pods -l app=test`
C) `kubectl remove pods --label app=test`
D) `kubectl delete pods --selector app:test`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl delete pods -l app=test` to delete all Pods matching the label selector. The `-l` or `--selector` flag filters which resources to delete. Be careful—this immediately deletes all matching Pods.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 93
[MEDIUM-HARD]

What is the purpose of `kubernetes.io/metadata.name` label on Namespaces?

A) To name the namespace
B) To enable namespace-based NetworkPolicies
C) To identify system namespaces
D) It's automatically added with the namespace name as value

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Kubernetes automatically adds the `kubernetes.io/metadata.name` label to all namespaces with the namespace name as the value. This enables namespace-based selection in NetworkPolicies and other selectors without needing to manually add labels.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 94
[HARD]

What is a LimitRange used for in a namespace?

A) To limit the number of namespaces
B) To set default and maximum resource limits for containers in a namespace
C) To limit network traffic
D) To restrict API access

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LimitRange sets default, minimum, and maximum resource constraints for containers, Pods, and PVCs in a namespace. If a Pod doesn't specify resources, LimitRange defaults are applied. Requests exceeding max limits are rejected.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 95
[MEDIUM-HARD]

Can you nest namespaces in Kubernetes?

A) Yes, using parent-child relationships
B) No, namespaces are flat with no hierarchy
C) Yes, by setting a parent namespace field
D) Yes, namespaces automatically inherit from default

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes namespaces are flat—there is no native support for hierarchy or parent-child relationships. All namespaces exist at the same level. You cannot nest one namespace inside another or establish inheritance between namespaces in core Kubernetes.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 96
[MEDIUM-HARD]

How do you select resources with a label key that exists but exclude specific values?

A) Use `NotIn` alone (it requires the key to exist)
B) Use `DoesNotExist`
C) This isn't possible
D) Use `Exists` combined with `NotIn`

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `NotIn` already requires the label key to exist—it matches resources where the key exists AND the value is not in the specified set. Adding `Exists` is redundant for this use case. To match resources WITHOUT the key, you would use `DoesNotExist` instead.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#set-based-requirement)

</details>

---

### Question 97
[HARD]

What is the field selector `status.phase=Running` used for?

A) To filter Pods by their phase using kubectl
B) To set the Pod phase
C) To create running Pods only
D) Field selectors don't exist

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Field selectors filter resources by field values (not labels). `kubectl get pods --field-selector status.phase=Running` lists only running Pods. Limited fields are supported—commonly: `metadata.name`, `metadata.namespace`, `status.phase`.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 98
[HARD]

What happens when you delete a namespace?

A) Only the namespace object is deleted
B) All resources in the namespace are deleted
C) Resources are moved to default namespace
D) The delete is blocked if resources exist

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deleting a namespace cascades to delete ALL resources within it—Pods, Services, Deployments, ConfigMaps, Secrets, everything. This is why namespace deletion should be done carefully. The namespace stays in "Terminating" status until all resources are cleaned up.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 99
[HARD]

What is the purpose of `finalizers` on a namespace?

A) To prevent immediate deletion until cleanup is done
B) To finalize the namespace configuration
C) To mark the namespace as complete
D) To prevent any changes to the namespace

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Finalizers are strings that prevent resource deletion until controllers remove them. Namespaces have a `kubernetes` finalizer that ensures all namespaced resources are deleted before the namespace itself is removed. Stuck finalizers can cause namespaces to hang in "Terminating".

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 100
[HARD]

A namespace is stuck in "Terminating" state. What is the likely cause?

A) Network issues
B) Resources with finalizers that can't be removed
C) Insufficient permissions
D) etcd is full

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A stuck "Terminating" namespace usually has resources with finalizers that controllers can't clear—often due to webhooks being unavailable, CRD controllers being deleted before resources, or orphaned resources. Check remaining resources and finalizers to diagnose.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

# Summary

**Total Questions:** 200
**Difficulty Distribution:**
- Medium: 20 (10%)
- Medium-Hard: 140 (70%)
- Hard: 40 (20%)

**Topics Covered:**
- Pods: 50 questions
- Deployments & ReplicaSets: 50 questions
- Services: 40 questions
- ConfigMaps & Secrets: 30 questions
- Namespaces, Labels & Selectors: 30 questions
