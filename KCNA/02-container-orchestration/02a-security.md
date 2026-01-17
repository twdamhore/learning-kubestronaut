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

---

### Question 2
[MEDIUM]

Which Kubernetes resource defines a set of permissions within a specific namespace?

A) ClusterRole
B) RoleBinding
C) Role
D) ServiceAccount

---

### Question 3
[MEDIUM-HARD]

What is the difference between a Role and a ClusterRole in Kubernetes?

A) Role is for users, ClusterRole is for service accounts
B) Role is namespace-scoped, ClusterRole is cluster-scoped
C) Role grants read access, ClusterRole grants write access
D) There is no difference; they are aliases

---

### Question 4
[MEDIUM-HARD]

Which resource binds a Role to a user or ServiceAccount within a namespace?

A) ClusterRoleBinding
B) RoleBinding
C) RoleAssignment
D) PermissionBinding

---

### Question 5
[MEDIUM-HARD]

What happens if you create a RoleBinding that references a ClusterRole?

A) The binding fails with an error
B) The ClusterRole permissions are granted only within the RoleBinding's namespace
C) The ClusterRole permissions are granted cluster-wide
D) The ClusterRole is automatically converted to a Role

---

### Question 6
[HARD]

Which RBAC verb allows a user to create new resources?

A) add
B) create
C) new
D) insert

---

### Question 7
[HARD]

What is the effect of the "escalate" verb in RBAC?

A) Allows a user to gain root access
B) Allows creating or updating Roles with permissions the user doesn't have
C) Allows bypassing admission controllers
D) Allows impersonating other users

---

### Question 8
[HARD]

How can you grant permission to access resources across all namespaces?

A) Use a Role with namespace: "*"
B) Use a ClusterRole with a ClusterRoleBinding
C) Use multiple RoleBindings in each namespace
D) Set the global flag on the Role

---

### Question 9
[HARD]

What is the purpose of the "bind" verb in RBAC?

A) Allows creating network bindings
B) Allows creating RoleBindings or ClusterRoleBindings that reference Roles
C) Allows binding volumes to pods
D) Allows binding services to endpoints

---

### Question 10
[HARD]

Which API group contains the RBAC resources in Kubernetes?

A) authorization.k8s.io
B) rbac.authorization.k8s.io
C) access.k8s.io
D) security.k8s.io

---

### Question 11
[HARD]

What happens when multiple RoleBindings grant different permissions to the same subject?

A) The most restrictive permissions apply
B) The last applied binding takes precedence
C) Permissions are additive (union of all grants)
D) An error is raised due to conflict

---

### Question 12
[HARD]

How do you restrict access to a specific resource by name using RBAC?

A) Use the resourceNames field in the Role rules
B) Use the nameSelector field in the RoleBinding
C) Use a label selector in the Role
D) Use a separate Role for each resource

---

## ServiceAccounts

### Question 13
[MEDIUM]

What is automatically created in every Kubernetes namespace?

A) An admin user
B) A default ServiceAccount
C) A default Role
D) A cluster-admin binding

---

### Question 14
[MEDIUM]

Where is a ServiceAccount token typically mounted in a Pod?

A) /etc/kubernetes/token
B) /var/run/secrets/kubernetes.io/serviceaccount
C) /opt/kubernetes/credentials
D) /home/kubernetes/.token

---

### Question 15
[MEDIUM-HARD]

What is the purpose of the automountServiceAccountToken field?

A) To automatically create tokens for new ServiceAccounts
B) To control whether a ServiceAccount token is mounted in Pods
C) To enable automatic token rotation
D) To mount tokens from multiple ServiceAccounts

---

### Question 16
[MEDIUM-HARD]

How do bound ServiceAccount tokens differ from legacy tokens?

A) Bound tokens are stored in Secrets, legacy tokens are not
B) Bound tokens are time-limited and audience-bound
C) Bound tokens can only be used once
D) Bound tokens are encrypted, legacy tokens are not

---

### Question 17
[HARD]

What is the default ServiceAccount used by Pods if none is specified?

A) system:serviceaccount
B) kube-system
C) default
D) pod-default

---

### Question 18
[HARD]

How can you prevent a ServiceAccount token from being automatically mounted?

A) Delete the ServiceAccount
B) Set automountServiceAccountToken: false on the Pod or ServiceAccount
C) Remove the token Secret
D) Use a custom securityContext

---

### Question 19
[HARD]

What information is included in a projected ServiceAccount token?

A) Only the ServiceAccount name
B) The namespace, ServiceAccount name, Pod name, and expiration time
C) Username and password
D) The cluster certificate authority

