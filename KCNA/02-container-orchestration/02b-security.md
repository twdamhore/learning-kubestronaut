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

What namespace contains the default ServiceAccount for system components?

A) default
B) kube-system
C) kube-public
D) system

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-system namespace contains ServiceAccounts for core Kubernetes system components like kube-controller-manager, kube-scheduler, and kube-proxy. Each component typically has its own ServiceAccount with appropriate RBAC permissions.

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

---

### Question 22
[HARD]

What are the security benefits of using short-lived ServiceAccount tokens?

A) Faster authentication
B) Reduced blast radius if compromised; tokens expire quickly
C) Better performance
D) Simpler configuration

---

## Pod Security

### Question 23
[MEDIUM]

What is a privileged container?

A) A container running as root
B) A container with almost all host capabilities and no isolation restrictions
C) A container with network privileges
D) A container that can access secrets

---

### Question 24
[MEDIUM]

Which Pod Security Standards level allows most workloads to run?

A) restricted
B) baseline
C) privileged
D) permissive

---

### Question 25
[MEDIUM]

What does the runAsUser field specify?

A) The username to run as
B) The numeric UID to run the container process as
C) The user who created the Pod
D) The ServiceAccount user

---

### Question 26
[MEDIUM-HARD]

What is the fsGroup field used for in securityContext?

A) To set the filesystem type
B) To set the group ID that owns Pod volumes
C) To configure file permissions
D) To specify filesystem quotas

---

### Question 27
[MEDIUM-HARD]

How do you drop all Linux capabilities from a container?

A) Set privileged: false
B) Use capabilities.drop: ["ALL"] in securityContext
C) Set runAsNonRoot: true
D) Capabilities cannot be dropped

---

### Question 28
[MEDIUM-HARD]

What is the difference between pod-level and container-level securityContext?

A) No difference; they are the same
B) Pod-level applies to all containers; container-level overrides for specific containers
C) Pod-level is deprecated
D) Container-level is more secure

---

### Question 29
[HARD]

What is the "baseline" Pod Security Standard designed to prevent?

A) All security vulnerabilities
B) Known privilege escalations while allowing common workloads
C) Network attacks only
D) Container escapes only

---

### Question 30
[HARD]

How do you configure Pod Security Admission cluster-wide?

A) Use namespace labels only
B) Configure the PodSecurity admission controller with a configuration file
C) Set cluster-wide annotations
D) Modify the API server binary

---

### Question 31
[HARD]

What is the supplementalGroups field used for?

A) To add groups to the primary group
B) To specify additional group IDs for the container process
C) To create new groups
D) To supplement user permissions

---

### Question 32
[HARD]

How does the MustRunAsNonRoot security context constraint work?

A) It sets the user to nobody
B) It validates that the container's image does not run as UID 0
C) It changes the user at runtime
D) It blocks all root processes

---

### Question 33
[HARD]

What is the seLinuxOptions field used for?

A) To enable SELinux
B) To set SELinux labels (user, role, type, level) for containers
C) To configure SELinux policies
D) To disable SELinux

---

### Question 34
[HARD]

What happens when you set readOnlyRootFilesystem to true?

A) The image becomes read-only
B) The container's root filesystem is mounted read-only
C) Volumes become read-only
D) Configuration files cannot be changed

---

### Question 35
[HARD]

How do you allow a container to bind to privileged ports (< 1024)?

A) Set privileged: true
B) Add the NET_BIND_SERVICE capability
C) Run as root
D) Use hostNetwork: true

---

### Question 36
[HARD]

What is the windowsOptions field in securityContext?

A) Configuration for Windows containers
B) Window manager settings
C) Terminal options
D) Display settings

---

### Question 37
[HARD]

How do Pod Security Admission exemptions work?

A) By deleting policies
B) By configuring usernames, namespaces, or runtimeClasses that bypass checks
C) By adding annotations
D) Exemptions are not supported

---

## Secrets Management

### Question 38
[MEDIUM]

What is the maximum size limit for a Kubernetes Secret?

A) 1KB
B) 1MB
C) 10MB
D) No limit

---

### Question 39
[MEDIUM]

How do you create a Secret from literal values using kubectl?

A) kubectl create secret literal
B) kubectl create secret generic --from-literal=key=value
C) kubectl apply secret
D) kubectl generate secret

---

### Question 40
[MEDIUM-HARD]

What is the stringData field in a Secret manifest?

A) A field for storing string data without base64 encoding
B) A deprecated field
C) A field for storing encrypted strings
D) A field for multi-line strings only

---

### Question 41
[MEDIUM-HARD]

How do Secrets differ from ConfigMaps in terms of security?

