# Troubleshooting - 100 MCQ Questions (Part A)

**Domain:** Container Orchestration (28%)
**Competency:** Troubleshooting
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## Pod Status and Lifecycle Issues

### Question 1
[MEDIUM]

What does a Pod status of "Pending" indicate?

A) The Pod is running but not ready
B) The Pod has not yet been scheduled to a node or is waiting for resources
C) The Pod has completed successfully
D) The Pod is being deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pending status means the Pod has been accepted by the cluster but hasn't started running. Common reasons include: waiting for scheduling, waiting for container images to download, or waiting for volumes to be mounted.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-phase)

</details>

---

### Question 2
[MEDIUM]

What is the most common cause of a Pod stuck in "ContainerCreating" state?

A) CPU limits too high
B) Image pull issues, volume mount problems, or network plugin delays
C) Too many replicas
D) Incorrect labels

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ContainerCreating indicates the Pod is scheduled but containers aren't running yet. Common causes: image pull failures (ImagePullBackOff), volume mount issues (PVC not bound), or CNI plugin problems setting up networking.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 3
[MEDIUM-HARD]

How do you determine why a Pod is in CrashLoopBackOff?

A) Check node status only
B) Use kubectl logs and kubectl describe pod to check container exit codes and events
C) Restart the kubelet
D) Delete the namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CrashLoopBackOff means the container keeps crashing. Use `kubectl logs <pod>` to see application output, `kubectl logs <pod> --previous` for the last crash, and `kubectl describe pod` to see exit codes and events explaining the failures.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

---

### Question 4
[MEDIUM-HARD]

What does exit code 137 indicate when a container terminates?

A) Application error
B) Container was killed by SIGKILL, often due to OOM or resource limits
C) Network failure
D) Volume not found

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Exit code 137 = 128 + 9 (SIGKILL). This typically indicates the container was killed by the OOM killer due to exceeding memory limits, or manually terminated. Check `kubectl describe pod` for OOMKilled reason or resource limit violations.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

---

### Question 5
[HARD]

A Pod shows "Running" but the application inside is not responding. What should you check first?

A) Node disk space only
B) Readiness probe configuration and application health endpoints
C) Cluster DNS only
D) API server logs only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Running Pod with unresponsive application suggests the readiness probe may not be configured correctly or the application is unhealthy. Check if readiness probes are defined and passing, exec into the Pod to test the application directly, and review application logs.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 6
[HARD]

What causes a Pod to enter the "Unknown" phase?

A) Image not found
B) Communication failure between the API server and the node running the Pod
C) Invalid YAML syntax
D) Insufficient CPU

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Unknown phase means the Pod state cannot be determined, usually due to communication failure with the node's kubelet. This can indicate node failure, network partition, or kubelet crash. Check node status and kubelet logs.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-phase)

</details>

---

### Question 7
[HARD]

How do you troubleshoot a Pod that keeps getting evicted?

A) Increase replicas
B) Check node resource pressure, Pod priority, and resource requests/limits
C) Change the image
D) Modify labels only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Eviction occurs due to node resource pressure (memory, disk, PIDs). Check: 1) Node conditions with `kubectl describe node`, 2) Pod QoS class (BestEffort evicted first), 3) Resource requests/limits, 4) PriorityClass settings. Set appropriate requests to get Guaranteed or Burstable QoS.

**Source:** [Node-pressure Eviction | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/)

</details>

---

### Question 8
[HARD]

What is the significance of the "Terminated" container state with reason "Completed"?

A) The container crashed
B) The container finished successfully with exit code 0
C) The container was OOM killed
D) The container failed to start

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Terminated with reason "Completed" and exit code 0 indicates successful completion. This is normal for init containers and Job Pods. For regular Pods with restartPolicy: Always, the container will restart. Check if this is expected behavior or if the application is exiting unexpectedly.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-states)

</details>

---

### Question 9
[HARD]

A Pod is stuck in "Terminating" state. What could be causing this?

A) Too many containers
B) Finalizers blocking deletion, stuck preStop hooks, or unresponsive processes ignoring SIGTERM
C) Invalid image
D) Wrong namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Stuck Terminating can be caused by: 1) Finalizers that can't complete, 2) preStop hooks taking too long, 3) Processes ignoring SIGTERM during grace period. Check `kubectl get pod -o yaml` for finalizers, try `kubectl delete pod --force --grace-period=0` as last resort.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 10
[HARD]

How do you identify the root cause when multiple Pods fail simultaneously?

A) Restart all nodes
B) Check common dependencies: node health, storage, network, and shared ConfigMaps/Secrets
C) Delete and recreate all Pods
D) Increase memory limits

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Simultaneous Pod failures suggest a shared dependency issue. Check: 1) Node status where Pods are running, 2) Shared storage (PV/PVC issues), 3) Network problems, 4) Common ConfigMaps/Secrets that may have been modified, 5) Resource exhaustion at node level.

**Source:** [Troubleshooting | Kubernetes](https://kubernetes.io/docs/tasks/debug/)

</details>

---

## Debugging Commands and Techniques

### Question 11
[MEDIUM]

Which command shows detailed information about a Pod including events?

A) kubectl get pod
B) kubectl describe pod <name>
C) kubectl logs pod
D) kubectl top pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe pod <name>` shows comprehensive information: Pod spec, container states, conditions, volumes, events, and more. The Events section at the bottom is particularly useful for troubleshooting scheduling and startup issues.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 12
[MEDIUM]

How do you view logs from a crashed container?

A) kubectl logs <pod>
B) kubectl logs <pod> --previous
C) kubectl describe pod only
D) kubectl get events only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl logs <pod> --previous` (or `-p`) to view logs from the previous container instance. This is essential for debugging CrashLoopBackOff situations where the current container hasn't produced logs yet or has already crashed.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

---

### Question 13
[MEDIUM-HARD]

What is the purpose of kubectl debug command?

A) To delete problematic Pods
B) To create ephemeral debug containers or copy Pods for troubleshooting
C) To restart containers
D) To view metrics only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl debug` creates ephemeral containers in running Pods or creates a copy of a Pod for debugging. You can attach debug tools without modifying the original Pod, useful for distroless images that lack shells and debugging utilities.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#ephemeral-container)

</details>

---

### Question 14
[MEDIUM-HARD]

How do you execute a command inside a running container?

A) kubectl run
B) kubectl exec -it <pod> -- <command>
C) kubectl attach only
D) kubectl cp only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl exec -it <pod> -- <command>` to run commands interactively inside a container. Add `-c <container>` for multi-container Pods. Common uses: checking files, testing network connectivity, or running diagnostic commands.

