# Administration - 100 MCQ Questions (Part B)

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Administration
**Difficulty Distribution:** 10% Medium | 20% Medium-Hard | 70% Hard

---

## kubectl Basics

### Question 1
[MEDIUM]

What is the default output format of kubectl commands?

A) JSON
B) YAML
C) Plain text/table
D) XML

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** By default, kubectl commands output in a human-readable plain text table format. You can change this using the `-o` flag to formats like `json`, `yaml`, `wide`, `name`, or custom columns.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 2
[MEDIUM]

What does the `kubectl explain` command do?

A) Shows examples of kubectl usage
B) Displays documentation for resource fields
C) Explains cluster architecture
D) Shows command history

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl explain` provides documentation for resource fields and their structure. For example, `kubectl explain pod.spec.containers` shows the fields available under a Pod's container spec. It's invaluable for understanding resource definitions without leaving the terminal.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 3
[HARD]

What is the purpose of `kubectl apply` compared to `kubectl create`?

A) apply is faster than create
B) apply supports declarative management with updates
C) create supports declarative management
D) They are identical in functionality

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl apply` is used for declarative configuration management. It creates resources if they don't exist and updates them if they do, preserving the desired state. `kubectl create` is imperative and will fail if the resource already exists. Apply tracks changes through annotations for intelligent updates.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 4
[HARD]

Which command shows the differences between a local manifest and the live cluster state?

A) kubectl compare -f file.yaml
B) kubectl diff -f file.yaml
C) kubectl delta -f file.yaml
D) kubectl changes -f file.yaml

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl diff -f file.yaml` shows the differences between the local configuration file and the live cluster state. This is useful for previewing changes before applying them, following infrastructure-as-code best practices.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 5
[HARD]

Which command immediately deletes a Pod without waiting for graceful termination?

A) kubectl delete pod nginx --now
B) kubectl delete pod nginx --force --grace-period=0
C) kubectl delete pod nginx --immediate
D) kubectl delete pod nginx --skip-graceful

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Using `--force --grace-period=0` together forces immediate deletion without waiting for graceful termination. This should be used cautiously as it doesn't allow the Pod to clean up properly. The Pod may continue running momentarily but is immediately removed from the API.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 6
[HARD]

How do you watch resources continuously for changes using kubectl?

A) kubectl get pods --live
B) kubectl get pods --watch
C) kubectl get pods --stream
D) kubectl get pods --continuous

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `--watch` or `-w` flag enables continuous watching of resources. kubectl will keep the connection open and print updates as resources change. This is useful for monitoring deployments, debugging, or observing cluster state changes in real-time.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## kubeconfig and Contexts

### Question 7
[MEDIUM]

What are the three main components of a kubeconfig file?

A) Users, Groups, Permissions
B) Clusters, Contexts, Users
C) Servers, Credentials, Namespaces
D) Endpoints, Tokens, Certificates

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A kubeconfig file contains three main sections: clusters (define server addresses and CA certificates), users (define authentication credentials), and contexts (combine a cluster with a user and optionally a default namespace). Contexts allow easy switching between different cluster/user combinations.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 8
[HARD]

How can you specify a different kubeconfig file for a single command?

A) kubectl --config=/path/to/config get pods
B) kubectl --kubeconfig=/path/to/config get pods
C) kubectl -c /path/to/config get pods
D) kubectl --file=/path/to/config get pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `--kubeconfig` flag allows you to specify an alternative kubeconfig file for that command only. This is useful when managing multiple clusters without modifying your default config or KUBECONFIG environment variable.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 9
[HARD]

When merging multiple kubeconfig files, what happens if the same context name exists in multiple files?

A) An error is thrown
B) The last file wins
C) The first file wins
D) Both contexts are renamed

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When kubeconfig files are merged, the first file in the KUBECONFIG list takes precedence for duplicate entries. If a context, cluster, or user with the same name exists in multiple files, the definition from the first file is used.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 10
[HARD]

How do you set a default namespace for a context?

A) kubectl config set-context --current --namespace=dev
B) kubectl namespace set dev
C) kubectl config default-namespace dev
D) kubectl set namespace dev

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl config set-context --current --namespace=dev` modifies the current context to use "dev" as the default namespace. Subsequent commands will operate in that namespace without requiring the `-n` flag.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Cluster Components

### Question 11
[MEDIUM]

Which component is responsible for storing all cluster data?

A) kube-apiserver
B) etcd
C) kube-controller-manager
D) kube-scheduler

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** etcd is the distributed key-value store that holds all cluster configuration and state data. It's the single source of truth for the cluster. All other components read from and write to etcd through the API server.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

### Question 12
[HARD]

What is the primary function of the kube-controller-manager?

A) Serve the Kubernetes API
B) Run controller loops that regulate cluster state
C) Schedule pods to nodes
D) Manage network routing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-controller-manager runs various controller loops (Node Controller, Replication Controller, Endpoints Controller, etc.) that watch the shared state of the cluster and make changes to move the current state toward the desired state.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

### Question 13
[HARD]

What is the role of kube-proxy?

A) Proxy requests to the API server
B) Maintain network rules for Service connectivity
C) Load balance external traffic
D) Secure inter-node communication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-proxy runs on each node and maintains network rules that allow network communication to Pods from inside or outside the cluster. It implements the Kubernetes Service concept, typically using iptables, IPVS, or other mechanisms.

**Source:** [kube-proxy | Kubernetes](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/)

</details>

---

### Question 14
[HARD]

Which component validates and configures data for API objects?

A) kubelet
B) kube-apiserver
C) kube-controller-manager
D) etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-apiserver is the front end of the Kubernetes control plane. It validates and configures data for API objects like Pods, Services, and controllers. It processes REST operations, validates them, and updates the state in etcd.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

