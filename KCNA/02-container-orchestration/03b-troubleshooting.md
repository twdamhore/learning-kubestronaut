# Troubleshooting - 100 MCQ Questions (Part B: Q1-100)

**Domain:** Container Orchestration (28%)
**Competency:** Troubleshooting
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## Pod Status and Lifecycle Issues

### Question 1
[MEDIUM]

What does the "Completed" status indicate for a Pod?

A) The Pod crashed and cannot restart
B) All containers in the Pod exited with exit code 0
C) The Pod is waiting for resources
D) The Pod has been marked for deletion

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod shows "Completed" status when all its containers have successfully terminated with exit code 0. This is common for Job Pods that run batch workloads. The Pod remains in this state until garbage collected or manually deleted.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 2
[MEDIUM]

Which field in Pod spec determines how many times a container restarts before giving up?

A) restartLimit
B) backoffLimit
C) restartPolicy only controls restart behavior, not count
D) maxRestartCount

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `restartPolicy` field (Always, OnFailure, Never) controls whether containers restart but doesn't limit the count. Kubernetes uses exponential backoff for restarts but doesn't stop after a fixed count. For Jobs, `backoffLimit` controls total Pod retry count, not container restarts.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#restart-policy)

</details>

---

### Question 3
[MEDIUM-HARD]

A Pod shows status "Unknown". What is the most likely cause?

A) The container image doesn't exist
B) Node running the Pod has lost contact with the control plane
C) The Pod spec is invalid
D) ResourceQuota is exceeded

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Unknown" status typically means the node running the Pod cannot be contacted. This occurs when the node loses network connectivity, crashes, or the kubelet stops reporting. The control plane cannot determine the actual Pod state, so it reports Unknown.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-phase)

</details>

---

### Question 4
[MEDIUM-HARD]

What happens to Pods in "Pending" state when the node they were scheduled to is removed?

A) They automatically move to another node
B) They stay bound to the removed node until eviction or deletion
C) They are immediately rescheduled by the scheduler
D) They immediately fail and need recreation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Once a Pod has `spec.nodeName` set, the scheduler does not reschedule it. When the node is removed, the node controller detects the node is gone and applies taints after timeouts. The Pod stays bound until evicted or deleted. Controllers (Deployment, StatefulSet) then create replacement Pods which get scheduled to healthy nodes.

**Source:** [Node Controller | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/#node-controller)

</details>

---

### Question 5
[HARD]

A Pod with `restartPolicy: Never` transitions directly from "Pending" to "Failed" without ever being "Running". Which scenario causes this?

A) Image pull failure after multiple retries
B) Init container exits with non-zero code before main container starts
C) Node pressure eviction
D) Container OOMKilled

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When an init container fails (exits with non-zero code) and the Pod has `restartPolicy: Never`, the Pod transitions to Failed without the main containers ever running. With other restart policies (Always or OnFailure), a failed init container would be retried instead of causing immediate Pod failure. Image pull failures keep the Pod in Pending. Node pressure eviction and OOMKill require the container to be running first.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

---

### Question 6
[HARD]

What is the significance of the "deletionTimestamp" field on a Pod object?

A) When the Pod was created
B) When the Pod will be forcefully deleted regardless of state
C) The Pod has been requested for deletion and is in termination
D) Scheduled time for Pod restart

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `deletionTimestamp` is set when a delete request is received. The Pod enters "Terminating" state and begins graceful shutdown. Containers receive SIGTERM, and after `terminationGracePeriodSeconds`, remaining processes get SIGKILL. The field indicates deletion is in progress, not a forced deletion time.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination)

</details>

---

### Question 7
[HARD]

How does Kubernetes handle a Pod whose container continuously exits with code 0 when restartPolicy is "Always"?

A) Stops restarting after backoffLimit
B) Keeps restarting with exponential backoff
C) Marks Pod as Completed
D) Removes the Pod from the cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `restartPolicy: Always`, Kubernetes restarts containers regardless of exit code. Even exit code 0 triggers a restart. The backoff delay increases exponentially (10s, 20s, 40s... up to 5 minutes) and resets after 10 minutes of successful running. This continues indefinitely.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#restart-policy)

</details>

---

### Question 8
[HARD]

A multi-container Pod shows all containers as "Waiting" with reason "PodInitializing". What does this indicate?

A) Main containers failed to start
B) Init containers are still running or haven't completed yet
C) The Pod is being deleted
D) Image pull is in progress for main containers only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "PodInitializing" in Waiting state indicates init containers are still running or haven't completed successfully. All main containers remain in this state until every init container completes with exit code 0. Once all init containers finish, main containers start simultaneously. Check init container status with `kubectl describe pod`.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/#understanding-init-containers)

</details>

---

### Question 9
[HARD]

What determines the order of container termination when a Pod is deleted?

A) Reverse order of container definition
B) Alphabetical by container name
C) All containers receive SIGTERM simultaneously
D) Based on resource consumption

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a Pod is deleted, all containers receive SIGTERM at the same time - there's no defined order. Each container then has `terminationGracePeriodSeconds` to shut down gracefully. Containers that need ordered shutdown must implement their own coordination mechanism.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination)

</details>

---

### Question 10
[HARD]

A Pod's container keeps restarting after receiving SIGKILL but shows no OOMKilled events. What should you investigate?

A) Syntax error in container command
B) Container not terminating within terminationGracePeriodSeconds, or external SIGKILL
C) Container reached CPU limit
D) Network timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** SIGKILL without OOMKilled events occurs when: the container doesn't terminate gracefully within `terminationGracePeriodSeconds` during Pod deletion (kubelet sends SIGKILL after SIGTERM timeout), or an external process sends SIGKILL. Check Pod termination settings and investigate if the application handles SIGTERM properly.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination)

</details>

---

## Debugging Commands and Techniques

### Question 11
[MEDIUM]

What is the purpose of `kubectl debug` with the `--copy-to` flag?

A) Copy logs to a file
B) Create a copy of the Pod with modified containers for debugging
C) Copy the Pod to another node
D) Backup the Pod specification

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl debug --copy-to` creates a copy of a Pod with modifications for debugging, such as adding a debug container or changing the image to include debugging tools. The original Pod remains unaffected, allowing safe debugging without disrupting the running workload.

**Source:** [Debugging Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#copying-a-pod-while-changing-its-command)

</details>

---

### Question 12
[MEDIUM]

How do you view the YAML manifest of a running Pod including runtime fields?

A) kubectl get pod <name> --show-all
B) kubectl get pod <name> -o yaml
C) kubectl describe pod <name> --yaml
D) kubectl export pod <name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl get pod <name> -o yaml` outputs the full Pod specification including status, conditions, and all runtime fields. This shows the complete object as stored in etcd, useful for seeing current state, assigned node, IP addresses, and container statuses.