A) Secrets are encrypted by default
B) Secrets are stored in tmpfs when mounted, have stricter RBAC defaults, and can be encrypted at rest
C) There is no security difference
D) ConfigMaps are more secure

---

### Question 42
[MEDIUM-HARD]

What is the kubernetes.io/basic-auth Secret type used for?

A) For OAuth tokens
B) For storing username and password credentials
C) For API keys
D) For SSH keys

---

### Question 43
[HARD]

How does the kube-apiserver encrypt Secrets at rest?

A) Using TLS
B) By configuring an EncryptionConfiguration that specifies encryption providers
C) Secrets are always encrypted automatically
D) Using the kubelet

---

### Question 44
[HARD]

What is envelope encryption for Secrets?

A) Encrypting the Secret manifest
B) Encrypting data with a DEK, then encrypting the DEK with a KEK from a KMS
C) Double encryption with the same key
D) Encrypting during transmission

---

### Question 45
[HARD]

How are Secret volume mounts updated when the Secret changes?

A) Immediately
B) Eventually by kubelet sync; depends on sync frequency and cache TTL
C) Never; Pods must be restarted
D) Only if the Pod has watch permissions

---

### Question 46
[HARD]

What is the relationship between Secrets and etcd?

A) Secrets are stored in a separate database
B) Secrets are stored in etcd, optionally encrypted at rest
C) etcd cannot store Secrets
D) Secrets are only stored in memory

---

### Question 47
[HARD]

How can you use external secret management systems with Kubernetes?

A) Direct integration only
B) Using tools like External Secrets Operator, Secrets Store CSI Driver, or custom controllers
C) External systems cannot be used
D) By mounting network volumes

---

### Question 48
[HARD]

What is the secretRef field used for in Pod specs?

A) To reference a specific key in a Secret
B) To load all key-value pairs from a Secret as environment variables
C) To mount a Secret as a volume
D) To create a new Secret

---

### Question 49
[HARD]

How do you restrict which Pods can access a specific Secret?

A) Using NetworkPolicies
B) Using RBAC to control ServiceAccount access to Secrets
C) Secrets are accessible by all Pods
D) Using Secret labels

---

## Network Policies

### Question 50
[MEDIUM]

What must be installed for NetworkPolicies to have any effect?

A) A firewall
B) A CNI plugin that supports NetworkPolicy
C) A special kernel module
D) The NetworkPolicy controller

---

### Question 51
[MEDIUM]

Which policyTypes can be specified in a NetworkPolicy?

A) Allow and Deny
B) Ingress and Egress
C) Input and Output
D) Inbound and Outbound

---

### Question 52
[MEDIUM-HARD]

How do you allow traffic only from Pods with a specific label?

A) Use a nodeSelector
B) Use podSelector in the ingress from field
C) Use a service selector
D) Labels cannot be used in NetworkPolicies

---

### Question 53
[MEDIUM-HARD]

What is the effect of an empty ingress array in a NetworkPolicy?

A) All ingress traffic is allowed
B) All ingress traffic is denied
C) The policy has no effect
D) Only egress is controlled

---

### Question 54
[HARD]

How do you create a default deny-all egress policy?

A) Set egress: deny in namespace
B) Create a NetworkPolicy selecting all Pods with policyTypes: ["Egress"] and no egress rules
C) Configure the CNI plugin
D) Use an annotation

---

### Question 55
[HARD]

What is the ipBlock selector used for in NetworkPolicies?

A) To select Pods by IP
B) To allow or deny traffic to/from specific IP CIDR ranges
C) To block IP addresses
D) To configure IP allocation

---

### Question 56
[HARD]

How do NetworkPolicies interact with Services?

A) NetworkPolicies block Service traffic
B) NetworkPolicies apply to Pod IPs, not Service IPs; traffic is filtered after DNAT
C) Services bypass NetworkPolicies
D) NetworkPolicies must reference Services directly

---

### Question 57
[HARD]

What is the except field used for in ipBlock selectors?

A) To exclude specific CIDRs from the allowed/denied range
B) To add exceptions to the policy
C) To except certain ports
D) To handle error cases

---

### Question 58
[HARD]

How do you allow egress to external IPs while blocking inter-pod traffic?

A) Cannot be done with NetworkPolicies
B) Use ipBlock to allow external CIDRs while not including Pod CIDRs
C) Use a firewall instead
D) Allow all egress and use another policy

---

### Question 59
[HARD]

What are the limitations of Kubernetes NetworkPolicies?

A) No limitations
B) No deny rules, no cluster-wide policies, no logging, CNI-dependent enforcement
C) Only work with TCP
D) Cannot cross namespaces

