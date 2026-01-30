# Kubernetes Core Concepts - Q61-Q70 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q61-Q70

---

### Question 61
[HARD]

A platform team manages a Deployment with 12 replicas across a cluster spanning three availability zones (us-east-1a, us-east-1b, us-east-1c). They want to ensure that no single zone runs more than 5 replicas at any time, even during rolling updates. They configure a Pod topology spread constraint with `maxSkew: 1`, `topologyKey: topology.kubernetes.io/zone`, and `whenUnsatisfiable: DoNotSchedule`. During a rolling update, zone us-east-1c loses all its nodes temporarily. What happens to the Pods that need to be scheduled?

A) All 12 replicas are evenly distributed across the two remaining zones (6 per zone), ignoring the maxSkew constraint during disruptions
B) The scheduler places Pods in the two remaining zones while respecting maxSkew, leaving some Pods in Pending state if the constraint cannot be satisfied
C) The scheduler automatically switches to `whenUnsatisfiable: ScheduleAnyway` when a zone is unavailable
D) Kubernetes removes the topology spread constraint for the duration of the rolling update to maintain replica count

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod topology spread constraints are enforced at scheduling time. When `whenUnsatisfiable` is set to `DoNotSchedule`, the scheduler treats the constraint as a hard requirement and will not place Pods in a topology that violates the `maxSkew`. If zone us-east-1c is unavailable, the scheduler can only use two zones, and if distributing all replicas across two zones would violate the skew, some Pods will remain Pending. Kubernetes does not automatically relax or remove topology spread constraints during disruptions or rolling updates. The constraint must be explicitly changed by the operator if different behavior is desired.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/

</details>

---

### Question 62
[HARD]

A team runs Pods in a cluster that uses a container runtime with kata-containers for stronger isolation. Each Pod's sandbox environment consumes 128Mi of memory and 0.25 CPU cores beyond what the application containers request. The team defines a RuntimeClass with `overhead` set to `memory: 128Mi` and `cpu: 250m`. A Pod specifies a single container requesting 512Mi memory and 0.5 CPU. When the kube-scheduler evaluates node placement for this Pod, what total resources does it consider?

A) 512Mi memory and 0.5 CPU, because Pod overhead only affects billing, not scheduling
B) 640Mi memory and 0.75 CPU, because the scheduler adds the RuntimeClass overhead to the container resource requests
C) 512Mi memory and 0.5 CPU, because overhead is only applied at the kubelet level after scheduling
D) 640Mi memory and 0.75 CPU, but only if the Pod explicitly references the overhead in its resource requests

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod overhead is a feature that allows the extra resources consumed by the Pod infrastructure (such as a VM-based runtime like kata-containers) to be accounted for in scheduling and resource management. When a RuntimeClass defines an `overhead` field and a Pod uses that RuntimeClass, the kubelet adds the overhead to the Pod's resource calculations. Critically, the kube-scheduler also factors in this overhead when determining whether a node has sufficient resources to run the Pod. So the scheduler sees 512Mi + 128Mi = 640Mi memory and 0.5 + 0.25 = 0.75 CPU. This overhead is also considered for eviction decisions and resource quota accounting.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/

</details>

---

### Question 63
[HARD]

A cluster administrator initiates a planned maintenance operation using `kubectl drain node-3 --grace-period=60 --ignore-daemonsets`. Node-3 is running three types of Pods: a DaemonSet Pod, a Deployment-managed Pod with a PodDisruptionBudget allowing 0 unavailable, and a static Pod managed by the kubelet. What is the expected outcome of this drain operation?

