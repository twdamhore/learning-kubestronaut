# Kubernetes Core Concepts - 200 MCQ Questions

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Kubernetes Core Concepts
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

## Pods

### Question 1
[MEDIUM]

What is the smallest deployable unit in Kubernetes?

A) Container
B) Pod
C) Node
D) Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod is the smallest deployable unit in Kubernetes. While containers run inside Pods, Kubernetes doesn't manage containers directly—it manages Pods. A Pod can contain one or more containers that share the same network namespace and storage volumes.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 2
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

### Question 3
[MEDIUM-HARD]

What happens when a container in a Pod with `restartPolicy: Always` exits with a non-zero exit code?

A) The Pod is deleted and recreated
B) The container is restarted by the kubelet
C) The Pod enters a Failed state permanently
D) A new Pod is scheduled on a different node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a container exits with a non-zero exit code and the Pod's `restartPolicy` is set to `Always`, the kubelet on that node will restart the container in place. The Pod itself is not recreated or rescheduled—only the container within it is restarted.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 4
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

### Question 5
[MEDIUM-HARD]

What is the purpose of an init container?

A) To run alongside the main container indefinitely
B) To perform initialization tasks before app containers start
C) To handle traffic routing to the Pod
D) To collect logs from the main container

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Init containers run to completion before any app containers start. They're used for initialization tasks like setting up configuration, waiting for dependencies, or preparing data. Init containers run sequentially, and the Pod won't start app containers until all init containers complete successfully.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

---

### Question 6
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

### Question 7
[HARD]

A Pod has the following configuration. What will happen when the main container exits with code 0?

```yaml
restartPolicy: OnFailure
```

A) The container will be restarted immediately
B) The container will not be restarted
C) The Pod will be rescheduled to another node
D) Kubernetes will wait 10 seconds then restart

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `restartPolicy: OnFailure`, containers are only restarted if they exit with a non-zero exit code (failure). An exit code of 0 indicates successful completion, so the container will not be restarted and the Pod will enter the Succeeded phase.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 8
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

### Question 9
[HARD]

Which field in the Pod spec determines the order in which init containers run?

A) The `priority` field
B) The order they are listed in the `initContainers` array
C) The `order` annotation
D) Init containers run in parallel, not sequentially

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Init containers run sequentially in the order they are listed in the `initContainers` array. Each init container must complete successfully before the next one starts. There is no priority field for init containers—their order is determined purely by their position in the array.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

---

### Question 10
[MEDIUM-HARD]

What happens if an init container fails?

A) The Pod continues with app containers anyway
B) Kubernetes restarts the init container according to the Pod's restart policy
C) The Pod is immediately deleted
D) The failed init container is skipped

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If an init container fails, Kubernetes restarts it according to the Pod's restart policy. With the default `Always` policy, the init container will keep restarting until it succeeds. The app containers will not start until all init containers complete successfully.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

---

### Question 11
[MEDIUM-HARD]

How can you specify resource requests for a container?

A) In the Pod's metadata section
B) In the container's `resources.requests` field
C) Using a ResourceQuota object
D) Through node labels

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Resource requests are specified in the container spec under `resources.requests`. This tells the scheduler how much CPU and memory the container needs, which is used for scheduling decisions. ResourceQuotas limit total resources in a namespace but don't set container-level requests.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 12
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

### Question 13
[MEDIUM-HARD]

Which of the following accurately describes a sidecar container?

A) A container that runs before the main container
B) A container that runs alongside the main container to provide supporting functionality
C) A container that only runs when the main container fails
D) A container that handles external traffic routing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A sidecar container runs alongside the main application container in the same Pod, providing supporting functionality like logging, monitoring, or proxying. Unlike init containers, sidecars run for the lifetime of the Pod alongside the main container.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 14
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

### Question 15
[HARD]

A Pod is in `Pending` status. Which of the following is NOT a possible reason?

A) Insufficient cluster resources
B) The image is being pulled
C) The Pod is waiting for a PersistentVolumeClaim to be bound
D) A container inside the Pod is crash-looping

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** A crash-looping container would put the Pod in `Running` status (with container status showing CrashLoopBackOff), not `Pending`. Pending status occurs before the Pod is scheduled or while waiting for resources like images or volumes. Once scheduled and containers start (even if they crash), the Pod is Running.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 16
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

### Question 17
[MEDIUM-HARD]

Which command shows the logs of a specific container in a multi-container Pod?

