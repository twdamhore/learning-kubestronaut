# Security - 100 MCQ Questions (Part A)

**Domain:** Container Orchestration (28%)
**Competency:** Security
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## RBAC Fundamentals

### Question 1
[MEDIUM]

What does RBAC stand for in Kubernetes?

A) Resource-Based Access Control
B) Role-Based Access Control
C) Rule-Based Access Configuration
D) Remote-Based Authentication Control

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RBAC stands for Role-Based Access Control, a method of regulating access to resources based on the roles of individual users within an organization. In Kubernetes, RBAC uses Roles and ClusterRoles to define permissions.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 2
[MEDIUM]

Which Kubernetes resource defines a set of permissions within a specific namespace?

A) ClusterRole
B) RoleBinding
C) Role
D) ServiceAccount

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A Role is a namespaced resource that contains rules representing a set of permissions within a specific namespace. Roles can only grant access to resources within the namespace where they are created.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 3
[MEDIUM-HARD]

What is the difference between a Role and a ClusterRole in Kubernetes?

A) Role is for users, ClusterRole is for service accounts
B) Role is namespace-scoped, ClusterRole is cluster-scoped
C) Role grants read access, ClusterRole grants write access
D) There is no difference; they are aliases

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Role is namespace-scoped and can only grant access to resources within a single namespace. A ClusterRole is cluster-scoped and can grant access to cluster-wide resources, non-resource endpoints, or resources across all namespaces.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 4
[MEDIUM-HARD]

Which resource binds a Role to a user or ServiceAccount within a namespace?

A) ClusterRoleBinding
B) RoleBinding
C) RoleAssignment
D) PermissionBinding

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A RoleBinding grants the permissions defined in a Role to a user or set of users within a specific namespace. It holds a list of subjects (users, groups, or ServiceAccounts) and a reference to the Role being granted.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 5
[MEDIUM-HARD]

What happens if you create a RoleBinding that references a ClusterRole?

A) The binding fails with an error
B) The ClusterRole permissions are granted only within the RoleBinding's namespace
C) The ClusterRole permissions are granted cluster-wide
D) The ClusterRole is automatically converted to a Role

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A RoleBinding can reference a ClusterRole to grant the permissions defined in that ClusterRole, but the permissions are limited to the RoleBinding's namespace. This allows common ClusterRoles to be reused across namespaces with namespace-scoped access.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 6
[HARD]

Which RBAC verb allows a user to create new resources?

A) add
B) create
C) new
D) insert

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "create" verb in RBAC allows a user to create new resources. Standard RBAC verbs include get, list, watch, create, update, patch, delete, and deletecollection.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 7
[HARD]

What is the effect of the "escalate" verb in RBAC?

A) Allows a user to gain root access
B) Allows creating or updating Roles or ClusterRoles with permissions the user doesn't have
C) Allows bypassing admission controllers
D) Allows impersonating other users

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "escalate" verb allows a user to create or modify Roles and ClusterRoles to include permissions that the user does not already have. This is a powerful permission that can lead to privilege escalation and should be granted carefully.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 8
[HARD]

How can you grant permission to access resources across all namespaces?

A) Use a Role with namespace: "*"
B) Use a ClusterRole with a ClusterRoleBinding
C) Use multiple RoleBindings in each namespace
D) Set the global flag on the Role

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To grant permissions across all namespaces, you must use a ClusterRole bound with a ClusterRoleBinding. ClusterRoleBindings grant cluster-wide access to the subjects they reference, applying the ClusterRole's permissions in all namespaces.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 9
[HARD]

What is the purpose of the "bind" verb in RBAC?

A) Allows creating network bindings
B) Allows creating RoleBindings or ClusterRoleBindings that reference Roles or ClusterRoles
C) Allows binding volumes to pods
D) Allows binding services to endpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "bind" verb allows a user to create RoleBindings or ClusterRoleBindings that reference a specific Role or ClusterRole. This prevents users from creating bindings to roles they cannot themselves use, providing a layer of privilege escalation protection.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 10
[HARD]

Which API group contains the RBAC resources in Kubernetes?

A) authorization.k8s.io
B) rbac.authorization.k8s.io
C) access.k8s.io
D) security.k8s.io

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RBAC resources (Role, ClusterRole, RoleBinding, ClusterRoleBinding) are part of the rbac.authorization.k8s.io API group. This group was introduced as part of the RBAC implementation in Kubernetes.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 11
[HARD]

What happens when multiple RoleBindings grant different permissions to the same subject?

A) The most restrictive permissions apply
B) The last applied binding takes precedence
C) Permissions are additive (union of all grants)
D) An error is raised due to conflict

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** RBAC permissions are purely additive. When multiple RoleBindings or ClusterRoleBindings grant permissions to the same subject, the effective permissions are the union of all granted permissions. There are no "deny" rules in RBAC.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 12
[HARD]

How do you restrict access to a specific resource by name using RBAC?

A) Use the resourceNames field in the Role rules
B) Use the nameSelector field in the RoleBinding
C) Use a label selector in the Role
D) Use a separate Role for each resource

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The resourceNames field in a Role's rules allows restricting access to specific instances of a resource by their names. This enables fine-grained access control to individual resources rather than all resources of a type.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

## ServiceAccounts

### Question 13
[MEDIUM]

What is automatically created in every Kubernetes namespace?

A) An admin user
B) A default ServiceAccount
C) A default Role
D) A cluster-admin binding

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes automatically creates a ServiceAccount named "default" in every namespace. If a Pod does not specify a ServiceAccount, it is automatically assigned the default ServiceAccount from its namespace.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 14
[MEDIUM]

Where is a ServiceAccount token typically mounted in a Pod?

