# Kubernetes Scheduling - 200 MCQ Questions

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Scheduling
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

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
[MEDIUM]
Which component does kube-scheduler communicate with to assign Pods to nodes?

A) kubelet
B) kube-proxy
C) kube-apiserver
D) etcd directly

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-scheduler communicates with the kube-apiserver to watch for unscheduled Pods and to update Pod assignments. It never communicates directly with etcd or kubelet—all communication goes through the API server.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 3
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

### Question 4
[MEDIUM-HARD]
In which phase does the scheduler filter out unsuitable nodes?

A) Scoring phase
B) Binding phase
C) Filtering phase
D) Preemption phase

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The filtering phase (also called predicates) eliminates nodes that don't meet the Pod's requirements. Only nodes that pass all filter plugins proceed to the scoring phase.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 5
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

### Question 6
[HARD]
What happens when multiple nodes have the same highest score?

A) Scheduling fails
B) The first node alphabetically is chosen
C) One is selected randomly
D) The Pod remains pending

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When multiple nodes have the same highest score, the scheduler selects one randomly (or round-robin in some implementations). This ensures fair distribution when nodes are equally suitable.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 7
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

### Question 8
[MEDIUM-HARD]
What is the default scheduler name in Kubernetes?

A) kube-scheduler
B) default-scheduler
C) scheduler
D) kubernetes-scheduler

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The default scheduler name is "default-scheduler". While the binary is called kube-scheduler, pods use "default-scheduler" as the schedulerName value unless otherwise specified.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 9
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

### Question 10
[MEDIUM-HARD]
What field in a Pod spec determines which scheduler handles it?

A) spec.scheduler
B) spec.schedulerName
C) metadata.scheduler
D) spec.nodeName

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `spec.schedulerName` field specifies which scheduler should handle the Pod. If not set, it defaults to "default-scheduler". nodeName bypasses the scheduler entirely.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

## Node Selection

### Question 11
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

### Question 12
[MEDIUM-HARD]
What happens if you specify a nodeName that doesn't exist?

A) The Pod is scheduled to a random node
B) The Pod remains in Pending state
C) The scheduler creates the node
D) The Pod fails immediately

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If the specified nodeName doesn't exist, the Pod remains Pending. The kubelet on that node would need to exist to run the Pod, and since the node doesn't exist, the Pod cannot be started.


**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)
</details>

---

### Question 13
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

### Question 14
[HARD]
What are the limitations of using nodeName for scheduling?

A) It only works with StatefulSets
B) It bypasses scheduling constraints and can fail if node doesn't exist
C) It requires admin privileges
D) It can only be used once per node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeName bypasses all scheduling constraints (taints, affinity, resource checks). If the node doesn't exist, has insufficient resources, or is unhealthy, the Pod may fail or remain pending indefinitely.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 15
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

### Question 16
[MEDIUM]
What is a nodeSelector?

A) A way to select containers
B) A simple label-based node selection mechanism
C) A network policy
D) A resource quota

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeSelector is a simple mechanism to constrain Pods to nodes with specific labels. It's the simplest form of node selection constraint in Kubernetes.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 17
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

### Question 18
[MEDIUM-HARD]
What type of matching does nodeSelector use?

A) Regex matching
B) Exact equality matching
C) Prefix matching
D) Wildcard matching

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeSelector uses exact equality matching. The node must have labels with exactly the same keys and values specified in the nodeSelector.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 19
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

### Question 20
[MEDIUM-HARD]
Can you use multiple labels in a nodeSelector?

A) No, only one label is allowed
B) Yes, and all must match (AND logic)
C) Yes, any can match (OR logic)
D) Only with node affinity

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Multiple labels can be specified in nodeSelector, and ALL must match (AND logic). The node must have every label with the exact values specified.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 21
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

### Question 22
[MEDIUM-HARD]
How do you label a node for use with nodeSelector?