**Source:** [Get a Shell to a Running Container | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)

</details>

---

### Question 15
[HARD]

How do you troubleshoot a Pod when the container has no shell?

A) Restart the Pod
B) Use kubectl debug to attach an ephemeral container with debugging tools
C) Delete and recreate with different image
D) Check events only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For distroless or minimal images without shells, use `kubectl debug <pod> -it --image=busybox --target=<container>` to attach an ephemeral container that shares the process namespace. This allows inspection of the target container's filesystem and processes.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#ephemeral-container)

</details>

---

### Question 16
[HARD]

What does kubectl get events --field-selector show?

A) Pod logs
B) Filtered cluster events based on specified criteria like reason, type, or involved object
C) Node metrics
D) Container states

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field selectors filter events by specific fields. Examples: `--field-selector reason=FailedScheduling` shows scheduling failures, `--field-selector type=Warning` shows warnings. Combine with `--sort-by=.lastTimestamp` for chronological troubleshooting.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 17
[HARD]

How do you capture network traffic from a Pod for debugging?

A) kubectl logs
B) Use kubectl debug with tcpdump or deploy a debug Pod with network tools
C) kubectl describe only
D) kubectl top

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For network debugging: 1) Use `kubectl debug <pod> -it --image=busybox --target=<container>` to attach an ephemeral container with networking tools, 2) Or create a debug Pod in the same namespace to test connectivity, 3) From within the debug container, use standard diagnostics like `wget`, `nslookup`, and `nc` to diagnose network issues.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#ephemeral-container)

</details>

---

### Question 18
[HARD]

What information does kubectl get pod -o wide provide for troubleshooting?

A) Container logs
B) Pod IP, node name, and nominated node information
C) Resource usage
D) Event history

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `-o wide` flag adds columns showing: Pod IP address, node where it's running, nominated node, and readiness gates. This quickly identifies which node hosts a Pod and its IP for network troubleshooting.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 19
[HARD]

How do you stream logs from multiple Pods simultaneously?

A) kubectl logs only works for one Pod
B) kubectl logs -l <label-selector> --all-containers -f
C) kubectl describe multiple Pods
D) kubectl get logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl logs -l app=myapp -f` to stream logs from all Pods matching the label selector. Add `--all-containers` for multi-container Pods. For production environments, implement centralized logging using the Kubernetes logging architecture (e.g., node-level agents that ship logs to a backend).

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 20
[HARD]

What is the purpose of kubectl port-forward in troubleshooting?

A) To expose Pods externally
B) To create a secure tunnel from local machine to a Pod or Service for testing
C) To change container ports
D) To restart networking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl port-forward pod/<name> <local-port>:<pod-port>` creates a tunnel to access Pod ports locally without exposing them via Service. Useful for testing applications, accessing admin interfaces, or debugging without modifying cluster networking.

**Source:** [Use Port Forwarding to Access Applications | Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/)

</details>

---

## Node and Cluster Troubleshooting

### Question 21
[MEDIUM]

What does a node status of "NotReady" indicate?

A) The node is being upgraded
B) The kubelet is not reporting healthy status to the API server
C) The node has no Pods
D) The node is being drained

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NotReady means the kubelet isn't responding or is reporting unhealthy conditions. Common causes: kubelet service stopped, network issues between node and control plane, or node resource exhaustion. Check `kubectl describe node` for conditions.

**Source:** [Node | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 22
[MEDIUM]

How do you check the conditions reported by a node?

A) kubectl get node only
B) kubectl describe node <name> and look at the Conditions section
C) kubectl logs node
D) kubectl top node only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe node <name>` shows Conditions including: Ready, MemoryPressure, DiskPressure, PIDPressure, NetworkUnavailable. Each condition has status (True/False/Unknown), reason, and message explaining the node's health.

**Source:** [Node | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/#condition)

</details>

---

### Question 23
[MEDIUM-HARD]

What should you check when a node shows MemoryPressure?

A) Network configuration
B) Memory usage of Pods, identify memory-heavy workloads, and check for memory leaks
C) Disk space only
D) CPU allocation only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** MemoryPressure means available memory is below the eviction threshold. Check: `kubectl top pods` on that node to find memory-heavy Pods, review Pod memory limits, look for Pods without limits (BestEffort QoS), and check for memory leaks in applications.

**Source:** [Node-pressure Eviction | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/)

</details>

---

### Question 24
[MEDIUM-HARD]

How do you view kubelet logs on a node?

A) kubectl logs kubelet
B) journalctl -u kubelet on the node or check /var/log/kubelet.log
C) kubectl describe kubelet
D) kubectl get kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubelet logs are on the node itself, not accessible via kubectl. SSH to the node and use `journalctl -u kubelet` for systemd-managed kubelets, or check `/var/log/kubelet.log`. These logs show container operations, volume mounts, and node-level issues.

**Source:** [Debugging Kubernetes Nodes | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/debug-node/)

</details>

---

### Question 25
[HARD]

What causes a node to be cordoned?

A) Automatic scaling
B) An administrator ran kubectl cordon, or the node was marked unschedulable for maintenance
C) Memory pressure only
D) Too many Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Cordoning marks a node as unschedulable, preventing new Pods from being scheduled there. It's done manually with `kubectl cordon <node>` for maintenance. Existing Pods continue running. Use `kubectl drain` to also evict existing Pods before maintenance.

**Source:** [Safely Drain a Node | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)

</details>

---

### Question 26
[HARD]

How do you troubleshoot nodes that repeatedly become NotReady?

A) Delete the nodes
B) Check kubelet logs, verify network connectivity, review system resources, and check for certificate issues
C) Restart the API server
D) Increase replicas

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Intermittent NotReady: 1) Check kubelet logs for errors, 2) Verify network stability to control plane, 3) Check node resources (CPU, memory, disk), 4) Verify kubelet certificates haven't expired, 5) Check node-to-API server firewall rules.

**Source:** [Debugging Kubernetes Nodes | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/debug-node/)

</details>

---

### Question 27
[HARD]

What does the DiskPressure condition indicate and how do you resolve it?

A) Network issues
B) Node disk usage exceeds threshold; clean up unused images, logs, and completed Pods
C) CPU overload
D) Memory leak

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DiskPressure means available disk space fell below the eviction threshold (default: 10% available for nodefs, 15% for imagefs). Resolve by: 1) Rely on kubelet's automatic image garbage collection to remove unused images, 2) Delete completed Pods and Jobs that are no longer needed, 3) Clean up old container logs, 4) Check for Pods writing excessive data to emptyDir volumes.

**Source:** [Garbage Collection | Kubernetes](https://kubernetes.io/docs/concepts/architecture/garbage-collection/#container-image-garbage-collection)

</details>

---

### Question 28
[HARD]

How do you identify which Pods are running on a specific node?

A) kubectl get pods only
B) kubectl get pods --all-namespaces --field-selector spec.nodeName=<node-name>
C) kubectl describe node only
D) kubectl top node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl get pods -A --field-selector spec.nodeName=<node>` to list all Pods on a specific node across all namespaces. This helps identify workloads affected by node issues and find resource-heavy Pods causing node pressure.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 29
[HARD]

