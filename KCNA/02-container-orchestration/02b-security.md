# Security - 100 MCQ Questions (Part B)

**Domain:** Container Orchestration (28%)
**Competency:** Security
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## RBAC Fundamentals

### Question 1
[MEDIUM]

Which Kubernetes resource grants permissions cluster-wide rather than within a single namespace?

A) Role
B) ClusterRole
C) RoleBinding
D) ServiceAccount

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ClusterRole is a cluster-scoped resource that defines permissions across the entire cluster, not limited to a single namespace. Unlike Roles which are namespaced, ClusterRoles can grant access to cluster-scoped resources (like nodes) and non-resource endpoints.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)

</details>

---

### Question 2
[MEDIUM]

What is the purpose of a ClusterRoleBinding?

A) To create a new ClusterRole
B) To bind a ClusterRole to subjects cluster-wide
C) To bind a Role across namespaces
D) To restrict ClusterRole permissions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A ClusterRoleBinding grants the permissions defined in a ClusterRole to one or more subjects (users, groups, or ServiceAccounts) across the entire cluster. The binding makes the permissions effective cluster-wide, regardless of namespace.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding)

</details>

---

### Question 3
[MEDIUM-HARD]

Which RBAC verb is required to watch for changes to resources?

A) observe
B) monitor
C) watch
D) subscribe

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The "watch" verb allows clients to receive streaming updates when resources change. This is commonly used by controllers and operators to react to resource modifications. The watch verb is distinct from get and list, requiring explicit permission.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 4
[MEDIUM-HARD]

How do you grant read-only access to Pods in a namespace using RBAC?

A) Create a Role with "read" verb
B) Create a Role with "get", "list", and "watch" verbs for pods
C) Assign the view ClusterRole directly
D) Use the readonly annotation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RBAC doesn't have a "read" verb. To grant read-only access, you create a Role with "get" (fetch single resources), "list" (fetch collections), and "watch" (receive updates) verbs for the pods resource. Then bind this Role to the subject with a RoleBinding.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 5
[MEDIUM-HARD]

What is the difference between "get" and "list" verbs in RBAC?

A) No difference; they are aliases
B) "get" retrieves a single resource by name; "list" retrieves all resources
C) "get" is for reading; "list" is for writing
D) "list" is deprecated in favor of "get"

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "get" verb allows retrieving a specific resource by its name (e.g., kubectl get pod my-pod). The "list" verb allows retrieving all resources of a type (e.g., kubectl get pods). Both are read operations but with different scopes - individual vs. collection.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 6
[HARD]

What is the "impersonate" verb used for in RBAC?

A) To copy another user's permissions
B) To allow acting as another user, group, or ServiceAccount
C) To create duplicate users
D) To audit user actions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "impersonate" verb allows a user to act as another user, group, or ServiceAccount. This is used for testing permissions (kubectl --as=) and by components like the API server. It's a powerful permission that should be granted carefully.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#user-impersonation)

</details>

---

### Question 7
[HARD]

How can you reference non-resource URLs in RBAC rules?

A) Use the urls field in Role rules
B) Use the nonResourceURLs field in ClusterRole rules
C) Non-resource URLs cannot be referenced
D) Use a special NetworkPolicy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Non-resource URLs (like /healthz, /api, /metrics) can only be referenced in ClusterRoles using the nonResourceURLs field. This is because these endpoints are cluster-scoped, not namespaced. Roles cannot reference non-resource URLs.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#referring-to-resources)

</details>

---

### Question 8
[HARD]

What are aggregated ClusterRoles and how do they work?

A) ClusterRoles that combine permissions from multiple Roles
B) ClusterRoles with aggregationRule that automatically include rules from other ClusterRoles with matching labels
C) ClusterRoles that are compressed for performance
D) ClusterRoles that span multiple clusters

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Aggregated ClusterRoles use an aggregationRule with label selectors. The controller automatically combines rules from all ClusterRoles matching the selector into the aggregated ClusterRole. This allows extending built-in roles like admin, edit, and view with custom permissions.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#aggregated-clusterroles)

</details>

---

### Question 9
[HARD]

Which default ClusterRole provides read access to most resources?

A) cluster-reader
B) view
C) reader
D) read-only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "view" ClusterRole is a default aggregated role that grants read-only access to most objects in a namespace (excluding secrets and role bindings). It's designed for non-destructive access, allowing users to see resources without modifying them.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles)

</details>

---

### Question 10
[HARD]

How do you grant access to subresources like pods/log using RBAC?

A) Grant access to pods and logs separately
B) Use the resources field with "pods/log" format
C) Subresources cannot be individually controlled
D) Use a special subresources field

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Subresources are referenced using the format "resource/subresource" in the resources field. For example, "pods/log" grants access to Pod logs, "pods/exec" grants exec access. This allows fine-grained control over specific subresource operations.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#referring-to-resources)

</details>

---

### Question 11
[HARD]

What is the purpose of the resourceNames field in RBAC rules?

A) To define new resource types
B) To restrict access to specific named resources
C) To rename resources
D) To create aliases for resources

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The resourceNames field restricts the rule to specific named instances of resources. For example, you can grant access to a specific ConfigMap named "my-config" rather than all ConfigMaps. This enables fine-grained, resource-instance-level access control.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#referring-to-resources)

</details>

---

### Question 12
[HARD]

How does RBAC handle wildcard permissions?

A) Wildcards are not supported
B) Use "*" to match all resources, verbs, or API groups
C) Use "all" keyword
D) Wildcards only work for verbs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RBAC supports the "*" wildcard to match all values. You can use it for apiGroups: ["*"] (all API groups), resources: ["*"] (all resources), or verbs: ["*"] (all verbs). The cluster-admin ClusterRole uses wildcards to grant full access.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

## ServiceAccounts

### Question 13
[MEDIUM]

Which namespace typically contains ServiceAccounts for core system components?

A) default
B) kube-system
C) kube-public
D) system

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-system namespace contains ServiceAccounts for core Kubernetes system components like kube-controller-manager, kube-scheduler, and kube-proxy. Note that every namespace also has its own "default" ServiceAccount created automatically, but system components use dedicated ServiceAccounts in kube-system.

