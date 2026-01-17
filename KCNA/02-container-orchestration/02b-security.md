# Security - 100 MCQ Questions (Part B)

**Domain:** Container Orchestration (28%)
**Competency:** Security
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## RBAC Fundamentals

### Question 1
[MEDIUM]

Which Kubernetes resource grants permissions cluster-wide rather than within a single namespace?

---

### Question 2
[MEDIUM]

What is the purpose of a ClusterRoleBinding?

---

### Question 3
[MEDIUM-HARD]

Which RBAC verb is required to watch for changes to resources?

---

### Question 4
[MEDIUM-HARD]

How do you grant read-only access to Pods in a namespace using RBAC?

---

### Question 5
[MEDIUM-HARD]

What is the difference between "get" and "list" verbs in RBAC?

---

### Question 6
[HARD]

What is the "impersonate" verb used for in RBAC?

---

### Question 7
[HARD]

How can you reference non-resource URLs in RBAC rules?

---

### Question 8
[HARD]

What are aggregated ClusterRoles and how do they work?

---

### Question 9
[HARD]

Which default ClusterRole provides read access to most resources?

---

### Question 10
[HARD]

How do you grant access to subresources like pods/log using RBAC?

---

### Question 11
[HARD]

What is the purpose of the resourceNames field in RBAC rules?

---

### Question 12
[HARD]

How does RBAC handle wildcard permissions?

---

## ServiceAccounts

### Question 13
[MEDIUM]

What namespace contains the default ServiceAccount for system components?

---

### Question 14
[MEDIUM]

How do you assign a specific ServiceAccount to a Pod?

---

### Question 15
[MEDIUM-HARD]

What is a projected volume in the context of ServiceAccount tokens?

---

### Question 16
[MEDIUM-HARD]

Why were bound ServiceAccount tokens introduced?

---

### Question 17
[HARD]

What is the expirationSeconds field for ServiceAccount tokens?

---

### Question 18
[HARD]

How do you create a non-expiring ServiceAccount token?

---

### Question 19
[HARD]

What happens when the ServiceAccount associated with a running Pod is deleted?

---

### Question 20
[HARD]

What is the purpose of the serviceAccountName vs serviceAccount field?

---

### Question 21
[HARD]

How does the BoundServiceAccountTokenVolume feature work?

---

### Question 22
[HARD]

What are the security benefits of using short-lived ServiceAccount tokens?

---

## Pod Security

### Question 23
[MEDIUM]

What is a privileged container?

---

### Question 24
[MEDIUM]

Which Pod Security Standards level allows most workloads to run?

---

### Question 25
[MEDIUM]

What does the runAsUser field specify?

---

### Question 26
[MEDIUM-HARD]

What is the fsGroup field used for in securityContext?

---

### Question 27
[MEDIUM-HARD]

How do you drop all Linux capabilities from a container?

---

### Question 28
[MEDIUM-HARD]

What is the difference between pod-level and container-level securityContext?

---

### Question 29
[HARD]

What is the "baseline" Pod Security Standard designed to prevent?

---

### Question 30
[HARD]

How do you configure Pod Security Admission cluster-wide?

---

### Question 31
[HARD]

What is the supplementalGroups field used for?

---

### Question 32
[HARD]

How does the MustRunAsNonRoot security context constraint work?

---

### Question 33
[HARD]

What is the seLinuxOptions field used for?

---

### Question 34
[HARD]

What happens when you set readOnlyRootFilesystem to true?

---

### Question 35
[HARD]

How do you allow a container to bind to privileged ports (< 1024)?

---

### Question 36
[HARD]

What is the windowsOptions field in securityContext?

---

### Question 37
[HARD]

How do Pod Security Admission exemptions work?

---

## Secrets Management

### Question 38
[MEDIUM]

What is the maximum size limit for a Kubernetes Secret?

---

### Question 39
[MEDIUM]

How do you create a Secret from literal values using kubectl?

---

### Question 40
[MEDIUM-HARD]

What is the stringData field in a Secret manifest?

---

### Question 41
[MEDIUM-HARD]

How do Secrets differ from ConfigMaps in terms of security?

---

### Question 42
[MEDIUM-HARD]

What is the kubernetes.io/basic-auth Secret type used for?

---

### Question 43
[HARD]

How does the kube-apiserver encrypt Secrets at rest?

---

### Question 44
[HARD]

What is envelope encryption for Secrets?

---

### Question 45
[HARD]

How are Secret volume mounts updated when the Secret changes?

---

### Question 46
[HARD]

What is the relationship between Secrets and etcd?

---

### Question 47
[HARD]

How can you use external secret management systems with Kubernetes?

