# Kubernetes Administration - 200 MCQ Questions

**Domain:** Kubernetes Fundamentals (44%)
**Competency:** Administration
**Difficulty Distribution:** 10% Medium | 70% Medium-Hard | 20% Hard

---

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

### Question 3
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

### Question 4
[MEDIUM-HARD]

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

### Question 5
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

### Question 6
[MEDIUM-HARD]

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

### Question 7
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

### Question 8
[MEDIUM-HARD]

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

### Question 9
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

### Question 10
[MEDIUM-HARD]

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

### Question 11
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

### Question 12
[MEDIUM-HARD]

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

### Question 13
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

### Question 14
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

### Question 15
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

### Question 16
[MEDIUM-HARD]

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

### Question 17
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

### Question 18
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

### Question 19
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

### Question 20
[MEDIUM-HARD]

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

### Question 21
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

### Question 22
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

### Question 23
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

### Question 24
[MEDIUM-HARD]

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

### Question 25
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

### Question 26
[MEDIUM-HARD]

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

### Question 27
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

### Question 28
[MEDIUM-HARD]

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

### Question 29
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

### Question 30
[MEDIUM-HARD]

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

### Question 31
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

### Question 32
[MEDIUM-HARD]

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

### Question 33
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

### Question 34
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

### Question 35
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

### Question 36
[MEDIUM-HARD]

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

### Question 37
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

### Question 38
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

### Question 39
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

### Question 40
[MEDIUM-HARD]

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

### Question 41
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

### Question 42
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

### Question 43
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

### Question 44
[MEDIUM-HARD]

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

### Question 45
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

### Question 46
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

### Question 47
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

### Question 48
[MEDIUM-HARD]

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

### Question 49
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

### Question 50
[MEDIUM-HARD]

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

### Question 51
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

### Question 52
[MEDIUM-HARD]

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

### Question 53
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

### Question 54
[MEDIUM-HARD]

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

### Question 55
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

### Question 56
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

### Question 57
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

### Question 58
[MEDIUM-HARD]

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

### Question 59
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

### Question 60
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

### Question 61
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

### Question 62
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

### Question 63
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

### Question 64
[MEDIUM-HARD]

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

### Question 65
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

### Question 66
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

### Question 67
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

### Question 68
[MEDIUM-HARD]

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

### Question 69
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

### Question 70
[MEDIUM-HARD]

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

### Question 71
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

### Question 72
[MEDIUM-HARD]

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

### Question 73
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

### Question 74
[MEDIUM-HARD]

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

### Question 75
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

### Question 76
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

### Question 77
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

### Question 78
[MEDIUM-HARD]

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

### Question 79
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

### Question 80
[MEDIUM-HARD]

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

### Question 81
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

### Question 82
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

### Question 83
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

### Question 84
[MEDIUM-HARD]

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

### Question 85
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

### Question 86
[MEDIUM-HARD]

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

### Question 87
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

### Question 88
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

### Question 89
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

### Question 90
[MEDIUM-HARD]

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

### Question 91
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

### Question 92
[MEDIUM-HARD]

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

### Question 93
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

### Question 94
[MEDIUM-HARD]

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

### Question 95
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

### Question 96
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

### Question 97
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

### Question 98
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

### Question 99
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

### Question 100
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

### Question 101
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

### Question 102
[MEDIUM-HARD]

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

### Question 103
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

### Question 104
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

### Question 105
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

### Question 106
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

### Question 107
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

### Question 108
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

### Question 109
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

### Question 110
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

### Question 111
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

### Question 112
[MEDIUM-HARD]

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

### Question 113
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

### Question 114
[MEDIUM-HARD]

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

### Question 115
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

### Question 116
[MEDIUM-HARD]

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

### Question 117
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

### Question 118
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

### Question 119
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

### Question 120
[MEDIUM-HARD]

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

### Question 121
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

### Question 122
[MEDIUM-HARD]

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

### Question 123
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

### Question 124
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

### Question 125
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

### Question 126
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

### Question 127
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

### Question 128
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

### Question 129
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

### Question 130
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

### Question 131
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

### Question 132
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

### Question 133
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

### Question 134
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

### Question 135
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

### Question 136
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

### Question 137
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

### Question 138
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

### Question 139
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

### Question 140
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

### Question 141
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

### Question 142
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

### Question 143
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

### Question 144
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

### Question 145
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

### Question 146
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

### Question 147
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

### Question 148
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

### Question 149
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

### Question 150
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

### Question 151
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

### Question 152
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

### Question 153
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

### Question 154
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

### Question 155
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

### Question 156
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

### Question 157
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

### Question 158
[MEDIUM-HARD]

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

### Question 159
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

### Question 160
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

### Question 161
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

### Question 162
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

### Question 163
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

### Question 164
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

### Question 165
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

### Question 166
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

### Question 167
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

### Question 168
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

### Question 169
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

### Question 170
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

### Question 171
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

### Question 172
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

### Question 173
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

### Question 174
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

### Question 175
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

### Question 176
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

### Question 177
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

### Question 178
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

### Question 179
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

### Question 180
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

### Question 181
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

### Question 182
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

### Question 183
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

### Question 184
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

### Question 185
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

### Question 186
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

### Question 187
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

### Question 188
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

### Question 189
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

### Question 190
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

### Question 191
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

### Question 192
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

### Question 193
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

### Question 194
[HARD]

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

### Question 195
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

### Question 196
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

### Question 197
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

### Question 198
[HARD]

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

### Question 199
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

### Question 200
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