**Source:** [Managing Service Accounts | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/)

</details>

---

### Question 14
[MEDIUM]

How do you assign a specific ServiceAccount to a Pod?

A) Use the account field in the Pod spec
B) Use the serviceAccountName field in the Pod spec
C) Create a RoleBinding
D) Use an annotation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To assign a specific ServiceAccount to a Pod, set the serviceAccountName field in the Pod spec. If not specified, the Pod uses the "default" ServiceAccount in its namespace. The ServiceAccount must exist before creating the Pod.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 15
[MEDIUM-HARD]

What is a projected volume in the context of ServiceAccount tokens?

A) A volume that projects tokens to multiple locations
B) A volume that combines multiple sources including ServiceAccount tokens
C) A volume for storing projected data
D) A deprecated token storage method

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A projected volume can combine multiple volume sources into a single directory, including ServiceAccount tokens, ConfigMaps, Secrets, and the downward API. For ServiceAccounts, this enables mounting time-bound, audience-bound tokens alongside other data.

**Source:** [Projected Volumes | Kubernetes](https://kubernetes.io/docs/concepts/storage/projected-volumes/)

</details>

---

### Question 16
[MEDIUM-HARD]

Why were bound ServiceAccount tokens introduced?

A) For better performance
B) To improve security with time-limited, audience-bound tokens
C) To simplify token management
D) For backward compatibility

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bound ServiceAccount tokens improve security over legacy Secret-based tokens. They are time-limited (expire after a configurable period), audience-bound (only valid for specific audiences), and bound to the Pod (invalidated when Pod is deleted). This reduces the impact of token compromise.

**Source:** [Service Account Token Volume Projection | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection)

</details>

---

### Question 17
[HARD]

What is the expirationSeconds field for ServiceAccount tokens?

A) Time until the ServiceAccount is deleted
B) The lifetime of the projected token
C) Time until token refresh
D) Maximum session duration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The expirationSeconds field specifies how long the projected ServiceAccount token is valid. The kubelet proactively rotates the token as it approaches expiration. The default is typically 3600 seconds (1 hour), with a minimum of 600 seconds (10 minutes).

**Source:** [Service Account Token Volume Projection | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection)

</details>

---

### Question 18
[HARD]

How do you create a non-expiring ServiceAccount token?

A) Set expirationSeconds to 0
B) Create a Secret of type kubernetes.io/service-account-token
C) Use the --no-expire flag
D) Non-expiring tokens are not possible

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To create a non-expiring (long-lived) ServiceAccount token, create a Secret of type kubernetes.io/service-account-token with an annotation referencing the ServiceAccount. The controller will populate the token. However, this is discouraged for security; bound tokens are preferred.

**Source:** [Managing Service Accounts | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/#manually-create-a-long-lived-api-token-for-a-serviceaccount)

</details>

---

### Question 19
[HARD]

What happens when the ServiceAccount associated with a running Pod is deleted?

A) The Pod is immediately terminated
B) The Pod continues running but token authentication may fail
C) A new ServiceAccount is automatically created
D) Nothing; Pods don't depend on ServiceAccounts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Deleting a ServiceAccount doesn't automatically terminate Pods using it. However, the Pod's token will become invalid for API authentication since the ServiceAccount no longer exists. The Pod continues running but any API calls using the token will fail authentication.

**Source:** [Managing Service Accounts | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/)

</details>

---

### Question 20
[HARD]

What is the purpose of the serviceAccountName vs serviceAccount field?

A) They are identical
B) serviceAccountName is the preferred field; serviceAccount is deprecated
C) serviceAccount is for system accounts
D) serviceAccountName is for external accounts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The serviceAccountName field is the preferred way to specify a Pod's ServiceAccount. The serviceAccount field is deprecated and maintained only for backward compatibility. Both refer to the same concept, but serviceAccountName should always be used in new configurations.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 21
[HARD]

How does the BoundServiceAccountTokenVolume feature work?

A) It binds volumes to ServiceAccounts
B) It projects time-bound, audience-bound tokens into Pods instead of Secret-based tokens
C) It limits volume access by ServiceAccount
D) It encrypts ServiceAccount volumes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** BoundServiceAccountTokenVolume (now default) projects time-bound, audience-bound tokens into Pods via a projected volume instead of using Secret-mounted tokens. These tokens are bound to the Pod's lifetime, have configurable expiration, and are automatically rotated by the kubelet.

**Source:** [Service Account Token Volume Projection | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection)

</details>

---

### Question 22
[HARD]

What are the security benefits of using short-lived ServiceAccount tokens?

A) Faster authentication
B) Reduced blast radius if compromised; tokens expire quickly
C) Better performance
D) Simpler configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Short-lived tokens reduce security risk because if compromised, they expire quickly, limiting the window of exploitation. Combined with automatic rotation, this significantly reduces the blast radius of token theft compared to long-lived Secret-based tokens that never expire.

**Source:** [Service Account Token Volume Projection | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/#serviceaccount-token-volume-projection)

</details>

---

## Pod Security

### Question 23
[MEDIUM]

What is a privileged container?

A) A container running as root
B) A container with almost all host capabilities and device access
C) A container with network privileges
D) A container that can access secrets

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A privileged container (privileged: true) runs with almost all capabilities of the host, including access to all host devices. This is essentially equivalent to running as root on the host. This is different from just running as root in a non-privileged container, which has fewer capabilities.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 24
[MEDIUM]

Which Pod Security Standards level prevents known privilege escalations while allowing most workloads?

A) restricted
B) baseline
C) privileged
D) permissive

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "baseline" Pod Security Standard level prevents known privilege escalations while allowing most workloads to run. It blocks dangerous configurations like hostNetwork, hostPID, and privileged containers but allows common workload patterns. "Privileged" has no restrictions, while "restricted" is heavily locked down.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 25
[MEDIUM]

What does the runAsUser field specify?

