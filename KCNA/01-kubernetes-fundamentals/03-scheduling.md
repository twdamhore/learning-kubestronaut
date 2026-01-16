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

---

### Question 2
[MEDIUM]
Which component does kube-scheduler communicate with to assign Pods to nodes?

A) kubelet
B) kube-proxy
C) kube-apiserver
D) etcd directly

---

### Question 3
[MEDIUM-HARD]
What happens to a Pod if no node satisfies its scheduling requirements?

A) The Pod is deleted
B) The Pod remains in Pending state
C) The Pod is scheduled to a random node
D) The scheduler creates a new node

---

### Question 4
[MEDIUM-HARD]
In which phase does the scheduler filter out unsuitable nodes?

A) Scoring phase
B) Binding phase
C) Filtering phase
D) Preemption phase

---

### Question 5
[MEDIUM-HARD]
What is the scoring phase in the scheduling process?

A) Eliminating nodes that don't meet requirements
B) Ranking filtered nodes by preference
C) Binding the Pod to a node
D) Validating Pod specifications

---

### Question 6
[HARD]
What happens when multiple nodes have the same highest score?

A) Scheduling fails
B) The first node alphabetically is chosen
C) One is selected randomly
D) The Pod remains pending

---

### Question 7
[MEDIUM-HARD]
Which scheduling phase comes first: filtering or scoring?

A) Scoring
B) Filtering
C) They run simultaneously
D) It depends on the scheduler configuration

---

### Question 8
[MEDIUM-HARD]
What is the default scheduler name in Kubernetes?

A) kube-scheduler
B) default-scheduler
C) scheduler
D) kubernetes-scheduler

---

### Question 9
[HARD]
Can a Pod specify which scheduler should schedule it?

A) No, all Pods use the default scheduler
B) Yes, using the schedulerName field
C) Yes, using an annotation
D) Only DaemonSet Pods can specify this

---

### Question 10
[MEDIUM-HARD]
What field in a Pod spec determines which scheduler handles it?

A) spec.scheduler
B) spec.schedulerName
C) metadata.scheduler
D) spec.nodeName

---

## Node Selection

### Question 11
[MEDIUM]
What is the simplest way to schedule a Pod to a specific node?

A) nodeSelector
B) nodeName
C) nodeAffinity
D) taints

---

### Question 12
[MEDIUM-HARD]
What happens if you specify a nodeName that doesn't exist?

A) The Pod is scheduled to a random node
B) The Pod remains in Pending state
C) The scheduler creates the node
D) The Pod fails immediately

---

### Question 13
[MEDIUM-HARD]
Does nodeName bypass the scheduler?

A) No, the scheduler still validates
B) Yes, completely
C) Only for system Pods
D) Only if the node exists

---

### Question 14
[HARD]
What are the limitations of using nodeName for scheduling?

A) It only works with StatefulSets
B) It bypasses scheduling constraints and can fail if node doesn't exist
C) It requires admin privileges
D) It can only be used once per node

---

### Question 15
[MEDIUM-HARD]
Can nodeName be changed after a Pod is created?

A) Yes, using kubectl edit
B) No, it is immutable
C) Only by an admin
D) Yes, but requires restart

---

## nodeSelector

### Question 16
[MEDIUM]
What is a nodeSelector?

A) A way to select containers
B) A simple label-based node selection mechanism
C) A network policy
D) A resource quota

---

### Question 17
[MEDIUM]
Where is nodeSelector specified in a Pod definition?

A) metadata.nodeSelector
B) spec.nodeSelector
C) spec.template.nodeSelector
D) spec.containers.nodeSelector

---

### Question 18
[MEDIUM-HARD]
What type of matching does nodeSelector use?

A) Regex matching
B) Exact equality matching
C) Prefix matching
D) Wildcard matching

---

### Question 19
[MEDIUM-HARD]
What happens if no nodes match the nodeSelector labels?

A) The Pod is scheduled randomly
B) The Pod remains Pending
C) The Pod fails
D) Labels are created automatically

---

### Question 20
[MEDIUM-HARD]
Can you use multiple labels in a nodeSelector?

A) No, only one label is allowed
B) Yes, and all must match (AND logic)
C) Yes, any can match (OR logic)
D) Only with node affinity

---

### Question 21
[HARD]
What is the relationship between nodeSelector and node affinity?

A) They are mutually exclusive
B) nodeSelector is a simpler form of node affinity
C) nodeSelector overrides node affinity
D) They cannot be used on the same Pod

---

### Question 22
[MEDIUM-HARD]
How do you label a node for use with nodeSelector?

A) kubectl label pods
B) kubectl label nodes node-name key=value
C) kubectl annotate nodes
D) kubectl taint nodes

---

### Question 23
[MEDIUM-HARD]
Are nodeSelector labels case-sensitive?

A) No
B) Yes
C) Only the key is case-sensitive
D) Only the value is case-sensitive

---

### Question 24
[MEDIUM-HARD]
Can nodeSelector use inequality operators?

