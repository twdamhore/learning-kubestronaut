# Administration - 100 MCQ Questions (Part A)

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Administration
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

## kubectl Basics

## kubectl Basics

### Question 1
[MEDIUM]

Which command displays the current Kubernetes cluster information?

A) kubectl cluster-status
B) kubectl cluster-info
C) kubectl get cluster
D) kubectl describe cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cluster-info` displays information about the Kubernetes cluster, including the addresses of the control plane and services. This is useful for verifying cluster connectivity and discovering service endpoints.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 2
[MEDIUM-HARD]

Which kubectl command would you use to view the API resources available in your cluster?

A) kubectl get resources
B) kubectl api-resources
C) kubectl describe api
D) kubectl list resources

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl api-resources` lists all the resource types available in the cluster, including their short names, API group, whether they're namespaced, and their kind. This is essential for understanding what resources you can manage.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 3
[MEDIUM-HARD]

Which flag would you use with kubectl to see additional columns in the output?

A) -o extended
B) -o verbose
C) -o wide
D) -o full

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The `-o wide` flag shows additional columns that aren't displayed by default, such as node name for Pods, selector for Services, and other resource-specific details. This provides more information without switching to full JSON/YAML output.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 4
[HARD]

When using `kubectl apply`, where is the last-applied-configuration stored?

A) In etcd as a separate object
B) As an annotation on the resource
C) In a local file on the client
D) In the kube-system namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl apply` stores the last-applied configuration as an annotation (`kubectl.kubernetes.io/last-applied-configuration`) on the resource itself. This allows kubectl to perform three-way merges when applying changes, comparing the new configuration, the last-applied configuration, and the live state.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 5
[MEDIUM-HARD]

What does the `--dry-run=client` flag do?

A) Sends the request to the server without persisting
B) Validates the request locally without server contact
C) Creates a backup before making changes
D) Runs in verbose mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--dry-run=client` processes the request locally without sending it to the API server. It's useful for generating manifests (e.g., `kubectl create deployment nginx --image=nginx --dry-run=client -o yaml`). Use `--dry-run=server` for server-side validation.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 6
[HARD]

What is the behavior of `kubectl delete` when using the `--wait=false` flag?

A) Deletion is cancelled
B) Command returns immediately without waiting for deletion
C) Forces immediate termination
D) Skips confirmation prompt

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--wait=false` makes kubectl return immediately after the deletion request is accepted, without waiting for the resource to be fully removed. By default, kubectl waits for the resource to be deleted. This is useful for scripting when you don't need to block on deletion completion.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## kubeconfig and Contexts

### Question 7
[MEDIUM]

Where is the default kubeconfig file located?

A) /etc/kubernetes/config
B) ~/.kube/config
C) /var/lib/kubernetes/config
D) ~/.kubernetes/config

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The default kubeconfig file is located at `~/.kube/config` in the user's home directory. This location can be overridden using the `KUBECONFIG` environment variable or the `--kubeconfig` flag with kubectl commands.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 8
[MEDIUM-HARD]

Which command switches to a different context in kubectl?

A) kubectl set-context
B) kubectl use-context
C) kubectl config use-context
D) kubectl switch-context

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** `kubectl config use-context <context-name>` switches the current context. This changes which cluster and user credentials kubectl will use for subsequent commands. You can view available contexts with `kubectl config get-contexts`.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 9
[MEDIUM-HARD]

What does the KUBECONFIG environment variable support for working with multiple config files?

A) Only a single file path
B) Colon-separated list of file paths
C) Directory path to scan for configs
D) URL to remote config

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The KUBECONFIG environment variable supports multiple colon-separated file paths (semicolon on Windows). When multiple files are specified, kubectl merges them into a single configuration at runtime. This allows you to organize configs across multiple files.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 10
[MEDIUM-HARD]

Which command displays the current context?

A) kubectl config get-context
B) kubectl config current-context
C) kubectl context show
D) kubectl config view-context

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl config current-context` displays the name of the currently active context. This is useful in scripts or when you need to verify which cluster you're connected to before running commands.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 11
[HARD]

What command would you use to view the merged kubeconfig settings with secrets redacted?

