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

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "0/3 ready replicas" means the Deployment wants 3 Pods but none are currently Ready. This could be due to Pods not yet created, Pods in Pending state, containers failing to start, or readiness probes failing. Check `kubectl describe deployment` and `kubectl get pods` to diagnose.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 2
[MEDIUM]

How do you check why a ReplicaSet is not creating Pods?

A) kubectl logs replicaset
B) kubectl describe replicaset <name> and check events
C) kubectl get pods only
D) kubectl debug replicaset

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl describe replicaset <name>` to see events explaining why Pods aren't being created. Common issues include ResourceQuota limits, LimitRange violations, or Pod template problems. The Events section shows creation failures and their reasons.

**Source:** [ReplicaSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)

</details>

---

### Question 3
[MEDIUM]

What causes a Deployment rollout to be stuck?

A) Too many replicas
B) Pods failing readiness probes, insufficient resources, or image pull errors
C) Network issues only
D) API server overload only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A stuck rollout occurs when new Pods cannot become Ready. Common causes include: Pods failing readiness probes, insufficient cluster resources to schedule Pods, image pull errors, or misconfigured Pod specs. Use `kubectl rollout status` and `kubectl describe pod` to diagnose.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#failed-deployment)

</details>

---

### Question 4
[MEDIUM]

How do you view the revision history of a Deployment?

A) kubectl get deployment --history
B) kubectl rollout history deployment/<name>
C) kubectl describe deployment --revisions
D) kubectl logs deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl rollout history deployment/<name>` to view revision history. Add `--revision=N` to see details of a specific revision. The history shows revision numbers and change causes, useful for understanding what changed and for rollback decisions.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#checking-rollout-history-of-a-deployment)

</details>

---

### Question 5
[MEDIUM]

What does kubectl rollout undo do?

A) Deletes the Deployment
B) Rolls back to the previous revision of the Deployment
C) Pauses the rollout
D) Restarts all Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl rollout undo deployment/<name>` rolls back to the previous revision. Add `--to-revision=N` to roll back to a specific revision. This creates a new revision with the old Pod template, useful for recovering from failed deployments.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment)

</details>

---

### Question 6
[MEDIUM]

How do you check the status of a DaemonSet?

A) kubectl logs daemonset
B) kubectl get daemonset and kubectl describe daemonset <name>
C) kubectl status daemonset
D) kubectl top daemonset

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl get daemonset` to see desired, current, ready, and available counts. Use `kubectl describe daemonset <name>` to see detailed status, node selection criteria, and events. The counts should match the number of eligible nodes.

**Source:** [DaemonSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

</details>

---

### Question 7
[MEDIUM]

What could cause a DaemonSet to not schedule Pods on all nodes?

A) Too few nodes
B) Node taints without tolerations, node selectors, or affinity rules
C) Insufficient memory only
D) Network issues only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets might not schedule on all nodes due to: node taints that the DaemonSet doesn't tolerate, nodeSelector limiting eligible nodes, or node affinity rules excluding nodes. Check `kubectl describe daemonset` for the node selector and tolerations.

**Source:** [DaemonSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

</details>

---

### Question 8
[MEDIUM]

How do you troubleshoot a StatefulSet with Pods stuck in Pending?

A) Delete the StatefulSet
B) Check PVC status, storage class, and Pod events for scheduling issues
C) Increase replicas
D) Change the service name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSet Pods stuck in Pending often relate to storage: PVCs not being bound due to no matching PV or StorageClass provisioning failures. StatefulSets create Pods sequentially, so check the first stuck Pod's events and its PVC status with `kubectl get pvc` and `kubectl describe pod`.

**Source:** [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

</details>

---

### Question 9
[MEDIUM]

What is the purpose of checking the Pod template in a Deployment?

A) To view running Pods
B) To verify container specs, resource requests, and configuration that will be applied to new Pods
C) To delete old Pods
D) To scale the Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Pod template in a Deployment defines the spec for all Pods it creates. Checking it helps verify: container images, resource requests/limits, environment variables, volumes, and probes. Any misconfiguration here affects all Pods. View with `kubectl get deployment -o yaml`.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

