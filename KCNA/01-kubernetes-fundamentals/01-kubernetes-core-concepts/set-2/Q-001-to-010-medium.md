# Kubernetes Core Concepts - Q1-Q10 [Medium]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Medium
**Questions:** Q1-Q10

---

### Question 1
[MEDIUM]

A cluster runs a ReplicaSet with `replicas: 3` across a three-node cluster. One worker node suddenly fails, taking one Pod down with it. After the node failure is detected, what happens to restore the desired Pod count?

A) The kubelet on the failed node automatically restarts the Pod once the node recovers
B) The ReplicaSet controller detects the shortfall and creates a new Pod, which the scheduler places on a healthy node
C) The kube-proxy reroutes traffic to the remaining two Pods but no new Pod is created
D) The kube-scheduler directly creates a replacement Pod on another node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ReplicaSet controller continuously watches the actual number of running Pods against the desired count. When a node fails and a Pod becomes unavailable, the controller detects the discrepancy and creates a new Pod object via the API server. The kube-scheduler then assigns this new Pod to a healthy node with sufficient resources. The scheduler does not create Pods itself — it only assigns unscheduled Pods to nodes. kube-proxy handles networking rules, not Pod lifecycle.

**Source:** https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/#how-a-replicaset-works

</details>

---

### Question 2
[MEDIUM]

A team maintains a web application whose container image is the same across staging and production, but the database connection string differs between environments. They want to avoid rebuilding the image for each environment. Which Kubernetes object allows them to inject environment-specific configuration into their Pods without modifying the container image?

A) Secret
B) PersistentVolume
C) ConfigMap
D) Annotation

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A ConfigMap is designed to decouple environment-specific configuration from container images, allowing the same image to be used across multiple environments. ConfigMaps can be consumed as environment variables or mounted as files inside a Pod. While a Secret could technically hold any data, it is intended for sensitive information, not general configuration like a database hostname. Annotations store metadata on objects and cannot be injected into containers. PersistentVolumes provide storage, not configuration data.

**Source:** https://kubernetes.io/docs/concepts/configuration/configmap/

</details>

---

### Question 3
[MEDIUM]

A developer stores a database password in a ConfigMap and mounts it into a Pod. A security review flags this as a risk. Why would using a Secret be more appropriate than a ConfigMap for this data?

A) Secrets encrypt data at rest by default in all Kubernetes clusters without any additional configuration
B) Secrets are stored in base64 encoding, transmitted with less exposure, and can be integrated with encryption-at-rest and RBAC policies designed specifically for sensitive data
C) Secrets are stored on disk in the Pod's filesystem while ConfigMaps are only held in memory
D) Secrets automatically rotate credentials on a schedule, preventing stale passwords

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Secrets are the Kubernetes-native construct for handling sensitive data such as passwords, tokens, and keys. They are base64-encoded (not encrypted by default), but Kubernetes provides mechanisms like encryption at rest for Secrets, and RBAC can restrict Secret access more tightly than ConfigMaps. This separation of concerns signals to the platform and operators that the data requires careful handling. Secrets are not automatically encrypted in all clusters without configuration, and they do not auto-rotate credentials. In fact, Secrets are typically held in tmpfs (memory) on nodes, not written to disk, which is the opposite of option C.

**Source:** https://kubernetes.io/docs/concepts/configuration/secret/

</details>

---

### Question 4
[MEDIUM]

An operator notices that the containerd process on a worker node has crashed and is not restarting. Existing containers on the node continue running briefly, but when the kubelet tries to start a newly scheduled Pod on that node, it fails. What is the most accurate explanation?

A) The kubelet itself crashes whenever the container runtime is unavailable
B) The kubelet cannot instruct the container runtime to pull images or start containers, so new Pods cannot be launched on that node
C) The kube-scheduler automatically removes the node from the cluster when containerd stops
D) All running containers immediately terminate the moment containerd stops

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet depends on the container runtime (such as containerd) via the Container Runtime Interface (CRI) to pull images, create containers, and manage their lifecycle. When containerd is down, the kubelet cannot fulfill these operations, so newly scheduled Pods fail to start. Existing containers may continue running briefly since they are already OS-level processes, but the kubelet loses the ability to manage them. The kubelet itself does not crash just because the runtime is unavailable, and the scheduler does not automatically remove nodes — the node's status transitions to NotReady over time.

**Source:** https://kubernetes.io/docs/concepts/architecture/#container-runtime

</details>

---

### Question 5
[MEDIUM]

A developer runs `kubectl get pods` and sees a Pod in the `Pending` phase. The Pod was created 10 minutes ago and has resource requests of 8 CPU cores. The cluster's nodes each have only 4 available cores. What is the most likely reason the Pod remains in `Pending`?

A) The container image does not exist in the registry
B) The kube-scheduler cannot find a node with sufficient resources to satisfy the Pod's resource requests
C) The Pod has entered the `Failed` phase and is being reported incorrectly
D) The kubelet on the assigned node is still pulling the container image

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod enters the `Pending` phase when it has been accepted by the cluster but is not yet running. One common reason is that the kube-scheduler cannot find a node that satisfies the Pod's resource requests — in this case, 8 CPU cores when no node has more than 4 available. The Pod stays `Pending` until sufficient resources become available. If the image did not exist, the Pod would first be scheduled to a node and then show `ErrImagePull` or `ImagePullBackOff` in a `Waiting` container state, not remain `Pending`. A Pod in `Pending` has not yet been assigned to a node, so the kubelet is not involved yet.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-phase

