# Kubernetes Core Concepts - Q51-Q60 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q51-Q60

---

### Question 51
[HARD]

A security engineer is reviewing the communication paths in a production Kubernetes cluster. She discovers that the API server initiates outbound connections to worker nodes for certain operations. Which of the following correctly describes a scenario where the API server opens a connection to the kubelet, and the security implication of that connection?

A) The API server connects to the kubelet only during node registration, and the connection uses plain HTTP by default since it is an internal cluster operation
B) The API server connects to the kubelet when streaming Pod logs or executing commands via `kubectl exec`, and by default the API server does not verify the kubelet's serving certificate, making the connection vulnerable to man-in-the-middle attacks
C) The API server never initiates connections to the kubelet; all communication is pull-based with the kubelet polling the API server for new PodSpecs
D) The API server connects to the kubelet exclusively through kube-proxy, which terminates TLS and forwards traffic to the kubelet over localhost

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The API server initiates HTTPS connections to the kubelet for operations such as fetching logs (`kubectl logs`), attaching to running containers (`kubectl attach`), and port-forwarding (`kubectl exec`). By default, the API server does not verify the kubelet's serving certificate, which means the connection is encrypted but susceptible to man-in-the-middle attacks. To fully secure this path, administrators must use the `--kubelet-certificate-authority` flag on the API server so it can verify kubelet certificates. The kubelet does not rely on kube-proxy for API server communication, and the API server does actively initiate connections rather than using a pure pull model.

**Source:** https://kubernetes.io/docs/concepts/architecture/control-plane-node-communication/#api-server-to-kubelet

</details>

---

### Question 52
[HARD]

A platform team is automating the process of adding new worker nodes to an existing Kubernetes cluster. They use `kubeadm join` with a token passed on the command line. An intern asks why this token is needed and what would happen if the token were compromised before being used. Which statement best describes the role of bootstrap tokens and the risk of compromise?

A) Bootstrap tokens authenticate the kubelet to the API server permanently; if compromised, an attacker gains long-lived cluster-admin access to the entire cluster
B) Bootstrap tokens are used only to encrypt etcd data during the join process; compromise would expose etcd contents but not allow unauthorized node joins
C) Bootstrap tokens allow a new node to authenticate to the API server temporarily so it can submit a certificate signing request (CSR) for a proper kubelet credential; if compromised before expiry, an attacker could join a rogue node to the cluster
D) Bootstrap tokens are stored in the kubelet's kubeconfig file and are used for all subsequent API calls; compromise would allow an attacker to impersonate the kubelet indefinitely

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Bootstrap tokens provide a limited, temporary authentication mechanism that allows a new node to prove its identity to the API server long enough to submit a certificate signing request (CSR). Once the CSR is approved and a client certificate is issued, the bootstrap token is no longer needed for that node. These tokens are stored as Secrets in the `kube-system` namespace and have a configurable TTL. If a token is compromised before it expires, an attacker could use it to join an unauthorized node to the cluster, which is why tokens should be short-lived and the `--discovery-token-ca-cert-hash` flag should be used for additional validation. They do not grant cluster-admin privileges or provide permanent authentication.

**Source:** https://kubernetes.io/docs/reference/access-authn-authz/bootstrap-tokens/

</details>

---

### Question 53
[HARD]

A security auditor discovers that a Kubernetes cluster's kubelet certificates have not been rotated in over a year. The kubelet's client certificate is used to authenticate to the API server. The auditor flags this as a risk. Which of the following best explains why automatic kubelet certificate rotation is a critical security mechanism?