A) The username to run as
B) The numeric UID to run the container process as
C) The user who created the Pod
D) The ServiceAccount user

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The runAsUser field specifies the numeric user ID (UID) that runs the container's entrypoint process. It overrides any USER instruction in the container image. For example, runAsUser: 1000 runs the container as UID 1000.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 26
[MEDIUM-HARD]

What is the fsGroup field used for in securityContext?

A) To set the filesystem type
B) To set the group ID that owns Pod volumes
C) To configure file permissions
D) To specify filesystem quotas

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The fsGroup field specifies a group ID that Kubernetes applies to all volumes in the Pod. Files created in these volumes will be owned by this group, and volume permissions are changed to be group-readable/writable. This enables sharing volumes between containers.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod)

</details>

---

### Question 27
[MEDIUM-HARD]

How do you drop all Linux capabilities from a container?

A) Set privileged: false
B) Use capabilities.drop: ["ALL"] in securityContext
C) Set runAsNonRoot: true
D) Capabilities cannot be dropped

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To drop all Linux capabilities, use capabilities.drop: ["ALL"] in the container's securityContext. You can then selectively add back specific capabilities with capabilities.add if needed. This follows the principle of least privilege by removing unnecessary capabilities.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-capabilities-for-a-container)

</details>

---

### Question 28
[MEDIUM-HARD]

What is the difference between pod-level and container-level securityContext?

A) No difference; they are the same
B) Pod-level applies to all containers; container-level overrides for specific containers
C) Pod-level is deprecated
D) Container-level is more secure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod-level securityContext (spec.securityContext) sets defaults for all containers in the Pod. Container-level securityContext (spec.containers[].securityContext) can override these settings for specific containers. Some fields like fsGroup only exist at Pod level.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 29
[HARD]

What does the "restricted" Pod Security Standard require?

A) Only that containers run as non-root
B) Dropping all capabilities, running as non-root, disallowing privilege escalation, and a seccomp profile
C) No hostPath mounts only
D) No special requirements

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The restricted Pod Security Standard is the most stringent level, requiring: dropping all capabilities (only NET_BIND_SERVICE may be added), running as non-root, disallowing privilege escalation, and requiring a seccomp profile. It enforces current Pod hardening best practices.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/#restricted)

</details>

---

### Question 30
[HARD]

How do you configure Pod Security Admission cluster-wide?

A) Use namespace labels only
B) Configure the PodSecurity admission controller with a configuration file
C) Set cluster-wide annotations
D) Modify the API server binary

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Cluster-wide Pod Security Admission defaults can be configured by providing an AdmissionConfiguration file to the API server with the --admission-control-config-file flag. This sets default policies, exemptions, and audit settings that apply when namespaces don't have explicit labels.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/#pod-security-admission-labels-for-namespaces)

</details>

---

### Question 31
[HARD]

What is the supplementalGroups field used for?

A) To add groups to the primary group
B) To specify additional group IDs for the container process
C) To create new groups
D) To supplement user permissions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The supplementalGroups field specifies additional group IDs that are added to the container's process. These are in addition to the primary GID and any groups from the container image. This is useful for granting access to shared volumes or other group-restricted resources.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 32
[HARD]

How does runAsNonRoot: true work in securityContext?

A) It sets the user to nobody
B) It validates that the container will not run as UID 0 (root)
C) It changes the user at runtime
D) It blocks all root processes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting runAsNonRoot: true validates at container startup that the container will not run as root (UID 0). If the image is configured to run as root and no runAsUser is specified, the container fails to start. It enforces rather than changes the user - it's a validation, not a transformation.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 33
[HARD]

What is the seLinuxOptions field used for?

A) To enable SELinux
B) To set SELinux labels (user, role, type, level) for containers
C) To configure SELinux policies
D) To disable SELinux

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The seLinuxOptions field sets SELinux context labels for containers, including user, role, type, and level. These labels determine what the container process can access under SELinux. The host must have SELinux enabled for these options to take effect.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 34
[HARD]

What happens when you set readOnlyRootFilesystem to true?

A) The image becomes read-only
B) The container's root filesystem is mounted read-only
C) Volumes become read-only
D) Configuration files cannot be changed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting readOnlyRootFilesystem: true mounts the container's root filesystem as read-only. The container cannot write to its filesystem, preventing attackers from modifying binaries or creating files. Writable volumes can still be mounted separately for data that needs to be written.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 35
[HARD]

How do you allow a container to bind to privileged ports (< 1024)?

A) Set privileged: true
B) Add the NET_BIND_SERVICE capability
C) Run as root
D) Use hostNetwork: true

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The NET_BIND_SERVICE capability allows a non-root process to bind to privileged ports (ports below 1024). This is preferable to running as root or in privileged mode, as it grants only the specific capability needed following the principle of least privilege.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-capabilities-for-a-container)

</details>

---

### Question 36
[HARD]

What is the windowsOptions field in securityContext?

A) Configuration for Windows containers
B) Window manager settings
C) Terminal options
D) Display settings

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The windowsOptions field contains security settings specific to Windows containers, including gmsaCredentialSpecName (for Active Directory group managed service accounts), runAsUserName (Windows username), and hostProcess (for privileged Windows containers).

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 37
[HARD]

How do Pod Security Admission exemptions work?

A) By deleting policies
B) By configuring usernames, namespaces, or runtimeClasses that bypass checks
C) By adding annotations
D) Exemptions are not supported

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod Security Admission supports exemptions configured in the admission controller's configuration file. You can exempt specific usernames, runtimeClasses, or namespaces from policy checks. This allows system components or trusted workloads to bypass restrictions without disabling enforcement entirely.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/#exemptions)

</details>

---

## Secrets Management

### Question 38
[MEDIUM]

What is the maximum size limit for a Kubernetes Secret?

A) 1KB
B) 1MB
C) 10MB
D) No limit

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes Secrets have a maximum size limit of 1MB. This limit exists because Secrets are stored in etcd, and large Secrets could impact API server and etcd performance. For larger data, consider using volume mounts or external storage solutions.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#restrictions)

</details>

---

### Question 39
[MEDIUM]

How do you create a Secret from literal values using kubectl?