A) All three Pod types are evicted; the DaemonSet Pod is recreated on another node
B) The DaemonSet Pod is ignored, the static Pod is evicted, and the Deployment Pod eviction is blocked by the PDB until the budget is satisfied
C) The DaemonSet Pod is ignored, the static Pod cannot be evicted by drain (it is kubelet-managed), and the Deployment Pod eviction is blocked by the PDB
D) All Pods are immediately terminated because the drain command overrides PDBs and DaemonSet protections

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `kubectl drain` command with `--ignore-daemonsets` will skip DaemonSet-managed Pods, as they are expected to run on every node and cannot be meaningfully rescheduled. Static Pods are managed directly by the kubelet via manifest files on the node, not through the API server, so `kubectl drain` cannot evict them through the normal eviction API. The Deployment-managed Pod is subject to the PodDisruptionBudget, and since the PDB allows 0 unavailable, the eviction API will refuse to evict that Pod until the budget can be satisfied (for example, if additional replicas are brought up first). The drain command will block waiting for the PDB to be satisfied or until a timeout is reached.

**Source:** https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/

</details>

---

### Question 64
[HARD]

A team configures health checks for a Java-based microservice that exposes an HTTP health endpoint at `/healthz` on port 8080, a TCP listener on port 9090 for its gRPC interface, and runs a startup script that writes a file `/tmp/ready` when initialization is complete. The application takes 90 seconds to start but is highly responsive once running. Which probe configuration best ensures Kubernetes accurately detects startup completion, ongoing liveness, and readiness to receive traffic?

A) Use an httpGet liveness probe on `/healthz:8080` with `initialDelaySeconds: 90`, an exec readiness probe checking for `/tmp/ready`, and no startup probe
B) Use a tcpSocket startup probe on port 9090 with `failureThreshold: 30` and `periodSeconds: 3`, an httpGet liveness probe on `/healthz:8080`, and an exec readiness probe checking for `/tmp/ready`
C) Use an httpGet startup probe on `/healthz:8080` with `failureThreshold: 30` and `periodSeconds: 3`, an httpGet liveness probe on `/healthz:8080`, and an exec readiness probe checking for `/tmp/ready`
D) Use an exec startup probe checking for `/tmp/ready`, a tcpSocket liveness probe on port 9090, and an httpGet readiness probe on `/healthz:8080`

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The optimal configuration uses an httpGet startup probe against the `/healthz` endpoint because this confirms the full HTTP stack is initialized, not merely that a TCP port is open. Setting `failureThreshold: 30` and `periodSeconds: 3` gives the application up to 90 seconds to start (30 x 3 = 90s). Until the startup probe succeeds, the liveness and readiness probes are disabled, preventing premature restarts. After startup completes, the httpGet liveness probe on `/healthz` continuously checks that the application process is healthy, while the exec readiness probe checking `/tmp/ready` ensures the Pod only receives traffic when it has signaled full readiness. Option A uses `initialDelaySeconds` which is a fixed wait and less precise than a startup probe. Option B uses tcpSocket for startup, which only verifies the port is open, not that the application is truly ready.

**Source:** https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/

</details>

---

### Question 65
[HARD]

A legacy application container takes between 30 seconds and 5 minutes to start, depending on the size of its cache warm-up. The team initially configured only a liveness probe with `initialDelaySeconds: 300` to account for the worst case. After switching to a startup probe, they notice significantly improved behavior for fast-starting instances. Why does the startup probe provide a better solution than a large `initialDelaySeconds` on the liveness probe?

A) The startup probe checks health more frequently than the liveness probe, so it detects failures faster during startup
B) Once the startup probe succeeds, the liveness probe activates immediately, so fast-starting instances get liveness protection within seconds rather than waiting the full 300 seconds
C) The startup probe replaces the liveness probe entirely, reducing resource consumption from probe checks
D) The startup probe automatically adjusts the liveness probe's `initialDelaySeconds` based on how long startup actually takes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Startup probes were introduced specifically to handle slow-starting containers. The key advantage is that the liveness probe is disabled as long as the startup probe has not yet succeeded. Once the startup probe succeeds (which could be after 30 seconds for a fast start), the liveness and readiness probes activate immediately. This means a fast-starting instance gets liveness protection right away, rather than sitting unmonitored for the full `initialDelaySeconds` period. With the old approach of `initialDelaySeconds: 300`, even a container that started in 30 seconds would have no liveness checking for the remaining 270 seconds, during which a crash would go undetected. The startup probe does not replace the liveness probe; it gates when the liveness probe begins.