A) Without certificate rotation, the kubelet cannot pull container images from private registries because the image pull secret is embedded in the certificate
B) Certificate rotation is purely cosmetic and required only for compliance reporting; expired kubelet certificates do not impact cluster functionality because the API server falls back to anonymous authentication
C) If a kubelet's long-lived client certificate is compromised, an attacker could impersonate that node to the API server for the entire certificate lifetime; automatic rotation with `--rotate-certificates` limits the exposure window by periodically requesting fresh short-lived certificates
D) Certificate rotation is needed because etcd rejects connections from kubelets with certificates older than 30 days, causing the node to become NotReady

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The kubelet uses a client certificate to authenticate itself to the API server. If this certificate has a long validity period and is compromised, an attacker could impersonate the node for that entire duration, potentially reading Secrets for Pods scheduled on that node or manipulating Pod status. Enabling automatic certificate rotation via `--rotate-certificates` causes the kubelet to request a new certificate from the API server before the current one expires, significantly reducing the window of exposure. The kubelet does not communicate directly with etcd, and a properly configured cluster should not fall back to anonymous authentication for kubelet communication.

**Source:** https://kubernetes.io/docs/reference/access-authn-authz/kubelet-tls-bootstrapping/#certificate-rotation

</details>

---

### Question 54
[HARD]

A developer deploys a Pod that needs to read ConfigMaps from the Kubernetes API at runtime. The developer has not configured any explicit credentials in the Pod spec. The Pod is successfully able to list ConfigMaps in its own namespace. Which mechanism is enabling the Pod to authenticate to the API server, and where does the credential come from?

A) The kubelet injects the node's own client certificate into every Pod, so the Pod authenticates as the node itself and inherits the node's full permissions
B) Kubernetes automatically mounts a projected ServiceAccount token into the Pod at a well-known path; this token is issued by the API server and bound to the Pod's ServiceAccount, which has an associated RBAC Role granting ConfigMap read access
C) The Pod inherits the cluster-admin credentials from the kube-system namespace because all Pods have implicit admin access to their own namespace
D) CoreDNS provides an authentication sidecar that generates JWT tokens on behalf of Pods, which the API server validates using the CoreDNS signing key

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Every Pod in Kubernetes is associated with a ServiceAccount (either explicitly or via the `default` ServiceAccount in its namespace). As of Kubernetes 1.22+, the kubelet uses the TokenRequest API to obtain a time-bound, audience-bound projected ServiceAccount token and mounts it at `/var/run/secrets/kubernetes.io/serviceaccount/token`. The Pod uses this token as a Bearer token when calling the API server. The API server validates the token and maps it to the ServiceAccount's identity. Access to resources like ConfigMaps is then governed by RBAC bindings attached to that ServiceAccount. Pods do not inherit node certificates or cluster-admin credentials, and CoreDNS plays no role in authentication.

**Source:** https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/

</details>

---

### Question 55
[HARD]

A cluster administrator is hardening API server authorization and notices that the kubelet on each node needs to read Secrets, ConfigMaps, and PersistentVolumeClaims, but only those that are referenced by Pods scheduled to that specific node. Which authorization mode enforces this node-scoped restriction, and how does it differ from standard RBAC?

A) The Webhook authorization mode, which calls an external service to verify whether a kubelet is allowed to access a specific Secret based on the node's IP address
B) The Node authorization mode, which is a special-purpose authorizer that grants kubelets access only to the specific objects related to Pods bound to their node, unlike RBAC which uses generic Roles that cannot inherently scope permissions per node
C) The ABAC authorization mode, which uses policy files that map each node name to a list of allowed resource names, providing finer granularity than RBAC
D) Standard RBAC with a ClusterRole bound to each node's ServiceAccount, which achieves the same per-node scoping by creating one ClusterRoleBinding per node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Node authorization mode is a special-purpose authorizer designed specifically for kubelet requests. It works in conjunction with the NodeRestriction admission plugin to ensure that a kubelet can only read Secrets, ConfigMaps, PersistentVolumeClaims, and PersistentVolumes that are referenced by Pods scheduled to the kubelet's own node. It can also only modify its own Node object and the status of Pods bound to it. Standard RBAC cannot natively enforce this per-node object scoping because Roles grant access to resource types broadly, not based on which Pods happen to be scheduled where. The Node authorizer inspects the graph of Pod-to-node bindings to make these fine-grained decisions.

