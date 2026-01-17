# Security - 100 MCQ Questions (Part A)

**Domain:** Container Orchestration (28%)
**Competency:** Security
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## RBAC Fundamentals

### Question 1
[MEDIUM]

What does RBAC stand for in Kubernetes?

---

### Question 2
[MEDIUM]

Which Kubernetes resource defines a set of permissions within a specific namespace?

---

### Question 3
[MEDIUM-HARD]

What is the difference between a Role and a ClusterRole in Kubernetes?

---

### Question 4
[MEDIUM-HARD]

Which resource binds a Role to a user or ServiceAccount within a namespace?

---

### Question 5
[MEDIUM-HARD]

What happens if you create a RoleBinding that references a ClusterRole?

---

### Question 6
[HARD]

Which RBAC verb allows a user to create new resources?

---

### Question 7
[HARD]

What is the effect of the "escalate" verb in RBAC?

---

### Question 8
[HARD]

How can you grant permission to access resources across all namespaces?

---

### Question 9
[HARD]

What is the purpose of the "bind" verb in RBAC?

---

### Question 10
[HARD]

Which API group contains the RBAC resources in Kubernetes?

---

### Question 11
[HARD]

What happens when multiple RoleBindings grant different permissions to the same subject?

---

### Question 12
[HARD]

How do you restrict access to a specific resource by name using RBAC?

---

## ServiceAccounts

### Question 13
[MEDIUM]

What is automatically created in every Kubernetes namespace?

---

### Question 14
[MEDIUM]

Where is a ServiceAccount token typically mounted in a Pod?

---

### Question 15
[MEDIUM-HARD]

What is the purpose of the automountServiceAccountToken field?

---

### Question 16
[MEDIUM-HARD]

How do bound ServiceAccount tokens differ from legacy tokens?

---

### Question 17
[HARD]

What is the default ServiceAccount used by Pods if none is specified?

---

### Question 18
[HARD]

How can you prevent a ServiceAccount token from being automatically mounted?

---

### Question 19
[HARD]

What information is included in a projected ServiceAccount token?

---

### Question 20
[HARD]

What is the TokenRequest API used for?

---

### Question 21
[HARD]

How does token audience validation work in Kubernetes?

---

### Question 22
[HARD]

What happens to bound tokens when a Pod is deleted?

---

## Pod Security

### Question 23
[MEDIUM]

What replaced PodSecurityPolicy in Kubernetes 1.25+?

---

### Question 24
[MEDIUM]

Which Pod Security Standards level is the most restrictive?

---

### Question 25
[MEDIUM]

What field in a container spec allows running as a specific user ID?

---

### Question 26
[MEDIUM-HARD]

What is the purpose of the allowPrivilegeEscalation field?

---

### Question 27
[MEDIUM-HARD]

Which securityContext field prevents writing to the container filesystem?

---

### Question 28
[MEDIUM-HARD]

What are the three Pod Security Standards levels?

---

### Question 29
[HARD]

How do you enforce Pod Security Standards at the namespace level?

---

### Question 30
[HARD]

What Linux capabilities are dropped by the "restricted" Pod Security Standard?

---

### Question 31
[HARD]

What is the difference between "enforce", "audit", and "warn" modes in Pod Security Admission?

---

### Question 32
[HARD]

Which securityContext field controls whether a container can gain more privileges than its parent process?

---

### Question 33
[HARD]

What is the purpose of the runAsNonRoot field?

---

### Question 34
[HARD]

How do you add a specific Linux capability to a container?

---

### Question 35
[HARD]

What is the seccompProfile field used for?

---

### Question 36
[HARD]

What happens if a Pod violates a namespace's "enforce" Pod Security Standard?

---

### Question 37
[HARD]

How can you exempt specific namespaces from Pod Security Admission?

---

## Secrets Management

### Question 38
[MEDIUM]

How are Kubernetes Secrets encoded by default?

---

### Question 39
[MEDIUM]

Which Secret type is used for storing Docker registry credentials?

---

### Question 40
[MEDIUM-HARD]

What are the two ways to expose a Secret to a Pod?

---

### Question 41
[MEDIUM-HARD]

What is encryption at rest for Secrets?

---

### Question 42
[MEDIUM-HARD]

Which Secret type is automatically created for ServiceAccounts?

---

### Question 43
[HARD]

How do you configure encryption at rest for Secrets in Kubernetes?

---

### Question 44
[HARD]

What is the difference between Opaque and kubernetes.io/tls Secret types?

---

### Question 45
[HARD]

How are Secret updates handled when mounted as volumes?

---

### Question 46
[HARD]

What is the immutable field used for in Secrets?

---

### Question 47
[HARD]

What encryption providers are supported for encrypting Secrets at rest?

---

### Question 48
[HARD]

How can you reference a specific key from a Secret in an environment variable?

---

### Question 49
[HARD]

What RBAC permissions are needed to read Secrets in a namespace?

---

## Network Policies

### Question 50
[MEDIUM]

What is the default network behavior for Pods without any NetworkPolicy?

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