**Source:** [kubectl Cheat Sheet | Kubernetes](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

</details>

---

### Question 13
[MEDIUM-HARD]

What does `kubectl logs --previous` display?

A) Logs from the previous Pod version
B) Logs from the last terminated container instance
C) Logs from yesterday
D) Logs from the previous namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl logs --previous` retrieves logs from the previously terminated instance of a container. This is essential for debugging crash loops, as it shows what happened in the container before it crashed and restarted. Only the immediately previous instance's logs are available.

**Source:** [Debugging Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#examine-pod-logs)

</details>

---

### Question 14
[MEDIUM-HARD]

How do you execute a command in a specific container of a multi-container Pod?

A) kubectl exec <pod> -- <command>
B) kubectl exec <pod> -c <container> -- <command>
C) kubectl run <container> -- <command>
D) kubectl exec <pod>/<container> -- <command>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `-c` or `--container` flag to specify which container to execute commands in: `kubectl exec <pod> -c <container> -- <command>`. Without this flag in a multi-container Pod, kubectl targets the first container by default, which may not be the one you need.

**Source:** [Get a Shell to a Running Container | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)

</details>

---

### Question 15
[HARD]

What is the difference between `kubectl debug` with `--target` versus `--share-processes`?

A) They are the same option with different names
B) --target joins container's namespace; --share-processes enables process namespace sharing at Pod level
C) --target specifies node; --share-processes copies processes
D) --share-processes is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--target` makes the ephemeral container join an existing container's namespace, allowing it to see that container's processes. `--share-processes` enables Pod-level process namespace sharing, letting all containers see each other's processes. They serve different debugging scenarios.

**Source:** [Debugging Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#ephemeral-container)

</details>

---

### Question 16
[HARD]

How do you collect Pod logs that span multiple restarts during a crash loop?

A) kubectl logs --all-restarts
B) You cannot - only current and previous instance logs are available via kubectl
C) kubectl logs --since-restart=all
D) kubectl logs --history

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kubectl can only retrieve logs from the current container instance and one previous instance (`--previous`). For logs spanning multiple restarts, you need external log aggregation (Fluentd, Loki) that captures logs before container termination, or check node-level log files if available.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 17
[HARD]

What does `kubectl get events --field-selector reason=FailedScheduling` show?

A) All Pod events
B) Only events where Pods could not be scheduled
C) Node failure events
D) Network scheduling failures

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field selectors filter events by specific fields. `reason=FailedScheduling` shows only events where the scheduler couldn't place a Pod. This is useful for quickly identifying scheduling problems across the cluster without wading through unrelated events.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 18
[HARD]

How can you debug a container that crashes immediately on startup before you can exec into it?

A) Use kubectl logs only
B) Modify the Pod command to sleep infinity, then exec in
C) Wait for the container to become stable
D) Use kubectl attach immediately

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For containers that crash before you can investigate, override the entrypoint with a sleep command: `kubectl debug <pod> --copy-to=debug-pod --container=app -- sleep infinity`. This keeps the container running so you can exec in and manually run commands to diagnose the issue.

**Source:** [Debugging Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#copying-a-pod-while-changing-its-command)

</details>

---

### Question 19
[HARD]

What information does `kubectl get pod -o wide` provide that standard output doesn't?

A) Full YAML specification
B) Node name, IP address, nominated node, and readiness gates
C) Container logs
D) Event history

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `-o wide` flag adds columns: NODE (which node the Pod runs on), IP (Pod IP address), NOMINATED NODE (for preemption), and READINESS GATES. This information is essential for network troubleshooting and understanding Pod placement without running describe.

**Source:** [kubectl Cheat Sheet | Kubernetes](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

</details>

---

### Question 20
[HARD]

How do you debug a node using `kubectl debug node`?

A) It SSHs into the node
B) It creates a privileged Pod with host namespaces and root filesystem mounted
C) It shows node logs
D) It restarts kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl debug node/<name>` creates a privileged Pod on that node with host namespaces (PID, network, IPC) and the node's root filesystem mounted at `/host`. This allows inspecting node-level processes, files, and system state without SSH access, using familiar container tools.

**Source:** [Debugging Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#debugging-via-a-shell-on-the-node)

</details>

---

## Node and Cluster Troubleshooting

### Question 21
[MEDIUM]

What does the "DiskPressure" condition on a node indicate?

A) Network connectivity issues
B) Node's disk capacity or inodes are running low
C) CPU overload
D) Memory pressure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DiskPressure condition becomes True when available disk space or inodes fall below kubelet eviction thresholds (configurable; defaults vary for nodefs and imagefs). This triggers Pod eviction based on disk usage. Monitor with `kubectl describe node` and check Conditions section.

**Source:** [Node-pressure Eviction | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/)

</details>

---

### Question 22
[MEDIUM]

How do you safely remove a node from the cluster for maintenance?

A) kubectl delete node <name>
B) kubectl drain <name> followed by maintenance, then kubectl uncordon
C) Simply shut down the node
D) kubectl remove node <name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl drain <node>` to safely evict Pods and mark the node unschedulable. After maintenance, `kubectl uncordon <node>` allows new Pod scheduling. Direct delete removes the node object but doesn't gracefully migrate workloads, potentially causing disruption.

**Source:** [Safely Drain a Node | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)

</details>

---

### Question 23
[MEDIUM-HARD]

What causes a node to show "NotReady" status?

A) Too many Pods scheduled
B) Kubelet stopped reporting, network issues, or critical node conditions
C) High CPU usage only
D) Pending Pod deployments

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NotReady status occurs when: kubelet stops sending heartbeats (after `node-monitor-grace-period`, default 40s), or node loses network connectivity to control plane. Note: Pressure conditions (MemoryPressure, DiskPressure, PIDPressure) are separate from Ready status - a node can be Ready while under pressure.

**Source:** [Node | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/#node-status)

</details>

---

### Question 24
[MEDIUM-HARD]

How do you view kubelet logs on a node using systemd?

A) kubectl logs kubelet
B) journalctl -u kubelet on the node
C) cat /var/log/kubelet.log
D) kubectl describe node --logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** On systemd-based systems, kubelet logs are accessed via `journalctl -u kubelet`. Add `-f` for following logs or `--since` for time filtering. This requires node access (SSH or kubectl debug node). The log location varies by installation method.

**Source:** [Troubleshooting kubeadm | Kubernetes](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/)

</details>

---

### Question 25
[HARD]

A node shows Ready but Pods report "NodeNotReady" mount errors. What is likely wrong?