A) `kubectl logs <pod> --all-containers`
B) `kubectl logs <pod> -c <container>`
C) `kubectl logs <pod>/<container>`
D) `kubectl describe pod <pod>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To view logs from a specific container in a multi-container Pod, use `kubectl logs <pod-name> -c <container-name>`. The `-c` or `--container` flag specifies which container's logs to retrieve.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 18
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

### Question 19
[HARD]

What is the purpose of `terminationGracePeriodSeconds` in a Pod spec?

A) Time to wait before force-starting a container
B) Time allowed for graceful shutdown before SIGKILL is sent
C) Maximum time a Pod can run before automatic termination
D) Delay before a Pod is scheduled

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `terminationGracePeriodSeconds` (default 30) specifies how long Kubernetes waits after sending SIGTERM before sending SIGKILL to forcefully terminate containers. This allows applications time to gracefully shut down, close connections, and clean up resources.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 20
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

### Question 21
[MEDIUM]

What is the status of a Pod that has been scheduled but is waiting for container images to download?

A) Pending
B) Waiting
C) ContainerCreating
D) ImagePullBackOff

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** While waiting for images to download, the Pod remains in `Pending` status. The container status might show `Waiting` with reason `ContainerCreating` or `ImagePullBackOff` if there are issues, but the Pod phase itself is `Pending` until containers start.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 22
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

### Question 23
[MEDIUM-HARD]

How do you execute a command inside a running container?

A) `kubectl run <pod> -- <command>`
B) `kubectl exec <pod> -- <command>`
C) `kubectl attach <pod> -- <command>`
D) `kubectl connect <pod> -- <command>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl exec` is used to execute commands inside a running container. Use `kubectl exec <pod> -- <command>` for a single command, or add `-it` for an interactive terminal session. For multi-container Pods, specify the container with `-c`.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 24
[MEDIUM-HARD]

What is the purpose of a Pod's `serviceAccountName` field?

A) To specify which Service exposes the Pod
B) To define the identity used by the Pod for API authentication
C) To set the DNS name of the Pod
D) To specify resource accounting

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `serviceAccountName` field specifies which ServiceAccount the Pod uses for authenticating with the Kubernetes API. This determines what permissions the Pod has when making API calls and what secrets are automatically mounted.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 25
[HARD]

What is the effect of setting `shareProcessNamespace: true` in a Pod spec?

A) Containers share CPU resources equally
B) Containers can see each other's processes
C) Containers share the same PID 1
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** With `shareProcessNamespace: true`, all containers in the Pod share a single process namespace. This means containers can see and signal each other's processes, and they share PID 1 (which becomes the pause container). This is useful for debugging or process monitoring sidecars.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 26
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

### Question 27
[MEDIUM-HARD]

What happens when a livenessProbe fails?

A) The Pod is removed from Service endpoints
B) The container is restarted
C) The Pod is rescheduled to another node
D) An alert is sent to the cluster administrator

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a livenessProbe fails (after the configured failure threshold), the kubelet kills the container and restarts it according to the Pod's restart policy. This is Kubernetes' mechanism for detecting and recovering from application hangs or deadlocks.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 28
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

### Question 29
[MEDIUM-HARD]

Which probe type executes a command inside the container?

A) httpGet
B) tcpSocket
C) exec
D) grpc

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `exec` probe type runs a command inside the container. If the command exits with status code 0, the probe is considered successful. This is useful when your application doesn't expose HTTP endpoints but can be checked via command-line tools.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 30
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

### Question 31
[HARD]

What is the significance of the `failureThreshold` field in a probe configuration?

A) Maximum number of probe attempts before giving up permanently
B) Number of consecutive failures before the probe is considered failed
C) Time in seconds before marking the probe as failed
D) Number of Pods that can fail simultaneously

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `failureThreshold` specifies how many consecutive probe failures are needed before the container is considered unhealthy (for liveness) or not ready (for readiness). The default is 3, meaning the probe must fail 3 times in a row before action is taken.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 32
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

### Question 33
[MEDIUM-HARD]

What is an ephemeral container used for?

A) Running short-lived batch jobs
B) Debugging a running Pod without restarting it
C) Caching data temporarily
D) Running init tasks

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ephemeral containers are temporary containers added to an existing Pod for debugging purposes. They're useful when you need to inspect a running Pod that lacks debugging tools. Use `kubectl debug` to add an ephemeral container.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

---

### Question 34
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

### Question 35
[MEDIUM-HARD]

What happens to a Pod when its node becomes unreachable?

A) The Pod is immediately deleted and rescheduled
B) The Pod remains in Running status until the node-monitor-grace-period expires
C) The Pod is marked as Unknown after the node status times out
D) Both B and C, then the Pod may be evicted

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** When a node becomes unreachable, the Pod initially remains Running. After the node-monitor-grace-period (default 40s), the node is marked NotReady. The Pod status becomes Unknown, and after pod-eviction-timeout (default 5m), the Pod may be evicted so it can be rescheduled elsewhere.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 36
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

### Question 37
[HARD]

What is the purpose of a PodPreset (in clusters where it's enabled)?

A) To set default resource limits for Pods
B) To automatically inject environment variables, volumes, and mounts into Pods
C) To define Pod templates for Deployments
D) To preset scheduling constraints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PodPresets (deprecated in v1.20+) were used to automatically inject additional runtime requirements like environment variables, volumes, and volume mounts into Pods at creation time. This functionality is now typically achieved through admission webhooks or operators.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 38
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

### Question 39
[MEDIUM-HARD]

What is the relationship between a Pod and its containers' restart count?

A) The Pod has a single restart count for all containers
B) Each container has its own restart count
C) Restart counts are not tracked in Kubernetes
D) Only the main container's restart count is tracked

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Each container in a Pod has its own restart count tracked independently. You can see this in `kubectl get pod <pod> -o yaml` under each container's status. The counts reflect how many times the kubelet has restarted that specific container.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 40
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

### Question 41
[MEDIUM-HARD]

Which of the following is NOT a valid Pod condition type?

A) PodScheduled
B) ContainersReady
C) Initialized
D) PodRunning

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Valid Pod condition types include `PodScheduled`, `ContainersReady`, `Initialized`, and `Ready`. There is no `PodRunning` condition—`Running` is a Pod phase, not a condition. Conditions are boolean states, while phases describe the overall Pod lifecycle stage.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 42
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

### Question 43
[HARD]

What happens when you specify `imagePullPolicy: Always` with an image tagged `:latest`?

A) The image is pulled once and cached
B) The image is pulled every time the container starts
C) Kubernetes throws an error
D) The behavior is undefined

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `imagePullPolicy: Always`, the kubelet always attempts to pull the image before starting the container. Combined with `:latest` tag, this ensures you always get the newest version, but it also means container startup depends on registry availability.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 44
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

### Question 45
[MEDIUM-HARD]

What is the purpose of `dnsPolicy: ClusterFirst`?

A) The Pod uses only cluster DNS for all queries
B) Cluster DNS is queried first, then falls back to node DNS
C) DNS queries go directly to external DNS servers
D) DNS is disabled for the Pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `ClusterFirst` (the default), DNS queries are sent to the cluster DNS service first. If the query doesn't match a cluster domain (like `.cluster.local`), it's forwarded to upstream DNS servers configured on the node.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 46
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

### Question 47
[MEDIUM-HARD]

What is the maximum number of containers that can run in a single Pod?

A) 10
B) 100
C) No hard limit (practical limits based on resources)
D) 5

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Kubernetes doesn't impose a hard limit on containers per Pod. The practical limit depends on node resources, API server capacity, and the complexity of managing many containers. However, best practice is to keep Pods focused with few containers.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

---

### Question 48
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

### Question 49
[MEDIUM-HARD]

What does the `securityContext.runAsNonRoot: true` setting enforce?

A) The container must run as the root user
B) The container cannot run as UID 0
C) The container has no root filesystem access
D) Privilege escalation is allowed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `runAsNonRoot: true` ensures the container cannot run as root (UID 0). If the container image is configured to run as root and no `runAsUser` is specified, the container will fail to start. This is a security best practice.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 50
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

### Question 51
[MEDIUM]

What is the primary purpose of a Deployment?

A) To expose Pods to network traffic
B) To provide declarative updates for Pods and ReplicaSets
C) To store configuration data
D) To manage persistent storage

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deployments provide declarative updates for Pods and ReplicaSets. They manage the rollout of new versions, enable rollbacks, and ensure the desired number of Pod replicas are running. Deployments are the recommended way to manage stateless applications.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 52
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

### Question 53
[MEDIUM-HARD]

What is the default deployment strategy?

A) Recreate
B) RollingUpdate
C) BlueGreen
D) Canary

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The default deployment strategy is `RollingUpdate`, which gradually replaces old Pods with new ones. This ensures zero downtime during updates. The `Recreate` strategy kills all old Pods before creating new ones, causing downtime.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 54
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

### Question 55
[MEDIUM-HARD]

What does `maxUnavailable` control in a rolling update?

A) Maximum Pods that can be created above desired count
B) Maximum Pods that can be unavailable during the update
C) Maximum time a Pod can be unhealthy
D) Maximum number of failed updates before rollback

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `maxUnavailable` specifies the maximum number of Pods that can be unavailable during a rolling update. With 10 replicas and maxUnavailable=1, at least 9 Pods must always be available. It can be an absolute number or percentage.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 56
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

### Question 57
[MEDIUM-HARD]

How do you trigger a rollback to the previous Deployment version?

A) `kubectl rollback deployment <name>`
B) `kubectl rollout undo deployment <name>`
C) `kubectl deploy rollback <name>`
D) `kubectl revert deployment <name>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl rollout undo deployment <deployment-name>` to roll back to the previous revision. You can also specify a specific revision with `--to-revision=<number>`. This creates a new ReplicaSet (or scales up an existing one) with the previous configuration.

**Source:** [kubectl rollout | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

</details>

---

### Question 58
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

### Question 59
[HARD]

What is the purpose of `minReadySeconds` in a Deployment?

A) Minimum time before a Pod is considered available after becoming ready
B) Minimum time to wait before starting the rollout
C) Minimum time a Pod must run before being terminated
D) Minimum time between creating new Pods

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `minReadySeconds` specifies how long a newly created Pod should be ready (passing readiness probe) without any containers crashing before it's considered available. This helps catch Pods that crash shortly after starting.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 60
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

### Question 61
[MEDIUM-HARD]

What does `progressDeadlineSeconds` control?

A) Maximum time for the entire Deployment to complete
B) Maximum time for Deployment to make progress before being marked failed
C) Time between progress checks
D) Deadline for Pod initialization

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `progressDeadlineSeconds` (default 600) specifies how long to wait for a Deployment to make progress. If no new Pods become available within this time, the Deployment is marked as failed with a `ProgressDeadlineExceeded` condition.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 62
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

### Question 63
[HARD]

A Deployment is paused. What happens when you update the Pod template?

A) A new rollout starts immediately
B) Changes are queued and applied when resumed
C) The update is rejected
D) Only the first change is applied when resumed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Deployment is paused, updates to the Pod template are accepted but don't trigger a rollout. All changes accumulate and are applied as a single rollout when you resume the Deployment with `kubectl rollout resume`.

**Source:** [kubectl rollout | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_rollout/)

</details>

---

### Question 64
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

### Question 65
[HARD]

What happens if you manually create a Pod with labels matching a ReplicaSet's selector?

A) The Pod is rejected by the API server
B) The ReplicaSet adopts the Pod and may terminate excess Pods
C) The Pod runs independently
D) The ReplicaSet is paused

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If a Pod's labels match a ReplicaSet's selector, the ReplicaSet will "adopt" it. If this causes the total Pod count to exceed the desired replicas, the ReplicaSet will terminate Pods (possibly including your manually created one) to maintain the desired count.

**Source:** [ReplicaSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

</details>

---

### Question 66
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

### Question 67
[MEDIUM-HARD]

How do you scale a Deployment to 5 replicas?

A) `kubectl replicas deployment <name> 5`
B) `kubectl scale deployment <name> --replicas=5`
C) `kubectl set replicas deployment <name> 5`
D) `kubectl resize deployment <name> 5`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl scale deployment <name> --replicas=5` to change the replica count. You can also edit the Deployment directly or use `kubectl patch`. Scaling is independent of rollouts—it doesn't change the Pod template.