---

## Authentication

### Question 60
[MEDIUM]

What is a bearer token in Kubernetes authentication?

A) A username/password combination
B) A token sent in the Authorization header to authenticate requests
C) A certificate
D) A cookie

---

### Question 61
[MEDIUM]

How do ServiceAccounts authenticate to the API server?

A) Using username and password
B) Using JWT tokens mounted in Pods
C) Using SSH keys
D) Using IP whitelisting

---

### Question 62
[MEDIUM-HARD]

What is the purpose of the --client-ca-file flag on the API server?

A) To set the server certificate
B) To specify the CA bundle for validating client certificates
C) To configure TLS
D) To enable mTLS

---

### Question 63
[MEDIUM-HARD]

How do you configure multiple authentication methods for the API server?

A) Only one method can be configured
B) Pass multiple authentication flags; the API server tries each in order
C) Use a configuration file only
D) Run multiple API servers

---

### Question 64
[HARD]

What is the authenticating proxy method?

A) Using a proxy server for load balancing
B) A front proxy that authenticates users and passes identity via headers
C) A reverse proxy for the API server
D) A method to proxy authentication to LDAP

---

### Question 65
[HARD]

How does the API server validate X.509 client certificates?

A) By checking the certificate expiration only
B) By verifying the certificate chain against the configured CA and extracting identity from CN/O
C) By contacting a CA server
D) By comparing to stored certificates

---

### Question 66
[HARD]

What is the purpose of the --oidc-issuer-url flag?

A) To set the API server URL
B) To specify the OIDC provider URL for token validation
C) To issue OIDC tokens
D) To configure OAuth

---

### Question 67
[HARD]

How do static token files work for authentication?

A) Tokens are generated dynamically
B) A CSV file maps tokens to users; the API server reads it at startup
C) Tokens are stored in etcd
D) Each user creates their own token file

---

### Question 68
[HARD]

What groups are automatically assigned to authenticated users?

A) No automatic groups
B) system:authenticated is added to all authenticated users
C) admin group
D) users group

---

### Question 69
[HARD]

What is the difference between user impersonation and sudo?

A) No difference
B) Impersonation allows acting as another user via API; sudo elevates privileges locally
C) Sudo is for containers; impersonation is for users
D) Impersonation is more secure

---

## Authorization

### Question 70
[MEDIUM]

What does it mean when authorization mode is set to AlwaysAllow?

A) Only admin requests are allowed
B) All authenticated requests are authorized without checking permissions
C) Allows all traffic
D) Allows anonymous access

---

### Question 71
[MEDIUM]

Which component makes authorization decisions in Kubernetes?

A) kubelet
B) kube-apiserver
C) kube-controller-manager
D) etcd

---

### Question 72
[MEDIUM-HARD]

What information is used to make authorization decisions?

A) Only the username
B) User, group, verb, resource, namespace, and API group
C) Only the resource
D) The request body

---

### Question 73
[MEDIUM-HARD]

How does the --authorization-mode flag work with multiple modes?

A) Only the first mode is used
B) Modes are evaluated in order; first to allow or deny wins
C) All modes must agree
D) Modes are randomly selected

---

### Question 74
[HARD]

What is the SubjectAccessReview API used for?

A) To review user accounts
B) To programmatically check if a subject can perform an action
C) To audit access logs
D) To create new subjects

---

### Question 75
[HARD]

How do you configure webhook authorization?

A) Enable it by default
B) Use --authorization-mode=Webhook and --authorization-webhook-config-file
C) Deploy a webhook controller
D) Configure in RBAC

---

### Question 76
[HARD]

What is the SelfSubjectAccessReview API?

A) For reviewing your own account
B) For checking if the current user can perform a specific action
C) For self-service account management
D) For auditing your own actions

---

### Question 77
[HARD]

How does Node authorization restrict kubelet permissions?

A) By limiting network access
B) By only allowing kubelets to access resources related to Pods scheduled on their node
C) By requiring node certificates
D) By rate limiting requests

---

### Question 78
[HARD]

What are the special groups in Kubernetes authorization?

A) admin, user, guest
B) system:authenticated, system:unauthenticated, system:masters, system:serviceaccounts
C) root, sudo, operator
D) There are no special groups

---

### Question 79
[HARD]

How can you audit authorization decisions?

A) Check kubectl output
B) Enable audit logging with appropriate audit policy rules
C) Query the authorization API
D) Check etcd directly

---

## Admission Controllers

### Question 80
[MEDIUM]

When are admission controllers invoked in the API request lifecycle?

A) Before authentication
B) After authentication and authorization, before persistence
C) After object persistence
D) During authentication

