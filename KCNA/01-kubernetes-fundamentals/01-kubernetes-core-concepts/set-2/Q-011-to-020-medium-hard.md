# Kubernetes Core Concepts - Q11-Q20 [Medium-Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Medium-Hard
**Questions:** Q11-Q20

---

### Question 11
[MEDIUM-HARD]

A developer defines a Pod with two init containers: `init-db-check` (listed first) and `init-config-load` (listed second). The `init-db-check` container fails on its first attempt but succeeds on retry. What happens to `init-config-load` during the time `init-db-check` is failing?

A) `init-config-load` runs in parallel with `init-db-check` since init containers are concurrent by default
B) `init-config-load` does not start at all until `init-db-check` completes successfully
C) `init-config-load` starts but is paused until `init-db-check` succeeds
D) `init-config-load` is skipped entirely because an init container failure aborts all subsequent init containers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Init containers run sequentially in the order they are defined in the Pod spec. Each init container must complete successfully (exit code 0) before the next one starts. While `init-db-check` is failing and being retried by the kubelet, `init-config-load` has not been started at all -- it remains waiting. Only after `init-db-check` exits successfully will `init-config-load` begin execution. Init containers are never run in parallel, and a failure does not skip subsequent init containers; instead, the failing one is retried according to the Pod's restartPolicy.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/init-containers/#understanding-init-containers

</details>

---

### Question 12
[MEDIUM-HARD]

A Pod has a liveness probe configured with `httpGet` on path `/healthz`, `initialDelaySeconds: 10`, `periodSeconds: 5`, and `failureThreshold: 3`. The application starts successfully but after 30 seconds begins returning HTTP 500 on `/healthz`. What action does the kubelet take after the failure threshold is reached?

A) The kubelet marks the Pod as NotReady and removes it from Service endpoints but keeps the container running
B) The kubelet kills the container and, subject to the Pod's restart policy, restarts it
C) The kubelet evicts the entire Pod from the node and the scheduler reschedules it elsewhere
D) The kubelet sends a SIGTERM to the process and waits for the terminationGracePeriodSeconds before force-killing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a liveness probe fails beyond the configured `failureThreshold`, the kubelet kills the container (not the Pod) and restarts it according to the Pod's `restartPolicy`. This is distinct from a readiness probe failure, which only removes the Pod from Service endpoints without restarting anything. The kubelet does not reschedule the Pod to another node -- that would require the Pod to be deleted and recreated by a controller. Option D describes graceful shutdown during Pod termination, not a liveness probe failure response; the kubelet kills the container directly.

**Source:** https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/#liveness-probes

</details>

---

### Question 13
[MEDIUM-HARD]

A Deployment has 3 replicas behind a Service. One replica's readiness probe begins failing, but its liveness probe continues to pass. What is the observable effect on traffic routing?

A) The failing Pod continues to receive traffic because it is still alive and running
B) The Service removes the failing Pod's IP from its Endpoints, so traffic is distributed only to the 2 healthy Pods
C) The kubelet restarts the container in the failing Pod, temporarily reducing capacity to 2 Pods
D) The Deployment controller immediately creates a 4th replica to compensate for the unhealthy Pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Readiness probes control whether a Pod's IP address is included in the Service's Endpoints list. When a readiness probe fails, the EndpointSlice controller removes that Pod from the Service's endpoints, preventing it from receiving new traffic. Crucially, because the liveness probe is still passing, the kubelet does not restart the container -- the Pod remains running. The Deployment controller does not create replacement Pods for Pods that are merely unready; it only cares about the total number of existing Pods matching its desired replica count. Traffic is routed only to the 2 Pods still passing readiness checks.

**Source:** https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/#readiness-probes

</details>

---

### Question 14
[MEDIUM-HARD]

A team deploys an application Pod that writes logs in a custom binary format. They add a second container to the same Pod that reads those log files, converts them to JSON, and exposes them on an HTTP endpoint for a log collector. Which multi-container Pod pattern does this describe?