A) kubectl config view
B) kubectl config show
C) kubectl config dump
D) kubectl config display

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl config view` displays the merged kubeconfig content with sensitive data like tokens and certificates redacted (shown as "REDACTED" or "DATA+OMITTED"). Use `--raw` to see the actual values if needed.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Cluster Components

### Question 12
[MEDIUM]

Which control plane component assigns Pods to nodes?

A) kubelet
B) kube-controller-manager
C) kube-scheduler
D) kube-proxy

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-scheduler watches for newly created Pods that have no node assigned and selects a node for them to run on. It considers factors like resource requirements, affinity/anti-affinity rules, taints/tolerations, and data locality.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

### Question 13
[MEDIUM-HARD]

Which component runs on every node and ensures containers are running in Pods?

A) kube-proxy
B) kubelet
C) container-runtime
D) kube-scheduler

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet is an agent that runs on each node in the cluster. It ensures that containers described in PodSpecs are running and healthy. It doesn't manage containers that weren't created by Kubernetes.

**Source:** [kubelet | Kubernetes](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/)

</details>

---

### Question 14
[HARD]

Which control plane components must be available before the scheduler can function?

A) Only etcd
B) etcd and kube-apiserver
C) All other control plane components
D) None, scheduler can start independently

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The scheduler depends on the API server to watch for unscheduled Pods and to bind Pods to nodes. The API server in turn requires etcd for persistent storage. Official docs describe component roles and dependencies but don't prescribe a fixed startup order beyond these dependencies.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

### Question 15
[HARD]

What happens if etcd becomes unavailable while the cluster is running?

A) All pods immediately stop
B) Existing pods continue but no new changes can be made
C) The cluster automatically fails over to backup
D) Nodes automatically form a new cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If etcd becomes unavailable, existing workloads continue to run because kubelet operates independently. However, no new Pods can be scheduled, no changes can be made to any resources, and the API server cannot process requests. The cluster enters a degraded state until etcd is restored.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

### Question 16
[HARD]

What is the cloud-controller-manager responsible for?

A) Managing cloud storage only
B) Running cloud-specific control loops
C) Authenticating with cloud providers
D) Billing and cost management

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The cloud-controller-manager runs controllers that interact with cloud provider APIs. It includes the Node Controller (checking if nodes exist in the cloud), Route Controller (setting up routes), and Service Controller (managing cloud load balancers). It separates cloud-specific code from the core Kubernetes code.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

## Namespaces

### Question 17
[MEDIUM]

Which namespace contains Kubernetes system components?

A) kubernetes-system
B) kube-system
C) system
D) default

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kube-system` namespace contains objects created by the Kubernetes system, including system Pods like kube-dns, kube-proxy, and the metrics server. This namespace is created automatically when a cluster is bootstrapped.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 18
[MEDIUM-HARD]

Which resources are NOT namespaced in Kubernetes?

A) Pods and Services
B) Nodes and PersistentVolumes
C) ConfigMaps and Secrets
D) Deployments and ReplicaSets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Nodes and PersistentVolumes are cluster-scoped (non-namespaced) resources. Other cluster-scoped resources include ClusterRoles, ClusterRoleBindings, Namespaces themselves, and StorageClasses. You can see which resources are namespaced using `kubectl api-resources --namespaced=true/false`.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 19
[MEDIUM-HARD]

How do you list all pods across all namespaces?

A) kubectl get pods --all
B) kubectl get pods -A
C) kubectl get pods --global
D) kubectl get pods --cluster-wide

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `-A` or `--all-namespaces` flag lists resources across all namespaces. This is useful for cluster-wide visibility, such as when troubleshooting or auditing resources across the entire cluster.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 20
[MEDIUM-HARD]

Which command creates a new namespace called "development"?

A) kubectl create ns development
B) kubectl new namespace development
C) kubectl add namespace development
D) kubectl namespace create development

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl create namespace development` or the shorthand `kubectl create ns development` creates a new namespace. Namespaces can also be created declaratively using a YAML manifest with `kubectl apply`.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

## Labels and Selectors

### Question 21
[MEDIUM]

What is the primary purpose of labels in Kubernetes?

A) To add documentation to resources
B) To organize and select subsets of objects
C) To define resource limits
D) To specify container images

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Labels are key-value pairs attached to objects that are used to organize and select subsets of objects. They're used by selectors to identify resources for services, deployments, and other controllers. Labels are the primary grouping mechanism in Kubernetes.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 22
[MEDIUM-HARD]

What is the difference between `matchLabels` and `matchExpressions`?

A) matchLabels is for Pods, matchExpressions is for Services
B) matchLabels uses equality, matchExpressions uses set operations
C) matchLabels is newer than matchExpressions
D) They are aliases for the same functionality

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `matchLabels` is a map of key-value pairs for equality matching. `matchExpressions` is a list of selector requirements using set-based operators (In, NotIn, Exists, DoesNotExist). Both can be combined in a selector, where all conditions must match (AND logic).

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 23
[MEDIUM-HARD]

Which kubectl command adds a label to an existing resource?

A) kubectl tag pod nginx app=web
B) kubectl label pod nginx app=web
C) kubectl annotate pod nginx app=web
D) kubectl set label pod nginx app=web

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl label` adds, modifies, or removes labels on resources. To add: `kubectl label pod nginx app=web`. To modify: add `--overwrite`. To remove: `kubectl label pod nginx app-` (note the trailing hyphen).

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 24
[MEDIUM-HARD]

What is the result of the selector `-l 'env in (prod, staging)'`?

A) Resources with env=prod AND env=staging
B) Resources with env=prod OR env=staging
C) Resources without env label
D) All resources with env label

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `in` operator is a set-based selector that matches resources where the label value is one of the specified values. So `env in (prod, staging)` matches resources where the env label is either "prod" OR "staging".

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 25
[HARD]

In a selector with multiple conditions, what is the logical relationship between them?

A) OR - any condition can match
B) AND - all conditions must match
C) XOR - exactly one must match
D) Configurable per selector

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When multiple conditions are specified in a selector (comma-separated for equality-based or multiple matchExpressions), they are combined with AND logic. All conditions must be satisfied for a resource to be selected.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Annotations

### Question 26
[MEDIUM]

What is the main difference between labels and annotations?

A) Annotations can be longer values
B) Annotations aren't used for selection
C) Both A and B
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Annotations are similar to labels but are not used to identify and select objects. They can store larger amounts of data (up to 256KB total) and are typically used for non-identifying metadata like build info, tool configuration, or human-readable descriptions.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 27
[MEDIUM-HARD]