A) Yes, using != syntax
B) No, only equality matching
C) Yes, using NotIn
D) Only with expressions

---

### Question 25
[HARD]
What built-in labels are available on nodes for scheduling?

A) Only custom labels
B) kubernetes.io/hostname, topology.kubernetes.io/zone, etc.
C) Only node-role labels
D) No built-in labels exist

---

## Node Affinity

### Question 26
[MEDIUM]
What is node affinity?

A) A way to reject nodes
B) An expressive way to constrain Pod placement on nodes
C) A node health metric
D) A network policy

---

### Question 27
[MEDIUM-HARD]
What are the two types of node affinity?

A) hard and soft
B) required and preferred
C) strict and relaxed
D) mandatory and optional

---

### Question 28
[MEDIUM-HARD]
What does requiredDuringSchedulingIgnoredDuringExecution mean?

A) Required at all times
B) Must match at scheduling, ignored if node changes later
C) Only checked during execution
D) Never required

---

### Question 29
[MEDIUM-HARD]
What does preferredDuringSchedulingIgnoredDuringExecution mean?

A) Strictly required
B) Preferred but not mandatory at scheduling
C) Ignored completely
D) Only for preferred nodes

---

### Question 30
[HARD]
What does "IgnoredDuringExecution" mean in node affinity rules?

A) Rules are always enforced
B) Running Pods won't be evicted if node labels change
C) Rules are ignored after 1 hour
D) Only new Pods follow the rules

---

### Question 31
[MEDIUM-HARD]
Which operators are available in node affinity expressions?

A) Only In and NotIn
B) In, NotIn, Exists, DoesNotExist, Gt, Lt
C) Equals and NotEquals only
D) Only Exists

---

### Question 32
[MEDIUM-HARD]
What does the In operator do in node affinity?

A) Checks if key is in a list
B) Checks if label value is in a list of values
C) Includes all nodes
D) Checks string contains

---

### Question 33
[MEDIUM-HARD]
What does the NotIn operator do in node affinity?

A) Excludes all nodes
B) Checks label value is not in the list
C) Removes labels
D) Negates the entire rule

---

### Question 34
[MEDIUM-HARD]
What does the Exists operator do in node affinity?

A) Checks if value exists
B) Checks if label key exists regardless of value
C) Checks if node exists
D) Creates the label if missing

---

### Question 35
[MEDIUM-HARD]
What does the DoesNotExist operator do in node affinity?

A) Deletes the label
B) Matches nodes that don't have the label key
C) Fails if label doesn't exist
D) Creates missing nodes

---

### Question 36
[HARD]
What do the Gt and Lt operators do in node affinity?

A) String comparison
B) Numeric comparison (greater than, less than)
C) Time comparison
D) Size comparison

---

### Question 37
[MEDIUM-HARD]
How do you specify weight for preferred node affinity?

A) Using priority field
B) Using weight field (1-100)
C) Using score field
D) Weights are automatic

---

### Question 38
[HARD]
What is the valid range for node affinity weights?

A) 0-100
B) 1-100
C) 1-1000
D) Any positive integer

---

### Question 39
[HARD]
How are multiple node affinity terms combined?

A) AND logic
B) OR logic
C) XOR logic
D) Only one term is evaluated

---

### Question 40
[HARD]
How are multiple matchExpressions within a term combined?

A) OR logic
B) AND logic
C) Randomly selected
D) First match wins

---

## Pod Affinity

### Question 41
[MEDIUM]
What is pod affinity?

A) Attracting nodes to pods
B) Scheduling pods near other pods with specific labels
C) Pod health checking
D) Pod networking

---

### Question 42
[MEDIUM-HARD]
What is the topologyKey in pod affinity?

A) A pod label
B) A node label key that defines the topology domain
C) A namespace
D) A container name

---

### Question 43
[MEDIUM-HARD]
What is a common topologyKey value?

A) pod.name
B) kubernetes.io/hostname
C) container.id
D) app.version

---

### Question 44
[MEDIUM-HARD]
What does pod affinity's requiredDuringSchedulingIgnoredDuringExecution do?

A) Optional matching
B) Must schedule near matching pods
C) Ignore all pods
D) Execute immediately

---

### Question 45
[HARD]
Can pod affinity reference pods in other namespaces?

A) No, never
B) Yes, using namespaces or namespaceSelector
C) Only system namespaces
D) Only with admin rights

---

### Question 46
[MEDIUM-HARD]
What is the labelSelector in pod affinity used for?

A) Selecting nodes
B) Selecting which pods to be near/avoid
C) Selecting containers
D) Selecting namespaces

---

### Question 47
[HARD]
What happens if topologyKey is set to kubernetes.io/hostname?

A) Pods are spread across hosts
B) Pods must be on the same node as matching pods
C) Hostname is ignored
D) Only one pod per cluster

---

### Question 48
[HARD]
What is the performance impact of pod affinity rules?