A) Node doesn't exist
B) Kubelet volume plugin or CSI driver has issues
C) Network plugin failure
D) All of the above could cause this

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The node can be Ready (kubelet responsive) while volume operations fail. Mount errors suggest kubelet volume plugin or CSI driver problems. Check CSI driver Pods are healthy, CSI node plugin logs, and kubelet logs for volume-related errors: `journalctl -u kubelet | grep -i volume`.

**Source:** [Troubleshooting | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/)

</details>

---

### Question 26
[HARD]

What is the effect of `kubectl cordon` on existing Pods running on the node?

A) Immediately evicts all Pods
B) No effect on existing Pods; only prevents new scheduling
C) Terminates non-critical Pods
D) Restarts all Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cordon` marks a node as unschedulable by setting `spec.unschedulable: true` on the node object (not a taint). This prevents the scheduler from placing new Pods on the node but doesn't affect running Pods. Existing workloads continue running until explicitly evicted with `kubectl drain` or until Pods terminate naturally.

**Source:** [Safely Drain a Node | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)

</details>

---

### Question 27
[HARD]

How does the node controller determine when to evict Pods from an unreachable node?

A) Immediately upon NotReady status
B) After pod-eviction-timeout (default 5 minutes) of NotReady
C) Based on Pod priority only
D) Never automatically evicts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The node controller waits for `pod-eviction-timeout` (default 5 minutes) after a node becomes NotReady before evicting Pods. This prevents unnecessary churn from transient network issues. With taint-based eviction, tolerations on Pods can extend this timeout.

**Source:** [Node | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/#node-controller)

</details>

---

### Question 28
[HARD]

A node has "NetworkUnavailable" condition True. What component is responsible for clearing this condition?

A) Kubelet
B) Cloud controller manager (route controller) or the CNI plugin
C) kube-proxy
D) API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The NetworkUnavailable condition is typically cleared by the cloud controller manager's route controller (which sets up node routes) or by some CNI plugins that manage this condition directly. The kubelet initially sets this condition to True, and it's cleared once networking is properly configured. If this stays True, check cloud-controller-manager logs, CNI plugin status, and node route configuration.

**Source:** [Node Conditions | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/#condition)

</details>

---

### Question 29
[HARD]

What happens to static Pods on a node when the API server is unreachable?

A) They are immediately deleted
B) They continue running as kubelet manages them directly
C) They enter Unknown state
D) They restart continuously

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static Pods are managed directly by kubelet from manifest files, not by the API server. They continue running even if the control plane is unreachable. The mirror Pods in the API server may show stale status, but actual static Pods remain unaffected.

**Source:** [Static Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/)

</details>

---

### Question 30
[HARD]

What does high "node-lease" renewal latency indicate?

A) Network latency between kubelet and API server
B) etcd performance issues
C) Either A or B, as leases go through API server to etcd
D) Pod scheduling delays

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Node lease renewal requires kubelet to update a Lease object via the API server, which writes to etcd. High latency could indicate network issues between kubelet and API server, or etcd performance problems (disk I/O, compaction). Monitor both layers when troubleshooting.

**Source:** [Node | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/#heartbeats)

</details>

---

## Network and Service Troubleshooting

### Question 31
[MEDIUM]

Why might a Service not be reachable even when endpoints exist?

A) Wrong selector
B) kube-proxy not running or iptables rules not created
C) No Pods available
D) Service doesn't exist

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With valid endpoints, Service unreachability suggests kube-proxy issues. kube-proxy creates iptables/IPVS rules for traffic routing. Check `kubectl logs -n kube-system kube-proxy-<pod>` and verify iptables rules with `iptables -L -t nat | grep <service>` on the node.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 32
[MEDIUM]

How do you verify if a Service selector matches any Pods?

A) kubectl describe service
B) kubectl get endpoints <service-name>
C) kubectl get pods --show-labels
D) Both A and B work, but B shows actual Pod IPs

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** `kubectl describe service` shows selector and endpoint IPs. `kubectl get endpoints <service-name>` directly shows which Pod IPs are registered as endpoints. If endpoints list is empty, the selector doesn't match any Ready Pods. Both work, but endpoints show concrete addresses.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 33
[MEDIUM-HARD]

A Pod can reach other Pods by IP but not by Service DNS name. What should you check?

A) Pod's network configuration
B) CoreDNS Pods and Service
C) Kube-proxy logs
D) Firewall rules only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If Pod-to-Pod IP connectivity works but DNS fails, the issue is DNS resolution. Check: CoreDNS Pods running (`kubectl get pods -n kube-system -l k8s-app=kube-dns`), CoreDNS Service has endpoints, and the Pod's `/etc/resolv.conf` points to CoreDNS ClusterIP.

**Source:** [Debugging DNS Resolution | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/)

</details>

---

### Question 34
[MEDIUM-HARD]

What causes a NodePort Service to be unreachable from outside the cluster?

A) Wrong Service type
B) Firewall blocking the NodePort, node network issues, or kube-proxy not routing
C) Pod not running
D) Incorrect ClusterIP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** External NodePort access requires: the port (30000-32767 range) open in firewalls/security groups, kube-proxy running to handle traffic, and network path to node IPs. Check cloud provider security groups, host firewall (iptables), and kube-proxy logs.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport)

</details>

---

### Question 35
[HARD]

How do you test if a Pod can reach a Service without relying on DNS?

A) ping the Service
B) Use Service ClusterIP directly: curl http://<cluster-ip>:<port>
C) Check iptables rules
D) Restart kube-proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To bypass DNS, curl the Service's ClusterIP directly from within a Pod: `kubectl exec <pod> -- curl http://<clusterIP>:<port>`. This isolates network connectivity from DNS issues. If ClusterIP works but DNS doesn't, focus on CoreDNS troubleshooting.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 36
[HARD]

What does an empty "Subsets" field in Endpoints indicate?

A) Service is healthy
B) No Pods match the selector or no Pods are Ready
C) Endpoints object is corrupted
D) Service uses ExternalName type

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Empty Subsets means no endpoints are registered. This occurs when: selector matches no Pods, matched Pods aren't Ready (failing readiness probes), or Pods haven't started. ExternalName Services don't use endpoints at all - they rely on DNS CNAME.

**Source:** [Endpoints | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#endpoints)

</details>

---

### Question 37
[HARD]

How does `publishNotReadyAddresses: true` on a Service affect endpoint registration?

A) No effect
B) Pods are added to endpoints even if not Ready
C) Publishes the Service to external DNS
D) Enables headless mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, only Ready Pods appear in endpoints. Setting `publishNotReadyAddresses: true` includes all matched Pods regardless of readiness. This is useful for StatefulSets where Pods need to discover each other during initialization before becoming Ready.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#headless-services)

</details>

---

### Question 38
[HARD]

A Service shows "EXTERNAL-IP: Pending" indefinitely. What's the most likely cause?