A) kubectl create secret literal
B) kubectl create secret generic --from-literal=key=value
C) kubectl apply secret
D) kubectl generate secret

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Use `kubectl create secret generic NAME --from-literal=key=value` to create a Secret from literal values. You can specify multiple --from-literal flags for multiple key-value pairs. The generic type creates an Opaque Secret suitable for arbitrary data.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#creating-a-secret)

</details>

---

### Question 40
[MEDIUM-HARD]

What is the stringData field in a Secret manifest?

A) A field for storing string data without base64 encoding
B) A deprecated field
C) A field for storing encrypted strings
D) A field for multi-line strings only

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The stringData field is a write-only convenience field that accepts non-base64-encoded strings. When you create or update a Secret, values in stringData are automatically base64-encoded and merged into the data field. It simplifies Secret creation in YAML manifests.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#creating-a-secret)

</details>

---

### Question 41
[MEDIUM-HARD]

How do Secrets differ from ConfigMaps in terms of security?

A) Secrets are encrypted by default
B) Secrets are stored in tmpfs when mounted, have stricter RBAC defaults, and can be encrypted at rest
C) There is no security difference
D) ConfigMaps are more secure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Secrets have several security advantages: they're stored in tmpfs (memory-backed) when mounted as volumes, they have separate RBAC permissions allowing stricter access control, and they can be encrypted at rest in etcd. However, they're only base64-encoded by default, not encrypted.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 42
[MEDIUM-HARD]

What is the kubernetes.io/basic-auth Secret type used for?

A) For OAuth tokens
B) For storing username and password credentials
C) For API keys
D) For SSH keys

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubernetes.io/basic-auth Secret type stores basic authentication credentials. It requires 'username' and 'password' keys. This type is used for authenticating to services that require basic auth, though the credentials are only base64-encoded, not encrypted.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#basic-authentication-secret)

</details>

---

### Question 43
[HARD]

How does the kube-apiserver encrypt Secrets at rest?

A) Using TLS
B) By configuring an EncryptionConfiguration that specifies encryption providers
C) Secrets are always encrypted automatically
D) Using the kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To encrypt Secrets at rest, you configure an EncryptionConfiguration resource specifying encryption providers (like aescbc, aesgcm, secretbox, or KMS). The API server uses this configuration with the --encryption-provider-config flag to encrypt Secrets before storing them in etcd.

**Source:** [Encrypting Confidential Data at Rest | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

</details>

---

### Question 44
[HARD]

What is envelope encryption for Secrets?

A) Encrypting the Secret manifest
B) Encrypting data with a DEK, then encrypting the DEK with a KEK from a KMS
C) Double encryption with the same key
D) Encrypting during transmission

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Envelope encryption uses two layers: data is encrypted with a Data Encryption Key (DEK), and the DEK is encrypted with a Key Encryption Key (KEK) from an external KMS provider via the KMS plugin. Only the encrypted DEK is stored alongside the data, while the KEK remains in the external KMS.

**Source:** [Using a KMS provider for data encryption | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/)

</details>

---

### Question 45
[HARD]

How are Secret volume mounts updated when the Secret changes?

A) Immediately
B) Eventually by kubelet sync; depends on sync frequency and cache TTL
C) Never; Pods must be restarted
D) Only if the Pod has watch permissions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Secret changes, the kubelet eventually updates the mounted volume. The delay depends on kubelet sync period and API server cache TTL (total delay can be up to sync period + cache TTL). Environment variables from Secrets are NOT updated; only volume mounts are refreshed.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets)

</details>

---

### Question 46
[HARD]

What is the relationship between Secrets and etcd?

A) Secrets are stored in a separate database
B) Secrets are stored in etcd, optionally encrypted at rest
C) etcd cannot store Secrets
D) Secrets are only stored in memory

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Like all Kubernetes resources, Secrets are stored in etcd. By default, they're stored base64-encoded but not encrypted. Enabling encryption at rest (via EncryptionConfiguration) encrypts Secrets before they're written to etcd. Securing etcd access is critical for Secret security.

**Source:** [Encrypting Confidential Data at Rest | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

</details>

---

### Question 47
[HARD]

How can you use external secret management systems with Kubernetes?

A) Direct integration only
B) Using custom controllers or integrations that sync secrets into Kubernetes
C) External systems cannot be used
D) By mounting network volumes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** External secret management systems can be integrated with Kubernetes using custom controllers or integrations that either sync secrets into Kubernetes Secret objects or provide secrets directly to Pods. This keeps the source of truth in a centralized, audited external store while making secrets available to workloads.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#alternatives-to-secrets)

</details>

---

### Question 48
[HARD]

What is the secretRef field used for in Pod specs?

A) To reference a specific key in a Secret
B) To load all key-value pairs from a Secret as environment variables
C) To mount a Secret as a volume
D) To create a new Secret

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The envFrom.secretRef field loads all key-value pairs from a Secret as environment variables in the container. Each key becomes an environment variable name, and its value becomes the variable's value. This is useful for bulk-loading configuration.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#using-secrets-as-environment-variables)

</details>

---

### Question 49
[HARD]

How do you restrict which Pods can access a specific Secret?

A) Using NetworkPolicies
B) Using RBAC to control ServiceAccount access to Secrets
C) Secrets are accessible by all Pods
D) Using Secret labels

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RBAC controls which ServiceAccounts can access Secrets. By creating Roles that grant 'get' permission on specific Secrets and binding them to ServiceAccounts, you control which Pods (using those ServiceAccounts) can access the Secrets. NetworkPolicies don't control Secret access.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/#best-practices)

</details>

---

## Network Policies

### Question 50
[MEDIUM]

What must be installed for NetworkPolicies to have any effect?

A) A firewall
B) A CNI plugin that supports NetworkPolicy
C) A special kernel module
D) The NetworkPolicy controller

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicies are implemented by the CNI (Container Network Interface) plugin. Creating a NetworkPolicy has no effect unless a CNI plugin that supports NetworkPolicy (like Calico, Cilium, or Weave Net) is installed. The default kubenet plugin does not support NetworkPolicy.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 51
[MEDIUM]