### Question 15
[HARD]

Which controller is responsible for maintaining the correct number of pod replicas?

A) Node Controller
B) Endpoint Controller
C) ReplicaSet Controller
D) Namespace Controller

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The ReplicaSet Controller (and Replication Controller for older ReplicationController resources) ensures that the specified number of pod replicas are running at any given time. It creates or deletes pods as needed to match the desired replica count.

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

### Question 16
[HARD]

What port does the kube-apiserver typically listen on?

A) 8080
B) 443
C) 6443
D) 2379

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kube-apiserver typically listens on port 6443 for HTTPS traffic. Port 2379 is used by etcd. Port 8080 was historically used for insecure API access but has been completely removed since Kubernetes 1.20 (the `--insecure-port` flag was deprecated and removed).

**Source:** [Cluster Components | Kubernetes](https://kubernetes.io/docs/concepts/overview/components/)

</details>

---

## Namespaces

### Question 17
[MEDIUM]

What happens to resources when their namespace is deleted?

A) Resources move to the default namespace
B) Resources are orphaned
C) All resources in the namespace are deleted
D) Deletion fails until namespace is empty

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a namespace is deleted, all resources within that namespace are also deleted. Kubernetes uses cascading deletion for namespaces—there's no need to manually delete resources first, and resources cannot be moved to another namespace.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 18
[HARD]

What is the purpose of the `kube-public` namespace?

A) For resources that should be publicly accessible
B) For resources readable by all users, including unauthenticated
C) For public-facing services only
D) For documentation and help resources

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kube-public` namespace is readable by all users (including unauthenticated ones). It's mostly used for cluster information that should be publicly accessible, like the cluster-info ConfigMap used during bootstrapping with kubeadm.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 19
[HARD]

What is the purpose of the `kube-node-lease` namespace?

A) To store node certificates
B) To hold Lease objects for node heartbeats
C) To manage node scheduling
D) To store node configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kube-node-lease` namespace contains Lease objects associated with each node. These leases are used for node heartbeats, which is more scalable than updating Node status for heartbeats. The kubelet updates its lease more frequently than node status, reducing load on the control plane.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

### Question 20
[HARD]

What constraint applies to namespace names?

A) Must be less than 64 characters
B) Must follow DNS label standards (lowercase, alphanumeric, hyphens)
C) Can contain underscores and dots
D) Must start with a letter

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Namespace names must be valid DNS labels: lowercase alphanumeric characters or hyphens, must start with an alphanumeric character, and be at most 63 characters. This is because namespace names can be used in DNS names for services.

**Source:** [Namespaces | Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

</details>

---

## Labels and Selectors

### Question 21
[MEDIUM]

Which selector type allows equality-based matching only?

A) Set-based selectors
B) Equality-based selectors
C) matchLabels
D) matchExpressions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Equality-based selectors (also called label selectors) support `=`, `==`, and `!=` operators for exact matching. Set-based selectors (matchExpressions) support `In`, `NotIn`, `Exists`, and `DoesNotExist` operators for more flexible matching.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 22
[HARD]

How do you filter pods by label using kubectl?

A) kubectl get pods --label=app:nginx
B) kubectl get pods -l app=nginx
C) kubectl get pods --filter app=nginx
D) kubectl get pods --select app=nginx

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `-l` or `--selector` flag filters resources by label. The syntax is `kubectl get pods -l app=nginx`. You can use multiple conditions with commas (AND logic) like `-l app=nginx,tier=frontend`.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 23
[HARD]

What happens when you modify a Deployment's selector after creation?

A) The selector updates and matches existing pods
B) It's blocked by the API server (selector is immutable)
C) Old pods are deleted and new ones created
D) The change is silently ignored

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The selector field in a Deployment's spec is immutable after creation. Attempting to change it results in an error. This prevents breaking the relationship between the Deployment and its ReplicaSets. You must delete and recreate the Deployment to change the selector.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 24
[HARD]

How do you select resources that have a specific label key regardless of its value?

A) kubectl get pods -l app
B) kubectl get pods -l app=*
C) kubectl get pods -l 'app exists'
D) kubectl get pods -l app!=''

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Using just the label key without a value (e.g., `-l app`) selects all resources that have that label key, regardless of value. This is equivalent to the `Exists` operator in set-based selectors.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 25
[HARD]

What is the maximum length allowed for a label key?

A) 32 characters
B) 63 characters
C) 253 characters for prefix + 63 for name
D) Unlimited

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Label keys have two segments: an optional prefix and a name. The name must be 63 characters or less. If a prefix is specified (like `app.kubernetes.io/`), it must be a valid DNS subdomain (max 253 characters) and is separated from the name by a slash.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Annotations

### Question 26
[HARD]

Which is a valid use case for annotations?

A) Selecting pods for a Service
B) Storing the git commit hash that created a resource
C) Grouping resources by environment
D) Defining replica counts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Annotations are perfect for storing metadata like git commit hashes, build timestamps, release versions, tool configuration, or links to documentation. Unlike labels, annotations aren't used for selection, making them suitable for data that doesn't need to be queryable.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 27
[HARD]

How do you add an annotation to a resource using kubectl?