What is the maximum size limit for annotation values?

A) 63 characters
B) 256 characters
C) No hard limit per value, but total must be under 256KB
D) 1MB

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Individual annotation values don't have a character limit, but the total size of all annotations on an object must not exceed 256KB. This allows storing larger data like JSON configurations, certificates, or detailed descriptions.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 28
[HARD]

Which annotation is used by `kubectl apply` for tracking configuration?

A) kubernetes.io/last-applied
B) kubectl.kubernetes.io/last-applied-configuration
C) app.kubernetes.io/managed-by
D) meta.kubernetes.io/applied-config

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl apply` uses the annotation `kubectl.kubernetes.io/last-applied-configuration` to store the full JSON of the last applied configuration. This enables three-way strategic merge patches when applying updates.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Resource Management

### Question 29
[MEDIUM]

What unit is used to specify CPU requests and limits?

A) Percentage
B) Cores or millicores
C) GHz
D) Threads

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CPU is specified in cores (e.g., `1`, `0.5`) or millicores (e.g., `500m` = 0.5 cores). One core equals 1000 millicores. This unit is consistent across different hardware. Memory uses bytes (Ki, Mi, Gi).

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 30
[MEDIUM-HARD]

What happens when a container tries to use more CPU than its limit?

A) The container is killed
B) The container is throttled
C) The node becomes unresponsive
D) The container steals CPU from other pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CPU is a compressible resource, so when a container tries to use more than its limit, it's throttled rather than killed. The container continues running but with reduced CPU time. This is different from memory, which triggers OOM kills.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 31
[MEDIUM-HARD]

What is the purpose of ResourceQuota?

A) To limit resources per container
B) To limit aggregate resource consumption per namespace
C) To schedule pods based on resources
D) To monitor resource usage

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ResourceQuota limits the total resource consumption (CPU, memory, storage) and object counts (pods, services, secrets) in a namespace. When quotas are enforced, new resources that would exceed the quota are rejected.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 32
[MEDIUM-HARD]

Which QoS class pods are evicted first during node memory pressure?

A) Guaranteed
B) Burstable
C) BestEffort
D) They are evicted randomly

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** During memory pressure, pods are evicted based on QoS class: BestEffort first, then Burstable (starting with those using most resources relative to their requests), and Guaranteed last. This protects workloads that have properly specified their requirements.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 33
[HARD]

What is the default behavior when no resource requests are specified?

A) Default requests are 100m CPU and 128Mi memory
B) The pod is rejected
C) The pod runs with no requests (BestEffort QoS)
D) Cluster-wide defaults are applied automatically

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Without resource requests/limits specified (and without a LimitRange applying defaults), the Pod runs with no resource guarantees and gets BestEffort QoS class. These pods can use whatever resources are available but are first to be evicted under pressure.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

## RBAC (Role-Based Access Control)

### Question 34
[MEDIUM]

What is the difference between a Role and a ClusterRole?

A) Roles are for users, ClusterRoles are for services
B) Roles are namespaced, ClusterRoles are cluster-scoped
C) Roles are read-only, ClusterRoles allow write
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Role grants permissions within a specific namespace, while a ClusterRole grants permissions across the entire cluster (or to cluster-scoped resources like nodes). ClusterRoles can also be bound to specific namespaces using RoleBindings.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 35
[MEDIUM-HARD]

What is a ServiceAccount used for?

A) To provide identity for users
B) To provide identity for pods
C) To manage billing accounts
D) To store credentials securely

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ServiceAccounts provide an identity for processes running in Pods. They're used to authenticate with the API server and other services. Each namespace has a "default" ServiceAccount automatically used by pods that don't specify one.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 36
[HARD]

What is the difference between "update" and "patch" verbs?

A) Update replaces the entire resource, patch modifies parts
B) Update is synchronous, patch is asynchronous
C) They are identical
D) Update is for status, patch is for spec

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The `update` verb allows replacing an entire resource (like PUT), while `patch` allows modifying specific fields (like PATCH). Strategic merge patches and JSON patches use the patch verb. Update requires sending the complete resource.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 37
[HARD]

What does the `*` (asterisk) mean in an RBAC rule?

A) Invalid syntax
B) All items (resources, verbs, or API groups)
C) Regex pattern matching
D) Required field

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In RBAC rules, `*` means "all" - all verbs, all resources, or all API groups depending on context. For example, `verbs: ["*"]` grants all possible actions, and `resources: ["*"]` applies to all resource types. Use with caution.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 38
[HARD]

What is an aggregated ClusterRole?

A) A ClusterRole that aggregates usage metrics
B) A ClusterRole that combines rules from multiple ClusterRoles
C) A ClusterRole shared by multiple clusters
D) A compressed ClusterRole for efficiency

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Aggregated ClusterRoles use `aggregationRule` to automatically combine rules from other ClusterRoles that match specified labels. This allows extending built-in roles (like admin, edit, view) without modifying them directly. When matching ClusterRoles change, the aggregated role updates automatically.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

## Node Management

### Question 39
[MEDIUM-HARD]

What is the difference between `kubectl cordon` and `kubectl drain`?

A) Cordon marks unschedulable, drain also evicts existing pods
B) They are identical commands
C) Cordon is for workers, drain is for control plane
D) Drain marks unschedulable, cordon evicts pods

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `cordon` only marks the node unschedulable for new pods. `drain` marks the node unschedulable AND evicts all pods (except DaemonSet pods by default). Drain is used before maintenance, upgrades, or decommissioning a node.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 40
[HARD]

What is a taint on a node used for?

A) To mark a node as faulty
B) To repel pods that don't tolerate the taint
C) To encrypt node communication
D) To track node health metrics

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Taints are applied to nodes and work with tolerations on pods. A taint "repels" pods unless they have a matching toleration. This is used to dedicate nodes for specific workloads (like GPU nodes) or to mark problematic nodes.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 41
[MEDIUM-HARD]

How do you add a taint to a node?

A) kubectl taint node worker1 key=value:NoSchedule
B) kubectl label node worker1 taint=key:value
C) kubectl mark node worker1 taint key=value
D) kubectl set taint node worker1 key=value

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl taint nodes <node-name> key=value:effect` adds a taint. Example: `kubectl taint nodes worker1 dedicated=gpu:NoSchedule`. To remove a taint, add a minus sign: `kubectl taint nodes worker1 dedicated=gpu:NoSchedule-`.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 42
[MEDIUM-HARD]