A) Service type is wrong
B) No cloud load balancer provisioner or controller running
C) DNS not configured
D) Service port conflict

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LoadBalancer type Services require a cloud provider or load balancer controller (like MetalLB for bare metal) to provision external IPs. Without one, EXTERNAL-IP stays Pending indefinitely. Check cloud-controller-manager logs or install a LoadBalancer implementation.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

</details>

---

### Question 39
[HARD]

How do you diagnose intermittent Service connectivity issues?

A) Check Service YAML
B) Investigate endpoint health, check for Pods cycling, verify CNI stability, and review kube-proxy rules
C) Restart all Pods
D) Recreate the Service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Intermittent issues suggest: some endpoints are unhealthy (check Pod logs/readiness), Pods are being rescheduled (check events), CNI has issues (check plugin logs), or iptables rules are flapping (check kube-proxy). Systematic investigation across these layers is needed.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 40
[HARD]

What is the effect of `internalTrafficPolicy: Local` on Service traffic?

A) Routes external traffic to local Pods
B) Restricts internal traffic to Pods on the same node as the client
C) Disables cross-node traffic completely
D) Enables mTLS for internal traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `internalTrafficPolicy: Local` routes cluster-internal traffic only to endpoints on the same node as the client Pod. If no local endpoints exist, traffic is dropped. This reduces latency and cross-node bandwidth but requires careful planning for endpoint availability.

**Source:** [Service Internal Traffic Policy | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service-traffic-policy/)

</details>

---

## Storage and Volume Troubleshooting

### Question 41
[MEDIUM]

What does a PVC status of "Pending" indicate?

A) PVC is being deleted
B) No PV matches the PVC requirements or dynamic provisioning hasn't completed
C) PVC is bound successfully
D) PVC has been successfully provisioned but not yet attached

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pending status means the PVC is waiting for a PV. This occurs when: no existing PV matches (size, access modes, storage class), dynamic provisioning is slow or failing, or the specified storage class doesn't exist. Check PVC events with `kubectl describe pvc`.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#phase)

</details>

---

### Question 42
[MEDIUM]

How do you check why a PV is not binding to a PVC?

A) kubectl get pv
B) kubectl describe pv <name> and check for capacity, access modes, and storage class match
C) kubectl logs pv
D) kubectl get events --all-namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe pv` shows capacity, access modes, storage class, and claim reference. Compare these with PVC requirements. Binding fails when: capacity is less than requested, access modes don't match, storage class differs, or PV is already bound to another PVC.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#binding)

</details>

---

### Question 43
[MEDIUM-HARD]

A Pod is stuck in "ContainerCreating" with event "FailedAttachVolume". What is the likely cause?

A) Image pull error
B) PV is attached to another node and the volume doesn't support multi-attach
C) Container configuration error
D) Network plugin failure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** FailedAttachVolume typically means the volume is still attached to another node. Most block storage (EBS, GCE PD) only supports single-node attachment. If a Pod moves nodes, the previous attachment must be released first. Check if another Pod or orphaned attachment exists.

**Source:** [Storage | Kubernetes](https://kubernetes.io/docs/concepts/storage/)

</details>

---

### Question 44
[MEDIUM-HARD]

What causes "FailedMount" with message "timeout expired waiting for volumes to attach"?

A) PVC doesn't exist
B) Volume attach operation taking too long, possibly due to cloud provider issues
C) Incorrect volume permissions
D) Container not starting

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** This timeout indicates the volume attachment isn't completing within expected time. Causes include: cloud provider API throttling or errors, CSI driver issues, volume stuck in attaching state on previous node. Check cloud provider console and CSI controller logs.

**Source:** [Storage | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 45
[HARD]

How do you troubleshoot CSI driver issues?

A) Check kubelet logs
B) Check CSI controller Pod logs, CSI node Pod logs, and kubelet logs
C) Restart all Pods
D) Recreate PVCs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CSI debugging requires checking multiple components: CSI controller (handles provisioning/attachment), CSI node Pods (handle mount/unmount on each node), and kubelet (interacts with CSI). Use `kubectl logs` for CSI Pods and `journalctl -u kubelet` for kubelet issues.

**Source:** [CSI | Kubernetes](https://kubernetes.io/docs/concepts/storage/volumes/#csi)

</details>

---

### Question 46
[HARD]

A PVC shows "Bound" but the Pod still shows "FailedMount" errors. What could cause this?

A) PVC binding issue
B) PV exists but underlying storage is unavailable, corrupted, or wrong filesystem type
C) Pod doesn't request the PVC
D) Service account missing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bound PVC means the Kubernetes binding succeeded, but actual storage might be problematic. Issues include: underlying storage deleted/corrupted, filesystem type mismatch, mount options invalid, or credentials expired. Check kubelet logs on the node for mount details.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 47
[HARD]

What is the purpose of the `volumeBindingMode: WaitForFirstConsumer` in a StorageClass?

A) Waits for manual PV creation
B) Delays PV provisioning until a Pod using the PVC is scheduled
C) Requires admin approval
D) Binds volume to first requesting namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `WaitForFirstConsumer` delays volume provisioning until a Pod requests the PVC. This ensures the volume is created in the same zone/region as the scheduled Pod, preventing zone mismatch issues. Without it, volumes might be provisioned in zones where no nodes can access them.

**Source:** [Storage Classes | Kubernetes](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode)

</details>

---

### Question 48
[HARD]

A volume shows "VolumeAttachment" stuck in attaching state. How do you force detach it?

A) Delete the Pod
B) Delete the VolumeAttachment object (use caution - may cause data corruption)
C) Restart kubelet
D) Scale Deployment to 0

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Force detaching requires deleting the VolumeAttachment object: `kubectl delete volumeattachment <name>`. Warning: this can cause data corruption if the volume is actually in use. Ensure the Pod is truly gone and the previous attachment is orphaned before force-deleting.

**Source:** [CSI | Kubernetes](https://kubernetes.io/docs/concepts/storage/volumes/#csi)

</details>

---

### Question 49
[HARD]

Why might a Pod fail with "subPath" related mount errors?

A) Container doesn't exist
B) SubPath refers to a non-existent path, symlink issues, or race condition during volume setup
C) Wrong image tag
D) Memory limit exceeded

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** SubPath errors occur when: the specified path doesn't exist in the volume, symlinks are used but subPathExpr isn't configured properly, or there's a race condition where the path is created after mount attempt. Ensure the path exists or use init containers to create it.

**Source:** [Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/volumes/#using-subpath)

</details>

---

### Question 50
[HARD]

How do you diagnose slow volume mount times?

A) Check Pod age
B) Examine CSI driver logs for slow operations, cloud provider latency, and node kubelet metrics
C) Increase timeout settings
D) Use faster storage class

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Slow mounts can be diagnosed by: checking CSI driver logs for operation timings, monitoring cloud provider API latency, examining kubelet volume manager metrics, and verifying filesystem creation time (formatting new volumes). Each stage can introduce delays.

**Source:** [Storage | Kubernetes](https://kubernetes.io/docs/concepts/storage/)

</details>

---

## Workload Controllers Troubleshooting

### Question 51
[MEDIUM]

What happens when a Deployment's selector is changed after creation?

A) Existing Pods are updated
B) Selector is immutable after creation; changes are rejected
C) New ReplicaSet is created
D) Deployment is deleted and recreated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `spec.selector` field of a Deployment is immutable after creation. Attempting to change it results in a validation error. This prevents orphaning existing Pods. To change selectors, you must delete and recreate the Deployment.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 52
[MEDIUM]

How do you pause a Deployment rollout to make multiple changes?

A) kubectl stop deployment
B) kubectl rollout pause deployment/<name>
C) Scale to 0 replicas
D) Edit the Deployment with --paused flag

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl rollout pause deployment/<name>` pauses the rollout, allowing multiple spec changes without triggering intermediate rollouts. After all changes, use `kubectl rollout resume deployment/<name>` to apply them in a single rollout.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#pausing-and-resuming-a-deployment)