A) /etc/kubernetes/token
B) /var/run/secrets/kubernetes.io/serviceaccount
C) /opt/kubernetes/credentials
D) /home/kubernetes/.token

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ServiceAccount tokens are automatically mounted at /var/run/secrets/kubernetes.io/serviceaccount in each container. This directory contains the token, namespace, and CA certificate files needed for API authentication.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 15
[MEDIUM-HARD]

What is the purpose of the automountServiceAccountToken field?

A) To automatically create tokens for new ServiceAccounts
B) To control whether a ServiceAccount token is mounted in Pods
C) To enable automatic token rotation
D) To mount tokens from multiple ServiceAccounts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The automountServiceAccountToken field controls whether Pods using a ServiceAccount will automatically have the token mounted. Setting it to false on either the ServiceAccount or the Pod prevents automatic token mounting, improving security for Pods that don't need API access.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 16
[MEDIUM-HARD]

How do bound ServiceAccount tokens differ from legacy tokens?

A) Bound tokens are stored in Secrets, legacy tokens are not
B) Bound tokens are time-limited and audience-bound
C) Bound tokens can only be used once
D) Bound tokens are encrypted, legacy tokens are not

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bound ServiceAccount tokens are time-limited (they expire) and audience-bound (they specify which audiences can accept them). This improves security compared to legacy tokens stored in Secrets, which never expire and can be used by any audience.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 17
[HARD]

What happens when you specify a non-existent ServiceAccount in a Pod spec?

A) The Pod uses the default ServiceAccount instead
B) The Pod fails to be created with an error
C) Kubernetes automatically creates the ServiceAccount
D) The Pod runs without any ServiceAccount

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If a Pod specifies a ServiceAccount that doesn't exist in the namespace, the Pod creation will fail. Kubernetes validates that the specified ServiceAccount exists before allowing the Pod to be scheduled.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/)

</details>

---

### Question 18
[HARD]

How can you prevent a ServiceAccount token from being automatically mounted?

A) Delete the ServiceAccount
B) Set automountServiceAccountToken: false on the Pod or ServiceAccount
C) Remove the token Secret
D) Use a custom securityContext

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting automountServiceAccountToken: false on either the Pod spec or the ServiceAccount prevents the token from being automatically mounted. The Pod-level setting takes precedence over the ServiceAccount setting.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 19
[HARD]

What information is included in a projected ServiceAccount token?

A) Only the ServiceAccount name
B) Namespace, ServiceAccount name/UID, Pod name/UID, audience, and expiration
C) Username and password
D) The cluster certificate authority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Projected ServiceAccount tokens are JWTs that include claims for the namespace, ServiceAccount name and UID, Pod name and UID, the configured audience, and expiration time. These bound tokens are more secure than legacy tokens because they are time-limited and audience-scoped.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 20
[HARD]

What is the TokenRequest API used for?

A) Requesting new user accounts
B) Requesting short-lived, audience-scoped ServiceAccount tokens
C) Requesting TLS certificates
D) Requesting API server access

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The TokenRequest API allows requesting short-lived, audience-scoped ServiceAccount tokens programmatically. These tokens have configurable expiration times and audiences, providing better security than static Secret-based tokens.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 21
[HARD]

How does token audience validation work in Kubernetes?

A) The token is validated against a list of allowed users
B) The token's audience claim is verified against the expected audience
C) The token is validated by an external identity provider
D) Audience validation is not supported in Kubernetes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Token audience validation verifies that the audience claim in the token matches the expected audience for the requesting service. This prevents tokens issued for one purpose from being used with a different service.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

### Question 22
[HARD]

What happens to bound tokens when a Pod is deleted?

A) They remain valid until expiration
B) They are immediately invalidated
C) They are transferred to another Pod
D) They are converted to legacy tokens

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bound ServiceAccount tokens are immediately invalidated when the Pod they are bound to is deleted. This is a security improvement over legacy tokens, which remained valid until manually deleted.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

</details>

---

## Pod Security

### Question 23
[MEDIUM]

What replaced PodSecurityPolicy in Kubernetes 1.25+?

A) SecurityContextConstraints
B) Pod Security Admission
C) PodSecurityStandards
D) ContainerSecurityPolicy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod Security Admission replaced PodSecurityPolicy starting in Kubernetes 1.25. It enforces Pod Security Standards at the namespace level using labels, providing a simpler and more maintainable security model.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 24
[MEDIUM]

Which Pod Security Standards level is the most restrictive?

A) privileged
B) baseline
C) restricted
D) hardened

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The "restricted" level is the most restrictive Pod Security Standard, enforcing best practices for hardened Pods. It requires dropping all capabilities, running as non-root, disallowing privilege escalation, and using a restricted seccomp profile among other requirements.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 25
[MEDIUM]

What field in a container spec allows running as a specific user ID?

A) userID
B) runAsUser
C) securityUser
D) containerUser

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The runAsUser field in the securityContext specifies the UID to run the container process as. This can be set at both the Pod level and the container level, with the container level taking precedence.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 26
[MEDIUM-HARD]

What is the purpose of the allowPrivilegeEscalation field?

A) To allow containers to run as root
B) To prevent a process from gaining more privileges than its parent
C) To enable sudo access within containers
D) To allow mounting privileged volumes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When allowPrivilegeEscalation is set to false, it prevents a process from gaining more privileges than its parent process. This blocks exploits that rely on setuid binaries or other privilege escalation mechanisms.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 27
[MEDIUM-HARD]

Which securityContext field prevents writing to the container filesystem?

A) readOnly
B) readOnlyRootFilesystem
C) immutableFilesystem
D) noWrite

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The readOnlyRootFilesystem field mounts the container's root filesystem as read-only, preventing any writes to the filesystem. This is a security best practice that limits the impact of container compromises.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 28
[MEDIUM-HARD]

What are the three Pod Security Standards levels?

