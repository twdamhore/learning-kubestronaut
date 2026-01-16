# Kubernetes Scheduling - 200 MCQ Questions

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Scheduling
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

## kube-scheduler Basics

### Question 1
[MEDIUM]
What is the primary role of kube-scheduler in Kubernetes?

### Question 2
[MEDIUM]
Which component does kube-scheduler communicate with to assign Pods to nodes?

### Question 3
[MEDIUM-HARD]
What happens to a Pod if no node satisfies its scheduling requirements?

### Question 4
[MEDIUM-HARD]
In which phase does the scheduler filter out unsuitable nodes?

### Question 5
[MEDIUM-HARD]
What is the scoring phase in the scheduling process?

### Question 6
[HARD]
What happens when multiple nodes have the same highest score?

### Question 7
[MEDIUM-HARD]
Which scheduling phase comes first: filtering or scoring?

### Question 8
[MEDIUM-HARD]
What is the default scheduler name in Kubernetes?

### Question 9
[HARD]
Can a Pod specify which scheduler should schedule it?

### Question 10
[MEDIUM-HARD]
What field in a Pod spec determines which scheduler handles it?

---

## Node Selection

### Question 11
[MEDIUM]
What is the simplest way to schedule a Pod to a specific node?

### Question 12
[MEDIUM-HARD]
What happens if you specify a nodeName that doesn't exist?

### Question 13
[MEDIUM-HARD]
Does nodeName bypass the scheduler?

### Question 14
[HARD]
What are the limitations of using nodeName for scheduling?

### Question 15
[MEDIUM-HARD]
Can nodeName be changed after a Pod is created?

---

## nodeSelector

### Question 16
[MEDIUM]
What is a nodeSelector?

### Question 17
[MEDIUM]
Where is nodeSelector specified in a Pod definition?

### Question 18
[MEDIUM-HARD]
What type of matching does nodeSelector use?

### Question 19
[MEDIUM-HARD]
What happens if no nodes match the nodeSelector labels?

### Question 20
[MEDIUM-HARD]
Can you use multiple labels in a nodeSelector?

### Question 21
[HARD]
What is the relationship between nodeSelector and node affinity?

### Question 22
[MEDIUM-HARD]
How do you label a node for use with nodeSelector?

### Question 23
[MEDIUM-HARD]
Are nodeSelector labels case-sensitive?

### Question 24
[MEDIUM-HARD]
Can nodeSelector use inequality operators?

### Question 25
[HARD]
What built-in labels are available on nodes for scheduling?

---

## Node Affinity

### Question 26
[MEDIUM]
What is node affinity?

### Question 27
[MEDIUM-HARD]
What are the two types of node affinity?

### Question 28
[MEDIUM-HARD]
What does requiredDuringSchedulingIgnoredDuringExecution mean?

### Question 29
[MEDIUM-HARD]
What does preferredDuringSchedulingIgnoredDuringExecution mean?

### Question 30
[HARD]
What does "IgnoredDuringExecution" mean in node affinity rules?

### Question 31
[MEDIUM-HARD]
Which operators are available in node affinity expressions?

### Question 32
[MEDIUM-HARD]
What does the In operator do in node affinity?

### Question 33
[MEDIUM-HARD]
What does the NotIn operator do in node affinity?

### Question 34
[MEDIUM-HARD]
What does the Exists operator do in node affinity?

### Question 35
[MEDIUM-HARD]
What does the DoesNotExist operator do in node affinity?

### Question 36
[HARD]
What do the Gt and Lt operators do in node affinity?

### Question 37
[MEDIUM-HARD]
How do you specify weight for preferred node affinity?

### Question 38
[HARD]
What is the valid range for node affinity weights?

### Question 39
[HARD]
How are multiple node affinity terms combined?

### Question 40
[HARD]
How are multiple matchExpressions within a term combined?

---

## Pod Affinity

### Question 41
[MEDIUM]
What is pod affinity?

### Question 42
[MEDIUM-HARD]
What is the topologyKey in pod affinity?

### Question 43
[MEDIUM-HARD]
What is a common topologyKey value?

### Question 44
[MEDIUM-HARD]
What does pod affinity's requiredDuringSchedulingIgnoredDuringExecution do?