**Source:** [kubectl scale | Kubernetes](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/)

</details>

---

### Question 68
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

### Question 69
[MEDIUM-HARD]

What annotation triggers a new Deployment rollout when changed?

A) `kubernetes.io/change-cause`
B) `deployment.kubernetes.io/revision`
C) Any change to the Pod template spec
D) `kubectl.kubernetes.io/last-applied-configuration`

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A new rollout is triggered by any change to the Deployment's `.spec.template`. Changing metadata or annotations doesn't trigger a rollout unless it's part of the Pod template. The `kubernetes.io/change-cause` annotation is for documentation but doesn't trigger rollouts.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 70
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

### Question 71
[HARD]

How do you update the image of a Deployment without editing the full manifest?

A) `kubectl update deployment <name> --image=<new-image>`
B) `kubectl set image deployment <name> <container>=<new-image>`
C) `kubectl patch image deployment <name> <new-image>`
D) `kubectl replace image deployment <name>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl set image deployment <name> <container-name>=<new-image>` to update a container's image. For example: `kubectl set image deployment nginx nginx=nginx:1.19`. This triggers a rolling update if the Deployment isn't paused.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 72
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

### Question 73
[MEDIUM-HARD]

When would you use the Recreate strategy instead of RollingUpdate?

A) When you want zero downtime
B) When your application can't run multiple versions simultaneously
C) When you have unlimited resources
D) When doing canary deployments

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `Recreate` when your application can't handle multiple versions running at once, such as when there are database schema incompatibilities, when Pods use exclusive resources (like host ports), or when the application maintains state that conflicts across versions.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 74
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

### Question 75
[MEDIUM-HARD]

What does the `strategy.rollingUpdate.maxSurge: 0` setting mean?

A) No new Pods created during update (invalid configuration)
B) Old Pods must be deleted before new ones are created
C) Unlimited new Pods can be created
D) The update happens instantly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `maxSurge: 0`, no extra Pods can be created during the update. Combined with `maxUnavailable > 0`, this means old Pods must be terminated before new ones are created. This is useful when you have strict resource constraints.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment)

