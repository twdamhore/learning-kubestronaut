# Kubernetes Core Concepts - Q91-Q100 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q91-Q100

---

### Question 91
[HARD]

A production Kubernetes cluster's kube-scheduler process crashes and cannot be restarted immediately. While the team works on restoring the scheduler, they observe that existing Pods on worker nodes continue running without interruption. However, a developer creates a new Deployment with 3 replicas during this outage. What happens to the newly created Pods?

A) The Pods are created and automatically assigned to nodes by the kubelet using a fallback scheduling algorithm
B) The Pods remain in a Pending state with no node assignment until the scheduler is restored
C) The API server rejects the Deployment creation because the scheduler health check fails
D) The Pods are evenly distributed across nodes by the kube-controller-manager, which assumes scheduling duties

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When the kube-scheduler is down, the rest of the control plane continues to function. The API server accepts the Deployment creation, and the Deployment controller (inside kube-controller-manager) creates the corresponding ReplicaSet and Pod objects in etcd. However, since no scheduler is running to watch for unassigned Pods and bind them to nodes, the Pods remain in a Pending state with an empty `spec.nodeName`. Existing Pods are unaffected because they are already bound to nodes and managed by their respective kubelets. No other component assumes the scheduler's role automatically.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/

</details>

---

### Question 92
[HARD]

An organization is designing a highly available etcd cluster for their Kubernetes control plane. An architect proposes using 4 etcd nodes to maximize redundancy. A senior engineer argues that 3 or 5 nodes would be a better choice. Why is an odd number of etcd nodes recommended over an even number?

A) Odd-numbered clusters use less memory per node because the Raft log is partitioned across fewer replicas
B) An even-numbered cluster cannot elect a leader because Raft requires an odd quorum, so the cluster fails to start
C) A 4-node cluster tolerates only 1 node failure (same as 3 nodes) because quorum requires a strict majority, so the extra node adds cost without improving fault tolerance
D) Even-numbered clusters split the Raft log across nodes differently, causing data corruption during leader election

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** etcd uses the Raft consensus algorithm, which requires a strict majority (quorum) of nodes to agree on any write operation. For a 3-node cluster, quorum is 2, tolerating 1 failure. For a 4-node cluster, quorum is 3, still tolerating only 1 failure. A 5-node cluster has quorum of 3 and tolerates 2 failures. Therefore, going from 3 to 4 nodes adds infrastructure cost and network overhead without improving fault tolerance. The jump from 3 to 5 is where the next tolerance improvement occurs. Even-numbered clusters can still elect leaders and function correctly, but they are suboptimal from a cost-to-resilience ratio.

**Source:** https://etcd.io/docs/v3.5/faq/#why-an-odd-number-of-cluster-members

</details>

---

### Question 93
[HARD]

A team is setting up a highly available Kubernetes cluster with three control plane nodes. Each node runs its own kube-apiserver instance. A load balancer sits in front of all three API servers. A kubelet on a worker node sends a request to create a Pod. How does this HA setup ensure that the Pod object is consistently persisted, even though multiple API server instances are running?

A) The load balancer directs all write requests to a single designated primary API server, while the other two handle only read requests
B) Each API server instance maintains its own independent etcd database, and they synchronize using a custom replication protocol
C) All API server instances are stateless and connect to the same etcd cluster, which handles consistency through Raft consensus
D) The API servers use a distributed lock manager to coordinate writes, ensuring only one server writes to etcd at any given time

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-apiserver is designed to be horizontally scalable and stateless. Multiple instances can run simultaneously, and any instance can handle any request (reads or writes) because none of them store cluster state themselves. All API server instances connect to the same etcd cluster, which is the single source of truth. etcd's Raft consensus protocol ensures that writes are consistent regardless of which API server instance initiates them. There is no primary/secondary distinction among API servers, and no external lock manager is needed because etcd itself provides the consistency guarantees.

**Source:** https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/

</details>

---

### Question 94
[HARD]

A network partition isolates a worker node from the Kubernetes control plane for an extended period. During this time, the kubelet on the isolated node continues to operate. Which of the following actions can the kubelet still perform while completely disconnected from the API server?