</details>

---

### Question 53
[MEDIUM-HARD]

A StatefulSet Pod is stuck in Terminating state. What is blocking deletion?

A) Pod has active connections
B) Pod finalizers or stuck volume detach/unmount operations
C) Too many replicas
D) Node is healthy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSet Pods can get stuck in Terminating due to: Pod finalizers preventing deletion until conditions are met, or volume unmount/detach operations hanging (especially if the node is unreachable). Note: PVC finalizers prevent PVC deletion while in use, not Pod deletion. Check `kubectl get pod -o yaml` for finalizers and events.

**Source:** [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

</details>

---

### Question 54
[MEDIUM-HARD]

What does "ProgressDeadlineExceeded" reason in Deployment conditions mean?

A) Deployment was deleted
B) Rollout didn't complete within progressDeadlineSeconds
C) All replicas are ready
D) Deployment is paused

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `ProgressDeadlineExceeded` indicates the rollout didn't complete within `progressDeadlineSeconds` (default 600s). New Pods couldn't become Ready in time. This doesn't roll back automatically but marks the Deployment as failed. Investigate why Pods aren't becoming Ready.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#progress-deadline-seconds)

</details>

---

### Question 55
[HARD]

Why might a DaemonSet not schedule Pods on certain nodes?

A) Node doesn't exist
B) Node taints without matching tolerations, node selectors, or affinity rules
C) Too many DaemonSets
D) DaemonSet is paused

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets don't schedule Pods on nodes with: taints the DaemonSet doesn't tolerate, nodeSelector that doesn't match node labels, or node affinity rules excluding the node. Check `kubectl describe daemonset` for nodeSelector and tolerations, compare with node taints.

**Source:** [DaemonSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

</details>

---

### Question 56
[HARD]

A ReplicaSet shows desired replicas but actual is 0. What should you investigate first?

A) Check Service
B) Check Events on ReplicaSet for admission/quota failures, then check Pod template validity
C) Restart controller-manager
D) Delete the ReplicaSet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Zero actual replicas despite desired count indicates Pod creation is failing. Check ReplicaSet events for: ResourceQuota exceeded, LimitRange violations, admission webhook rejections, or invalid Pod template. `kubectl describe rs <name>` shows these creation failures.

**Source:** [ReplicaSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

</details>

---

### Question 57
[HARD]

How does StatefulSet handle a Pod that's stuck and not terminating?

A) Force deletes it
B) Waits indefinitely by default; won't create replacement on same ordinal
C) Creates duplicate Pod
D) Scales down automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSet maintains strict ordering and identity. If a Pod is stuck Terminating, StatefulSet won't create a replacement with the same ordinal to prevent duplicate identities. Manual intervention (force delete) may be needed. Consider `--force --grace-period=0` for stuck Pods.

**Source:** [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/#pod-management-policies)

</details>

---

### Question 58
[HARD]

What is the purpose of `.spec.minReadySeconds` in a Deployment?

A) Minimum time Pods must exist
B) Wait time after Pod becomes Ready before considering it Available
C) Minimum container runtime
D) Scheduling delay

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `minReadySeconds` specifies how long a new Pod must be Ready without any containers crashing before it's considered Available. This catches Pods that pass initial probes but crash shortly after. During rollout, progression waits for this period.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#min-ready-seconds)

</details>

---

### Question 59
[HARD]

A Job with parallelism=3 and completions=10 only runs 2 Pods. What might cause this?

A) Job completed
B) ResourceQuota limiting Pods, pending Pod failures, or node capacity constraints
C) Wrong parallelism setting
D) Job timeout exceeded

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Less than expected parallelism can be caused by: ResourceQuota limiting total Pods in namespace, insufficient cluster resources to schedule more Pods, or previous Pod failures counting toward backoffLimit. Check Job events, namespace quotas, and cluster capacity.

**Source:** [Jobs | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/job/)

</details>

---

### Question 60
[HARD]

How do you troubleshoot a Deployment stuck at "1 old replicas are pending termination"?

A) Check Service
B) Investigate the old Pod: check for finalizers, PreStop hooks, or termination grace period issues
C) Delete the Deployment
D) Scale to 0

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Pending termination" means the old Pod won't terminate. Check: finalizers blocking deletion, long PreStop hooks executing, long terminationGracePeriodSeconds, or stuck volume unmounts. Use `kubectl describe pod` on the terminating Pod to identify the block.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

## Configuration and Probes Troubleshooting

### Question 61
[MEDIUM]

What happens if a ConfigMap referenced by a Pod doesn't exist?

A) Pod uses default values
B) Pod fails to start with CreateContainerConfigError
C) ConfigMap is created automatically
D) Pod starts without the ConfigMap data

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If a required ConfigMap doesn't exist, the Pod cannot start and shows `CreateContainerConfigError` status. This applies to ConfigMaps mounted as volumes or used for environment variables. Mark ConfigMap reference as optional to allow Pod startup without it.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 62
[MEDIUM]

How do you make a Pod continue starting even if a ConfigMap is missing?

A) Use init containers
B) Set optional: true in the volume or envFrom configuration
C) Create an empty ConfigMap
D) Use default values in container

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Adding `optional: true` to the ConfigMap reference allows the Pod to start even if the ConfigMap doesn't exist. For volumes, add it to the configMap volume spec. For envFrom, add it to the configMapRef. Missing data simply isn't injected.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/#optional-configmaps)

</details>

---

### Question 63
[MEDIUM-HARD]