Which policyTypes can be specified in a NetworkPolicy?

A) Allow and Deny
B) Ingress and Egress
C) Input and Output
D) Inbound and Outbound

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicies support two policyTypes: "Ingress" (controls incoming traffic to selected Pods) and "Egress" (controls outgoing traffic from selected Pods). You can specify one or both. If not specified, Ingress is assumed if ingress rules exist, and Egress if egress rules exist.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/#the-networkpolicy-resource)

</details>

---

### Question 52
[MEDIUM-HARD]

How do you allow traffic only from Pods with a specific label?

A) Use a nodeSelector
B) Use podSelector in the ingress from field
C) Use a service selector
D) Labels cannot be used in NetworkPolicies

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ingress.from.podSelector field matches Pods by labels. For example, to allow traffic only from Pods with label "role: frontend", specify podSelector with matchLabels: {role: frontend}. This can be combined with namespaceSelector to match Pods in specific namespaces.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/#the-networkpolicy-resource)

</details>

---

### Question 53
[MEDIUM-HARD]

What is the effect of an empty ingress array in a NetworkPolicy?

A) All ingress traffic is allowed
B) All ingress traffic is denied
C) The policy has no effect
D) Only egress is controlled

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An empty ingress array (ingress: []) with policyTypes including "Ingress" denies all incoming traffic to the selected Pods. This creates a deny-all ingress policy. To allow specific traffic, you must add ingress rules. No rules means no traffic is allowed.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/#default-deny-all-ingress-traffic)

</details>

---

### Question 54
[HARD]

How do you create a default deny-all egress policy?

A) Set egress: deny in namespace
B) Create a NetworkPolicy selecting all Pods with policyTypes: ["Egress"] and no egress rules
C) Configure the CNI plugin
D) Use an annotation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To create a default deny-all egress policy, create a NetworkPolicy with podSelector: {} (selects all Pods in namespace), policyTypes: ["Egress"], and no egress rules. This blocks all outbound traffic from Pods in the namespace until explicitly allowed by other policies.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/#default-deny-all-egress-traffic)

</details>

---

### Question 55
[HARD]

What is the ipBlock selector used for in NetworkPolicies?

A) To select Pods by IP
B) To allow or deny traffic to/from specific IP CIDR ranges
C) To block IP addresses
D) To configure IP allocation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ipBlock selector allows specifying CIDR ranges for traffic rules. It's useful for allowing or controlling traffic to/from external IPs, on-premise networks, or specific IP ranges. It includes a 'cidr' field for the range and optional 'except' field for exclusions.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/#the-networkpolicy-resource)

</details>

---

### Question 56
[HARD]

How do NetworkPolicies interact with Services?

A) NetworkPolicies block Service traffic
B) NetworkPolicies apply to Pod IPs, not Service IPs; traffic is filtered after DNAT
C) Services bypass NetworkPolicies
D) NetworkPolicies must reference Services directly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicies operate at the Pod IP level. When traffic goes through a Service, the policy is evaluated after DNAT (Destination NAT) translates the Service IP to the Pod IP. You cannot directly reference Services in NetworkPolicies; you must use Pod selectors or IP blocks.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 57
[HARD]

What is the except field used for in ipBlock selectors?

A) To exclude specific CIDRs from the allowed/denied range
B) To add exceptions to the policy
C) To except certain ports
D) To handle error cases

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The 'except' field in ipBlock allows you to exclude specific CIDR ranges from the main CIDR. For example, allowing 10.0.0.0/8 except 10.0.0.0/24 allows all traffic from 10.x.x.x except the 10.0.0.x subnet. Except CIDRs must be within the main CIDR.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/#the-networkpolicy-resource)

</details>

---

### Question 58
[HARD]

How do you allow egress to external IPs while blocking inter-pod traffic?

A) Cannot be done with NetworkPolicies
B) Use ipBlock to allow external CIDRs while not including Pod CIDRs
C) Use a firewall instead
D) Allow all egress and use another policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** You can use ipBlock to allow external CIDRs (like 0.0.0.0/0) while using 'except' to exclude the cluster's Pod CIDR ranges. This allows egress to external IPs while preventing direct Pod-to-Pod communication that doesn't go through allowed services.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 59
[HARD]

What are the limitations of Kubernetes NetworkPolicies?

A) No limitations
B) No deny rules, no cluster-wide policies, no logging, CNI-dependent enforcement
C) Only work with TCP
D) Cannot cross namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Standard NetworkPolicies have limitations: no explicit deny rules (only allow-list), no cluster-wide policies (must be created per-namespace), no built-in logging, and enforcement depends on CNI plugin support. Some CNI plugins offer extended features beyond the standard API.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

## Authentication

### Question 60
[MEDIUM]

What is a bearer token in Kubernetes authentication?

A) A username/password combination
B) A token sent in the Authorization header to authenticate requests
C) A certificate
D) A cookie

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A bearer token is sent in the HTTP Authorization header as "Authorization: Bearer <token>". The API server validates the token and extracts the user identity. ServiceAccount tokens and static tokens are examples of bearer tokens in Kubernetes.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#putting-a-bearer-token-in-a-request)

</details>

---

### Question 61
[MEDIUM]

How do ServiceAccounts authenticate to the API server?

A) Using username and password
B) Using JWT tokens mounted in Pods
C) Using SSH keys
D) Using IP whitelisting

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ServiceAccounts authenticate using JWT (JSON Web Tokens) that are automatically mounted into Pods at /var/run/secrets/kubernetes.io/serviceaccount/token. The API server validates these tokens against the ServiceAccount signing key to authenticate the Pod.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#service-account-tokens)

</details>

---

### Question 62
[MEDIUM-HARD]

What is the purpose of the --client-ca-file flag on the API server?

A) To set the server certificate
B) To specify the CA bundle for validating client certificates
C) To configure TLS
D) To enable mTLS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The --client-ca-file flag specifies a CA certificate bundle used to validate client certificates presented during X.509 client certificate authentication. If a client presents a certificate signed by one of these CAs, they are authenticated with the CN as username and O as groups.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#x509-client-certs)