What should you check when the API server is slow or unresponsive?

A) Pod logs only
B) etcd health, API server resource usage, request latency metrics, and audit logs
C) Node count only
D) Service configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Slow API server: 1) Check etcd latency and health, 2) Review API server CPU/memory usage, 3) Check `apiserver_request_duration_seconds` metrics, 4) Look for expensive requests in audit logs, 5) Verify no webhook is timing out and blocking requests.

**Source:** [Debugging Kubernetes Nodes | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/)

</details>

---

### Question 30
[HARD]

How do you verify control plane component health?

A) kubectl get pods only
B) kubectl get componentstatuses, check control plane Pod logs, and verify endpoints
C) kubectl describe cluster
D) kubectl health-check

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Check control plane health: 1) Query API server health endpoints (`/readyz`, `/livez`, `/healthz`), 2) Check control plane Pods in kube-system: `kubectl get pods -n kube-system`, 3) Review component logs: `kubectl logs -n kube-system <component-pod>`, 4) Verify etcd cluster health with etcdctl.

**Source:** [API Server Health | Kubernetes](https://kubernetes.io/docs/reference/using-api/health-checks/)

</details>

---

## Network and Service Troubleshooting

### Question 31
[MEDIUM]

What should you check first when a Service has no endpoints?

A) Node status
B) Service selector matches Pod labels and Pods are in Ready state
C) Ingress configuration
D) DNS settings

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Empty endpoints means no Pods match the Service selector or matching Pods aren't Ready. Check: 1) `kubectl describe service` for selector, 2) `kubectl get pods --show-labels` to verify labels match, 3) Ensure Pods are Running and Ready (passing readiness probes).

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 32
[MEDIUM]

How do you test DNS resolution inside a cluster?

A) ping the service name
B) kubectl exec <pod> -- nslookup <service-name> or dig
C) kubectl describe dns
D) kubectl get dns

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Test DNS with: `kubectl exec <pod> -- nslookup <service>` or `kubectl exec <pod> -- nslookup <service>.<namespace>.svc.cluster.local`. This verifies CoreDNS is working and the Service is resolvable. DNS issues cause connection failures to Services.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/#does-the-service-work-by-dns-name)

</details>

---

### Question 33
[MEDIUM-HARD]

What causes "connection refused" when connecting to a Service?

A) DNS failure
B) No Pods behind the Service or application not listening on the target port
C) Firewall only
D) TLS issues only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Connection refused" means nothing is listening on the port. Causes: 1) Service has no endpoints (no matching Ready Pods), 2) Application inside container isn't listening on the targetPort, 3) Container crashed. Check endpoints and verify the application is running correctly.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 34
[MEDIUM-HARD]

How do you troubleshoot a NetworkPolicy blocking traffic?

A) Delete all policies
B) Check policy selectors, verify ingress/egress rules, and test connectivity with and without policies
C) Restart kube-proxy
D) Change CNI plugin

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicy troubleshooting: 1) List policies: `kubectl get networkpolicies`, 2) Check podSelector matches affected Pods, 3) Verify ingress/egress rules allow required traffic, 4) Test by temporarily removing policy, 5) Ensure CNI supports NetworkPolicy.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 35
[HARD]

A Pod can reach external services but not other Pods. What should you check?

A) External firewall only
B) CNI plugin status, kube-proxy, NetworkPolicies, and Pod network configuration
C) API server logs only
D) etcd health only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod-to-Pod issues while external works: 1) Check CNI plugin Pods are healthy, 2) Verify kube-proxy is running on nodes, 3) Look for NetworkPolicies blocking internal traffic, 4) Check Pod CIDR routing, 5) Verify no iptables rules blocking cluster traffic.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 36
[HARD]

What causes intermittent connection timeouts to a Service?

A) Too few replicas only
B) Unhealthy endpoints, network congestion, or some backend Pods not responding
C) DNS caching
D) Wrong port numbers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Intermittent timeouts suggest some backends are unhealthy. Check: 1) All endpoint Pods are truly healthy (not just Running), 2) Readiness probes are correctly configured, 3) Some Pods may be overloaded, 4) Network issues affecting specific nodes, 5) Load balancing hitting slow Pods.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 37
[HARD]

How do you verify kube-proxy is correctly configuring Service routing?

A) kubectl describe proxy
B) Check iptables rules or IPVS tables on nodes, and verify kube-proxy Pods are running
C) kubectl logs service
D) kubectl get proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify kube-proxy: 1) Check Pods: `kubectl get pods -n kube-system -l k8s-app=kube-proxy`, 2) On node, check rules: `iptables -L -t nat | grep <service-ip>` or `ipvsadm -Ln`, 3) Review kube-proxy logs for sync errors. Missing rules mean Services won't route traffic.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 38
[HARD]

What does "no route to host" error indicate when connecting between Pods?

A) DNS failure
B) Network routing issue, CNI misconfiguration, or firewall blocking at network level
C) Service not created
D) Wrong port

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "No route to host" indicates layer 3 routing failure. The packet can't reach the destination IP. Causes: 1) CNI plugin not properly configuring routes, 2) Node firewall blocking Pod CIDR, 3) Cloud provider route tables missing Pod network routes.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 39
[HARD]

How do you troubleshoot a LoadBalancer Service stuck in Pending?

