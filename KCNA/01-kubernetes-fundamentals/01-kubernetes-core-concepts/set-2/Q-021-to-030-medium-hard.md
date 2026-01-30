# Kubernetes Core Concepts - Q21-Q30 [Medium-Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Medium-Hard
**Questions:** Q21-Q30

---

### Question 21
[MEDIUM-HARD]

A production Kubernetes cluster runs three API server instances behind a load balancer for high availability. During a maintenance window, one of the three API server instances crashes unexpectedly. What is the immediate impact on the cluster?

A) The cluster becomes completely unavailable until the crashed API server is restored
B) The remaining two API servers continue serving requests, and clients are routed to healthy instances by the load balancer
C) etcd automatically promotes a new API server instance to replace the crashed one
D) The kube-scheduler and kube-controller-manager stop functioning until all three API servers are online

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In a highly available control plane, multiple kube-apiserver instances run simultaneously behind a load balancer. Each API server instance is stateless and connects to the same etcd cluster, so any instance can serve any request. When one instance crashes, the load balancer detects the failure and routes traffic to the remaining healthy instances with no cluster downtime. etcd does not manage API server instances, and the scheduler and controller-manager can continue operating through any available API server.

**Source:** https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/ha-topology/

</details>

---

### Question 22
[MEDIUM-HARD]

A cluster administrator is planning a disaster recovery strategy. The etcd cluster suffers a catastrophic failure and all data is lost. The administrator has no etcd snapshot. What is the consequence for the Kubernetes cluster?

A) Only running Pods are affected; Services and ConfigMaps are stored in kube-apiserver memory
B) The kubelet recreates all objects from its local cache on each node
C) All cluster state is permanently lost, including Deployments, Services, Secrets, and ConfigMaps, because etcd is the sole persistent store
D) The kube-controller-manager rebuilds the cluster state by querying running containers on each node

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** etcd is the single source of truth for all Kubernetes cluster state. Every API object -- Pods, Deployments, Services, Secrets, ConfigMaps, RBAC rules, and more -- is persisted exclusively in etcd. Without a snapshot backup, a total etcd failure means permanent loss of all cluster configuration and state. While containers may still be running on nodes, the control plane has no record of them and cannot manage them. This is why regular etcd snapshots are a critical part of cluster operations.

**Source:** https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster

</details>

---

### Question 23
[MEDIUM-HARD]

A developer creates a Pod with a container image tagged `internal-registry.company.com/app:latest`. The cluster has an admission controller configured that denies any Pod using images not from `approved-registry.company.com`. At which point in the API request lifecycle does this denial occur?

A) During authentication, before the request reaches the API server logic
B) During scheduling, when the kube-scheduler evaluates the Pod specification
C) After authentication and authorization, but before the object is persisted to etcd
D) After the object is persisted to etcd, when the kubelet attempts to pull the image

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Admission controllers intercept requests to the Kubernetes API server after authentication and authorization have succeeded, but before the object is written to etcd. They can mutate or validate (or reject) requests. In this scenario, a validating admission controller inspects the Pod spec, finds the image does not come from the approved registry, and rejects the request before it is ever persisted. The scheduler and kubelet never see the Pod because it is rejected at the admission stage.

**Source:** https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/

</details>

---

### Question 24
[MEDIUM-HARD]

A ReplicaSet controller observes that its desired replica count is 5 but only 3 Pods currently exist. What does the controller do next, and what pattern does this behavior exemplify?

A) It sends a restart signal to the two missing Pods and exemplifies the event-driven pattern
B) It creates 2 new Pods to match the desired state and exemplifies the reconciliation loop pattern
C) It waits for the kube-scheduler to create the missing Pods and exemplifies the delegation pattern
D) It scales down to 3 replicas to match the current state and exemplifies the self-healing pattern

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes controllers follow the reconciliation loop (also called the control loop) pattern: they continuously observe the current state of the cluster, compare it against the desired state declared in the API object's spec, and take action to converge the two. When the ReplicaSet controller detects a discrepancy (3 actual vs. 5 desired), it creates 2 new Pod objects through the API server to reconcile the difference. The controller never adjusts the desired state downward to match reality -- it always drives current state toward desired state.

**Source:** https://kubernetes.io/docs/concepts/architecture/controller/#controller-pattern

</details>

---

### Question 25
[MEDIUM-HARD]

A developer deletes a Deployment named `web-app` that manages a ReplicaSet, which in turn manages 3 Pods. Shortly after deletion, the developer notices the ReplicaSet and all 3 Pods are also gone. What Kubernetes mechanism caused the cascading deletion?

A) The kube-scheduler detected orphaned Pods and terminated them
B) The kubelet on each node stopped the Pods when it lost contact with the Deployment
C) The garbage collector deleted the ReplicaSet and Pods because they had ownerReferences pointing to the deleted Deployment
D) Kubernetes Services automatically clean up backend Pods when their associated Deployment is removed

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a Deployment creates a ReplicaSet, it sets an ownerReference on the ReplicaSet pointing back to itself. Similarly, the ReplicaSet sets ownerReferences on its Pods. The Kubernetes garbage collector watches for deleted owner objects and cascades the deletion to all dependents whose ownerReferences point to the deleted owner. This is called foreground or background cascading deletion. The scheduler, kubelet, and Services play no role in this cleanup process.

**Source:** https://kubernetes.io/docs/concepts/architecture/garbage-collection/#owners-dependents