**Source:** https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/#startup-probes

</details>

---

### Question 66
[HARD]

A team runs a critical service with a Deployment of 5 replicas and a PodDisruptionBudget specifying `minAvailable: 4`. During a cluster upgrade, the administrator needs to drain two nodes simultaneously, each running one replica of this service. What behavior should the team expect?

A) Both nodes drain successfully because the PDB only applies to application-initiated disruptions, not administrative drain operations
B) The first node drains one replica successfully (leaving 4 available), but the second drain blocks because evicting another replica would violate the PDB's minAvailable of 4
C) Both drains proceed simultaneously because Kubernetes evaluates PDBs per-node, not cluster-wide
D) Both drains are blocked because the PDB prevents any evictions when the Deployment has exactly 5 replicas

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PodDisruptionBudgets protect against voluntary disruptions, which explicitly include administrative operations like `kubectl drain`. The PDB is evaluated cluster-wide, not per-node. When the first drain evicts one replica, the available count drops to 4, which still satisfies `minAvailable: 4`. However, when the second drain attempts to evict another replica, the eviction API checks the PDB and finds that evicting this Pod would drop available replicas to 3, violating the `minAvailable: 4` requirement. The second drain will therefore block until an additional replica becomes available elsewhere in the cluster. This is the primary purpose of PDBs: ensuring that voluntary disruptions do not degrade service availability below the specified threshold.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets

</details>

---

### Question 67
[HARD]

A node in a Kubernetes cluster begins experiencing severe memory pressure. The kubelet detects that available memory has crossed the eviction threshold. The node is running three Pods: Pod A is a BestEffort Pod (no resource requests or limits), Pod B is a Burstable Pod (requests 256Mi, limits 512Mi, currently using 400Mi), and Pod C is a Guaranteed Pod (requests and limits both 512Mi, currently using 480Mi). Which Pod does the kubelet evict first?

A) Pod C, because it is using the most absolute memory (480Mi)
B) Pod B, because it has exceeded its resource requests by the largest margin
C) Pod A, because BestEffort Pods are always evicted first during node-pressure eviction, regardless of actual memory usage
D) The Pod that was most recently started, regardless of QoS class

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a node experiences memory pressure, the kubelet follows a specific eviction order based on Pod Quality of Service (QoS) classes. BestEffort Pods (those with no resource requests or limits) are evicted first because they made no resource guarantees and have the lowest priority. Next, Burstable Pods that are exceeding their resource requests are evicted, ordered by their usage relative to requests. Guaranteed Pods are evicted last, only when no lower QoS Pods remain and they are exceeding their limits (which is rare since limits are enforced). Pod A, as a BestEffort Pod, will be evicted first regardless of its actual memory consumption relative to other Pods.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/#pod-selection-for-kubelet-eviction

</details>

---

### Question 68
[HARD]

An administrator adds a taint `maintenance=true:NoExecute` with a `tolerationSeconds` not set on the taint itself to a node that is currently running three Pods. Pod X has no tolerations. Pod Y tolerates the taint with `tolerationSeconds: 300`. Pod Z tolerates the taint with no `tolerationSeconds` specified. What happens to each Pod after the taint is applied?

A) All three Pods continue running because NoExecute only affects future scheduling, not running Pods
B) Pod X is evicted immediately, Pod Y is evicted after 300 seconds, and Pod Z continues running indefinitely
C) All three Pods are evicted immediately because NoExecute always evicts all Pods on the node
D) Pod X and Pod Y are evicted immediately, while Pod Z continues running because it has an unconditional toleration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `NoExecute` taint effect is unique among taint effects because it affects Pods that are already running on the node, not just future scheduling decisions. When a NoExecute taint is applied, Pods that do not tolerate the taint (Pod X) are evicted immediately. Pods that tolerate the taint with a `tolerationSeconds` value (Pod Y with 300 seconds) will continue running for that duration and then be evicted. Pods that tolerate the taint without specifying `tolerationSeconds` (Pod Z) are treated as tolerating the taint indefinitely and will continue running on the node. This mechanism is used for scenarios like node maintenance and is also how Kubernetes automatically handles node conditions like NotReady.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#taint-based-evictions