A) Wait longer
B) Check cloud provider integration, cloud-controller-manager logs, and cloud API quotas
C) Change to ClusterIP
D) Delete and recreate

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LoadBalancer Pending means external LB isn't provisioned. Check: 1) Cloud-controller-manager is running and has credentials, 2) Cloud provider quota for load balancers, 3) Service annotations for provider-specific requirements, 4) Controller logs for API errors.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

</details>

---

### Question 40
[HARD]

What should you investigate when cross-namespace Service communication fails?

A) Node capacity
B) Use FQDN format, check NetworkPolicies in both namespaces, and verify DNS resolution
C) Restart CoreDNS
D) Delete namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Cross-namespace communication: 1) Use FQDN: `<service>.<namespace>.svc.cluster.local`, 2) Check NetworkPolicies in both source and destination namespaces, 3) Test DNS: `nslookup <service>.<namespace>`, 4) Verify Service exists in target namespace.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

## Storage and Volume Troubleshooting

### Question 41
[MEDIUM]

What does a PersistentVolumeClaim status of "Pending" indicate?

A) The PVC is being deleted
B) No PersistentVolume matches the claim or dynamic provisioning hasn't completed
C) The PVC is bound successfully
D) The storage is full

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pending PVC means no suitable PV is available. Causes: 1) No PV matches size/accessModes/storageClass, 2) Dynamic provisioner hasn't created PV yet, 3) StorageClass doesn't exist or provisioner is failing. Check events with `kubectl describe pvc`.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 42
[MEDIUM]

How do you check why a PVC is not binding?

A) kubectl get pv only
B) kubectl describe pvc to see events and verify matching PV requirements
C) kubectl logs pvc
D) kubectl delete pvc

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl describe pvc <name>` to see: 1) Events showing binding attempts and failures, 2) Requested storage size and access modes, 3) StorageClass name. Compare with available PVs using `kubectl get pv` to find mismatches.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 43
[MEDIUM-HARD]

What causes "FailedMount" events for a volume?

A) CPU limits
B) Volume doesn't exist, wrong mount options, or storage backend issues
C) Memory pressure
D) Network policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** FailedMount indicates kubelet couldn't mount the volume. Causes: 1) PV/PVC doesn't exist, 2) Storage backend unreachable (NFS server down, cloud disk detached), 3) Incorrect mount options, 4) Filesystem corruption, 5) Node doesn't have required drivers.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 44
[MEDIUM-HARD]

How do you troubleshoot a PV stuck in "Released" state?

A) Delete the PVC
B) Check reclaimPolicy, manually clear claimRef if reusing, or delete and recreate PV
C) Restart kubelet
D) Increase size

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Released means the PVC was deleted but PV retains data per reclaimPolicy (Retain). To reuse: 1) Backup data if needed, 2) Edit PV to remove `claimRef`, or 3) Delete and recreate PV. For Delete policy, PV should be automatically deleted.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming)

</details>

---

### Question 45
[HARD]

A Pod reports "Unable to attach or mount volumes" for a cloud disk. What should you check?

A) DNS settings
B) Cloud provider credentials, disk availability zone, and whether disk is attached to another node
C) CPU limits
D) Memory settings

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Cloud disk mount failures: 1) Check cloud credentials/IAM permissions, 2) Verify disk exists and is in same zone as node, 3) Check if disk is already attached to another node (can't multi-attach), 4) Review cloud-controller-manager logs for API errors.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 46
[HARD]

What causes volume mount to succeed but Pod still fails to start with permission errors?

A) Network issues
B) Security context mismatch, fsGroup not set, or volume mounted as read-only
C) Wrong image
D) CPU throttling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Permission errors on mounted volumes: 1) Set fsGroup in securityContext to change volume ownership, 2) Verify container runs as user with access to files, 3) Check if volume is mounted readOnly when write is needed, 4) Some storage backends don't support ownership changes.

**Source:** [Configure a Security Context | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 47
[HARD]

How do you diagnose slow storage performance affecting Pods?

A) Increase replicas
B) Check storage class IOPS limits, monitor disk metrics, and test with fio benchmark
C) Change images
D) Modify labels

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Diagnose storage performance: 1) Check StorageClass provisioner and parameters for IOPS limits, 2) Monitor disk latency/throughput metrics, 3) Run `fio` benchmark from a debug Pod, 4) Check if storage backend is overloaded, 5) Consider using faster storage class.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

### Question 48
[HARD]

What happens when a node with a local PV fails?

A) Data is automatically replicated
B) Pods using the local PV become unschedulable until the node recovers or PV is recreated
C) PV moves to another node
D) Nothing changes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Local PVs are bound to specific nodes. If that node fails: 1) Pods can't be scheduled elsewhere (node affinity), 2) Data is inaccessible until node recovers, 3) For permanent failure, must delete PVC/PV and recreate, losing data. Local storage isn't suitable for high availability.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#local)

</details>

---

### Question 49
[HARD]

How do you troubleshoot a CSI driver not provisioning volumes?

A) Delete the StorageClass
B) Check CSI driver Pods, review provisioner logs, and verify CSI driver registration
C) Restart API server
D) Change volume access mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CSI provisioning issues: 1) Check CSI controller and node driver Pods are running, 2) Review provisioner logs in CSI controller, 3) Verify `CSIDriver` and `CSINode` objects exist, 4) Check StorageClass references correct provisioner name, 5) Verify cloud credentials.

**Source:** [Kubernetes CSI Developer Documentation](https://kubernetes.io/docs/concepts/storage/volumes/#csi)

</details>

---

### Question 50
[HARD]

A PVC resize is stuck. What should you investigate?

A) Delete the PVC
B) Check if StorageClass allows expansion, CSI driver supports resize, and Pod must be restarted for filesystem resize
C) Reduce the size
D) Change access mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PVC resize issues: 1) Verify StorageClass has `allowVolumeExpansion: true`, 2) Check CSI driver supports expansion, 3) For filesystem resize, Pod may need restart, 4) Some storage backends require offline resize. Check `kubectl describe pvc` for resize conditions.

**Source:** [Resizing Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#expanding-persistent-volumes-claims)

</details>

---

## Workload Controllers Troubleshooting

### Question 51
[MEDIUM]

What does it mean when a Deployment shows "0/3 ready replicas"?

A) Deployment is paused
B) None of the desired 3 Pods are in Ready state
C) Deployment succeeded
D) Scaling down

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "0/3 ready" means the Deployment wants 3 Pods but none are Ready. Check: 1) Pod status with `kubectl get pods`, 2) Pod events with `kubectl describe pod`, 3) Common issues: image pull failures, resource constraints, or probe failures.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 52
[MEDIUM]

How do you check why a Deployment rollout is stuck?

A) Delete the Deployment
B) kubectl rollout status and kubectl describe deployment to see progress and events
C) kubectl logs deployment
D) kubectl get replicas

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl rollout status deployment/<name>` to see rollout progress and `kubectl describe deployment` for events. Stuck rollouts usually mean new Pods aren't becoming Ready due to: image issues, probe failures, or resource constraints.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#failed-deployment)