A) No impact
B) Can significantly slow scheduling in large clusters
C) Improves performance
D) Only affects networking

---

### Question 49
[MEDIUM-HARD]
Can you combine pod affinity with node affinity?

A) No, they conflict
B) Yes, both are evaluated
C) Only one can be active
D) Only in StatefulSets

---

### Question 50
[HARD]
What is the namespaceSelector field in pod affinity?

A) Selects namespace for the pod
B) Matches namespaces containing pods to consider
C) Creates namespaces
D) Deletes namespaces

---

## Pod Anti-Affinity

### Question 51
[MEDIUM]
What is pod anti-affinity?

A) Pods that hate each other
B) Scheduling pods away from pods with specific labels
C) Removing pod labels
D) Deleting pods

---

### Question 52
[MEDIUM-HARD]
When would you use pod anti-affinity?

A) To group pods together
B) To spread replicas across nodes for high availability
C) To speed up scheduling
D) To reduce costs

---

### Question 53
[MEDIUM-HARD]
How do you specify pod anti-affinity in a Pod spec?

A) spec.antiAffinity
B) spec.affinity.podAntiAffinity
C) spec.nodeAntiAffinity
D) metadata.antiAffinity

---

### Question 54
[HARD]
What is the difference between required and preferred anti-affinity?

A) No difference
B) Required must be satisfied; preferred is best-effort
C) Preferred is stronger
D) Required is deprecated

---

### Question 55
[MEDIUM-HARD]
Can pod anti-affinity use the same operators as pod affinity?

A) No, different operators
B) Yes, same labelSelector operators
C) Only Exists
D) Only In

---

### Question 56
[HARD]
What happens when anti-affinity conflicts with other scheduling constraints?

A) Anti-affinity always wins
B) Pod may remain pending if no valid node exists
C) Constraints are ignored
D) Random node selected

---

### Question 57
[HARD]
How does anti-affinity affect Deployment rollouts?

A) No effect
B) May slow rollouts if nodes are limited
C) Speeds up rollouts
D) Prevents rollouts

---

### Question 58
[MEDIUM-HARD]
What topologyKey would spread pods across availability zones?

A) kubernetes.io/hostname
B) topology.kubernetes.io/zone
C) node.kubernetes.io/zone
D) cluster.zone

---

### Question 59
[HARD]
Can anti-affinity reference pods from the same Deployment?

A) No, only other deployments
B) Yes, using matching labels
C) Only StatefulSets
D) Only with special annotation

---

### Question 60
[HARD]
What are the limitations of pod anti-affinity?

A) None
B) Performance impact, requires topologyKey, complexity
C) Only works with 3+ nodes
D) Cannot use with DaemonSets

---

## Taints and Tolerations

### Question 61
[MEDIUM]
What is a taint in Kubernetes?

A) A security vulnerability
B) A property on nodes that repels pods
C) A pod label
D) A network policy

---

### Question 62
[MEDIUM]
What is a toleration?

A) A node property
B) A pod property that allows scheduling on tainted nodes
C) A security setting
D) A network rule

---

### Question 63
[MEDIUM-HARD]
What are the three taint effects?

A) Allow, Deny, Maybe
B) NoSchedule, PreferNoSchedule, NoExecute
C) Hard, Soft, Medium
D) Block, Warn, Pass

---

### Question 64
[MEDIUM-HARD]
What does the NoSchedule effect do?

A) Schedules pods normally
B) Prevents new pods without toleration from scheduling
C) Removes all pods
D) Only affects system pods

---

### Question 65
[MEDIUM-HARD]
What does the PreferNoSchedule effect do?

A) Strictly prevents scheduling
B) Tries to avoid scheduling but allows if necessary
C) Same as NoSchedule
D) Only for preferred pods

---

### Question 66
[MEDIUM-HARD]
What does the NoExecute effect do?

A) Only affects new pods
B) Evicts running pods without toleration and prevents new ones
C) Executes pods immediately
D) Disables pod execution

---

### Question 67
[MEDIUM-HARD]
How do you add a taint to a node?

A) kubectl label node
B) kubectl taint nodes node-name key=value:effect
C) kubectl annotate node
D) kubectl apply taint

---

### Question 68
[MEDIUM-HARD]
How do you remove a taint from a node?

A) kubectl taint nodes node-name key:effect-
B) kubectl untaint node
C) kubectl remove taint
D) kubectl delete taint

---

### Question 69
[MEDIUM-HARD]
Where are tolerations specified?

A) On nodes
B) In Pod spec under tolerations
C) In namespace
D) In ConfigMap

---

### Question 70
[HARD]
What operators are available for tolerations?

A) Only Equal
B) Equal and Exists
C) In, NotIn, Exists
D) All comparison operators

---

### Question 71
[MEDIUM-HARD]
What does the Equal operator do in tolerations?

A) Matches any taint
B) Matches taint with same key and value
C) Checks equality of nodes
D) Compares pod names

---

### Question 72
[MEDIUM-HARD]
What does the Exists operator do in tolerations?