</details>

---

### Question 63
[MEDIUM-HARD]

How do you configure multiple authentication methods for the API server?

A) Only one method can be configured
B) Pass multiple authentication flags; the API server tries each in order
C) Use a configuration file only
D) Run multiple API servers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The API server supports multiple authentication methods simultaneously (X.509 certificates, bearer tokens, OIDC, etc.). Configure each using its respective flag. The API server tries each enabled authenticator until one succeeds. If all fail, the request is denied.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

</details>

---

### Question 64
[HARD]

What is the authenticating proxy method?

A) Using a proxy server for load balancing
B) A front proxy that authenticates users and passes identity via headers
C) A reverse proxy for the API server
D) A method to proxy authentication to LDAP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Authenticating proxy authentication allows a front proxy to authenticate users and pass their identity to the API server via request headers (like X-Remote-User, X-Remote-Group). The API server trusts requests from the proxy (validated by client certificate) and extracts identity from headers.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#authenticating-proxy)

</details>

---

### Question 65
[HARD]

How does the API server validate X.509 client certificates?

A) By checking the certificate expiration only
B) By verifying the certificate chain against the configured CA and extracting identity from CN/O
C) By contacting a CA server
D) By comparing to stored certificates

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The API server validates X.509 client certificates by verifying the certificate chain against the CA specified in --client-ca-file and checking expiration. It then extracts the Common Name (CN) as the username and Organization (O) fields as groups. Note: The API server does not check certificate revocation.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#x509-client-certs)

</details>

---

### Question 66
[HARD]

What is the purpose of the --oidc-issuer-url flag?

A) To set the API server URL
B) To specify the OIDC provider URL for token validation
C) To issue OIDC tokens
D) To configure OAuth

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The --oidc-issuer-url flag specifies the URL of the OpenID Connect provider. The API server uses this URL to discover the provider's configuration (via .well-known/openid-configuration) and validate ID tokens by checking the issuer claim matches this URL.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens)

</details>

---

### Question 67
[HARD]

How do static token files work for authentication?

A) Tokens are generated dynamically
B) A CSV file maps tokens to users; the API server reads it at startup
C) Tokens are stored in etcd
D) Each user creates their own token file

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Static token authentication uses a CSV file (--token-auth-file) with format: token,user,uid,"group1,group2". The API server reads this file at startup. Changing tokens requires restarting the API server. This method is simple but not recommended for production.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#static-token-file)

</details>

---

### Question 68
[HARD]

What groups are automatically assigned to authenticated users?

A) No automatic groups
B) system:authenticated is added to all authenticated users
C) admin group
D) users group

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** All authenticated users are automatically added to the system:authenticated group. Similarly, unauthenticated requests (when anonymous auth is enabled) are assigned the system:unauthenticated group. These groups can be used in RBAC bindings for default permissions.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#anonymous-requests)

</details>

---

### Question 69
[HARD]

What is the difference between user impersonation and sudo?

A) No difference
B) Impersonation allows acting as another user via API; sudo elevates privileges locally
C) Sudo is for containers; impersonation is for users
D) Impersonation is more secure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes impersonation (using --as flag or Impersonate headers) allows acting as another user/group for API requests, useful for testing permissions. Unlike sudo which elevates local system privileges, impersonation works at the API level and requires explicit RBAC permission for the "impersonate" verb.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#user-impersonation)

</details>

---

## Authorization

### Question 70
[MEDIUM]

What does it mean when authorization mode is set to AlwaysAllow?

A) Only admin requests are allowed
B) All requests are authorized without checking permissions
C) Only allows RBAC-approved traffic
D) Denies anonymous access

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** AlwaysAllow mode authorizes all requests without any permission checks, including anonymous requests if anonymous authentication is enabled. This mode provides no access control and should never be used in production. It may be used for testing or development scenarios.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#authorization-modules)

</details>

---

### Question 71
[MEDIUM]

Which component makes authorization decisions in Kubernetes?

A) kubelet
B) kube-apiserver
C) kube-controller-manager
D) etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-apiserver makes all authorization decisions. When a request arrives, after authentication, the API server evaluates the request against the configured authorization modules (RBAC, ABAC, Node, Webhook) to determine if the action is permitted.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)

</details>

---

### Question 72
[MEDIUM-HARD]

What information is used to make authorization decisions?

A) Only the username
B) User, group, verb, resource, namespace, and API group
C) Only the resource
D) The request body

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Authorization decisions use multiple request attributes: the authenticated user and groups, the API verb (get, list, create, etc.), the resource type and name, the namespace, and the API group. These attributes are matched against authorization rules (like RBAC policies).

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#review-your-request-attributes)

</details>

---

### Question 73
[MEDIUM-HARD]

How does the --authorization-mode flag work with multiple modes?

A) Only the first mode is used
B) Modes are evaluated in order; if any allows, the request is permitted
C) All modes must agree
D) Modes are randomly selected

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When multiple authorization modes are specified (e.g., --authorization-mode=Node,RBAC), they're evaluated in order. Each authorizer can allow the request or have no opinion (pass). If any authorizer allows, the request proceeds immediately. If all authorizers have no opinion, the request is denied.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#authorization-modules)

</details>

---

### Question 74
[HARD]

What is the SubjectAccessReview API used for?

A) To review user accounts
B) To programmatically check if a subject can perform an action
C) To audit access logs
D) To create new subjects

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** SubjectAccessReview is an API for programmatically checking if a specific user/group can perform an action. You create a SubjectAccessReview resource specifying the subject and action, and the API returns whether it's allowed. Useful for building authorization UIs or automated checks.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#checking-api-access)

</details>

---

### Question 75
[HARD]

How do you configure webhook authorization?

A) Enable it by default
B) Use --authorization-mode=Webhook and --authorization-webhook-config-file
C) Deploy a webhook controller
D) Configure in RBAC

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To enable webhook authorization, set --authorization-mode to include Webhook and specify the webhook configuration using --authorization-webhook-config-file. The config file contains the webhook service URL and authentication credentials for the API server to call the external authorizer.