A) kubectl label pod nginx description="Web server"
B) kubectl annotate pod nginx description="Web server"
C) kubectl metadata pod nginx description="Web server"
D) kubectl tag pod nginx description="Web server"

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl annotate` is used to add, update, or remove annotations. The syntax is similar to `kubectl label`. To remove an annotation, use a trailing hyphen: `kubectl annotate pod nginx description-`.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Resource Management

### Question 28
[MEDIUM]

What is the difference between resource requests and limits?

A) Requests are hard limits, limits are soft limits
B) Requests are for scheduling, limits are hard maximums
C) They are interchangeable terms
D) Requests apply to memory, limits apply to CPU

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Requests are used by the scheduler to determine which node to place a Pod on—the node must have at least that much available. Limits are hard maximums enforced by the kubelet—containers cannot exceed their limits (CPU is throttled, memory causes OOM kill).

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 29
[HARD]

What happens when a container tries to use more memory than its limit?

A) The container is throttled
B) The container is OOM killed
C) The request is queued
D) Memory is swapped to disk

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a container exceeds its memory limit, it's terminated by the OOM (Out of Memory) killer. If the Pod's restart policy allows, the container is restarted. Unlike CPU, memory is not compressible and cannot be throttled.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 30
[HARD]

What is a LimitRange used for?

A) To set default resource limits for a cluster
B) To define min/max and default resources for a namespace
C) To limit the number of pods in a namespace
D) To control network bandwidth limits

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** LimitRange defines minimum, maximum, and default resource requests/limits for containers in a namespace. If a Pod doesn't specify resources, defaults from LimitRange are applied. It can also enforce minimum/maximum constraints and default values per container or Pod.

**Source:** [Limit Ranges | Kubernetes](https://kubernetes.io/docs/concepts/policy/limit-range/)

</details>

---

### Question 31
[HARD]

What QoS class is assigned to a Pod with requests equal to limits for all containers?

A) BestEffort
B) Burstable
C) Guaranteed
D) Reserved

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Pods with requests exactly equal to limits for all containers (and for both CPU and memory) get the "Guaranteed" QoS class. These pods are least likely to be evicted during resource pressure. "Burstable" means some limits/requests, "BestEffort" means no limits/requests.

**Source:** [Resource Quotas | Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/)

</details>

---

### Question 32
[HARD]

What command shows resource usage of pods?

A) kubectl get pods --resources
B) kubectl top pods
C) kubectl describe pods --usage
D) kubectl resources pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl top pods` shows current CPU and memory usage for pods. This requires the metrics-server to be installed in the cluster. You can also use `kubectl top nodes` for node-level metrics.

**Source:** [kubectl Reference | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## RBAC (Role-Based Access Control)

### Question 33
[MEDIUM]

What are the four main RBAC resources in Kubernetes?

A) Users, Groups, Permissions, Policies
B) Roles, ClusterRoles, RoleBindings, ClusterRoleBindings
C) Accounts, Credentials, Access, Controls
D) Subjects, Objects, Actions, Targets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes RBAC uses four main resources: Role (namespaced permissions), ClusterRole (cluster-wide permissions), RoleBinding (grants Role to subjects in a namespace), and ClusterRoleBinding (grants ClusterRole cluster-wide). Users, groups, and service accounts are subjects, not RBAC resources.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 34
[HARD]

Can a RoleBinding reference a ClusterRole?

A) No, it must reference a Role
B) Yes, it grants the ClusterRole's permissions within that namespace only
C) Yes, it grants cluster-wide permissions
D) Only if the ClusterRole is marked as "bindable"

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A RoleBinding can reference a ClusterRole, which grants the ClusterRole's permissions but only within the RoleBinding's namespace. This is useful for reusing common permission sets across namespaces without duplicating Roles.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 35
[HARD]

Which verb allows creating new resources?

A) add
B) write
C) create
D) new

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** RBAC uses specific verbs: `create`, `get`, `list`, `watch`, `update`, `patch`, `delete`, and `deletecollection`. The verb `create` allows creating new resources. There's no `add`, `write`, or `new` verb in Kubernetes RBAC.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 36
[HARD]

How do you check if a user can perform a specific action?

A) kubectl check-permission
B) kubectl auth can-i
C) kubectl rbac verify
D) kubectl access check

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl auth can-i` checks if the current user (or specified user/serviceaccount) can perform an action. Examples: `kubectl auth can-i create pods`, `kubectl auth can-i delete deployments --as=john`. Useful for debugging RBAC issues.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 37
[HARD]

Which command lists all RoleBindings in all namespaces?

A) kubectl get rolebindings --all
B) kubectl get rolebindings -A
C) kubectl get rolebindings --cluster
D) kubectl get bindings -A

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl get rolebindings -A` or `--all-namespaces` lists RoleBindings across all namespaces. Note that ClusterRoleBindings are separate and listed with `kubectl get clusterrolebindings`.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

## Node Management

### Question 38
[MEDIUM]

What does the `kubectl cordon` command do?