</details>

---

### Question 26
[MEDIUM-HARD]

A developer writes a custom controller that needs to manage Deployment objects. When constructing the API request path, they must use the correct API group. Which API group and resource path is correct for Deployments?

A) `/api/v1/deployments` -- Deployments belong to the core (legacy) API group
B) `/apis/apps/v1/deployments` -- Deployments belong to the `apps` API group
C) `/apis/extensions/v1/deployments` -- Deployments belong to the `extensions` API group
D) `/apis/batch/v1/deployments` -- Deployments belong to the `batch` API group

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deployments belong to the `apps` API group at version `v1`, making the correct path `/apis/apps/v1/deployments`. The core API group (accessed via `/api/v1/`) contains fundamental resources like Pods, Services, and ConfigMaps, but not Deployments. While Deployments were historically available under `extensions/v1beta1`, they were moved to `apps/v1` and the extensions path has been deprecated. The `batch` group is for Jobs and CronJobs, not Deployments.

**Source:** https://kubernetes.io/docs/reference/using-api/#api-groups

</details>

---

### Question 27
[MEDIUM-HARD]

An administrator needs to list all Pods running on a specific node named `worker-03`. They also need to list all Pods with the label `team=backend`. Which types of selectors should they use for each query, respectively?

A) A label selector for both queries, since node name is a label
B) A field selector (`spec.nodeName=worker-03`) for the node query, and a label selector (`team=backend`) for the team query
C) An annotation selector for the node query, and a label selector for the team query
D) A field selector for both queries, since field selectors are more efficient than label selectors

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field selectors filter resources based on built-in object fields such as `metadata.name`, `metadata.namespace`, and `spec.nodeName`. To list Pods on a specific node, you use the field selector `spec.nodeName=worker-03`. Label selectors, on the other hand, filter based on user-defined key-value pairs attached to objects. The team designation is a label, so `team=backend` is a label selector. Kubernetes does not have annotation selectors, and field selectors support only a limited set of fields per resource type -- they cannot replace label selectors for arbitrary metadata.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/field-selectors/

</details>

---

### Question 28
[MEDIUM-HARD]

An administrator adds a finalizer named `custom-cleanup/protect` to a PersistentVolumeClaim (PVC). Later, a developer runs `kubectl delete pvc my-data`. The developer notices that the PVC enters a `Terminating` state but is not actually removed. What explains this behavior?

A) The PVC cannot be deleted because it is bound to a PersistentVolume
B) The finalizer prevents the object from being removed from etcd until the finalizer is explicitly removed from the object's metadata
C) The delete command failed silently and needs to be run with `--force`
D) The PVC is stuck because the associated StorageClass has a `reclaimPolicy` of `Retain`

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Finalizers are keys in an object's `metadata.finalizers` list that signal to Kubernetes that pre-deletion cleanup must occur before the object can be fully removed. When a delete request is issued, Kubernetes sets a `deletionTimestamp` on the object (putting it in `Terminating` state) but does not remove it from etcd until all finalizers are cleared. The controller responsible for the finalizer must perform its cleanup logic and then remove the finalizer from the list, after which Kubernetes completes the deletion. The `--force` flag and StorageClass reclaim policy do not override finalizers.

**Source:** https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/

</details>

---

### Question 29
[MEDIUM-HARD]

A developer reports that their Pod keeps restarting but they cannot determine why from `kubectl describe pod` alone. An SRE suggests checking Kubernetes events for the namespace. What information do Kubernetes events provide, and what is a key limitation the developer should be aware of?

A) Events provide a persistent audit log of all API changes, retained indefinitely for compliance purposes
B) Events provide timestamped records of state changes and errors (such as image pull failures or scheduling decisions), but they are short-lived and typically expire after one hour by default
C) Events only capture container-level logs and are equivalent to running `kubectl logs`
D) Events are only generated for control plane components and do not cover workload-related issues

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes events are API objects that record significant occurrences in the cluster, such as Pod scheduling decisions, image pull errors, container restarts, volume mount failures, and node conditions. They are invaluable for debugging because they surface information not always visible in `kubectl describe`. However, events have a default TTL of one hour (configurable via `--event-ttl` on the API server), so they are not a long-term audit trail. They are distinct from container logs and cover far more than just control plane activity.

**Source:** https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/event-v1/

</details>

---

### Question 30
[MEDIUM-HARD]

A node in a Kubernetes cluster stops responding to the API server and its status transitions to `NotReady`. After the default pod-eviction-timeout elapses, what happens to the Pods that were running on that node?

A) The Pods continue running on the NotReady node indefinitely and are unaffected
B) The kubelet on the node gracefully terminates all Pods as soon as the node becomes NotReady
C) The node controller taints the node and, after the toleration timeout, Pods without matching tolerations are evicted and rescheduled by their controllers on healthy nodes
D) The kube-scheduler immediately moves all Pods to other nodes without any waiting period

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When the node controller detects that a node has stopped reporting its status, it applies a `node.kubernetes.io/not-ready` taint with the `NoExecute` effect. Pods that do not tolerate this taint are evicted after the `tolerationSeconds` period (default 300 seconds). Workload controllers like Deployments and ReplicaSets then create replacement Pods that the scheduler places on healthy nodes. The kubelet on the NotReady node is unresponsive, so it cannot perform graceful termination. The process is not immediate -- the timeout exists to handle transient network issues.

**Source:** https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#taint-based-evictions

</details>