</details>

---

### Question 69
[HARD]

A team deploys a stateful application with 6 replicas using a Deployment. They want to ensure no two replicas run on the same node to maximize fault tolerance, but they also want replicas spread as evenly as possible across their three availability zones. They configure `podAntiAffinity` with `requiredDuringSchedulingIgnoredDuringExecution` matching on `kubernetes.io/hostname`, and a `topologySpreadConstraint` with `maxSkew: 1` on `topology.kubernetes.io/zone`. The cluster has 3 zones with 2 nodes each (6 nodes total). What happens if one node fails?

A) The replacement Pod is scheduled on any available node in any zone, ignoring both the anti-affinity and topology spread constraints
B) The replacement Pod can only be scheduled on the remaining node in the same zone as the failed node, because both the anti-affinity and topology spread constraints must be satisfied
C) The replacement Pod remains Pending because no node can satisfy the hard anti-affinity requirement without violating the topology spread constraint
D) The replacement Pod is scheduled on the remaining node in the failed node's zone if available, since anti-affinity is a hard requirement but spread constraints are best-effort by default

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `requiredDuringSchedulingIgnoredDuringExecution` anti-affinity on hostname, no two replicas can be placed on the same node, which is a hard requirement. The topology spread constraint with `maxSkew: 1` and `DoNotSchedule` (the default for `whenUnsatisfiable` when not specified) ensures replicas are evenly distributed across zones. With 6 replicas across 3 zones and 2 nodes per zone, the ideal distribution is 2 replicas per zone, one on each node. If one node fails, its replica needs rescheduling. The remaining node in that zone has no replica of this application (the other one was on the failed node), so it satisfies the anti-affinity rule. Placing the Pod there also maintains the 2-2-2 zone distribution, satisfying the topology spread constraint. This is the only valid placement that satisfies both constraints.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity

</details>

---

### Question 70
[HARD]

A Pod receives a deletion request and has `terminationGracePeriodSeconds` set to the default value of 30. The Pod runs a container with a preStop hook that executes a script taking 10 seconds, and the main application process requires 15 seconds to complete in-flight requests after receiving SIGTERM. What is the sequence of events, and does the Pod terminate gracefully?

A) The preStop hook runs (10s), then SIGTERM is sent (application uses 15s), totaling 25 seconds, and the Pod terminates gracefully within the 30-second window
B) SIGTERM is sent immediately, the preStop hook runs in parallel, and the Pod is killed after 30 seconds regardless of whether the application has finished
C) The preStop hook runs (10s), then SIGTERM is sent, but the 30-second grace period started when the deletion was requested, so the application has only 20 seconds remaining, which is sufficient for its 15-second shutdown
D) The preStop hook and SIGTERM are sent simultaneously, and the grace period only starts after both signals are delivered

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a Pod deletion is initiated, the grace period timer starts immediately. Kubernetes first executes the preStop hook if one is defined. The preStop hook runs to completion (taking 10 seconds in this scenario). Only after the preStop hook finishes does Kubernetes send SIGTERM to the container's main process. Critically, the 30-second grace period includes the time spent on the preStop hook. So after the 10-second preStop hook, the application has 20 seconds remaining before Kubernetes sends SIGKILL. Since the application needs only 15 seconds to handle in-flight requests after SIGTERM, it completes gracefully within the remaining window. If the combined time exceeded 30 seconds, the kubelet would send SIGKILL to forcefully terminate the container.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination

</details>
