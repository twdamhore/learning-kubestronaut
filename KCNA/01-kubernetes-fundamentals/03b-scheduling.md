# Scheduling - 100 MCQ Questions (Part B)

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Scheduling
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

## kube-scheduler Basics

### Question 1
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

### Question 2
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

### Question 3
[HARD]
What happens when multiple nodes have the same highest score?

A) Scheduling fails
B) The first node alphabetically is chosen
C) One is selected randomly
D) The Pod remains pending

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When multiple nodes have the same highest score, the scheduler selects one randomly. This ensures fair distribution when nodes are equally suitable.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 4
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

### Question 5
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

### Question 6
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

### Question 7
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

## nodeSelector

### Question 8
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

### Question 9
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

### Question 10
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

### Question 11
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

### Question 12
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

## Node Affinity

### Question 13
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

### Question 14
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

### Question 15
[HARD]
What does "IgnoredDuringExecution" mean in node affinity rules?

A) Rules are always enforced
B) Running Pods won't be evicted if node labels change
C) Rules are ignored after 1 hour
D) Only new Pods follow the rules

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** "IgnoredDuringExecution" means affinity rules are only checked at scheduling time. If a node's labels change after the Pod is running, the Pod won't be evicted. The Pod continues running even if it no longer satisfies the affinity rules.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity)

</details>

---

### Question 16
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

### Question 17
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

### Question 18
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

### Question 19
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

### Question 20
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

### Question 21
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

### Question 22
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

### Question 23
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

### Question 24
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

### Question 25
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

### Question 26
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

### Question 27
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

### Question 28
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

### Question 29
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

### Question 30
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

### Question 31
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

### Question 32
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

### Question 33
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

### Question 34
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

### Question 35
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

### Question 36
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

### Question 37
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

### Question 38
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

### Question 39
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

### Question 40
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

### Question 41
[MEDIUM-HARD]
What resources are typically specified for scheduling?

A) Only CPU
B) CPU and memory
C) Only memory
D) Disk and network

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CPU and memory are the most common resources for scheduling. If specified, ephemeral-storage and extended resources (like GPUs) are also considered by the scheduler. Network bandwidth is not a schedulable resource in core Kubernetes.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

---

### Question 42
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

### Question 43
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

### Question 44
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

### Question 45
[HARD]
How does the NodeResourcesFit plugin's LeastAllocated scoring strategy work?

A) Prefers busy nodes
B) Prefers nodes with most available resources
C) Random selection
D) Round-robin

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The NodeResourcesFit plugin with LeastAllocated scoring strategy gives higher scores to nodes with more free resources (capacity minus requested). This spreads load across nodes rather than packing them. (Note: "LeastRequestedPriority" is legacy terminology.)

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

## Pod Priority and Preemption

### Question 46
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

### Question 47
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

### Question 48
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

### Question 49
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

### Question 50
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

### Question 51
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

### Question 52
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

## Pod Topology Spread Constraints

### Question 53
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

### Question 54
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

### Question 55
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

### Question 56
[HARD]
How do topology spread constraints differ from pod anti-affinity?

A) No difference
B) Spread constrains skew within maxSkew; anti-affinity just separates pods
C) Anti-affinity is better
D) Spread is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Anti-affinity only ensures pods are on different domains. Topology spread constrains skew within a configurable maxSkew to keep distribution balanced across domains. Unlike anti-affinity, spread allows controlled imbalance rather than strict separation.

**Source:** [Topology Spread Constraints | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)

</details>

---

### Question 57
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

## DaemonSet Scheduling

### Question 58
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

### Question 59
[MEDIUM-HARD]
How do taints affect DaemonSet scheduling?

A) Ignored completely
B) DaemonSets respect taints but have some auto-tolerations
C) DaemonSets ignore all taints
D) Only NoSchedule is respected

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSets respect taints but the DaemonSet controller automatically adds tolerations for: not-ready and unreachable (NoExecute), plus disk-pressure, memory-pressure, pid-pressure, and unschedulable (NoSchedule). For hostNetwork pods, network-unavailable (NoSchedule) is also added. This ensures DaemonSet pods run on nodes that need monitoring/logging.

**Source:** [Taints and Tolerations | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)