A) low, medium, high
B) permissive, standard, strict
C) privileged, baseline, restricted
D) open, controlled, locked

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The three Pod Security Standards levels are privileged (unrestricted), baseline (minimally restrictive, prevents known privilege escalations), and restricted (heavily restricted, follows security best practices).

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 29
[HARD]

How do you enforce Pod Security Standards at the namespace level?

A) Create a PodSecurityPolicy in the namespace
B) Apply labels like pod-security.kubernetes.io/enforce to the namespace
C) Configure the kubelet with security settings
D) Create a SecurityContext for the namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod Security Standards are enforced by applying labels to namespaces, such as pod-security.kubernetes.io/enforce: restricted. The Pod Security Admission controller reads these labels and enforces the specified standards.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 30
[HARD]

What Linux capabilities are dropped by the "restricted" Pod Security Standard?

A) Only NET_RAW
B) Only SYS_ADMIN
C) ALL capabilities must be dropped; only NET_BIND_SERVICE may be added back
D) No capabilities are dropped

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The restricted Pod Security Standard requires that ALL capabilities be dropped via capabilities.drop. The only capability that may be added back is NET_BIND_SERVICE (to allow binding to privileged ports without full root). Any other capability in capabilities.add violates the restricted profile.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

---

### Question 31
[HARD]

What is the difference between "enforce", "audit", and "warn" modes in Pod Security Admission?

A) They apply different security levels
B) Enforce blocks violations, audit logs them, warn adds warnings to API responses
C) They control different types of resources
D) There is no difference; they are aliases

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The three modes serve different purposes: enforce rejects Pods that violate the policy, audit logs violations to the audit log without blocking, and warn returns warnings to the user but allows the Pod to be created.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 32
[HARD]

What is the purpose of capabilities.drop in securityContext?

A) To remove Linux capabilities from a container
B) To drop network connections
C) To disable container features
D) To reduce memory allocation

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The capabilities.drop field removes specified Linux capabilities from a container. Dropping capabilities like NET_RAW, SYS_ADMIN, or ALL reduces the attack surface by limiting what system calls the container can make. The restricted Pod Security Standard requires dropping ALL capabilities.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 33
[HARD]

What is the purpose of the runAsNonRoot field?

A) To specify the exact user ID to run as
B) To ensure the container does not run as UID 0
C) To disable root access to the node
D) To prevent privilege escalation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The runAsNonRoot field validates that the container will not run as UID 0 (root). If the container image specifies a root user and runAsNonRoot is true, the container will fail to start.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 34
[HARD]

How do you add a specific Linux capability to a container?

A) Use the capabilities.add field in securityContext
B) Set privileged: true
C) Use the extraCapabilities field
D) Modify the container runtime configuration

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Linux capabilities can be added to a container using the capabilities.add field in the container's securityContext. Similarly, capabilities.drop removes capabilities. This allows fine-grained control over container privileges.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 35
[HARD]

What is the seccompProfile field used for?

A) To enable SELinux
B) To configure system call filtering for containers
C) To set memory limits
D) To configure AppArmor profiles

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The seccompProfile field configures seccomp (secure computing mode) profiles that filter which system calls a container can make. This reduces the attack surface by limiting available kernel interfaces.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 36
[HARD]

What happens if a Pod violates a namespace's "enforce" Pod Security Standard?

A) The Pod is created but flagged
B) The Pod creation is rejected by the API server
C) The Pod runs with reduced privileges
D) A warning is logged but the Pod is created

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Pod violates a namespace's enforce-level Pod Security Standard, the API server rejects the Pod creation request. The Pod is not created, and an error is returned to the user.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 37
[HARD]

How can you exempt specific namespaces from Pod Security Admission?

A) Delete the namespace labels
B) Configure exemptions in the PodSecurity admission controller configuration
C) Create an exemption Role
D) Namespaces cannot be exempted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Exemptions can be configured in the PodSecurity admission controller's configuration file. Exemptions can be based on usernames, runtimeClassNames, or namespaces, allowing certain workloads to bypass policy enforcement.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

## Secrets Management

### Question 38
[MEDIUM]

How are Kubernetes Secrets encoded by default?

A) Encrypted with AES-256
B) Base64 encoded
C) Plain text
D) Hashed with SHA-256

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes Secrets are base64 encoded by default, not encrypted. Base64 encoding is not a security measure—it simply allows binary data to be stored. Encryption at rest must be separately configured.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 39
[MEDIUM]

Which Secret type is used for storing Docker registry credentials?

A) kubernetes.io/basic-auth
B) kubernetes.io/dockerconfigjson
C) kubernetes.io/ssh-auth
D) kubernetes.io/registry

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubernetes.io/dockerconfigjson Secret type stores Docker registry credentials in the same format as ~/.docker/config.json. It's used for authenticating to private container registries when pulling images.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 40
[MEDIUM-HARD]

What are the two ways to expose a Secret to a Pod?

A) ConfigMap and Volume
B) Environment variables and volume mounts
C) Labels and annotations
D) Direct API access and sidecar

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Secrets can be exposed to Pods as environment variables using envFrom or valueFrom, or as files in a volume mount. Volume mounts are generally preferred as they can be updated without restarting the Pod.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 41
[MEDIUM-HARD]

What is encryption at rest for Secrets?

A) Encrypting Secrets during network transmission
B) Encrypting Secret data stored in etcd
C) Encrypting the Secret manifest files
D) Encrypting container memory

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Encryption at rest refers to encrypting Secret data as it is stored in etcd, the Kubernetes data store. This protects against unauthorized access to the etcd data files and backups.

**Source:** [Encrypting Secret Data at Rest | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

</details>

---

### Question 42
[MEDIUM-HARD]

Which Secret type is used for legacy ServiceAccount token Secrets?

A) kubernetes.io/service-account-token
B) kubernetes.io/basic-auth
C) Opaque
D) kubernetes.io/tls

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The kubernetes.io/service-account-token Secret type is used for legacy ServiceAccount tokens. Since Kubernetes v1.24, token Secrets are no longer automatically created for ServiceAccounts; instead, the TokenRequest API and projected volumes are used. This Secret type remains for backward compatibility and manual token creation.

