# Kubernetes Core Concepts - 100 MCQ Questions (Part A)

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

### Question 3
[MEDIUM]

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

### Question 4
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

### Question 5
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

### Question 6
[MEDIUM]

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

### Question 7
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

### Question 8
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

### Question 9
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

### Question 10
[MEDIUM-HARD]

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

### Question 11
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

### Question 12
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

### Question 13
[MEDIUM-HARD]

What is the effect of setting `shareProcessNamespace: true` in a Pod spec?

A) Containers share CPU resources equally
B) Containers can see and signal each other's processes
C) Each container gets its own PID namespace
D) Container networking is disabled

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `shareProcessNamespace: true`, all containers in the Pod share a single process namespace. This means containers can see and signal each other's processes. The pause container becomes PID 1, and all container processes are visible across the shared namespace. This is useful for debugging or process monitoring sidecars.

**Source:** [Share Process Namespace | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/share-process-namespace/)

</details>

---

### Question 14
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

### Question 15
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

### Question 16
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

### Question 17
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

### Question 18
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

### Question 19
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

### Question 20
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

### Question 21
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

### Question 22
[MEDIUM-HARD]

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

### Question 23
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

### Question 24
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

### Question 25
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

## Deployments & ReplicaSets

### Question 26
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

### Question 27
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

### Question 28
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

### Question 29
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

### Question 30
[MEDIUM-HARD]

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

### Question 31
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

### Question 32
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

### Question 33
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

### Question 34
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

### Question 35
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

### Question 36
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

### Question 37
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

### Question 38
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

### Question 39
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

### Question 40
[MEDIUM-HARD]

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

### Question 41
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

### Question 42
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

### Question 43
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

### Question 44
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

### Question 45
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

### Question 46
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

### Question 47
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

### Question 48
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

### Question 49
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

### Question 50
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

## Services

### Question 51
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

### Question 52
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

### Question 53
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

### Question 54
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

### Question 55
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

### Question 56
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

### Question 57
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

### Question 58
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

### Question 59
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

### Question 60
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

### Question 61
[MEDIUM-HARD]

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

### Question 62
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

### Question 63
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

### Question 64
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

### Question 65
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

### Question 66
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

### Question 67
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

### Question 68
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

### Question 69
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

### Question 70
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

## ConfigMaps & Secrets

### Question 71
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

### Question 72
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

### Question 73
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

### Question 74
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

### Question 75
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

### Question 76
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

### Question 77
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

### Question 78
[MEDIUM-HARD]

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

### Question 79
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

### Question 80
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

### Question 81
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

### Question 82
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

### Question 83
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

### Question 84
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

### Question 85
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

## Namespaces, Labels & Selectors

### Question 86
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

### Question 87
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

### Question 88
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

### Question 89
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

### Question 90
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

### Question 91
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

### Question 92
[MEDIUM-HARD]

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

### Question 93
[MEDIUM-HARD]

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

### Question 94
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

### Question 95
[MEDIUM-HARD]

What is a ResourceQuota used for?

A) To quote resources for billing
B) To limit aggregate resource usage in a namespace
C) To allocate resources to specific Pods
D) To track resource utilization

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota limits total resource consumption in a namespace—like total CPU, memory, number of Pods, Services, etc. If the quota includes CPU/memory requests or limits, Pods must specify those fields; otherwise only the counted resources are enforced. Requests exceeding available quota are rejected.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 96
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

### Question 97
[MEDIUM-HARD]

What annotation is often used to describe a resource's purpose?

A) `description`
B) `kubernetes.io/description`
C) There is no standard; teams use custom annotations (e.g., `description`)
D) Annotations shouldn't be used for descriptions

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** There's no standard description annotation. Teams often use custom annotations like `description` for human-readable metadata.

**Source:** [Annotations | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

</details>

---

### Question 98
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

### Question 99
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

### Question 100
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