A) Checks if pod exists
B) Matches taint by key only, regardless of value
C) Creates missing taints
D) Validates node existence

---

### Question 73
[HARD]
How do you tolerate all taints on a node?

A) Cannot be done
B) Use empty key with Exists operator
C) Use wildcard *
D) Set toleration to "all"

---

### Question 74
[HARD]
What is tolerationSeconds used for?

A) Timeout for scheduling
B) Time to remain on node with NoExecute taint before eviction
C) Scheduling delay
D) Taint duration

---

### Question 75
[MEDIUM-HARD]
What built-in taints does Kubernetes add automatically?

A) None
B) node.kubernetes.io/not-ready, unreachable, memory-pressure, etc.
C) Only custom taints
D) Only on master nodes

---

### Question 76
[HARD]
What is the node.kubernetes.io/not-ready taint?

A) Manual taint
B) Auto-added when node is not ready
C) For new nodes only
D) Deprecated taint

---

### Question 77
[HARD]
What is the node.kubernetes.io/unreachable taint?

A) For offline nodes
B) Auto-added when node controller can't reach the node
C) Manual taint
D) Network policy

---

### Question 78
[HARD]
How do taints and tolerations differ from node affinity?

A) No difference
B) Taints repel pods; affinity attracts pods
C) Taints are for nodes; affinity is for pods
D) They are mutually exclusive

---

### Question 79
[MEDIUM-HARD]
Can a Pod tolerate multiple taints?

A) No, only one
B) Yes, by specifying multiple tolerations
C) Only two
D) Only with special flag

---

### Question 80
[HARD]
What happens to running pods when a NoExecute taint is added?

A) Nothing
B) Pods without matching toleration are evicted
C) All pods are evicted
D) Only new pods are affected

---

## Resource Requests and Scheduling

### Question 81
[MEDIUM]
How do resource requests affect scheduling?

A) They don't affect scheduling
B) Scheduler uses requests to find nodes with sufficient resources
C) Only limits matter
D) Resources are ignored

---

### Question 82
[MEDIUM-HARD]
What resources are typically specified for scheduling?

A) Only CPU
B) CPU and memory
C) Only memory
D) Disk and network

---

### Question 83
[MEDIUM-HARD]
What happens if no node has enough resources for a Pod's requests?

A) Pod is scheduled anyway
B) Pod remains Pending
C) Resources are borrowed
D) Node is scaled up

---

### Question 84
[MEDIUM-HARD]
Does the scheduler consider resource limits or requests?

A) Only limits
B) Only requests
C) Both equally
D) Neither

---

### Question 85
[HARD]
What is the allocatable capacity of a node?

A) Total hardware resources
B) Resources available for pods after system reservations
C) Maximum pod count
D) Network bandwidth

---

### Question 86
[MEDIUM-HARD]
How is allocatable different from total capacity?

A) They are the same
B) Allocatable = Capacity - reserved for system
C) Allocatable is always higher
D) Allocatable is for storage only

---

### Question 87
[HARD]
What resources are reserved for system components?

A) None
B) kube-reserved and system-reserved (CPU, memory, etc.)
C) Only memory
D) Only disk

---

### Question 88
[MEDIUM-HARD]
Can a Pod be scheduled if it exceeds available resources?

A) Yes, always
B) No, it will remain Pending
C) Only with priority
D) Only system pods

---

### Question 89
[HARD]
What is resource overcommitment?

A) Using more resources than requested
B) Scheduling pods whose total requests exceed node capacity
C) Requesting infinite resources
D) Resource sharing

---

### Question 90
[HARD]
How does the LeastRequestedPriority scoring plugin work?

A) Prefers busy nodes
B) Prefers nodes with most available resources
C) Random selection
D) Round-robin

---

## Pod Priority and Preemption

### Question 91
[MEDIUM]
What is Pod priority?

A) Network priority
B) A value determining scheduling and eviction order
C) CPU priority
D) Start order

---

### Question 92
[MEDIUM-HARD]
How do you set a Pod's priority?

A) spec.priority
B) spec.priorityClassName
C) metadata.priority
D) labels.priority

---

### Question 93
[MEDIUM-HARD]
What is a PriorityClass?

A) A pod label
B) A cluster resource defining priority value and settings
C) A node type
D) A namespace

---

### Question 94
[MEDIUM-HARD]
What is the valid range for priority values?

A) 0-100
B) Any 32-bit integer
C) 1-1000
D) Only positive numbers

---

### Question 95
[HARD]
What does preemption mean in Kubernetes scheduling?

A) Scheduling faster
B) Evicting lower-priority pods to schedule higher-priority ones
C) Preventing scheduling
D) Priority inversion

---

### Question 96
[MEDIUM-HARD]
When does preemption occur?

A) Always
B) When a high-priority pod can't be scheduled due to resources
C) Never
D) Only manually triggered

---

### Question 97
[HARD]
Can preemption be disabled for a PriorityClass?