**Source:** [Service Accounts | Kubernetes](https://kubernetes.io/docs/concepts/security/service-accounts/#service-account-token-secrets)

</details>

---

### Question 43
[HARD]

How do you configure encryption at rest for Secrets in Kubernetes?

A) Enable TLS on the API server
B) Configure an EncryptionConfiguration and pass it to the API server
C) Set the encrypted flag on each Secret
D) Use a special Secret type

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Encryption at rest is configured by creating an EncryptionConfiguration file that specifies encryption providers and keys, then passing it to the kube-apiserver using the --encryption-provider-config flag.

**Source:** [Encrypting Secret Data at Rest | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

</details>

---

### Question 44
[HARD]

What is the difference between Opaque and kubernetes.io/tls Secret types?

A) Opaque is encrypted, TLS is not
B) Opaque is for arbitrary data, TLS requires tls.crt and tls.key fields
C) TLS Secrets can only be used by Ingress
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Opaque is the default Secret type for arbitrary user-defined data. The kubernetes.io/tls type requires specific keys (tls.crt and tls.key) and validates that they contain valid PEM-encoded certificate and key data.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 45
[HARD]

How are Secret updates handled when mounted as volumes?

A) Pods must be restarted to see updates
B) Updates are eventually propagated to mounted volumes automatically
C) Updates are never propagated
D) Only environment variable Secrets are updated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When Secrets are mounted as volumes, the kubelet periodically syncs the mounted data with the current Secret value. The sync period depends on the kubelet's sync configuration and cache TTL. Environment variables are not updated.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 46
[HARD]

What is the immutable field used for in Secrets?

A) To encrypt the Secret
B) To prevent the Secret from being modified after creation
C) To make the Secret persist across cluster restarts
D) To prevent the Secret from being deleted

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting immutable: true prevents any changes to the Secret's data after creation. This improves performance (kubelet doesn't need to watch for changes) and provides protection against accidental or unwanted modifications.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 47
[HARD]

What encryption providers are supported for encrypting Secrets at rest?

A) Only AES-CBC
B) identity, secretbox, aesgcm, aescbc, and KMS providers
C) Only KMS
D) RSA and AES only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes supports multiple encryption providers: identity (no encryption), secretbox, aesgcm, aescbc, and KMS (Key Management Service) providers. KMS providers integrate with external key management systems like AWS KMS, Google Cloud KMS, or HashiCorp Vault.

**Source:** [Encrypting Secret Data at Rest | Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

</details>

---

### Question 48
[HARD]

How can you reference a specific key from a Secret in an environment variable?

A) Use secretKeyRef in the env valueFrom field
B) Use the key name directly as the variable name
C) Reference the full Secret and extract the key
D) Keys cannot be referenced individually

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** To reference a specific key from a Secret as an environment variable, use the secretKeyRef field within the env.valueFrom specification, specifying the Secret name and the key to extract.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

---

### Question 49
[HARD]

What is the minimum RBAC permission needed to read a specific Secret?

A) cluster-admin role
B) get verb on secrets resource
C) list and watch verbs on secrets resource
D) read-only ClusterRole

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To read a specific Secret, a subject needs the get verb on the secrets resource. The list verb is only needed to enumerate all Secrets, and watch is only needed for streaming updates. The get verb alone is sufficient to retrieve a Secret by name.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

## Network Policies

### Question 50
[MEDIUM]

What is the default network behavior for Pods without any NetworkPolicy?

A) All traffic is denied
B) All traffic is allowed
C) Only intra-namespace traffic is allowed
D) Only DNS traffic is allowed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, Pods are non-isolated and accept traffic from any source. NetworkPolicies are additive—only when a policy selects a Pod does the Pod become isolated, with only explicitly allowed traffic permitted.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 51
[MEDIUM]

Which resource is used to control traffic flow between Pods?

A) SecurityPolicy
B) NetworkPolicy
C) TrafficPolicy
D) PodPolicy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicy is the Kubernetes resource used to control network traffic flow at the IP address or port level. It allows you to specify how Pods are allowed to communicate with each other and with external endpoints.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 52
[MEDIUM-HARD]

What happens when you apply a NetworkPolicy that selects a Pod?

A) All traffic to that Pod is blocked
B) The Pod becomes isolated and only explicitly allowed traffic is permitted
C) The Pod's network is reset
D) Nothing changes until the policy is activated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a NetworkPolicy selects a Pod, that Pod becomes isolated for the specified traffic direction (ingress and/or egress). Only traffic explicitly allowed by NetworkPolicy rules is permitted; all other traffic in that direction is denied.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 53
[MEDIUM-HARD]

How do you create a default deny-all ingress policy for a namespace?

A) Set a namespace annotation
B) Create a NetworkPolicy with empty ingress rules that selects all Pods
C) Configure the CNI plugin
D) Use a ClusterNetworkPolicy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A default deny-all ingress policy is created by defining a NetworkPolicy with an empty podSelector (selecting all Pods), specifying policyTypes: ["Ingress"], and providing no ingress rules. This isolates all Pods in the namespace for ingress traffic.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 54
[HARD]

Do NetworkPolicies apply to Pods that use hostNetwork: true?

A) Yes, NetworkPolicies apply to all Pods
B) No, hostNetwork Pods bypass NetworkPolicy enforcement
C) Only egress policies apply
D) Only ingress policies apply

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicies do not apply to Pods that use hostNetwork: true. These Pods share the host's network namespace and are not isolated by Pod network policies. This is an important security consideration when designing network isolation strategies.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 55
[HARD]