What is the purpose of the node condition taint `node.kubernetes.io/not-ready`?

A) To mark nodes that haven't joined the cluster
B) To automatically taint nodes when they become unhealthy
C) To prevent scheduling on nodes during upgrades
D) To mark nodes reserved for system pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes automatically adds taints like `node.kubernetes.io/not-ready`, `node.kubernetes.io/unreachable`, and others based on node conditions. This helps protect workloads by preventing scheduling on problematic nodes without manual intervention.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

## etcd Administration

### Question 43
[MEDIUM]

What type of data store is etcd?

A) Relational database
B) Document database
C) Distributed key-value store
D) Graph database

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** etcd is a distributed, reliable key-value store used by Kubernetes to store all cluster data. It uses the Raft consensus algorithm for distributed consistency and is designed to be highly available and consistent.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

### Question 44
[HARD]

What is the recommended number of etcd members for high availability?

A) 2
B) 3 or 5
C) 6
D) Any even number

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** etcd uses Raft consensus, which requires a majority (quorum) to function. An odd number (3, 5, or 7) of members is recommended. Three members can tolerate one failure, five can tolerate two. Even numbers provide no additional fault tolerance over the odd number below them.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

### Question 45
[HARD]

What is the purpose of the etcd compaction process?

A) To compress data for storage efficiency
B) To remove historical versions of keys
C) To merge fragmented data files
D) To encrypt sensitive data

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** etcd compaction removes superseded key versions up to a specified revision, reclaiming storage space. After compaction, only the latest version of keys (up to that revision) is kept. This prevents unbounded storage growth from key history.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

### Question 46
[HARD]

What happens to Kubernetes if etcd loses quorum?

A) The cluster continues normally
B) Pods stop immediately
C) API server becomes read-only/unavailable
D) Cluster automatically recovers

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Without quorum, etcd cannot process writes, making the API server unable to make changes. Existing workloads continue running (kubelet operates independently), but no new pods can be scheduled, and no changes can be made until quorum is restored.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

## Cluster Upgrades

### Question 47
[MEDIUM]

What is the recommended order for upgrading Kubernetes components?

A) Workers first, then control plane
B) Control plane first, then workers
C) All components simultaneously
D) etcd last

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The recommended upgrade order is: etcd (if external), control plane components (kube-apiserver, kube-controller-manager, kube-scheduler), then worker nodes. The control plane must be upgraded before workers to maintain version compatibility.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

### Question 48
[MEDIUM-HARD]

What tool is commonly used to upgrade kubeadm-based clusters?

A) kubectl upgrade
B) kubeadm upgrade
C) kubernetes-upgrade
D) cluster-upgrade

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubeadm upgrade` is used to upgrade kubeadm-based clusters. The process involves: `kubeadm upgrade plan` (shows upgrade options), `kubeadm upgrade apply` (upgrades control plane), then upgrading kubelet and kubectl on each node.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

### Question 49
[MEDIUM-HARD]

During a cluster upgrade, what happens to running pods?

A) They are automatically restarted
B) They continue running unless the node is drained
C) They are paused during upgrade
D) They are deleted and recreated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Upgrading control plane components doesn't affect running pods. When upgrading worker nodes, you typically drain each node first (which evicts pods), upgrade, then uncordon. Pods continue running on non-drained nodes during the process.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

### Question 50
[MEDIUM-HARD]

What command shows the upgrade plan in a kubeadm cluster?

A) kubeadm upgrade status
B) kubeadm upgrade plan
C) kubeadm upgrade check
D) kubeadm cluster upgrade-plan

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubeadm upgrade plan` checks the current cluster version, available upgrades, and shows any prerequisite steps needed. It validates the cluster state and provides the exact commands to run for the upgrade.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

## API and Versioning

### Question 51
[MEDIUM]

What are the three stages of API version stability in Kubernetes?

A) dev, test, prod
B) alpha, beta, stable
C) v1, v2, v3
D) experimental, standard, deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes API versions follow three stages: alpha (e.g., v1alpha1 - disabled by default, may be buggy), beta (e.g., v1beta1 - enabled by default, well-tested), and stable (e.g., v1 - production-ready). Stable APIs may be deprecated and eventually removed following Kubernetes deprecation policy, which requires proper notice periods and migration paths.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 52
[MEDIUM-HARD]

