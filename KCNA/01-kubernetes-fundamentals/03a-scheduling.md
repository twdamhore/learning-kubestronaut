# Scheduling - 100 MCQ Questions (Part A)

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Scheduling
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

## kube-scheduler Basics

## kube-scheduler Basics

### Question 1
[MEDIUM]
What is the primary role of kube-scheduler in Kubernetes?

A) Running containers on nodes
B) Assigning Pods to nodes
C) Managing the API server
D) Storing cluster state

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-scheduler's primary role is to assign newly created Pods to nodes. It watches for Pods without a node assignment and selects optimal nodes based on resource requirements, constraints, and policies.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 2
[MEDIUM-HARD]
What happens to a Pod if no node satisfies its scheduling requirements?

A) The Pod is deleted
B) The Pod remains in Pending state
C) The Pod is scheduled to a random node
D) The scheduler creates a new node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If no node satisfies a Pod's scheduling requirements (resources, affinity, tolerations, etc.), the Pod remains in Pending state. The scheduler will continue to retry scheduling as cluster state changes.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 3
[MEDIUM-HARD]
What is the scoring phase in the scheduling process?

A) Eliminating nodes that don't meet requirements
B) Ranking filtered nodes by preference
C) Binding the Pod to a node
D) Validating Pod specifications

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scoring phase ranks the nodes that passed filtering. Each scoring plugin assigns scores based on criteria like resource availability, affinity preferences, and spread. The node with the highest total score is selected.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 4
[MEDIUM-HARD]
Which scheduling phase comes first: filtering or scoring?

A) Scoring
B) Filtering
C) They run simultaneously
D) It depends on the scheduler configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Filtering always comes before scoring. The scheduler first eliminates unsuitable nodes (filtering), then ranks the remaining nodes (scoring). This is more efficient than scoring all nodes.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 5
[HARD]
Can a Pod specify which scheduler should schedule it?

A) No, all Pods use the default scheduler
B) Yes, using the schedulerName field
C) Yes, using an annotation
D) Only DaemonSet Pods can specify this

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pods can specify a scheduler using the `spec.schedulerName` field. This enables running multiple schedulers for different workload types or custom scheduling logic.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

## Node Selection

### Question 6
[MEDIUM]
What is the simplest way to schedule a Pod to a specific node?

A) nodeSelector
B) nodeName
C) nodeAffinity
D) taints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting `spec.nodeName` directly is the simplest way to schedule a Pod to a specific node. It bypasses the scheduler entirely and places the Pod on the named node.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 7
[MEDIUM-HARD]
Does nodeName bypass the scheduler?

A) No, the scheduler still validates
B) Yes, completely
C) Only for system Pods
D) Only if the node exists

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Yes, nodeName completely bypasses the scheduler. When nodeName is set, the scheduler ignores the Pod. The Pod is directly assigned to that node without any scheduling logic.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 8
[MEDIUM-HARD]
Can nodeName be changed after a Pod is created?

A) Yes, using kubectl edit
B) No, it is immutable
C) Only by an admin
D) Yes, but requires restart

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeName is immutable after Pod creation. Once set (either explicitly or by the scheduler), it cannot be changed. To move a Pod, you must delete and recreate it.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

## nodeSelector

### Question 9
[MEDIUM]
Where is nodeSelector specified in a Pod definition?

A) metadata.nodeSelector
B) spec.nodeSelector
C) spec.template.nodeSelector
D) spec.containers.nodeSelector

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeSelector is specified under `spec.nodeSelector` in a Pod definition. It's a map of key-value pairs that must match node labels.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 10
[MEDIUM-HARD]
What happens if no nodes match the nodeSelector labels?

A) The Pod is scheduled randomly
B) The Pod remains Pending
C) The Pod fails
D) Labels are created automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If no nodes match the nodeSelector labels, the Pod remains in Pending state. The scheduler cannot find a suitable node and will continue retrying.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 11
[HARD]
What is the relationship between nodeSelector and node affinity?

A) They are mutually exclusive
B) nodeSelector is a simpler form of node affinity
C) nodeSelector overrides node affinity
D) They cannot be used on the same Pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeSelector is a simpler, more limited form of node affinity. Node affinity provides more expressive rules with operators like In, NotIn, Exists. Both can be used together—both constraints must be satisfied.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 12
[MEDIUM-HARD]
Are nodeSelector labels case-sensitive?