A) Sidecar pattern -- the second container extends the primary container's functionality
B) Ambassador pattern -- the second container proxies network traffic to external services
C) Adapter pattern -- the second container transforms the primary container's output into a standardized format
D) Init pattern -- the second container runs before the primary to prepare the environment

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The adapter pattern involves a helper container that transforms the output of the primary container into a format expected by an external consumer. In this scenario, the second container reads binary logs and converts them to JSON -- a classic data transformation task. The sidecar pattern extends functionality (e.g., log shipping, syncing files) without transforming output format. The ambassador pattern proxies outbound network connections (e.g., handling service discovery or connection pooling for external databases). An init container runs to completion before the main containers start, which does not match a continuously running log converter.

**Source:** https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/

</details>

---

### Question 15
[MEDIUM-HARD]

A team creates a bare Pod (not managed by any controller) with `restartPolicy: Never`. The single container in the Pod exits with a non-zero exit code. What is the final state of the Pod?

A) The Pod enters a CrashLoopBackOff state as the kubelet repeatedly tries to restart it
B) The container is restarted once, and if it fails again, the Pod is marked as Failed
C) The Pod transitions to the Failed phase and the container is not restarted
D) The kubelet deletes the Pod automatically and it disappears from `kubectl get pods`

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** With `restartPolicy: Never`, the kubelet will not restart any container in the Pod regardless of exit code. When the container exits with a non-zero code, the Pod's phase becomes `Failed` and remains visible in `kubectl get pods` output until explicitly deleted. CrashLoopBackOff only occurs with `restartPolicy: Always` or `restartPolicy: OnFailure`, where the kubelet attempts repeated restarts with exponential backoff. The kubelet never automatically deletes Pods -- garbage collection of finished Pods is handled by the controller that owns them (e.g., a Job's TTL mechanism), but bare Pods have no such controller.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#restart-policy

</details>

---

### Question 16
[MEDIUM-HARD]

A developer needs to expose a microservice to other Pods within the cluster, but the service should NOT be accessible from outside the cluster. The team also wants to minimize cloud provider costs. Which Service type is the most appropriate choice?

A) NodePort -- it is the simplest type and only exposes the service on each node's IP
B) ClusterIP -- it provides an internal-only virtual IP accessible only from within the cluster
C) LoadBalancer -- it provides a stable endpoint and can be restricted with firewall rules
D) ExternalName -- it maps the service to an internal DNS name without exposing externally

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ClusterIP is the default Service type and assigns a virtual IP that is only reachable from within the cluster network. It satisfies both requirements: internal-only access and zero cloud provider cost (no external load balancer is provisioned). NodePort exposes a port on every node's external IP (30000-32767 range), making the service reachable from outside the cluster. LoadBalancer provisions a cloud load balancer, adding cost and external exposure. ExternalName does not create a proxy or ClusterIP at all -- it returns a CNAME record pointing to a specified external DNS name, which is the opposite of what is needed.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#type-clusterip

</details>

---

### Question 17
[MEDIUM-HARD]

A Pod in the `payments` Namespace needs to connect to a Service named `db-primary` in the `databases` Namespace. The developer configures the connection string as `db-primary:5432`. The connection fails. What is the correct DNS name the developer should use?

A) `db-primary.databases:5432`
B) `db-primary.databases.svc.cluster.local:5432`
C) `databases.db-primary.svc.cluster.local:5432`
D) `db-primary.svc.databases.cluster.local:5432`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Within a Kubernetes cluster, Services are assigned DNS records following the pattern `<service-name>.<namespace>.svc.cluster.local`. The short name `db-primary` (without a namespace qualifier) only resolves within the same Namespace as the calling Pod, which is `payments` in this case -- so the connection fails because there is no `db-primary` Service in `payments`. To reach a Service in a different Namespace, the developer must include at least the namespace: `db-primary.databases` works as a shorter form, but the fully qualified domain name is `db-primary.databases.svc.cluster.local`. Option C reverses the service and namespace order, and option D places `svc` incorrectly.

