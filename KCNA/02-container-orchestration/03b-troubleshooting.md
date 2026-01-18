# Troubleshooting - 100 MCQ Questions (Part B)

**Domain:** Container Orchestration (28%)
**Competency:** Troubleshooting
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## Workload Troubleshooting

### Question 1
[MEDIUM]

What does it mean when a Deployment shows 0/3 ready replicas?

A) The Deployment is being deleted
B) None of the desired 3 Pods are in Ready state
C) The Deployment is paused
D) All Pods are running successfully

---

### Question 2
[MEDIUM]

How do you check why a ReplicaSet is not creating Pods?

A) kubectl logs replicaset
B) kubectl describe replicaset <name> and check events
C) kubectl get pods only
D) kubectl debug replicaset

---

### Question 3
[MEDIUM]

What causes a Deployment rollout to be stuck?

A) Too many replicas
B) Pods failing readiness probes, insufficient resources, or image pull errors
C) Network issues only
D) API server overload only

---

### Question 4
[MEDIUM]

How do you view the revision history of a Deployment?

A) kubectl get deployment --history
B) kubectl rollout history deployment/<name>
C) kubectl describe deployment --revisions
D) kubectl logs deployment

---

### Question 5
[MEDIUM]

What does kubectl rollout undo do?

A) Deletes the Deployment
B) Rolls back to the previous revision of the Deployment
C) Pauses the rollout
D) Restarts all Pods

---

### Question 6
[MEDIUM]

How do you check the status of a DaemonSet?

A) kubectl logs daemonset
B) kubectl get daemonset and kubectl describe daemonset <name>
C) kubectl status daemonset
D) kubectl top daemonset

---

### Question 7
[MEDIUM]

What could cause a DaemonSet to not schedule Pods on all nodes?

A) Too few nodes
B) Node taints without tolerations, node selectors, or affinity rules
C) Insufficient memory only
D) Network issues only

---

### Question 8
[MEDIUM]

How do you troubleshoot a StatefulSet with Pods stuck in Pending?

A) Delete the StatefulSet
B) Check PVC status, storage class, and Pod events for scheduling issues
C) Increase replicas
D) Change the service name

---

### Question 9
[MEDIUM]

What is the purpose of checking the Pod template in a Deployment?

A) To view running Pods
B) To verify container specs, resource requests, and configuration that will be applied to new Pods
C) To delete old Pods
D) To scale the Deployment

---

### Question 10
[MEDIUM]

How do you identify which ReplicaSet is active for a Deployment?

A) kubectl get deployment only
B) kubectl get replicasets -l app=<name> and check which has non-zero desired replicas
C) kubectl describe pods
D) kubectl logs deployment

---

## Service Troubleshooting

### Question 11
[MEDIUM]

What should you check first when a Service is not accessible?

A) Node status only
B) Service endpoints, Pod readiness, and selector matching
C) API server logs only
D) etcd health only

---

### Question 12
[MEDIUM]

How do you verify a Service selector matches Pod labels?

A) kubectl get service only
B) Compare kubectl describe service selector with kubectl get pods --show-labels
C) kubectl test selector
D) kubectl validate service

---

### Question 13
[MEDIUM]

What does kubectl get endpoints show for troubleshooting Services?

A) Service configuration only
B) The IP addresses and ports of Pods backing the Service
C) Network policies
D) Node information

---

### Question 14
[MEDIUM]

How do you test internal Service connectivity?

A) ping the Service
B) kubectl exec into a Pod and use curl/wget to access the Service
C) kubectl connect service
D) kubectl test service

---

### Question 15
[MEDIUM]

What could cause a LoadBalancer Service to stay in Pending state?

A) Too many Pods
B) Cloud provider integration issues or no LoadBalancer provisioner available
C) DNS issues only
D) Pod readiness failures only

---

### Question 16
[MEDIUM]

How do you troubleshoot a NodePort Service that is not accessible?

A) Check DNS only
B) Verify firewall rules, node security groups, and that Pods are ready
C) Restart kube-proxy only
D) Delete the Service

---

### Question 17
[MEDIUM]

What is the difference between ClusterIP and Endpoints in troubleshooting?