### Question 45
[HARD]
Can pod affinity reference pods in other namespaces?

### Question 46
[MEDIUM-HARD]
What is the labelSelector in pod affinity used for?

### Question 47
[HARD]
What happens if topologyKey is set to kubernetes.io/hostname?

### Question 48
[HARD]
What is the performance impact of pod affinity rules?

### Question 49
[MEDIUM-HARD]
Can you combine pod affinity with node affinity?

### Question 50
[HARD]
What is the namespaceSelector field in pod affinity?

---

## Pod Anti-Affinity

### Question 51
[MEDIUM]
What is pod anti-affinity?

### Question 52
[MEDIUM-HARD]
When would you use pod anti-affinity?

### Question 53
[MEDIUM-HARD]
How do you specify pod anti-affinity in a Pod spec?

### Question 54
[HARD]
What is the difference between required and preferred anti-affinity?

### Question 55
[MEDIUM-HARD]
Can pod anti-affinity use the same operators as pod affinity?

### Question 56
[HARD]
What happens when anti-affinity conflicts with other scheduling constraints?

### Question 57
[HARD]
How does anti-affinity affect Deployment rollouts?

### Question 58
[MEDIUM-HARD]
What topologyKey would spread pods across availability zones?

### Question 59
[HARD]
Can anti-affinity reference pods from the same Deployment?

### Question 60
[HARD]
What are the limitations of pod anti-affinity?

---

## Taints and Tolerations

### Question 61
[MEDIUM]
What is a taint in Kubernetes?

### Question 62
[MEDIUM]
What is a toleration?

### Question 63
[MEDIUM-HARD]
What are the three taint effects?

### Question 64
[MEDIUM-HARD]
What does the NoSchedule effect do?

### Question 65
[MEDIUM-HARD]
What does the PreferNoSchedule effect do?

### Question 66
[MEDIUM-HARD]
What does the NoExecute effect do?

### Question 67
[MEDIUM-HARD]
How do you add a taint to a node?

### Question 68
[MEDIUM-HARD]
How do you remove a taint from a node?

### Question 69
[MEDIUM-HARD]
Where are tolerations specified?

### Question 70
[HARD]
What operators are available for tolerations?

### Question 71
[MEDIUM-HARD]
What does the Equal operator do in tolerations?

### Question 72
[MEDIUM-HARD]
What does the Exists operator do in tolerations?

### Question 73
[HARD]
How do you tolerate all taints on a node?

### Question 74
[HARD]
What is tolerationSeconds used for?

### Question 75
[MEDIUM-HARD]
What built-in taints does Kubernetes add automatically?

### Question 76
[HARD]
What is the node.kubernetes.io/not-ready taint?

### Question 77
[HARD]
What is the node.kubernetes.io/unreachable taint?

### Question 78
[HARD]
How do taints and tolerations differ from node affinity?

### Question 79
[MEDIUM-HARD]
Can a Pod tolerate multiple taints?

### Question 80
[HARD]
What happens to running pods when a NoExecute taint is added?

---

## Resource Requests and Scheduling

### Question 81
[MEDIUM]
How do resource requests affect scheduling?

### Question 82
[MEDIUM-HARD]
What resources are typically specified for scheduling?

### Question 83
[MEDIUM-HARD]
What happens if no node has enough resources for a Pod's requests?

### Question 84
[MEDIUM-HARD]
Does the scheduler consider resource limits or requests?

### Question 85
[HARD]
What is the allocatable capacity of a node?

### Question 86
[MEDIUM-HARD]
How is allocatable different from total capacity?

### Question 87
[HARD]
What resources are reserved for system components?

### Question 88
[MEDIUM-HARD]
Can a Pod be scheduled if it exceeds available resources?

### Question 89
[HARD]
What is resource overcommitment?

### Question 90
[HARD]
How does the LeastRequestedPriority scoring plugin work?

---

## Pod Priority and Preemption

### Question 91
[MEDIUM]
What is Pod priority?

### Question 92
[MEDIUM-HARD]
How do you set a Pod's priority?

### Question 93
[MEDIUM-HARD]
What is a PriorityClass?