### Question 10
[MEDIUM]

How do you identify which ReplicaSet is active for a Deployment?

A) kubectl get deployment only
B) kubectl get replicasets -l app=<name> and check which has non-zero desired replicas
C) kubectl describe pods
D) kubectl logs deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Deployment manages multiple ReplicaSets (one per revision). The active ReplicaSet has non-zero desired replicas while old ones have 0. Use `kubectl get replicasets -l app=<deployment-label>` to see all ReplicaSets and their replica counts to identify the current active one.

**Source:** [Deployments | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

</details>

---

## Service Troubleshooting

### Question 11
[MEDIUM]

What should you check first when a Service is not accessible?

A) Node status only
B) Service endpoints, Pod readiness, and selector matching
C) API server logs only
D) etcd health only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Service is not accessible, first check: 1) `kubectl get endpoints` to see if there are backend Pods, 2) `kubectl get pods` to verify Pods are Ready, 3) Verify selector labels match. Empty endpoints usually means no Pods match the selector or Pods aren't Ready.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 12
[MEDIUM]

How do you verify a Service selector matches Pod labels?

A) kubectl get service only
B) Compare kubectl describe service selector with kubectl get pods --show-labels
C) kubectl test selector
D) kubectl validate service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To verify selector matching: 1) `kubectl describe service <name>` shows the Selector field, 2) `kubectl get pods --show-labels` shows Pod labels. Compare them to ensure they match exactly. Even a small typo will prevent the Service from discovering Pods.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 13
[MEDIUM]

What does kubectl get endpoints show for troubleshooting Services?

