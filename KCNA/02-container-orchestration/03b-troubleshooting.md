# Troubleshooting - 100 MCQ Questions (Part B)

**Domain:** Container Orchestration (28%)
**Competency:** Troubleshooting
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## Workload Troubleshooting

### Question 1
[MEDIUM]

What does it mean when a Deployment shows 0/3 ready replicas?

---

### Question 2
[MEDIUM]

How do you check why a ReplicaSet is not creating Pods?

---

### Question 3
[MEDIUM]

What causes a Deployment rollout to be stuck?

---

### Question 4
[MEDIUM]

How do you view the revision history of a Deployment?

---

### Question 5
[MEDIUM]

What does kubectl rollout undo do?

---

### Question 6
[MEDIUM]

How do you check the status of a DaemonSet?

---

### Question 7
[MEDIUM]

What could cause a DaemonSet to not schedule Pods on all nodes?

---

### Question 8
[MEDIUM]

How do you troubleshoot a StatefulSet with Pods stuck in Pending?

---

### Question 9
[MEDIUM]

What is the purpose of checking the Pod template in a Deployment?

---

### Question 10
[MEDIUM]

How do you identify which ReplicaSet is active for a Deployment?

---

## Service Troubleshooting

### Question 11
[MEDIUM]

What should you check first when a Service is not accessible?

---

### Question 12
[MEDIUM]

How do you verify a Service selector matches Pod labels?

---

### Question 13
[MEDIUM]

What does kubectl get endpoints show for troubleshooting Services?

---

### Question 14
[MEDIUM]

How do you test internal Service connectivity?

---

### Question 15
[MEDIUM]

What could cause a LoadBalancer Service to stay in Pending state?

---

### Question 16
[MEDIUM]

How do you troubleshoot a NodePort Service that is not accessible?

---

### Question 17
[MEDIUM]

What is the difference between ClusterIP and Endpoints in troubleshooting?

---

### Question 18
[MEDIUM]

How do you check if kube-proxy is functioning correctly?

---

### Question 19
[MEDIUM]

What causes "connection refused" errors when accessing a Service?

---

### Question 20
[MEDIUM]

How do you verify the targetPort configuration in a Service?

---

## Ingress and External Access Troubleshooting

### Question 21
[MEDIUM-HARD]

What should you check when an Ingress is not routing traffic?

---

### Question 22
[MEDIUM-HARD]

How do you verify the Ingress controller is running?

---

### Question 23
[MEDIUM-HARD]

What could cause a 404 error when accessing an Ingress path?

---

### Question 24
[MEDIUM-HARD]

How do you troubleshoot TLS certificate issues in Ingress?

---

### Question 25
[MEDIUM-HARD]

What does the Ingress ADDRESS field indicate?

---

### Question 26
[MEDIUM-HARD]

How do you check Ingress controller logs for routing issues?

---

### Question 27
[MEDIUM-HARD]

What causes "502 Bad Gateway" errors in Ingress?

---

### Question 28
[MEDIUM-HARD]

How do you verify backend Service health from the Ingress perspective?

---

### Question 29
[MEDIUM-HARD]

What should you check when Ingress annotations are not working?

---

### Question 30
[MEDIUM-HARD]

How do you troubleshoot path-based routing in Ingress?

---

## ConfigMap and Secret Troubleshooting

### Question 31
[MEDIUM-HARD]

What happens when a Pod references a non-existent ConfigMap?

---

### Question 32
[MEDIUM-HARD]

How do you troubleshoot environment variables not being set from ConfigMaps?

---

### Question 33
[MEDIUM-HARD]

What causes volume mount failures for ConfigMaps?

---

### Question 34
[MEDIUM-HARD]

How do you check if a Secret was correctly mounted in a container?

---

### Question 35
[MEDIUM-HARD]

What is the impact of updating a ConfigMap on running Pods?

---

### Question 36
[MEDIUM-HARD]

How do you troubleshoot imagePullSecrets issues?

---

### Question 37
[MEDIUM-HARD]

What could cause "secret not found" errors during Pod creation?

---

### Question 38
[MEDIUM-HARD]

How do you verify the contents of a mounted ConfigMap?

---

### Question 39
[MEDIUM-HARD]

What happens when a ConfigMap used as a volume is deleted?

---

### Question 40
[MEDIUM-HARD]

How do you troubleshoot subPath mount issues with ConfigMaps?

---

## Job and CronJob Troubleshooting

### Question 41
[HARD]

What does a Job status of "1/1 Completions" indicate?

---

### Question 42
[HARD]

How do you troubleshoot a Job that keeps creating new Pods?

---

### Question 43
[HARD]

What causes a Job to reach its backoffLimit?

---

### Question 44
[HARD]

How do you check why a CronJob is not triggering?