</details>

---

### Question 53
[MEDIUM-HARD]

A DaemonSet is not creating Pods on all nodes. What should you check?

A) Replica count
B) Node taints, DaemonSet tolerations, and nodeSelector/affinity settings
C) Deployment strategy
D) Service configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSet scheduling issues: 1) Check node taints with `kubectl describe node`, 2) Verify DaemonSet has required tolerations, 3) Check nodeSelector or affinity rules excluding nodes, 4) Ensure nodes aren't cordoned. `kubectl describe daemonset` shows desired vs current counts.

**Source:** [DaemonSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

</details>

---

### Question 54
[MEDIUM-HARD]

How do you troubleshoot a StatefulSet with Pods stuck in Pending?

A) Increase replicas
B) Check PVC status for each Pod, verify StorageClass exists, and check resource availability
C) Change service name
D) Modify Pod template

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSet Pods often wait for storage. Check: 1) PVCs for each Pod: `kubectl get pvc`, 2) PVCs are bound (not Pending), 3) StorageClass exists and can provision, 4) StatefulSets create Pods sequentially - if first Pod fails, others wait.

**Source:** [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

</details>

---

### Question 55
[HARD]

A Job keeps creating Pods but never completes. What could be the cause?

A) Too many completions
B) Pods are failing with non-zero exit codes before reaching backoffLimit
C) Wrong parallelism
D) Schedule syntax error

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Jobs retry failed Pods until backoffLimit (default 6). If Pods keep failing: 1) Check Pod logs for application errors, 2) Review exit codes in `kubectl describe pod`, 3) Fix the underlying issue, 4) If backoffLimit reached, Job is marked Failed.

**Source:** [Jobs | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/job/)

</details>

---

### Question 56
[HARD]

How do you identify which ReplicaSet is causing issues in a Deployment?