A) No
B) Yes, using preemptionPolicy: Never
C) Only for system classes
D) Only temporarily

---

### Question 98
[HARD]
What is the preemptionPolicy field?

A) Network policy
B) Controls whether pods of this class can preempt others
C) Eviction policy
D) Scheduling policy

---

### Question 99
[MEDIUM-HARD]
What is the default priority for pods without a PriorityClass?

A) 0
B) -1
C) 100
D) Highest

---

### Question 100
[HARD]
What is the system-cluster-critical PriorityClass?

A) User-defined class
B) Built-in class for critical cluster components
C) Deprecated class
D) Default class

---

### Question 101
[HARD]
What is the system-node-critical PriorityClass?

A) For user pods
B) For critical node-level components, higher than cluster-critical
C) Same as system-cluster-critical
D) Deprecated

---

### Question 102
[HARD]
How does the scheduler choose which pods to preempt?

A) Random selection
B) Lowest priority first, minimizing preemptions
C) Oldest pods first
D) Largest pods first

---

### Question 103
[MEDIUM-HARD]
What is the globalDefault field in PriorityClass?

A) Sets global timeout
B) Makes this class the default for pods without priorityClassName
C) Applies to all clusters
D) Default namespace

---

### Question 104
[HARD]
Can preemption evict pods protected by PodDisruptionBudget?

A) Yes, always
B) No, PDB is respected
C) Only for critical pods
D) PDB is ignored during preemption

---

### Question 105
[HARD]
What happens to preempted pods?

A) They are deleted permanently
B) They receive SIGTERM and are gracefully terminated
C) They are paused
D) They move to another node automatically

---

## Pod Topology Spread Constraints

### Question 106
[MEDIUM-HARD]
What are Pod Topology Spread Constraints?

A) Network constraints
B) Rules to spread pods evenly across topology domains
C) Security policies
D) Resource limits

---

### Question 107
[MEDIUM-HARD]
What is maxSkew in topology spread?

A) Maximum pods per node
B) Maximum difference in pod count between domains
C) Network latency
D) CPU imbalance

---

### Question 108
[MEDIUM-HARD]
What values can whenUnsatisfiable take?

A) Allow, Deny
B) DoNotSchedule, ScheduleAnyway
C) Required, Preferred
D) Hard, Soft

---

### Question 109
[HARD]
What does DoNotSchedule do in topology spread?

A) Allows scheduling
B) Prevents scheduling if constraint can't be satisfied
C) Deletes pods
D) Ignores constraint

---

### Question 110
[HARD]
What does ScheduleAnyway do in topology spread?

A) Strict enforcement
B) Schedules even if constraint violated, but still tries to minimize skew
C) Ignores constraints
D) Random scheduling

---

### Question 111
[MEDIUM-HARD]
What is topologyKey in topology spread constraints?

A) Pod label
B) Node label key defining topology domains
C) Namespace
D) Container name

---

### Question 112
[HARD]
How do topology spread constraints differ from pod anti-affinity?

A) No difference
B) Spread ensures even distribution; anti-affinity just separates pods
C) Anti-affinity is better
D) Spread is deprecated

---

### Question 113
[HARD]
Can you specify multiple topology spread constraints?

A) No, only one
B) Yes, all must be satisfied
C) Maximum of two
D) Only in namespaces

---

### Question 114
[HARD]
What is minDomains in topology spread constraints?

A) Minimum nodes
B) Minimum number of domains that must have matching pods
C) Minimum skew
D) Minimum pods

---

### Question 115
[HARD]
How does the scheduler calculate skew?

A) Random
B) Max pods in domain minus min pods in domain
C) Average minus min
D) Total divided by domains

---

## DaemonSet Scheduling

### Question 116
[MEDIUM]
How are DaemonSet pods scheduled?

A) By user manually
B) One pod per node matching the selector
C) Random nodes
D) Only on master nodes

---

### Question 117
[MEDIUM-HARD]
Does DaemonSet use the default scheduler?

A) No, never
B) Yes, by default
C) Uses custom scheduler
D) Kubelet schedules directly

---

### Question 118
[MEDIUM-HARD]
How do taints affect DaemonSet scheduling?

A) Ignored completely
B) DaemonSets respect taints but have some auto-tolerations
C) DaemonSets ignore all taints
D) Only NoSchedule is respected

---

### Question 119
[HARD]
What tolerations do DaemonSets automatically get?

A) None
B) Tolerations for node.kubernetes.io/not-ready and unreachable with NoExecute
C) All tolerations
D) Only NoSchedule tolerations

---

### Question 120
[MEDIUM-HARD]
Can you use nodeSelector with DaemonSets?

A) No
B) Yes, to limit which nodes get pods
C) Only with affinity
D) Only for system DaemonSets

---

### Question 121
[MEDIUM-HARD]
Can you use node affinity with DaemonSets?

A) No
B) Yes
C) Only required affinity
D) Only preferred affinity

---

### Question 122
[HARD]
What happens when a new node joins the cluster with a DaemonSet?

