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
B) Allows creating or updating Roles with permissions the user doesn't have
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
B) Allows creating RoleBindings or ClusterRoleBindings that reference Roles
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

What is the default ServiceAccount used by Pods if none is specified?

A) system:serviceaccount
B) kube-system
C) default
D) pod-default

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** If a Pod does not specify a ServiceAccount, it is assigned the "default" ServiceAccount from the Pod's namespace. Every namespace has a "default" ServiceAccount created automatically.

**Source:** [Configure Service Accounts for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

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
B) The namespace, ServiceAccount name, Pod name, and expiration time
C) Username and password
D) The cluster certificate authority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Projected ServiceAccount tokens are JWTs that include claims for the namespace, ServiceAccount name, Pod name (and UID), and expiration time. They also include the configured audience, making them more secure than legacy tokens.

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

**Explanation:** The "restricted" level is the most restrictive Pod Security Standard, enforcing best practices for hardened Pods. It requires dropping all capabilities, running as non-root, and using read-only root filesystems among other restrictions.

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
C) ALL capabilities must be dropped
D) No capabilities are dropped

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The restricted Pod Security Standard requires that ALL capabilities be dropped. Containers may only add back the NET_BIND_SERVICE capability if needed. This follows the principle of least privilege.

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

Which securityContext field controls whether a container can gain more privileges than its parent process?

A) privileged
B) allowPrivilegeEscalation
C) runAsNonRoot
D) capabilities

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The allowPrivilegeEscalation field controls whether a process can gain more privileges than its parent. Setting it to false prevents exploits using setuid binaries and is required by the restricted Pod Security Standard.

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

---

### Question 42
[MEDIUM-HARD]

Which Secret type is automatically created for ServiceAccounts?

A) kubernetes.io/service-account-token
B) kubernetes.io/basic-auth
C) Opaque
D) kubernetes.io/tls

---

### Question 43
[HARD]

How do you configure encryption at rest for Secrets in Kubernetes?

A) Enable TLS on the API server
B) Configure an EncryptionConfiguration and pass it to the API server
C) Set the encrypted flag on each Secret
D) Use a special Secret type

---

### Question 44
[HARD]

What is the difference between Opaque and kubernetes.io/tls Secret types?

A) Opaque is encrypted, TLS is not
B) Opaque is for arbitrary data, TLS requires tls.crt and tls.key fields
C) TLS Secrets can only be used by Ingress
D) There is no difference

---

### Question 45
[HARD]

How are Secret updates handled when mounted as volumes?

A) Pods must be restarted to see updates
B) Updates are eventually propagated to mounted volumes automatically
C) Updates are never propagated
D) Only environment variable Secrets are updated

---

### Question 46
[HARD]

What is the immutable field used for in Secrets?

A) To encrypt the Secret
B) To prevent the Secret from being modified after creation
C) To make the Secret persist across cluster restarts
D) To prevent the Secret from being deleted

---

### Question 47
[HARD]

What encryption providers are supported for encrypting Secrets at rest?

A) Only AES-CBC
B) identity, secretbox, aesgcm, aescbc, and KMS providers
C) Only KMS
D) RSA and AES only

---

### Question 48
[HARD]

How can you reference a specific key from a Secret in an environment variable?

A) Use secretKeyRef in the env valueFrom field
B) Use the key name directly as the variable name
C) Reference the full Secret and extract the key
D) Keys cannot be referenced individually

---

### Question 49
[HARD]

What RBAC permissions are needed to read Secrets in a namespace?

A) cluster-admin only
B) get and list verbs on secrets resource
C) Any authenticated user can read Secrets
D) read-only ClusterRole

---

## Network Policies

### Question 50
[MEDIUM]

What is the default network behavior for Pods without any NetworkPolicy?

A) All traffic is denied
B) All traffic is allowed
C) Only intra-namespace traffic is allowed
D) Only DNS traffic is allowed

---

