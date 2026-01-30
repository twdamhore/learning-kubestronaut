# Kubernetes Core Concepts - Q1-Q10 [Medium]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 1
**Difficulty:** Medium
**Questions:** Q1-Q10

---

### Question 1
[MEDIUM]

A developer needs to run two tightly coupled containers that must share the same network interface and storage volumes. What Kubernetes construct should they use?

A) Deploy each container as a separate Deployment
B) Place both containers in the same Pod
C) Use a Service to link two Pods together
D) Create a ReplicaSet with two container images

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod is the smallest deployable unit in Kubernetes and can contain multiple containers that share the same network namespace (localhost) and storage volumes. This sidecar pattern is the standard approach for tightly coupled containers that need to communicate over localhost or share files. Separate Deployments or Pods would give each container its own network namespace, preventing localhost communication.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/#how-pods-manage-multiple-containers

</details>

---

### Question 2
[MEDIUM]

An operator notices that after restarting the kube-apiserver, the cluster state (Pods, Services, ConfigMaps) is fully preserved. Which component is responsible for persisting this state?

A) kube-controller-manager
B) kubelet
C) etcd
D) kube-scheduler

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** etcd is a consistent, highly-available key-value store that serves as the single source of truth for all cluster data. Every object created through the API server — Pods, Services, ConfigMaps, Secrets, and more — is persisted in etcd. The kube-apiserver is stateless and reads from etcd on startup, which is why the cluster state survives an API server restart. The other components react to state; they do not store it.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#etcd

</details>

---

### Question 3
[MEDIUM]

A team is running multiple projects in a single Kubernetes cluster and needs to prevent resource name collisions between projects while applying per-project resource quotas. Which Kubernetes feature best addresses both requirements?

A) Labels and selectors
B) Namespaces
C) Annotations
D) Node affinity rules

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Namespaces provide both a scope for names (preventing collisions — two Pods named "web" can exist in different Namespaces) and a boundary for applying ResourceQuotas and LimitRanges. Labels can organize objects but do not provide name scoping or quota boundaries. Annotations store metadata but have no impact on resource isolation.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

</details>

---

### Question 4
[MEDIUM]

A Pod is scheduled to a worker node but its containers fail to start. Which component on the worker node is directly responsible for pulling the container image and starting the containers?

A) kube-proxy
B) kube-controller-manager
C) kubelet
D) CoreDNS

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kubelet is the primary node agent that runs on every worker node. After the kube-scheduler assigns a Pod to a node, the kubelet on that node receives the PodSpec via the API server and instructs the container runtime (e.g., containerd) to pull the image and start the containers. kube-proxy handles network rules, not container lifecycle. kube-controller-manager runs on the control plane, not the worker node.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#kubelet

</details>

---

### Question 5
[MEDIUM]

In a Kubernetes cluster, all components (kubelet, kube-scheduler, kube-controller-manager) communicate with one central component to read and write cluster state. Which component is this?

A) etcd
B) kube-apiserver
C) kube-proxy
D) cloud-controller-manager

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-apiserver is the only component that communicates directly with etcd. All other components — kubelet, kube-scheduler, kube-controller-manager — interact with the cluster state exclusively through the API server's RESTful interface. This design centralizes authentication, authorization, and admission control in one place. Components never read from or write to etcd directly.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver

</details>

---

### Question 6
[MEDIUM]

A team deploys a backend application as multiple Pod replicas. They need a stable DNS name and IP address that load-balances traffic across all healthy replicas, even as Pods are replaced. What Kubernetes object provides this?

A) Ingress
B) Endpoint
C) Service
D) ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A Service provides a stable virtual IP (ClusterIP) and DNS name that persists regardless of Pod lifecycle. It uses label selectors to discover backend Pods and distributes traffic across them. When Pods are replaced, the Service automatically updates its Endpoints to reflect the current healthy set. An Ingress operates at L7 and routes external HTTP traffic to Services, but does not itself provide the internal stable endpoint.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/

</details>

---

### Question 7
[MEDIUM]

A new Kubernetes cluster has just been bootstrapped. An administrator runs `kubectl get pods -n kube-system` and sees CoreDNS and kube-proxy running. What does this tell you about the `kube-system` Namespace?

A) It was manually created by the administrator during setup
B) It is an initial Namespace automatically created by Kubernetes for system components
C) It is an alias for the default Namespace
D) It only exists when CoreDNS is installed separately

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kube-system` is one of four initial Namespaces created automatically in every Kubernetes cluster (along with `default`, `kube-public`, and `kube-node-lease`). It hosts objects created by the Kubernetes system itself, such as CoreDNS, kube-proxy, and other cluster add-ons. It is not an alias for `default` — they are separate Namespaces with distinct scopes.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces

</details>

---

### Question 8
[MEDIUM]

A developer wants to update their application from v1 to v2 with zero downtime, and needs the ability to roll back if v2 has issues. Which Kubernetes object provides both rolling updates and rollback capabilities out of the box?

A) ReplicaSet
B) Pod
C) Deployment
D) DaemonSet

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A Deployment manages ReplicaSets and provides declarative rolling update and rollback capabilities. When you update a Deployment's Pod template, it creates a new ReplicaSet and gradually scales it up while scaling down the old one (rolling update). If something goes wrong, `kubectl rollout undo` reverts to the previous ReplicaSet. A bare ReplicaSet does not provide update strategy or rollback history on its own.

**Source:** https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment

</details>

---

### Question 9
[MEDIUM]

A cluster has three worker nodes with varying CPU and memory capacities. When a new Pod with specific resource requests is created, which control plane component evaluates node capacity and constraints to decide where the Pod should run?

A) kube-controller-manager
B) kube-scheduler
C) kubelet
D) etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-scheduler is responsible for watching for newly created Pods with no assigned node and selecting the best node based on resource availability, constraints (taints, tolerations, affinity rules), and scoring criteria. The kube-controller-manager manages controllers like ReplicaSet and Deployment controllers but does not make scheduling decisions. The kubelet executes the scheduling decision on the assigned node.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/

</details>

---

### Question 10
[MEDIUM]

A team uses `app: frontend` and `env: production` Labels on their Pods. A Service is configured with the selector `app: frontend, env: production`. A new Pod is created with only the label `app: frontend`. Will the Service route traffic to this new Pod?

A) Yes, because it matches at least one label in the selector
B) Yes, because label selectors use OR logic by default
C) No, because the selector requires all specified labels to match
D) No, because Services can only match a single label

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Label selectors in Kubernetes use AND logic — all key-value pairs in the selector must match for a resource to be selected. Since the new Pod only has `app: frontend` but lacks `env: production`, it does not satisfy the full selector and the Service will not route traffic to it. This AND behavior applies to equality-based selectors across Services, Deployments, ReplicaSets, and other controllers.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#label-selectors

</details>