What are the three types of selectors available in NetworkPolicy rules?

A) podSelector, nodeSelector, serviceSelector
B) podSelector, namespaceSelector, ipBlock
C) labelSelector, fieldSelector, nameSelector
D) ingressSelector, egressSelector, policySelector

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicy ingress and egress rules support three selector types: podSelector (select Pods by labels), namespaceSelector (select Pods in namespaces by namespace labels), and ipBlock (select IP CIDR ranges for external traffic).

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 56
[HARD]

How do you allow traffic from Pods in a different namespace using NetworkPolicy?

A) Use a ClusterNetworkPolicy
B) Use namespaceSelector in the ingress rules
C) Reference the namespace directly by name
D) NetworkPolicies cannot cross namespaces

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To allow traffic from Pods in other namespaces, use namespaceSelector in the ingress from rules. The selector matches namespaces by their labels, and you can combine it with podSelector to further filter which Pods are allowed.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 57
[HARD]

What is the effect of an empty podSelector in a NetworkPolicy?

A) The policy applies to no Pods
B) The policy applies to all Pods in the namespace
C) The policy is invalid
D) The policy applies cluster-wide

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An empty podSelector {} in a NetworkPolicy selects all Pods in the policy's namespace. This is commonly used to create default deny policies or policies that apply to the entire namespace.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 58
[HARD]

How do you create an egress policy that allows DNS traffic?

A) Allow all UDP traffic
B) Allow egress to DNS pods using namespaceSelector/podSelector on port 53 UDP/TCP
C) DNS traffic is always allowed
D) Use a special DNS exception field

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To allow DNS traffic in an egress policy, explicitly allow traffic to port 53 (both UDP and TCP) targeting DNS pods. Since NetworkPolicies cannot select Services directly, use namespaceSelector to target kube-system and podSelector to match CoreDNS/kube-dns pods, or use ipBlock with the DNS ClusterIP. DNS traffic is not automatically exempted from NetworkPolicies.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 59
[HARD]

What is required for NetworkPolicies to be enforced in a cluster?

A) A NetworkPolicy controller
B) A CNI plugin that supports NetworkPolicy
C) The NetworkPolicy API to be enabled
D) A special kernel module

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NetworkPolicies require a CNI plugin that implements the NetworkPolicy specification. Creating NetworkPolicy resources has no effect unless the CNI plugin enforces them. Examples of supporting plugins include Calico, Cilium, and Weave Net.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

## Authentication

### Question 60
[MEDIUM]

Which component handles authentication in Kubernetes?

A) kubelet
B) kube-apiserver
C) kube-controller-manager
D) etcd

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-apiserver handles authentication for all API requests. It supports multiple authentication methods (certificates, tokens, OIDC, etc.) and verifies the identity of clients before processing requests.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/)

</details>

---

### Question 61
[MEDIUM]

What is the default location where kubectl looks for cluster configuration?

A) /etc/kubernetes/admin.conf
B) ~/.kube/config
C) /var/lib/kubelet/kubeconfig
D) /opt/kubernetes/config

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, kubectl looks for a file named config in the ~/.kube directory. This can be overridden using the KUBECONFIG environment variable or the --kubeconfig flag. The kubeconfig file contains cluster connection details, authentication credentials, and context information.

**Source:** [Organizing Cluster Access Using kubeconfig Files | Kubernetes](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)

</details>

---

### Question 62
[MEDIUM-HARD]

What authentication method uses X.509 certificates?

A) Token authentication
B) Client certificate authentication
C) OIDC authentication
D) Basic authentication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Client certificate authentication uses X.509 certificates to authenticate users to the Kubernetes API server. The API server is configured with a certificate authority (CA), and any client presenting a valid certificate signed by that CA is authenticated. The certificate's Common Name (CN) becomes the username.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#x509-client-certs)

</details>

---

### Question 63
[MEDIUM-HARD]

How does OpenID Connect (OIDC) authentication work with Kubernetes?

A) Kubernetes acts as an OIDC provider
B) Users authenticate with an external OIDC provider and present tokens to the API server
C) OIDC replaces all other authentication methods
D) OIDC is only for ServiceAccounts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With OIDC authentication, users authenticate with an external identity provider (like Google, Okta, or Keycloak) and receive an ID token. This token is then presented to the Kubernetes API server, which validates it against the configured OIDC provider. Kubernetes does not act as an OIDC provider itself.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#openid-connect-tokens)

</details>

---

### Question 64
[HARD]

What is the difference between authentication and authorization in Kubernetes?

A) They are the same thing
B) Authentication verifies identity; authorization determines what actions are permitted
C) Authentication is for users; authorization is for services
D) Authentication uses RBAC; authorization uses certificates

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Authentication (authn) verifies who you are - confirming your identity through certificates, tokens, or other credentials. Authorization (authz) determines what you can do - checking if your authenticated identity has permission to perform the requested action. In Kubernetes, authentication happens first, then authorization is checked using modes like RBAC.

**Source:** [Controlling Access to the Kubernetes API | Kubernetes](https://kubernetes.io/docs/concepts/security/controlling-access/)

</details>

---

### Question 65
[HARD]

How are users represented in Kubernetes?

A) As User resources in the API
B) Users are not represented as API objects; they exist externally
C) As special ServiceAccounts
D) As ConfigMaps with user data

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes does not have User objects or a built-in user management system. Normal users are managed externally through private keys, certificates, or external identity providers. The API server extracts user identity from authentication credentials but doesn't store user information. ServiceAccounts are the only type of identity managed by Kubernetes itself.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#users-in-kubernetes)

</details>

---

### Question 66
[HARD]

What is the purpose of the --anonymous-auth flag on the API server?