### Question 51
[MEDIUM]

Which resource is used to control traffic flow between Pods?

A) SecurityPolicy
B) NetworkPolicy
C) TrafficPolicy
D) PodPolicy

---

### Question 52
[MEDIUM-HARD]

What happens when you apply a NetworkPolicy that selects a Pod?

A) All traffic to that Pod is blocked
B) The Pod becomes isolated and only explicitly allowed traffic is permitted
C) The Pod's network is reset
D) Nothing changes until the policy is activated

---

### Question 53
[MEDIUM-HARD]

How do you create a default deny-all ingress policy for a namespace?

A) Set a namespace annotation
B) Create a NetworkPolicy with empty ingress rules that selects all Pods
C) Configure the CNI plugin
D) Use a ClusterNetworkPolicy

---

### Question 54
[HARD]

Can NetworkPolicies block traffic from the Kubernetes API server?

A) Yes, always
B) No, API server traffic bypasses NetworkPolicies
C) It depends on the CNI plugin implementation
D) Only with a ClusterNetworkPolicy

---

### Question 55
[HARD]

What are the three types of selectors available in NetworkPolicy rules?

A) podSelector, nodeSelector, serviceSelector
B) podSelector, namespaceSelector, ipBlock
C) labelSelector, fieldSelector, nameSelector
D) ingressSelector, egressSelector, policySelector

---

### Question 56
[HARD]

How do you allow traffic from Pods in a different namespace using NetworkPolicy?

A) Use a ClusterNetworkPolicy
B) Use namespaceSelector in the ingress rules
C) Reference the namespace directly by name
D) NetworkPolicies cannot cross namespaces

---

### Question 57
[HARD]

What is the effect of an empty podSelector in a NetworkPolicy?

A) The policy applies to no Pods
B) The policy applies to all Pods in the namespace
C) The policy is invalid
D) The policy applies cluster-wide

---

### Question 58
[HARD]

How do you create an egress policy that allows DNS traffic?

A) Allow all UDP traffic
B) Allow egress to port 53 UDP (and TCP) to the DNS service or kube-dns namespace
C) DNS traffic is always allowed
D) Use a special DNS exception field

---

### Question 59
[HARD]

What is required for NetworkPolicies to be enforced in a cluster?

A) A NetworkPolicy controller
B) A CNI plugin that supports NetworkPolicy
C) The NetworkPolicy API to be enabled
D) A special kernel module

---

## Authentication

### Question 60
[MEDIUM]

Which component handles authentication in Kubernetes?

A) kubelet
B) kube-apiserver
C) kube-controller-manager
D) etcd

---

### Question 61
[MEDIUM]

What file contains cluster connection information and credentials for kubectl?

A) /etc/kubernetes/admin.conf
B) ~/.kube/config
C) /var/lib/kubelet/kubeconfig
D) Both A and B can be used

---

### Question 62
[MEDIUM-HARD]

What authentication method uses X.509 certificates?

A) Token authentication
B) Client certificate authentication
C) OIDC authentication
D) Basic authentication

---

### Question 63
[MEDIUM-HARD]

How does OpenID Connect (OIDC) authentication work with Kubernetes?

A) Kubernetes acts as an OIDC provider
B) Users authenticate with an external OIDC provider and present tokens to the API server
C) OIDC replaces all other authentication methods
D) OIDC is only for ServiceAccounts

---

### Question 64
[HARD]

What is the difference between authentication and authorization in Kubernetes?

A) They are the same thing
B) Authentication verifies identity; authorization determines what actions are permitted
C) Authentication is for users; authorization is for services
D) Authentication uses RBAC; authorization uses certificates

---

### Question 65
[HARD]

How are users represented in Kubernetes?

A) As User resources in the API
B) Users are not represented as API objects; they exist externally
C) As special ServiceAccounts
D) As ConfigMaps with user data

---

### Question 66
[HARD]