A) No
B) Yes
C) Only the key is case-sensitive
D) Only the value is case-sensitive

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Yes, both label keys and values are case-sensitive in Kubernetes. "Environment=Production" and "environment=production" are different labels.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 13
[HARD]
What built-in labels are available on nodes for scheduling?

A) Only custom labels
B) kubernetes.io/hostname, topology.kubernetes.io/zone, etc.
C) Only node-role labels
D) No built-in labels exist

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Nodes may have well-known labels such as kubernetes.io/hostname, kubernetes.io/os, kubernetes.io/arch, topology.kubernetes.io/zone, topology.kubernetes.io/region, and node.kubernetes.io/instance-type, depending on environment and cloud provider. These are set by kubelet or cloud controllers, not guaranteed on all nodes.

**Source:** [Well-Known Labels | Kubernetes](https://kubernetes.io/docs/reference/labels-annotations-taints/)

</details>

---

## Node Affinity

### Question 14
[MEDIUM-HARD]
What are the two types of node affinity?

A) hard and soft
B) required and preferred
C) strict and relaxed
D) mandatory and optional

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The two types are requiredDuringSchedulingIgnoredDuringExecution (required/hard) and preferredDuringSchedulingIgnoredDuringExecution (preferred/soft).

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 15
[MEDIUM-HARD]
What does preferredDuringSchedulingIgnoredDuringExecution mean?

A) Strictly required
B) Preferred but not mandatory at scheduling
C) Ignored completely
D) Only for preferred nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduler will try to satisfy these rules but will schedule the Pod even if no matching node is found. It's a soft preference, not a hard requirement.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 16
[MEDIUM-HARD]
Which operators are available in node affinity expressions?

A) Only In and NotIn
B) In, NotIn, Exists, DoesNotExist, Gt, Lt
C) Equals and NotEquals only
D) Only Exists

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Node affinity supports six operators: In, NotIn, Exists, DoesNotExist, Gt (greater than), and Lt (less than). Gt and Lt are for numeric comparisons.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 17
[MEDIUM-HARD]
What does the NotIn operator do in node affinity?

A) Excludes all nodes
B) Checks label value is not in the list
C) Removes labels
D) Negates the entire rule

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NotIn checks that the node's label value is NOT one of the specified values. It's useful for excluding specific nodes or zones.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 18
[MEDIUM-HARD]
What does the DoesNotExist operator do in node affinity?

A) Deletes the label
B) Matches nodes that don't have the label key
C) Fails if label doesn't exist
D) Creates missing nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DoesNotExist matches nodes that do NOT have the specified label key. Useful for excluding nodes with certain labels.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 19
[MEDIUM-HARD]
How do you specify weight for preferred node affinity?

A) Using priority field
B) Using weight field (1-100)
C) Using score field
D) Weights are automatic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Each preferred term has a weight field (1-100). Higher weights mean stronger preference. When a node matches the preference, the scheduler adds the weight to the node's total score. Nodes with higher total scores are preferred for scheduling.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 20
[HARD]
How are multiple node affinity terms combined?

A) AND logic
B) OR logic
C) XOR logic
D) Only one term is evaluated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Multiple terms in nodeSelectorTerms are combined with OR logic—a node must match ANY of the terms. This is different from matchExpressions within a term.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

## Pod Affinity

### Question 21
[MEDIUM]
What is pod affinity?

A) Attracting nodes to pods
B) Scheduling pods near other pods with specific labels
C) Pod health checking
D) Pod networking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod affinity allows you to constrain which nodes a Pod can be scheduled on based on labels of Pods already running on nodes. It enables co-locating related Pods.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 22
[MEDIUM-HARD]
What is a common topologyKey value?

A) pod.name
B) kubernetes.io/hostname
C) container.id
D) app.version

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kubernetes.io/hostname is common for same-node affinity. topology.kubernetes.io/zone is used for zone-level affinity. These are node labels, not pod labels.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 23
[HARD]
Can pod affinity reference pods in other namespaces?

A) No, never
B) Yes, using namespaces or namespaceSelector
C) Only system namespaces
D) Only with admin rights

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod affinity can reference pods in other namespaces using the `namespaces` field (list of namespaces) or `namespaceSelector` (label selector for namespaces). By default, it only considers the same namespace.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 24
[HARD]
What happens if topologyKey is set to kubernetes.io/hostname?