Which API group contains Deployments?

A) core
B) extensions
C) apps
D) workloads

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Deployments, StatefulSets, DaemonSets, and ReplicaSets are in the `apps` API group. The apiVersion for a Deployment is `apps/v1`. The `extensions` group previously contained these resources but they were moved to `apps`.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 53
[MEDIUM-HARD]

How do you list all API versions available in a cluster?

A) kubectl api-groups
B) kubectl api-versions
C) kubectl get apis
D) kubectl version --all

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl api-versions` lists all API versions (group/version combinations) available in the cluster. This is useful for determining which apiVersion to use in manifests and checking for available API groups.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 54
[MEDIUM-HARD]

What helps identify deprecated API usage in manifests?

A) kubectl deprecate check
B) kubectl api-resources --deprecated
C) External tools like pluto or kubent
D) kubectl validate --deprecated

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** External tools like `pluto` and `kubent` scan manifests and cluster resources for deprecated API usage. kubectl itself shows deprecation warnings when deprecated resources are accessed but doesn't have a dedicated deprecation scanning command. These tools are essential for preparing cluster upgrades.

**Source:** [Deprecated API Migration Guide | Kubernetes](https://kubernetes.io/docs/reference/using-api/deprecation-guide/)

</details>

---

### Question 55
[MEDIUM-HARD]

What are the two types of admission webhooks?

A) Pre and Post
B) Sync and Async
C) Mutating and Validating
D) Internal and External

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Mutating admission webhooks can modify incoming objects (e.g., adding default values or sidecars). Validating webhooks can only accept or reject requests. Mutating webhooks run before validating webhooks. Both allow extending admission control without modifying the API server.

**Source:** [Admission Controllers Reference | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

---

## Logging and Monitoring

### Question 56
[MEDIUM]

What command shows logs from a container in a Pod?

A) kubectl get logs pod-name
B) kubectl logs pod-name
C) kubectl describe pod-name --logs
D) kubectl show logs pod-name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl logs <pod-name>` shows container logs. For multi-container pods, use `-c <container-name>` to specify which container. Add `-f` to follow/stream logs and `--previous` to see logs from a previous container instance.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 57
[MEDIUM-HARD]

What component is responsible for cluster-level logging aggregation?

A) kubelet
B) kube-proxy
C) No built-in component (requires external solution)
D) kube-logger

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Kubernetes doesn't provide a built-in cluster-level logging solution. Container logs are stored on nodes by the container runtime. Cluster-level logging requires external tools like the EFK stack (Elasticsearch, Fluentd, Kibana), Loki, or cloud provider solutions.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 58
[HARD]

What is the difference between container logging and node-level logging?

A) Container logs are stderr, node logs are stdout
B) Container logs are app output, node logs are system components
C) They are the same thing
D) Container logs are persistent, node logs are not

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Container logging captures stdout/stderr from application containers. Node-level logging refers to logs from system components like kubelet, container runtime, and kube-proxy. Both are important for troubleshooting but managed differently.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 59
[MEDIUM-HARD]

Which flag limits the number of log lines returned?

A) kubectl logs --lines=100
B) kubectl logs --tail=100
C) kubectl logs --limit=100
D) kubectl logs --count=100

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl logs --tail=100` returns only the last 100 lines of logs. This is useful for large logs where you only need recent entries. You can combine it with `-f` to stream new logs after showing the last N lines.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

## Service Accounts

### Question 60
[MEDIUM]

What is automatically created in every namespace?

A) An admin user
B) A default ServiceAccount
C) A cluster role
D) A network policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes automatically creates a ServiceAccount named "default" in every namespace. Pods that don't specify a ServiceAccount automatically use this default ServiceAccount for authentication with the API server.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 61
[HARD]

What is mounted into a Pod for ServiceAccount authentication?

A) Username and password
B) A projected token volume
C) An SSH key
D) A client certificate only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, Kubernetes mounts a projected ServiceAccount token into pods at `/var/run/secrets/kubernetes.io/serviceaccount/`. This includes the token, CA certificate, and namespace. The token is used to authenticate with the API server.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 62
[HARD]

What changed in Kubernetes 1.24 regarding ServiceAccount tokens?

A) Tokens are no longer supported
B) Auto-generated Secret-based tokens were removed
C) Token rotation became mandatory
D) Tokens expire after 1 hour

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes 1.24 stopped automatically generating Secret-based tokens for ServiceAccounts. Instead, the TokenRequest API provides time-limited, audience-bound tokens via projected volumes. Manual creation of Secret-based tokens is still possible if needed, but the recommended approach is using the TokenRequest API for improved security.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

## kubectl Advanced Usage

### Question 63
[MEDIUM-HARD]

What does `kubectl get pods -o jsonpath='{.items[*].metadata.name}'` return?

A) Full JSON output of all pods
B) Only the names of all pods
C) The metadata section of all pods
D) An error because syntax is wrong

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** JSONPath allows extracting specific fields from kubectl output. `{.items[*].metadata.name}` gets the name field from metadata for all items (pods). This is useful for scripting and extracting specific data without parsing full JSON.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 64
[MEDIUM-HARD]

What does `kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase` do?

A) Shows default output plus custom columns
B) Shows only specified custom columns
C) Creates new fields on the resources
D) Exports to CSV format

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Custom columns output shows only the specified columns with custom headers. This is useful for creating specific views of resources without the full default output. Multiple columns are comma-separated with NAME:JSONPath format.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 65
[HARD]

What is the purpose of `kubectl proxy`?

A) To proxy traffic between pods
B) To create a local proxy to the API server
C) To set up a network proxy for the cluster
D) To proxy external traffic to services

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl proxy` creates a local HTTP proxy to the Kubernetes API server, handling authentication automatically. This allows accessing the API via localhost without providing credentials. Useful for development, debugging, or accessing the Kubernetes dashboard.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 66
[HARD]