A) kubectl get deployment only
B) kubectl get replicasets with deployment labels, check which has non-zero replicas
C) kubectl logs deployment
D) kubectl describe service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl get rs -l app=<deployment-label>` to see all ReplicaSets. The active one has non-zero desired replicas. Check `kubectl describe rs <name>` for events. During stuck rollouts, both old and new RS may have replicas.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 57
[HARD]

A CronJob is not creating Jobs at scheduled times. What should you investigate?

A) Pod logs
B) CronJob schedule syntax, suspend field, and controller-manager logs
C) Service endpoints
D) PVC status

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CronJob not triggering: 1) Verify schedule syntax is valid cron format, 2) Check `spec.suspend` isn't true, 3) Look at `.status.lastScheduleTime`, 4) Check controller-manager logs, 5) Verify timezone (UTC by default), 6) Check if startingDeadlineSeconds was exceeded.

**Source:** [CronJob | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)

</details>

---

### Question 58
[HARD]

What does "progressDeadlineSeconds exceeded" mean for a Deployment?

A) Deployment completed
B) New Pods haven't become Ready within the deadline, marking the rollout as failed
C) Pods exceeded memory
D) Network timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** progressDeadlineSeconds (default 600s) sets how long a rollout can stall. If new Pods don't progress (become Ready) within this time, the Deployment condition changes to Progressing=False. The rollout pauses but isn't automatically rolled back.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#progress-deadline-seconds)

</details>

---

### Question 59
[HARD]

How do you troubleshoot StatefulSet Pod identity issues?

A) Delete all Pods
B) Verify headless Service exists, check DNS resolution for Pod hostnames, and verify stable network identity
C) Change replica count
D) Modify storage class

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSet identity depends on: 1) Headless Service (clusterIP: None) must exist, 2) Pods get stable hostname: `<pod-name>.<service>.<namespace>.svc.cluster.local`, 3) Test DNS resolution from other Pods, 4) PVCs named `<claim>-<pod-name>` for stable storage.

**Source:** [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

</details>

---

### Question 60
[HARD]

A Deployment rollback isn't working. What should you verify?

A) Delete the Deployment
B) Check revision history exists, verify revisionHistoryLimit, and use kubectl rollout undo correctly
C) Increase replicas
D) Change image

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Rollback issues: 1) Check history: `kubectl rollout history deployment/<name>`, 2) Verify `revisionHistoryLimit` hasn't been set to 0, 3) Use `kubectl rollout undo deployment/<name> --to-revision=N`, 4) Ensure target revision exists. Rollback creates a new revision.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment)

</details>

---

## Configuration and Probes Troubleshooting

### Question 61
[MEDIUM]

What happens when a Pod references a non-existent ConfigMap?

A) Default values are used
B) Pod fails to start and shows a warning event
C) ConfigMap is auto-created
D) Pod starts without the data

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If a required ConfigMap doesn't exist, the Pod stays in ContainerCreating with events showing "configmap not found". The container won't start until the ConfigMap exists. Use `optional: true` if the ConfigMap is not required.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 62
[MEDIUM]

How do you verify environment variables are correctly set from a ConfigMap?

A) kubectl describe configmap
B) kubectl exec into Pod and run env command to check variables
C) kubectl logs configmap
D) kubectl get env

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify env vars by: `kubectl exec <pod> -- env | grep <VAR_NAME>`. If empty, check: 1) ConfigMap exists and has the key, 2) Pod spec correctly references the ConfigMap, 3) Pod was restarted after ConfigMap changes (env vars don't auto-update).

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 63
[MEDIUM-HARD]

A liveness probe is failing and causing container restarts. What should you check?

A) Increase replicas
B) Probe endpoint, timing settings, and whether application needs more startup time
C) Change image
D) Modify service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Liveness probe failures: 1) Verify endpoint returns success (HTTP 200, command exit 0), 2) Check `initialDelaySeconds` is enough for app startup, 3) Adjust `timeoutSeconds` if app is slow, 4) Review `failureThreshold` before restart. Test endpoint manually via exec.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 64
[MEDIUM-HARD]

What is the difference in behavior between readiness and liveness probe failures?

A) Both restart containers
B) Readiness removes Pod from Service endpoints; liveness restarts the container
C) Both are the same
D) Readiness restarts; liveness removes from Service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Readiness probe failure: Pod removed from Service endpoints, no traffic sent to it. Container keeps running. Liveness probe failure: Container is killed and restarted. Use readiness for "not ready to serve traffic" and liveness for "application is broken and needs restart".

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 65
[HARD]

An application takes 5 minutes to start but liveness probes are killing it. How do you fix this?

A) Remove liveness probe
B) Add a startup probe or increase initialDelaySeconds significantly
C) Decrease failureThreshold
D) Use TCP probe instead

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For slow-starting apps, use a startup probe. It runs before liveness/readiness and can have longer timeouts. Once startup probe succeeds, liveness probe takes over. Alternative: set initialDelaySeconds > startup time, but startup probe is cleaner.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes)

</details>

---

### Question 66
[HARD]

ConfigMap volume mount shows old data after ConfigMap update. Why?

A) Always shows old data
B) Using subPath mount which doesn't receive automatic updates
C) ConfigMap wasn't updated
D) Volume is read-only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** SubPath mounted ConfigMaps don't receive automatic updates - the file is a copy at mount time. Regular volume mounts update automatically (with kubelet sync delay). For subPath mounts, Pod must be restarted to see changes.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/#mounted-configmaps-are-updated-automatically)

</details>

---

### Question 67
[HARD]

How do you troubleshoot imagePullSecrets not working?

A) Delete the image
B) Verify Secret exists, is type dockerconfigjson, is in same namespace, and check registry credentials
C) Change registry
D) Remove Secret

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** imagePullSecrets issues: 1) Secret must exist in same namespace as Pod, 2) Type must be `kubernetes.io/dockerconfigjson`, 3) Credentials must be valid for the registry, 4) Check Secret is referenced in Pod spec or ServiceAccount, 5) Events show auth failures.

**Source:** [Pull an Image from a Private Registry | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

</details>

---

### Question 68
[HARD]

Probes work locally but fail in Kubernetes. What could be different?

A) Probes are disabled
B) Different port/path, container listens only on localhost, or network namespace isolation
C) Kubernetes doesn't support probes
D) Probes only work on certain nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Common differences: 1) App binds to 127.0.0.1 instead of 0.0.0.0 (kubelet can't reach it), 2) Different port or path than configured in probe, 3) App expects headers not sent by probe, 4) HTTPS vs HTTP mismatch. Test probe endpoint via kubectl exec.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

### Question 69
[HARD]

How do you debug Secret data not appearing in mounted volume?

A) Delete the Secret
B) Check Secret exists, verify mount path, and exec into Pod to check actual file contents
C) Increase volume size
D) Change storage class

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Debug Secret mounts: 1) `kubectl get secret <name>` to verify it exists, 2) Check mount path doesn't conflict, 3) `kubectl exec <pod> -- ls -la /mount/path` to see files, 4) Each key becomes a file, 5) Data is base64 decoded in files.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 70
[HARD]

A probe passes sometimes and fails other times. What causes this flakiness?

A) Probe configuration is fine
B) Application performance issues, garbage collection pauses, or timeoutSeconds too low
C) Wrong probe type
D) Network policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Flaky probes: 1) Application may be slow under load (increase timeoutSeconds), 2) JVM garbage collection pauses, 3) Endpoint sometimes returns errors, 4) Resource contention affecting response time, 5) Increase failureThreshold to tolerate occasional failures.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

---

## Resource Management and Quotas

### Question 71
[MEDIUM]

What happens when a Pod tries to use more CPU than its limit?

A) Pod is killed
B) CPU is throttled but Pod continues running
C) Node crashes
D) Quota error

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CPU limits cause throttling, not termination. The container's CPU usage is capped at the limit. Unlike memory (which causes OOM kill), exceeding CPU limit just slows down the process. Monitor for CPU throttling metrics to identify constrained Pods.

**Source:** [Resource Management | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 72
[MEDIUM]

How do you check current resource usage against ResourceQuota?

A) kubectl get pods
B) kubectl describe resourcequota to see Used vs Hard limits
C) kubectl top quota
D) kubectl resource usage

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl describe resourcequota <name>` to see Used column (current consumption) and Hard column (limits). If Used approaches Hard, new resources may be rejected. Also shows count quotas (pods, services, configmaps, etc.).

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 73
[MEDIUM-HARD]

A Pod creation fails with "exceeded quota" error. How do you resolve it?

A) Delete the quota
B) Check which resource exceeded, free up resources or request quota increase
C) Restart API server
D) Change namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The error indicates which resource exceeded quota. Solutions: 1) Delete unused resources in namespace, 2) Reduce resource requests in Pod spec, 3) Request administrator to increase quota, 4) Check if unused completed Jobs/Pods are consuming quota.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 74
[MEDIUM-HARD]

What is the effect of LimitRange on Pods without resource specifications?

A) Pods are rejected
B) Default requests and limits from LimitRange are applied automatically
C) Unlimited resources
D) Node resources are used

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LimitRange can set default requests/limits for containers that don't specify them. It also enforces min/max constraints. If a Pod violates LimitRange (too high or too low), it's rejected. Check `kubectl describe limitrange` for defaults and constraints.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 75
[HARD]

A Pod is OOMKilled but its memory limit seems adequate. What should you investigate?

A) CPU settings
B) Container memory usage patterns, memory leaks, and whether limit accounts for all memory types
C) Storage size
D) Network bandwidth

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** OOM despite adequate limits: 1) Memory leak in application, 2) Limit doesn't account for JVM off-heap memory, 3) Multiple containers sharing Pod memory, 4) Kernel memory usage not counted properly, 5) Burst memory usage during garbage collection.