A) Pods are spread across hosts
B) Pods must be on the same node as matching pods
C) Hostname is ignored
D) Only one pod per cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With topologyKey: kubernetes.io/hostname, pods with affinity must be on the exact same node as matching pods (since each node has a unique hostname).

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 25
[MEDIUM-HARD]
Can you combine pod affinity with node affinity?

A) No, they conflict
B) Yes, both are evaluated
C) Only one can be active
D) Only in StatefulSets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod affinity and node affinity can be used together. Both constraints are evaluated, and the Pod must satisfy all of them to be scheduled.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

## Pod Anti-Affinity

### Question 26
[MEDIUM]
What is pod anti-affinity?

A) Pods that hate each other
B) Scheduling pods away from pods with specific labels
C) Removing pod labels
D) Deleting pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod anti-affinity constrains pods to NOT be scheduled on nodes with pods matching certain labels. It's used to spread pods across nodes for high availability.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 27
[MEDIUM-HARD]
How do you specify pod anti-affinity in a Pod spec?

A) spec.antiAffinity
B) spec.affinity.podAntiAffinity
C) spec.nodeAntiAffinity
D) metadata.antiAffinity

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod anti-affinity is specified under `spec.affinity.podAntiAffinity`. It has the same structure as podAffinity with required and preferred sections.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 28
[MEDIUM-HARD]
Can pod anti-affinity use the same operators as pod affinity?

A) No, different operators
B) Yes, same labelSelector operators
C) Only Exists
D) Only In

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod anti-affinity uses the same labelSelector structure and operators (In, NotIn, Exists, DoesNotExist) as pod affinity.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 29
[HARD]
How does anti-affinity affect Deployment rollouts?

A) No effect
B) May slow rollouts if nodes are limited
C) Speeds up rollouts
D) Prevents rollouts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Required anti-affinity can slow rollouts because new pods need nodes without existing pods. With limited nodes, you may need to scale down old pods before new ones can schedule.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 30
[HARD]
Can anti-affinity reference pods from the same Deployment?

A) No, only other deployments
B) Yes, using matching labels
C) Only StatefulSets
D) Only with special annotation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Anti-affinity commonly references pods from the same Deployment using the deployment's pod labels. This spreads replicas across nodes.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

## Taints and Tolerations

### Question 31
[MEDIUM]
What is a taint in Kubernetes?

A) A security vulnerability
B) A property on nodes that repels pods
C) A pod label
D) A network policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A taint is a property on a node that repels pods. Pods must have a matching toleration to be scheduled on a tainted node.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 32
[MEDIUM-HARD]
What are the three taint effects?

A) Allow, Deny, Maybe
B) NoSchedule, PreferNoSchedule, NoExecute
C) Hard, Soft, Medium
D) Block, Warn, Pass

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The three effects are: NoSchedule (don't schedule), PreferNoSchedule (try to avoid), and NoExecute (don't schedule AND evict existing pods).

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 33
[MEDIUM-HARD]
What does the PreferNoSchedule effect do?

A) Strictly prevents scheduling
B) Tries to avoid scheduling but allows if necessary
C) Same as NoSchedule
D) Only for preferred pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PreferNoSchedule is a soft version of NoSchedule. The scheduler tries to avoid placing pods without tolerations but will do so if no other options exist.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 34
[MEDIUM-HARD]
How do you add a taint to a node?