What does `kubectl port-forward pod/nginx 8080:80` do?

A) Opens port 8080 on the pod
B) Forwards local port 8080 to pod port 80
C) Creates a service on port 8080
D) Exposes the pod externally on port 8080

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl port-forward` creates a tunnel from your local machine to a pod. `8080:80` means local port 8080 forwards to pod port 80. Access the pod via localhost:8080. Useful for debugging without exposing services externally.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Advanced Administration

### Question 67
[HARD]

What is the purpose of the PodDisruptionBudget resource?

A) To limit pod memory usage
B) To ensure minimum availability during voluntary disruptions
C) To set network bandwidth limits
D) To control pod scheduling priority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PodDisruptionBudget (PDB) limits voluntary disruptions (like drains, upgrades) by specifying minimum available or maximum unavailable pods. This ensures high availability during maintenance. Involuntary disruptions (node failures) aren't blocked by PDBs.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 68
[HARD]

What is the PriorityClass resource used for?

A) To set network traffic priority
B) To define pod scheduling and preemption priority
C) To prioritize API requests
D) To set storage I/O priority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PriorityClass defines the priority of Pods for scheduling. Higher priority pods can preempt (evict) lower priority pods when resources are scarce. System-critical pods use high priorities. Pods reference PriorityClass via `priorityClassName`.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 69
[HARD]

What is the default priority value for pods without a PriorityClass?

A) -1
B) 0
C) 100
D) 1000

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pods without a PriorityClass have a default priority of 0. You can set a different cluster-wide default using `globalDefault: true` in a PriorityClass. System-critical pods typically use priorities around 2 billion.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 70
[HARD]

What is the purpose of finalizers in Kubernetes?

A) To define resource cleanup order
B) To prevent deletion until certain conditions are met
C) To finalize transactions
D) To compress resources before deletion

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Finalizers are keys on resources that tell Kubernetes to wait before fully deleting the resource. Controllers watch for resources with their finalizer, perform cleanup, then remove the finalizer. Only when all finalizers are removed is the resource actually deleted.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 71
[MEDIUM-HARD]

What garbage collection mode deletes dependents before the owner?

A) Background
B) Foreground
C) Orphan
D) Cascade

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Foreground cascading deletion deletes dependents first, then the owner. Background deletion (default) deletes the owner immediately while dependents are cleaned up in the background. Orphan deletion removes the owner but leaves dependents (removing owner references).

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Lease Objects and Leader Election

### Question 72
[HARD]

What is a Lease object used for in Kubernetes?

A) Network lease management
B) Resource locking and leader election
C) Storage lease allocation
D) License management

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Lease objects are used for distributed coordination, particularly node heartbeats and leader election for controllers. They provide a lightweight way to implement leader election without complex distributed systems. The lease holder is the leader until the lease expires.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Events

### Question 73
[MEDIUM]

How do you view events in the current namespace?

A) kubectl get events
B) kubectl describe events
C) kubectl show events
D) kubectl list events

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl get events` lists events in the current namespace. Events provide information about what's happening in the cluster—pod scheduling, image pulls, container starts, errors, etc. Add `--sort-by=.metadata.creationTimestamp` to sort by time (note: `.lastTimestamp` is deprecated in events.k8s.io/v1).

**Source:** [Events | Kubernetes](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/event-v1/)

</details>

---

### Question 74
[MEDIUM-HARD]

What types of events does Kubernetes generate?

A) Info and Error only
B) Normal and Warning
C) Debug, Info, and Error
D) Low, Medium, and High

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes events have two types: Normal (informational, things working as expected) and Warning (something unexpected but not necessarily an error). There's no Error type—problems are reported as Warning events with appropriate messages.

**Source:** [Events | Kubernetes](https://kubernetes.io/docs/reference/kubernetes-api/cluster-resources/event-v1/)

</details>

---

## Context Switching and Multi-Cluster

### Question 75
[HARD]

How do you run a kubectl command against a different context without switching?

A) kubectl --context=other-context get pods
B) kubectl --cluster=other-context get pods
C) kubectl -c other-context get pods
D) kubectl @other-context get pods

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The `--context` flag allows running commands against a specific context without changing the current context. Example: `kubectl --context=production get pods`. This is useful for quick checks or scripts that operate across multiple clusters.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Security Contexts

### Question 76
[MEDIUM-HARD]

What is a Security Context in Kubernetes?

A) RBAC configuration
B) Pod/container-level security settings
C) Network security rules
D) Authentication settings

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Security Context defines privilege and access control settings for Pods and containers. It includes settings like runAsUser, runAsGroup, fsGroup, capabilities, readOnlyRootFilesystem, and allowPrivilegeEscalation. It's set in pod.spec.securityContext or container.securityContext.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 77
[HARD]