A) Deletes a node from the cluster
B) Marks a node as unschedulable
C) Restarts all pods on a node
D) Updates node labels

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cordon` marks a node as unschedulable, preventing new pods from being scheduled on it. Existing pods continue to run. This is useful when preparing for maintenance. Use `kubectl uncordon` to make the node schedulable again.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 39
[HARD]

What flag allows draining a node with pods that have local storage?

A) --force
B) --delete-local-data
C) --delete-emptydir-data
D) --ignore-local

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** `--delete-emptydir-data` (previously `--delete-local-data`) allows draining a node even if pods are using emptyDir volumes. Without this flag, drain refuses to evict such pods because their local data would be lost.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 40
[HARD]

What are the three taint effects?

A) Hard, Soft, Prefer
B) NoSchedule, PreferNoSchedule, NoExecute
C) Block, Warn, Allow
D) Reject, Defer, Accept

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The three taint effects are: `NoSchedule` (new pods without toleration won't schedule), `PreferNoSchedule` (scheduler avoids the node but will use it if necessary), and `NoExecute` (new pods won't schedule AND existing pods without toleration are evicted).

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 41
[HARD]

What happens when a NoExecute taint is added to a node with running pods?

A) Nothing, pods continue running
B) Pods without matching toleration are immediately evicted
C) Pods without toleration are evicted after tolerationSeconds
D) B or C depending on whether tolerationSeconds is specified

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** When NoExecute taint is added, pods without matching tolerations are evicted. If a pod has a matching toleration with `tolerationSeconds` specified, it will be evicted after that duration. Without `tolerationSeconds`, the pod remains indefinitely.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

### Question 42
[HARD]

How do you view the taints on a node?

A) kubectl get taints node worker1
B) kubectl describe node worker1
C) kubectl get node worker1 -o yaml
D) Both B and C

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Node taints can be viewed using `kubectl describe node` (shows in the Taints section) or `kubectl get node -o yaml` (shows in spec.taints). There's no direct `kubectl get taints` command.

**Source:** [Nodes | Kubernetes](https://kubernetes.io/docs/concepts/architecture/nodes/)

</details>

---

## etcd Administration

### Question 43
[HARD]

What port does etcd typically listen on for client connections?

A) 6443
B) 2379
C) 2380
D) 10250

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** etcd listens on port 2379 for client connections (from API server) and port 2380 for peer communication (between etcd cluster members). Port 6443 is for the API server, and 10250 is for kubelet.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

### Question 44
[HARD]

What command is used to create an etcd snapshot?

A) kubectl backup etcd
B) etcdctl snapshot save
C) etcdctl backup create
D) kubectl etcd snapshot

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `etcdctl snapshot save <filename>` creates a backup of etcd data. You must provide the correct certificates and endpoints. Example: `ETCDCTL_API=3 etcdctl snapshot save backup.db --endpoints=https://127.0.0.1:2379 --cacert=... --cert=... --key=...`

**Source:** [Backing up an etcd cluster | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster)

</details>

---

### Question 45
[HARD]

What tool is used to restore an etcd cluster from a snapshot?

A) kubectl restore etcd
B) etcdctl snapshot restore
C) etcd-restore
D) kubeadm etcd restore

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `etcdctl snapshot restore` restores etcd data from a snapshot file. This creates a new data directory that can be used to start an etcd member. Each member in a cluster must restore from the same snapshot to reform the cluster.

**Source:** [Backing up an etcd cluster | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster)

</details>

---

### Question 46
[HARD]

Where is etcd data stored by default in a kubeadm cluster?

A) /etc/kubernetes/etcd
B) /var/lib/etcd
C) /opt/etcd/data
D) /data/etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In kubeadm-based clusters, etcd data is typically stored in `/var/lib/etcd`. This directory contains the etcd database (member directory with WAL and snap subdirectories). This location is critical for backups.

**Source:** [Operating etcd clusters for Kubernetes | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

</details>

---

## Cluster Upgrades

### Question 47
[HARD]

How many minor versions can kubelet lag behind the API server (Kubernetes 1.28+)?

A) 1 minor version
B) 2 minor versions
C) 3 minor versions
D) No version lag allowed

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Since Kubernetes 1.28, the version skew policy allows kubelet to be up to 3 minor versions older than kube-apiserver (previously it was 2 minor versions for kubelet < 1.25). For example, if apiserver is 1.35, kubelet can be 1.35, 1.34, 1.33, or 1.32. This enables multi-version upgrades in a single cycle.

**Source:** [Version Skew Policy | Kubernetes](https://kubernetes.io/releases/version-skew-policy/)

</details>

---

### Question 48
[HARD]

What is the first step before upgrading a kubeadm cluster?

A) Upgrade kubelet on all nodes
B) Run kubeadm upgrade plan
C) Upgrade kubeadm package itself
D) Cordon all nodes

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Before running upgrade commands, you must first upgrade the kubeadm package to the target version. Then `kubeadm upgrade plan` checks the current state and shows available upgrades. Finally, `kubeadm upgrade apply` performs the actual upgrade.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

### Question 49
[HARD]

What is the maximum supported version skew between kube-controller-manager and kube-apiserver?

A) 0 minor versions (must match)
B) 1 minor version
C) 2 minor versions
D) 3 minor versions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-controller-manager, kube-scheduler, and cloud-controller-manager must not be newer than the apiserver and can be at most 1 minor version older. During upgrades, apiserver is upgraded first, followed by other control plane components.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

### Question 50
[HARD]

When upgrading a multi-master cluster with kubeadm, what command is used on the first control plane node?

A) kubeadm upgrade apply
B) kubeadm upgrade node
C) kubeadm upgrade plan
D) kubeadm upgrade init

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** In a multi-master kubeadm cluster, the first control plane node is upgraded with `kubeadm upgrade apply`, which performs the full upgrade including updating cluster configuration. Subsequent control plane nodes use `kubeadm upgrade node`, which only upgrades the local kubelet configuration. All control plane nodes must be upgraded before worker nodes.

**Source:** [Upgrading kubeadm clusters | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

</details>

---

## API and Versioning

### Question 51
[HARD]

What does the API group contain in Kubernetes?

A) Only core resources like pods and services
B) Related resources grouped by functionality
C) Deprecated resources
D) External custom resources only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** API groups organize related resources by functionality. For example, `apps` group contains Deployments and StatefulSets, `batch` contains Jobs and CronJobs. Core resources (pods, services) are in the legacy group (empty string). Groups enable independent versioning.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 52
[HARD]

What is the difference between core API group and named API groups?