A) kubectl label node
B) kubectl taint nodes node-name key=value:effect
C) kubectl annotate node
D) kubectl apply taint

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl taint nodes <node-name> <key>=<value>:<effect>` to add a taint. Example: `kubectl taint nodes node1 dedicated=gpu:NoSchedule`

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 35
[MEDIUM-HARD]
Where are tolerations specified?

A) On nodes
B) In Pod spec under tolerations
C) In namespace
D) In ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Tolerations are specified in the Pod's spec under the `tolerations` field. They're pod properties, not node properties.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 36
[MEDIUM-HARD]
What does the Equal operator do in tolerations?

A) Matches any taint
B) Matches taint with same key and value
C) Checks equality of nodes
D) Compares pod names

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Equal operator matches a taint only if both the key and value match exactly. The effect must also match.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 37
[HARD]
How do you tolerate all taints on a node?

A) Cannot be done
B) Use empty key with Exists operator
C) Use wildcard *
D) Set toleration to "all"

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An empty key with Exists operator tolerates all taints: `tolerations: [{operator: "Exists"}]`. This is useful for pods that should run anywhere.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 38
[MEDIUM-HARD]
What built-in taints does Kubernetes add automatically?

A) None
B) node.kubernetes.io/not-ready, unreachable, memory-pressure, etc.
C) Only custom taints
D) Only on master nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes automatically adds taints for node conditions: not-ready, unreachable, memory-pressure, disk-pressure, pid-pressure, network-unavailable, and unschedulable.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 39
[HARD]
What is the node.kubernetes.io/unreachable taint?

A) For offline nodes
B) Auto-added when node controller can't reach the node
C) Manual taint
D) Network policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** This NoExecute taint is added when the node controller cannot reach the node (network issues). It's different from not-ready which indicates the node itself is unhealthy.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 40
[MEDIUM-HARD]
Can a Pod tolerate multiple taints?

A) No, only one
B) Yes, by specifying multiple tolerations
C) Only two
D) Only with special flag

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod can have multiple tolerations in its spec. Each toleration can match different taints. The Pod must tolerate ALL taints on a node to be scheduled there.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

## Resource Requests and Scheduling

### Question 41
[MEDIUM]
How do resource requests affect scheduling?

A) They don't affect scheduling
B) Scheduler uses requests to find nodes with sufficient resources
C) Only limits matter
D) Resources are ignored

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduler uses resource requests (not limits) to determine if a node has sufficient capacity. A Pod is only scheduled if the node's allocatable resources minus existing requests >= the Pod's requests.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 42
[MEDIUM-HARD]
What happens if no node has enough resources for a Pod's requests?

A) Pod is scheduled anyway
B) Pod remains Pending
C) Resources are borrowed
D) Node is scaled up

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If no node has sufficient allocatable resources to satisfy a Pod's requests, the Pod remains in Pending state until resources become available (pods finish, new nodes added).

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 43
[HARD]
What is the allocatable capacity of a node?

A) Total hardware resources
B) Resources available for pods after system reservations
C) Maximum pod count
D) Network bandwidth

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Allocatable = Capacity - kube-reserved - system-reserved - eviction-threshold. It's the resources actually available for pod scheduling after accounting for system needs.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 44
[HARD]
What resources are reserved for system components?

A) None
B) kube-reserved and system-reserved (CPU, memory, etc.)
C) Only memory
D) Only disk

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-reserved is for Kubernetes daemons (kubelet, container runtime). system-reserved is for OS daemons. Both can reserve CPU, memory, and ephemeral storage.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 45
[HARD]
What is resource overcommitment?

A) When actual resource usage exceeds requested amounts
B) When the sum of resource limits exceeds node capacity
C) Requesting infinite resources
D) Resource sharing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Overcommitment occurs when the total resource limits of all pods on a node exceed the node's capacity. Kubernetes allows this because pods rarely use their full limits simultaneously. The scheduler uses requests (not limits) for placement, so limits can sum to more than 100% of capacity.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

## Pod Priority and Preemption

### Question 46
[MEDIUM]
What is Pod priority?

A) Network priority
B) A value determining scheduling and eviction order
C) CPU priority
D) Start order

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod priority is an integer value that indicates the importance of a Pod. Higher priority pods are scheduled first and can preempt lower priority pods.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 47
[MEDIUM-HARD]
What is a PriorityClass?

A) A pod label
B) A cluster resource defining priority value and settings
C) A node type
D) A namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PriorityClass is a cluster-scoped resource that defines a priority value, optional preemption policy, and optional description. Pods reference it by name.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 48
[HARD]
What does preemption mean in Kubernetes scheduling?

A) Scheduling faster
B) Evicting lower-priority pods to schedule higher-priority ones
C) Preventing scheduling
D) Priority inversion

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Preemption is when the scheduler evicts (preempts) lower-priority pods from a node to make room for a higher-priority pod that cannot otherwise be scheduled.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 49
[HARD]
Can preemption be disabled for a PriorityClass?

A) No
B) Yes, using preemptionPolicy: Never
C) Only for system classes
D) Only temporarily

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting `preemptionPolicy: Never` in a PriorityClass prevents pods of that class from preempting others. They still have scheduling priority but won't evict other pods.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 50
[MEDIUM-HARD]
What is the default priority for pods without a PriorityClass?

A) 0
B) -1
C) 100
D) Highest

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Pods without a priorityClassName get priority 0 by default (unless a global default PriorityClass is defined). This is the lowest normal priority.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 51
[HARD]
What is the system-node-critical PriorityClass?

A) For user pods
B) For critical node-level components, higher than cluster-critical
C) Same as system-cluster-critical
D) Deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** system-node-critical has the highest priority (~2 billion + 1000) for node-critical components like kube-proxy. It's even higher than system-cluster-critical.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 52
[MEDIUM-HARD]
What is the globalDefault field in PriorityClass?

A) Sets global timeout
B) Makes this class the default for pods without priorityClassName
C) Applies to all clusters
D) Default namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting `globalDefault: true` makes this PriorityClass the default for pods that don't specify a priorityClassName. Only one PriorityClass should be the global default.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 53
[HARD]
What happens to preempted pods?

A) They are deleted permanently
B) They receive SIGTERM and are gracefully terminated
C) They are paused
D) They move to another node automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Preempted pods receive SIGTERM for graceful termination. If managed by a controller (Deployment, ReplicaSet), replacements are scheduled elsewhere. The pods don't automatically move.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

## Pod Topology Spread Constraints

### Question 54
[MEDIUM-HARD]
What is maxSkew in topology spread?

A) Maximum pods per node
B) Maximum difference in pod count between domains
C) Network latency
D) CPU imbalance

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** maxSkew is the maximum allowed difference between the number of matching pods in any two topology domains. A skew of 1 means perfect balance.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 55
[HARD]
What does DoNotSchedule do in topology spread?

A) Allows scheduling
B) Prevents scheduling if constraint can't be satisfied
C) Deletes pods
D) Ignores constraint

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DoNotSchedule is a hard constraint. If scheduling the pod would violate maxSkew, the pod remains Pending until a valid placement exists.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 56
[MEDIUM-HARD]
What is topologyKey in topology spread constraints?

A) Pod label
B) Node label key defining topology domains
C) Namespace
D) Container name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** topologyKey is the node label key that defines topology domains. Nodes with the same value for this label are in the same domain. Common keys: kubernetes.io/hostname, topology.kubernetes.io/zone.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 57
[HARD]
Can you specify multiple topology spread constraints?

A) No, only one
B) Yes, and all DoNotSchedule constraints must be satisfied
C) Maximum of two
D) Only in namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Multiple topology spread constraints can be specified. All `DoNotSchedule` constraints must be satisfied for scheduling. However, `ScheduleAnyway` constraints are best-effort and may be violated if no node satisfies them. This allows spreading across both zones AND nodes.

**Source:** [Pod Topology Spread Constraints | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)

</details>

---

### Question 58
[HARD]
How does the scheduler calculate skew?

A) Random
B) Max pods in domain minus min pods in domain
C) Average minus min
D) Total divided by domains

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Skew = (max pods in any domain) - (min pods in any domain). The scheduler checks if adding the pod to a domain would exceed maxSkew.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

## DaemonSet Scheduling

### Question 59
[MEDIUM-HARD]
Does DaemonSet use the default scheduler?

A) No, never
B) Yes, by default
C) Uses custom scheduler
D) Kubelet schedules directly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Since Kubernetes 1.12, DaemonSets use the default scheduler by default. Previously, the DaemonSet controller handled scheduling directly.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 60
[HARD]
What tolerations do DaemonSets automatically get?

A) None
B) Tolerations for not-ready, unreachable, disk-pressure, memory-pressure, pid-pressure, unschedulable
C) All tolerations
D) Only NoExecute tolerations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSet pods automatically get tolerations for: not-ready and unreachable (NoExecute), plus disk-pressure, memory-pressure, pid-pressure, and unschedulable (NoSchedule). For hostNetwork pods, network-unavailable is also added.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 61
[MEDIUM-HARD]
Can you use node affinity with DaemonSets?

A) No
B) Yes
C) Only required affinity
D) Only preferred affinity

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets fully support node affinity. You can use both required and preferred affinity rules to control which nodes run DaemonSet pods.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 62
[MEDIUM-HARD]
How do you prevent a DaemonSet from scheduling on specific nodes?

A) Cannot be done
B) Use nodeSelector, node affinity, or taints
C) Delete the nodes
D) Disable the DaemonSet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use nodeSelector/affinity to limit which nodes are eligible, or add taints to nodes you want to exclude (and don't add matching tolerations to the DaemonSet).

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 63
[HARD]
How do DaemonSets handle unschedulable nodes?

A) Skip them
B) They schedule anyway if no conflicting taints
C) Create new nodes
D) Wait indefinitely

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets automatically tolerate the node.kubernetes.io/unschedulable taint, so they can schedule on cordoned nodes. This ensures system pods run everywhere.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

## Static Pods

### Question 64
[MEDIUM-HARD]
Who manages static Pods?

A) kube-scheduler
B) kubelet on the node
C) kube-controller-manager
D) etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet directly manages static pods. It reads manifests from a configured directory and creates/maintains pods without API server involvement.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 65
[MEDIUM-HARD]
How does kubelet discover static Pod manifests?

A) API server notifies it
B) Watches a configured directory (staticPodPath)
C) Manual reload required
D) Through etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet is configured with --pod-manifest-path (staticPodPath) to watch a directory. It automatically detects new/modified/deleted manifest files.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 66
[MEDIUM-HARD]
What is a mirror Pod?

A) A backup pod
B) A read-only API representation of a static pod
C) A replicated pod
D) A shadow container

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Mirror pods are created by kubelet in the API server to represent static pods. They allow you to see static pod status through normal API tools but can't be modified.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 67
[MEDIUM-HARD]
What control plane components run as static Pods?

A) None
B) kube-apiserver, kube-controller-manager, kube-scheduler, etcd
C) Only etcd
D) Only kube-proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In kubeadm clusters, control plane components (apiserver, controller-manager, scheduler, etcd) run as static pods. This bootstraps the cluster before the API is available.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 68
[HARD]
What happens if a static Pod manifest is deleted?

A) Pod continues running
B) Kubelet terminates the pod
C) Pod becomes orphaned
D) Nothing until reboot

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a static pod manifest is deleted, the kubelet detects this and terminates the pod. The mirror pod is also removed from the API.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

## Manual Scheduling

### Question 69
[MEDIUM-HARD]
What field is used for manual scheduling?

A) spec.scheduler
B) spec.nodeName
C) spec.node
D) spec.target

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** spec.nodeName specifies the exact node for the pod. When set, the scheduler is bypassed completely.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 70
[MEDIUM-HARD]
Does manual scheduling bypass admission controllers?

A) Yes, completely
B) No, admission controllers still run
C) Only some controllers
D) Depends on configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Admission controllers still validate the pod even with nodeName set. What's bypassed is the scheduler—not admission control, authentication, or authorization.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 71
[HARD]
How can you create a custom scheduler?

A) Modify kube-scheduler code
B) Write a program that watches pods and creates Bindings
C) Only through plugins
D) Cannot be done

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A custom scheduler watches for pods with its schedulerName, makes scheduling decisions, and creates Binding objects to assign pods to nodes.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 72
[HARD]
Can you change nodeName after Pod creation?

A) Yes, with kubectl edit
B) No, nodeName is immutable after scheduling
C) Only for running pods
D) Only with admin rights

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeName is immutable. Once the pod is bound to a node (either by scheduler or manually), it cannot be moved. Delete and recreate to change placement.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 73
[MEDIUM-HARD]
Does nodeName respect taints?

A) Yes
B) No, nodeName bypasses taint checks
C) Only NoSchedule
D) Only NoExecute

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeName bypasses the scheduler entirely, including taint checks. However, NoExecute taints still evict running pods without tolerations.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

## Multiple Schedulers

### Question 74
[MEDIUM-HARD]
How do you specify which scheduler should schedule a Pod?

A) spec.scheduler
B) spec.schedulerName
C) metadata.scheduler
D) annotation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Set spec.schedulerName to the name of the scheduler. If not specified, "default-scheduler" is used.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 75
[HARD]
What happens if the specified scheduler doesn't exist?

A) Default scheduler takes over
B) Pod remains Pending indefinitely
C) Pod fails
D) Error at creation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If no scheduler with the specified name is running, the pod remains Pending forever. No scheduler will claim it. The default scheduler only handles pods with its name.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 76
[HARD]
Can multiple schedulers compete for the same Pod?

A) Yes
B) No, only one scheduler is specified per pod
C) Sometimes
D) Only with locks

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Each pod has exactly one schedulerName. Only that scheduler will attempt to schedule it. There's no competition or conflict.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 77
[HARD]
How do you configure scheduler leader election?

A) Not needed
B) Via --leader-elect flag and lease objects
C) Manual configuration
D) Automatic only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For HA, multiple scheduler replicas use leader election via --leader-elect. Only the leader schedules pods. They use Lease objects for coordination.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 78
[HARD]
How do scheduler plugins differ from extenders?

A) Same thing
B) Plugins are compiled in; extenders are external webhooks
C) Extenders are faster
D) Plugins are deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Plugins are Go code compiled into the scheduler (fast, full access). Extenders are external HTTP services (slower, more flexible deployment). Plugins are preferred for performance.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

## Scheduler Profiles

### Question 79
[HARD]
Can a single scheduler run multiple profiles?

A) No
B) Yes, pods select profile via schedulerName
C) Maximum two
D) Only in clusters

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** One scheduler instance can serve multiple profiles. Each profile has a unique name used as schedulerName. Different profiles can have different plugin configurations.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 80
[HARD]
What are the scheduler extension points?

A) API endpoints
B) Stages where plugins can hook into scheduling
C) Network points
D) Storage points

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Extension points are phases in scheduling where plugins run: QueueSort, PreFilter, Filter, PostFilter, PreScore, Score, Reserve, Permit, PreBind, Bind, PostBind.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 81
[HARD]
What is the Filter extension point?

A) Network filtering
B) Determines which nodes are feasible for the pod
C) Log filtering
D) Event filtering

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Filter plugins check each node to determine if it can run the pod. Nodes failing any filter are eliminated. Only passing nodes proceed to scoring.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 82
[HARD]
What is the Score extension point?

A) Game scoring
B) Ranks feasible nodes by preference
C) Health scoring
D) Priority scoring

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Score plugins assign scores (0-100) to feasible nodes based on preferences (resource balance, affinity, spread). Nodes are ranked by total weighted score.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 83
[HARD]
What is the Bind extension point?

A) Network binding
B) Actually binds the pod to the node
C) Volume binding only
D) Service binding

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bind plugins create the binding between pod and node. The default Bind plugin calls the API server to set the pod's nodeName. Custom plugins can handle special binding logic.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

## Scheduler Plugins

### Question 84
[HARD]
What is the NodeResourcesFit plugin?

A) Resizes nodes
B) Checks if node has enough resources for pod
C) Balances resources
D) Limits resources

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NodeResourcesFit filters nodes that don't have sufficient resources (CPU, memory) to satisfy the pod's requests. It also scores based on resource fit strategies.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 85
[HARD]
What is the PodTopologySpread plugin?

A) Network topology
B) Implements topology spread constraints
C) Pod distribution
D) Zone management

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PodTopologySpread implements topology spread constraints. It filters nodes that would violate maxSkew and scores to minimize skew across topology domains.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 86
[HARD]
What is the TaintToleration plugin?

A) Adds taints
B) Filters nodes based on taints and pod tolerations
C) Removes taints
D) Validates tolerations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** TaintToleration filters nodes with taints not tolerated by the pod. It ensures pods only schedule on nodes whose taints they can tolerate.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 87
[HARD]
What is the default set of enabled plugins?

A) None
B) NodeResourcesFit, NodeAffinity, TaintToleration, and many others
C) Only NodeResourcesFit
D) All plugins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Default plugins include NodeResourcesFit, NodeAffinity, TaintToleration, NodePorts, PodTopologySpread, InterPodAffinity, VolumeBinding, and several others.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 88
[HARD]
What is the scheduler framework?

A) UI framework
B) The plugin-based architecture for kube-scheduler
C) Network framework
D) Testing framework

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduler framework is the plugin-based architecture introduced in Kubernetes 1.15+. It replaced the old predicate/priority functions with a more modular, extensible design.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

## Scheduling Troubleshooting

### Question 89
[MEDIUM-HARD]
What events indicate scheduling failures?

A) Started events
B) FailedScheduling events
C) Killed events
D) Created events

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** FailedScheduling events indicate the scheduler couldn't place the pod. The event message describes reasons: insufficient resources, unmet affinity, taints, etc.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 90
[MEDIUM-HARD]
What does "node(s) had taint that pod didn't tolerate" mean?

A) Node has no taints
B) Pod lacks toleration for node's taint
C) Taint is invalid
D) Pod has too many tolerations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The node has a taint that the pod doesn't tolerate. Add a matching toleration to the pod spec or remove the taint from the node.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 91
[HARD]
How do you debug node affinity issues?

A) Check pod events only
B) Compare pod's affinity rules with node labels
C) Restart scheduler
D) Delete affinity

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Debug by: 1) kubectl describe pod to see events, 2) kubectl get nodes --show-labels to see node labels, 3) Compare labels against affinity expressions.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 92
[MEDIUM-HARD]
What does "0/3 nodes are available" mean?

A) Cluster has no nodes
B) No nodes passed the filter phase
C) All nodes are ready
D) Three nodes are pending

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** This means 0 out of 3 nodes passed all filter checks. The message usually lists why each node failed (taints, resources, affinity, etc.).

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 93
[HARD]
What is the scheduler's verbose logging?

A) Disabled by default
B) Detailed logs at higher verbosity levels (-v=10)
C) Separate log file
D) UI dashboard

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Increase verbosity with -v flag (e.g., -v=10) to see detailed scheduling decisions, scoring, and filtering. Logs show why nodes were selected or rejected.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

## Advanced Scheduling Concepts

### Question 94
[HARD]
What does the MostAllocated scoring strategy do in NodeResourcesFit?

A) Spreads pods across nodes
B) Favors nodes with higher resource allocation (pack pods tightly)
C) Ignores resource allocation
D) Only considers CPU

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** MostAllocated is a scoring strategy in the NodeResourcesFit plugin that favors nodes with higher resource allocation. This packs pods onto fewer nodes, maximizing utilization and potentially reducing costs.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 95
[HARD]
How does the scheduler handle pod overhead?

A) Ignores it
B) Includes overhead in resource calculations
C) Separate scheduling
D) Only for VMs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod overhead (specified in RuntimeClass) is added to container requests when scheduling. This accounts for sandbox/VM overhead in virtualization runtimes like Kata.

**Source:** [Managing Resources for Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 96
[HARD]
What are the sub-queues in the scheduling queue?

A) Only one queue
B) Active, backoff, and unschedulable queues
C) Priority queues only
D) FIFO only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Three queues: Active (ready to schedule), Backoff (recently failed, waiting to retry), Unschedulable (waiting for cluster changes that might help).

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 97
[HARD]
What is the nominated node?

A) Preferred node
B) Node where pod will be scheduled after preemption completes
C) Random node
D) Backup node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When preemption is triggered, the nominated node is where the pod will schedule once lower-priority pods are evicted and resources are freed.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 98
[HARD]
What is delayed binding for volumes?

A) Instant binding
B) Wait to bind PVC until pod is scheduled
C) Never bind
D) Manual binding

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** WaitForFirstConsumer storage class delays PVC binding until a pod using it is scheduled. This allows the scheduler to consider pod constraints when choosing volume topology.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 99
[HARD]
How does scheduling work with generic ephemeral volumes?

A) Not supported
B) Follows PVC binding; WaitForFirstConsumer enables topology-aware placement
C) Same as emptyDir
D) No scheduling needed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Generic ephemeral volumes are PVC-backed and follow standard PVC binding. Using WaitForFirstConsumer storage class enables topology-aware placement, ensuring pods are scheduled on nodes where storage is available. Note: other ephemeral volumes like emptyDir, configMap, and secret don't involve topology-aware scheduling.

**Source:** [Ephemeral Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/) and [Storage Classes | Kubernetes](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode)

</details>

---

### Question 100
[HARD]
What is the Kubernetes Descheduler?

A) Built-in component
B) Separate project that evicts pods to improve balance
C) Scheduler plugin
D) Deprecated tool

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Descheduler is a separate component (not built into Kubernetes) that evicts pods based on policies to improve cluster balance. It complements the scheduler by handling post-scheduling optimization, but must be deployed separately.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