A) They are the same
B) ClusterIP is the Service virtual IP; Endpoints are actual Pod IPs that receive traffic
C) ClusterIP is for external access
D) Endpoints are always empty

---

### Question 18
[MEDIUM]

How do you check if kube-proxy is functioning correctly?

A) kubectl get proxy
B) Check kube-proxy pods/logs, and verify iptables/ipvs rules on nodes
C) kubectl describe proxy
D) kubectl test proxy

---

### Question 19
[MEDIUM]

What causes "connection refused" errors when accessing a Service?

A) DNS issues only
B) No Pods match the selector, Pods not ready, or application not listening on the port
C) Network policy blocking
D) kube-proxy failure only

---

### Question 20
[MEDIUM]

How do you verify the targetPort configuration in a Service?

A) kubectl get service only
B) Check Service targetPort matches the port the application listens on in the container
C) kubectl validate port
D) kubectl test connection

---

## Ingress and External Access Troubleshooting

### Question 21
[MEDIUM-HARD]

What should you check when an Ingress is not routing traffic?

A) Only Pod logs
B) Ingress controller status, backend Service health, and Ingress configuration
C) Only DNS settings
D) Only node status

---

### Question 22
[MEDIUM-HARD]

How do you verify the Ingress controller is running?

A) kubectl get ingress only
B) kubectl get pods -n <ingress-controller-namespace> and check controller logs
C) kubectl describe ingress only
D) kubectl test ingress

---

### Question 23
[MEDIUM-HARD]

What could cause a 404 error when accessing an Ingress path?

A) TLS issues only
B) Path not matching rules, backend Service not found, or no Pods ready
C) DNS issues only
D) Network policy blocking

---

### Question 24
[MEDIUM-HARD]

How do you troubleshoot TLS certificate issues in Ingress?

A) Ignore TLS errors
B) Verify Secret exists, contains valid cert/key, and is referenced correctly in Ingress
C) Delete the Ingress
D) Restart the API server

---

### Question 25
[MEDIUM-HARD]

What does the Ingress ADDRESS field indicate?

A) The internal cluster IP
B) The external IP or hostname where the Ingress is accessible
C) The backend Service IP
D) The Pod IP

---

### Question 26
[MEDIUM-HARD]

How do you check Ingress controller logs for routing issues?

A) kubectl logs ingress
B) kubectl logs -n <ingress-namespace> <ingress-controller-pod>
C) kubectl describe ingress only
D) kubectl get events only

---

### Question 27
[MEDIUM-HARD]

What causes "502 Bad Gateway" errors in Ingress?

A) DNS issues only
B) Backend Service or Pods not responding, or misconfigured health checks
C) TLS errors only
D) Path configuration only

---

### Question 28
[MEDIUM-HARD]

How do you verify backend Service health from the Ingress perspective?

A) Check Ingress status only
B) Verify Service endpoints exist and Pods are ready and responding
C) Check node status only
D) Restart the Ingress controller

---

### Question 29
[MEDIUM-HARD]

What should you check when Ingress annotations are not working?

A) Pod logs only
B) Verify annotation syntax, check controller supports the annotation, and review controller logs
C) DNS settings only
D) Service configuration only

---

### Question 30
[MEDIUM-HARD]

How do you troubleshoot path-based routing in Ingress?

A) Check DNS only
B) Verify path rules, pathType setting, and test with exact paths matching the configuration
C) Restart all Pods
D) Delete the Ingress

---

## ConfigMap and Secret Troubleshooting

### Question 31
[MEDIUM-HARD]

What happens when a Pod references a non-existent ConfigMap?

A) The Pod uses default values
B) The Pod fails to start and shows a warning event
C) The Pod starts without the ConfigMap
D) The ConfigMap is created automatically

---

### Question 32
[MEDIUM-HARD]

How do you troubleshoot environment variables not being set from ConfigMaps?

A) Restart the cluster
B) Verify ConfigMap exists, check envFrom/env syntax, and exec into Pod to check env vars
C) Delete the Pod only
D) Check node status only

---

### Question 33
[MEDIUM-HARD]

What causes volume mount failures for ConfigMaps?