A) Core is internal only
B) Core resources use apiVersion without group (e.g., "v1")
C) Named groups are for third-party resources only
D) Core is deprecated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Core API resources (Pods, Services, ConfigMaps, etc.) use a "legacy" group with no name, so their apiVersion is just "v1" instead of "group/v1". Named groups like "apps/v1" or "batch/v1" explicitly include the group name in the apiVersion.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 53
[HARD]

What happens when a resource's API version is deprecated?

A) The resource stops working immediately
B) The resource continues working but may be removed in future versions
C) The resource is automatically migrated
D) An error is thrown for all operations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deprecated APIs continue to work but generate warnings. Kubernetes deprecation policy: beta APIs are supported for at least 9 months or 3 releases (whichever is longer), GA/stable APIs for at least 12 months or 3 releases. Users should migrate to newer API versions before removal.

**Source:** [Kubernetes Deprecation Policy | Kubernetes](https://kubernetes.io/docs/reference/using-api/deprecation-policy/)

</details>

---

### Question 54
[HARD]

What is the purpose of admission controllers in the API request flow?

A) To authenticate users
B) To intercept and potentially modify or reject requests
C) To route requests to the correct component
D) To log API requests

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Admission controllers are plugins that intercept API requests after authentication and authorization but before persistence. They can modify (mutating) or reject (validating) requests. Examples include NamespaceLifecycle, LimitRanger, ServiceAccount, NodeRestriction, and ResourceQuota.

**Source:** [Admission Controllers Reference | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

---

### Question 55
[HARD]

In what order are admission controllers processed?

A) Alphabetically by name
B) Mutating first, then validating
C) Validating first, then mutating
D) Random order

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Mutating admission controllers/webhooks run first and may modify the object. Then validating controllers/webhooks run and can only accept or reject the (potentially modified) request. This order ensures validating webhooks see the final version of the object.

**Source:** [Admission Controllers Reference | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

---

## Logging and Monitoring

### Question 56
[HARD]

How do you view logs from a previous container instance?

A) kubectl logs pod-name --old
B) kubectl logs pod-name --previous
C) kubectl logs pod-name --history
D) kubectl logs pod-name --last

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl logs --previous` shows logs from the previous container instance. This is useful when a container has crashed and restarted—you can see what happened before the crash. Also useful with `-p` shorthand.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 57
[HARD]

Which metrics server is commonly used for `kubectl top` commands?

A) Prometheus
B) metrics-server
C) Heapster
D) Grafana

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** metrics-server is the lightweight, in-cluster component that provides resource metrics (CPU/memory) for kubectl top and Horizontal Pod Autoscaler. Prometheus is a more comprehensive monitoring solution but isn't used directly by kubectl top.

**Source:** [Resource metrics pipeline | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/)

</details>

---

### Question 58
[HARD]

What happens to container logs when a Pod is deleted?

A) Logs are archived automatically
B) Logs become inaccessible via kubectl logs
C) Logs remain indefinitely
D) Logs are moved to a backup location

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Container logs are stored on the node's filesystem and retained based on kubelet log rotation settings. When a Pod is deleted, `kubectl logs` becomes unavailable, but log files may persist on the node until garbage collected by the container runtime or removed by log rotation. This is why cluster-level logging is important for log retention.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

### Question 59
[HARD]

What is a sidecar container pattern for logging?

A) A container that only collects metrics
B) A container in the same Pod that processes/ships application logs
C) A DaemonSet that collects logs from all nodes
D) A separate Pod dedicated to logging

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The sidecar pattern uses an additional container in the same Pod to handle log processing/shipping. The sidecar can read log files written by the main container (via shared volume) and forward them to a logging backend. This keeps the main application simple.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

---

## Service Accounts

### Question 60
[HARD]

How do you specify a custom ServiceAccount for a Pod?

A) In the Pod's metadata.serviceAccount
B) In the Pod's spec.serviceAccountName
C) In the Pod's spec.identity
D) In the Pod's annotations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Set `spec.serviceAccountName` in the Pod specification to use a custom ServiceAccount. Example: `spec: serviceAccountName: my-sa`. The ServiceAccount must exist in the same namespace as the Pod.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 61
[HARD]

How do you prevent automatic mounting of ServiceAccount tokens?

A) Delete the default ServiceAccount
B) Set automountServiceAccountToken: false
C) Use a network policy
D) Remove RBAC permissions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Set `automountServiceAccountToken: false` in either the ServiceAccount spec (applies to all pods using it) or the Pod spec (applies to that pod only). This prevents the token from being mounted, useful for pods that don't need API access.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 62
[MEDIUM-HARD]

Which command creates a ServiceAccount?

A) kubectl add serviceaccount my-sa
B) kubectl create serviceaccount my-sa
C) kubectl new sa my-sa
D) kubectl serviceaccount create my-sa

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl create serviceaccount my-sa` or `kubectl create sa my-sa` creates a new ServiceAccount. You can also specify the namespace with `-n`. ServiceAccounts can also be created declaratively using YAML manifests.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

## kubectl Advanced Usage

### Question 63
[HARD]

How do you sort kubectl output by a specific field?

A) kubectl get pods --sort=metadata.name
B) kubectl get pods --sort-by=.metadata.name
C) kubectl get pods --order-by=name
D) kubectl get pods | sort

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--sort-by=.field.path` sorts output by the specified field. Common uses include sorting by creation timestamp (`--sort-by=.metadata.creationTimestamp`) or resource usage. The field path uses JSONPath syntax.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 64
[MEDIUM-HARD]

How do you execute a command inside a running container?

A) kubectl run -it pod-name -- /bin/bash
B) kubectl exec -it pod-name -- /bin/bash
C) kubectl shell pod-name
D) kubectl connect pod-name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl exec -it pod-name -- /bin/bash` opens an interactive shell in a container. `-i` keeps stdin open, `-t` allocates a TTY. For multi-container pods, use `-c container-name`. The `--` separates kubectl args from the command.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 65
[MEDIUM-HARD]