A) Nothing
B) DaemonSet controller creates a pod on the new node
C) Manual intervention needed
D) Node must be labeled first

---

### Question 123
[MEDIUM-HARD]
How do you prevent a DaemonSet from scheduling on specific nodes?

A) Cannot be done
B) Use nodeSelector, node affinity, or taints
C) Delete the nodes
D) Disable the DaemonSet

---

### Question 124
[HARD]
What is the scheduling strategy for DaemonSet updates?

A) All at once
B) RollingUpdate or OnDelete
C) Blue-green
D) Canary only

---

### Question 125
[HARD]
How do DaemonSets handle unschedulable nodes?

A) Skip them
B) They schedule anyway if no conflicting taints
C) Create new nodes
D) Wait indefinitely

---

## Static Pods

### Question 126
[MEDIUM]
What is a static Pod?

A) A pod that never moves
B) A pod managed directly by kubelet, not the API server
C) A pod with static IP
D) A frozen pod

---

### Question 127
[MEDIUM-HARD]
Who manages static Pods?

A) kube-scheduler
B) kubelet on the node
C) kube-controller-manager
D) etcd

---

### Question 128
[MEDIUM-HARD]
Where are static Pod manifests stored?

A) In etcd
B) In a directory on the node (e.g., /etc/kubernetes/manifests)
C) In ConfigMaps
D) In the API server

---

### Question 129
[MEDIUM-HARD]
How does kubelet discover static Pod manifests?

A) API server notifies it
B) Watches a configured directory (staticPodPath)
C) Manual reload required
D) Through etcd

---

### Question 130
[HARD]
Can static Pods be managed by the API server?

A) Yes, fully
B) No, but mirror pods are visible in the API
C) Only for deletion
D) Only for viewing

---

### Question 131
[MEDIUM-HARD]
What is a mirror Pod?

A) A backup pod
B) A read-only API representation of a static pod
C) A replicated pod
D) A shadow container

---

### Question 132
[HARD]
Can you delete a static Pod through the API?

A) Yes
B) No, must delete the manifest file; mirror pod will reappear
C) Only with force
D) Only as admin

---

### Question 133
[MEDIUM-HARD]
What control plane components run as static Pods?

A) None
B) kube-apiserver, kube-controller-manager, kube-scheduler, etcd
C) Only etcd
D) Only kube-proxy

---

### Question 134
[HARD]
How do you modify a static Pod?

A) kubectl edit
B) Edit the manifest file on the node
C) kubectl apply
D) API patch

---

### Question 135
[HARD]
What happens if a static Pod manifest is deleted?

A) Pod continues running
B) Kubelet terminates the pod
C) Pod becomes orphaned
D) Nothing until reboot

---

## Manual Scheduling

### Question 136
[MEDIUM]
How do you manually schedule a Pod?

A) Use nodeSelector
B) Set spec.nodeName directly
C) Use taints
D) Label the pod

---

### Question 137
[MEDIUM-HARD]
What field is used for manual scheduling?

A) spec.scheduler
B) spec.nodeName
C) spec.node
D) spec.target

---

### Question 138
[HARD]
Can you use nodeName with a nonexistent node?

A) Yes, pod will wait
B) Pod will be stuck in Pending with scheduling errors
C) Error at creation
D) Node is created automatically

---

### Question 139
[MEDIUM-HARD]
Does manual scheduling bypass admission controllers?

A) Yes, completely
B) No, admission controllers still run
C) Only some controllers
D) Depends on configuration

---

### Question 140
[HARD]
What is the Binding API?

A) Network binding
B) API to bind a Pod to a Node programmatically
C) Volume binding
D) Service binding

---

### Question 141
[HARD]
How can you create a custom scheduler?

A) Modify kube-scheduler code
B) Write a program that watches pods and creates Bindings
C) Only through plugins
D) Cannot be done

---

### Question 142
[MEDIUM-HARD]
What happens if you set nodeName on a pending Pod?

A) It's ignored
B) The pod is immediately scheduled to that node
C) Error occurs
D) Pod is deleted

---

### Question 143
[HARD]
Can you change nodeName after Pod creation?

A) Yes, with kubectl edit
B) No, nodeName is immutable after scheduling
C) Only for running pods
D) Only with admin rights

---

### Question 144
[HARD]
What are the use cases for manual scheduling?

A) Production workloads
B) Testing, debugging, bypassing scheduler issues
C) High availability
D) Auto-scaling

---

### Question 145
[MEDIUM-HARD]
Does nodeName respect taints?

A) Yes
B) No, nodeName bypasses taint checks
C) Only NoSchedule
D) Only NoExecute

---

## Multiple Schedulers

### Question 146
[MEDIUM-HARD]
Can you run multiple schedulers in Kubernetes?

A) No
B) Yes
C) Only two
D) Only in multi-cluster

---

### Question 147
[MEDIUM-HARD]
How do you specify which scheduler should schedule a Pod?