**Source:** [Webhook Mode | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/webhook/)

</details>

---

### Question 76
[HARD]

What is the SelfSubjectAccessReview API?

A) For reviewing your own account
B) For checking if the current user can perform a specific action
C) For self-service account management
D) For auditing your own actions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** SelfSubjectAccessReview allows users to check their own permissions without needing admin access. Unlike SubjectAccessReview (which checks any user's permissions), SelfSubjectAccessReview only checks the calling user's permissions. This is what `kubectl auth can-i` uses.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#checking-api-access)

</details>

---

### Question 77
[HARD]

How does Node authorization restrict kubelet permissions?

A) By limiting network access
B) By only allowing kubelets to access resources related to Pods scheduled on their node
C) By requiring node certificates
D) By rate limiting requests

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Node authorization restricts kubelets to only access resources they need: reading Services, Endpoints, Nodes, and Pods; reading Secrets/ConfigMaps/PVCs referenced by Pods on their node; and updating their own Node status. This limits the damage if a node is compromised.

**Source:** [Node Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/node/)

</details>

---

### Question 78
[HARD]

What are the special groups in Kubernetes authorization?

A) admin, user, guest
B) system:authenticated, system:unauthenticated, system:masters, system:serviceaccounts
C) root, sudo, operator
D) There are no special groups

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes has special system groups: system:authenticated (all authenticated users), system:unauthenticated (anonymous requests), system:masters (superuser access), system:serviceaccounts (all ServiceAccounts), and system:serviceaccounts:<namespace> (ServiceAccounts in a namespace).

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#default-roles-and-role-bindings)

</details>

---

### Question 79
[HARD]

How can you audit authorization decisions?

A) Check kubectl output
B) Enable audit logging with appropriate audit policy rules
C) Query the authorization API
D) Check etcd directly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To audit authorization decisions, enable Kubernetes audit logging with an audit policy that captures authorization events. The audit log records who made requests, what resources were accessed, and whether requests were allowed or denied. Configure with --audit-policy-file and --audit-log-path.

**Source:** [Auditing | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

</details>

---

## Admission Controllers

### Question 80
[MEDIUM]

When are admission controllers invoked in the API request lifecycle?

A) Before authentication
B) After authentication and authorization, before persistence
C) After object persistence
D) During authentication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Admission controllers are invoked after a request passes authentication and authorization, but before the object is persisted to etcd. The order is: Authentication → Authorization → Mutating Admission → Schema Validation → Validating Admission → Persistence.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

---

### Question 81
[MEDIUM]

Which admission controller sets default values for resource requests?

A) ResourceDefaults
B) LimitRanger
C) DefaultResources
D) ResourceQuota

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The LimitRanger admission controller sets default resource requests and limits based on LimitRange objects in the namespace. If a Pod doesn't specify resource requests/limits, LimitRanger applies the defaults defined in the namespace's LimitRange.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#limitranger)

</details>

---

### Question 82
[MEDIUM]

What is a dynamic admission controller?

A) A controller that changes behavior at runtime
B) An admission webhook that is registered dynamically via API resources
C) A controller that adapts to load
D) A built-in controller that can be configured

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Dynamic admission controllers are webhooks registered through ValidatingWebhookConfiguration or MutatingWebhookConfiguration API resources. Unlike built-in admission controllers that require API server restart to change, webhooks can be added, modified, or removed at runtime.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)

</details>

---

### Question 83
[MEDIUM-HARD]

How do you enable or disable built-in admission controllers?

A) Using a configuration file only
B) Using --enable-admission-plugins and --disable-admission-plugins flags
C) By deploying or removing controllers
D) Through RBAC settings

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Built-in admission controllers are enabled or disabled using API server flags: --enable-admission-plugins adds controllers to the default set, and --disable-admission-plugins removes them. Changes require API server restart. Some controllers are enabled by default.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#how-do-i-turn-on-an-admission-controller)

</details>

---

### Question 84
[MEDIUM-HARD]

What is the purpose of the ResourceQuota admission controller?

A) To set default resource limits
B) To enforce resource quotas on namespaces and reject requests that exceed them
C) To monitor resource usage
D) To allocate resources to pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ResourceQuota admission controller enforces ResourceQuota objects in namespaces. It tracks resource usage and rejects requests that would cause the namespace to exceed its quota. This prevents any single namespace from consuming excessive cluster resources.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#resourcequota)

</details>

---

### Question 85
[HARD]

What is a MutatingWebhookConfiguration?

A) A webhook that changes its own configuration
B) A resource that configures webhooks that can modify objects during admission
C) A configuration for mutating API servers
D) A webhook for configuration changes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** MutatingWebhookConfiguration is a Kubernetes resource that configures mutating admission webhooks. These webhooks can modify (mutate) objects during admission - adding defaults, injecting sidecars, or modifying fields. They run before validating webhooks.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)

</details>

---

### Question 86
[HARD]

How do you specify which resources an admission webhook should process?

A) Using a label selector only
B) Using the rules field with apiGroups, apiVersions, resources, and operations
C) The webhook processes all resources by default
D) Using RBAC rules

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The rules field in webhook configuration specifies which requests trigger the webhook: apiGroups (core, apps, etc.), apiVersions (v1), resources (pods, deployments), and operations (CREATE, UPDATE, DELETE). Only matching requests are sent to the webhook.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#matching-requests-rules)

</details>

---

### Question 87
[HARD]

What is the failurePolicy field in webhook configurations?

A) How to handle webhook errors
B) Defines behavior (Fail or Ignore) when the webhook cannot be reached
C) Policy for failed admissions
D) Retry policy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The failurePolicy field specifies what happens when the webhook cannot be reached or returns an error: "Fail" rejects the request (fail-closed, more secure), "Ignore" allows the request to proceed (fail-open, more available). Default is "Fail".

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#failure-policy)

</details>

---

### Question 88
[HARD]

Which admission controller enforces that images come from allowed registries?