How do you copy files between local machine and a Pod?

A) kubectl scp local-file pod:/path
B) kubectl cp local-file pod:/path
C) kubectl copy local-file pod:/path
D) kubectl transfer local-file pod:/path

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cp` copies files to/from containers. Syntax: `kubectl cp local-file pod:/remote/path` or `kubectl cp pod:/remote/path local-file`. For specific containers use `-c container-name`. Requires tar in the container.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 66
[MEDIUM-HARD]

Which flag makes kubectl wait for a resource to reach a certain condition?

A) kubectl get pods --until=Ready
B) kubectl wait --for=condition=Ready pods
C) kubectl get pods --condition=Ready
D) kubectl watch pods --ready

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl wait --for=condition=Ready pod/nginx` blocks until the specified condition is met. Supports conditions like Ready, Complete (for Jobs), and also `--for=delete` to wait for deletion. Useful in scripts and CI/CD pipelines.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Advanced Administration

### Question 67
[MEDIUM-HARD]

What does `minAvailable: 2` in a PodDisruptionBudget mean?

A) At least 2 pods must be created
B) At least 2 pods must remain running during disruptions
C) Maximum 2 pods can be disrupted
D) 2 pods will be restarted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `minAvailable: 2` means at least 2 pods matching the selector must remain available during voluntary disruptions. If disrupting a pod would bring the count below 2, the disruption is blocked. Can be a number or percentage.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 68
[MEDIUM-HARD]

What happens when a high-priority Pod cannot be scheduled?

A) It waits indefinitely
B) It may preempt lower-priority Pods
C) It's automatically deleted
D) It scales down other deployments

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a high-priority Pod can't be scheduled due to resource constraints, the scheduler may preempt (evict) lower-priority Pods to make room. Preemption can evict pods regardless of PodDisruptionBudgets (PDBs apply to voluntary disruptions, not scheduler preemption), though it honors graceful termination periods.

**Source:** [Pod Priority and Preemption | Kubernetes](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/)

</details>

---

### Question 69
[MEDIUM-HARD]

What is a RuntimeClass used for?

A) To specify the Java runtime version
B) To select different container runtimes
C) To define class-based resource limits
D) To categorize runtime errors

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RuntimeClass allows selecting different container runtime configurations (handlers) for Pods. This is useful when you have multiple runtimes (like containerd and gVisor/Kata) and want to run specific workloads with specific runtimes for isolation or compatibility.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 70
[HARD]

What is an owner reference used for?

A) To track who created a resource
B) To establish parent-child relationships for garbage collection
C) To define RBAC ownership
D) To log resource changes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Owner references create parent-child relationships between resources. When a parent (owner) is deleted, dependent resources with owner references are automatically garbage collected. For example, ReplicaSets own Pods, and Deployments own ReplicaSets.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 71
[HARD]

What flag prevents cascading deletion when deleting a resource?

A) --no-cascade
B) --cascade=false
C) --orphan
D) --cascade=orphan

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** `--cascade=orphan` (formerly `--cascade=false`) deletes the owner but leaves dependents running by removing their owner references. This "orphans" the dependent resources. `--cascade=background` (default) or `--cascade=foreground` are the other options.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Lease Objects and Leader Election

### Question 72
[HARD]

How do kubelets use Lease objects?

A) To request node resources
B) To report node heartbeats efficiently
C) To lease IP addresses
D) To schedule pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Each node has a Lease object in the kube-node-lease namespace. Kubelets update their lease regularly (default every 10 seconds) as a heartbeat. This is more scalable than updating the full Node status object, reducing load on etcd.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Events

### Question 73
[MEDIUM-HARD]

How long are events retained by default in Kubernetes?

A) 30 minutes
B) 1 hour
C) 1 day
D) 1 week

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Events are retained for 1 hour by default (controlled by `--event-ttl` on the API server). Events are meant for debugging recent issues, not long-term storage. For persistent event storage, use external logging solutions.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Context Switching and Multi-Cluster

### Question 74
[MEDIUM-HARD]

Which kubectl command switches to a different context?

A) kubectl context switch my-context
B) kubectl config use-context my-context
C) kubectl set-context my-context
D) kubectl switch my-context

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl config use-context my-context` switches the current context to the specified one. To change the default namespace for the current context, use `kubectl config set-context --current --namespace=my-namespace`. These are the native kubectl commands for context and namespace management.

**Source:** [Configure Access to Multiple Clusters | Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)

</details>

---

### Question 75
[MEDIUM-HARD]

What does `kubectl config set-context` do?

A) Switches to a different context
B) Creates or modifies a context entry
C) Lists all contexts
D) Validates context configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl config set-context` creates or modifies a context entry in kubeconfig. You can set the cluster, user, and namespace for a context. Example: `kubectl config set-context dev --cluster=dev-cluster --user=dev-user --namespace=development`.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Security Contexts

### Question 76
[MEDIUM-HARD]

What does `runAsNonRoot: true` enforce?

A) Container must run as root
B) Container must run as a non-root user
C) Container cannot access root filesystem
D) Container cannot use privileged mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `runAsNonRoot: true` ensures the container runs with a non-root user (UID != 0). If the container image tries to run as root, the container fails to start. This is a security best practice to limit potential damage from container breakouts.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 77
[HARD]

What are Linux capabilities in the context of Kubernetes?

