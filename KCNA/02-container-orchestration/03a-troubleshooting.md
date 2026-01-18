# Troubleshooting - 100 MCQ Questions (Part A)

**Domain:** Container Orchestration (28%)
**Competency:** Troubleshooting
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## Pod Status Troubleshooting

### Question 1
[MEDIUM]

What does the Pod status "Pending" indicate?

A) The Pod is running but not ready
B) The Pod has been accepted but is not yet scheduled or has unmet dependencies
C) The Pod has completed successfully
D) The Pod is being deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod in Pending status has been accepted by the Kubernetes system but is not yet running. This can occur because the Pod is waiting to be scheduled to a node, waiting for volumes to be bound, or waiting for images to be pulled. Use `kubectl describe pod` to see the specific reason.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-phase)

</details>

---

### Question 2
[MEDIUM]

Which command displays the events associated with a specific Pod?

A) kubectl logs <pod-name>
B) kubectl describe pod <pod-name>
C) kubectl get pod <pod-name> --events
D) kubectl events <pod-name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl describe pod <pod-name>` command shows detailed information about a Pod, including its events at the bottom of the output. Events provide valuable troubleshooting information such as scheduling decisions, image pulls, and container state changes.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 3
[MEDIUM]

What does the "CrashLoopBackOff" status indicate?

A) The container image cannot be pulled
B) The container keeps crashing and Kubernetes is waiting before restarting it
C) The Pod is pending scheduling
D) The node is under memory pressure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CrashLoopBackOff indicates that a container is repeatedly crashing after starting. Kubernetes uses an exponential backoff delay (10s, 20s, 40s, up to 5 minutes) before restarting the container again. Check container logs with `kubectl logs` to diagnose the crash cause.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/#my-pod-is-crashing-or-otherwise-unhealthy)

</details>

---

### Question 4
[MEDIUM]

Which command is used to view container logs in a Pod?

A) kubectl describe pod <pod-name>
B) kubectl logs <pod-name>
C) kubectl get logs <pod-name>
D) kubectl show logs <pod-name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl logs <pod-name>` command retrieves the logs from a container in a Pod. For multi-container Pods, use the `-c` flag to specify the container. This is essential for debugging application issues and understanding why containers might be failing.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 5
[MEDIUM]

What does the "ImagePullBackOff" status indicate?

A) The container is running out of memory
B) Kubernetes is waiting before retrying a failed image pull
C) The Pod is waiting for a volume to be mounted
D) The container is restarting repeatedly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ImagePullBackOff indicates that Kubernetes failed to pull the container image and is waiting before retrying. Common causes include incorrect image names, missing registry credentials, network issues, or the image not existing. Use `kubectl describe pod` to see the specific error.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

---

### Question 6
[MEDIUM]

How do you check why a Pod is stuck in Pending state?

A) kubectl logs <pod-name>
B) kubectl describe pod <pod-name>
C) kubectl exec <pod-name> -- cat /var/log/messages
D) kubectl top pod <pod-name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Pod is stuck in Pending, `kubectl describe pod <pod-name>` shows the reason in the Events section. Common causes include insufficient resources, node selector or affinity mismatches, taints without tolerations, or pending PersistentVolumeClaims.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/#my-pod-stays-pending)

</details>

---

### Question 7
[MEDIUM]

What is the purpose of kubectl describe pod?