A Pod keeps restarting due to failed liveness probe but logs show the application is running fine. What's the likely issue?

A) Wrong container image
B) Liveness probe misconfigured: wrong port, path, or probe timing parameters
C) Memory leak
D) Network policy blocking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If the app runs but liveness probes fail, check probe configuration: correct port (container port, not host), correct path for HTTP probes, adequate initialDelaySeconds for slow-starting apps, and appropriate timeoutSeconds. Also verify the probe endpoint actually returns 200-399.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 64
[MEDIUM-HARD]

What is the difference between a Pod showing "Running" but with 0/1 Ready versus 1/1 Ready?

A) No difference
B) 0/1 means container is running but readiness probe is failing
C) 0/1 means container hasn't started
D) 0/1 means Pod is terminating

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Running with 0/1 Ready indicates the container is running but failing readiness probes. The Pod won't receive Service traffic until probes pass. This commonly occurs during application startup or when the app is unhealthy but not crashed.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes)

</details>

---

### Question 65
[HARD]

How do you debug probe failures when there are no obvious errors?

A) Remove the probes
B) Exec into container and manually test the probe endpoint/command
C) Restart the Pod
D) Increase all timeout values

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Manually test what the probe does: `kubectl exec <pod> -- curl localhost:<port>/<path>` for HTTP probes, or run the command for exec probes. This shows actual responses and errors. Check if the app binds to correct interface (localhost vs 0.0.0.0) and port.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 66
[HARD]

A Secret update doesn't reflect in a running Pod's environment variables. Why?

A) Secret is immutable
B) Environment variables are set at container start and don't update dynamically
C) Wrong Secret reference
D) RBAC blocking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Environment variables from Secrets/ConfigMaps are injected at container startup and don't update afterward. To see changes, the Pod must be restarted. For dynamic updates, mount Secrets as volumes - kubelet syncs volume contents periodically (kubelet sync period plus cache TTL, up to ~2 minutes by default).

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-environment-variables)

</details>

---

### Question 67
[HARD]

What causes ConfigMap keys to be skipped when using envFrom to set environment variables?

A) ConfigMap too large
B) Key names are not valid environment variable names (must start with letter/underscore, contain only alphanumerics/underscores)
C) Wrong namespace
D) ConfigMap is secret type

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When using `envFrom` to load all ConfigMap keys as environment variables, keys that are not valid env var names are skipped and a warning event is recorded (not a hard error). Valid env var names must start with a letter or underscore and contain only letters, digits, and underscores. When using `env` with `valueFrom.configMapKeyRef`, the env var name you explicitly specify must also be valid.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 68
[HARD]

How do startupProbe, livenessProbe, and readinessProbe interact during Pod startup?

A) They run simultaneously from start
B) startupProbe runs first; liveness and readiness only start after startup succeeds
C) Only one probe type can be defined
D) They are aliases for the same probe

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** startupProbe runs first for slow-starting containers. Until it succeeds, liveness and readiness probes are disabled. Once startup succeeds, it's disabled and liveness/readiness take over. This prevents liveness probes from killing slow-starting apps.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes)

</details>

---

### Question 69
[HARD]

A gRPC probe is failing but the gRPC service works fine when tested manually. What might be wrong?

A) gRPC not supported
B) The health checking protocol implementation might be missing or the service name is incorrect
C) Wrong port
D) TLS required

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes gRPC probes use the standard gRPC Health Checking Protocol. The application must implement this protocol and respond to health check requests. If only the main service works but health checks fail, the health service implementation is missing or the service name in the probe is wrong.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-grpc-liveness-probe)

</details>

---

### Question 70
[HARD]

How do you troubleshoot a Pod that restarts exactly at the same interval repeatedly?

A) Random failure
B) Check if liveness probe failure timing matches restart interval; probe might be too aggressive
C) Memory leak
D) Network issues

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Predictable restart intervals suggest probe timing issues. Calculate: `initialDelaySeconds + ((failureThreshold - 1) × periodSeconds)`. For example, with defaults (initialDelaySeconds=0, periodSeconds=10, failureThreshold=3), restart occurs at 20 seconds. If restarts match this calculation, the probe fails before the app is truly ready. Adjust timing or add startupProbe for slow apps.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

## Resource Management and Quotas

### Question 71
[MEDIUM]

What happens when a namespace exceeds its ResourceQuota for CPU requests?

A) Existing Pods are evicted
B) New Pods that would exceed the quota are rejected
C) Pods run with reduced CPU
D) Quota is automatically increased

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota is enforced at admission time. When creating Pods would exceed the quota, the request is rejected with an error. Existing Pods are not affected. The quota prevents new resource consumption, not current usage.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 72
[MEDIUM]

How do you view current ResourceQuota usage in a namespace?

A) kubectl get quota
B) kubectl describe resourcequota <name> -n <namespace>
C) kubectl top quota
D) kubectl get limits

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe resourcequota <name>` shows both the quota limits and current usage for each resource type. It displays used/hard values making it easy to see how close to limits the namespace is. `kubectl get quota` shows quotas but less detail.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 73
[MEDIUM-HARD]

A Pod creation fails with "exceeded quota" but calculations show quota should be available. What might cause this?

A) Calculation error
B) Pods in Terminating state still count against quota until fully deleted
C) Quota is disabled
D) Wrong namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pods in Terminating state continue counting against ResourceQuota until completely deleted. If Pods are stuck terminating, they consume quota space. Check for terminating Pods with `kubectl get pods` and investigate why they won't terminate.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 74
[MEDIUM-HARD]

What is the effect of LimitRange on Pods without resource specifications?

A) Pods are rejected
B) Default limits and requests are automatically applied
C) Pods run unlimited
D) Pods use node capacity

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LimitRange can specify default resource requests and limits. Pods without explicit resources get these defaults applied automatically. This ensures all Pods in a namespace have resource constraints even if developers don't specify them, enabling better scheduling and quota accounting.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 75
[HARD]

How do you identify which Pods are consuming the most resources against a quota?

A) kubectl top quota
B) List Pods in namespace and sum their resource requests; compare with quota
C) Check kubelet metrics
D) View etcd directly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota counts requests, not actual usage. List Pods: `kubectl get pods -n <ns> -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.containers[*].resources.requests}{"\n"}{end}'`. Sum requests per resource type to find major consumers. `kubectl top pods` shows actual usage, not quota consumption.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 76
[HARD]

A namespace has both ResourceQuota and LimitRange. In what order are they evaluated?

A) Quota first, then LimitRange
B) LimitRange applies defaults first, then quota is evaluated
C) They're evaluated simultaneously
D) Only one can be active

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LimitRange defaults are applied first to fill in missing resource specifications. Then ResourceQuota admission checks if the total (including defaults) fits within quota. This ordering means LimitRange defaults affect quota calculations, so ensure defaults align with quota capacity.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 77
[HARD]

