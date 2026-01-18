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

---

### Question 2
[MEDIUM]

Which command displays the events associated with a specific Pod?

A) kubectl logs <pod-name>
B) kubectl describe pod <pod-name>
C) kubectl get pod <pod-name> --events
D) kubectl events <pod-name>

---

### Question 3
[MEDIUM]

What does the "CrashLoopBackOff" status indicate?

A) The container image cannot be pulled
B) The container keeps crashing and Kubernetes is waiting before restarting it
C) The Pod is pending scheduling
D) The node is under memory pressure

---

### Question 4
[MEDIUM]

Which command is used to view container logs in a Pod?

A) kubectl describe pod <pod-name>
B) kubectl logs <pod-name>
C) kubectl get logs <pod-name>
D) kubectl show logs <pod-name>

---

### Question 5
[MEDIUM]

What does the "ImagePullBackOff" status indicate?

A) The container is running out of memory
B) Kubernetes is waiting before retrying a failed image pull
C) The Pod is waiting for a volume to be mounted
D) The container is restarting repeatedly

---

### Question 6
[MEDIUM]

How do you check why a Pod is stuck in Pending state?

A) kubectl logs <pod-name>
B) kubectl describe pod <pod-name>
C) kubectl exec <pod-name> -- cat /var/log/messages
D) kubectl top pod <pod-name>

---

### Question 7
[MEDIUM]

What is the purpose of kubectl describe pod?

A) To delete a Pod
B) To show detailed information including events, status, and configuration
C) To update a Pod's configuration
D) To view only the container logs

---

### Question 8
[MEDIUM]

Which field in Pod status shows the reason for container termination?

A) status.phase
B) status.containerStatuses[].state.terminated.reason
C) status.message
D) spec.terminationReason

---

### Question 9
[MEDIUM]

What does "ErrImagePull" status mean?

A) The container has insufficient CPU
B) Kubernetes failed to pull the container image
C) The Pod is evicted
D) The volume mount failed

---

### Question 10
[MEDIUM]

How do you view logs from a previous container instance?

A) kubectl logs <pod-name> --previous
B) kubectl logs <pod-name> --old
C) kubectl logs <pod-name> --history
D) kubectl logs <pod-name> --last

---

## Debugging Commands

### Question 11
[MEDIUM]

What command allows you to execute a command inside a running container?

A) kubectl run
B) kubectl exec
C) kubectl attach
D) kubectl shell

---

### Question 12
[MEDIUM]

How do you get a shell session inside a running container?

A) kubectl shell <pod-name>
B) kubectl exec -it <pod-name> -- /bin/sh
C) kubectl connect <pod-name>
D) kubectl attach <pod-name> --shell

---

### Question 13
[MEDIUM]

What is the purpose of the kubectl debug command?

A) To view debug logs only
B) To create debugging sessions using ephemeral containers or copy of Pods
C) To enable debug mode on the API server
D) To increase log verbosity

---

### Question 14
[MEDIUM]

How do you view logs from a specific container in a multi-container Pod?

A) kubectl logs <pod-name> --all
B) kubectl logs <pod-name> -c <container-name>
C) kubectl logs <pod-name>/<container-name>
D) kubectl logs --container=<container-name> <pod-name>

---

### Question 15
[MEDIUM]

What does kubectl get events show?

A) Only Pod creation events
B) Cluster-wide events including warnings, errors, and normal events
C) Only error events
D) Node metrics

---

### Question 16
[MEDIUM]

How do you follow (stream) logs from a container in real-time?

A) kubectl logs <pod-name> --stream
B) kubectl logs <pod-name> -f
C) kubectl logs <pod-name> --live
D) kubectl logs <pod-name> --tail

---

### Question 17
[MEDIUM]

What command shows the resource usage of Pods?

A) kubectl describe pod
B) kubectl top pod
C) kubectl resources pod
D) kubectl usage pod

---

### Question 18
[MEDIUM]

How do you check the rollout status of a Deployment?

A) kubectl describe deployment
B) kubectl rollout status deployment/<name>
C) kubectl get deployment --status
D) kubectl deployment status <name>

---

### Question 19
[MEDIUM]

What is the purpose of kubectl port-forward?

A) To expose a Service externally
B) To forward local ports to a Pod for debugging
C) To change the container port
D) To configure port mapping in a Service

---

### Question 20
[MEDIUM]

How do you view the YAML definition of a running Pod?

A) kubectl describe pod <pod-name> --yaml
B) kubectl get pod <pod-name> -o yaml
C) kubectl export pod <pod-name>
D) kubectl show pod <pod-name> --format=yaml

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

---

### Question 27
[MEDIUM-HARD]

How do you cordon a node to prevent new Pod scheduling?

---

### Question 28
[MEDIUM-HARD]

What is the difference between cordon and drain?

---

### Question 29
[MEDIUM-HARD]

Which component is responsible for reporting node status?

---

### Question 30
[MEDIUM-HARD]

What does the "PIDPressure" node condition indicate?

---

## Network Troubleshooting

### Question 31
[MEDIUM-HARD]

How do you test DNS resolution from within a Pod?

---

### Question 32
[MEDIUM-HARD]

What is the default DNS service name in Kubernetes?

---

### Question 33
[MEDIUM-HARD]

How do you check if a Service is reachable from a Pod?

---

### Question 34
[MEDIUM-HARD]

What could cause a Service to have no endpoints?

---

### Question 35
[MEDIUM-HARD]

How do you verify that a NetworkPolicy is working correctly?

---

### Question 36
[MEDIUM-HARD]

What command shows the endpoints for a Service?

---