**Source:** [Resource Management | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 76
[HARD]

How do you identify which Pods are causing namespace resource exhaustion?

A) kubectl get pods
B) kubectl top pods -n <namespace> --sort-by=cpu or memory to find heavy consumers
C) kubectl describe namespace
D) kubectl quota show

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl top pods -n <namespace> --sort-by=cpu` or `--sort-by=memory` to see actual usage (requires metrics-server). Compare with resource requests to find over-requesting Pods. Also check for too many Pods consuming count quotas.

**Source:** [Tools for Monitoring Resources | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-usage-monitoring/)

</details>

---

### Question 77
[HARD]

Pods are Pending due to insufficient resources but nodes show available capacity. Why?

A) Scheduling disabled
B) Resource requests exceed allocatable capacity, or requests + existing allocations exceed node capacity
C) Too many nodes
D) Wrong labels

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduler considers requests, not actual usage. If sum of all Pod requests on a node exceeds allocatable capacity, new Pods can't be scheduled even if actual usage is low. Check: 1) `kubectl describe node` for Allocated resources, 2) Pod requests may be too high.

**Source:** [Resource Management | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 78
[HARD]

How do you troubleshoot HPA not scaling?

A) Delete HPA
B) Check metrics-server, verify HPA target metrics exist, and review HPA events for errors
C) Increase replicas manually
D) Change Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** HPA troubleshooting: 1) Check metrics-server is running: `kubectl top pods`, 2) `kubectl describe hpa` for events and current metrics, 3) Verify target metric exists and is being collected, 4) Check min/max replicas bounds, 5) Allow stabilization time for scaling decisions.

**Source:** [Horizontal Pod Autoscaling | Kubernetes](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

</details>

---

### Question 79
[HARD]

Resource requests are set but kubectl top shows much higher usage. Is this a problem?

A) Always a problem
B) Not necessarily; requests are guarantees, actual usage can exceed requests up to the limit
C) Node is broken
D) Metrics are wrong

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Requests are minimum guarantees for scheduling. Actual usage can exceed requests (burstable). It's only a problem if: 1) Node becomes overcommitted and Pods are evicted, 2) Usage approaches limits causing throttling/OOM. Set requests closer to typical usage for better scheduling.

**Source:** [Resource Management | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 80
[HARD]

A namespace is stuck with "exceeded quota" but describe shows available quota. What's happening?

A) Quota is broken
B) BestEffort Pods may be counted, or scope selectors limit what's counted
C) Cache issue
D) API bug

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota can have scopes (BestEffort, NotBestEffort, etc.) that limit what's counted. A Pod may exceed a scoped quota while overall quota shows availability. Also check for multiple quotas in namespace with different scope selectors.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/#quota-scopes)

</details>

---

## Security and Access Troubleshooting

### Question 81
[MEDIUM]

A user gets "Forbidden" error accessing resources. What should you check first?

A) Network policies
B) RBAC permissions - verify Roles, ClusterRoles, and bindings
C) DNS settings
D) Pod status

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Forbidden (403) indicates RBAC denial. Check: 1) `kubectl auth can-i <verb> <resource> --as=<user>` to test permissions, 2) List bindings: `kubectl get rolebindings,clusterrolebindings -A`, 3) Verify user/group is bound to appropriate Role/ClusterRole.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 82
[MEDIUM]

How do you test if a ServiceAccount has specific permissions?

A) kubectl describe sa
B) kubectl auth can-i <verb> <resource> --as=system:serviceaccount:<namespace>:<name>
C) kubectl get sa permissions
D) kubectl rbac test

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl auth can-i get pods --as=system:serviceaccount:default:my-sa` to check if a ServiceAccount can perform an action. Add `-n <namespace>` for namespace-scoped resources. Returns yes/no for quick permission verification.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 83
[MEDIUM-HARD]

A Pod can't access the Kubernetes API despite having correct RBAC. What else could be wrong?

A) DNS only
B) ServiceAccount token not mounted, API server network unreachable, or token expired
C) Wrong image
D) CPU limits

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Beyond RBAC: 1) Check `automountServiceAccountToken` isn't false, 2) Verify token is mounted at `/var/run/secrets/kubernetes.io/serviceaccount`, 3) Test API connectivity: can Pod reach kubernetes.default.svc, 4) For bound service account tokens, check if token expired.