A) To disable all authentication
B) To control whether unauthenticated requests are allowed
C) To enable anonymous user creation
D) To log anonymous access attempts

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The --anonymous-auth flag controls whether anonymous requests to the API server are allowed. When enabled (default), requests that fail all authentication methods are assigned the username system:anonymous and group system:unauthenticated. Authorization rules can then permit or deny these anonymous requests.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#anonymous-requests)

</details>

---

### Question 67
[HARD]

How do bootstrap tokens work in Kubernetes?

A) They are permanent tokens for cluster access
B) They are short-lived tokens used for node joining and initial cluster setup
C) They replace ServiceAccount tokens
D) They are used for kubectl authentication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Bootstrap tokens are short-lived tokens stored as Secrets in the kube-system namespace. They are primarily used for cluster bootstrapping, particularly when joining new nodes with kubeadm. These tokens have a configurable TTL and are designed for initial cluster setup, not ongoing authentication.

**Source:** [Authenticating with Bootstrap Tokens | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/bootstrap-tokens/)

</details>

---

### Question 68
[HARD]

What information is extracted from an X.509 client certificate for authentication?

A) Only the public key
B) The Common Name (CN) as username and Organization (O) as groups
C) The certificate serial number
D) The issuer name only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When using X.509 client certificate authentication, Kubernetes extracts the Common Name (CN) field as the username and the Organization (O) fields as group memberships. For example, a certificate with CN=jane and O=developers,O=admins would authenticate as user "jane" in groups "developers" and "admins".

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#x509-client-certs)

</details>

---

### Question 69
[HARD]

What is the webhook token authentication method?

A) Using webhooks to generate tokens
B) Validating bearer tokens by calling an external webhook service
C) Authenticating webhook requests
D) Creating tokens for webhook endpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Webhook token authentication allows the API server to validate bearer tokens by making a request to an external webhook service. When a token is presented, the API server sends a TokenReview request to the configured webhook, which responds with whether the token is valid and the associated user information.

**Source:** [Authenticating | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication)

</details>

---

## Authorization

### Question 70
[MEDIUM]

Which authorization mode uses Roles and RoleBindings to grant permissions?

A) ABAC
B) RBAC
C) AlwaysAllow
D) Webhook

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RBAC (Role-Based Access Control) uses Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings to define and grant permissions. Roles define permissions within a namespace, while ClusterRoles define cluster-wide permissions. Bindings associate users or groups with roles.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

</details>

---

### Question 71
[MEDIUM]

Which authorization mode grants full access to the cluster?

A) RBAC
B) Node
C) AlwaysAllow
D) Webhook

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The AlwaysAllow authorization mode grants all requests without any permission checks, effectively giving full access to everyone. This mode should never be used in production environments as it provides no access control. It may be used in development or testing scenarios.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#authorization-modules)

</details>

---

### Question 72
[MEDIUM-HARD]

Which authorization modes are available in Kubernetes?

A) Only RBAC and ABAC
B) RBAC, ABAC, and Webhook only
C) Node, RBAC, ABAC, Webhook, AlwaysAllow, and AlwaysDeny
D) RBAC and Node only

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Kubernetes supports six authorization modes: Node (for kubelet authorization), RBAC (Role-Based Access Control), ABAC (Attribute-Based Access Control), Webhook (external authorization service), AlwaysAllow (permits all requests), and AlwaysDeny (blocks all requests). Multiple modes can be enabled simultaneously using the --authorization-mode flag.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#authorization-modules)

</details>

---

### Question 73
[MEDIUM-HARD]

How does the Node authorization mode work?

A) Grants full access to nodes
B) Authorizes kubelets to access resources needed to run Pods scheduled on their node
C) Allows nodes to authenticate users
D) Controls which nodes can join the cluster

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Node authorization mode specifically authorizes API requests made by kubelets. It grants kubelets permission to read Services, Endpoints, Nodes, Pods, and Secrets/ConfigMaps/PVCs bound to Pods scheduled on their node. This limits kubelet access to only the resources they need.

**Source:** [Node Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/node/)

</details>

---

### Question 74
[HARD]

In what order are authorization modes evaluated?

A) Alphabetically
B) In the order specified in --authorization-mode
C) RBAC is always evaluated first
D) All modes must agree

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Authorization modes are evaluated in the order specified in the --authorization-mode flag using short-circuit logic. The first authorizer to return allow or deny decides the outcome immediately. If an authorizer has no opinion, evaluation continues to the next. If all authorizers have no opinion, the request is denied by default.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#authorization-modules)

</details>

---

### Question 75
[HARD]

What is Attribute-Based Access Control (ABAC)?

A) Authorization based on resource attributes only
B) Authorization using policy files that define rules based on request attributes
C) A newer replacement for RBAC
D) Authorization based on Active Directory attributes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ABAC (Attribute-Based Access Control) grants access based on policies defined in a file. Each policy specifies attributes like user, group, namespace, and resource that must match for the request to be allowed. ABAC requires API server restart to update policies, making RBAC the preferred choice for most deployments.

**Source:** [Using ABAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/abac/)

</details>

---

### Question 76
[HARD]

How does webhook authorization work?

A) Webhooks create authorization tokens
B) The API server sends authorization requests to an external HTTP service
C) Webhooks bypass normal authorization
D) Authorization decisions are cached in webhooks

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Webhook authorization allows the API server to delegate authorization decisions to an external HTTP service. The API server sends a SubjectAccessReview request containing the user and request details, and the webhook responds with whether the request should be allowed or denied.

**Source:** [Webhook Mode | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/webhook/)

</details>

---

### Question 77
[HARD]

What happens if all authorization modes deny a request?

A) The request is allowed by default
B) The request is denied with a 403 Forbidden response
C) The request is retried
D) The cluster admin is notified

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** If all configured authorization modes deny a request (or none approve it), the API server returns an HTTP 403 Forbidden response. The default behavior is deny-all; explicit approval from at least one authorizer is required for a request to proceed.