---

### Question 81
[MEDIUM]

Which admission controller sets default values for resource requests?

A) ResourceDefaults
B) LimitRanger
C) DefaultResources
D) ResourceQuota

---

### Question 82
[MEDIUM]

What is a dynamic admission controller?

A) A controller that changes behavior at runtime
B) An admission webhook that is registered dynamically via API resources
C) A controller that adapts to load
D) A built-in controller that can be configured

---

### Question 83
[MEDIUM-HARD]

How do you enable or disable built-in admission controllers?

A) Using a configuration file only
B) Using --enable-admission-plugins and --disable-admission-plugins flags
C) By deploying or removing controllers
D) Through RBAC settings

---

### Question 84
[MEDIUM-HARD]

What is the purpose of the ResourceQuota admission controller?

A) To set default resource limits
B) To enforce resource quotas on namespaces and reject requests that exceed them
C) To monitor resource usage
D) To allocate resources to pods

---

### Question 85
[HARD]

What is a MutatingWebhookConfiguration?

A) A webhook that changes its own configuration
B) A resource that configures webhooks that can modify objects during admission
C) A configuration for mutating API servers
D) A webhook for configuration changes

---

### Question 86
[HARD]

How do you specify which resources an admission webhook should process?

A) Using a label selector only
B) Using the rules field with apiGroups, apiVersions, resources, and operations
C) The webhook processes all resources by default
D) Using RBAC rules

---

### Question 87
[HARD]

What is the failurePolicy field in webhook configurations?

A) How to handle webhook errors
B) Defines behavior (Fail or Ignore) when the webhook cannot be reached
C) Policy for failed admissions
D) Retry policy

---

### Question 88
[HARD]

Which admission controller enforces that images come from allowed registries?

A) ImageRegistry
B) ImagePolicyWebhook or custom ValidatingAdmissionWebhook
C) RegistryEnforcer
D) There is no such controller

---

### Question 89
[HARD]

How do reinvocation policies work for mutating webhooks?

A) They control retry behavior
B) If set to IfNeeded, webhooks are re-invoked if other webhooks modified the object
C) They control webhook ordering
D) They prevent duplicate invocations

---

## Container Security

### Question 90
[MEDIUM]

What is the difference between an image tag and an image digest?

A) No difference
B) Tags are mutable labels; digests are immutable SHA256 hashes
C) Digests are shorter
D) Tags are more secure

---

### Question 91
[MEDIUM]

Why is it recommended to run containers as non-root?

A) For better performance
B) To limit damage if the container is compromised; principle of least privilege
C) Containers cannot run as root
D) For easier debugging

---

### Question 92
[MEDIUM-HARD]

What is a distroless container image?

A) An image without a Linux distribution
B) An image containing only the application and runtime dependencies, no shell or package manager
C) A compressed image
D) An image without configuration

---

### Question 93
[HARD]

How do you configure seccomp profiles for containers?

A) Using annotations only
B) Using securityContext.seccompProfile with type and optionally localhostProfile
C) Through the container runtime only
D) Seccomp cannot be configured in Kubernetes

---

### Question 94
[HARD]

What are Linux namespaces in container isolation?

A) Kubernetes namespaces
B) Kernel features that isolate process views of system resources (PID, network, mount, etc.)
C) DNS namespaces
D) File naming conventions

---

### Question 95
[HARD]

How does user namespace remapping improve container security?

A) By creating new users
B) By mapping container root (UID 0) to an unprivileged user on the host
C) By encrypting user data
D) By isolating user files

---

### Question 96
[HARD]

What is the Unconfined seccomp profile?

A) A highly restrictive profile
B) A profile that applies no seccomp filtering
C) The default secure profile
D) A profile for untrusted workloads

---

### Question 97
[HARD]

How do cgroups contribute to container security?

A) By encrypting container data
B) By limiting and isolating resource usage (CPU, memory, I/O) to prevent DoS
C) By controlling network access
D) By managing container images

---

### Question 98
[HARD]

What is container image signing and verification?

A) Encrypting images
B) Cryptographically signing images and verifying signatures before deployment
C) Compressing images
D) Watermarking images

---

### Question 99
[HARD]

How do you prevent privilege escalation attacks in containers?

A) Run as root
B) Set allowPrivilegeEscalation: false, drop capabilities, use seccomp, run as non-root
C) Use host networking
D) Disable security contexts

---

### Question 100
[HARD]

What are the security implications of using hostPath volumes?

A) No implications
B) Containers can access and modify host filesystem, potentially escaping isolation
C) Only performance implications
D) hostPath is automatically sandboxed

---