A) To delete a Pod
B) To show detailed information including events, status, and configuration
C) To update a Pod's configuration
D) To view only the container logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl describe pod` command provides comprehensive information about a Pod including its configuration, status, conditions, volumes, events, and container states. This is one of the most important troubleshooting commands for understanding Pod issues.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 8
[MEDIUM]

Which field in Pod status shows the reason for container termination?

A) status.phase
B) status.containerStatuses[].state.terminated.reason
C) status.message
D) spec.terminationReason

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The termination reason is found in `status.containerStatuses[].state.terminated.reason`. Common values include "Completed" (exit code 0), "Error" (non-zero exit), and "OOMKilled" (out of memory). The exitCode field provides the actual exit code.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-states)

</details>

---

### Question 9
[MEDIUM]

What does "ErrImagePull" status mean?

A) The container has insufficient CPU
B) Kubernetes failed to pull the container image
C) The Pod is evicted
D) The volume mount failed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ErrImagePull indicates an immediate failure to pull a container image. This differs from ImagePullBackOff, which is the state after repeated failures. Common causes include wrong image name, authentication issues, network problems, or registry unavailability.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

---

### Question 10
[MEDIUM]

How do you view logs from a previous container instance?

A) kubectl logs <pod-name> --previous
B) kubectl logs <pod-name> --old
C) kubectl logs <pod-name> --history
D) kubectl logs <pod-name> --last

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The `kubectl logs <pod-name> --previous` (or `-p`) flag retrieves logs from the previous instance of a container. This is essential for debugging CrashLoopBackOff situations where the current container has restarted and the crash logs are in the previous instance.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

## Debugging Commands

### Question 11
[MEDIUM]

What command allows you to execute a command inside a running container?

A) kubectl run
B) kubectl exec
C) kubectl attach
D) kubectl shell

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl exec` command executes a command inside a running container. Use `kubectl exec <pod-name> -- <command>` for single commands or `kubectl exec -it <pod-name> -- /bin/sh` for an interactive shell session.

**Source:** [Get a Shell to a Running Container | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)

</details>

---

### Question 12
[MEDIUM]

How do you get a shell session inside a running container?

A) kubectl shell <pod-name>
B) kubectl exec -it <pod-name> -- /bin/sh
C) kubectl connect <pod-name>
D) kubectl attach <pod-name> --shell

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To get an interactive shell inside a container, use `kubectl exec -it <pod-name> -- /bin/sh` (or /bin/bash if available). The `-i` flag keeps stdin open and `-t` allocates a TTY. For multi-container Pods, add `-c <container-name>`.

**Source:** [Get a Shell to a Running Container | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/get-shell-running-container/)

</details>

---

### Question 13
[MEDIUM]

What is the purpose of the kubectl debug command?

A) To view debug logs only
B) To create debugging sessions using ephemeral containers or copy of Pods
C) To enable debug mode on the API server
D) To increase log verbosity

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl debug` command creates debugging sessions by adding ephemeral containers to running Pods, creating a copy of a Pod with modifications, or creating a debugging Pod on a node. This is useful when containers lack debugging tools.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

---

### Question 14
[MEDIUM]

How do you view logs from a specific container in a multi-container Pod?

A) kubectl logs <pod-name> --all
B) kubectl logs <pod-name> -c <container-name>
C) kubectl logs <pod-name>/<container-name>
D) kubectl logs --container=<container-name> <pod-name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl logs <pod-name> -c <container-name>` to view logs from a specific container in a multi-container Pod. Without the `-c` flag, kubectl will prompt you to select a container if there are multiple containers in the Pod.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 15
[MEDIUM]

What does kubectl get events show?

A) Only Pod creation events
B) Cluster-wide events including warnings, errors, and normal events
C) Only error events
D) Node metrics

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl get events` command shows cluster-wide events including Normal and Warning types. Events provide information about what is happening in the cluster such as Pod scheduling, image pulls, volume mounts, and errors. Use `--sort-by='.lastTimestamp'` to sort by time.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 16
[MEDIUM]

How do you follow (stream) logs from a container in real-time?

A) kubectl logs <pod-name> --stream
B) kubectl logs <pod-name> -f
C) kubectl logs <pod-name> --live
D) kubectl logs <pod-name> --tail

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `-f` (or `--follow`) flag streams logs from a container in real-time, similar to `tail -f`. This is useful for watching application behavior as it happens. Combine with `--tail=N` to start from the last N lines.

**Source:** [Debug Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-pods/)

</details>

---

### Question 17
[MEDIUM]

What command shows the resource usage of Pods?

A) kubectl describe pod
B) kubectl top pod
C) kubectl resources pod
D) kubectl usage pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl top pod` command displays CPU and memory usage of Pods. This requires the Metrics Server to be installed in the cluster. Use `kubectl top pod --containers` to see per-container usage or `kubectl top nodes` for node-level metrics.

**Source:** [Resource Metrics Pipeline | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/)

</details>

---

### Question 18
[MEDIUM]

How do you check the rollout status of a Deployment?