What is the purpose of the --anonymous-auth flag on the API server?

A) To disable all authentication
B) To control whether unauthenticated requests are allowed
C) To enable anonymous user creation
D) To log anonymous access attempts

---

### Question 67
[HARD]

How do bootstrap tokens work in Kubernetes?

A) They are permanent tokens for cluster access
B) They are short-lived tokens used for node joining and initial cluster setup
C) They replace ServiceAccount tokens
D) They are used for kubectl authentication

---

### Question 68
[HARD]

What information is extracted from an X.509 client certificate for authentication?

A) Only the public key
B) The Common Name (CN) as username and Organization (O) as groups
C) The certificate serial number
D) The issuer name only

---

### Question 69
[HARD]

What is the webhook token authentication method?

A) Using webhooks to generate tokens
B) Validating bearer tokens by calling an external webhook service
C) Authenticating webhook requests
D) Creating tokens for webhook endpoints

---

## Authorization

### Question 70
[MEDIUM]

What is the default authorization mode in most Kubernetes distributions?

A) ABAC
B) RBAC
C) AlwaysAllow
D) Webhook

---

### Question 71
[MEDIUM]

Which authorization mode grants full access to the cluster?

A) RBAC
B) Node
C) AlwaysAllow
D) Webhook

---

### Question 72
[MEDIUM-HARD]

What are the four authorization modes available in Kubernetes?

A) RBAC, ABAC, Webhook, AlwaysAllow
B) Node, RBAC, ABAC, Webhook
C) RBAC, Node, AlwaysAllow, AlwaysDeny
D) All of the above modes exist

---

### Question 73
[MEDIUM-HARD]

How does the Node authorization mode work?

A) Grants full access to nodes
B) Authorizes kubelets to access resources needed to run Pods scheduled on their node
C) Allows nodes to authenticate users
D) Controls which nodes can join the cluster

---

### Question 74
[HARD]

In what order are authorization modes evaluated?

A) Alphabetically
B) In the order specified in --authorization-mode, first allow wins
C) RBAC is always evaluated first
D) All modes must agree

---

### Question 75
[HARD]

What is Attribute-Based Access Control (ABAC)?

A) Authorization based on resource attributes only
B) Authorization using policy files that define rules based on request attributes
C) A newer replacement for RBAC
D) Authorization based on Active Directory attributes

---

### Question 76
[HARD]

How does webhook authorization work?

A) Webhooks create authorization tokens
B) The API server sends authorization requests to an external HTTP service
C) Webhooks bypass normal authorization
D) Authorization decisions are cached in webhooks

---

### Question 77
[HARD]

What happens if all authorization modes deny a request?

A) The request is allowed by default
B) The request is denied with a 403 Forbidden response
C) The request is retried
D) The cluster admin is notified

---

### Question 78
[HARD]

What is the purpose of the system:masters group?

A) To identify master nodes
B) To grant unrestricted superuser access that bypasses RBAC
C) To manage the control plane
D) To identify cluster administrators

---

### Question 79
[HARD]

How can you check if a user has permission to perform an action?

A) Use kubectl describe user
B) Use kubectl auth can-i
C) Check the API server logs
D) Query the RBAC API directly

---

## Admission Controllers

### Question 80
[MEDIUM]

What is an admission controller in Kubernetes?

A) A component that manages user admission to the cluster
B) Code that intercepts requests to the API server before object persistence
C) A network policy controller
D) A certificate authority

---

### Question 81
[MEDIUM]

Which admission controller enforces Pod Security Standards?

A) PodSecurityPolicy
B) PodSecurity
C) SecurityContextDeny
D) PodSecurityAdmission

---

### Question 82
[MEDIUM]

What is the difference between validating and mutating admission controllers?

A) Validating controllers are faster
B) Mutating controllers can modify objects; validating controllers only accept or reject
C) Validating controllers run first
D) There is no difference

---

### Question 83
[MEDIUM-HARD]