</details>

---

### Question 76
[HARD]

What happens during a failed rollout when `progressDeadlineSeconds` is exceeded?

A) The Deployment automatically rolls back
B) The Deployment is marked with a Failed condition but continues trying
C) All Pods are terminated
D) The Deployment is deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When `progressDeadlineSeconds` is exceeded, the Deployment's condition is set to `Progressing=False` with reason `ProgressDeadlineExceeded`. The Deployment continues trying—it doesn't automatically roll back. Manual intervention is required to fix or roll back.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 77
[MEDIUM-HARD]

How do you see the current revision number of a Deployment?

A) `kubectl get deployment <name> -o wide`
B) Check the `deployment.kubernetes.io/revision` annotation
C) `kubectl describe deployment <name>`
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** The current revision is stored in the `deployment.kubernetes.io/revision` annotation on both the Deployment and its current ReplicaSet. You can also see it in `kubectl describe deployment` output or by viewing the annotation directly.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 78
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

### Question 79
[HARD]

A Deployment update fails because new Pods are crash-looping. The old Pods are still running. How does Kubernetes handle this?

A) Automatically rolls back after 3 failures
B) Continues the rollout until progressDeadlineSeconds is exceeded
C) Deletes all Pods
D) Pauses the Deployment automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes doesn't automatically roll back failed deployments. It continues trying until `progressDeadlineSeconds` expires, then marks the Deployment as failed. Old Pods remain running (within the maxUnavailable constraint) until you manually fix or roll back.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 80
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

### Question 81
[HARD]

You want to update a Deployment but immediately roll back if any Pod fails readiness within 60 seconds. Which fields should you configure?

A) `progressDeadlineSeconds` and `minReadySeconds`
B) `failureThreshold` in readinessProbe only
C) `maxUnavailable` set to 0
D) There's no built-in way to do this automatically

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Kubernetes doesn't support automatic rollback on readiness failures. While `progressDeadlineSeconds` marks the Deployment as failed, it doesn't trigger rollback. You'd need external tooling (like Argo Rollouts or Flagger) for automatic rollback based on health metrics.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 82
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

### Question 83
[MEDIUM-HARD]

What does the annotation `deployment.kubernetes.io/revision` indicate?

A) The Deployment's overall version number
B) The revision number of the associated ReplicaSet
C) A Git commit hash
D) The API version

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** This annotation on a ReplicaSet indicates its revision number within the Deployment's history. The Deployment also has this annotation pointing to the current revision. This is how `kubectl rollout undo --to-revision` knows which ReplicaSet to scale up.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 84
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

### Question 85
[MEDIUM-HARD]

How do you annotate a Deployment change for historical tracking?

A) Add a `change-cause` label
B) Use `--record` flag or set `kubernetes.io/change-cause` annotation
C) Edit the `history` field
D) Use `kubectl annotate` after the change

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Set the `kubernetes.io/change-cause` annotation to document why a change was made. This appears in `kubectl rollout history` output. The `--record` flag (deprecated) used to do this automatically by recording the command.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 86
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

### Question 87
[MEDIUM-HARD]

A ReplicaSet is managing 5 Pods. You manually delete 2 Pods. What happens?

A) The ReplicaSet creates 2 new Pods to maintain 5 replicas
B) The replica count drops to 3
C) The ReplicaSet is marked as failed
D) Nothing, deleted Pods are not replaced

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** ReplicaSets continuously reconcile actual vs. desired state. When Pods are deleted (by any means), the ReplicaSet controller notices the discrepancy and creates new Pods to maintain the desired replica count. This is Kubernetes self-healing in action.

**Source:** [ReplicaSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

</details>

---

### Question 88
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

### Question 89
[HARD]

A Deployment has `revisionHistoryLimit: 0`. What happens when you update it?

A) Updates are rejected
B) Old ReplicaSets are immediately deleted after successful rollout
C) Rollback becomes impossible
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** With `revisionHistoryLimit: 0`, old ReplicaSets are garbage collected immediately after a successful rollout. This saves resources but makes rollback impossible since there's no history to roll back to. The current ReplicaSet is always retained.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 90
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

### Question 91
[HARD]

You update a Deployment twice in quick succession before the first rollout completes. What happens?

A) The second update waits for the first to complete
B) The first rollout is cancelled, and Kubernetes proceeds with the second
C) Both updates are merged
D) The second update is rejected

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes doesn't queue rollouts. If you update during a rollout, Kubernetes abandons the in-progress rollout and starts a new one with the latest spec. This means the intermediate state may never be fully achieved.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 92
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

### Question 93
[MEDIUM-HARD]

What does `kubectl apply -f deployment.yaml` do if the Deployment already exists?

A) Fails with an error
B) Deletes and recreates the Deployment
C) Updates the Deployment with changes from the file
D) Creates a second Deployment

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** `kubectl apply` performs a three-way merge: it compares the current state, last-applied configuration, and new manifest to calculate changes. It then patches the existing Deployment. This is the declarative way to manage Kubernetes resources.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 94
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

### Question 95
[MEDIUM-HARD]

How do you prevent a Deployment from being accidentally deleted?

A) Set `deletionProtection: true`
B) Use finalizers or RBAC to restrict delete permissions
C) Enable delete locks in the Deployment spec
D) Deployments cannot be protected from deletion

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes doesn't have built-in deletion protection for Deployments. Use RBAC to restrict who can delete resources. Finalizers can delay deletion but won't prevent it. Some organizations use admission webhooks to implement deletion protection.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 96
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

### Question 97
[MEDIUM-HARD]

What happens to traffic when a Pod's readiness probe fails?

A) The Pod is terminated
B) The Pod is removed from Service endpoints
C) The Pod is rescheduled
D) Nothing, traffic continues

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a readiness probe fails, the Pod's IP is removed from the Service's endpoints, stopping new traffic from being routed to it. The Pod continues running and can become ready again. This is different from liveness probe failure, which causes restart.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 98
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

### Question 99
[MEDIUM-HARD]

What label does a Deployment automatically add to Pods it creates?