---

### Question 20
[HARD]

What is the TokenRequest API used for?

A) Requesting new user accounts
B) Requesting short-lived, audience-scoped ServiceAccount tokens
C) Requesting TLS certificates
D) Requesting API server access

---

### Question 21
[HARD]

How does token audience validation work in Kubernetes?

A) The token is validated against a list of allowed users
B) The token's audience claim is verified against the expected audience
C) The token is validated by an external identity provider
D) Audience validation is not supported in Kubernetes

---

### Question 22
[HARD]

What happens to bound tokens when a Pod is deleted?

A) They remain valid until expiration
B) They are immediately invalidated
C) They are transferred to another Pod
D) They are converted to legacy tokens

---

## Pod Security

### Question 23
[MEDIUM]

What replaced PodSecurityPolicy in Kubernetes 1.25+?

A) SecurityContextConstraints
B) Pod Security Admission
C) PodSecurityStandards
D) ContainerSecurityPolicy

---

### Question 24
[MEDIUM]

Which Pod Security Standards level is the most restrictive?

A) privileged
B) baseline
C) restricted
D) hardened

---

### Question 25
[MEDIUM]

What field in a container spec allows running as a specific user ID?

A) userID
B) runAsUser
C) securityUser
D) containerUser

---

### Question 26
[MEDIUM-HARD]

What is the purpose of the allowPrivilegeEscalation field?

A) To allow containers to run as root
B) To prevent a process from gaining more privileges than its parent
C) To enable sudo access within containers
D) To allow mounting privileged volumes

---

### Question 27
[MEDIUM-HARD]

Which securityContext field prevents writing to the container filesystem?

A) readOnly
B) readOnlyRootFilesystem
C) immutableFilesystem
D) noWrite

---

### Question 28
[MEDIUM-HARD]

What are the three Pod Security Standards levels?

A) low, medium, high
B) permissive, standard, strict
C) privileged, baseline, restricted
D) open, controlled, locked

---

### Question 29
[HARD]

How do you enforce Pod Security Standards at the namespace level?

A) Create a PodSecurityPolicy in the namespace
B) Apply labels like pod-security.kubernetes.io/enforce to the namespace
C) Configure the kubelet with security settings
D) Create a SecurityContext for the namespace

---

### Question 30
[HARD]

What Linux capabilities are dropped by the "restricted" Pod Security Standard?

A) Only NET_RAW
B) Only SYS_ADMIN
C) ALL capabilities must be dropped
D) No capabilities are dropped

---

### Question 31
[HARD]

What is the difference between "enforce", "audit", and "warn" modes in Pod Security Admission?

A) They apply different security levels
B) Enforce blocks violations, audit logs them, warn adds warnings to API responses
C) They control different types of resources
D) There is no difference; they are aliases

---

### Question 32
[HARD]

Which securityContext field controls whether a container can gain more privileges than its parent process?

A) privileged
B) allowPrivilegeEscalation
C) runAsNonRoot
D) capabilities

---

### Question 33
[HARD]

What is the purpose of the runAsNonRoot field?

A) To specify the exact user ID to run as
B) To ensure the container does not run as UID 0
C) To disable root access to the node
D) To prevent privilege escalation

---

### Question 34
[HARD]

How do you add a specific Linux capability to a container?

A) Use the capabilities.add field in securityContext
B) Set privileged: true
C) Use the extraCapabilities field
D) Modify the container runtime configuration

---

### Question 35
[HARD]

What is the seccompProfile field used for?

A) To enable SELinux
B) To configure system call filtering for containers
C) To set memory limits
D) To configure AppArmor profiles

---

### Question 36
[HARD]

What happens if a Pod violates a namespace's "enforce" Pod Security Standard?

A) The Pod is created but flagged
B) The Pod creation is rejected by the API server
C) The Pod runs with reduced privileges
D) A warning is logged but the Pod is created

---

### Question 37
[HARD]

How can you exempt specific namespaces from Pod Security Admission?

A) Delete the namespace labels
B) Configure exemptions in the PodSecurity admission controller configuration
C) Create an exemption Role
D) Namespaces cannot be exempted

---

## Secrets Management

### Question 38
[MEDIUM]

How are Kubernetes Secrets encoded by default?

A) Encrypted with AES-256
B) Base64 encoded
C) Plain text
D) Hashed with SHA-256

---

### Question 39
[MEDIUM]

Which Secret type is used for storing Docker registry credentials?

A) kubernetes.io/basic-auth
B) kubernetes.io/dockerconfigjson
C) kubernetes.io/ssh-auth
D) kubernetes.io/registry

---