A) spec.scheduler
B) spec.schedulerName
C) metadata.scheduler
D) annotation

---

### Question 148
[HARD]
What is the schedulerName field?

A) Node name
B) Name of the scheduler to handle this pod
C) Namespace
D) Label selector

---

### Question 149
[HARD]
What happens if the specified scheduler doesn't exist?

A) Default scheduler takes over
B) Pod remains Pending indefinitely
C) Pod fails
D) Error at creation

---

### Question 150
[HARD]
How do you deploy a custom scheduler?

A) Replace kube-scheduler
B) Deploy as a Deployment with appropriate RBAC
C) Cannot be deployed
D) Must modify kubelet

---

### Question 151
[HARD]
Can multiple schedulers compete for the same Pod?

A) Yes
B) No, only one scheduler is specified per pod
C) Sometimes
D) Only with locks

---

### Question 152
[HARD]
What permissions does a custom scheduler need?

A) None
B) Read pods, create bindings, read nodes
C) Cluster admin
D) Only pod access

---

### Question 153
[HARD]
How do you configure scheduler leader election?

A) Not needed
B) Via --leader-elect flag and lease objects
C) Manual configuration
D) Automatic only

---

### Question 154
[HARD]
What is the scheduler extender?

A) UI extension
B) Webhook to add custom filtering/scoring logic
C) Deprecated feature
D) Plugin type

---

### Question 155
[HARD]
How do scheduler plugins differ from extenders?

A) Same thing
B) Plugins are compiled in; extenders are external webhooks
C) Extenders are faster
D) Plugins are deprecated

---

## Scheduler Profiles

### Question 156
[HARD]
What is a scheduler profile?

A) User profile
B) A named configuration for the scheduler with specific plugins
C) Performance profile
D) Security profile

---

### Question 157
[HARD]
Can a single scheduler run multiple profiles?

A) No
B) Yes, pods select profile via schedulerName
C) Maximum two
D) Only in clusters

---

### Question 158
[HARD]
How do you configure scheduler profiles?

A) kubectl
B) KubeSchedulerConfiguration YAML
C) Environment variables
D) ConfigMap only

---

### Question 159
[HARD]
What are the scheduler extension points?

A) API endpoints
B) Stages where plugins can hook into scheduling
C) Network points
D) Storage points

---

### Question 160
[HARD]
What is the PreFilter extension point?

A) Post-processing
B) Preprocessing before filtering, can reject early
C) Logging
D) Caching

---

### Question 161
[HARD]
What is the Filter extension point?

A) Network filtering
B) Determines which nodes are feasible for the pod
C) Log filtering
D) Event filtering

---

### Question 162
[HARD]
What is the PostFilter extension point?

A) Logging
B) Runs after filtering fails, used for preemption
C) Cleanup
D) Notification

---

### Question 163
[HARD]
What is the Score extension point?

A) Game scoring
B) Ranks feasible nodes by preference
C) Health scoring
D) Priority scoring

---

### Question 164
[HARD]
What is the Reserve extension point?

A) Storage reservation
B) Reserves resources on selected node before binding
C) Namespace reservation
D) IP reservation

---

### Question 165
[HARD]
What is the Bind extension point?

A) Network binding
B) Actually binds the pod to the node
C) Volume binding only
D) Service binding

---

## Scheduler Plugins

### Question 166
[HARD]
What are scheduler plugins?

A) External programs
B) Modular components implementing scheduling logic at extension points
C) UI plugins
D) Network plugins

---

### Question 167
[HARD]
What is the NodeResourcesFit plugin?

A) Resizes nodes
B) Checks if node has enough resources for pod
C) Balances resources
D) Limits resources

---

### Question 168
[HARD]
What is the NodeAffinity plugin?

A) Node health check
B) Implements node affinity/anti-affinity rules
C) Node labeling
D) Node selection

---

### Question 169
[HARD]
What is the PodTopologySpread plugin?

A) Network topology
B) Implements topology spread constraints
C) Pod distribution
D) Zone management

---

### Question 170
[HARD]
What is the InterPodAffinity plugin?

A) Pod networking
B) Implements pod affinity and anti-affinity
C) Pod communication
D) Pod grouping

---

### Question 171
[HARD]
What is the TaintToleration plugin?

A) Adds taints
B) Filters nodes based on taints and pod tolerations
C) Removes taints
D) Validates tolerations

---

### Question 172
[HARD]
How do you enable or disable scheduler plugins?

A) kubectl commands
B) In scheduler configuration via enabled/disabled lists
C) Environment variables
D) Cannot change

---

### Question 173
[HARD]
What is the default set of enabled plugins?

A) None
B) NodeResourcesFit, NodeAffinity, TaintToleration, and many others
C) Only NodeResourcesFit
D) All plugins

---

### Question 174
[HARD]
Can you write custom scheduler plugins?

A) No
B) Yes, by implementing the plugin interfaces in Go
C) Only in Python
D) Only approved vendors

---