**Source:** [Configure Service Accounts | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 84
[MEDIUM-HARD]

Pod Security Admission is rejecting Pods. How do you troubleshoot?

A) Disable PSA
B) Check namespace labels for enforce/warn levels, review Pod spec against policy requirements
C) Delete namespace
D) Restart API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PSA troubleshooting: 1) Check namespace labels: `kubectl get ns <name> --show-labels` for pod-security.kubernetes.io/* labels, 2) Review which policy level is enforced, 3) Compare Pod spec against that level's requirements, 4) Events show which field violates policy.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 85
[HARD]

A container needs to run as root but Pod Security enforces restricted. How do you resolve this?

A) Delete the policy
B) Use a different namespace with baseline/privileged level, or modify the container to not require root
C) Change the image tag
D) Increase replicas

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Options: 1) Move Pod to namespace with less restrictive PSA labels, 2) Modify container to run as non-root (preferred), 3) Use baseline level which allows root but restricts other privileges, 4) Create exemptions (if using webhook-based policy). Best practice: adapt containers to run rootless.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 86
[HARD]

How do you verify a Pod's security context is correctly applied?

A) kubectl describe only
B) kubectl exec into Pod and check id, capabilities, and filesystem permissions
C) kubectl logs security
D) kubectl get securitycontext

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify security context by execing into the Pod: 1) `id` shows user/group (runAsUser/runAsGroup), 2) `cat /proc/1/status | grep Cap` shows capabilities, 3) `mount | grep ' / '` shows if rootfs is read-only, 4) Test writing to filesystem to verify readOnlyRootFilesystem.

**Source:** [Configure a Security Context | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 87
[HARD]

A Pod fails with "cannot exec as root" but securityContext specifies runAsUser: 0. Why?

A) Bug in Kubernetes
B) Pod Security Admission or other admission controllers are overriding/blocking root
C) Image doesn't support root
D) Node doesn't allow root

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Admission controllers can override or block root. Check: 1) Namespace PSA labels may enforce restricted (blocks root), 2) Custom admission webhooks may modify or reject, 3) PodSecurityPolicies (if still enabled) may restrict. Check events for admission denials.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 88
[HARD]

How do you troubleshoot NetworkPolicy blocking legitimate traffic?

A) Delete all policies
B) List policies, check selectors and rules, test connectivity with policy disabled temporarily
C) Restart CNI
D) Change namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Debug NetworkPolicies: 1) `kubectl get networkpolicies -n <ns>` to list policies, 2) Check podSelector matches affected Pods, 3) Verify ingress/egress rules allow the traffic, 4) Test by temporarily removing policy, 5) Check CNI supports and correctly implements NetworkPolicy.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 89
[HARD]

What causes "operation not permitted" errors inside containers?

A) Network issues
B) Dropped capabilities, seccomp restrictions, or AppArmor/SELinux denials
C) DNS failure
D) Volume errors

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Operation not permitted" (EPERM) indicates security restrictions: 1) Required Linux capabilities dropped (default drops most), 2) Seccomp profile blocking syscall, 3) AppArmor/SELinux policy denial. Check dmesg for security denials, review securityContext capabilities.

**Source:** [Configure a Security Context | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 90
[HARD]

A certificate-based user can't authenticate. What should you verify?

A) RBAC bindings only
B) Certificate is valid, not expired, signed by cluster CA, and has correct CN/O fields
C) Service account token
D) Password

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Certificate authentication issues: 1) Check certificate expiration, 2) Verify signed by cluster CA, 3) CN becomes username, O becomes group - check these match RBAC bindings, 4) Ensure API server has --client-ca-file set correctly, 5) Test with `kubectl --client-certificate --client-key`.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

</details>

---

## Advanced Diagnostics and Tools

### Question 91
[MEDIUM]

What information do Kubernetes events provide?

A) Container logs only
B) State changes, warnings, scheduling decisions, and resource lifecycle events
C) Metrics only
D) Network traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Events record significant occurrences: Pod scheduling, image pulls, container starts/stops, probe failures, volume mounts, and warnings. View with `kubectl get events` or in `kubectl describe` output. Events are retained for about 1 hour by default.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 92
[MEDIUM]

How do you check all events across the cluster sorted by time?

A) kubectl get events
B) kubectl get events -A --sort-by=.lastTimestamp
C) kubectl describe events
D) kubectl events --all

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl get events -A --sort-by=.lastTimestamp` to see cluster-wide events in chronological order. Add `--field-selector type=Warning` to filter warnings only. This gives a timeline of cluster activity for troubleshooting.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 93
[MEDIUM-HARD]

How do you use audit logs for troubleshooting?

A) kubectl logs audit
B) Review API server audit log files to see who made what API calls and when
C) kubectl get audit
D) kubectl audit show

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Audit logs record API requests: who (user/SA), what (verb, resource), when, and response. Located where configured in API server. Useful for: tracking who deleted a resource, identifying unauthorized access, understanding activity timeline during incidents.

**Source:** [Auditing | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

</details>

---

### Question 94
[MEDIUM-HARD]

What is the purpose of the conditions field in resource status?

A) Only for display
B) Provides structured status information with type, status, reason, and message for each condition
C) Internal use only
D) Deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Conditions provide standardized status reporting: type (e.g., Ready, Available), status (True/False/Unknown), reason (machine-readable), message (human-readable). Check conditions to understand why a resource isn't in desired state. Use `kubectl get -o jsonpath` to extract specific conditions.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-conditions)

</details>

---

### Question 95
[HARD]

How do you troubleshoot finalizers blocking resource deletion?

A) Force delete always
B) Check resource for finalizers, identify which controller owns them, or remove manually if controller is gone
C) Restart API server
D) Delete namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Stuck finalizers: 1) `kubectl get <resource> -o yaml | grep finalizers` to see them, 2) Identify the controller that should remove them, 3) Check if controller is running, 4) If controller is gone, manually remove finalizers with `kubectl patch` (caution: may leave orphaned resources).

**Source:** [Finalizers | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/)

</details>

---

### Question 96
[HARD]

What causes admission webhooks to slow down cluster operations?

A) Too many Pods
B) Webhook Pod unhealthy, high latency, or timeoutSeconds too long
C) DNS issues only
D) etcd problems

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Slow webhooks delay all mutating/validating operations. Causes: 1) Webhook Pod overloaded or unhealthy, 2) Network latency between API server and webhook, 3) Webhook processing taking too long, 4) timeoutSeconds too high causing waits. Check failurePolicy to understand impact of failures.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)

</details>

---

### Question 97
[HARD]

How do you correlate metrics with events to diagnose issues?

A) Ignore metrics
B) Match metric timestamps with event timestamps to identify what changed when issues occurred
C) Delete old metrics
D) Reset events

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Correlation approach: 1) Identify when issue started from alerts/reports, 2) Check events around that time: `kubectl get events --sort-by=.lastTimestamp`, 3) Query metrics (CPU, memory, network) for same timeframe, 4) Look for: resource spikes, deployment changes, node issues coinciding with symptoms.

**Source:** [Tools for Monitoring Resources | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-usage-monitoring/)

</details>

---

### Question 98
[HARD]

What is the systematic approach to diagnosing unknown Kubernetes issues?

A) Restart everything
B) Start broad then narrow: check control plane, then nodes, then workloads, examining logs and events at each level
C) Delete and recreate
D) Ignore and wait

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Systematic approach: 1) Check control plane health (API server, etcd, scheduler, controller-manager), 2) Check node conditions, 3) Check affected workload status, 4) Review events chronologically, 5) Examine logs at relevant level, 6) Check recent changes (deployments, config updates), 7) Isolate: cluster-wide vs namespace vs Pod specific.

**Source:** [Troubleshooting | Kubernetes](https://kubernetes.io/docs/tasks/debug/)

</details>

---

### Question 99
[HARD]

How do you use kubectl debug to troubleshoot a node?

A) kubectl debug node doesn't exist
B) kubectl debug node/<name> -it --image=<debug-image> creates a privileged Pod with host access
C) kubectl debug --node flag only
D) kubectl ssh node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl debug node/<name> -it --image=busybox` creates a privileged debugging Pod on that node with access to host filesystem (/host), host network, and host PID namespace. This allows inspection of node-level issues, kubelet logs, and system resources directly.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/#debugging-via-a-shell-on-the-node)

</details>

---

### Question 100
[HARD]

What tools help aggregate logs from multiple Pods for troubleshooting?

A) Only kubectl logs
B) kubectl logs -l <selector> or centralized logging with node-level agents
C) kubectl describe only
D) API server logs only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For multi-Pod log aggregation: 1) Use `kubectl logs -l <selector> -f` to stream logs from Pods matching a label, 2) Implement cluster-level logging using node-level agents (e.g., Fluentd, Fluent Bit) that ship logs to a backend like Elasticsearch, 3) Some cloud providers offer integrated logging solutions. Centralized logging is essential for production troubleshooting.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---