A) `app: <deployment-name>`
B) `pod-template-hash`
C) `deployment: <deployment-name>`
D) `managed-by: deployment`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deployments automatically add a `pod-template-hash` label to both ReplicaSets and Pods. This hash is computed from the Pod template and ensures each ReplicaSet manages only Pods from its specific template version.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 100
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

### Question 101
[MEDIUM]

What is the primary purpose of a Kubernetes Service?

A) To deploy applications
B) To provide stable networking for a set of Pods
C) To store configuration
D) To manage secrets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Services provide a stable network endpoint (IP and DNS name) for a set of Pods. Since Pods are ephemeral and their IPs change, Services abstract away this volatility, enabling reliable communication to application Pods.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 102
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

### Question 103
[MEDIUM-HARD]

What port range does NodePort use by default?

A) 80-443
B) 1024-65535
C) 30000-32767
D) 8000-9000

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** NodePort Services allocate a port from the range 30000-32767 by default. This port is opened on all nodes, and traffic to any node on that port is routed to the Service. The range is configurable via the API server's `--service-node-port-range` flag.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 104
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

### Question 105
[MEDIUM-HARD]

What is the difference between `port` and `targetPort` in a Service spec?

A) They are aliases, no difference
B) `port` is the Service port, `targetPort` is the Pod port
C) `port` is external, `targetPort` is internal
D) `port` is for TCP, `targetPort` is for UDP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `port` is the port on which the Service listens. `targetPort` is the port on the Pod where traffic is sent. They can be different—for example, Service listens on 80 but forwards to Pod port 8080. If `targetPort` is omitted, it defaults to the same value as `port`.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 106
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

### Question 107
[MEDIUM-HARD]

When would you use a headless Service?

A) When you need load balancing
B) When clients need to discover individual Pod IPs
C) When exposing services externally
D) When you want a single stable IP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Headless Services are used when you need direct Pod discovery—for example, with StatefulSets where each Pod has a unique identity, or when using custom service discovery. DNS returns individual Pod IPs instead of a single VIP.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#headless-services)

</details>

---

### Question 108
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

### Question 109
[HARD]

A Service has `sessionAffinity: ClientIP`. What does this mean?

A) All traffic goes to one Pod
B) Traffic from the same client IP goes to the same Pod
C) The client IP is logged
D) Only specific client IPs can connect

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `sessionAffinity: ClientIP` enables sticky sessions based on client IP. Traffic from the same source IP is routed to the same backend Pod for the duration configured by `sessionAffinityConfig.clientIP.timeoutSeconds` (default 10800 seconds/3 hours).

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 110
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

### Question 111
[MEDIUM-HARD]

What Service type creates an external cloud load balancer?

A) ClusterIP
B) NodePort
C) LoadBalancer
D) ExternalName

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** `LoadBalancer` type provisions an external load balancer from the cloud provider (AWS ELB, GCP Load Balancer, etc.). It also creates a NodePort and ClusterIP. Traffic flows: External LB → NodePort → ClusterIP → Pods.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 112
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

### Question 113
[MEDIUM-HARD]

How do you expose a Service on a specific external IP?

A) Use `externalIPs` field in the Service spec
B) Use `nodeIP` field
C) Only LoadBalancer type can use external IPs
D) External IPs are assigned automatically

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The `externalIPs` field lets you specify external IPs where the Service should be reachable. Traffic arriving at any node for these IPs on the Service port is routed to the Service. These IPs must be routable to your nodes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 114
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

### Question 115
[HARD]

You need a Service to point to an external database at `db.example.com:5432`. What's the best approach?

A) Create a LoadBalancer Service
B) Create an ExternalName Service pointing to `db.example.com`
C) Create a Service without selector and manually create Endpoints
D) Both B and C work, depending on requirements

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Both work but differently. ExternalName creates a DNS alias (no port mapping). For port mapping or IP-based external services, create a selector-less Service with manual Endpoints. ExternalName is simpler but doesn't allow port remapping.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 116
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

### Question 117
[MEDIUM-HARD]

What is `externalTrafficPolicy: Local` used for?

A) To route all traffic to local Pods only
B) To preserve the client source IP and avoid extra network hops
C) To enable local DNS resolution
D) To disable external traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `externalTrafficPolicy: Local` routes external traffic only to Pods on the node receiving traffic, preserving client source IP. Without it (Cluster mode), traffic may hop to another node, and source IP is replaced with the node IP via SNAT.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 118
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

### Question 119
[MEDIUM-HARD]

How do you create a Service using an imperative command?

A) `kubectl create service clusterip my-svc --tcp=80:8080`
B) `kubectl expose deployment my-app --port=80 --target-port=8080`
C) `kubectl service create my-svc --port=80`
D) Both A and B work

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Both commands create Services. `kubectl expose` creates a Service for an existing resource (Deployment, Pod, etc.). `kubectl create service` creates a Service directly. The expose command is often more convenient as it inherits selectors from the target resource.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 120
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

### Question 121
[HARD]

What is the difference between Service port `nodePort`, `port`, and `targetPort`?

A) They're three names for the same thing
B) `nodePort` is external node port, `port` is Service port, `targetPort` is Pod port
C) `nodePort` is only for NodePort Services
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** `nodePort` is the port on each node (30000-32767 range, only for NodePort/LoadBalancer). `port` is the Service's ClusterIP port. `targetPort` is where Pods receive traffic. Traffic flow: nodePort → port → targetPort.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 122
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

### Question 123
[HARD]

Environment variables for Service discovery have a limitation. What is it?

A) They don't include the port
B) They're only set for Services created before the Pod
C) They only work for ClusterIP Services
D) They're deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Service environment variables are only injected for Services that exist when the Pod starts. Services created after the Pod won't have their variables injected. DNS doesn't have this limitation—it always resolves current Services.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 124
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

### Question 125
[MEDIUM-HARD]

What is the purpose of `service.spec.ipFamilyPolicy`?

A) To set IP address family preferences (IPv4/IPv6)
B) To configure network policies
C) To set DNS family
D) To configure IP masquerading

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `ipFamilyPolicy` controls IP family selection: `SingleStack` (one family), `PreferDualStack` (both if available, fallback to one), or `RequireDualStack` (must have both). This enables IPv4/IPv6 dual-stack Services.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 126
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

### Question 127
[MEDIUM-HARD]