In what order are mutating and validating admission webhooks called?

A) Validating first, then mutating
B) Mutating first, then validating
C) They run in parallel
D) The order is random

---

### Question 84
[MEDIUM-HARD]

Which admission controller ensures namespaces exist before creating resources?

A) NamespaceAutoProvision
B) NamespaceExists
C) NamespaceLifecycle
D) NamespaceValidator

---

### Question 85
[HARD]

How do you configure a custom validating admission webhook?

A) Modify the API server configuration
B) Create a ValidatingWebhookConfiguration resource
C) Deploy a special controller
D) Use kubectl plugins

---

### Question 86
[HARD]

What is the purpose of the LimitRanger admission controller?

A) To limit the number of resources in a namespace
B) To enforce default resource requests/limits and validate against LimitRange objects
C) To limit API request rates
D) To enforce network bandwidth limits

---

### Question 87
[HARD]

What happens if an admission webhook is unavailable?

A) The request always fails
B) Depends on the failurePolicy setting (Fail or Ignore)
C) The request always succeeds
D) The API server retries indefinitely

---

### Question 88
[HARD]

Which admission controller prevents deletion of namespaces with finalizers?

A) NamespaceLifecycle
B) FinalizerProtection
C) ResourceProtection
D) DeletionGuard

---

### Question 89
[HARD]

How can you exclude certain resources from admission webhook processing?

A) Use the excludeResources field
B) Use namespaceSelector, objectSelector, or matchPolicy in the webhook configuration
C) Webhooks process all resources
D) Add an annotation to skip webhooks

---

## Container Security

### Question 90
[MEDIUM]

What is a container image digest?

A) A compressed version of the image
B) A SHA256 hash that uniquely identifies an image
C) The image's metadata
D) A signature for the image

---

### Question 91
[MEDIUM]

What is the purpose of a read-only root filesystem?

A) To improve performance
B) To prevent malicious processes from modifying the filesystem
C) To reduce image size
D) To enable faster container startup

---

### Question 92
[MEDIUM-HARD]

What is seccomp in the context of container security?

A) A secure computing mode that filters system calls
B) A secure communication protocol
C) A secret management system
D) A security compliance tool

---

### Question 93
[HARD]

How do you specify an image by digest instead of tag?

A) image: myimage:sha256@abc123
B) image: myimage@sha256:abc123...
C) image: myimage#sha256:abc123
D) digest: sha256:abc123 in the image spec

---

### Question 94
[HARD]

What is AppArmor and how is it used with Kubernetes?

A) A network firewall for containers
B) A Linux security module that restricts program capabilities via profiles
C) A container runtime
D) An admission controller

---

### Question 95
[HARD]

What is the RuntimeDefault seccomp profile?

A) A profile that blocks all system calls
B) The container runtime's default seccomp profile
C) A profile with no restrictions
D) A profile specific to Kubernetes

---

### Question 96
[HARD]

How do container runtimes provide isolation between containers?

A) Using virtual machines
B) Using Linux namespaces, cgroups, and security modules
C) Using network segmentation only
D) Using separate physical servers

---

### Question 97
[HARD]

What is the purpose of the privileged flag in a container security context?

A) To run as root user
B) To give the container almost all capabilities of the host
C) To enable network privileges
D) To access secrets

---

### Question 98
[HARD]

How do you prevent a container from running as root?

A) Set privileged: false
B) Set runAsNonRoot: true in securityContext
C) Use a non-root base image only
D) Configure the container runtime

---

### Question 99
[HARD]

What are the security implications of sharing the host PID namespace?

A) No security implications
B) Container can see and potentially signal host processes
C) Only affects networking
D) Improves container isolation

---

### Question 100
[HARD]

What is the purpose of the procMount field in securityContext?

A) To mount the proc filesystem
B) To control how /proc is mounted in the container (Default or Unmasked)
C) To configure process limits
D) To enable process monitoring

---