**Source:** [Authorization Overview | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/)

</details>

---

### Question 78
[HARD]

What is the purpose of the system:masters group?

A) To identify master nodes
B) To provide superuser access via the cluster-admin ClusterRoleBinding
C) To manage the control plane
D) To identify cluster administrators

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The system:masters group is bound to the cluster-admin ClusterRole by a default ClusterRoleBinding, granting full access to all resources via RBAC. This is not a bypass of RBAC but rather RBAC working as intended with a built-in binding. Members of this group have superuser privileges. This group should be used sparingly.

**Source:** [Using RBAC Authorization | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#default-roles-and-role-bindings)

</details>

---

### Question 79
[HARD]

How can you check if a user has permission to perform an action?

A) Use kubectl describe user
B) Use kubectl auth can-i
C) Check the API server logs
D) Query the RBAC API directly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `kubectl auth can-i` command checks whether the current user (or a specified user with --as) has permission to perform a given action. For example, `kubectl auth can-i create pods` returns yes or no. Administrators can also use `--list` to see all allowed actions.

**Source:** [Checking API Access | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/authorization/#checking-api-access)

</details>

---

## Admission Controllers

### Question 80
[MEDIUM]

What is an admission controller in Kubernetes?

A) A component that manages user admission to the cluster
B) Code that intercepts requests to the API server before object persistence
C) A network policy controller
D) A certificate authority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Admission controllers are plugins that intercept requests to the Kubernetes API server after authentication and authorization but before the object is persisted. They can validate or mutate (modify) the request, enforcing policies and defaults on resources being created or updated.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

---

### Question 81
[MEDIUM]

Which admission controller enforces Pod Security Standards?

A) PodSecurityPolicy
B) PodSecurity
C) SecurityContextDeny
D) PodSecurityAdmission

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The PodSecurity admission controller enforces Pod Security Standards (privileged, baseline, restricted) at the namespace level. It replaced the deprecated PodSecurityPolicy in Kubernetes v1.25. The controller is configured using namespace labels.

**Source:** [Pod Security Admission | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

</details>

---

### Question 82
[MEDIUM]

What is the difference between validating and mutating admission controllers?

A) Validating controllers are faster
B) Mutating controllers can modify objects; validating controllers only accept or reject
C) Validating controllers run first
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Mutating admission controllers can modify the objects they process, adding defaults or changing fields. Validating admission controllers only accept or reject requests without modification. Mutating controllers run first so validators can check the final modified object.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

---

### Question 83
[MEDIUM-HARD]

In what order are mutating and validating admission webhooks called?

A) Validating first, then mutating
B) Mutating first, then validating
C) They run in parallel
D) The order is random

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Mutating admission webhooks are called first, allowing them to modify the object. Then validating webhooks are called to verify the final object. This order ensures validators check the complete, modified object rather than the original request.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/)

</details>

---

### Question 84
[MEDIUM-HARD]

Which admission controller ensures namespaces exist before creating resources?

A) NamespaceAutoProvision
B) NamespaceExists
C) NamespaceLifecycle
D) NamespaceValidator

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The NamespaceLifecycle admission controller prevents creating resources in non-existent namespaces, blocks deletion of system namespaces (default, kube-system, kube-public), and prevents creating resources in namespaces that are being terminated.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#namespacelifecycle)

</details>

---

### Question 85
[HARD]

How do you configure a custom validating admission webhook?

A) Modify the API server configuration
B) Create a ValidatingWebhookConfiguration resource
C) Deploy a special controller
D) Use kubectl plugins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Custom validating admission webhooks are configured by creating a ValidatingWebhookConfiguration resource. This resource specifies the webhook service endpoint, which resources to intercept, the failure policy, and other settings. No API server restart is required.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#configure-admission-webhooks-on-the-fly)

</details>

---

### Question 86
[HARD]

What is the purpose of the LimitRanger admission controller?

A) To limit the number of resources in a namespace
B) To enforce default resource requests/limits and validate against LimitRange objects
C) To limit API request rates
D) To enforce network bandwidth limits

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The LimitRanger admission controller enforces LimitRange objects in namespaces. It sets default resource requests and limits for Pods that don't specify them, and validates that resource requests/limits fall within the defined ranges. It also enforces min/max ratios.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#limitranger)

</details>

---

### Question 87
[HARD]

What happens if an admission webhook is unavailable?

A) The request always fails
B) Depends on the failurePolicy setting (Fail or Ignore)
C) The request always succeeds
D) The API server retries indefinitely

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The failurePolicy field in webhook configuration determines behavior when the webhook is unavailable or returns an error. "Fail" rejects the request (fail-closed), while "Ignore" allows it to proceed (fail-open). The default is "Fail" for security.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#failure-policy)

</details>

---

### Question 88
[HARD]

What does the NamespaceLifecycle admission controller prevent?

A) Deletion of namespaces with finalizers
B) Creation of objects in non-existent or terminating namespaces
C) Creation of namespaces with invalid names
D) Deletion of system namespaces only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The NamespaceLifecycle admission controller prevents creation of objects in namespaces that don't exist or are being terminated. It also prevents deletion of the default, kube-system, and kube-public namespaces. Note: Finalizers on namespace objects prevent actual deletion until they're removed, but this is a separate mechanism from NamespaceLifecycle.

**Source:** [Using Admission Controllers | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#namespacelifecycle)

</details>

---

### Question 89
[HARD]

How can you exclude certain resources from admission webhook processing?

A) Use the excludeResources field
B) Use rules, namespaceSelector, and objectSelector in the webhook configuration
C) Webhooks process all resources
D) Add an annotation to skip webhooks

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Webhook configurations support several mechanisms to control which requests are sent to the webhook: the rules field specifies which API groups, versions, resources, and operations to match; namespaceSelector filters by namespace labels; and objectSelector filters by object labels. matchPolicy only controls Exact vs Equivalent matching, not exclusions.