What is the effect of deleting a Service?

A) Associated Pods are deleted
B) Only the Service object is deleted, Pods continue running
C) The Deployment is also deleted
D) Network policies are removed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deleting a Service only removes the Service object and its network endpoint. Pods selected by that Service continue running—they just lose the stable IP/DNS name the Service provided. Deployments and other controllers are unaffected.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 128
[HARD]

What is EndpointSlice and why was it introduced?

A) A way to slice network traffic
B) A scalable replacement for Endpoints with better performance
C) A method to distribute endpoints across zones
D) A security feature for endpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** EndpointSlices are a more scalable way to track network endpoints. Unlike Endpoints (single object per Service), EndpointSlices split endpoints across multiple smaller objects. This improves performance for Services with many Pods (>100) by reducing etcd and network overhead.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 129
[MEDIUM-HARD]

You see `kube-proxy` running on each node. What is its role with Services?

A) It creates Service objects
B) It implements Service networking using iptables/IPVS rules
C) It routes external traffic only
D) It manages DNS for Services

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-proxy watches Services and Endpoints, then programs the node's network (using iptables, IPVS, or other modes) to implement Service load balancing. It ensures traffic to a Service ClusterIP is distributed to backend Pods.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 130
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

### Question 131
[MEDIUM-HARD]

What does `service.spec.allocateLoadBalancerNodePorts: false` do?

A) Disables NodePort allocation for LoadBalancer Services
B) Disables load balancer creation
C) Allocates ports from a different range
D) Makes the Service internal-only

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Setting this to false prevents NodePort allocation for LoadBalancer Services when using cloud providers that support direct routing to Pods (like some implementations of AWS NLB). This saves NodePort allocation when they're not needed.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 132
[HARD]

A Service has `internalTrafficPolicy: Local`. What does this mean?

A) External traffic uses local routing
B) Internal cluster traffic only routes to Pods on the same node
C) The Service is only accessible locally
D) Traffic stays within the same zone

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `internalTrafficPolicy: Local` (introduced in v1.21) makes internal traffic (from within the cluster) route only to Pods on the same node as the client. This can reduce latency and cross-node traffic. If no local Pods exist, the request fails.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 133
[MEDIUM-HARD]

How do you specify multiple ports for a Service?

A) Create multiple Services
B) Add multiple entries to `spec.ports[]` array
C) Use port ranges
D) Multiple ports aren't supported

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Services support multiple ports by adding entries to the `spec.ports` array. Each entry needs a unique name if there's more than one port. Example: expose both HTTP (80) and HTTPS (443) on the same Service.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 134
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

### Question 135
[HARD]

What is the purpose of `service.spec.healthCheckNodePort`?

A) Port for container health checks
B) Port used by external load balancers to health check nodes
C) Port for kube-proxy health
D) Port for readiness probes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `healthCheckNodePort` specifies a port (allocated from NodePort range) where an HTTP health check endpoint is exposed. External load balancers use this to check if a node has healthy Pods (for `externalTrafficPolicy: Local`). Kubernetes auto-allocates if not specified.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 136
[MEDIUM-HARD]

What is the topology-aware routing feature in Services?

A) Routing based on network topology hints
B) Preferring endpoints in the same zone to reduce latency
C) DNS-based geographic routing
D) Both A and B

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Topology-aware routing (topology hints) enables Services to prefer endpoints in the same zone as the client. This reduces cross-zone traffic and latency. Enable with annotation `service.kubernetes.io/topology-mode: auto` or through EndpointSlice hints.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 137
[HARD]

A NodePort Service shows EXTERNAL-IP as `<none>`. Why?

A) NodePort Services don't allocate external IPs; access is via any node IP on the nodePort
B) It's waiting for IP allocation
C) There's a configuration error
D) The cloud provider hasn't responded yet

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** NodePort Services don't provision external IPs. `kubectl get svc` shows `<none>` for EXTERNAL-IP on NodePort Services. Access is via any node's IP address on the allocated nodePort (default range 30000-32767). Only LoadBalancer Services get external IPs (and show `<pending>` while waiting for cloud provisioning).

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types)

</details>

---

### Question 138
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

### Question 139
[MEDIUM-HARD]

What command shows the endpoints of a Service?

A) `kubectl get endpoints <service-name>`
B) `kubectl describe service <service-name>`
C) `kubectl get endpointslices -l kubernetes.io/service-name=<service-name>`
D) All of the above

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** All commands show endpoint information. `kubectl get endpoints` shows the Endpoints object directly. `kubectl describe service` includes endpoints in its output. `kubectl get endpointslices` shows the newer EndpointSlice objects.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 140
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

### Question 141
[MEDIUM]

What is the primary purpose of a ConfigMap?

A) To store sensitive data like passwords
B) To store non-sensitive configuration data
C) To configure network policies
D) To map containers to nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ConfigMaps store non-sensitive configuration data as key-value pairs. They decouple configuration from container images, allowing the same image to be used with different configurations. For sensitive data like passwords, use Secrets instead.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 142
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

### Question 143
[MEDIUM-HARD]

What is the key difference between ConfigMaps and Secrets?

A) Secrets are encrypted at rest by default
B) Secrets are base64 encoded and intended for sensitive data
C) ConfigMaps support larger data sizes
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Secrets are intended for sensitive data and are base64 encoded (not encrypted by default). They can be encrypted at rest if configured. ConfigMaps are for non-sensitive config. Both have the same size limit (~1MB). The main difference is semantic and security practices around each.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 144
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

### Question 145
[MEDIUM-HARD]

What happens when you update a ConfigMap that's mounted as a volume?

A) The Pod must be restarted to see changes
B) The mounted files are automatically updated (with delay)
C) The update fails
D) Only new Pods get the update

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a ConfigMap is mounted as a volume, updates are automatically propagated to the Pod (with a delay up to the kubelet sync period + cache TTL, typically around a minute). However, if using `subPath`, updates are NOT propagated.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 146
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

### Question 147
[MEDIUM-HARD]

How do you create a Secret from literal values?

A) `kubectl create secret generic my-secret --from-literal=password=mypass`
B) `kubectl create secret my-secret password=mypass`
C) `kubectl secret create --value=password:mypass`
D) Secrets can only be created from files

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Use `kubectl create secret generic <name> --from-literal=<key>=<value>` to create a Secret from literal values. You can specify multiple `--from-literal` flags. The values are automatically base64 encoded.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 148
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