What is the difference between `readOnlyRootFilesystem` and `allowPrivilegeEscalation`?

A) They control the same thing
B) readOnlyRootFilesystem prevents writes; allowPrivilegeEscalation prevents gaining privileges
C) readOnlyRootFilesystem is for pods; allowPrivilegeEscalation is for containers
D) Both prevent privilege escalation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `readOnlyRootFilesystem: true` makes the container's root filesystem read-only, preventing writes. `allowPrivilegeEscalation: false` prevents processes from gaining more privileges than their parent (blocks setuid binaries). Both are security best practices but control different aspects.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 78
[MEDIUM-HARD]

What capability is needed for a container to bind to ports below 1024?

A) CAP_PORT_BIND
B) CAP_NET_BIND_SERVICE
C) CAP_LOW_PORT
D) CAP_PRIVILEGED

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `NET_BIND_SERVICE` capability allows binding to privileged ports (below 1024). Without running as root or this capability, containers cannot listen on ports like 80 or 443. Adding only this capability is better than running privileged.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

## ConfigMaps and Secrets Administration

### Question 79
[MEDIUM-HARD]

How do you create a ConfigMap from a file?

A) kubectl create configmap my-config --from-file=config.txt
B) kubectl add configmap my-config --file=config.txt
C) kubectl configmap create my-config --data-file=config.txt
D) kubectl new configmap my-config --source=config.txt

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl create configmap my-config --from-file=config.txt` creates a ConfigMap with the file name as key and contents as value. Use `--from-file=key=file` to specify a custom key name. Multiple `--from-file` flags can be used.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 80
[HARD]

What happens when a ConfigMap mounted as a volume is updated?

A) Changes never propagate
B) Changes propagate automatically (with some delay)
C) The pod must be restarted
D) The container crashes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ConfigMaps mounted as volumes are updated automatically (kubelet sync period + cache propagation delay). The total delay can be up to the kubelet sync period (default 1 minute) plus the ConfigMap cache TTL (default 1 minute), so up to ~2 minutes in total. ConfigMaps used as environment variables don't update—the pod must be restarted. The application must also re-read the files.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 81
[HARD]

How do you enable encryption at rest for Secrets?

A) kubectl encrypt secrets
B) Configure EncryptionConfiguration on kube-apiserver
C) Set secret.encrypted: true
D) Use a special secret type

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Encryption at rest requires configuring an EncryptionConfiguration file and passing it to kube-apiserver via `--encryption-provider-config`. This encrypts secrets before storing in etcd. Providers include aescbc, aesgcm, and KMS.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

## Namespaced vs Cluster-scoped Resources

### Question 82
[MEDIUM-HARD]

Which of these is a cluster-scoped resource?

A) Pod
B) Service
C) PersistentVolume
D) ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** PersistentVolumes are cluster-scoped—they exist independently of namespaces and can be claimed by PersistentVolumeClaims from any namespace. Pods, Services, and ConfigMaps are all namespaced resources.

**Source:** [Persistent Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

</details>

---

## Field Selectors

### Question 83
[MEDIUM-HARD]

What is a field selector in kubectl?

A) A way to select specific output fields
B) A way to filter resources by field values
C) A JSONPath expression
D) A label selector alias

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field selectors filter resources by specific field values (not labels). Unlike labels, fields are resource properties. Example: `kubectl get pods --field-selector=status.phase=Running`. Supported fields vary by resource type; metadata.name and metadata.namespace are commonly supported.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 84
[MEDIUM-HARD]

Can field selectors be combined with label selectors?

A) No, only one type can be used
B) Yes, they can be used together
C) Only with certain resource types
D) Only in YAML, not command line

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field selectors (`--field-selector`) and label selectors (`-l` or `--selector`) can be used together. Both conditions must match. Example: `kubectl get pods -l app=nginx --field-selector status.phase=Running` gets running nginx pods.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## API Server Access

### Question 85
[MEDIUM-HARD]

How do you impersonate another user with kubectl?

A) kubectl --user=john get pods
B) kubectl --as=john get pods
C) kubectl --impersonate=john get pods
D) kubectl --sudo=john get pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl --as=john` impersonates the user "john" for that command. This is useful for testing RBAC permissions. You can also use `--as-group=developers` to impersonate group membership. Requires impersonation permissions.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

</details>

---

## Kubectl Plugins

### Question 86
[MEDIUM-HARD]

How does kubectl discover plugins?

A) From a configuration file
B) From the Kubernetes API
C) From executable files named kubectl-* in PATH
D) From a plugin registry

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** kubectl discovers plugins by looking for executable files named `kubectl-<plugin-name>` in your PATH. For example, `kubectl-foo` is invoked as `kubectl foo`. Plugins can be written in any language—they just need to be executable.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 87
[MEDIUM-HARD]

Which command lists installed kubectl plugins?

A) kubectl plugin list
B) kubectl plugins
C) kubectl get plugins
D) kubectl krew list

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl plugin list` shows all discovered plugins (executables matching kubectl-* in PATH). It also shows warnings about plugins with naming conflicts or issues. If using krew, `kubectl krew list` shows krew-managed plugins specifically.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Ephemeral Containers

### Question 88
[HARD]

What command adds an ephemeral debug container to a running pod?

A) kubectl exec -it pod -- debug
B) kubectl debug pod -it --image=busybox
C) kubectl attach pod --debug
D) kubectl add container pod --debug

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl debug <pod> -it --image=busybox` adds an ephemeral container running busybox to the pod. You can use `--target=<container>` to share process namespace with a specific container. The debug container can access the pod's network and volumes.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Resource Versions