**Source:** [Dynamic Admission Control | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/#matching-requests)

</details>

---

## Container Security

### Question 90
[MEDIUM]

What is a container image digest?

A) A compressed version of the image
B) A SHA256 hash that uniquely identifies an image
C) The image's metadata
D) A signature for the image

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A container image digest is a SHA256 hash of the image manifest that uniquely and immutably identifies a specific image version. Unlike tags which can be moved to point to different images, digests are content-addressable and cannot change.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

---

### Question 91
[MEDIUM]

What does the privileged field in securityContext control?

A) Whether the container can access the host network
B) Whether the container runs with all Linux capabilities and host device access
C) Whether the container can run as root user
D) Whether the container can mount volumes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting privileged: true gives the container nearly equivalent access to the host as processes running outside containers. This includes all Linux capabilities, access to all host devices, and the ability to modify certain kernel parameters. Privileged containers should be avoided in production.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 92
[MEDIUM-HARD]

What is seccomp in the context of container security?

A) A secure computing mode that filters system calls
B) A secure communication protocol
C) A secret management system
D) A security compliance tool

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Seccomp (Secure Computing Mode) is a Linux kernel feature that restricts which system calls a process can make. Kubernetes supports seccomp profiles to limit container syscalls, reducing the attack surface. Profiles can allow, deny, or log specific syscalls.

**Source:** [Restrict a Container's Syscalls with seccomp | Kubernetes](https://kubernetes.io/docs/tutorials/security/seccomp/)

</details>

---

### Question 93
[HARD]

How do you specify an image by digest instead of tag?

A) image: myimage:sha256@abc123
B) image: myimage@sha256:abc123...
C) image: myimage#sha256:abc123
D) digest: sha256:abc123 in the image spec

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To reference an image by digest, use the @ symbol followed by sha256: and the full digest hash (e.g., nginx@sha256:abc123...). This ensures the exact image version is used regardless of any tag changes, providing immutable deployments.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/#image-names)

</details>

---

### Question 94
[HARD]

What is AppArmor and how is it used with Kubernetes?

A) A network firewall for containers
B) A Linux security module that restricts program capabilities via profiles
C) A container runtime
D) An admission controller

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** AppArmor is a Linux Security Module that restricts programs' capabilities using per-program profiles. In Kubernetes, AppArmor profiles are applied to containers via securityContext.appArmorProfile, which specifies the profile type (RuntimeDefault, Localhost, or Unconfined) and restricts file access, network capabilities, and other operations.

**Source:** [Restrict a Container's Access to Resources with AppArmor | Kubernetes](https://kubernetes.io/docs/tutorials/security/apparmor/)

</details>

---

### Question 95
[HARD]

What is the RuntimeDefault seccomp profile?

A) A profile that blocks all system calls
B) The container runtime's default seccomp profile
C) A profile with no restrictions
D) A profile specific to Kubernetes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** RuntimeDefault refers to the container runtime's (containerd, CRI-O) default seccomp profile. It provides a reasonable security baseline by blocking dangerous syscalls while allowing common operations. Setting seccompProfile.type: RuntimeDefault applies this profile to containers.

**Source:** [Restrict a Container's Syscalls with seccomp | Kubernetes](https://kubernetes.io/docs/tutorials/security/seccomp/)

</details>

---

### Question 96
[HARD]

How do container runtimes provide isolation between containers?

A) Using virtual machines
B) Using Linux namespaces, cgroups, and security modules
C) Using network segmentation only
D) Using separate physical servers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Container runtimes use Linux kernel features for isolation: namespaces isolate process trees, network, mounts, and users; cgroups limit and account for resource usage (CPU, memory); and security modules (SELinux, AppArmor, seccomp) restrict what processes can do.

**Source:** [Container Runtime Interface | Kubernetes](https://kubernetes.io/docs/concepts/architecture/cri/)

</details>

---

### Question 97
[HARD]

What is the purpose of the fsGroup field in Pod securityContext?

A) To set file system quotas
B) To specify a supplemental group that owns Pod volumes
C) To configure file system encryption
D) To limit file system access

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The fsGroup field specifies a supplemental group ID that is applied to all containers in the Pod. Files created in volumes will be owned by this group, and the group ownership of volume contents is changed to this GID. This enables multiple containers to share volume data with proper permissions.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 98
[HARD]

What is the purpose of the runAsGroup field in securityContext?

A) To specify which group can create the Pod
B) To specify the primary GID that the container process will run as
C) To limit which groups can access the Pod
D) To define which Kubernetes group the Pod belongs to

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The runAsGroup field specifies the primary group ID (GID) that the container's main process will run as. This affects file creation permissions and group membership. Like runAsUser, it can be set at the Pod level or container level. When combined with fsGroup, it provides fine-grained control over file permissions.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---

### Question 99
[HARD]

What are the security implications of sharing the host PID namespace?

A) No security implications
B) Container can see and potentially signal host processes
C) Only affects networking
D) Improves container isolation

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting hostPID: true allows container processes to see all processes on the host node. This breaks process isolation - containers can view process information, environment variables (potentially containing secrets), and with appropriate privileges, send signals to host processes.

**Source:** [Share Process Namespace between Containers | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/share-process-namespace/)

</details>

---

### Question 100
[HARD]

What is the purpose of the procMount field in securityContext?

A) To mount the proc filesystem
B) To control how /proc is mounted in the container (Default or Unmasked)
C) To configure process limits
D) To enable process monitoring

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The procMount field controls how the /proc filesystem is mounted in the container. "Default" uses the container runtime's default masked /proc (hiding sensitive paths), while "Unmasked" provides an unmasked /proc. Unmasked is only allowed when privileged mode is also enabled.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

---
