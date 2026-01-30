# Kubernetes Core Concepts - Q1-Q10 [Medium]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 1
**Difficulty:** Medium
**Questions:** Q1-Q10

---

### Question 1
[MEDIUM]

What is the smallest deployable unit in Kubernetes?

A) Container
B) Pod
C) Node
D) Deployment

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod is the smallest deployable unit in Kubernetes. A Pod represents a single instance of a running process and can contain one or more containers that share the same network namespace and storage volumes. While containers run inside Pods, Kubernetes schedules and manages workloads at the Pod level, not the container level.

**Source:** https://kubernetes.io/docs/concepts/workloads/pods/

</details>

---

### Question 2
[MEDIUM]

Which control plane component serves as the front-end for the Kubernetes API?

A) etcd
B) kube-scheduler
C) kube-apiserver
D) kube-controller-manager

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-apiserver is the front-end for the Kubernetes control plane. It exposes the Kubernetes API and is the central management entity that receives all REST requests for modifications to Pods, Services, ReplicaSets, and other resources. All communication between components goes through the API server.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#kube-apiserver

</details>

---

### Question 3
[MEDIUM]

What is the purpose of a Kubernetes Namespace?

A) To provide persistent storage for Pods
B) To divide cluster resources between multiple users or teams
C) To define network routing rules between Pods
D) To schedule Pods on specific nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Namespaces provide a mechanism for isolating groups of resources within a single cluster. They are intended for use in environments with many users spread across multiple teams or projects. Namespaces provide a scope for names, and resource quotas can be applied per namespace to divide cluster resources.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

</details>

---

### Question 4
[MEDIUM]

Which component runs on every worker node and ensures that containers are running in a Pod?

A) kube-proxy
B) kube-scheduler
C) kubelet
D) kube-controller-manager

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kubelet is an agent that runs on each worker node in the cluster. It watches for PodSpecs assigned to its node and ensures the containers described in those PodSpecs are running and healthy. The kubelet communicates with the API server and manages the lifecycle of containers on its node.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#kubelet

</details>

---

### Question 5
[MEDIUM]

What does etcd store in a Kubernetes cluster?

A) Container images
B) Pod logs
C) All cluster data and state
D) Node metrics

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** etcd is a consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data. It stores the entire state of the cluster including configuration data, the state of each node and Pod, Secrets, ConfigMaps, and all other API objects. It is the single source of truth for the cluster.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#etcd

</details>

---

### Question 6
[MEDIUM]

What is the role of a Kubernetes Service?

A) To build container images
B) To expose an application running on a set of Pods as a network service
C) To schedule Pods across nodes
D) To store configuration data

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Kubernetes Service is an abstraction that defines a logical set of Pods and a policy by which to access them. Services enable loose coupling between dependent Pods. Since Pods are ephemeral and can be replaced at any time, a Service provides a stable endpoint (IP address and DNS name) to reach the Pods that match its selector.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/

</details>

---

### Question 7
[MEDIUM]

Which of the following is a default Namespace in a new Kubernetes cluster?

A) kube-admin
B) kube-system
C) kube-core
D) kube-master

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A new Kubernetes cluster comes with four initial Namespaces: `default` (for objects with no other namespace), `kube-system` (for objects created by the Kubernetes system), `kube-public` (readable by all users, reserved for cluster usage), and `kube-node-lease` (for node heartbeat data). `kube-system` contains core components like CoreDNS and the kube-proxy DaemonSet.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces

</details>

---

### Question 8
[MEDIUM]

What is the primary function of a Deployment in Kubernetes?

A) To manage storage volumes
B) To provide declarative updates for Pods and ReplicaSets
C) To configure network policies
D) To manage cluster-level permissions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Deployment provides declarative updates for Pods and ReplicaSets. You describe a desired state in a Deployment, and the Deployment controller changes the actual state to the desired state at a controlled rate. Deployments manage the creation, scaling, and updating of ReplicaSets and the Pods they own, enabling features like rolling updates and rollbacks.

**Source:** https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

</details>

---

### Question 9
[MEDIUM]

Which component is responsible for assigning newly created Pods to nodes?

A) kubelet
B) kube-proxy
C) kube-scheduler
D) etcd

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-scheduler watches for newly created Pods that have no node assigned and selects a node for them to run on. Scheduling decisions take into account resource requirements, hardware/software constraints, affinity and anti-affinity specifications, data locality, and other factors. Once a decision is made, the scheduler updates the Pod's spec with the node assignment via the API server.

**Source:** https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler

</details>

---

### Question 10
[MEDIUM]

What are Labels in Kubernetes primarily used for?

A) To store sensitive configuration data
B) To organize and select subsets of objects
C) To define resource limits for containers
D) To specify container image versions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Labels are key/value pairs attached to Kubernetes objects such as Pods. They are used to organize and select subsets of objects. Labels allow efficient queries and watches and are used by Services, Deployments, and other controllers to identify and group the Pods they manage. Unlike annotations, labels are intended to be used with selectors to identify meaningful groupings.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/

</details>