### Question 37
[MEDIUM-HARD]

How do you troubleshoot inter-Pod communication issues?

---

### Question 38
[MEDIUM-HARD]

What does it mean when a Service has "Endpoints: <none>"?

---

### Question 39
[MEDIUM-HARD]

How do you check if CoreDNS is running properly?

---

### Question 40
[MEDIUM-HARD]

What is the FQDN format for a Service in Kubernetes?

---

## Resource and OOM Issues

### Question 41
[HARD]

What does the "OOMKilled" termination reason indicate?

---

### Question 42
[HARD]

How do you identify which container in a Pod was OOMKilled?

---

### Question 43
[HARD]

What is the difference between resource requests and limits in troubleshooting context?

---

### Question 44
[HARD]

How do you check the actual resource usage of a container?

---

### Question 45
[HARD]

What happens when a container exceeds its memory limit?

---

### Question 46
[HARD]

What happens when a container exceeds its CPU limit?

---

### Question 47
[HARD]

How do you troubleshoot a Pod that keeps getting evicted?

---

### Question 48
[HARD]

What is the QoS class of a Pod and how does it affect eviction?

---

### Question 49
[HARD]

How do you check if a ResourceQuota is blocking Pod creation?

---

### Question 50
[HARD]

What does the "Evicted" Pod status indicate?

---

## Control Plane Troubleshooting

### Question 51
[HARD]

How do you check the health of the kube-apiserver?

---

### Question 52
[HARD]

What are the common symptoms of etcd issues?

---

### Question 53
[HARD]

How do you view logs from control plane components on a kubeadm cluster?

---

### Question 54
[HARD]

What happens when the kube-scheduler is not running?

---

### Question 55
[HARD]

How do you check the status of the kube-controller-manager?

---

### Question 56
[HARD]

What are common causes of API server unavailability?

---

### Question 57
[HARD]

How do you troubleshoot certificate-related issues in Kubernetes?

---

### Question 58
[HARD]

What command checks the health of cluster components?

---

### Question 59
[HARD]

How do you identify if etcd is the bottleneck?

---

### Question 60
[HARD]

What logs should you check when Pods are not being scheduled?

---

## Kubelet and Container Runtime Issues

### Question 61
[HARD]

How do you check the status of kubelet on a node?

---

### Question 62
[HARD]

Where are kubelet logs typically located?

---

### Question 63
[HARD]

What are common causes of kubelet failing to start?

---

### Question 64
[HARD]

How do you troubleshoot container runtime issues?

---

### Question 65
[HARD]

What does "container runtime is down" error indicate?

---

### Question 66
[HARD]

How do you check if the container runtime is responding?

---

### Question 67
[HARD]

What is the CRI and how do you troubleshoot CRI issues?

---

### Question 68
[HARD]

How do you identify kubelet connectivity issues with the API server?

---

### Question 69
[HARD]

What could cause kubelet to report "PLEG is not healthy"?

---

### Question 70
[HARD]

How do you troubleshoot image pull failures from private registries?

---

## Storage Troubleshooting

### Question 71
[HARD]

What does a PVC status of "Pending" indicate?

---

### Question 72
[HARD]

How do you troubleshoot a Pod stuck waiting for volume mount?

---

### Question 73
[HARD]

What causes a "FailedMount" warning in Pod events?

---

### Question 74
[HARD]

How do you check if a PersistentVolume is correctly bound?

---

### Question 75
[HARD]

What does "VolumeBindingWaitForFirstConsumer" mean?

---

### Question 76
[HARD]

How do you troubleshoot NFS mount failures?

---

### Question 77
[HARD]

What are common causes of "Unable to attach or mount volumes"?

---

### Question 78
[HARD]

How do you identify storage class issues?

---

### Question 79
[HARD]

What does the "FailedAttachVolume" event indicate?

---

### Question 80
[HARD]

How do you troubleshoot CSI driver issues?

---

## Application and Probe Issues

### Question 81
[HARD]

What happens when a liveness probe fails?

---

### Question 82
[HARD]

What happens when a readiness probe fails?

---

### Question 83
[HARD]

How do you troubleshoot a container that keeps restarting due to probe failures?

---

### Question 84
[HARD]

What are common causes of probe failures?

---

### Question 85
[HARD]

How do you check the probe configuration of a running Pod?

---

### Question 86
[HARD]

What is the difference between startup probe and liveness probe failures?

---

### Question 87
[HARD]

How do you identify if an application is failing health checks?

---

### Question 88
[HARD]

What does "Unhealthy" in Pod events indicate?

---

### Question 89
[HARD]

How do you troubleshoot slow-starting containers that fail liveness probes?

---

### Question 90
[HARD]

What probe settings should you check when containers keep restarting?

---

## Advanced Troubleshooting

### Question 91
[HARD]

How do you use ephemeral debug containers?

---

### Question 92
[HARD]

What is the purpose of kubectl debug node?

---

### Question 93
[HARD]

How do you troubleshoot a Pod that cannot resolve external DNS names?

---

### Question 94
[HARD]

What tools can you use to capture network traffic in a Pod?

---

### Question 95
[HARD]

How do you troubleshoot intermittent Pod failures?

---

### Question 96
[HARD]

What is the purpose of the terminationMessagePath field?

---

### Question 97
[HARD]

How do you analyze a core dump from a crashed container?

---

### Question 98
[HARD]

What is the best approach to troubleshoot init container failures?

---

### Question 99
[HARD]

How do you troubleshoot RBAC permission denied errors?

---

### Question 100
[HARD]

What is the systematic approach to troubleshooting a non-responsive application?

---