### Question 149
[HARD]

What is the `immutable` field in ConfigMaps and Secrets used for?

A) To encrypt the data
B) To prevent any changes after creation
C) To lock the object for a specific time
D) To make data readable only by specific Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting `immutable: true` prevents any changes to the ConfigMap or Secret after creation. This improves performance (kubelet doesn't need to watch for changes) and protects against accidental modifications. The only way to update is to delete and recreate.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 150
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

### Question 151
[MEDIUM-HARD]

What is the maximum size of a ConfigMap or Secret?

A) 256 KB
B) 1 MB
C) 10 MB
D) No limit

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ConfigMaps and Secrets are limited to 1 MB (1048576 bytes) including all keys, values, and metadata. This limit exists because they're stored in etcd, which has per-object size limits. For larger data, use external storage.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 152
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

### Question 153
[MEDIUM-HARD]

How do you use a specific key from a ConfigMap as an environment variable?

A) `envFrom.configMapRef`
B) `env.valueFrom.configMapKeyRef`
C) `configMap.key`
D) It's not possible to use specific keys

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `env.valueFrom.configMapKeyRef` to inject a specific key as an environment variable. Specify `name` (ConfigMap name) and `key` (the key to use). This differs from `envFrom` which imports all keys.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 154
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

### Question 155
[HARD]

You mount a ConfigMap as a volume. What permissions do the files have by default?

A) 0644 (rw-r--r--)
B) 0755 (rwxr-xr-x)
C) 0600 (rw-------)
D) Depends on the container's umask

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** ConfigMap files are mounted with 0644 permissions by default. You can change this using `defaultMode` in the volume spec or `mode` for individual items. Secret files default to 0644 as well, though 0400 is often recommended for secrets.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 156
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

### Question 157
[HARD]

What happens to existing files in a directory when you mount a ConfigMap volume there?

A) They're preserved alongside ConfigMap files
B) They're hidden/overwritten by the mount
C) The mount fails
D) They're deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Mounting a volume (including ConfigMap) at a path overwrites/hides any existing files at that path. To add ConfigMap files without hiding existing content, use `subPath` for each file, but note this disables automatic updates.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 158
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

### Question 159
[MEDIUM-HARD]

How do you reference a Secret for pulling private container images?

A) Mount the Secret as a volume
B) Use `imagePullSecrets` in the Pod spec
C) Set environment variables
D) Add credentials to the container command

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `imagePullSecrets` in the Pod spec (or ServiceAccount) to reference docker-registry Secrets. Kubernetes uses these credentials to authenticate with private registries when pulling images. Example: `imagePullSecrets: [{name: my-registry-secret}]`.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 160
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

### Question 161
[MEDIUM-HARD]

How can you prevent a ConfigMap from being accidentally deleted?

A) Set `deletionProtection: true`
B) Use finalizers or RBAC restrictions
C) Mark it as immutable
D) Kubernetes has no built-in deletion protection

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes doesn't have built-in deletion protection (no `deletionProtection` field). RBAC can restrict who can delete ConfigMaps. Finalizers or admission webhooks can also block deletion. Note: `immutable: true` prevents updates to the ConfigMap but does NOT prevent deletion—the ConfigMap can still be deleted.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 162
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

### Question 163
[MEDIUM-HARD]

Which commands can update a ConfigMap in place?

A) `kubectl update configmap`
B) `kubectl edit configmap <name>`
C) `kubectl set configmap`
D) Both B and `kubectl apply -f <updated-manifest>`

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Multiple methods work: `kubectl edit configmap <name>` opens an editor for interactive changes. `kubectl apply -f` with an updated manifest updates declaratively. `kubectl patch` can also modify specific fields. There's no `kubectl update` or `kubectl set configmap` command.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 164
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

### Question 165
[MEDIUM-HARD]

What is the purpose of `kubernetes.io/tls` Secret type?

A) To enable TLS between Pods
B) To store TLS certificate and private key
C) To configure network encryption
D) To store CA certificates only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubernetes.io/tls` Secrets store TLS certificates. They must contain `tls.crt` (certificate) and `tls.key` (private key). Often used with Ingress controllers for HTTPS. Create with `kubectl create secret tls <name> --cert=<path> --key=<path>`.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 166
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

### Question 167
[MEDIUM-HARD]

Can you create a ConfigMap with binary data?

A) No, ConfigMaps are text only
B) Yes, using the `binaryData` field
C) Yes, by storing raw binary in the `data` field
D) Binary data is not supported in ConfigMaps

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ConfigMaps support binary data via the `binaryData` field, which stores base64-encoded content. The `data` field is strictly for UTF-8 text strings. When creating ConfigMaps from binary files, kubectl automatically uses `binaryData`. You cannot store raw binary in `data`—it must be valid UTF-8.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 168
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

### Question 169
[MEDIUM-HARD]

How do you list all ConfigMaps in a namespace?

A) `kubectl get cm`
B) `kubectl get configmaps`
C) `kubectl list configmaps`
D) Both A and B

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Both `kubectl get cm` and `kubectl get configmaps` work—`cm` is the short name. Use `-n <namespace>` to specify a namespace or `--all-namespaces` for all. Add `-o yaml` or `-o json` for full details.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 170
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

### Question 171
[MEDIUM]

What is the purpose of namespaces in Kubernetes?

A) To separate network traffic
B) To organize and isolate resources logically
C) To set resource limits
D) To enable multi-tenancy automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Namespaces provide logical isolation and organization for resources. They allow multiple teams or projects to share a cluster. Namespaces don't provide network isolation by default (need NetworkPolicies for that) or automatic multi-tenancy, but they're foundational for both.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 172
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

### Question 173
[MEDIUM-HARD]

What are the default namespaces created in a new Kubernetes cluster?

A) `default` only
B) `default`, `kube-system`, `kube-public`
C) `default`, `kube-system`, `kube-public`, `kube-node-lease`
D) No namespaces are created by default

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Four namespaces are created by default: `default` (for user resources without a namespace), `kube-system` (system components), `kube-public` (publicly readable resources), and `kube-node-lease` (node heartbeat leases).

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 174
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

### Question 175
[HARD]

Can a Pod in one namespace access a Service in another namespace?

A) No, namespaces provide network isolation by default
B) Yes, using the full DNS name `<service>.<namespace>.svc.cluster.local`
C) Only with a NetworkPolicy allowing it
D) Only through an Ingress

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, Kubernetes networking is flat—Pods can access Services across namespaces using the full DNS name. Note: while cross-namespace access is possible, Services can only SELECT Pods in their own namespace. NetworkPolicies can be applied to restrict cross-namespace traffic.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 176
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

### Question 177
[MEDIUM]

What is the difference between labels and annotations?

A) Labels are for large data, annotations for small
B) Labels are used for selection/filtering, annotations for non-identifying metadata
C) Labels are immutable, annotations are mutable
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Labels are for identifying/selecting resources (used by selectors). Annotations are for non-identifying metadata that isn't used for selection—like build info, tool configurations, or human-readable descriptions. Both are key-value pairs.

**Source:** [Annotations | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

**Source:** [Annotations | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

</details>

---

### Question 178
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

### Question 179
[MEDIUM-HARD]

How do you select all Pods with label `app=frontend` using kubectl?

A) `kubectl get pods -l app=frontend`
B) `kubectl get pods --selector=app:frontend`
C) `kubectl get pods --filter app=frontend`
D) `kubectl get pods -s app=frontend`

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Use `kubectl get pods -l app=frontend` or `--selector=app=frontend`. The `-l` flag accepts equality (`=`, `!=`) and set-based (`in`, `notin`) selectors. Example: `-l 'app in (frontend, backend),env!=test'`.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 180
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

### Question 181
[MEDIUM-HARD]

How do you add a label to an existing Pod?

A) `kubectl set label pod <name> key=value`
B) `kubectl label pod <name> key=value`
C) `kubectl annotate pod <name> key=value`
D) `kubectl tag pod <name> key=value`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl label <resource-type> <name> <key>=<value>` to add or update labels. To remove a label, use `kubectl label <resource-type> <name> <key>-` (with trailing minus). Use `--overwrite` to change existing labels.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 182
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