A) ImageRegistry
B) ImagePolicyWebhook or custom ValidatingAdmissionWebhook
C) RegistryEnforcer
D) There is no such controller

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ImagePolicyWebhook admission controller can enforce image policies like requiring images from specific registries by delegating to an external service. Alternatively, a custom ValidatingAdmissionWebhook can implement registry restrictions. There's no built-in controller that directly restricts registries.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook)

</details>

---

### Question 89
[HARD]

How do reinvocation policies work for mutating webhooks?

A) They control retry behavior
B) If set to IfNeeded, webhooks are re-invoked if other webhooks modified the object
C) They control webhook ordering
D) They prevent duplicate invocations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The reinvocationPolicy field (Never or IfNeeded) controls whether mutating webhooks are called again if later webhooks modify the object. "IfNeeded" re-invokes webhooks that need to see the final object state. This handles dependencies between webhooks.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#reinvocation-policy)

</details>

---

## Container Security

### Question 90
[MEDIUM]

What is the difference between an image tag and an image digest?

A) No difference
B) Tags are mutable labels; digests are immutable SHA256 hashes
C) Digests are shorter
D) Tags are more secure

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Image tags (like :latest or :v1.0) are mutable references that can point to different images over time. Digests (sha256:abc123...) are immutable SHA256 hashes that uniquely identify a specific image. Using digests ensures reproducible deployments.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

---

### Question 91
[MEDIUM]

Why is it recommended to run containers as non-root?

A) For better performance
B) To limit damage if the container is compromised; principle of least privilege
C) Containers cannot run as root
D) For easier debugging

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Running containers as non-root follows the principle of least privilege. If a container is compromised, an attacker has limited capabilities compared to root. Root in a container might still exploit kernel vulnerabilities or misconfigured security to escalate privileges.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 92
[MEDIUM-HARD]

What is the purpose of the imagePullPolicy field?

A) To set image compression level
B) To control when kubelet pulls container images (Always, IfNotPresent, Never)
C) To specify image registry credentials
D) To validate image signatures

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The imagePullPolicy field controls when kubelet pulls container images: Always (pull every time), IfNotPresent (pull only if not cached locally), or Never (use local image only). Using Always with immutable tags or digests ensures you always get the intended image version.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/#image-pull-policy)

</details>

---

### Question 93
[HARD]

How do you configure seccomp profiles for containers?

A) Using annotations only
B) Using securityContext.seccompProfile with type and optionally localhostProfile
C) Through the container runtime only
D) Seccomp cannot be configured in Kubernetes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Seccomp profiles are configured via securityContext.seccompProfile. The type can be RuntimeDefault (container runtime's default), Localhost (custom profile from node), or Unconfined (no filtering). For Localhost, specify the profile path via localhostProfile.

**Source:** [Restrict a Container's Syscalls with seccomp | Kubernetes](https://kubernetes.io/docs/tutorials/security/seccomp/)

</details>

---

### Question 94
[HARD]

What are Linux namespaces in container isolation?

A) Kubernetes namespaces
B) Kernel features that isolate process views of system resources (PID, network, mount, etc.)
C) DNS namespaces
D) File naming conventions

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Linux namespaces are kernel features that isolate what a process can see: PID (process IDs), network (network interfaces), mount (filesystems), UTS (hostname), IPC (inter-process communication), and user (UID/GID). Containers use namespaces for isolation from the host and each other.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

---

### Question 95
[HARD]

What is the purpose of supplementalGroups in Pod securityContext?

A) To add users to the Pod
B) To specify additional group IDs applied to all containers in the Pod
C) To create backup groups
D) To define RBAC groups

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The supplementalGroups field specifies a list of additional group IDs that are applied to the first process in each container. These groups are in addition to the container's primary GID and any groups defined in the container image. Useful for accessing shared volumes with specific group permissions.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 96
[HARD]

What is the Unconfined seccomp profile?

A) A highly restrictive profile
B) A profile that applies no seccomp filtering
C) The default secure profile
D) A profile for untrusted workloads

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Unconfined seccomp profile type disables seccomp filtering entirely, allowing all system calls. This is the least secure option and should be avoided. Use RuntimeDefault for basic protection or custom Localhost profiles for fine-grained control.

**Source:** [Restrict a Container's Syscalls with seccomp | Kubernetes](https://kubernetes.io/docs/tutorials/security/seccomp/)

</details>

---

### Question 97
[HARD]

How do cgroups contribute to container security?

A) By encrypting container data
B) By limiting and isolating resource usage (CPU, memory, I/O) to prevent DoS
C) By controlling network access
D) By managing container images

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Control groups (cgroups) limit and isolate resource usage for containers. By setting CPU, memory, and I/O limits, cgroups prevent any single container from consuming all host resources (DoS prevention) and provide fair resource allocation between containers.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

---

### Question 98
[HARD]

Why should you use image digests instead of tags?

A) Digests are shorter
B) Digests are immutable and guarantee you get the exact same image content
C) Tags are deprecated
D) Digests improve pull speed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Image digests (e.g., image@sha256:abc123...) are immutable and uniquely identify specific image content. Unlike tags which can be moved to point to different images, digests guarantee you always pull the exact same image. This prevents unexpected changes when a tag is updated and improves security and reproducibility.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/#image-names)

</details>

---

### Question 99
[HARD]

How do you prevent privilege escalation attacks in containers?

A) Run as root
B) Set allowPrivilegeEscalation: false, drop capabilities, use seccomp, run as non-root
C) Use host networking
D) Disable security contexts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Prevent privilege escalation by: setting allowPrivilegeEscalation: false (prevents setuid binaries), dropping all capabilities, using seccomp profiles to restrict syscalls, running as non-root user, and using read-only root filesystem. The restricted Pod Security Standard enforces these.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 100
[HARD]

What are the security implications of using hostPath volumes?

A) No implications
B) Containers can access and modify host filesystem, potentially escaping isolation
C) Only performance implications
D) hostPath is automatically sandboxed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** hostPath volumes mount host filesystem paths into containers, breaking isolation. Containers can read/write host files, potentially accessing secrets, modifying system files, or exploiting this for container escape. The baseline and restricted Pod Security Standards prohibit hostPath.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---