</details>

---

### Question 6
[MEDIUM]

A team member uses `kubectl create deployment nginx --image=nginx` to deploy an application, then later modifies the local YAML file and runs `kubectl apply -f deployment.yaml`. Another team member argues they should have used `kubectl apply` from the start. What is the key advantage of the declarative (`apply`) approach over the imperative (`create`) approach?

A) `kubectl apply` is faster because it skips validation against the API server
B) `kubectl apply` tracks the desired state in the manifest and merges changes, allowing repeatable updates without errors if the resource already exists
C) `kubectl create` cannot set resource limits, while `kubectl apply` can
D) `kubectl apply` automatically creates Namespaces, while `kubectl create` does not

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The declarative approach using `kubectl apply` works by comparing the desired state in the manifest with the current live state and merging differences. This makes it idempotent — running it multiple times with the same manifest produces the same result without "already exists" errors. In contrast, `kubectl create` is imperative and fails if the resource already exists. Both commands can set resource limits and neither auto-creates Namespaces. The declarative model is preferred for production workflows, version control, and GitOps pipelines.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/object-management/#declarative-object-configuration

</details>

---

### Question 7
[MEDIUM]

A platform team needs to attach a JSON blob of build metadata (commit SHA, CI pipeline URL, build timestamp) to a Deployment for tooling integration. This metadata is not used for selecting or grouping objects. Should they use Labels or Annotations, and why?

A) Labels, because all metadata in Kubernetes must be stored as Labels
B) Annotations, because they are designed for non-identifying metadata that tools and libraries can retrieve, without the constraints imposed on Label values
C) Labels, because Annotations cannot be read by external tools
D) Neither — this metadata should be stored in a ConfigMap referenced by the Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Annotations are intended for attaching arbitrary non-identifying metadata to objects — data that is not used to select or group resources. Unlike Labels, Annotations can hold large values, structured data, and characters that are not permitted in Label values (which are limited to 63 characters and specific character sets). Since build metadata like commit SHAs and pipeline URLs are informational and not used for selectors or scheduling, Annotations are the correct choice. Labels should be reserved for identifying attributes used in queries and selectors.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/

</details>

---

### Question 8
[MEDIUM]

The kube-controller-manager on a cluster's control plane stops running due to a crash. The kube-apiserver and etcd remain healthy. A Deployment currently has 3 replicas running. If one of those Pods is manually deleted, what happens?

A) The Pod is immediately recreated because the kubelet on the node handles replica recovery
B) The kube-scheduler detects the missing Pod and creates a replacement
C) The Pod is not replaced because the controller responsible for maintaining the desired replica count is unavailable
D) etcd automatically restores the deleted Pod from its stored state

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-controller-manager runs the core control loops, including the ReplicaSet controller that ensures the actual Pod count matches the desired replica count. When the kube-controller-manager is down, no controller is watching for discrepancies, so a deleted Pod will not be replaced. The kube-scheduler only assigns Pods to nodes — it does not create them. The kubelet runs Pods on its node but does not manage replica counts. etcd stores state but does not act on it. Once the kube-controller-manager restarts, it will detect the shortfall and create a replacement Pod.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager

</details>

---

### Question 9
[MEDIUM]

A cluster administrator notices that after creating a new ClusterIP Service, Pods on every node can immediately reach the Service's virtual IP. No external load balancer is involved. Which component running on each node is responsible for making this Service IP reachable?

A) kubelet, which updates each Pod's /etc/hosts file with the Service IP
B) CoreDNS, which resolves the Service name and routes the traffic
C) kube-proxy, which programs iptables or IPVS rules on each node to intercept traffic destined for the Service IP and forward it to backend Pod IPs
D) The container runtime, which configures network namespaces to include Service routing

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** kube-proxy runs on every node and watches the API server for Service and Endpoints changes. When a new Service is created, kube-proxy programs the node's network stack (using iptables, IPVS, or nftables rules) so that any traffic destined for the Service's ClusterIP is intercepted and forwarded to one of the backend Pod IPs. CoreDNS resolves Service names to ClusterIPs but does not handle the actual packet routing. The kubelet manages Pod lifecycle and does not configure Service networking. The container runtime handles container processes, not cluster-wide Service routing.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ip-addressing-mechanism

</details>

---

### Question 10
[MEDIUM]

A developer deploys a frontend Pod and a backend Service named `api` in the `production` Namespace. The frontend Pod needs to make HTTP requests to the backend. Instead of hardcoding an IP address, the developer uses `http://api.production.svc.cluster.local`. Which cluster component resolves this DNS name to the backend Service's ClusterIP?

A) kube-proxy, which maintains a DNS lookup table on each node
B) The kubelet, which injects DNS entries into each Pod at startup
C) CoreDNS (cluster DNS), which runs as a Service in the cluster and resolves Service names to their ClusterIPs
D) etcd, which stores DNS records alongside cluster state and responds to queries directly

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** CoreDNS is the default cluster DNS provider in Kubernetes. It runs as Pods behind a Service (typically in the `kube-system` Namespace) and watches the API server for Service objects. When a Pod performs a DNS lookup for `api.production.svc.cluster.local`, the request is sent to CoreDNS, which resolves it to the ClusterIP of the `api` Service. The kubelet configures each Pod's `/etc/resolv.conf` to point to the CoreDNS Service IP, but the kubelet itself does not resolve DNS. kube-proxy handles packet-level Service routing, not DNS resolution. etcd stores cluster state but does not serve DNS queries.

**Source:** https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/

</details>