---

### Question 45
[HARD]

What does the "Suspend" field in CronJob do?

---

### Question 46
[HARD]

How do you troubleshoot overlapping CronJob executions?

---

### Question 47
[HARD]

What is the purpose of activeDeadlineSeconds in Jobs?

---

### Question 48
[HARD]

How do you identify failed Job Pods?

---

### Question 49
[HARD]

What causes "Too many missed start times" in CronJobs?

---

### Question 50
[HARD]

How do you troubleshoot a Job with parallelism issues?

---

## Namespace and Resource Quota Issues

### Question 51
[HARD]

What happens when a namespace has no available ResourceQuota?

---

### Question 52
[HARD]

How do you check current resource usage against quotas?

---

### Question 53
[HARD]

What causes "exceeded quota" errors during Pod creation?

---

### Question 54
[HARD]

How do you troubleshoot LimitRange violations?

---

### Question 55
[HARD]

What is the impact of deleting a namespace on its resources?

---

### Question 56
[HARD]

How do you identify pods consuming the most resources in a namespace?

---

### Question 57
[HARD]

What happens when a namespace is stuck in Terminating state?

---

### Question 58
[HARD]

How do you troubleshoot cross-namespace communication issues?

---

### Question 59
[HARD]

What causes namespace isolation to fail?

---

### Question 60
[HARD]

How do you verify ResourceQuota is correctly applied?

---

## Cluster Component Diagnostics

### Question 61
[HARD]

How do you diagnose slow API server responses?

---

### Question 62
[HARD]

What metrics indicate control plane health issues?

---

### Question 63
[HARD]

How do you troubleshoot leader election failures?

---

### Question 64
[HARD]

What causes watch connection drops from the API server?

---

### Question 65
[HARD]

How do you check for etcd cluster health?

---

### Question 66
[HARD]

What indicates etcd disk I/O problems?

---

### Question 67
[HARD]

How do you troubleshoot admission webhook failures?

---

### Question 68
[HARD]

What causes "unable to retrieve container logs" errors?

---

### Question 69
[HARD]

How do you diagnose controller reconciliation issues?

---

### Question 70
[HARD]

What should you check when Custom Resources are not being processed?

---

## Multi-Container Pod Issues

### Question 71
[HARD]

How do you troubleshoot sidecar container failures?

---

### Question 72
[HARD]

What causes init container ordering issues?

---

### Question 73
[HARD]

How do you identify which container is causing Pod restarts?

---

### Question 74
[HARD]

What happens when containers share a volume incorrectly?

---

### Question 75
[HARD]

How do you troubleshoot inter-container communication within a Pod?

---

### Question 76
[HARD]

What causes one container to affect another in the same Pod?

---

### Question 77
[HARD]

How do you check resource consumption per container in a multi-container Pod?

---

### Question 78
[HARD]

What indicates a lifecycle hook failure?

---

### Question 79
[HARD]

How do you troubleshoot postStart hook issues?

---

### Question 80
[HARD]

What happens when a preStop hook times out?

---

## Security and Access Troubleshooting

### Question 81
[HARD]

How do you troubleshoot ServiceAccount permission issues?

---

### Question 82
[HARD]

What causes "Forbidden" errors when accessing the API?

---

### Question 83
[HARD]

How do you verify Pod security context is applied correctly?

---

### Question 84
[HARD]

What indicates SecurityContext conflicts?

---

### Question 85
[HARD]

How do you troubleshoot PodSecurityPolicy violations?

---

### Question 86
[HARD]

What causes service account token mount failures?

---

### Question 87
[HARD]

How do you check if a Pod has the required capabilities?

---

### Question 88
[HARD]

What indicates a seccomp profile is blocking syscalls?

---

### Question 89
[HARD]

How do you troubleshoot AppArmor profile issues?

---

### Question 90
[HARD]

What causes "operation not permitted" errors in containers?

---

## Advanced Diagnostics

### Question 91
[HARD]

How do you use audit logs to troubleshoot issues?

---

### Question 92
[HARD]

What information do Kubernetes events provide for troubleshooting?

---

### Question 93
[HARD]

How do you correlate metrics with cluster issues?

---

### Question 94
[HARD]

What is the role of the conditions field in resource troubleshooting?

---

### Question 95
[HARD]

How do you troubleshoot webhook timeout issues?

---

### Question 96
[HARD]

What causes garbage collection to fail?

---

### Question 97
[HARD]

How do you diagnose finalizer-related stuck resources?

---

### Question 98
[HARD]

What indicates a controller is not watching resources correctly?

---

### Question 99
[HARD]

How do you troubleshoot CRD validation errors?

---

### Question 100
[HARD]

What is the systematic approach to diagnosing unknown cluster issues?

---