A) Hardware capabilities of nodes
B) Fine-grained privileges that can be added or dropped
C) Container resource limits
D) Network capabilities

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Linux capabilities break down root privileges into fine-grained units. Containers can drop unnecessary capabilities (drop: ALL) or add specific ones (add: NET_BIND_SERVICE). This follows the principle of least privilege—only granting what's needed.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

## ConfigMaps and Secrets Administration

### Question 78
[MEDIUM]

What is the maximum size of a ConfigMap or Secret?

A) 256 KiB
B) 1 MiB
C) 10 MiB
D) No limit

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ConfigMaps and Secrets are limited to 1 MiB (1,048,576 bytes) in size. This is because they're stored in etcd, which has object size limits. For larger data, consider using volumes or external storage solutions.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 79
[HARD]

What is the difference between `--from-file` and `--from-literal` when creating ConfigMaps?

A) from-file is for binary, from-literal is for text
B) from-file reads from files, from-literal takes inline values
C) from-file creates mounted volumes, from-literal creates env vars
D) No difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--from-file` reads content from files (key is filename, value is content). `--from-literal` takes inline key=value pairs directly in the command (e.g., `--from-literal=key1=value1`). Both can be combined in one command.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

---

### Question 80
[MEDIUM-HARD]

How are Secrets encoded in Kubernetes?

A) Encrypted by default
B) Base64 encoded (not encrypted)
C) Plain text
D) SHA-256 hashed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Secret data is base64 encoded, NOT encrypted by default. This encoding is for handling binary data, not security. For encryption at rest, you must enable encryption configuration for etcd. Base64 is easily decoded and provides no security.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

## Namespaced vs Cluster-scoped Resources

### Question 81
[MEDIUM-HARD]

Which command lists only cluster-scoped (non-namespaced) resources?

A) kubectl api-resources --cluster-scoped
B) kubectl api-resources --namespaced=false
C) kubectl get cluster-resources
D) kubectl api-resources --global

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl api-resources --namespaced=false` lists cluster-scoped resources that aren't bound to namespaces. Examples include Nodes, PersistentVolumes, ClusterRoles, and Namespaces themselves. Use `--namespaced=true` for namespace-scoped resources.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 82
[HARD]

Why are CustomResourceDefinitions cluster-scoped?

A) For security reasons
B) They define types available across all namespaces
C) Technical limitation
D) They were designed before namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CRDs are cluster-scoped because they define new resource types that should be consistently available across the entire cluster. Once defined, custom resources of that type can be created in any namespace (if the CRD specifies namespaced scope).

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Field Selectors

### Question 83
[HARD]

Which field selector gets all pods NOT running on a specific node?

A) kubectl get pods --field-selector spec.nodeName!=node1
B) kubectl get pods --field-selector status.node!=node1
C) kubectl get pods -l node!=node1
D) kubectl get pods --exclude-node=node1

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `--field-selector spec.nodeName!=node1` filters pods not scheduled on node1. Field selectors support = and != operators. The `spec.nodeName` field contains the node where the pod is scheduled. Note: unscheduled pods have empty nodeName.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## API Server Access

### Question 84
[HARD]

What is the purpose of the `kubectl auth reconcile` command?

A) Synchronize RBAC rules from files
B) Verify user authentication
C) Reset authentication credentials
D) Check cluster connectivity

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** `kubectl auth reconcile -f rbac.yaml` creates or updates RBAC resources from a file, reconciling differences intelligently. It's useful for managing RBAC as code, supporting ClusterRoles, Roles, ClusterRoleBindings, and RoleBindings.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 85
[HARD]

What permission is needed to impersonate another user?

A) admin role
B) impersonate verb on users resource
C) cluster-admin only
D) sudo permission

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To impersonate users, you need the `impersonate` verb on the `users` resource in the RBAC rules. Similarly, impersonating groups requires `impersonate` on `groups`, and impersonating service accounts requires it on `serviceaccounts`.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)

</details>

---

## Kubectl Plugins

### Question 86
[MEDIUM-HARD]

What tool is commonly used to manage kubectl plugins?

A) kubectl plugin install
B) krew
C) helm
D) apt-get

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Krew is the plugin manager for kubectl. It provides a centralized repository of plugins and handles installation, updates, and removal. Install plugins with `kubectl krew install <plugin>`. Krew itself is installed as a kubectl plugin.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Ephemeral Containers

### Question 87
[HARD]

What are ephemeral containers used for?

A) Temporary storage
B) Debugging running pods without restart
C) Auto-scaling workloads
D) Temporary network connections

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ephemeral containers are temporary containers added to existing pods for debugging purposes. They're useful for troubleshooting distroless or minimal images that lack debugging tools. Added via `kubectl debug` command without restarting the pod.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 88
[HARD]

Can ephemeral containers be removed from a pod?

A) Yes, using kubectl delete ephemeral-container
B) Yes, they auto-remove after exit
C) No, they remain until pod deletion
D) Yes, using kubectl debug --remove

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Ephemeral containers cannot be removed from a pod once added—they exist until the pod is deleted. However, they can be stopped (exited). This is because the ephemeral containers list is append-only; you can add ephemeral containers to a running pod, but removal requires deleting the pod.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

---

## Resource Versions

### Question 89
[HARD]

How is resourceVersion used in watch operations?

A) To filter resources by version
B) To start watching from a specific point
C) To limit results to recent versions
D) To enable compression

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When watching resources, you can specify a resourceVersion to start watching from that point forward. This enables resuming watches after disconnection without missing events. Using resourceVersion=0 uses the latest cached version.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

## Server-Side Apply

### Question 90
[HARD]

What is Server-Side Apply in Kubernetes?