---

### Question 48
[HARD]

What is the secretRef field used for in Pod specs?

---

### Question 49
[HARD]

How do you restrict which Pods can access a specific Secret?

---

## Network Policies

### Question 50
[MEDIUM]

What must be installed for NetworkPolicies to have any effect?

---

### Question 51
[MEDIUM]

Which policyTypes can be specified in a NetworkPolicy?

---

### Question 52
[MEDIUM-HARD]

How do you allow traffic only from Pods with a specific label?

---

### Question 53
[MEDIUM-HARD]

What is the effect of an empty ingress array in a NetworkPolicy?

---

### Question 54
[HARD]

How do you create a default deny-all egress policy?

---

### Question 55
[HARD]

What is the ipBlock selector used for in NetworkPolicies?

---

### Question 56
[HARD]

How do NetworkPolicies interact with Services?

---

### Question 57
[HARD]

What is the except field used for in ipBlock selectors?

---

### Question 58
[HARD]

How do you allow egress to external IPs while blocking inter-pod traffic?

---

### Question 59
[HARD]

What are the limitations of Kubernetes NetworkPolicies?

---

## Authentication

### Question 60
[MEDIUM]

What is a bearer token in Kubernetes authentication?

---

### Question 61
[MEDIUM]

How do ServiceAccounts authenticate to the API server?

---

### Question 62
[MEDIUM-HARD]

What is the purpose of the --client-ca-file flag on the API server?

---

### Question 63
[MEDIUM-HARD]

How do you configure multiple authentication methods for the API server?

---

### Question 64
[HARD]

What is the authenticating proxy method?

---

### Question 65
[HARD]

How does the API server validate X.509 client certificates?

---

### Question 66
[HARD]

What is the purpose of the --oidc-issuer-url flag?

---

### Question 67
[HARD]

How do static token files work for authentication?

---

### Question 68
[HARD]

What groups are automatically assigned to authenticated users?

---

### Question 69
[HARD]

What is the difference between user impersonation and sudo?

---

## Authorization

### Question 70
[MEDIUM]

What does it mean when authorization mode is set to AlwaysAllow?

---

### Question 71
[MEDIUM]

Which component makes authorization decisions in Kubernetes?

---

### Question 72
[MEDIUM-HARD]

What information is used to make authorization decisions?

---

### Question 73
[MEDIUM-HARD]

How does the --authorization-mode flag work with multiple modes?

---

### Question 74
[HARD]

What is the SubjectAccessReview API used for?

---

### Question 75
[HARD]

How do you configure webhook authorization?

---

### Question 76
[HARD]

What is the SelfSubjectAccessReview API?

---

### Question 77
[HARD]

How does Node authorization restrict kubelet permissions?

---

### Question 78
[HARD]

What are the special groups in Kubernetes authorization?

---

### Question 79
[HARD]

How can you audit authorization decisions?

---

## Admission Controllers

### Question 80
[MEDIUM]

When are admission controllers invoked in the API request lifecycle?

---

### Question 81
[MEDIUM]

Which admission controller sets default values for resource requests?

---

### Question 82
[MEDIUM]

What is a dynamic admission controller?

---

### Question 83
[MEDIUM-HARD]

How do you enable or disable built-in admission controllers?

---

### Question 84
[MEDIUM-HARD]

What is the purpose of the ResourceQuota admission controller?

---

### Question 85
[HARD]

What is a MutatingWebhookConfiguration?

---

### Question 86
[HARD]

How do you specify which resources an admission webhook should process?

---

### Question 87
[HARD]

What is the failurePolicy field in webhook configurations?

---

### Question 88
[HARD]

Which admission controller enforces that images come from allowed registries?

---

### Question 89
[HARD]

How do reinvocation policies work for mutating webhooks?

---

## Container Security

### Question 90
[MEDIUM]

What is the difference between an image tag and an image digest?

---

### Question 91
[MEDIUM]

Why is it recommended to run containers as non-root?

---

### Question 92
[MEDIUM-HARD]

What is a distroless container image?

---

### Question 93
[HARD]

How do you configure seccomp profiles for containers?

---

### Question 94
[HARD]

What are Linux namespaces in container isolation?

---

### Question 95
[HARD]

How does user namespace remapping improve container security?

---

### Question 96
[HARD]

What is the Unconfined seccomp profile?

---

### Question 97
[HARD]

How do cgroups contribute to container security?

---

### Question 98
[HARD]

What is container image signing and verification?

---

### Question 99
[HARD]

How do you prevent privilege escalation attacks in containers?

---

### Question 100
[HARD]

What are the security implications of using hostPath volumes?

---