</details>

---

### Question 60
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

### Question 61
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

### Question 62
[HARD]
What is the scheduling strategy for DaemonSet updates?

A) All at once
B) RollingUpdate or OnDelete
C) Blue-green
D) Canary only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DaemonSet updateStrategy can be RollingUpdate (gradually replaces pods) or OnDelete (only replaces when pod is manually deleted). RollingUpdate uses maxUnavailable to control how many pods can be unavailable during updates.

**Source:** [DaemonSet | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

</details>

---

## Static Pods

### Question 63
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

### Question 64
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

### Question 65
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

### Question 66
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

### Question 67
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

## Manual Scheduling

### Question 68
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

### Question 69
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

### Question 70
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

### Question 71
[MEDIUM-HARD]
What happens if you create a Pod with nodeName already set?

A) It's ignored and normal scheduling occurs
B) The Pod bypasses the scheduler and is assigned directly to that node
C) Error occurs
D) Pod is deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Pod is created with nodeName set, it bypasses the scheduler entirely and is assigned directly to that node (if it exists). Note: nodeName is immutable after creation—you cannot set it on an existing pending Pod. To assign an existing Pod, use the Binding API.

**Source:** [Assigning Pods to Nodes | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

</details>

---

### Question 72
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

## Multiple Schedulers

### Question 73
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

### Question 74
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

### Question 75
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

### Question 76
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

### Question 77
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

## Scheduler Profiles

### Question 78
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

### Question 79
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

### Question 80
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

### Question 81
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

### Question 82
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

## Scheduler Plugins

### Question 83
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

### Question 84
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

### Question 85
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

### Question 86
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

### Question 87
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

## Scheduling Troubleshooting

### Question 88
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

### Question 89
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

### Question 90
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

### Question 91
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

### Question 92
[HARD]
How do you simulate scheduling without actually scheduling?

A) --dry-run
B) Use scheduler's verbose logging or custom tools
C) Cannot simulate
D) kubectl simulate

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** There's no built-in dry-run for scheduling. To understand scheduling decisions: increase scheduler verbosity (-v=10), examine pod events (`kubectl describe pod`), or check scheduler logs for filtering/scoring information.

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

## Advanced Scheduling Concepts

### Question 93
[HARD]
What are scheduler profiles?

A) User account profiles
B) Named configurations with different plugins/settings for a single scheduler
C) Network profiles
D) Storage profiles

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduler profiles allow running multiple scheduling configurations within a single kube-scheduler. Each profile has a unique name and can enable/disable different plugins or configure them differently. Pods select a profile via spec.schedulerName.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 94
[HARD]
What does the LeastAllocated scoring strategy do in NodeResourcesFit?

A) Packs pods onto fewer nodes
B) Favors nodes with lower resource allocation (spread pods)
C) Ignores resource allocation
D) Only considers memory

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LeastAllocated is a scoring strategy in the NodeResourcesFit plugin that favors nodes with lower resource allocation. This spreads pods across nodes, improving resilience but potentially using more nodes.

**Source:** [Scheduler Configuration | Kubernetes](https://kubernetes.io/docs/reference/scheduling/config/)

</details>

---

### Question 95
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

### Question 96
[HARD]
What triggers a Pod to move back to the active queue?

A) Time only (backoff expiration)
B) Cluster state changes or backoff timer expiration
C) Manual trigger
D) Never moves back

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pods move back to the active queue in two ways: from the backoff queue when the backoff timer expires, or from the unschedulable queue when relevant cluster changes occur (nodes added/updated, pods deleted freeing resources, PVs available, etc.).

**Source:** [Kubernetes Scheduler | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)

</details>

---

### Question 97
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

### Question 98
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

### Question 99
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

### Question 100
[HARD]
How do scheduling gates work?

A) Network gates
B) Block pod from scheduling until gates are removed
C) Security gates
D) Rate limiting

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Scheduling gates (spec.schedulingGates) block a pod from being considered for scheduling until all gates are removed. External controllers can add/remove gates to control scheduling timing. This feature (PodSchedulingReadiness) is stable as of Kubernetes 1.27.

**Source:** [Pod Scheduling Readiness | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-scheduling-readiness/)

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