**Source:** https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#services

</details>

---

### Question 18
[MEDIUM-HARD]

A container is configured with a memory request of 256Mi and a memory limit of 512Mi. During a traffic spike, the container's resident memory usage grows to 600Mi. What happens to this container?

A) The kubelet throttles the container's memory allocation back down to 512Mi, similar to CPU throttling
B) The container is OOMKilled by the kernel because it exceeded its memory limit
C) The Pod is evicted from the node by the kubelet's eviction manager
D) The container continues running at 600Mi but is flagged for eviction during the next node pressure event

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Unlike CPU, which can be throttled, memory is an incompressible resource in Kubernetes. When a container attempts to allocate memory beyond its configured limit, the Linux kernel's OOM (Out of Memory) killer terminates the process. The container's exit reason will show `OOMKilled`. The kubelet's eviction manager handles node-level memory pressure by evicting Pods whose total usage exceeds node allocatable resources, but that is a different mechanism from per-container limit enforcement. Memory cannot be "throttled" like CPU -- once allocated, the kernel must either grant or deny the allocation.

**Source:** https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#how-pods-with-resource-limits-are-run

</details>

---

### Question 19
[MEDIUM-HARD]

An engineer runs `kubectl get pods` and sees a Pod stuck in `Pending` status for several minutes. They run `kubectl describe pod` and see the event message: `0/3 nodes are available: 3 Insufficient cpu.` What is the most likely cause and the correct remediation?

A) The Pod's CPU request exceeds the allocatable CPU on all nodes; reduce the request or add nodes with more capacity
B) The Pod has a node affinity rule that excludes all nodes; update the affinity configuration
C) The container image cannot be pulled, causing the scheduler to defer placement; verify the image name and registry access
D) The Pod's CPU limit is set too high, and the scheduler rejects Pods that might burst beyond node capacity

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The event message `Insufficient cpu` explicitly indicates that the kube-scheduler evaluated all 3 nodes and found that none have enough allocatable CPU to satisfy the Pod's resource request. The scheduler uses requests (not limits) for placement decisions -- it must guarantee that the requested resources are available on the chosen node. Reducing the Pod's CPU request, scaling down other workloads to free resources, or adding nodes with more CPU capacity will resolve the issue. Node affinity failures produce a different event message (e.g., "didn't match Pod's node affinity/selector"). Image pull issues result in `ErrImagePull` or `ImagePullBackOff`, not `Pending` with a scheduling event.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/pod-scheduling-readiness/

</details>

---

### Question 20
[MEDIUM-HARD]

A team needs to deploy a distributed database (e.g., Cassandra) where each instance requires a stable network identity, persistent storage that follows the Pod across rescheduling, and ordered rolling updates. They currently use a Deployment. Why should they switch to a StatefulSet?

A) StatefulSets support rolling updates while Deployments do not
B) StatefulSets provide each Pod with a stable hostname, ordered deployment/scaling, and stable persistent storage via volumeClaimTemplates, which Deployments cannot guarantee
C) StatefulSets automatically distribute Pods across failure domains, which Deployments lack
D) StatefulSets use a headless Service by default, which provides better load balancing than a standard ClusterIP Service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSets are designed specifically for stateful workloads like databases. They provide three guarantees that Deployments do not: (1) stable, unique network identifiers -- each Pod gets a predictable hostname like `cassandra-0`, `cassandra-1`, etc., maintained across rescheduling; (2) stable, persistent storage -- each Pod is associated with a specific PersistentVolumeClaim via `volumeClaimTemplates` that reattaches if the Pod is rescheduled; (3) ordered, graceful deployment and scaling -- Pods are created in sequence (0, 1, 2...) and terminated in reverse order. Deployments do support rolling updates (so option A is wrong), and topology spread constraints for failure domains are available to both (so option C is wrong). A headless Service is often used with StatefulSets for direct Pod DNS, but it does not provide "better load balancing" -- it provides no load balancing, which is the point.

**Source:** https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/

</details>