What causes "must specify limits" error even when LimitRange has defaults?

A) LimitRange not applied yet
B) ResourceQuota includes limits.* (e.g., limits.cpu, limits.memory) and LimitRange defaults don't cover all containers
C) Wrong namespace
D) LimitRange is invalid

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When ResourceQuota includes `limits.cpu` or `limits.memory`, every container must specify those limits. LimitRange defaults may not apply if: they only set defaults for some resource types, there are init containers without defaults, or the LimitRange was created after the Pod creation attempt. Ensure LimitRange covers all resource types the quota requires.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/#compute-resource-quota)

</details>

---

### Question 78
[HARD]

How do PriorityClass and ResourceQuota interact?

A) No interaction
B) Quota can be scoped to specific priority classes
C) Higher priority bypasses quota
D) Priority determines quota order

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota can use scope selectors to apply different quotas based on PriorityClass. For example, limit low-priority batch Pods differently than high-priority production Pods. This allows reserving cluster capacity for critical workloads while limiting lower-priority consumption.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/#resource-quota-per-priorityclass)

</details>

---

### Question 79
[HARD]

A container is OOMKilled but its memory usage (from kubectl top) shows below the limit. What explains this?

A) Metrics are wrong
B) kubectl top shows container memory, but kernel also counts filesystem cache and other memory
C) Limit isn't enforced
D) Container restarted before measurement

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Container memory limits include all memory charged to the cgroup: anonymous memory, tmpfs, kernel buffers, and sometimes filesystem cache. `kubectl top` shows working set, but the actual cgroup memory can be higher. Check detailed cgroup stats for full picture.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 80
[HARD]

How does eviction priority work when a node is under memory pressure?

A) Random selection
B) By QoS class first (BestEffort, then Burstable, then Guaranteed), then by priority and usage within each class
C) Alphabetical by name
D) Oldest first

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubelet eviction order follows QoS class first: BestEffort Pods are evicted before Burstable, and Burstable before Guaranteed. Within each QoS class, Pods are ranked by priority and then by how much their usage exceeds their requests. Guaranteed Pods with usage at or below requests are most protected.

**Source:** [Node-pressure Eviction | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/)

</details>

---

## Security and Access Troubleshooting

### Question 81
[MEDIUM]

A Pod fails with "Error: container has runAsNonRoot and image will run as root". How do you fix this?

A) Remove the security context
B) Use an image that runs as non-root or set runAsUser to a non-zero value
C) Add root permissions
D) Disable security policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `runAsNonRoot: true` security context prevents containers from running as UID 0. Fix by: using an image built to run as non-root user, or explicitly setting `runAsUser: <non-zero-uid>` in securityContext. Don't remove the security control.

**Source:** [Configure a Security Context | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 82
[MEDIUM]

How do you check if a ServiceAccount has permission to perform an action?

A) kubectl get serviceaccount
B) kubectl auth can-i <verb> <resource> --as=system:serviceaccount:<namespace>:<name>
C) kubectl describe serviceaccount
D) kubectl get rolebinding

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl auth can-i` with `--as` flag to impersonate the ServiceAccount and check permissions. For example: `kubectl auth can-i get pods --as=system:serviceaccount:default:my-sa`. This directly tests RBAC rules without needing to trace through all bindings.

**Source:** [Checking API Access | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#checking-api-access)

</details>

---

### Question 83
[MEDIUM-HARD]

A Pod can't access the Kubernetes API despite having a ServiceAccount with appropriate RBAC. What else should you check?

A) Only RBAC matters
B) ServiceAccount token automount might be disabled, or the token might be expired
C) Pod IP address
D) Container image

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Besides RBAC, check: `automountServiceAccountToken: false` in Pod or ServiceAccount spec disables token mounting, token expiration with bound service account tokens, NetworkPolicy blocking API server access, or the ServiceAccount specified doesn't exist.

**Source:** [Configure Service Accounts | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 84
[MEDIUM-HARD]

What does "error: unable to upgrade connection" or container not ready error indicate when exec-ing into a Pod?

A) Wrong container name
B) The container is not in a running state; kubectl exec requires the container to be running
C) Container doesn't exist
D) Permission denied

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kubectl exec requires the target container to be in a running state. If the container is still starting, in CrashLoopBackOff, or otherwise not running, exec will fail. Wait for the container to become Running, check why it's not starting with `kubectl describe pod`, or fix any startup issues first.

**Source:** [Get a Shell to a Running Container | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)

</details>

---

### Question 85
[HARD]

A user has ClusterRoleBinding to "edit" but can't create Pods in a namespace. What might restrict this?

A) Edit role doesn't include Pods
B) ResourceQuota, LimitRange, or admission controllers blocking Pod creation
C) User token expired
D) API server down

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The edit ClusterRole includes Pod creation permissions. However, non-RBAC mechanisms can block creation: ResourceQuota prevents creation when limits are exceeded, LimitRange rejects Pods missing required resource specs, Pod Security Admission blocks Pods violating namespace security policy, or custom admission webhooks reject the request. Note: RBAC is additive - RoleBindings cannot remove permissions granted by ClusterRoleBindings.

**Source:** [RBAC | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 86
[HARD]

A Pod can't access the Kubernetes API with "connection refused" errors despite correct ServiceAccount permissions. What should you check?

A) RBAC permissions only
B) Network connectivity to API server, NetworkPolicy blocking egress, or API server endpoint
C) ServiceAccount doesn't exist
D) Wrong namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With correct RBAC, API access failures suggest network issues: 1) NetworkPolicy may block egress to the API server, 2) The kubernetes Service endpoint may be unreachable, 3) Firewall rules may block traffic to port 443. Verify with `kubectl exec <pod> -- wget -qO- https://kubernetes.default.svc/healthz --no-check-certificate`.

**Source:** [Access Cluster API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 87
[HARD]

A NetworkPolicy is created but Pod traffic isn't being filtered. What might cause this?

A) NetworkPolicy is namespace-scoped
B) CNI plugin doesn't support NetworkPolicy or policy selectors don't match
C) Pods need restart
D) NetworkPolicy applies immediately

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Not all CNI plugins support NetworkPolicy (e.g., Flannel without Calico). Even with supported plugins, policies only apply to Pods matching the podSelector. Empty podSelector ({}) matches all Pods. Verify CNI supports policies and selector labels match target Pods.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 88
[HARD]

A bound ServiceAccount token fails authentication with "audience mismatch" error. What causes this?