A) Network issues only
B) ConfigMap not found, incorrect mount path, or permission issues
C) CPU limits only
D) Memory limits only

---

### Question 34
[MEDIUM-HARD]

How do you check if a Secret was correctly mounted in a container?

A) kubectl describe secret only
B) kubectl exec into the Pod and check the mount path contents
C) kubectl get secret only
D) kubectl logs only

---

### Question 35
[MEDIUM-HARD]

What is the impact of updating a ConfigMap on running Pods?

A) Pods restart automatically
B) Volume-mounted ConfigMaps update automatically; env vars require Pod restart
C) No impact at all
D) Pods are deleted

---

### Question 36
[MEDIUM-HARD]

How do you troubleshoot imagePullSecrets issues?

A) Delete the image
B) Verify Secret exists, is type kubernetes.io/dockerconfigjson, and is referenced correctly
C) Restart kubelet only
D) Change the image registry

---

### Question 37
[MEDIUM-HARD]

What could cause "secret not found" errors during Pod creation?

A) Network issues only
B) Secret doesn't exist, is in a different namespace, or name is misspelled
C) CPU limits only
D) Memory limits only

---

### Question 38
[MEDIUM-HARD]

How do you verify the contents of a mounted ConfigMap?

A) kubectl describe configmap only
B) kubectl exec <pod> -- cat /path/to/mounted/file
C) kubectl logs only
D) kubectl get configmap only

---

### Question 39
[MEDIUM-HARD]

What happens when a ConfigMap used as a volume is deleted?

A) The Pod continues with cached data
B) The mounted files disappear, potentially causing application errors
C) The Pod is automatically deleted
D) A new ConfigMap is created

---

### Question 40
[MEDIUM-HARD]

How do you troubleshoot subPath mount issues with ConfigMaps?

A) Delete the ConfigMap
B) Verify subPath matches a key in the ConfigMap and check mount path is correct
C) Increase volume size
D) Change storage class

---

## Job and CronJob Troubleshooting

### Question 41
[HARD]

What does a Job status of "1/1 Completions" indicate?

A) The Job failed
B) One Pod completed successfully out of one required completion
C) The Job is still running
D) The Job was deleted

---

### Question 42
[HARD]

How do you troubleshoot a Job that keeps creating new Pods?

A) Delete the Job only
B) Check Pod exit codes, review restartPolicy, and examine backoffLimit settings
C) Increase parallelism
D) Change the image

---

### Question 43
[HARD]

What causes a Job to reach its backoffLimit?

A) Successful completion
B) Pods failing repeatedly until the retry limit is reached
C) Too many completions
D) Network issues only

---

### Question 44
[HARD]

How do you check why a CronJob is not triggering?

A) Check Pod logs only
B) Verify schedule syntax, check CronJob status and events, and ensure it's not suspended
C) Restart the API server
D) Delete the namespace

---

### Question 45
[HARD]

What does the "Suspend" field in CronJob do?

A) Pauses running Jobs
B) Prevents new Job creation from the CronJob while set to true
C) Deletes the CronJob
D) Increases concurrency

---

### Question 46
[HARD]

How do you troubleshoot overlapping CronJob executions?

A) Increase parallelism
B) Check concurrencyPolicy setting and adjust schedule or job duration
C) Delete all Jobs
D) Change the namespace

---

### Question 47
[HARD]

What is the purpose of activeDeadlineSeconds in Jobs?

A) To set the retry limit
B) To set maximum time a Job can run before being terminated
C) To set parallelism
D) To set completions count

---

### Question 48
[HARD]

How do you identify failed Job Pods?

A) kubectl get jobs only
B) kubectl get pods --selector=job-name=<job> and check for Failed status
C) kubectl logs job only
D) kubectl describe job only

---

### Question 49
[HARD]

What causes "Too many missed start times" in CronJobs?

A) Too many completions
B) CronJob controller was unable to create Jobs for multiple scheduled times
C) Network issues only
D) Memory pressure only

---

### Question 50
[HARD]

How do you troubleshoot a Job with parallelism issues?

A) Delete all Pods
B) Check parallelism and completions settings, verify resources are available for parallel Pods
C) Increase backoffLimit
D) Change the schedule

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