### Question 183
[HARD]

What is the difference between `matchLabels` and `matchExpressions` in a selector?

A) No difference, they're aliases
B) `matchLabels` is equality-based, `matchExpressions` allows set-based expressions
C) `matchLabels` is for Pods, `matchExpressions` is for Services
D) `matchExpressions` is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `matchLabels` uses simple equality matching (`key: value`). `matchExpressions` allows set-based expressions with operators (`key`, `operator`, `values`). Both can be used together—all conditions must match (AND logic).

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 184
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

### Question 185
[HARD]

What happens when you change a Pod's labels to no longer match its ReplicaSet's selector?

A) The Pod is deleted
B) The Pod is orphaned; ReplicaSet creates a new Pod
C) The ReplicaSet selector updates automatically
D) An error occurs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If a Pod's labels are changed so they no longer match the ReplicaSet's selector, the ReplicaSet stops managing that Pod (orphaned). The ReplicaSet then creates a new Pod to maintain the desired replica count. The orphaned Pod continues running independently.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 186
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

### Question 187
[MEDIUM-HARD]

How do you see all labels on a resource?

A) `kubectl get <resource> --show-labels`
B) `kubectl describe <resource>`
C) `kubectl labels <resource>`
D) Both A and B

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** `kubectl get <resource> --show-labels` shows labels in the output columns. `kubectl describe <resource>` shows labels in the detailed description. Use `-o yaml` or `-o json` for the complete label set programmatically.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 188
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

### Question 189
[MEDIUM-HARD]

What is a ResourceQuota used for?

A) To quote resources for billing
B) To limit aggregate resource usage in a namespace
C) To allocate resources to specific Pods
D) To track resource utilization

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota limits total resource consumption in a namespace—like total CPU, memory, number of Pods, Services, etc. When a quota is set, resource requests become mandatory for Pods, and requests exceeding available quota are rejected.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 190
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

### Question 191
[HARD]

What is the `Exists` operator in set-based selectors?

A) Checks if the resource exists
B) Matches resources that have the specified label key (any value)
C) Checks if the namespace exists
D) Matches resources that exist in etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `Exists` operator matches resources that have the specified label key, regardless of its value. Example: `{key: "tier", operator: "Exists"}` matches any resource with a `tier` label, whether it's `tier=frontend`, `tier=backend`, or any other value.

**Source:** [Labels and Selectors | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

</details>

---

### Question 192
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

### Question 193
[MEDIUM-HARD]

What annotation is often used to describe a resource's purpose?

A) `description`
B) `kubernetes.io/description`
C) `meta.helm.sh/description` or custom annotations
D) Annotations shouldn't be used for descriptions

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** There's no standard description annotation. Tools like Helm use their own (e.g., `meta.helm.sh/release-name`). Teams often use custom annotations like `description` or `app.kubernetes.io/description` for human-readable descriptions.

**Source:** [Annotations | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

</details>

---

### Question 194
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

### Question 195
[MEDIUM-HARD]

How do you set the default namespace for your kubectl context?

A) `kubectl config set-default-namespace <name>`
B) `kubectl config set-context --current --namespace=<name>`
C) `kubectl namespace set <name>`
D) `kubectl use-namespace <name>`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl config set-context --current --namespace=<namespace>` to set the default namespace for your current context. After this, commands without `-n` use this namespace. Verify with `kubectl config view --minify | grep namespace`.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 196
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

### Question 197
[MEDIUM-HARD]

What command shows resources across all namespaces?

A) `kubectl get <resource> --all`
B) `kubectl get <resource> --all-namespaces`
C) `kubectl get <resource> -A`
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Both `--all-namespaces` and its short form `-A` show resources across all namespaces. Example: `kubectl get pods -A` lists Pods from every namespace. The output includes a NAMESPACE column.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 198
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

### Question 199
[MEDIUM-HARD]

How do you list all namespaces?

A) `kubectl get namespaces`
B) `kubectl get ns`
C) `kubectl namespaces list`
D) Both A and B

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Both `kubectl get namespaces` and `kubectl get ns` (short form) list all namespaces. Add `--show-labels` to see namespace labels or `-o yaml` for full details.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 200
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