A) kubectl label pods
B) kubectl label nodes node-name key=value
C) kubectl annotate nodes
D) kubectl taint nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl label nodes <node-name> <key>=<value>` to add labels to nodes. These labels can then be used in nodeSelector to constrain Pod placement.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 23
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

### Question 24
[MEDIUM-HARD]
Can nodeSelector use inequality operators?

A) Yes, using != syntax
B) No, only equality matching
C) Yes, using NotIn
D) Only with expressions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nodeSelector only supports equality matching. For inequality or other operators (NotIn, Exists, DoesNotExist), you must use node affinity with matchExpressions.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 25
[HARD]
What built-in labels are available on nodes for scheduling?

A) Only custom labels
B) kubernetes.io/hostname, topology.kubernetes.io/zone, etc.
C) Only node-role labels
D) No built-in labels exist

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes automatically adds labels like kubernetes.io/hostname, kubernetes.io/os, kubernetes.io/arch, topology.kubernetes.io/zone, topology.kubernetes.io/region, and node.kubernetes.io/instance-type.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

## Node Affinity

### Question 26
[MEDIUM]
What is node affinity?

A) A way to reject nodes
B) An expressive way to constrain Pod placement on nodes
C) A node health metric
D) A network policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Node affinity is an expressive way to constrain which nodes a Pod can be scheduled on based on node labels. It's more flexible than nodeSelector, supporting operators like In, NotIn, Exists.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 27
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

### Question 28
[MEDIUM-HARD]
What does requiredDuringSchedulingIgnoredDuringExecution mean?

A) Required at all times
B) Must match at scheduling, ignored if node changes later
C) Only checked during execution
D) Never required

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The rule must be satisfied for the Pod to be scheduled. "IgnoredDuringExecution" means if node labels change after scheduling, the Pod won't be evicted.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 29
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

### Question 30
[HARD]
What does "IgnoredDuringExecution" mean in node affinity rules?

A) Rules are always enforced
B) Running Pods won't be evicted if node labels change
C) Rules are ignored after 1 hour
D) Only new Pods follow the rules

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "IgnoredDuringExecution" means affinity rules are only checked at scheduling time. If a node's labels change after the Pod is running, the Pod won't be evicted. A future "RequiredDuringExecution" type would evict pods.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 31
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

### Question 32
[MEDIUM-HARD]
What does the In operator do in node affinity?

A) Checks if key is in a list
B) Checks if label value is in a list of values
C) Includes all nodes
D) Checks string contains

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The In operator checks if the node's label value for a given key is one of the specified values. Example: key: zone, operator: In, values: [us-east-1a, us-east-1b].

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 33
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

### Question 34
[MEDIUM-HARD]
What does the Exists operator do in node affinity?

A) Checks if value exists
B) Checks if label key exists regardless of value
C) Checks if node exists
D) Creates the label if missing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Exists checks only that the label key exists on the node—the value doesn't matter. You don't specify values with Exists.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 35
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

### Question 36
[HARD]
What do the Gt and Lt operators do in node affinity?

A) String comparison
B) Numeric comparison (greater than, less than)
C) Time comparison
D) Size comparison

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Gt (greater than) and Lt (less than) perform numeric comparisons on label values. The label value must be parseable as an integer. Useful for version-based or capacity-based scheduling.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 37
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

### Question 38
[HARD]
What is the valid range for node affinity weights?

A) 0-100
B) 1-100
C) 1-1000
D) Any positive integer

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Weights must be in the range 1-100. Weight 0 is not valid. The total score is the sum of (weight × match) across all preferred terms.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 39
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

### Question 40
[HARD]
How are multiple matchExpressions within a term combined?

A) OR logic
B) AND logic
C) Randomly selected
D) First match wins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Multiple matchExpressions within the same nodeSelectorTerm are combined with AND logic—a node must satisfy ALL expressions in the term.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

## Pod Affinity

### Question 41
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

### Question 42
[MEDIUM-HARD]
What is the topologyKey in pod affinity?

A) A pod label
B) A node label key that defines the topology domain
C) A namespace
D) A container name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** topologyKey is a node label key that defines topology domains. Pods are co-located when they're on nodes with the same value for this label. Common values: kubernetes.io/hostname, topology.kubernetes.io/zone.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 43
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

### Question 44
[MEDIUM-HARD]
What does pod affinity's requiredDuringSchedulingIgnoredDuringExecution do?

A) Optional matching
B) Must schedule near matching pods
C) Ignore all pods
D) Execute immediately

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Required pod affinity means the Pod MUST be scheduled on a node in the same topology domain as pods matching the labelSelector. If no such node exists, the Pod stays Pending.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 45
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

### Question 46
[MEDIUM-HARD]
What is the labelSelector in pod affinity used for?

A) Selecting nodes
B) Selecting which pods to be near/avoid
C) Selecting containers
D) Selecting namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The labelSelector in pod affinity specifies which pods to consider for the affinity rule. The scheduler looks for pods matching these labels and places the new pod accordingly.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 47
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

### Question 48
[HARD]
What is the performance impact of pod affinity rules?

A) No impact
B) Can significantly slow scheduling in large clusters
C) Improves performance
D) Only affects networking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod affinity requires checking all pods in relevant namespaces against the selector, which can be expensive in large clusters. This is why it's recommended to use with caution at scale.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 49
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

### Question 50
[HARD]
What is the namespaceSelector field in pod affinity?

A) Selects namespace for the pod
B) Matches namespaces containing pods to consider
C) Creates namespaces
D) Deletes namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** namespaceSelector uses label selectors to determine which namespaces' pods should be considered for affinity. This is more dynamic than listing specific namespaces.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

## Pod Anti-Affinity

### Question 51
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

### Question 52
[MEDIUM-HARD]
When would you use pod anti-affinity?

A) To group pods together
B) To spread replicas across nodes for high availability
C) To speed up scheduling
D) To reduce costs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod anti-affinity is typically used to spread replicas across failure domains (nodes, zones) to ensure high availability. If one node fails, not all replicas are lost.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 53
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

### Question 54
[HARD]
What is the difference between required and preferred anti-affinity?

A) No difference
B) Required must be satisfied; preferred is best-effort
C) Preferred is stronger
D) Required is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Required anti-affinity must be satisfied or the Pod won't schedule. Preferred anti-affinity is best-effort—the scheduler tries to satisfy it but will schedule anyway if it can't.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 55
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

### Question 56
[HARD]
What happens when anti-affinity conflicts with other scheduling constraints?

A) Anti-affinity always wins
B) Pod may remain pending if no valid node exists
C) Constraints are ignored
D) Random node selected

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If required anti-affinity conflicts with other constraints (like resource requirements or node affinity), and no node satisfies all constraints, the Pod remains Pending.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 57
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

### Question 58
[MEDIUM-HARD]
What topologyKey would spread pods across availability zones?

A) kubernetes.io/hostname
B) topology.kubernetes.io/zone
C) node.kubernetes.io/zone
D) cluster.zone

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** topology.kubernetes.io/zone is the standard label for availability zones. Using this as topologyKey spreads pods across different zones.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

### Question 59
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

### Question 60
[HARD]
What are the limitations of pod anti-affinity?

A) None
B) Performance impact, requires topologyKey, complexity
C) Only works with 3+ nodes
D) Cannot use with DaemonSets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Limitations include: performance overhead in large clusters, topologyKey is required, can make scheduling impossible with limited nodes, and adds complexity to Pod specs.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity)

</details>

---

## Taints and Tolerations

### Question 61
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

### Question 62
[MEDIUM]
What is a toleration?

A) A node property
B) A pod property that allows scheduling on tainted nodes
C) A security setting
D) A network rule

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A toleration is specified on Pods and allows (but doesn't require) the Pod to be scheduled on nodes with matching taints.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 63
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

### Question 64
[MEDIUM-HARD]
What does the NoSchedule effect do?

A) Schedules pods normally
B) Prevents new pods without toleration from scheduling
C) Removes all pods
D) Only affects system pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NoSchedule prevents pods without a matching toleration from being scheduled on the node. Existing pods are not affected.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 65
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

### Question 66
[MEDIUM-HARD]
What does the NoExecute effect do?

A) Only affects new pods
B) Evicts running pods without toleration and prevents new ones
C) Executes pods immediately
D) Disables pod execution

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NoExecute affects both scheduling and running pods. Pods without matching tolerations are evicted from the node, and new pods won't be scheduled.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 67
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

### Question 68
[MEDIUM-HARD]
How do you remove a taint from a node?

A) kubectl taint nodes node-name key:effect-
B) kubectl untaint node
C) kubectl remove taint
D) kubectl delete taint

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Add a minus sign at the end to remove: `kubectl taint nodes node1 dedicated=gpu:NoSchedule-` or `kubectl taint nodes node1 dedicated:NoSchedule-`

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 69
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

### Question 70
[HARD]
What operators are available for tolerations?

A) Only Equal
B) Equal and Exists
C) In, NotIn, Exists
D) All comparison operators

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Tolerations support two operators: Equal (matches specific key-value) and Exists (matches any taint with that key regardless of value).

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 71
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

### Question 72
[MEDIUM-HARD]
What does the Exists operator do in tolerations?

A) Checks if pod exists
B) Matches taint by key only, regardless of value
C) Creates missing taints
D) Validates node existence

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Exists operator matches any taint with the specified key, regardless of value. You don't specify a value when using Exists.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 73
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

### Question 74
[HARD]
What is tolerationSeconds used for?

A) Timeout for scheduling
B) Time to remain on node with NoExecute taint before eviction
C) Scheduling delay
D) Taint duration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** tolerationSeconds specifies how long a pod can remain on a node after a NoExecute taint is applied. After this time, the pod is evicted. Without it, the pod stays indefinitely.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 75
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

### Question 76
[HARD]
What is the node.kubernetes.io/not-ready taint?

A) Manual taint
B) Auto-added when node is not ready
C) For new nodes only
D) Deprecated taint

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** This taint is automatically added when a node's Ready condition is False. It has NoExecute effect, so pods without toleration are evicted after tolerationSeconds.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 77
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

### Question 78
[HARD]
How do taints and tolerations differ from node affinity?

A) No difference
B) Taints repel pods; affinity attracts pods
C) Taints are for nodes; affinity is for pods
D) They are mutually exclusive

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Taints/tolerations repel pods from nodes (opt-out model). Node affinity attracts pods to nodes (opt-in model). Both are complementary—use taints to repel, affinity to attract.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 79
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

### Question 80
[HARD]
What happens to running pods when a NoExecute taint is added?

A) Nothing
B) Pods without matching toleration are evicted
C) All pods are evicted
D) Only new pods are affected

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a NoExecute taint is added, pods without matching toleration are evicted. Pods with toleration and tolerationSeconds are evicted after that duration.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

## Resource Requests and Scheduling

### Question 81
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

### Question 82
[MEDIUM-HARD]
What resources are typically specified for scheduling?

A) Only CPU
B) CPU and memory
C) Only memory
D) Disk and network

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CPU and memory are the primary resources for scheduling. Extended resources (like GPUs) can also be scheduled. Disk and network aren't typically used for scheduling decisions.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 83
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

### Question 84
[MEDIUM-HARD]
Does the scheduler consider resource limits or requests?

A) Only limits
B) Only requests
C) Both equally
D) Neither

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduler only considers requests for placement decisions. Limits are enforced by the kubelet at runtime. A Pod with high limits but low requests might be scheduled on a node that can't actually support the limits.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 85
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

### Question 86
[MEDIUM-HARD]
How is allocatable different from total capacity?

A) They are the same
B) Allocatable = Capacity - reserved for system
C) Allocatable is always higher
D) Allocatable is for storage only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Capacity is total node resources. Allocatable is what's available for pods after subtracting resources reserved for Kubernetes components and the operating system.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 87
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

### Question 88
[MEDIUM-HARD]
Can a Pod be scheduled if it exceeds available resources?

A) Yes, always
B) No, it will remain Pending
C) Only with priority
D) Only system pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Pod cannot be scheduled if its requests exceed available resources on all nodes. It remains Pending. Priority and preemption might evict lower-priority pods to make room.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 89
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

### Question 90
[HARD]
How does the LeastRequestedPriority scoring plugin work?

A) Prefers busy nodes
B) Prefers nodes with most available resources
C) Random selection
D) Round-robin

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LeastRequestedPriority gives higher scores to nodes with more free resources (capacity minus requested). This spreads load across nodes rather than packing them.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

## Pod Priority and Preemption

### Question 91
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

### Question 92
[MEDIUM-HARD]
How do you set a Pod's priority?

A) spec.priority
B) spec.priorityClassName
C) metadata.priority
D) labels.priority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Set priority using `spec.priorityClassName` which references a PriorityClass. The actual priority value comes from the PriorityClass definition.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 93
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

### Question 94
[MEDIUM-HARD]
What is the valid range for priority values?

A) 0-100
B) Any 32-bit integer
C) 1-1000
D) Only positive numbers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Priority values can be any 32-bit integer. Higher values mean higher priority. System priorities (like system-cluster-critical) use values around 2 billion.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 95
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

### Question 96
[MEDIUM-HARD]
When does preemption occur?

A) Always
B) When a high-priority pod can't be scheduled due to resources
C) Never
D) Only manually triggered

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Preemption occurs when a pending Pod has higher priority than running pods, can't be scheduled normally, and evicting some lower-priority pods would allow it to schedule.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 97
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

### Question 98
[HARD]
What is the preemptionPolicy field?

A) Network policy
B) Controls whether pods of this class can preempt others
C) Eviction policy
D) Scheduling policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** preemptionPolicy can be PreemptLowerPriority (default, allows preemption) or Never (disables preemption for this class). Never is useful for batch jobs that shouldn't interrupt others.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 99
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

### Question 100
[HARD]
What is the system-cluster-critical PriorityClass?

A) User-defined class
B) Built-in class for critical cluster components
C) Deprecated class
D) Default class

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** system-cluster-critical is a built-in PriorityClass (priority ~2 billion) for cluster-critical components like coredns. It can run in any namespace.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 101
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

### Question 102
[HARD]
How does the scheduler choose which pods to preempt?

A) Random selection
B) Lowest priority first, minimizing preemptions
C) Oldest pods first
D) Largest pods first

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduler preempts the minimum number of lowest-priority pods needed to schedule the pending pod. It tries to minimize disruption while respecting PodDisruptionBudgets.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 103
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

### Question 104
[HARD]
Can preemption evict pods protected by PodDisruptionBudget?

A) Yes, always ignores PDB
B) No, PDB is always strictly enforced
C) PDB is supported but not guaranteed during preemption
D) Only system pods can violate PDB

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** During preemption, PodDisruptionBudget is supported but not guaranteed. The scheduler attempts to respect PDBs when selecting victims, but if no preemption candidates exist without violating PDB, preemption may still proceed. This is a best-effort consideration, not a hard constraint.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 105
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

### Question 106
[MEDIUM-HARD]
What are Pod Topology Spread Constraints?

A) Network constraints
B) Rules to spread pods evenly across topology domains
C) Security policies
D) Resource limits

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Topology spread constraints control how pods are distributed across topology domains (zones, nodes, regions) to improve availability and resource utilization.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 107
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

### Question 108
[MEDIUM-HARD]
What values can whenUnsatisfiable take?

A) Allow, Deny
B) DoNotSchedule, ScheduleAnyway
C) Required, Preferred
D) Hard, Soft

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** whenUnsatisfiable can be DoNotSchedule (don't schedule if constraint can't be met) or ScheduleAnyway (schedule but try to minimize skew).

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 109
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

### Question 110
[HARD]
What does ScheduleAnyway do in topology spread?

A) Strict enforcement
B) Schedules even if constraint violated, but still tries to minimize skew
C) Ignores constraints
D) Random scheduling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ScheduleAnyway is a soft constraint. The scheduler prioritizes nodes that minimize skew but will schedule even if maxSkew is exceeded.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 111
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

### Question 112
[HARD]
How do topology spread constraints differ from pod anti-affinity?

A) No difference
B) Spread ensures even distribution; anti-affinity just separates pods
C) Anti-affinity is better
D) Spread is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Anti-affinity only ensures pods are on different domains. Topology spread ensures EVEN distribution across domains, which is more sophisticated and useful for balanced workloads.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 113
[HARD]
Can you specify multiple topology spread constraints?

A) No, only one
B) Yes, all must be satisfied
C) Maximum of two
D) Only in namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Multiple topology spread constraints can be specified. ALL constraints must be satisfied for scheduling. This allows spreading across both zones AND nodes.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 114
[HARD]
What is minDomains in topology spread constraints?

A) Minimum nodes
B) Minimum number of eligible domains for scheduling calculation
C) Minimum skew
D) Minimum pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** minDomains specifies the minimum number of eligible domains to consider. When the number of eligible domains is less than minDomains, the global minimum is treated as 0 for skew calculation. This ensures pods spread across at least minDomains domains as they become available.

**Source:** [Pod Topology Spread Constraints | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)

</details>

---

### Question 115
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

### Question 116
[MEDIUM]
How are DaemonSet pods scheduled?

A) By user manually
B) One pod per node matching the selector
C) Random nodes
D) Only on master nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets ensure one pod runs on each node (or nodes matching nodeSelector/affinity). The DaemonSet controller creates pods for each eligible node.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 117
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

### Question 118
[MEDIUM-HARD]
How do taints affect DaemonSet scheduling?

A) Ignored completely
B) DaemonSets respect taints but have some auto-tolerations
C) DaemonSets ignore all taints
D) Only NoSchedule is respected

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets respect taints but the DaemonSet controller automatically adds NoExecute tolerations for node.kubernetes.io/not-ready and node.kubernetes.io/unreachable. This ensures DaemonSet pods aren't evicted from unhealthy nodes, which is important for monitoring and logging workloads.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 119
[HARD]
What tolerations do DaemonSets automatically get?

A) None
B) Tolerations for node.kubernetes.io/not-ready and unreachable with NoExecute
C) All tolerations
D) Only NoSchedule tolerations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSet pods automatically get tolerations for not-ready and unreachable taints (with NoExecute effect) so they continue running on problematic nodes for monitoring/logging.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 120
[MEDIUM-HARD]
Can you use nodeSelector with DaemonSets?

A) No
B) Yes, to limit which nodes get pods
C) Only with affinity
D) Only for system DaemonSets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets support nodeSelector to limit pods to specific nodes. Only nodes matching the selector get a DaemonSet pod.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 121
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

### Question 122
[HARD]
What happens when a new node joins the cluster with a DaemonSet?

A) Nothing
B) DaemonSet controller creates a pod on the new node
C) Manual intervention needed
D) Node must be labeled first

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The DaemonSet controller watches for new nodes. When a node joins and matches the selector/affinity, a new pod is automatically created for that node.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 123
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

### Question 124
[HARD]
What is the scheduling strategy for DaemonSet updates?

A) All at once
B) RollingUpdate or OnDelete
C) Blue-green
D) Canary only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSet updateStrategy can be RollingUpdate (gradually replaces pods) or OnDelete (only replaces when pod is manually deleted). RollingUpdate has maxUnavailable and maxSurge settings.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 125
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

### Question 126
[MEDIUM]
What is a static Pod?

A) A pod that never moves
B) A pod managed directly by kubelet, not the API server
C) A pod with static IP
D) A frozen pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static pods are managed directly by the kubelet on a specific node, without going through the API server. They're defined by files in a directory the kubelet watches.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 127
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

### Question 128
[MEDIUM-HARD]
Where are static Pod manifests stored?

A) In etcd
B) In a directory on the node (e.g., /etc/kubernetes/manifests)
C) In ConfigMaps
D) In the API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static pod manifests are YAML/JSON files in a directory on the node, typically /etc/kubernetes/manifests. The kubelet watches this directory.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 129
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

### Question 130
[HARD]
Can static Pods be managed by the API server?

A) Yes, fully
B) No, but mirror pods are visible in the API
C) Only for deletion
D) Only for viewing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static pods can't be managed through the API, but kubelet creates "mirror pods" in the API for visibility. These are read-only representations with status info.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 131
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

### Question 132
[HARD]
Can you delete a static Pod through the API?

A) Yes
B) No, must delete the manifest file; mirror pod will reappear
C) Only with force
D) Only as admin

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deleting a mirror pod through the API is ineffective—kubelet will recreate it. To remove a static pod, delete the manifest file from the node.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 133
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

### Question 134
[HARD]
How do you modify a static Pod?

A) kubectl edit
B) Edit the manifest file on the node
C) kubectl apply
D) API patch

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static pods can only be modified by editing the manifest file directly on the node. kubectl commands affect the mirror pod, not the actual static pod.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 135
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

### Question 136
[MEDIUM]
How do you manually schedule a Pod?

A) Use nodeSelector
B) Set spec.nodeName directly
C) Use taints
D) Label the pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting spec.nodeName directly bypasses the scheduler and places the pod on the specified node. This is manual/direct scheduling.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 137
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

### Question 138
[HARD]
Can you use nodeName with a nonexistent node?

A) Yes, pod will wait
B) Pod will be stuck in Pending with scheduling errors
C) Error at creation
D) Node is created automatically

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If nodeName references a nonexistent node, the pod is created but remains Pending. There's no node for the kubelet to run it on.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 139
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

### Question 140
[HARD]
What is the Binding API?

A) Network binding
B) API to bind a Pod to a Node programmatically
C) Volume binding
D) Service binding

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Binding API allows programmatically assigning a Pod to a Node. This is how schedulers (including custom ones) assign pods. It creates a Binding object.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 141
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

### Question 142
[MEDIUM-HARD]
What happens if you set nodeName on a pending Pod?

A) It's ignored
B) The pod is immediately scheduled to that node
C) Error occurs
D) Pod is deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Once a pod spec has nodeName, it's assigned to that node immediately (if the node exists). The pod transitions from Pending to scheduled.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 143
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

### Question 144
[HARD]
What are the use cases for manual scheduling?

A) Production workloads
B) Testing, debugging, bypassing scheduler issues
C) High availability
D) Auto-scaling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Manual scheduling (nodeName) is useful for testing, debugging scheduler issues, or running pods on specific hardware. It's not recommended for normal workloads.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 145
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

### Question 146
[MEDIUM-HARD]
Can you run multiple schedulers in Kubernetes?

A) No
B) Yes
C) Only two
D) Only in multi-cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes supports multiple schedulers running simultaneously. Pods specify which scheduler to use via schedulerName.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 147
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

### Question 148
[HARD]
What is the schedulerName field?

A) Node name
B) Name of the scheduler to handle this pod
C) Namespace
D) Label selector

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** schedulerName identifies which scheduler should place this pod. Multiple schedulers watch for pods with their name and only handle those pods.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 149
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

### Question 150
[HARD]
How do you deploy a custom scheduler?

A) Replace kube-scheduler
B) Deploy as a Deployment with appropriate RBAC
C) Cannot be deployed
D) Must modify kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deploy a custom scheduler as a Deployment (or Pod) with RBAC permissions to read pods, nodes, and create bindings. Give it a unique name.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 151
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

### Question 152
[HARD]
What permissions does a custom scheduler need?

A) None
B) Read pods, create bindings, read nodes
C) Cluster admin
D) Only pod access

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Custom schedulers need: get/list/watch pods, create bindings (in pods/binding subresource), get/list/watch nodes, and possibly other resources depending on scheduling logic.

**Source:** [Configure Multiple Schedulers | Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/)

</details>

---

### Question 153
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

### Question 154
[HARD]
What is the scheduler extender?

A) UI extension
B) Webhook to add custom filtering/scoring logic
C) Deprecated feature
D) Plugin type

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduler extenders are webhooks called during scheduling to add custom filter and score logic without modifying the scheduler code. They're configured via KubeSchedulerConfiguration.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 155
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

### Question 156
[HARD]
What is a scheduler profile?

A) User profile
B) A named configuration for the scheduler with specific plugins
C) Performance profile
D) Security profile

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduler profiles are named configurations with specific plugin settings. A single scheduler can run multiple profiles, selected via pod's schedulerName.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 157
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

### Question 158
[HARD]
How do you configure scheduler profiles?

A) kubectl
B) KubeSchedulerConfiguration YAML
C) Environment variables
D) ConfigMap only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Profiles are configured in KubeSchedulerConfiguration file under the profiles field. Each profile specifies schedulerName and plugin configurations.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 159
[HARD]
What are the scheduler extension points?

A) API endpoints
B) Stages where plugins can hook into scheduling
C) Network points
D) Storage points

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Extension points are phases in scheduling where plugins run: PreFilter, Filter, PostFilter, PreScore, Score, Reserve, Permit, PreBind, Bind, PostBind.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 160
[HARD]
What is the PreFilter extension point?

A) Post-processing
B) Preprocessing before filtering, can reject early
C) Logging
D) Caching

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PreFilter runs before Filter to do pod-level preprocessing. It can reject pods early (e.g., if a required feature isn't available anywhere) without checking every node.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 161
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

### Question 162
[HARD]
What is the PostFilter extension point?

A) Logging
B) Runs after filtering fails, used for preemption
C) Cleanup
D) Notification

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PostFilter runs when no nodes pass filtering. It's primarily used for preemption—finding lower-priority pods to evict so the pending pod can schedule.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 163
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

### Question 164
[HARD]
What is the Reserve extension point?

A) Storage reservation
B) Reserves resources on selected node before binding
C) Namespace reservation
D) IP reservation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Reserve is called after node selection but before binding. Plugins can reserve resources (like volumes or IPs) that would prevent scheduling conflicts.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 165
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

### Question 166
[HARD]
What are scheduler plugins?

A) External programs
B) Modular components implementing scheduling logic at extension points
C) UI plugins
D) Network plugins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduler plugins are modular Go components that implement scheduling logic. Each plugin can operate at one or more extension points (Filter, Score, etc.).

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 167
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

### Question 168
[HARD]
What is the NodeAffinity plugin?

A) Node health check
B) Implements node affinity/anti-affinity rules
C) Node labeling
D) Node selection

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The NodeAffinity plugin implements node affinity/anti-affinity rules. It filters nodes not matching required rules and scores based on preferred rules.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 169
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

### Question 170
[HARD]
What is the InterPodAffinity plugin?

A) Pod networking
B) Implements pod affinity and anti-affinity
C) Pod communication
D) Pod grouping

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** InterPodAffinity implements pod affinity/anti-affinity rules. It checks pod labels on nodes to determine if placement satisfies affinity constraints.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 171
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

### Question 172
[HARD]
How do you enable or disable scheduler plugins?

A) kubectl commands
B) In scheduler configuration via enabled/disabled lists
C) Environment variables
D) Cannot change

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In KubeSchedulerConfiguration, each profile has enabled/disabled plugin lists per extension point. You can enable custom plugins or disable defaults.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 173
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

### Question 174
[HARD]
Can you write custom scheduler plugins?

A) No
B) Yes, by implementing the plugin interfaces in Go
C) Only in Python
D) Only approved vendors

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Custom plugins implement Go interfaces for extension points (FilterPlugin, ScorePlugin, etc.) and are compiled into the scheduler. This requires building a custom scheduler binary.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 175
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

### Question 176
[MEDIUM]
How do you check why a Pod is Pending?

A) kubectl logs
B) kubectl describe pod
C) kubectl get events only
D) kubectl exec

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kubectl describe pod shows conditions, events, and scheduling status. Look for "Events" section with FailedScheduling reasons explaining why the pod can't be placed.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 177
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

### Question 178
[MEDIUM-HARD]
What does "Insufficient cpu" mean?

A) Node has too much CPU
B) No node has enough CPU to satisfy request
C) CPU is disabled
D) Invalid CPU value

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "Insufficient cpu" means no node has enough allocatable CPU (capacity minus existing requests) to satisfy this pod's CPU request.

**Source:** [Managing Resources for Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 179
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

### Question 180
[MEDIUM-HARD]
What does "node(s) didn't match node selector" mean?

A) Selector is empty
B) No node has labels matching the nodeSelector
C) Too many matches
D) Selector syntax error

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** No node has all the labels specified in the pod's nodeSelector. Check node labels with kubectl get nodes --show-labels.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 181
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

### Question 182
[HARD]
How do you check a node's allocatable resources?

A) kubectl get pods
B) kubectl describe node
C) kubectl top
D) kubectl logs node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kubectl describe node shows Capacity, Allocatable, and current resource usage (Allocated resources). Compare against pod requests to understand availability.

**Source:** [Managing Resources for Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 183
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

### Question 184
[HARD]
How do you simulate scheduling without actually scheduling?

A) --dry-run
B) Use scheduler's verbose logging or custom tools
C) Cannot simulate
D) kubectl simulate

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** There's no built-in simulation. Options: increase scheduler verbosity (-v=10) to see decisions, use tools like kubectl-scheduler_simulator, or manually check constraints.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 185
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

### Question 186
[HARD]
What is gang scheduling?

A) Scheduling one pod
B) Scheduling a group of pods together or not at all
C) Priority scheduling
D) Random scheduling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Gang scheduling schedules a group of pods together (all-or-nothing). If the group can't be placed entirely, none are scheduled. Used for tightly coupled workloads like MPI jobs.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 187
[HARD]
What is bin packing in scheduling?

A) Spreading pods
B) Packing pods tightly onto fewer nodes
C) Compression
D) Archiving

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bin packing maximizes utilization by filling nodes before using new ones. This reduces costs (fewer nodes needed) but may reduce resilience.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 188
[HARD]
What is spreading in scheduling?

A) Same as bin packing
B) Distributing pods across many nodes
C) Network spreading
D) Data spreading

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Spreading distributes pods across nodes for resilience. The opposite of bin packing. It improves availability but may use more nodes.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 189
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

### Question 190
[HARD]
What is the scheduling queue?

A) Network queue
B) Queue of pods waiting to be scheduled
C) Event queue
D) Message queue

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduling queue holds pods awaiting scheduling. Pods enter when created without nodeName and leave when scheduled or failed.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 191
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

### Question 192
[HARD]
What triggers a Pod to move back to the active queue?

A) Time only
B) Cluster state changes (new node, pod deleted, etc.)
C) Manual trigger
D) Never moves back

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pods move from unschedulable to active when relevant cluster changes occur: nodes added/updated, pods deleted (freeing resources), PVs available, etc.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 193
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

### Question 194
[HARD]
How does the scheduler handle volume topology?

A) Ignores volumes
B) Considers volume zone requirements when scheduling
C) Separate process
D) Only for local volumes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The VolumeBinding plugin considers volume topology constraints. For zone-specific volumes (like EBS), pods are scheduled in the same zone as the volume.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 195
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

### Question 196
[HARD]
What is the NodeVolumeLimits plugin?

A) Limits node count
B) Checks if node has reached volume attachment limits
C) Volume size limit
D) Network limit

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NodeVolumeLimits checks cloud provider volume attachment limits (e.g., AWS limits EBS volumes per instance type). It prevents scheduling if the limit would be exceeded.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 197
[HARD]
How does scheduling work with ephemeral volumes?

A) Not supported
B) Scheduler considers storage capacity and topology
C) Same as persistent
D) No scheduling needed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For ephemeral volumes (CSI ephemeral, generic ephemeral), the scheduler can consider storage capacity tracking to avoid scheduling on nodes without sufficient storage.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 198
[HARD]
What is descheduling?

A) Same as scheduling
B) Moving pods off nodes to rebalance the cluster
C) Deleting scheduler
D) Pausing scheduling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Descheduling evicts pods from nodes to rebalance workloads. Over time, cluster state can become imbalanced—descheduling corrects this by triggering rescheduling.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 199
[HARD]
What is the Kubernetes Descheduler?

A) Built-in component
B) Separate project that evicts pods to improve balance
C) Scheduler plugin
D) Deprecated tool

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Descheduler is a separate project (sigs.k8s.io/descheduler) that runs policies to evict pods. It's not built into Kubernetes and must be deployed separately.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 200
[HARD]
How do scheduling gates work?

A) Network gates
B) Block pod from scheduling until gates are removed
C) Security gates
D) Rate limiting

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduling gates (spec.schedulingGates) block a pod from being considered for scheduling until all gates are removed. External controllers can add/remove gates to control scheduling timing.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

## Summary

This question set covers Kubernetes scheduling topics essential for the KCNA certification:

- **kube-scheduler basics** (Questions 1-10)
- **Node selection and nodeSelector** (Questions 11-25)
- **Node affinity** (Questions 26-40)
- **Pod affinity and anti-affinity** (Questions 41-60)
- **Taints and tolerations** (Questions 61-80)
- **Resource requests and scheduling** (Questions 81-90)
- **Pod priority and preemption** (Questions 91-105)
- **Topology spread constraints** (Questions 106-115)
- **DaemonSet scheduling** (Questions 116-125)
- **Static pods** (Questions 126-135)
- **Manual scheduling** (Questions 136-145)
- **Multiple schedulers** (Questions 146-155)
- **Scheduler profiles and plugins** (Questions 156-175)
- **Troubleshooting** (Questions 176-185)
- **Advanced concepts** (Questions 186-200)