A) kubectl describe deployment
B) kubectl rollout status deployment/<name>
C) kubectl get deployment --status
D) kubectl deployment status <name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl rollout status deployment/<name>` command shows the progress of a Deployment rollout. It displays whether the rollout is complete, in progress, or has stalled. This is useful for monitoring updates and detecting issues during deployments.

**Source:** [Managing Resources | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)

</details>

---

### Question 19
[MEDIUM]

What is the purpose of kubectl port-forward?

A) To expose a Service externally
B) To forward local ports to a Pod for debugging
C) To change the container port
D) To configure port mapping in a Service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl port-forward` command forwards one or more local ports to a Pod, allowing you to access applications running in the cluster from your local machine without exposing them externally. This is useful for debugging and testing.

**Source:** [Use Port Forwarding to Access Applications in a Cluster | Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/)

</details>

---

### Question 20
[MEDIUM]

How do you view the YAML definition of a running Pod?

A) kubectl describe pod <pod-name> --yaml
B) kubectl get pod <pod-name> -o yaml
C) kubectl export pod <pod-name>
D) kubectl show pod <pod-name> --format=yaml

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl get pod <pod-name> -o yaml` to output the full YAML definition of a running Pod, including its current status. You can also use `-o json` for JSON format. This shows both the spec and current status of the resource.

**Source:** [kubectl Cheat Sheet | Kubernetes](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

</details>

---

## Node Troubleshooting

### Question 21
[MEDIUM-HARD]

What does a Node condition of "Ready: False" indicate?

A) The node is healthy and accepting Pods
B) The node is not healthy and may have issues with kubelet, networking, or resources
C) The node is being upgraded
D) The node is cordoned

---

### Question 22
[MEDIUM-HARD]

Which command shows the status of all nodes in a cluster?

A) kubectl describe nodes
B) kubectl get nodes
C) kubectl status nodes
D) kubectl list nodes

---

### Question 23
[MEDIUM-HARD]

What does the "DiskPressure" node condition indicate?

A) The node has high CPU usage
B) The node's available disk space is low
C) The node has network issues
D) The node's memory is full

---

### Question 24
[MEDIUM-HARD]

How do you check why a node is in NotReady state?

A) kubectl logs node/<node-name>
B) kubectl describe node <node-name>
C) kubectl get node <node-name> --reason
D) kubectl debug node <node-name>

---

### Question 25
[MEDIUM-HARD]

What is the "MemoryPressure" node condition?

A) The node has high CPU utilization
B) The node's available memory is below the eviction threshold
C) The node's disk is full
D) The node has too many Pods

---

### Question 26
[MEDIUM-HARD]

What happens to Pods when a node becomes NotReady?

A) Pods are immediately deleted
B) After a timeout, Pods may be evicted and rescheduled to other nodes
C) Pods continue running normally
D) Pods are paused until the node recovers

---

### Question 27
[MEDIUM-HARD]

How do you cordon a node to prevent new Pod scheduling?

A) kubectl taint node <node-name>
B) kubectl cordon <node-name>
C) kubectl disable <node-name>
D) kubectl pause <node-name>

---

### Question 28
[MEDIUM-HARD]

What is the difference between cordon and drain?

A) They are the same operation
B) Cordon prevents new Pods; drain also evicts existing Pods
C) Drain prevents new Pods; cordon evicts existing Pods
D) Cordon is for nodes; drain is for namespaces

---

### Question 29
[MEDIUM-HARD]

Which component is responsible for reporting node status?

A) kube-scheduler
B) kubelet
C) kube-controller-manager
D) kube-proxy

---

### Question 30
[MEDIUM-HARD]

What does the "PIDPressure" node condition indicate?

A) The node has too many processes running
B) The node is running low on available process IDs
C) The node's CPU is overloaded
D) The node has network issues

---

## Network Troubleshooting

### Question 31
[MEDIUM-HARD]

How do you test DNS resolution from within a Pod?

A) kubectl dns test
B) kubectl exec <pod> -- nslookup <service-name>
C) kubectl resolve <service-name>
D) kubectl network test dns

---

### Question 32
[MEDIUM-HARD]

What is the default DNS service name in Kubernetes?

A) dns-service
B) kube-dns
C) cluster-dns
D) core-dns

---

### Question 33
[MEDIUM-HARD]

How do you check if a Service is reachable from a Pod?

A) kubectl test service <service-name>
B) kubectl exec <pod> -- curl <service-name>:<port> or wget
C) kubectl ping <service-name>
D) kubectl connect <service-name>

---

### Question 34
[MEDIUM-HARD]

What could cause a Service to have no endpoints?

A) The Service port is incorrect
B) No Pods match the Service selector, or matching Pods are not ready
C) The Service type is ClusterIP
D) The namespace is wrong

---

### Question 35
[MEDIUM-HARD]

How do you verify that a NetworkPolicy is working correctly?

A) kubectl test networkpolicy
B) Test connectivity from affected Pods and verify traffic is allowed or blocked as expected
C) kubectl validate networkpolicy
D) kubectl describe networkpolicy shows test results

---

### Question 36
[MEDIUM-HARD]

What command shows the endpoints for a Service?

A) kubectl get service <name> --endpoints
B) kubectl get endpoints <service-name>
C) kubectl describe endpoints
D) kubectl list endpoints <service-name>

---

### Question 37
[MEDIUM-HARD]

How do you troubleshoot inter-Pod communication issues?

A) Only check NetworkPolicies
B) Check Pod IPs, DNS resolution, NetworkPolicies, and CNI plugin status
C) Restart all Pods
D) Only check the CNI plugin

---

### Question 38
[MEDIUM-HARD]

What does it mean when a Service has "Endpoints: <none>"?

A) The Service is working correctly
B) No Pods match the Service selector or no matching Pods are ready
C) The Service is of type ExternalName
D) The endpoints are being updated

---

### Question 39
[MEDIUM-HARD]

How do you check if CoreDNS is running properly?

A) kubectl get dns
B) kubectl get pods -n kube-system -l k8s-app=kube-dns
C) kubectl dns status
D) kubectl check coredns

---

### Question 40
[MEDIUM-HARD]

What is the FQDN format for a Service in Kubernetes?

A) <service-name>.<namespace>
B) <service-name>.<namespace>.svc.cluster.local
C) <namespace>.<service-name>.local
D) <service-name>.cluster.local

---

## Resource and OOM Issues

### Question 41
[HARD]

What does the "OOMKilled" termination reason indicate?

A) The container ran out of CPU
B) The container exceeded its memory limit and was killed by the kernel
C) The container crashed due to an application error
D) The Pod was evicted due to node pressure

---

### Question 42
[HARD]

How do you identify which container in a Pod was OOMKilled?

A) kubectl logs <pod-name>
B) kubectl describe pod <pod-name> and check containerStatuses for terminated reason
C) kubectl top pod <pod-name>
D) kubectl events <pod-name>

---

### Question 43
[HARD]

What is the difference between resource requests and limits in troubleshooting context?

A) They are the same thing
B) Requests affect scheduling; limits affect runtime enforcement and OOM kills
C) Limits affect scheduling; requests affect runtime
D) Neither affects Pod behavior

---

### Question 44
[HARD]

How do you check the actual resource usage of a container?

A) kubectl describe pod
B) kubectl top pod <pod-name> --containers
C) kubectl usage <pod-name>
D) kubectl resources <pod-name>

---

### Question 45
[HARD]

What happens when a container exceeds its memory limit?

A) The container is throttled
B) The container is OOMKilled by the kernel
C) The container continues running
D) The Pod is rescheduled

---

### Question 46
[HARD]

What happens when a container exceeds its CPU limit?

A) The container is killed
B) The container is throttled but not killed
C) The Pod is evicted
D) The node becomes NotReady

---

### Question 47
[HARD]

How do you troubleshoot a Pod that keeps getting evicted?

A) Increase the node count
B) Check node conditions, resource pressure, Pod QoS class, and resource requests
C) Delete and recreate the Pod
D) Change the Pod priority

---

### Question 48
[HARD]

What is the QoS class of a Pod and how does it affect eviction?

A) QoS class determines Pod priority; Guaranteed Pods are evicted last
B) QoS class only affects scheduling
C) QoS class determines network priority
D) QoS class has no effect on eviction

---

### Question 49
[HARD]

How do you check if a ResourceQuota is blocking Pod creation?

A) kubectl logs
B) kubectl describe resourcequota and kubectl describe pod to see quota-related events
C) kubectl get quota --status
D) kubectl quota check

---

### Question 50
[HARD]

What does the "Evicted" Pod status indicate?

A) The Pod was manually deleted
B) The Pod was evicted due to node resource pressure
C) The Pod completed successfully
D) The Pod failed a health check

---

## Control Plane Troubleshooting

### Question 51
[HARD]

How do you check the health of the kube-apiserver?

A) kubectl get apiserver
B) Access the /healthz or /livez endpoints, or check Pod status in kube-system
C) kubectl describe apiserver
D) kubectl health apiserver

---

### Question 52
[HARD]

What are the common symptoms of etcd issues?

A) Only network problems
B) Slow API responses, failed writes, cluster instability, leader election failures
C) Only Pod scheduling issues
D) Only authentication failures

---

### Question 53
[HARD]

How do you view logs from control plane components on a kubeadm cluster?

A) kubectl logs -n default
B) kubectl logs -n kube-system <component-pod-name> or journalctl for static pods
C) cat /var/log/kubernetes
D) kubectl describe controlplane

---

### Question 54
[HARD]

What happens when the kube-scheduler is not running?

A) Pods are scheduled randomly
B) New Pods remain in Pending state and are not assigned to nodes
C) Existing Pods are terminated
D) The cluster shuts down

---

### Question 55
[HARD]

How do you check the status of the kube-controller-manager?

A) kubectl get controllers
B) kubectl get pods -n kube-system and check controller-manager pod, or access /healthz
C) kubectl describe controller-manager
D) kubectl status controller-manager

---

### Question 56
[HARD]

What are common causes of API server unavailability?

A) Only network issues
B) Certificate expiry, etcd unavailability, resource exhaustion, misconfigurations
C) Only Pod failures
D) Only DNS issues

---

### Question 57
[HARD]

How do you troubleshoot certificate-related issues in Kubernetes?

A) Restart all components
B) Check certificate expiry dates, verify CA chain, check component logs for TLS errors
C) Delete and recreate certificates automatically
D) Ignore certificate errors

---

### Question 58
[HARD]

What command checks the health of cluster components?

A) kubectl health
B) kubectl get componentstatuses (deprecated) or check /healthz endpoints
C) kubectl cluster-health
D) kubectl status components

---

### Question 59
[HARD]

How do you identify if etcd is the bottleneck?

A) Only check CPU usage
B) Monitor etcd metrics, check latency, disk I/O, and etcd logs for slow operations
C) Restart etcd
D) Check Pod logs

---

### Question 60
[HARD]

What logs should you check when Pods are not being scheduled?

A) Only kubelet logs
B) kube-scheduler logs and kubectl describe pod for scheduling events
C) Only API server logs
D) Only etcd logs

---

## Kubelet and Container Runtime Issues

### Question 61
[HARD]

How do you check the status of kubelet on a node?

A) kubectl get kubelet
B) systemctl status kubelet on the node
C) kubectl describe kubelet
D) kubectl logs kubelet

---

### Question 62
[HARD]

Where are kubelet logs typically located?

A) /var/log/pods
B) journalctl -u kubelet or /var/log/kubelet.log depending on setup
C) /etc/kubernetes/logs
D) kubectl logs kubelet

---

### Question 63
[HARD]

What are common causes of kubelet failing to start?

A) Only network issues
B) Configuration errors, certificate issues, container runtime not running, resource issues
C) Only disk space issues
D) Only memory issues

---

### Question 64
[HARD]

How do you troubleshoot container runtime issues?

A) Restart the node
B) Check runtime status, logs, socket connectivity, and verify runtime configuration
C) Reinstall Kubernetes
D) Only check kubelet logs

---

### Question 65
[HARD]

What does "container runtime is down" error indicate?

A) The container is crashing
B) Kubelet cannot communicate with the container runtime (containerd, CRI-O)
C) The Pod is pending
D) The image cannot be pulled

---

### Question 66
[HARD]

How do you check if the container runtime is responding?

A) kubectl get runtime
B) crictl info or systemctl status containerd/cri-o
C) docker ps only
D) kubectl describe runtime

---

### Question 67
[HARD]

What is the CRI and how do you troubleshoot CRI issues?

A) Container Runtime Integration; restart Docker
B) Container Runtime Interface; check socket connectivity, runtime logs, and use crictl
C) Container Resource Interface; increase resources
D) Cluster Runtime Interface; restart the cluster

---

### Question 68
[HARD]

How do you identify kubelet connectivity issues with the API server?

A) Check Pod logs
B) Check kubelet logs for connection errors, verify network, certificates, and API server health
C) Restart the API server
D) Only check firewall rules

---

### Question 69
[HARD]

What could cause kubelet to report "PLEG is not healthy"?

A) Network issues only
B) Container runtime issues, high Pod count, slow disk I/O, or runtime not responding
C) Memory pressure only
D) Certificate expiry only

---

### Question 70
[HARD]

How do you troubleshoot image pull failures from private registries?

A) Use public images only
B) Check imagePullSecrets, registry credentials, network connectivity, and registry availability
C) Restart kubelet
D) Delete the Pod

---

## Storage Troubleshooting

### Question 71
[HARD]

What does a PVC status of "Pending" indicate?

A) The PVC is ready to use
B) No matching PV is available or StorageClass cannot provision a volume
C) The PVC is being deleted
D) The volume is mounted

---

### Question 72
[HARD]

How do you troubleshoot a Pod stuck waiting for volume mount?

A) Delete the Pod
B) Check PVC status, PV binding, node availability, and Pod events for mount errors
C) Increase volume size
D) Change storage class

---

### Question 73
[HARD]

What causes a "FailedMount" warning in Pod events?

A) Only permission issues
B) Volume not found, mount path issues, node cannot access storage, or CSI driver issues
C) Only network issues
D) Only Pod configuration errors

---

### Question 74
[HARD]

How do you check if a PersistentVolume is correctly bound?

A) kubectl get volume
B) kubectl get pv and verify STATUS is Bound and CLAIM shows the correct PVC
C) kubectl describe storage
D) kubectl check pv

---

### Question 75
[HARD]

What does "VolumeBindingWaitForFirstConsumer" mean?

A) The volume failed to bind
B) Volume binding is delayed until a Pod using the PVC is scheduled to a node
C) The volume is corrupted
D) The storage class is invalid

---

### Question 76
[HARD]

How do you troubleshoot NFS mount failures?

A) Restart the NFS server only
B) Check NFS server availability, network connectivity, mount permissions, and firewall rules
C) Delete the PVC
D) Change to a different storage class

---

### Question 77
[HARD]

What are common causes of "Unable to attach or mount volumes"?

A) Only Pod configuration errors
B) Volume already attached elsewhere, node issues, storage backend problems, or CSI driver failures
C) Only network issues
D) Only permission issues

---

### Question 78
[HARD]

How do you identify storage class issues?

A) kubectl get pods
B) kubectl describe storageclass, check provisioner status, and review PVC events
C) kubectl logs storageclass
D) kubectl debug storageclass

---

### Question 79
[HARD]

What does the "FailedAttachVolume" event indicate?

A) The volume is full
B) The volume could not be attached to the node, often due to cloud provider or CSI issues
C) The volume is corrupted
D) The Pod is misconfigured

---

### Question 80
[HARD]

How do you troubleshoot CSI driver issues?

A) Restart all nodes
B) Check CSI driver pods, controller logs, node plugin logs, and CSI socket connectivity
C) Reinstall Kubernetes
D) Delete all PVCs

---

## Application and Probe Issues

### Question 81
[HARD]

What happens when a liveness probe fails?

A) The Pod is rescheduled
B) The container is restarted by kubelet
C) The Pod is removed from Service endpoints
D) Nothing happens

---

### Question 82
[HARD]

What happens when a readiness probe fails?

A) The container is restarted
B) The Pod is removed from Service endpoints but keeps running
C) The Pod is deleted
D) The node is marked unhealthy

---

### Question 83
[HARD]

How do you troubleshoot a container that keeps restarting due to probe failures?

A) Disable all probes
B) Check probe configuration, test the probe endpoint manually, review container logs and events
C) Increase memory limits
D) Change the container image

---

### Question 84
[HARD]

What are common causes of probe failures?

A) Only network issues
B) Application not ready, wrong port/path, timeout too short, or application crashes
C) Only memory issues
D) Only CPU issues

---

### Question 85
[HARD]

How do you check the probe configuration of a running Pod?

A) kubectl logs <pod-name>
B) kubectl get pod <pod-name> -o yaml or kubectl describe pod <pod-name>
C) kubectl probe <pod-name>
D) kubectl health <pod-name>

---

### Question 86
[HARD]

What is the difference between startup probe and liveness probe failures?

A) They are the same
B) Startup probe failures delay liveness checks; liveness failures restart the container after startup succeeds
C) Startup probes are only for init containers
D) Liveness probes run before startup probes

---

### Question 87
[HARD]

How do you identify if an application is failing health checks?

A) Only check application logs
B) Check Pod events for Unhealthy warnings, verify probe endpoints, and test manually with kubectl exec
C) Restart the application
D) Check node status

---

### Question 88
[HARD]

What does "Unhealthy" in Pod events indicate?

A) The node is unhealthy
B) A probe (liveness, readiness, or startup) failed for the container
C) The Pod is being deleted
D) The image is corrupted

---

### Question 89
[HARD]

How do you troubleshoot slow-starting containers that fail liveness probes?

A) Remove the liveness probe
B) Add a startup probe or increase initialDelaySeconds for the liveness probe
C) Decrease the timeout
D) Increase CPU limits only

---

### Question 90
[HARD]

What probe settings should you check when containers keep restarting?

A) Only the probe path
B) initialDelaySeconds, periodSeconds, timeoutSeconds, failureThreshold, and the probe endpoint
C) Only the container port
D) Only the image tag

---

## Advanced Troubleshooting

### Question 91
[HARD]

How do you use ephemeral debug containers?

A) kubectl exec --debug
B) kubectl debug <pod-name> --image=<debug-image> --target=<container>
C) kubectl attach --debug
D) kubectl run --debug

---

### Question 92
[HARD]

What is the purpose of kubectl debug node?

A) To debug network issues only
B) To create a privileged Pod for debugging node-level issues with host access
C) To restart the node
D) To view node metrics

---

### Question 93
[HARD]

How do you troubleshoot a Pod that cannot resolve external DNS names?

A) Restart CoreDNS only
B) Check CoreDNS pods, DNS policy, upstream DNS config, and network connectivity to DNS servers
C) Delete the Pod
D) Change the namespace

---

### Question 94
[HARD]

What tools can you use to capture network traffic in a Pod?

A) Only kubectl logs
B) tcpdump, wireshark, or similar tools via kubectl exec or ephemeral debug containers
C) kubectl network capture
D) kubectl debug --network

---

### Question 95
[HARD]

How do you troubleshoot intermittent Pod failures?

A) Ignore them
B) Review historical logs, events, metrics, check for resource contention, and monitor over time
C) Restart the cluster
D) Delete and recreate the Pod

---

### Question 96
[HARD]

What is the purpose of the terminationMessagePath field?

A) To specify where logs are stored
B) To specify a file path where the container writes its termination message for debugging
C) To configure graceful shutdown
D) To set the termination grace period

---

### Question 97
[HARD]

How do you analyze a core dump from a crashed container?

A) Use kubectl logs
B) Configure the container to write core dumps to a volume, then analyze with debugging tools
C) Core dumps are not supported
D) Use kubectl describe only

---

### Question 98
[HARD]

What is the best approach to troubleshoot init container failures?

A) Skip init containers
B) Check init container logs with kubectl logs <pod> -c <init-container>, review events and status
C) Delete the Pod
D) Restart the node

---

### Question 99
[HARD]

How do you troubleshoot RBAC permission denied errors?

A) Grant cluster-admin to everyone
B) Use kubectl auth can-i, check RoleBindings/ClusterRoleBindings, and review API server audit logs
C) Restart the API server
D) Delete all RBAC resources

---

### Question 100
[HARD]

What is the systematic approach to troubleshooting a non-responsive application?

A) Immediately restart everything
B) Check Pod status, events, logs, resource usage, network connectivity, and probe health systematically
C) Delete and recreate the deployment
D) Scale down to zero replicas

---