A) Schedule new Pods to the node based on pending Pod specs cached locally
B) Restart containers that crash within already-running Pods using the restart policy defined in their PodSpec
C) Pull updated container images for running Pods by contacting the container registry
D) Evict Pods that exceed their resource limits by communicating with the kube-controller-manager

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet caches the PodSpecs of Pods assigned to its node and can operate autonomously for already-running workloads. If a container crashes, the kubelet applies the restart policy (Always, OnFailure, Never) from the cached PodSpec without needing to contact the API server. The kubelet does not perform scheduling (that is the scheduler's role), so it cannot assign new Pods to itself. While the kubelet could technically reach a container registry if network to the registry is available, it does not autonomously decide to pull updated images for running Pods. Eviction decisions based on resource pressure are made locally by the kubelet, but eviction due to node conditions is coordinated by the node lifecycle controller, not the kubelet-to-controller-manager communication path.

**Source:** https://kubernetes.io/docs/concepts/architecture/#kubelet

</details>

---

### Question 95
[HARD]

In early versions of Kubernetes, cloud-specific logic for managing load balancers, routes, and node instances was embedded directly in the kube-controller-manager. Starting with Kubernetes v1.6, the cloud-controller-manager (CCM) was introduced as a separate component. What is the primary architectural reason the cloud controller logic was extracted into its own process?

A) The kube-controller-manager could not handle the additional CPU load required by cloud API calls, so offloading to a separate process improved performance
B) Separating cloud logic allows cloud providers to develop, release, and iterate on their integrations independently of the core Kubernetes release cycle
C) The cloud-controller-manager runs on worker nodes instead of control plane nodes, reducing the blast radius of cloud API failures
D) Running cloud logic in a separate process enables the kube-controller-manager to operate without any network access, improving security

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The primary motivation for extracting cloud-specific controller logic into the cloud-controller-manager was to decouple cloud provider code from the core Kubernetes codebase. When cloud logic was embedded in kube-controller-manager, cloud providers had to submit changes to the main Kubernetes repository and wait for Kubernetes releases to ship their updates. With the CCM, cloud providers can develop, test, and release their integrations on their own schedule as out-of-tree plugins. The CCM still runs on control plane nodes (not worker nodes), and the kube-controller-manager still requires network access to communicate with the API server.

**Source:** https://kubernetes.io/docs/concepts/architecture/cloud-controller/

</details>

---

### Question 96
[HARD]

A worker node in a Kubernetes cluster experiences a kernel panic and stops sending heartbeats to the control plane. The node lifecycle controller detects this condition. Assuming default settings, what sequence of events occurs after the node stops reporting?

A) The node is immediately deleted from the cluster, and all its Pods are terminated and rescheduled to healthy nodes
B) The node is marked as NotReady after the node-monitor-grace-period, then after the pod-eviction-timeout, the controller begins evicting Pods from the node
C) The kubelet on the node detects the kernel panic and gracefully drains all Pods before the control plane takes any action
D) The kube-scheduler immediately stops assigning new Pods to the node, but existing Pods continue running indefinitely without eviction

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The node lifecycle controller (part of kube-controller-manager) monitors node heartbeats. When a node stops sending heartbeats, the controller waits for the node-monitor-grace-period (default 40 seconds) before marking the node condition as Unknown/NotReady. After this, the controller waits for the pod-eviction-timeout (default 5 minutes) before it begins adding eviction taints or evicting Pods from the unresponsive node. The node is not deleted from the cluster; it remains as an object with NotReady status. Since the kernel panicked, the kubelet is not running and cannot perform any graceful drain. The scheduler does stop assigning new Pods to NotReady nodes, but existing Pods are eventually evicted, not left indefinitely.

**Source:** https://kubernetes.io/docs/concepts/architecture/nodes/#node-controller

</details>

---

### Question 97
[HARD]

Kubernetes originally used full Node status updates as heartbeats, where the kubelet would periodically report the entire Node status object to the API server. In Kubernetes v1.17, Lease objects in the `kube-node-lease` namespace became the default heartbeat mechanism. What is the primary reason Lease-based heartbeats were introduced to replace Node status updates?

A) Lease objects contain more detailed health information than Node status, allowing the control plane to make better scheduling decisions
B) Lease objects are significantly smaller than Node status objects, reducing the etcd write load and API server resource consumption at scale
C) Lease objects are stored in a separate etcd cluster dedicated to heartbeats, preventing heartbeat traffic from affecting cluster state storage
D) Lease objects use UDP instead of TCP to communicate heartbeats, reducing network latency for large clusters

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Node status objects can be quite large, containing conditions, addresses, capacity, allocatable resources, and other metadata. When every kubelet in a large cluster updates the full Node status object every 10 seconds, it generates substantial write load on both the API server and etcd. Lease objects are tiny (only a few fields including the holder identity and renewal time), so updating them places far less pressure on etcd and the API server. Lease objects are stored in the same etcd cluster as all other Kubernetes objects, not in a separate one. They still use standard HTTPS communication to the API server, not UDP. Node status updates still happen, but at a much lower frequency (default 5 minutes or on change), while Leases handle the frequent heartbeat signal.

**Source:** https://kubernetes.io/docs/concepts/architecture/nodes/#heartbeats

</details>

---