A) Applying manifests from the server
B) A new apply mechanism that tracks field ownership
C) Applying changes to all nodes simultaneously
D) Server-side rendering of manifests

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Server-Side Apply (SSA) is a declarative resource management mechanism that tracks which fields are managed by which controllers/users. It enables better multi-manager scenarios and avoids the issues of client-side apply. Enabled with `kubectl apply --server-side`.

**Source:** [Access Clusters Using the Kubernetes API | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/access-cluster-api/)

</details>

---

### Question 91
[HARD]

How do you enable Server-Side Apply with kubectl?

A) kubectl apply --ssa
B) kubectl apply --server-side
C) kubectl ssa apply
D) kubectl apply --mode=server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl apply --server-side` enables Server-Side Apply. You can also specify a field manager with `--field-manager=my-manager`. SSA provides better conflict detection and field ownership tracking compared to client-side apply.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Debugging and Troubleshooting

### Question 92
[MEDIUM-HARD]

How do you see why a Pod is in Pending state?

A) kubectl logs pod-name
B) kubectl describe pod pod-name
C) kubectl get pod pod-name --pending
D) kubectl status pod pod-name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe pod` shows the Events section which typically explains why a pod is Pending (e.g., insufficient resources, node selectors not matching, PVC not bound). The Conditions section also provides status information.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

### Question 93
[MEDIUM-HARD]

How do you get all pods that are not in Running state?

A) kubectl get pods --not-running
B) kubectl get pods --field-selector=status.phase!=Running
C) kubectl get pods --status=!Running
D) kubectl get pods -l status!=Running

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Field selectors can filter by status.phase. Using `status.phase!=Running` shows pods in Pending, Succeeded, Failed, or Unknown states. This is useful for quickly identifying problematic pods across namespaces.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Token Management

### Question 94
[HARD]

What command creates a temporary token for a ServiceAccount?

A) kubectl token create
B) kubectl create token <serviceaccount>
C) kubectl serviceaccount token
D) kubectl auth token

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl create token <serviceaccount>` generates a new time-limited token using the TokenRequest API. You can specify duration with `--duration` and audience with `--audience`. This is the preferred method since Kubernetes 1.24 removed auto-generated secret tokens.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 95
[MEDIUM-HARD]

What is token audience binding?

A) Restricting who can view tokens
B) Limiting token validity to specific intended recipients
C) Encrypting tokens
D) Logging token usage

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Audience binding restricts tokens to specific recipients (audiences). A token created with `--audience=vault.example.com` is only valid for that audience. This prevents tokens meant for one service from being used with another, improving security.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

## Cluster-Info and Diagnostics

### Question 96
[MEDIUM-HARD]

What command verifies cluster connectivity quickly?

A) kubectl ping
B) kubectl cluster-info
C) kubectl connect
D) kubectl verify

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl cluster-info` quickly verifies connectivity by showing the API server endpoint and core services. If this fails, you know there's a connectivity or authentication issue. For more detail, add `dump` to get comprehensive diagnostics.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Dry Run Modes

### Question 97
[MEDIUM-HARD]

When would you use `--dry-run=server` over `--dry-run=client`?

A) When generating YAML templates
B) When validating against admission controllers
C) When offline
D) For performance

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Server-side dry run validates against the actual cluster state, including admission webhooks, resource quotas, and validation webhooks. Client-side dry run cannot catch these. Use server-side when you need complete validation before applying.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Final Advanced Topics

### Question 98
[HARD]

What is a managed field in Kubernetes objects?

A) A field managed by a specific controller
B) A field with validation rules
C) A field with field manager ownership tracking
D) An encrypted field

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Managed fields (metadata.managedFields) track which field manager owns which fields in an object. This metadata is used by Server-Side Apply to determine conflict resolution. Each manager only modifies fields it owns.

**Source:** [Server-Side Apply | Kubernetes](https://kubernetes.io/docs/reference/using-api/server-side-apply/)

</details>

---

### Question 99
[MEDIUM-HARD]

What is the `--grace-period` flag used for?

A) Setting request timeout
B) Setting time for graceful pod termination
C) Setting scheduling delay
D) Setting retry interval

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--grace-period` specifies seconds to wait for graceful termination during deletion. Pods receive SIGTERM, then SIGKILL after the grace period. Default is from the pod spec (usually 30s). `--grace-period=0` with `--force` enables immediate deletion.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

---

### Question 100
[HARD]

What is the purpose of the `--show-managed-fields` flag?

A) Shows field descriptions
B) Shows field manager ownership information
C) Shows required fields
D) Shows deprecated fields

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `--show-managed-fields` includes the managedFields metadata in output (normally hidden for readability). This shows which field managers own which fields, useful for debugging Server-Side Apply conflicts and understanding who modified what.

**Source:** [Command line tool (kubectl) | Kubernetes](https://kubernetes.io/docs/reference/kubectl/)

</details>

---

## Summary

This question set covers Kubernetes administration topics essential for the KCNA certification:

- **kubectl basics and advanced usage** (Questions 1-12, 125-132)
- **kubeconfig and contexts** (Questions 13-21, 148-150)
- **Cluster components** (Questions 22-32)
- **Namespaces** (Questions 33-40)
- **Labels, selectors, and annotations** (Questions 41-55)
- **Resource management** (Questions 56-65)
- **RBAC** (Questions 66-75)
- **Node management** (Questions 76-84)
- **etcd administration** (Questions 85-92)
- **Cluster upgrades** (Questions 93-100)
- **API and versioning** (Questions 101-110)
- **Logging and monitoring** (Questions 111-118)
- **Service accounts** (Questions 119-124)
- **Advanced administration** (Questions 133-200)