A) Service configuration only
B) The IP addresses and ports of Pods backing the Service
C) Network policies
D) Node information

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl get endpoints <service-name>` shows the actual Pod IPs and ports that will receive traffic. If it shows `<none>`, no Pods match the selector or none are Ready. This is crucial for verifying that the Service has backend targets.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 14
[MEDIUM]

How do you test internal Service connectivity?

A) ping the Service
B) kubectl exec into a Pod and use curl/wget to access the Service
C) kubectl connect service
D) kubectl test service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Test Service connectivity by running `kubectl exec <pod> -- curl <service-name>:<port>` or `wget`. This tests both DNS resolution and actual connectivity. Services use TCP, so ping (ICMP) won't work. Test from within the cluster to verify internal networking.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 15
[MEDIUM]

What could cause a LoadBalancer Service to stay in Pending state?

A) Too many Pods
B) Cloud provider integration issues or no LoadBalancer provisioner available
C) DNS issues only
D) Pod readiness failures only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A LoadBalancer Service stays Pending when: the cluster isn't running on a cloud provider with LoadBalancer support, the cloud-controller-manager isn't configured, there's no MetalLB or similar on bare metal, or there are cloud API errors. Check `kubectl describe service` for events.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

</details>

---

### Question 16
[MEDIUM]

How do you troubleshoot a NodePort Service that is not accessible?

A) Check DNS only
B) Verify firewall rules, node security groups, and that Pods are ready
C) Restart kube-proxy only
D) Delete the Service

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For NodePort access issues: verify firewall/security groups allow the NodePort (30000-32767), ensure kube-proxy is running on nodes, check that Pods are Ready and endpoints exist. Test locally on the node first with `curl localhost:<nodeport>` to isolate network vs. service issues.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport)

</details>

---

### Question 17
[MEDIUM]

What is the difference between ClusterIP and Endpoints in troubleshooting?

A) They are the same
B) ClusterIP is the Service virtual IP; Endpoints are actual Pod IPs that receive traffic
C) ClusterIP is for external access
D) Endpoints are always empty

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ClusterIP is the stable virtual IP assigned to the Service. Endpoints are the actual Pod IPs and ports that receive traffic. Traffic to ClusterIP is forwarded to Endpoints by kube-proxy. If ClusterIP works but no response, check if Endpoints exist and Pods are responding.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 18
[MEDIUM]

How do you check if kube-proxy is functioning correctly?

A) kubectl get proxy
B) Check kube-proxy pods/logs, and verify iptables/ipvs rules on nodes
C) kubectl describe proxy
D) kubectl test proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify kube-proxy by: 1) `kubectl get pods -n kube-system -l k8s-app=kube-proxy` to check it's running, 2) Review kube-proxy logs for errors, 3) On nodes, check `iptables -L -t nat` or `ipvsadm -Ln` to verify Service rules exist. Missing rules indicate kube-proxy issues.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 19
[MEDIUM]

What causes "connection refused" errors when accessing a Service?

A) DNS issues only
B) No Pods match the selector, Pods not ready, or application not listening on the port
C) Network policy blocking
D) kube-proxy failure only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Connection refused" typically means: nothing is listening on the target port. This occurs when: no endpoints exist (no matching Pods or Pods not Ready), or the application inside the container isn't listening on the expected port. Check endpoints and verify the app is running and bound to the correct port.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 20
[MEDIUM]

How do you verify the targetPort configuration in a Service?

A) kubectl get service only
B) Check Service targetPort matches the port the application listens on in the container
C) kubectl validate port
D) kubectl test connection

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify targetPort by: 1) `kubectl describe service` to see the targetPort, 2) Check the Pod spec's containerPort or exec into the Pod and use `netstat -tlnp` or `ss -tlnp` to see what port the application is listening on. Mismatched ports cause connection failures.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Ingress and External Access Troubleshooting

### Question 21
[MEDIUM-HARD]

What should you check when an Ingress is not routing traffic?

A) Only Pod logs
B) Ingress controller status, backend Service health, and Ingress configuration
C) Only DNS settings
D) Only node status

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When Ingress is not routing traffic, check: 1) Ingress controller Pods are running and healthy, 2) Backend Services have endpoints (Pods are Ready), 3) Ingress rules are correctly configured with matching hosts/paths, 4) `kubectl describe ingress` for events and status.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 22
[MEDIUM-HARD]

How do you verify the Ingress controller is running?

A) kubectl get ingress only
B) kubectl get pods -n <ingress-controller-namespace> and check controller logs
C) kubectl describe ingress only
D) kubectl test ingress

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify the Ingress controller by: 1) Check controller Pods are Running: `kubectl get pods -n ingress-nginx` (namespace varies by controller), 2) Review logs: `kubectl logs -n ingress-nginx <controller-pod>`, 3) Check for configuration reload errors or backend connectivity issues in logs.

**Source:** [Ingress Controllers | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

</details>

---

### Question 23
[MEDIUM-HARD]

What could cause a 404 error when accessing an Ingress path?

A) TLS issues only
B) Path not matching rules, backend Service not found, or no Pods ready
C) DNS issues only
D) Network policy blocking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A 404 error from Ingress typically means: 1) Request path doesn't match any Ingress rules (check pathType: Prefix vs Exact), 2) Backend Service doesn't exist or is misconfigured, 3) Service has no endpoints (no Ready Pods). Use `kubectl describe ingress` and `kubectl get endpoints` to diagnose.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 24
[MEDIUM-HARD]

How do you troubleshoot TLS certificate issues in Ingress?

A) Ignore TLS errors
B) Verify Secret exists, contains valid cert/key, and is referenced correctly in Ingress
C) Delete the Ingress
D) Restart the API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Troubleshoot TLS issues by: 1) Verify Secret exists in same namespace: `kubectl get secret <tls-secret>`, 2) Ensure Secret type is `kubernetes.io/tls` with `tls.crt` and `tls.key`, 3) Check Ingress references correct Secret name, 4) Verify certificate validity with `openssl x509 -in tls.crt -text`.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)

</details>

---

### Question 25
[MEDIUM-HARD]

What does the Ingress ADDRESS field indicate?

A) The internal cluster IP
B) The external IP or hostname where the Ingress is accessible
C) The backend Service IP
D) The Pod IP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ADDRESS field in `kubectl get ingress` shows the external IP or hostname assigned by the Ingress controller for external access. If empty, the controller hasn't assigned an address yet (common with pending LoadBalancer). This is the entry point for external traffic to reach the Ingress.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 26
[MEDIUM-HARD]

How do you check Ingress controller logs for routing issues?

A) kubectl logs ingress
B) kubectl logs -n <ingress-namespace> <ingress-controller-pod>
C) kubectl describe ingress only
D) kubectl get events only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Access Ingress controller logs with: `kubectl logs -n <namespace> <controller-pod>`. For nginx-ingress: `kubectl logs -n ingress-nginx -l app.kubernetes.io/name=ingress-nginx`. Logs show upstream connection errors, configuration reloads, and routing decisions helpful for diagnosing issues.

**Source:** [Ingress Controllers | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

</details>

---

### Question 27
[MEDIUM-HARD]

What causes "502 Bad Gateway" errors in Ingress?

A) DNS issues only
B) Backend Service or Pods not responding, or misconfigured health checks
C) TLS errors only
D) Path configuration only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "502 Bad Gateway" means the Ingress controller couldn't get a response from the backend. Common causes: 1) Backend Pods not Ready or crashing, 2) Service endpoints empty, 3) Application not responding on the targetPort, 4) Health check failures. Check `kubectl get endpoints` and Pod status.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 28
[MEDIUM-HARD]

How do you verify backend Service health from the Ingress perspective?

A) Check Ingress status only
B) Verify Service endpoints exist and Pods are ready and responding
C) Check node status only
D) Restart the Ingress controller

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify backend health by: 1) `kubectl get endpoints <service>` to confirm Pod IPs exist, 2) `kubectl get pods` to check Pods are Ready, 3) Test backend directly: `kubectl exec <debug-pod> -- curl <service>:<port>`. The Ingress controller only routes to healthy backends.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 29
[MEDIUM-HARD]

What should you check when Ingress annotations are not working?

A) Pod logs only
B) Verify annotation syntax, check controller supports the annotation, and review controller logs
C) DNS settings only
D) Service configuration only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When annotations don't work: 1) Verify annotation key syntax matches your controller (e.g., `nginx.ingress.kubernetes.io/` for nginx-ingress), 2) Confirm controller version supports the annotation, 3) Check controller logs for configuration errors or warnings about unknown annotations.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 30
[MEDIUM-HARD]

How do you troubleshoot path-based routing in Ingress?

A) Check DNS only
B) Verify path rules, pathType setting, and test with exact paths matching the configuration
C) Restart all Pods
D) Delete the Ingress

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Troubleshoot path routing by: 1) Review pathType: `Prefix` matches path prefixes, `Exact` requires exact match, `ImplementationSpecific` depends on controller, 2) Check path order (more specific rules first), 3) Test with curl using exact paths, 4) Review controller logs for routing decisions.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/#path-types)

</details>

---

## ConfigMap and Secret Troubleshooting

### Question 31
[MEDIUM-HARD]

What happens when a Pod references a non-existent ConfigMap?

A) The Pod uses default values
B) The Pod fails to start and shows a warning event
C) The Pod starts without the ConfigMap
D) The ConfigMap is created automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Pod references a non-existent ConfigMap (required by default), the Pod fails to start and stays in `ContainerCreating` state. Events show "configmap not found" warnings. Use `optional: true` in the volume/env source if the ConfigMap should be optional.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 32
[MEDIUM-HARD]

How do you troubleshoot environment variables not being set from ConfigMaps?

A) Restart the cluster
B) Verify ConfigMap exists, check envFrom/env syntax, and exec into Pod to check env vars
C) Delete the Pod only
D) Check node status only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Troubleshoot ConfigMap env vars by: 1) Verify ConfigMap exists: `kubectl get configmap`, 2) Check Pod spec syntax for `envFrom` or `env.valueFrom.configMapKeyRef`, 3) Exec into Pod: `kubectl exec <pod> -- env | grep KEY`, 4) Note: env vars require Pod restart to update.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/#configmaps-and-pods)

</details>

---

### Question 33
[MEDIUM-HARD]

What causes volume mount failures for ConfigMaps?

A) Network issues only
B) ConfigMap not found, incorrect mount path, or permission issues
C) CPU limits only
D) Memory limits only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ConfigMap volume mount failures occur when: 1) ConfigMap doesn't exist in the namespace, 2) Mount path conflicts with existing directory or file, 3) Volume name mismatch between `volumes` and `volumeMounts`, 4) File permissions prevent reading. Check events with `kubectl describe pod`.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/#using-configmaps-as-files-from-a-pod)

</details>

---

### Question 34
[MEDIUM-HARD]

How do you check if a Secret was correctly mounted in a container?

A) kubectl describe secret only
B) kubectl exec into the Pod and check the mount path contents
C) kubectl get secret only
D) kubectl logs only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify Secret mounts by: `kubectl exec <pod> -- ls /path/to/secret` to see files (each key becomes a file), and `kubectl exec <pod> -- cat /path/to/secret/<key>` to view contents. Secrets are mounted as tmpfs and each data key becomes a file with its value as contents.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-files-from-a-pod)

</details>

---

### Question 35
[MEDIUM-HARD]

What is the impact of updating a ConfigMap on running Pods?

A) Pods restart automatically
B) Volume-mounted ConfigMaps update automatically; env vars require Pod restart
C) No impact at all
D) Pods are deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When ConfigMaps are updated: 1) Volume-mounted ConfigMaps are automatically updated by kubelet (with sync period delay), 2) Environment variables from ConfigMaps are NOT updated until Pod restart. SubPath volume mounts also don't receive automatic updates.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/#mounted-configmaps-are-updated-automatically)

</details>

---

### Question 36
[MEDIUM-HARD]

How do you troubleshoot imagePullSecrets issues?

A) Delete the image
B) Verify Secret exists, is type kubernetes.io/dockerconfigjson, and is referenced correctly
C) Restart kubelet only
D) Change the image registry

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Troubleshoot imagePullSecrets by: 1) Verify Secret exists: `kubectl get secret <name>`, 2) Check type is `kubernetes.io/dockerconfigjson`, 3) Ensure Secret is in same namespace as Pod, 4) Verify `imagePullSecrets` references correct Secret name, 5) Check credentials are valid for the registry.

**Source:** [Pull an Image from a Private Registry | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

</details>

---

### Question 37
[MEDIUM-HARD]

What could cause "secret not found" errors during Pod creation?

A) Network issues only
B) Secret doesn't exist, is in a different namespace, or name is misspelled
C) CPU limits only
D) Memory limits only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Secret not found" errors occur when: 1) Secret doesn't exist in the cluster, 2) Secret is in a different namespace (Secrets are namespace-scoped), 3) Secret name is misspelled in Pod spec. Verify with `kubectl get secret <name> -n <namespace>` and check spelling carefully.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 38
[MEDIUM-HARD]

How do you verify the contents of a mounted ConfigMap?

A) kubectl describe configmap only
B) kubectl exec <pod> -- cat /path/to/mounted/file
C) kubectl logs only
D) kubectl get configmap only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verify mounted ConfigMap contents by execing into the Pod: `kubectl exec <pod> -- cat /path/to/mounted/file`. This shows the actual data available to the application. Compare with `kubectl get configmap <name> -o yaml` to ensure data matches expectations.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 39
[MEDIUM-HARD]

What happens when a ConfigMap used as a volume is deleted?

A) The Pod continues with cached data
B) The mounted files disappear, potentially causing application errors
C) The Pod is automatically deleted
D) A new ConfigMap is created

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a ConfigMap is deleted, volume-mounted files become unavailable. The mounted directory may become empty or inaccessible. Applications reading from the mount path will encounter errors. The Pod itself continues running but may fail if it depends on the ConfigMap data.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 40
[MEDIUM-HARD]

How do you troubleshoot subPath mount issues with ConfigMaps?

A) Delete the ConfigMap
B) Verify subPath matches a key in the ConfigMap and check mount path is correct
C) Increase volume size
D) Change storage class

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For subPath issues: 1) Verify `subPath` value exactly matches a key in the ConfigMap, 2) Ensure `mountPath` is the full file path (not directory), 3) Note: subPath mounts don't receive automatic updates when ConfigMap changes. Check Pod events for mount errors.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/#using-configmaps-as-files-from-a-pod)

</details>

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

A) All Pods are deleted
B) Pods can be created without resource restrictions
C) The namespace is deleted
D) No Pods can be created

---

### Question 52
[HARD]

How do you check current resource usage against quotas?

A) kubectl get pods only
B) kubectl describe resourcequota <name> shows Used vs Hard limits
C) kubectl top namespace
D) kubectl quota status

---

### Question 53
[HARD]

What causes "exceeded quota" errors during Pod creation?

A) Network issues
B) Creating resources would exceed the namespace's ResourceQuota limits
C) DNS failures
D) API server issues

---

### Question 54
[HARD]

How do you troubleshoot LimitRange violations?

A) Delete the LimitRange
B) Check LimitRange settings and ensure Pod requests/limits comply with min/max constraints
C) Increase node resources
D) Change namespace

---

### Question 55
[HARD]

What is the impact of deleting a namespace on its resources?

A) Resources are orphaned
B) All resources within the namespace are deleted
C) Resources are moved to default namespace
D) Only Pods are deleted

---

### Question 56
[HARD]

How do you identify pods consuming the most resources in a namespace?

A) kubectl get pods only
B) kubectl top pods -n <namespace> --sort-by=cpu or memory
C) kubectl describe namespace
D) kubectl logs namespace

---

### Question 57
[HARD]

What happens when a namespace is stuck in Terminating state?

A) It will eventually delete
B) Finalizers on resources are blocking deletion; identify and remove them
C) Restart the API server
D) Delete the cluster

---

### Question 58
[HARD]

How do you troubleshoot cross-namespace communication issues?

A) Only check DNS
B) Check NetworkPolicies, Service FQDN usage, and DNS resolution across namespaces
C) Delete namespaces
D) Restart all Pods

---

### Question 59
[HARD]

What causes namespace isolation to fail?

A) Too many namespaces
B) No NetworkPolicies applied, or NetworkPolicies misconfigured
C) DNS issues only
D) Resource quota issues

---

### Question 60
[HARD]

How do you verify ResourceQuota is correctly applied?

A) kubectl get pods
B) kubectl describe resourcequota and attempt to create resources exceeding limits
C) kubectl validate quota
D) kubectl test quota

---

## Cluster Component Diagnostics

### Question 61
[HARD]

How do you diagnose slow API server responses?

A) Restart the API server only
B) Check API server metrics, audit logs, etcd latency, and request queuing
C) Delete Pods only
D) Increase node count

---

### Question 62
[HARD]

What metrics indicate control plane health issues?

A) Pod count only
B) API server request latency, etcd disk sync duration, scheduler queue depth, and controller work queue
C) Node memory only
D) Network throughput only

---

### Question 63
[HARD]

How do you troubleshoot leader election failures?

A) Delete the leader
B) Check component logs, verify connectivity between replicas, and check for network issues
C) Restart all components
D) Delete the cluster

---

### Question 64
[HARD]

What causes watch connection drops from the API server?

A) Too many Pods
B) Network issues, API server restarts, resource pressure, or client-side timeouts
C) DNS failures only
D) Storage issues only

---

### Question 65
[HARD]

How do you check for etcd cluster health?

A) kubectl get etcd
B) etcdctl endpoint health, member list, and check etcd metrics
C) kubectl describe etcd
D) kubectl logs etcd

---

### Question 66
[HARD]

What indicates etcd disk I/O problems?

A) High CPU usage
B) High disk sync duration metrics, slow writes, and backend commit latency
C) Network errors only
D) Memory pressure only

---

### Question 67
[HARD]

How do you troubleshoot admission webhook failures?

A) Delete all webhooks
B) Check webhook pod health, network connectivity, timeout settings, and webhook logs
C) Restart the API server only
D) Delete namespaces

---

### Question 68
[HARD]

What causes "unable to retrieve container logs" errors?

A) Pod is running normally
B) Container not running, kubelet issues, or container runtime problems
C) DNS failures only
D) Network policies only

---

### Question 69
[HARD]

How do you diagnose controller reconciliation issues?

A) Delete the controller
B) Check controller-manager logs, look for reconciliation errors, and verify RBAC permissions
C) Restart all Pods
D) Delete the namespace

---

### Question 70
[HARD]

What should you check when Custom Resources are not being processed?

A) Delete the CRD
B) Verify operator/controller is running, check its logs, and verify CRD is installed correctly
C) Restart the API server
D) Delete all Custom Resources

---

## Multi-Container Pod Issues

### Question 71
[HARD]

How do you troubleshoot sidecar container failures?

A) Delete the Pod
B) Check sidecar logs with -c flag, verify resource allocation, and check dependencies
C) Remove the sidecar
D) Restart the node

---

### Question 72
[HARD]

What causes init container ordering issues?

A) Random scheduling
B) Init containers run sequentially; a failure blocks subsequent containers
C) Network issues only
D) Memory issues only

---

### Question 73
[HARD]

How do you identify which container is causing Pod restarts?

A) kubectl logs only
B) kubectl describe pod and check restartCount per container in containerStatuses
C) kubectl top pod
D) kubectl get events only

---

### Question 74
[HARD]

What happens when containers share a volume incorrectly?

A) The Pod fails immediately
B) File conflicts, permission issues, or data corruption may occur
C) The volume is automatically resized
D) Containers are isolated automatically

---

### Question 75
[HARD]

How do you troubleshoot inter-container communication within a Pod?

A) Check DNS only
B) Containers share localhost; verify port bindings, check logs, and test with netstat/ss
C) Check network policies
D) Restart the Pod

---

### Question 76
[HARD]

What causes one container to affect another in the same Pod?

A) Network isolation
B) Shared resources (CPU, memory, network, volumes) within the Pod
C) Separate namespaces
D) Different nodes

---

### Question 77
[HARD]

How do you check resource consumption per container in a multi-container Pod?

A) kubectl describe pod only
B) kubectl top pod <name> --containers
C) kubectl logs --all-containers
D) kubectl get pod -o wide

---

### Question 78
[HARD]

What indicates a lifecycle hook failure?

A) Pod runs normally
B) FailedPostStartHook or FailedPreStopHook events in Pod description
C) Container restarts only
D) Network errors only

---

### Question 79
[HARD]

How do you troubleshoot postStart hook issues?

A) Remove the hook
B) Check events for hook failures, verify command/HTTP endpoint, and check container logs
C) Restart the node
D) Delete the namespace

---

### Question 80
[HARD]

What happens when a preStop hook times out?

A) The hook runs indefinitely
B) The container is forcefully terminated after terminationGracePeriodSeconds
C) The Pod remains running
D) The node is drained

---

## Security and Access Troubleshooting

### Question 81
[HARD]

How do you troubleshoot ServiceAccount permission issues?

A) Delete the ServiceAccount
B) Use kubectl auth can-i --as=system:serviceaccount:<ns>:<sa-name>, check RBAC bindings
C) Restart the API server
D) Change namespaces

---

### Question 82
[HARD]

What causes "Forbidden" errors when accessing the API?

A) Network issues
B) RBAC denying the request due to missing permissions
C) DNS failures
D) Certificate issues only

---

### Question 83
[HARD]

How do you verify Pod security context is applied correctly?

A) kubectl describe only
B) kubectl exec into Pod and check id, cat /proc/1/status for capabilities
C) kubectl logs only
D) kubectl get pod -o wide

---

### Question 84
[HARD]

What indicates SecurityContext conflicts?

A) Network errors
B) Pod fails to start with security-related error in events
C) DNS failures
D) Storage issues

---

### Question 85
[HARD]

How do you troubleshoot PodSecurityPolicy violations?

A) Delete all policies
B) Check PSP annotations, verify ServiceAccount can use the PSP, and review Pod events
C) Restart kubelet
D) Delete the namespace

---

### Question 86
[HARD]

What causes service account token mount failures?

A) Network issues
B) ServiceAccount doesn't exist, automountServiceAccountToken issues, or token controller problems
C) DNS failures
D) Storage issues

---

### Question 87
[HARD]

How do you check if a Pod has the required capabilities?

A) kubectl describe pod only
B) kubectl exec and check /proc/1/status or use capsh --print
C) kubectl logs only
D) kubectl get pod

---

### Question 88
[HARD]

What indicates a seccomp profile is blocking syscalls?

A) Network errors
B) Container crashes with SIGSYS or operation not permitted errors
C) DNS failures
D) Storage errors

---

### Question 89
[HARD]

How do you troubleshoot AppArmor profile issues?

A) Disable AppArmor
B) Check dmesg for denied operations, verify profile is loaded, and check Pod annotations
C) Restart the node
D) Delete the Pod

---

### Question 90
[HARD]

What causes "operation not permitted" errors in containers?

A) Network issues
B) Missing capabilities, seccomp/AppArmor restrictions, or read-only filesystem
C) DNS failures
D) Storage quota exceeded

---

## Advanced Diagnostics

### Question 91
[HARD]

How do you use audit logs to troubleshoot issues?

A) kubectl logs audit
B) Review API server audit logs to see all API requests, including who made them and the response
C) kubectl get audit
D) kubectl describe audit

---

### Question 92
[HARD]

What information do Kubernetes events provide for troubleshooting?

A) Only Pod creation times
B) State changes, warnings, errors, and reasons for resource status changes
C) Only network information
D) Only storage information

---

### Question 93
[HARD]

How do you correlate metrics with cluster issues?

A) Ignore metrics
B) Compare metric timestamps with events, look for anomalies during incident timeframes
C) Delete metrics
D) Restart Prometheus

---

### Question 94
[HARD]

What is the role of the conditions field in resource troubleshooting?

A) It shows only the resource name
B) It provides detailed status information about the resource's current state and any issues
C) It is only for internal use
D) It shows only timestamps

---

### Question 95
[HARD]

How do you troubleshoot webhook timeout issues?

A) Delete the webhook
B) Check webhook pod health, network latency, increase timeout settings, and review webhook logs
C) Restart the API server
D) Delete all resources

---

### Question 96
[HARD]

What causes garbage collection to fail?

A) Too many Pods
B) Finalizers blocking deletion, owner references issues, or controller-manager problems
C) Network issues only
D) DNS failures only

---

### Question 97
[HARD]

How do you diagnose finalizer-related stuck resources?

A) Delete the cluster
B) kubectl get <resource> -o yaml to check finalizers, identify the controller, or manually remove
C) Restart the API server
D) Delete the namespace

---

### Question 98
[HARD]

What indicates a controller is not watching resources correctly?

A) High CPU usage only
B) Resources not being reconciled, stale status, or missing events in controller logs
C) Network errors only
D) Storage issues only

---

### Question 99
[HARD]

How do you troubleshoot CRD validation errors?

A) Delete the CRD
B) Check the error message, verify spec against CRD schema, and use dry-run for testing
C) Restart the API server
D) Delete all Custom Resources

---

### Question 100
[HARD]

What is the systematic approach to diagnosing unknown cluster issues?

A) Restart everything immediately
B) Check component health, review events and logs, examine metrics, and narrow down systematically
C) Delete and recreate the cluster
D) Ignore the issues

---