### Question 98
[HARD]

A cluster administrator is configuring a monitoring system to check the health of the kube-apiserver. They discover three different health check endpoints: `/healthz`, `/readyz`, and `/livez`. The administrator wants to configure a load balancer to remove an API server instance from rotation only when it cannot serve traffic, but not during its startup phase when it is still loading data. Which endpoint should the load balancer use, and why?

A) `/healthz` - because it provides a comprehensive check that includes both liveness and readiness, suitable for load balancer decisions
B) `/livez` - because it indicates the process is alive and should be restarted if it fails, which is equivalent to being ready for traffic
C) `/readyz` - because it returns success only when the API server has completed initialization and is ready to serve requests, unlike `/livez` which only checks if the process should be restarted
D) `/livez` and `/readyz` combined - the load balancer must check both endpoints and only route traffic when both return success

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `/readyz` endpoint indicates that the API server has completed its initialization (such as loading informer caches) and is ready to accept and properly serve requests. The `/livez` endpoint indicates that the process is running and has not entered an unrecoverable state; it is analogous to a container liveness probe and is used to determine if the process needs to be restarted, not whether it can handle traffic. The `/healthz` endpoint is a legacy endpoint that combines aspects of both and is deprecated in favor of the split endpoints. For load balancer routing decisions, `/readyz` is the correct choice because it distinguishes between a healthy-but-not-yet-ready server (during startup) and a fully ready server.

**Source:** https://kubernetes.io/docs/reference/using-api/health-checks/

</details>

---

### Question 99
[HARD]

A junior administrator runs `kubeadm init` to bootstrap a new Kubernetes cluster on the first control plane node. The process completes successfully and outputs a `kubeadm join` command. Which of the following best describes the sequence of critical steps that `kubeadm init` performs during the bootstrap process?

A) Installs the container runtime, then deploys etcd as a container, generates certificates, starts the API server, and installs CoreDNS and kube-proxy
B) Generates PKI certificates and kubeconfig files, starts the kubelet, deploys control plane components (etcd, API server, controller manager, scheduler) as static Pods, then installs CoreDNS and kube-proxy as add-ons
C) Downloads Kubernetes binaries, configures the kernel parameters, starts all control plane components as systemd services, then joins the node to itself as both control plane and worker
D) Creates the cluster namespace in etcd, generates a single shared certificate for all components, starts the API server as a systemd service, and then launches the scheduler and controller manager as Pods managed by a Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubeadm init` process follows a well-defined sequence: it first runs preflight checks, then generates the PKI certificates (CA, API server, front proxy, etcd, and SA key pair) and kubeconfig files for the admin, controller manager, and scheduler. It then starts the kubelet (which is already installed as a systemd service) and writes static Pod manifests for etcd, kube-apiserver, kube-controller-manager, and kube-scheduler to `/etc/kubernetes/manifests/`. The kubelet watches this directory and launches these components as static Pods. Finally, kubeadm installs CoreDNS and kube-proxy as cluster add-ons. kubeadm does not install the container runtime or the kubelet binary itself; these are prerequisites.

**Source:** https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/

</details>

---

### Question 100
[HARD]

A team manages a Kubernetes cluster running version 1.29. They are planning a component-by-component upgrade. According to the Kubernetes version skew policy, the kube-apiserver must be upgraded first. After upgrading the kube-apiserver to version 1.30, which of the following configurations is supported by the version skew policy?

A) kubelet at v1.28, kube-controller-manager at v1.29, kube-scheduler at v1.29
B) kubelet at v1.27, kube-controller-manager at v1.30, kube-scheduler at v1.30
C) kubelet at v1.29, kube-controller-manager at v1.28, kube-scheduler at v1.29
D) kubelet at v1.30, kube-controller-manager at v1.29, kube-scheduler at v1.28

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The Kubernetes version skew policy defines strict compatibility rules between components. The kube-controller-manager and kube-scheduler must not be newer than the kube-apiserver and may be up to one minor version older (so v1.29 or v1.30 with a v1.30 API server). The kubelet must not be newer than the kube-apiserver and may be up to three minor versions older (so v1.27 through v1.30 with a v1.30 API server). Option A has kubelet at v1.28 (two versions behind, within the three-version window) and both controller-manager and scheduler at v1.29 (one version behind, within the one-version window). Option B has kubelet at v1.27 (which is valid), but kube-controller-manager at v1.30 is the same version, which is actually valid too, yet the combination in A is also valid. Option C has kube-controller-manager at v1.28 (two versions behind the API server), which exceeds the one-version skew limit. Option D has kube-scheduler at v1.28, also exceeding the one-version limit.

**Source:** https://kubernetes.io/releases/version-skew-policy/

</details>