A) Token is invalid
B) The token's `aud` claim doesn't match the API server's `--api-audiences` configuration
C) RBAC is namespace-specific
D) Token hasn't been refreshed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bound ServiceAccount tokens (projected volume tokens) include an `aud` (audience) claim. The API server validates this against its `--api-audiences` configuration. If they don't match, authentication fails. This commonly occurs when using TokenRequest API with a custom audience or when the API server's audiences are misconfigured. Create tokens with correct audiences using TokenRequest API.

**Source:** [Service Account Tokens | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/)

</details>

---

### Question 89
[HARD]

A Pod fails to start with "operation not permitted" for seccomp profile. How do you diagnose this?

A) Check container logs
B) Verify seccomp profile exists on node, check profile path, and ensure kubelet can read it
C) Remove seccomp configuration
D) Change container user

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Seccomp profiles referenced in Pods must exist on nodes at the specified path. For custom profiles, check: profile file exists at correct path (default: /var/lib/kubelet/seccomp/), kubelet has read permissions, and JSON syntax is valid. Use RuntimeDefault for built-in profile.

**Source:** [Restrict Syscalls with Seccomp | Kubernetes](https://kubernetes.io/docs/tutorials/security/seccomp/)

</details>

---

### Question 90
[HARD]

How do you audit which RBAC permissions a failing API request needed?

A) Check user permissions
B) Enable audit logging and look for RBAC decision details in audit events
C) Try different permissions
D) Check API server logs only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes audit logs capture RBAC decisions with details about required permissions. Configure audit policy to log request metadata and authorization decisions. The audit events show exactly which resource/verb/namespace was requested and why it was denied.

**Source:** [Auditing | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

</details>

---

## Advanced Diagnostics and Tools

### Question 91
[MEDIUM]

What is the purpose of `kubectl cluster-info dump`?

A) Delete cluster information
B) Export comprehensive cluster state for debugging including logs and configs
C) Show cluster version
D) Backup etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cluster-info dump` exports cluster state: component status, node info, events, and logs from kube-system namespace. Add `--all-namespaces` for complete dump. Output goes to stdout or a directory with `--output-directory`. Useful for sharing debug info with support.

**Source:** [Troubleshooting | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/)

</details>

---

### Question 92
[MEDIUM]

How do you check if the API server is healthy?

A) kubectl get nodes
B) kubectl get --raw /healthz or /livez or /readyz
C) ping the API server
D) kubectl cluster-info only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** API server exposes health endpoints: `/healthz` (deprecated), `/livez` (liveness), `/readyz` (readiness). Use `kubectl get --raw /readyz?verbose=true` for detailed component health. These show individual subsystem health (etcd, informers, etc.).

**Source:** [API Server | Kubernetes](https://kubernetes.io/docs/reference/using-api/health-checks/)

</details>

---

### Question 93
[MEDIUM-HARD]

What information does `kubectl get componentstatuses` provide?

A) Pod statuses
B) Health of control plane components (deprecated, may show inaccurate data)
C) Node component status
D) Network component health

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl get componentstatuses` (or `cs`) shows control plane component health: scheduler, controller-manager, etcd. However, this API is deprecated and may show incorrect data in modern clusters. Use direct health endpoints (`/healthz`) on each component instead.

**Source:** [Troubleshooting | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/)

</details>

---

### Question 94
[MEDIUM-HARD]

How do you get detailed information about why a specific Pod is not being scheduled?

A) kubectl get pod
B) kubectl describe pod <name> and check Events section for scheduler messages
C) kubectl logs scheduler
D) kubectl get events only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe pod` shows Events including scheduler decisions. Messages like "0/3 nodes are available: 1 node had taint, 2 insufficient memory" explain exactly why scheduling failed. Events are attached to the Pod object by the scheduler.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 95
[HARD]

How do you enable verbose output for kubectl to debug API issues?

A) kubectl --debug
B) kubectl -v=<level> where higher levels show more detail (8-9 shows HTTP requests/responses)
C) kubectl --trace
D) Set DEBUG=true environment variable

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kubectl verbosity levels: -v=6 shows request URLs, -v=7 shows request headers, -v=8 shows request/response bodies, -v=9 shows curl commands. Example: `kubectl -v=8 get pods` shows the full HTTP interaction with the API server.

**Source:** [kubectl | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 96
[HARD]

What does high "workqueue depth" in controller-manager metrics indicate?

A) Normal operation
B) Controllers are falling behind processing events, possible performance issue
C) Queue is empty
D) Metrics are broken

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Workqueue depth measures pending items for each controller. High depth means events are queuing faster than processing, indicating: controller performance issues, etcd latency, or excessive cluster changes. Monitor `workqueue_depth` metric per controller type.

**Source:** [Controller Manager Metrics | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/system-metrics/)

</details>

---

### Question 97
[HARD]

How do you identify etcd performance issues affecting the cluster?

A) Check API server logs
B) Monitor etcd metrics: request latency, disk fsync duration, leader changes, and database size
C) Restart etcd
D) Check kubelet logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Key etcd metrics: `etcd_disk_wal_fsync_duration_seconds` (disk performance), `etcd_server_leader_changes_seen_total` (cluster stability), `etcd_mvcc_db_total_size_in_bytes` (database size), and request latency histograms. Slow etcd causes cluster-wide API latency.

**Source:** [Operating etcd | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

### Question 98
[HARD]

What does the admission webhook timeout error indicate and how do you troubleshoot it?

A) API server timeout
B) Webhook service didn't respond in time; check webhook Pod logs and network connectivity
C) Invalid webhook configuration
D) RBAC issue

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Webhook timeouts mean the webhook service (ValidatingWebhookConfiguration or MutatingWebhookConfiguration) didn't respond within the configured timeout (default 10s). Check: webhook Pod health/logs, network connectivity to webhook Service, and consider adjusting timeoutSeconds or failurePolicy.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)

</details>

---

### Question 99
[HARD]

How do you trace the path of a request through the Kubernetes API server?

A) Use kubectl describe
B) Enable audit logging with RequestReceived stage and trace through audit events using audit ID
C) Check API server logs only
D) Use network packet capture

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes audit logs track requests through stages: RequestReceived, ResponseStarted, ResponseComplete, Panic. Each event includes an audit ID for correlation. Configure audit policy to capture needed detail level. This shows authentication, authorization, and admission decisions.

**Source:** [Auditing | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

</details>

---

### Question 100
[HARD]

A cluster has intermittent API server errors. How do you identify if it's a specific control plane component issue?

A) Restart all components
B) Check each component's health endpoint, logs, and metrics independently
C) Assume it's network related
D) Redeploy the cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Systematic diagnosis: check API server `/readyz?verbose=true` for failing checks, examine each component's logs (scheduler, controller-manager, etcd), monitor metrics for latency and errors, and verify network connectivity between components. Correlate timestamps across components.

**Source:** [Troubleshooting | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/)

</details>