### Question 94
[MEDIUM-HARD]
What is the valid range for priority values?

### Question 95
[HARD]
What does preemption mean in Kubernetes scheduling?

### Question 96
[MEDIUM-HARD]
When does preemption occur?

### Question 97
[HARD]
Can preemption be disabled for a PriorityClass?

### Question 98
[HARD]
What is the preemptionPolicy field?

### Question 99
[MEDIUM-HARD]
What is the default priority for pods without a PriorityClass?

### Question 100
[HARD]
What is the system-cluster-critical PriorityClass?

### Question 101
[HARD]
What is the system-node-critical PriorityClass?

### Question 102
[HARD]
How does the scheduler choose which pods to preempt?

### Question 103
[MEDIUM-HARD]
What is the globalDefault field in PriorityClass?

### Question 104
[HARD]
Can preemption evict pods protected by PodDisruptionBudget?

### Question 105
[HARD]
What happens to preempted pods?

---

## Pod Topology Spread Constraints

### Question 106
[MEDIUM-HARD]
What are Pod Topology Spread Constraints?

### Question 107
[MEDIUM-HARD]
What is maxSkew in topology spread?

### Question 108
[MEDIUM-HARD]
What values can whenUnsatisfiable take?

### Question 109
[HARD]
What does DoNotSchedule do in topology spread?

### Question 110
[HARD]
What does ScheduleAnyway do in topology spread?

### Question 111
[MEDIUM-HARD]
What is topologyKey in topology spread constraints?

### Question 112
[HARD]
How do topology spread constraints differ from pod anti-affinity?

### Question 113
[HARD]
Can you specify multiple topology spread constraints?

### Question 114
[HARD]
What is minDomains in topology spread constraints?

### Question 115
[HARD]
How does the scheduler calculate skew?

---

## DaemonSet Scheduling

### Question 116
[MEDIUM]
How are DaemonSet pods scheduled?

### Question 117
[MEDIUM-HARD]
Does DaemonSet use the default scheduler?

### Question 118
[MEDIUM-HARD]
How do taints affect DaemonSet scheduling?

### Question 119
[HARD]
What tolerations do DaemonSets automatically get?

### Question 120
[MEDIUM-HARD]
Can you use nodeSelector with DaemonSets?

### Question 121
[MEDIUM-HARD]
Can you use node affinity with DaemonSets?

### Question 122
[HARD]
What happens when a new node joins the cluster with a DaemonSet?

### Question 123
[MEDIUM-HARD]
How do you prevent a DaemonSet from scheduling on specific nodes?

### Question 124
[HARD]
What is the scheduling strategy for DaemonSet updates?

### Question 125
[HARD]
How do DaemonSets handle unschedulable nodes?

---

## Static Pods

### Question 126
[MEDIUM]
What is a static Pod?

### Question 127
[MEDIUM-HARD]
Who manages static Pods?

### Question 128
[MEDIUM-HARD]
Where are static Pod manifests stored?

### Question 129
[MEDIUM-HARD]
How does kubelet discover static Pod manifests?

### Question 130
[HARD]
Can static Pods be managed by the API server?

### Question 131
[MEDIUM-HARD]
What is a mirror Pod?

### Question 132
[HARD]
Can you delete a static Pod through the API?

### Question 133
[MEDIUM-HARD]
What control plane components run as static Pods?

### Question 134
[HARD]
How do you modify a static Pod?

### Question 135
[HARD]
What happens if a static Pod manifest is deleted?

---

## Manual Scheduling

### Question 136
[MEDIUM]
How do you manually schedule a Pod?

### Question 137
[MEDIUM-HARD]
What field is used for manual scheduling?

### Question 138
[HARD]
Can you use nodeName with a nonexistent node?

### Question 139
[MEDIUM-HARD]
Does manual scheduling bypass admission controllers?

### Question 140
[HARD]
What is the Binding API?

### Question 141
[HARD]
How can you create a custom scheduler?

### Question 142
[MEDIUM-HARD]
What happens if you set nodeName on a pending Pod?

### Question 143
[HARD]
Can you change nodeName after Pod creation?

### Question 144
[HARD]
What are the use cases for manual scheduling?