### Question 175
[HARD]
What is the scheduler framework?

A) UI framework
B) The plugin-based architecture for kube-scheduler
C) Network framework
D) Testing framework

---

## Scheduling Troubleshooting

### Question 176
[MEDIUM]
How do you check why a Pod is Pending?

A) kubectl logs
B) kubectl describe pod
C) kubectl get events only
D) kubectl exec

---

### Question 177
[MEDIUM-HARD]
What events indicate scheduling failures?

A) Started events
B) FailedScheduling events
C) Killed events
D) Created events

---

### Question 178
[MEDIUM-HARD]
What does "Insufficient cpu" mean?

A) Node has too much CPU
B) No node has enough CPU to satisfy request
C) CPU is disabled
D) Invalid CPU value

---

### Question 179
[MEDIUM-HARD]
What does "node(s) had taint that pod didn't tolerate" mean?

A) Node has no taints
B) Pod lacks toleration for node's taint
C) Taint is invalid
D) Pod has too many tolerations

---

### Question 180
[MEDIUM-HARD]
What does "node(s) didn't match node selector" mean?

A) Selector is empty
B) No node has labels matching the nodeSelector
C) Too many matches
D) Selector syntax error

---

### Question 181
[HARD]
How do you debug node affinity issues?

A) Check pod events only
B) Compare pod's affinity rules with node labels
C) Restart scheduler
D) Delete affinity

---

### Question 182
[HARD]
How do you check a node's allocatable resources?

A) kubectl get pods
B) kubectl describe node
C) kubectl top
D) kubectl logs node

---

### Question 183
[MEDIUM-HARD]
What does "0/3 nodes are available" mean?

A) Cluster has no nodes
B) No nodes passed the filter phase
C) All nodes are ready
D) Three nodes are pending

---

### Question 184
[HARD]
How do you simulate scheduling without actually scheduling?

A) --dry-run
B) Use scheduler's verbose logging or custom tools
C) Cannot simulate
D) kubectl simulate

---

### Question 185
[HARD]
What is the scheduler's verbose logging?

A) Disabled by default
B) Detailed logs at higher verbosity levels (-v=10)
C) Separate log file
D) UI dashboard

---

## Advanced Scheduling Concepts

### Question 186
[HARD]
What is gang scheduling?

A) Scheduling one pod
B) Scheduling a group of pods together or not at all
C) Priority scheduling
D) Random scheduling

---

### Question 187
[HARD]
What is bin packing in scheduling?

A) Spreading pods
B) Packing pods tightly onto fewer nodes
C) Compression
D) Archiving

---

### Question 188
[HARD]
What is spreading in scheduling?

A) Same as bin packing
B) Distributing pods across many nodes
C) Network spreading
D) Data spreading

---

### Question 189
[HARD]
How does the scheduler handle pod overhead?

A) Ignores it
B) Includes overhead in resource calculations
C) Separate scheduling
D) Only for VMs

---

### Question 190
[HARD]
What is the scheduling queue?

A) Network queue
B) Queue of pods waiting to be scheduled
C) Event queue
D) Message queue

---

### Question 191
[HARD]
What are the sub-queues in the scheduling queue?

A) Only one queue
B) Active, backoff, and unschedulable queues
C) Priority queues only
D) FIFO only

---

### Question 192
[HARD]
What triggers a Pod to move back to the active queue?

A) Time only
B) Cluster state changes (new node, pod deleted, etc.)
C) Manual trigger
D) Never moves back

---

### Question 193
[HARD]
What is the nominated node?

A) Preferred node
B) Node where pod will be scheduled after preemption completes
C) Random node
D) Backup node

---

### Question 194
[HARD]
How does the scheduler handle volume topology?

A) Ignores volumes
B) Considers volume zone requirements when scheduling
C) Separate process
D) Only for local volumes

---

### Question 195
[HARD]
What is delayed binding for volumes?

A) Instant binding
B) Wait to bind PVC until pod is scheduled
C) Never bind
D) Manual binding

---

### Question 196
[HARD]
What is the NodeVolumeLimits plugin?

A) Limits node count
B) Checks if node has reached volume attachment limits
C) Volume size limit
D) Network limit

---

### Question 197
[HARD]
How does scheduling work with ephemeral volumes?

A) Not supported
B) Scheduler considers storage capacity and topology
C) Same as persistent
D) No scheduling needed

---

### Question 198
[HARD]
What is descheduling?

A) Same as scheduling
B) Moving pods off nodes to rebalance the cluster
C) Deleting scheduler
D) Pausing scheduling

---

### Question 199
[HARD]
What is the Kubernetes Descheduler?

A) Built-in component
B) Separate project that evicts pods to improve balance
C) Scheduler plugin
D) Deprecated tool

---

### Question 200
[HARD]
How do scheduling gates work?

A) Network gates
B) Block pod from scheduling until gates are removed
C) Security gates
D) Rate limiting

---

## Summary

This question set covers Kubernetes scheduling topics essential for the KCNA certification.