### Question 89
[HARD]

What is `resourceVersion` in Kubernetes objects?

A) The API version of the resource
B) A string that identifies the version of the object in etcd
C) The Kubernetes version that created it
D) A semantic version number

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `resourceVersion` is an opaque string that represents the internal version of an object as stored in etcd. It changes on every modification. It's used for optimistic concurrency control—updates can fail if the resourceVersion has changed (conflict).

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 90
[HARD]

What error occurs when updating a resource with a stale resourceVersion?

A) 404 Not Found
B) 409 Conflict
C) 400 Bad Request
D) 403 Forbidden

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When you try to update a resource but someone else modified it first (resourceVersion changed), you get a 409 Conflict error. This implements optimistic concurrency control. The client must fetch the latest version and retry the update.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

## Server-Side Apply

### Question 91
[HARD]

What is a "field manager" in Server-Side Apply?

A) A controller that validates fields
B) An identifier for who manages specific fields
C) A tool for renaming fields
D) A schema validator

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field managers identify who "owns" specific fields in an object. When using SSA, each applier gets a field manager name (default: kubectl). This enables tracking which fields were set by whom, preventing conflicts when multiple managers update the same resource.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

## Debugging and Troubleshooting

### Question 92
[MEDIUM-HARD]

What does `kubectl describe` show that `kubectl get` doesn't?

A) More columns
B) Events and detailed status information
C) YAML format
D) Historical data

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe` provides detailed information including events, conditions, status, and related resources. It's formatted for human reading and troubleshooting. `kubectl get` shows tabular summary data, while describe shows comprehensive details including recent events.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 93
[HARD]

What command shows resource usage by containers in a pod?

A) kubectl describe pod
B) kubectl top pod --containers
C) kubectl stats pod
D) kubectl resources pod

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl top pod <pod-name> --containers` shows CPU and memory usage broken down by container. Without `--containers`, it shows aggregate pod usage. Requires metrics-server to be installed and running.

**Source:** [Resource metrics pipeline | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/)

</details>

---

### Question 94
[HARD]

What does `kubectl debug node/<node-name>` do?

A) Shows node debug information
B) Creates a privileged pod for node-level debugging
C) Enables debug mode on the node
D) Connects to node's kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl debug node/<node-name>` creates a privileged debugging pod with host filesystem access. It mounts the host root filesystem at /host, enabling inspection of node configuration, logs, and system processes. Useful for debugging node-level issues.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Token Management

### Question 95
[HARD]

What is the default expiration for tokens created with `kubectl create token`?

A) 1 hour
B) 24 hours
C) 1 year
D) Never expires

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Tokens created with `kubectl create token` default to 1 hour expiration. You can request longer durations with `--duration`, but the API server may cap/shorten the requested expiration based on `--service-account-max-token-expiration`. Short-lived tokens are more secure as they reduce the window for token theft.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

## Cluster-Info and Diagnostics

### Question 96
[MEDIUM-HARD]

What does `kubectl cluster-info dump` produce?

A) A summary of cluster health
B) Comprehensive diagnostic information for debugging
C) A backup of cluster configuration
D) Network topology diagram

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cluster-info dump` outputs detailed diagnostic information including pod logs from kube-system, events, and resource states. It's useful for troubleshooting and collecting information for bug reports. Output can be saved to a directory with `--output-directory`.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Dry Run Modes

### Question 97
[MEDIUM-HARD]

What is the difference between `--dry-run=client` and `--dry-run=server`?

A) Client is faster, server is more accurate
B) Client validates locally, server validates on the API server
C) They are identical
D) Client is for creates, server is for updates

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--dry-run=client` processes the request client-side without contacting the server (useful for generating YAML). `--dry-run=server` sends the request to the API server for validation but doesn't persist (catches admission webhook rejections, quota violations).

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Final Advanced Topics

### Question 98
[HARD]

What is the purpose of `--cascade=background` vs `--cascade=foreground` in deletion?

A) Background deletes faster
B) Background deletes owner first; foreground deletes dependents first
C) Foreground uses more resources
D) They produce different events

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--cascade=background` (default) deletes the owner immediately while garbage collector deletes dependents asynchronously. `--cascade=foreground` blocks until all dependents are deleted, then deletes the owner. Foreground gives more control over deletion order.

**Source:** [Garbage Collection | Kubernetes](https://kubernetes.io/docs/concepts/architecture/garbage-collection/)

</details>

---

### Question 99
[HARD]

What command shows the differences introduced by changes to a configmap?

A) kubectl diff configmap my-config
B) kubectl diff -f new-configmap.yaml
C) kubectl compare configmap my-config
D) kubectl configmap diff my-config

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl diff -f new-configmap.yaml` shows what would change if you applied the file. It compares the local file against the live cluster state. This works for any resource type, not just ConfigMaps.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 100
[HARD]

What does `kubectl auth whoami` display?

A) Current username only
B) Current user, groups, and authentication info
C) List of all users
D) Password information

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl auth whoami` (available in newer kubectl versions) shows your authenticated identity including username, UID, groups, and extra attributes. This is useful for debugging authentication issues and understanding your effective identity.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

</details>

---