**Source:** https://kubernetes.io/docs/reference/access-authn-authz/node/

</details>

---

### Question 56
[HARD]

A compliance team requires that all API requests in a Kubernetes cluster be recorded for forensic analysis, including which user made the request, what resource was affected, and what the request body contained. The team is evaluating Kubernetes audit logging. Which statement correctly describes how API audit logging works and what level of detail is available?

A) Audit logging is handled by etcd, which writes a transaction log of every key-value change; the API server has no built-in audit capability
B) The API server supports audit logging via an audit policy that defines rules at four levels — None, Metadata, Request, and RequestResponse — allowing administrators to capture varying detail per resource type, and events can be sent to log backends or webhook backends
C) Audit logging only captures authentication failures and is not capable of recording successful API requests or response bodies
D) Kubernetes relies exclusively on the container runtime's system call logs (such as seccomp logs) to reconstruct API activity; there is no application-level audit log

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes API audit logging is a built-in feature of the kube-apiserver. Administrators define an audit policy file that specifies rules controlling what events are recorded and at what level of detail. The four audit levels are: None (do not log), Metadata (log request metadata like user, timestamp, resource, verb), Request (log metadata plus the request body), and RequestResponse (log metadata, request body, and response body). Events can be written to a log file backend or sent to an external webhook backend for centralized processing. This provides comprehensive forensic capability far beyond what etcd transaction logs or container runtime logs can offer.

**Source:** https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/

</details>

---

### Question 57
[HARD]

An organization stores sensitive database credentials as Kubernetes Secrets. A security review reveals that anyone with direct read access to the etcd datastore could view these Secrets in plaintext. The team decides to enable encryption at rest. Which of the following correctly describes what encryption at rest protects and what it does NOT protect?

A) Encryption at rest encrypts Secret data before it is written to etcd, so direct etcd access no longer reveals plaintext values; however, it does not protect Secrets in transit between the API server and etcd, nor does it prevent authorized API users from reading Secrets through the API
B) Encryption at rest encrypts all network traffic between the API server and etcd, but the data stored in etcd remains in plaintext for performance reasons
C) Encryption at rest encrypts the entire etcd disk using dm-crypt, and Kubernetes manages the LUKS keys automatically without any additional API server configuration
D) Encryption at rest only applies to ConfigMaps and does not cover Secrets, which must be encrypted using a separate third-party tool like HashiCorp Vault

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** When encryption at rest is enabled via an EncryptionConfiguration on the API server, Secret data (and optionally other resources) is encrypted before being written to etcd. This means that if an attacker gains direct access to etcd's data files or the etcd API, they see ciphertext rather than plaintext Secret values. However, encryption at rest does not encrypt data in transit (that is handled by TLS between the API server and etcd), and it does not change API-level access control. Authorized users with RBAC permissions to read Secrets can still retrieve the decrypted values through the API server, which decrypts them transparently. Kubernetes supports multiple encryption providers including AES-CBC, AES-GCM, and KMS integrations.

**Source:** https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/

</details>

---

### Question 58
[HARD]

A platform team enforces a policy that no container in their production namespace should run as the root user. A developer submits a Deployment where the container image's Dockerfile specifies `USER root`. The Pod spec includes `securityContext: { runAsNonRoot: true }` but does not set a specific `runAsUser`. What happens when Kubernetes attempts to start this Pod?

A) The container starts successfully because `runAsNonRoot` only generates a warning in the Pod events but does not block execution
B) The kubelet overrides the image's USER directive and automatically selects a random non-root UID, allowing the container to start
C) The container fails to start because the kubelet validates that the container's runtime user is not root (UID 0), and since the image specifies root as the user, the validation fails and the container is rejected with a "must not run as root" error
D) The API server rejects the Pod at admission time before it reaches any node, because `runAsNonRoot` is validated during the admission phase and the API server inspects the image metadata

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When `runAsNonRoot: true` is set in the Pod's SecurityContext and no explicit `runAsUser` is specified, the kubelet performs a runtime check. It inspects the container image's configured user, and if that user resolves to UID 0 (root), the kubelet refuses to start the container with an error such as "container has runAsNonRoot and image will run as root." This validation happens at the node level when the kubelet is about to start the container, not at the API server admission phase. The kubelet does not override the image's user to a non-root UID; it simply rejects the container. This mechanism ensures that even if an image defaults to root, the security policy is enforced.