### Question 145
[MEDIUM-HARD]
Does nodeName respect taints?

---

## Multiple Schedulers

### Question 146
[MEDIUM-HARD]
Can you run multiple schedulers in Kubernetes?

### Question 147
[MEDIUM-HARD]
How do you specify which scheduler should schedule a Pod?

### Question 148
[HARD]
What is the schedulerName field?

### Question 149
[HARD]
What happens if the specified scheduler doesn't exist?

### Question 150
[HARD]
How do you deploy a custom scheduler?

### Question 151
[HARD]
Can multiple schedulers compete for the same Pod?

### Question 152
[HARD]
What permissions does a custom scheduler need?

### Question 153
[HARD]
How do you configure scheduler leader election?

### Question 154
[HARD]
What is the scheduler extender?

### Question 155
[HARD]
How do scheduler plugins differ from extenders?

---

## Scheduler Profiles

### Question 156
[HARD]
What is a scheduler profile?

### Question 157
[HARD]
Can a single scheduler run multiple profiles?

### Question 158
[HARD]
How do you configure scheduler profiles?

### Question 159
[HARD]
What are the scheduler extension points?

### Question 160
[HARD]
What is the PreFilter extension point?

### Question 161
[HARD]
What is the Filter extension point?

### Question 162
[HARD]
What is the PostFilter extension point?

### Question 163
[HARD]
What is the Score extension point?

### Question 164
[HARD]
What is the Reserve extension point?

### Question 165
[HARD]
What is the Bind extension point?

---

## Scheduler Plugins

### Question 166
[HARD]
What are scheduler plugins?

### Question 167
[HARD]
What is the NodeResourcesFit plugin?

### Question 168
[HARD]
What is the NodeAffinity plugin?

### Question 169
[HARD]
What is the PodTopologySpread plugin?

### Question 170
[HARD]
What is the InterPodAffinity plugin?

### Question 171
[HARD]
What is the TaintToleration plugin?

### Question 172
[HARD]
How do you enable or disable scheduler plugins?

### Question 173
[HARD]
What is the default set of enabled plugins?

### Question 174
[HARD]
Can you write custom scheduler plugins?

### Question 175
[HARD]
What is the scheduler framework?

---

## Scheduling Troubleshooting

### Question 176
[MEDIUM]
How do you check why a Pod is Pending?

### Question 177
[MEDIUM-HARD]
What events indicate scheduling failures?

### Question 178
[MEDIUM-HARD]
What does "Insufficient cpu" mean?

### Question 179
[MEDIUM-HARD]
What does "node(s) had taint that pod didn't tolerate" mean?

### Question 180
[MEDIUM-HARD]
What does "node(s) didn't match node selector" mean?

### Question 181
[HARD]
How do you debug node affinity issues?

### Question 182
[HARD]
How do you check a node's allocatable resources?

### Question 183
[MEDIUM-HARD]
What does "0/3 nodes are available" mean?

### Question 184
[HARD]
How do you simulate scheduling without actually scheduling?

### Question 185
[HARD]
What is the scheduler's verbose logging?

---

## Advanced Scheduling Concepts

### Question 186
[HARD]
What is gang scheduling?

### Question 187
[HARD]
What is bin packing in scheduling?

### Question 188
[HARD]
What is spreading in scheduling?

### Question 189
[HARD]
How does the scheduler handle pod overhead?

### Question 190
[HARD]
What is the scheduling queue?

### Question 191
[HARD]
What are the sub-queues in the scheduling queue?

### Question 192
[HARD]
What triggers a Pod to move back to the active queue?

### Question 193
[HARD]
What is the nominated node?

### Question 194
[HARD]
How does the scheduler handle volume topology?

### Question 195
[HARD]
What is delayed binding for volumes?

### Question 196
[HARD]
What is the NodeVolumeLimits plugin?

### Question 197
[HARD]
How does scheduling work with ephemeral volumes?

### Question 198
[HARD]
What is descheduling?

### Question 199
[HARD]
What is the Kubernetes Descheduler?

### Question 200
[HARD]
How do scheduling gates work?

---

## Summary

This question set covers Kubernetes scheduling topics essential for the KCNA certification.