### Question 40
[MEDIUM-HARD]

What are the two ways to expose a Secret to a Pod?

A) ConfigMap and Volume
B) Environment variables and volume mounts
C) Labels and annotations
D) Direct API access and sidecar

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

---

### Question 52
[MEDIUM-HARD]

What happens when you apply a NetworkPolicy that selects a Pod?

---

### Question 53
[MEDIUM-HARD]

How do you create a default deny-all ingress policy for a namespace?

---

### Question 54
[HARD]

Can NetworkPolicies block traffic from the Kubernetes API server?

---

### Question 55
[HARD]

What are the three types of selectors available in NetworkPolicy rules?

---

### Question 56
[HARD]

How do you allow traffic from Pods in a different namespace using NetworkPolicy?

---

### Question 57
[HARD]

What is the effect of an empty podSelector in a NetworkPolicy?

---

### Question 58
[HARD]

How do you create an egress policy that allows DNS traffic?

---

### Question 59
[HARD]

What is required for NetworkPolicies to be enforced in a cluster?

---

## Authentication

### Question 60
[MEDIUM]

Which component handles authentication in Kubernetes?

---

### Question 61
[MEDIUM]

What file contains cluster connection information and credentials for kubectl?

---

### Question 62
[MEDIUM-HARD]

What authentication method uses X.509 certificates?

---

### Question 63
[MEDIUM-HARD]

How does OpenID Connect (OIDC) authentication work with Kubernetes?

---

### Question 64
[HARD]

What is the difference between authentication and authorization in Kubernetes?

---

### Question 65
[HARD]

How are users represented in Kubernetes?

---

### Question 66
[HARD]

What is the purpose of the --anonymous-auth flag on the API server?

---

### Question 67
[HARD]

How do bootstrap tokens work in Kubernetes?

---

### Question 68
[HARD]

What information is extracted from an X.509 client certificate for authentication?

---

### Question 69
[HARD]

What is the webhook token authentication method?

---

## Authorization

### Question 70
[MEDIUM]

What is the default authorization mode in most Kubernetes distributions?

---

### Question 71
[MEDIUM]

Which authorization mode grants full access to the cluster?

---

### Question 72
[MEDIUM-HARD]

What are the four authorization modes available in Kubernetes?

---

### Question 73
[MEDIUM-HARD]

How does the Node authorization mode work?

---

### Question 74
[HARD]

In what order are authorization modes evaluated?

---

### Question 75
[HARD]

What is Attribute-Based Access Control (ABAC)?

---

### Question 76
[HARD]

How does webhook authorization work?

---

### Question 77
[HARD]

What happens if all authorization modes deny a request?

---

### Question 78
[HARD]

What is the purpose of the system:masters group?

---

### Question 79
[HARD]

How can you check if a user has permission to perform an action?

---

## Admission Controllers

### Question 80
[MEDIUM]

What is an admission controller in Kubernetes?

---

### Question 81
[MEDIUM]

Which admission controller enforces Pod Security Standards?

---

### Question 82
[MEDIUM]

What is the difference between validating and mutating admission controllers?

---

### Question 83
[MEDIUM-HARD]

In what order are mutating and validating admission webhooks called?

---

### Question 84
[MEDIUM-HARD]

Which admission controller ensures namespaces exist before creating resources?

---

### Question 85
[HARD]

How do you configure a custom validating admission webhook?

---

### Question 86
[HARD]

What is the purpose of the LimitRanger admission controller?

---

### Question 87
[HARD]

What happens if an admission webhook is unavailable?

---

### Question 88
[HARD]

Which admission controller prevents deletion of namespaces with finalizers?

---

### Question 89
[HARD]

How can you exclude certain resources from admission webhook processing?

---

## Container Security

### Question 90
[MEDIUM]

What is a container image digest?

---

### Question 91
[MEDIUM]

What is the purpose of a read-only root filesystem?

---

### Question 92
[MEDIUM-HARD]

What is seccomp in the context of container security?

---

### Question 93
[HARD]

How do you specify an image by digest instead of tag?

---

### Question 94
[HARD]

What is AppArmor and how is it used with Kubernetes?

---

### Question 95
[HARD]

What is the RuntimeDefault seccomp profile?

---

### Question 96
[HARD]

How do container runtimes provide isolation between containers?

---

### Question 97
[HARD]

What is the purpose of the privileged flag in a container security context?

---

### Question 98
[HARD]

How do you prevent a container from running as root?

---

### Question 99
[HARD]

What are the security implications of sharing the host PID namespace?

---

### Question 100
[HARD]

What is the purpose of the procMount field in securityContext?

---