**Source:** https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod

</details>

---

### Question 59
[HARD]

A cluster administrator needs to grant a CI/CD pipeline ServiceAccount permission to create and update Deployments in the `staging` namespace, but not delete them and not access any resources in other namespaces. The administrator is considering using a ClusterRole with a RoleBinding versus a Role with a RoleBinding. Which approach correctly achieves the stated requirement, and why might one be preferred over the other?

A) Only a ClusterRole with a ClusterRoleBinding can work because Deployments are cluster-scoped resources that cannot be restricted to a single namespace
B) A Role defining create and update verbs on Deployments, bound via a RoleBinding in the `staging` namespace to the ServiceAccount, correctly limits access to that namespace; alternatively, a ClusterRole with the same permissions bound via a namespace-scoped RoleBinding achieves the same effect, but the ClusterRole approach is reusable across multiple namespaces
C) A Role with a RoleBinding is the only valid option because ClusterRoles cannot be referenced by namespace-scoped RoleBindings; they can only be used with ClusterRoleBindings
D) Neither RBAC mechanism can restrict verbs at the individual level; RBAC only supports granting full CRUD access or no access to a given resource type

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Both approaches achieve the goal. A namespace-scoped Role with a RoleBinding directly limits the permissions to the `staging` namespace. Alternatively, a ClusterRole defining the same permissions can be referenced by a RoleBinding in the `staging` namespace, which grants those permissions only within that namespace despite the ClusterRole being cluster-wide in definition. The advantage of the ClusterRole approach is reusability: the same ClusterRole can be referenced by RoleBindings in multiple namespaces without duplicating the Role definition. Deployments are namespace-scoped resources, so they can absolutely be restricted per namespace. RBAC supports fine-grained verb control (get, list, create, update, patch, delete, watch) on any resource type.

**Source:** https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding

</details>

---

### Question 60
[HARD]

A network engineer joins a team managing a Kubernetes cluster and asks how Pods on different nodes communicate without Network Address Translation (NAT). The existing team explains the Kubernetes network model. Which of the following correctly describes the fundamental networking guarantee and the architectural implication it creates?

A) Kubernetes requires that every Pod receives a cluster-unique IP address and can communicate with any other Pod using that IP without NAT; this means the CNI plugin must provision a flat network or overlay that provides Pod-to-Pod reachability across nodes, and each Pod sees its own IP as the source address when communicating
B) Kubernetes uses kube-proxy to perform DNAT on all Pod-to-Pod traffic so that Pods communicate using their node's IP address, and the receiving Pod sees the node IP as the source
C) Kubernetes assigns Pods a shared IP per node (one IP per node, not per Pod), and all Pods on the same node share that IP using different port ranges, similar to traditional Docker bridge networking
D) Kubernetes does not impose any networking requirements; Pod-to-Pod communication only works within the same node, and cross-node communication requires manually configured Services or Ingress resources

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The Kubernetes network model mandates three fundamental rules: every Pod gets its own unique IP address, Pods on any node can communicate with all other Pods on any other node without NAT, and agents on a node can communicate with all Pods on that node. This means the IP a Pod sees for itself is the same IP that other Pods see when communicating with it. Implementing this model is the responsibility of the CNI (Container Network Interface) plugin, which may use overlay networks (such as VXLAN), BGP-routed networks, or cloud-provider VPC routing. kube-proxy handles Service IP translation, not Pod-to-Pod NAT. Pods do not share IPs per node, and cross-node Pod communication is a fundamental requirement, not an optional feature.

**Source:** https://kubernetes.io/docs/concepts/services-networking/#the-kubernetes-network-model
</details>
