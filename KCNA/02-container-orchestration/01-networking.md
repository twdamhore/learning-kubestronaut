# Networking - 200 MCQ Questions

**Domain:** Container Orchestration (28%)
**Competency:** Networking
**Difficulty Distribution:** 20% Medium | 20% Medium-Hard | 60% Hard

---

## CNI Fundamentals

### Question 1
[MEDIUM]

What does CNI stand for in Kubernetes networking?

A) Container Network Infrastructure
B) Container Network Interface
C) Cluster Network Integration
D) Cloud Native Interface

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 2
[MEDIUM]

Which of the following is the primary responsibility of a CNI plugin?

A) Managing container images
B) Providing network connectivity to Pods
C) Scheduling Pods to nodes
D) Managing persistent storage

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 3
[MEDIUM]

Which CNI plugin is commonly used in cloud environments and supports network policies natively?

A) Flannel
B) Calico
C) Bridge
D) Host-local

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 4
[MEDIUM]

What happens when a Pod is created in terms of CNI?

A) The API server directly configures the network
B) The kubelet calls the CNI plugin to set up networking
C) The scheduler assigns the IP address
D) etcd stores the network configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 5
[MEDIUM]

Where are CNI plugin configuration files typically stored on a Kubernetes node?

A) /etc/kubernetes/cni/
B) /etc/cni/net.d/
C) /var/lib/cni/config/
D) /opt/cni/conf/

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 6
[MEDIUM-HARD]

Which CNI plugin uses VXLAN overlay networking by default?

A) Calico with IPIP mode
B) Flannel with vxlan backend
C) Weave with fastdp
D) Cilium with native routing

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 7
[MEDIUM-HARD]

What is the purpose of the IPAM section in a CNI configuration?

A) To define network policies
B) To manage IP address allocation for Pods
C) To configure DNS settings
D) To set up load balancing

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 8
[MEDIUM-HARD]

Which CNI plugin leverages eBPF for high-performance networking?

A) Flannel
B) Calico
C) Cilium
D) Weave

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 9
[MEDIUM-HARD]

What is the main advantage of using a CNI plugin with BGP support?

A) Simplified configuration
B) Native routing without overlay encapsulation
C) Better support for Windows containers
D) Automatic SSL/TLS encryption

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 10
[MEDIUM-HARD]

In a multi-node cluster, what ensures that Pod IP addresses don't conflict?

A) The kube-scheduler
B) IPAM (IP Address Management) with cluster-wide coordination
C) The API server's validation webhook
D) etcd's unique key constraints

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 11
[HARD]

When configuring Calico with IPIP mode, what encapsulation method is used?

A) VXLAN with UDP port 4789
B) IP-in-IP with protocol number 4
C) GRE tunneling with protocol 47
D) Geneve with UDP port 6081

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 12
[HARD]

Which CNI plugin configuration option specifies the network subnet for Pod IP allocation?

A) podCIDR
B) subnet
C) ipRange
D) networkRange

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 13
[HARD]

What is the difference between CNI ADD and CNI DEL operations?

A) ADD creates the Pod, DEL deletes it
B) ADD sets up network for a container, DEL tears it down
C) ADD allocates CPU, DEL deallocates it
D) ADD starts the container, DEL stops it

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 14
[HARD]

In a chained CNI configuration, what is the purpose of multiple plugins?

A) Load balancing between plugins
B) Each plugin handles different aspects of networking
C) Failover in case one plugin crashes
D) Parallel execution for better performance

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 15
[HARD]

Which file format is used for CNI plugin configurations?

A) YAML
B) JSON
C) TOML
D) XML

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

## Kubernetes Services - ClusterIP

### Question 16
[MEDIUM]

What is the default Service type in Kubernetes?

A) NodePort
B) LoadBalancer
C) ClusterIP
D) ExternalName

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 17
[MEDIUM]

What is the primary purpose of a ClusterIP Service?

A) Expose the application to the internet
B) Provide internal cluster communication
C) Load balance traffic across nodes
D) Map to an external DNS name

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 18
[MEDIUM]

How does a ClusterIP Service identify which Pods to route traffic to?

A) By Pod name
B) By node name
C) By label selector
D) By IP address

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 19
[MEDIUM]

Which port field in a Service specification refers to the port the Service listens on?

A) targetPort
B) nodePort
C) port
D) containerPort

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 20
[MEDIUM]

What is the valid IP range for ClusterIP Services?

A) The Pod CIDR range
B) The Service CIDR range defined in cluster configuration
C) Any private IP range
D) The node's subnet range

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 21
[MEDIUM-HARD]

If a Service's `targetPort` is not specified, what happens?

A) The Service fails to create
B) It defaults to the same value as `port`
C) It defaults to port 80
D) It uses the first exposed container port

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 22
[MEDIUM-HARD]

What happens to existing connections when a Pod backing a Service is terminated?

A) They are immediately dropped
B) They are gracefully drained during the termination grace period
C) They are migrated to another Pod
D) They remain connected until client timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 23
[MEDIUM-HARD]

How can you verify which endpoints are associated with a Service?

A) kubectl get pods
B) kubectl describe service <name>
C) kubectl get endpoints <name>
D) kubectl logs service/<name>

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 24
[MEDIUM-HARD]

What is the purpose of `sessionAffinity` in a Service?

A) To ensure TLS encryption
B) To route requests from the same client to the same Pod
C) To prioritize certain Pods over others
D) To enable HTTP/2 multiplexing

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 25
[MEDIUM-HARD]

Which sessionAffinity option uses client IP for sticky sessions?

A) Cookie
B) ClientIP
C) Header
D) Session

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 26
[HARD]

What is the default session affinity timeout when `sessionAffinity: ClientIP` is set?

A) 1 hour
B) 3 hours (10800 seconds)
C) 24 hours
D) No timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 27
[HARD]

In a Service definition, what does `publishNotReadyAddresses: true` do?

A) Publishes the Service to external DNS
B) Includes Pod IPs in endpoints even if readiness probes fail
C) Makes the Service available before the cluster is ready
D) Allows traffic to unscheduled Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 28
[HARD]

What happens if a Service selector matches Pods in multiple namespaces?

A) The Service includes all matching Pods
B) An error occurs during Service creation
C) Services can only select Pods in the same namespace
D) The Service uses round-robin across namespaces

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 29
[HARD]

How does kube-proxy implement ClusterIP Services in iptables mode?

A) By creating virtual interfaces
B) By programming iptables NAT rules
C) By modifying the routing table
D) By intercepting packets in userspace

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 30
[HARD]

What is the purpose of the `ipFamilyPolicy` field in a Service specification?

A) To enable IPv4 only
B) To configure dual-stack (IPv4/IPv6) behavior
C) To set the IP family for node communication
D) To restrict IP ranges for clients

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

## Kubernetes Services - NodePort

### Question 31
[MEDIUM]

What is the default port range for NodePort Services?

A) 80-443
B) 1024-65535
C) 30000-32767
D) 8000-9000

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 32
[MEDIUM]

On which IP addresses is a NodePort Service accessible?

A) Only the ClusterIP
B) Only the node's external IP
C) All node IPs on the specified port
D) Only the master node IP

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 33
[MEDIUM]

What is automatically created when you create a NodePort Service?

A) An Ingress resource
B) A ClusterIP for internal access
C) A LoadBalancer
D) An external DNS record

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 34
[MEDIUM]

How can you specify a particular NodePort number?

A) It's always automatically assigned
B) Using the `nodePort` field in the Service spec
C) Using an annotation
D) Through a ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 35
[MEDIUM-HARD]

What happens if you specify a NodePort that is already in use?

A) The new Service takes over the port
B) Both Services share the port
C) The Service creation fails
D) A random port is assigned instead

<details>
<summary>Show Answer</summary>

**Answer:** C

</details>

---

### Question 36
[MEDIUM-HARD]

How does traffic flow when accessing a NodePort Service from external?

A) External -> NodePort -> ClusterIP -> Pod
B) External -> Pod directly
C) External -> LoadBalancer -> NodePort -> Pod
D) External -> Ingress -> NodePort -> Pod

<details>
<summary>Show Answer</summary>

**Answer:** A

</details>

---

### Question 37
[MEDIUM-HARD]

What is the `externalTrafficPolicy` field used for in NodePort Services?

A) To set rate limiting
B) To control whether traffic is routed only to local Pods or cluster-wide
C) To enable SSL termination
D) To configure firewall rules

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 38
[MEDIUM-HARD]

What is the effect of setting `externalTrafficPolicy: Local`?

A) All traffic goes to the local node only
B) Traffic is only routed to Pods on the receiving node, preserving client IP
C) Traffic is encrypted locally
D) The Service becomes unavailable externally

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 39
[HARD]

When `externalTrafficPolicy: Local` is set, what happens if no Pods exist on a node?

A) Traffic is forwarded to another node
B) The node's health check fails and no traffic is sent to it
C) The request hangs until a Pod is scheduled
D) A 503 error is immediately returned

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 40
[HARD]

What is the benefit of using `externalTrafficPolicy: Cluster` (default)?

A) Better client IP preservation
B) More even load distribution across all Pods
C) Lower latency
D) Reduced network hops

<details>
<summary>Show Answer</summary>

**Answer:** B

</details>

---

### Question 41
[HARD]

How can you change the default NodePort range in a Kubernetes cluster?

A) Modify the Service specification
B) Update kube-apiserver's --service-node-port-range flag
C) Edit the kube-proxy ConfigMap
D) Change the CNI configuration

---

### Question 42
[HARD]

What iptables chain does kube-proxy use for NodePort DNAT rules?

A) INPUT
B) KUBE-SERVICES
C) KUBE-NODEPORTS
D) PREROUTING

---

### Question 43
[HARD]

In a cloud environment, why might NodePort Services be less preferred than LoadBalancer?

A) NodePort is slower
B) NodePort exposes all nodes and requires external load balancing
C) NodePort doesn't support TCP
D) NodePort Services cost more

---

## Kubernetes Services - LoadBalancer

### Question 44
[MEDIUM]

What cloud resource is typically provisioned when creating a LoadBalancer Service?

A) Virtual machine
B) Cloud load balancer (e.g., AWS ELB, GCP Load Balancer)
C) DNS record
D) Storage volume

---

### Question 45
[MEDIUM]

What happens when you create a LoadBalancer Service in a bare-metal cluster without a cloud provider?

A) A software load balancer is automatically created
B) The Service remains in Pending state
C) It falls back to NodePort automatically
D) An error is thrown

---

### Question 46
[MEDIUM]

Which components are created when a LoadBalancer Service is provisioned?

A) LoadBalancer only
B) ClusterIP and NodePort only
C) ClusterIP, NodePort, and external LoadBalancer
D) External LoadBalancer only

---

### Question 47
[MEDIUM-HARD]

How does MetalLB enable LoadBalancer Services in bare-metal clusters?

A) By deploying cloud provider APIs
B) By announcing Service IPs via ARP/BGP protocols
C) By creating virtual machines
D) By proxying through the master node

---

### Question 48
[MEDIUM-HARD]

What annotation is commonly used to specify an internal load balancer in cloud environments?

A) service.kubernetes.io/load-balancer-internal
B) cloud.google.com/load-balancer-type: "Internal" or similar cloud-specific annotation
C) kubernetes.io/internal-lb: "true"
D) loadbalancer.kubernetes.io/internal

---

### Question 49
[MEDIUM-HARD]

What is the purpose of the `loadBalancerIP` field in a Service specification?

A) To get the assigned load balancer IP
B) To request a specific IP address for the load balancer
C) To configure the backend IP
D) To set the ClusterIP

---

### Question 50
[HARD]

What is the purpose of `loadBalancerSourceRanges` in a LoadBalancer Service?

A) To specify the IP ranges of backend Pods
B) To restrict which client IPs can access the load balancer
C) To define the load balancer's IP pool
D) To configure source NAT ranges

---

### Question 51
[HARD]

How does the cloud-controller-manager interact with LoadBalancer Services?

A) It doesn't; kube-proxy handles everything
B) It watches for LoadBalancer Services and provisions cloud resources
C) It only handles node registration
D) It manages Pod scheduling

---

### Question 52
[HARD]

What is the `allocateLoadBalancerNodePorts` field used for?

A) To allocate more ports for the load balancer
B) To control whether NodePorts are allocated for LoadBalancer Services
C) To specify the number of load balancer instances
D) To configure port mapping

---

### Question 53
[HARD]

When using AWS NLB (Network Load Balancer), what annotation preserves the client IP?

A) service.beta.kubernetes.io/aws-load-balancer-type: "nlb"
B) service.beta.kubernetes.io/aws-load-balancer-proxy-protocol: "*"
C) service.beta.kubernetes.io/aws-load-balancer-target-group-attributes with preserve_client_ip
D) No annotation needed; NLB preserves client IP by default in instance mode

---

### Question 54
[HARD]

What is the difference between a Layer 4 and Layer 7 load balancer in Kubernetes context?

A) Layer 4 is faster, Layer 7 is more secure
B) Layer 4 operates at TCP/UDP level, Layer 7 operates at HTTP level
C) Layer 4 is internal, Layer 7 is external
D) Layer 4 is cloud-only, Layer 7 is on-premises

---

## Kubernetes Services - ExternalName and Headless

### Question 55
[MEDIUM]

What is an ExternalName Service used for?

A) To expose internal services externally
B) To create a CNAME alias to an external DNS name
C) To assign external IPs to Pods
D) To configure external authentication

---

### Question 56
[MEDIUM]

What makes a Service "headless"?

A) Setting type: Headless
B) Setting clusterIP: None
C) Removing all selectors
D) Setting replicas: 0

---

### Question 57
[MEDIUM]

What is returned when you do a DNS lookup for a headless Service?

A) The ClusterIP
B) The IP addresses of all backing Pods
C) Nothing; DNS is disabled
D) The node IPs

---

### Question 58
[MEDIUM-HARD]

What is a common use case for headless Services?

A) Load balancing HTTP traffic
B) StatefulSet Pod discovery and direct Pod access
C) External service exposure
D) SSL termination

---

### Question 59
[MEDIUM-HARD]

For an ExternalName Service, what type of DNS record is created?

A) A record
B) AAAA record
C) CNAME record
D) SRV record

---

### Question 60
[MEDIUM-HARD]

Can an ExternalName Service have a selector?

A) Yes, it's required
B) Yes, but it's optional
C) No, ExternalName Services cannot have selectors
D) Only if targeting internal services

---

### Question 61
[HARD]

What happens when a headless Service has a selector defined?

A) Endpoints are automatically populated with Pod IPs
B) The Service becomes a ClusterIP Service
C) An error occurs
D) Only the first Pod is selected

---

### Question 62
[HARD]

How can you manually define endpoints for a headless Service without a selector?

A) Create an Endpoints resource with the same name
B) Add IPs to the Service annotations
C) Use a ConfigMap
D) Define them in a separate YAML file

---

### Question 63
[HARD]

What is the DNS format for individual Pods with a headless Service?

A) pod-ip.service.namespace.svc.cluster.local
B) pod-name.service.namespace.svc.cluster.local
C) pod-ip-dashed.namespace.pod.cluster.local
D) hostname.subdomain.namespace.svc.cluster.local

---

### Question 64
[HARD]

What field in a StatefulSet specification links it to a headless Service?

A) serviceName
B) headlessService
C) serviceRef
D) linkedService

---

### Question 65
[HARD]

Can an ExternalName Service point to another Kubernetes Service?

A) Yes, by using the full DNS name
B) No, it can only point to external names
C) Only within the same namespace
D) Only with specific annotations

---

## Ingress and Ingress Controllers

### Question 66
[MEDIUM]

What is the primary purpose of an Ingress resource?

A) To create internal Services
B) To manage external HTTP/HTTPS access to Services
C) To configure network policies
D) To manage Pod networking

---

### Question 67
[MEDIUM]

What must be installed in a cluster for Ingress resources to work?

A) kube-proxy
B) An Ingress controller
C) CoreDNS
D) A CNI plugin

---

### Question 68
[MEDIUM]

Which of the following is a popular Ingress controller?

A) kube-proxy
B) nginx-ingress-controller
C) flannel
D) coredns

---

### Question 69
[MEDIUM]

What type of routing does Ingress support?

A) TCP routing only
B) UDP routing only
C) HTTP/HTTPS routing based on host and path
D) ICMP routing

---

### Question 70
[MEDIUM]

How do you specify the backend Service for an Ingress rule?

A) Using labels
B) Using the service name and port
C) Using the Pod IP
D) Using annotations only

---

### Question 71
[MEDIUM-HARD]

What is the purpose of the `ingressClassName` field?

A) To name the Ingress resource
B) To specify which Ingress controller should handle this Ingress
C) To define the class of traffic
D) To set priority

---

### Question 72
[MEDIUM-HARD]

How do you configure TLS termination in an Ingress?

A) Using the tls section with a Secret reference
B) Using annotations only
C) TLS is always automatic
D) Using a ConfigMap

---

### Question 73
[MEDIUM-HARD]

What type of Secret is used for Ingress TLS configuration?

A) Opaque
B) kubernetes.io/tls
C) kubernetes.io/ssh-auth
D) kubernetes.io/dockerconfigjson

---

### Question 74
[MEDIUM-HARD]

What is path-based routing in Ingress?

A) Routing based on the URL path to different Services
B) Routing based on file system paths
C) Routing based on node paths
D) Routing based on network paths

---

### Question 75
[MEDIUM-HARD]

What is the difference between `pathType: Prefix` and `pathType: Exact`?

A) Prefix is faster than Exact
B) Prefix matches the path and all subpaths, Exact matches only the specific path
C) Prefix is for HTTP, Exact is for HTTPS
D) There is no difference

---

### Question 76
[HARD]

What happens when multiple Ingress rules match the same host and path?

A) All rules are applied
B) The first rule created wins
C) The most specific rule wins
D) An error occurs

---

### Question 77
[HARD]

How can you implement rate limiting in nginx-ingress-controller?

A) Using the rateLimiting field in Ingress spec
B) Using annotations like nginx.ingress.kubernetes.io/limit-rps
C) Rate limiting is not supported
D) Using a separate ConfigMap

---

### Question 78
[HARD]

What is the purpose of a default backend in an Ingress?

A) To specify the primary service
B) To handle requests that don't match any rules
C) To provide health checks
D) To store default configurations

---

### Question 79
[HARD]

How does the nginx Ingress controller discover Ingress resources?

A) By polling the API server
B) By watching Ingress resources via the Kubernetes API
C) By reading from etcd directly
D) By receiving push notifications from kubelet

---

### Question 80
[HARD]

What is the purpose of the `nginx.ingress.kubernetes.io/rewrite-target` annotation?

A) To rewrite the response body
B) To rewrite the URL path before forwarding to the backend
C) To rewrite the Host header
D) To rewrite the client IP

---

### Question 81
[HARD]

How can you configure sticky sessions in nginx-ingress?

A) Using sessionAffinity in the Service
B) Using nginx.ingress.kubernetes.io/affinity annotation
C) Sticky sessions are not supported
D) Using a Cookie header in the request

---

### Question 82
[HARD]

What is the IngressClass resource used for?

A) To define the Ingress API version
B) To define parameters and controller references for Ingress controllers
C) To classify traffic types
D) To group Ingress resources

---

### Question 83
[HARD]

How can you set an IngressClass as the default for the cluster?

A) Using the default: true field
B) Using the ingressclass.kubernetes.io/is-default-class annotation
C) Setting it in kube-controller-manager
D) It's automatic for the first IngressClass created

---

### Question 84
[HARD]

What is the difference between Ingress and Gateway API?

A) Ingress is newer than Gateway API
B) Gateway API provides more expressive routing and role-oriented design
C) Ingress supports more protocols
D) There is no difference

---

### Question 85
[HARD]

How can you configure client certificate authentication (mTLS) in nginx-ingress?

A) Using TLS secrets only
B) Using annotations like nginx.ingress.kubernetes.io/auth-tls-secret
C) mTLS is not supported
D) Using a sidecar container

---

## Network Policies

### Question 86
[MEDIUM]

What is a Network Policy used for?

A) To define routing rules
B) To control traffic flow to and from Pods
C) To configure DNS
D) To manage Service endpoints

---

### Question 87
[MEDIUM]

Which component enforces Network Policies?

A) kube-proxy
B) The CNI plugin (if it supports Network Policies)
C) kube-controller-manager
D) The API server

---

### Question 88
[MEDIUM]

What is the default network policy behavior when no policies are applied to a Pod?

A) All traffic is denied
B) All traffic is allowed
C) Only ingress is allowed
D) Only egress is allowed

---

### Question 89
[MEDIUM]

What happens when you create a Network Policy that selects a Pod?

A) All traffic to that Pod is allowed
B) Only traffic matching the policy rules is allowed (default deny for selected direction)
C) The Pod is isolated from all traffic
D) Nothing changes

---

### Question 90
[MEDIUM]

Which CNI plugins support Network Policies?

A) Flannel (without extensions)
B) Calico, Cilium, Weave
C) Bridge CNI only
D) All CNI plugins

---

### Question 91
[MEDIUM-HARD]

What does `podSelector: {}` in a Network Policy mean?

A) Select no Pods
B) Select all Pods in the namespace
C) Select Pods with empty labels
D) Invalid syntax

---

### Question 92
[MEDIUM-HARD]

How do you specify allowed source Pods in an ingress rule?

A) Using sourceSelector
B) Using from with podSelector
C) Using allowedPods
D) Using ingressPods

---

### Question 93
[MEDIUM-HARD]

Can Network Policies restrict traffic based on ports?

A) No, only IP-based filtering
B) Yes, using the ports field
C) Only for egress
D) Only for TCP

---

### Question 94
[MEDIUM-HARD]

What is the scope of a Network Policy?

A) Cluster-wide
B) Namespace-scoped
C) Node-scoped
D) Pod-scoped

---

### Question 95
[MEDIUM-HARD]

How do you allow traffic from all Pods in a specific namespace?

A) Using namespaceSelector with matching labels
B) Using allowNamespace field
C) Using fromNamespace field
D) Network Policies can't filter by namespace

---

### Question 96
[HARD]

What is the effect of an empty ingress rule (ingress: []) in a Network Policy?

A) Allow all ingress traffic
B) Deny all ingress traffic
C) No effect on ingress
D) Invalid syntax

---

### Question 97
[HARD]

How do you create a Network Policy that allows traffic only from a specific CIDR block?

A) Using cidrSelector
B) Using ipBlock with cidr field
C) Using ipRange
D) Using sourceIP

---

### Question 98
[HARD]

What is the purpose of the `except` field in an ipBlock?

A) To add exceptions to the policy
B) To exclude specific IPs from the allowed CIDR range
C) To handle exception errors
D) To specify fallback IPs

---

### Question 99
[HARD]

How can you deny all egress traffic from Pods except DNS?

A) It's not possible
B) Create a policy with egress rules allowing only port 53
C) Use a default deny policy with no exceptions
D) Configure kube-proxy

---

### Question 100
[HARD]

What happens when multiple Network Policies select the same Pod?

A) Only the first policy applies
B) Only the last policy applies
C) The union of all policies applies (additive)
D) An error occurs

---

### Question 101
[HARD]

How do you allow traffic from Pods matching BOTH a podSelector AND namespaceSelector?

A) Put them in the same from entry
B) Create two separate from entries
C) Use the AND operator
D) Use a composite selector

---

### Question 102
[HARD]

What is the difference between putting selectors in the same `from` entry vs separate entries?

A) No difference
B) Same entry = AND logic, separate entries = OR logic
C) Same entry = OR logic, separate entries = AND logic
D) Separate entries are not allowed

---

### Question 103
[HARD]

Can Network Policies block traffic between Pods on the same node?

A) No, local traffic is always allowed
B) Yes, if the CNI plugin supports it
C) Only with specific annotations
D) Only in host network mode

---

### Question 104
[HARD]

How do you specify that a Network Policy applies to both ingress and egress?

A) Create two separate policies
B) Set policyTypes to include both Ingress and Egress
C) It's automatic
D) Use the bidirectional field

---

### Question 105
[HARD]

What is the behavior if policyTypes is not specified but ingress rules are defined?

A) Only Ingress type is assumed
B) Both Ingress and Egress are assumed
C) The policy is invalid
D) Default deny for all

---

## DNS in Kubernetes

### Question 106
[MEDIUM]

What is the default DNS server in most Kubernetes clusters?

A) BIND
B) dnsmasq
C) CoreDNS
D) Unbound

---

### Question 107
[MEDIUM]

What is the fully qualified domain name (FQDN) format for a Service?

A) service.namespace.cluster.local
B) service.namespace.svc.cluster.local
C) namespace.service.svc.cluster.local
D) service.svc.namespace.cluster.local

---

### Question 108
[MEDIUM]

What DNS record type is created for a regular ClusterIP Service?

A) CNAME
B) A record (or AAAA for IPv6)
C) SRV
D) TXT

---

### Question 109
[MEDIUM]

Where is the cluster DNS server IP configured in Pods?

A) /etc/hosts
B) /etc/resolv.conf
C) Environment variables
D) /etc/dns.conf

---

### Question 110
[MEDIUM]

What is the default domain suffix for Services in Kubernetes?

A) kubernetes.local
B) cluster.local
C) svc.local
D) k8s.local

---

### Question 111
[MEDIUM-HARD]

What happens when you query a Service name without the full domain from within the same namespace?

A) The query fails
B) The search domains append the namespace and cluster domain
C) It returns all Service IPs
D) It returns the node IP

---

### Question 112
[MEDIUM-HARD]

What is the DNS format for discovering named ports on a Service?

A) port.protocol.service.namespace.svc.cluster.local
B) _port._protocol.service.namespace.svc.cluster.local (SRV record)
C) service.port.namespace.svc.cluster.local
D) Named ports don't have DNS records

---

### Question 113
[MEDIUM-HARD]

What Pod DNS policy uses the node's DNS settings?

A) ClusterFirst
B) Default
C) None
D) NodeLocal

---

### Question 114
[MEDIUM-HARD]

What is the purpose of the `dnsConfig` field in a Pod spec?

A) To completely override DNS settings
B) To customize DNS settings alongside the policy
C) To disable DNS
D) To set the DNS server IP

---

### Question 115
[MEDIUM-HARD]

How does CoreDNS know about Services in the cluster?

A) By reading /etc/hosts
B) By watching the Kubernetes API for Service and Endpoint changes
C) By querying external DNS
D) From ConfigMap updates only

---

### Question 116
[HARD]

What is the purpose of the `ndots` option in resolv.conf?

A) To set the number of DNS servers
B) To determine when to use absolute vs relative DNS queries
C) To configure DNS caching
D) To set query timeout

---

### Question 117
[HARD]

How can you optimize DNS resolution for Pods making many external DNS queries?

A) Increase ndots value
B) Decrease ndots value or use FQDNs
C) Disable DNS caching
D) Use IP addresses only

---

### Question 118
[HARD]

What is NodeLocal DNSCache?

A) A DNS caching layer running on each node for improved performance
B) A replacement for CoreDNS
C) A caching plugin for kube-proxy
D) A node-level DNS configuration

---

### Question 119
[HARD]

How can you configure CoreDNS to forward specific domains to external DNS servers?

A) Using the forward plugin in CoreDNS ConfigMap
B) By editing /etc/resolv.conf on nodes
C) Through the API server
D) Using Network Policies

---

### Question 120
[HARD]

What happens to DNS resolution if CoreDNS Pods are not running?

A) DNS continues working from cache
B) Pods cannot resolve Service names
C) External DNS is used instead
D) The cluster automatically restarts CoreDNS

---

### Question 121
[HARD]

What is the purpose of the `autopath` plugin in CoreDNS?

A) To automatically configure paths
B) To optimize search path resolution for Pod queries
C) To set up routing paths
D) To configure file paths

---

### Question 122
[HARD]

How does DNS work for StatefulSet Pods?

A) Same as regular Pods
B) Each Pod gets a predictable DNS entry: pod-name.service-name.namespace.svc.cluster.local
C) StatefulSet Pods don't have DNS
D) Only the first Pod gets a DNS entry

---

### Question 123
[HARD]

What is the `pods` directive in CoreDNS Kubernetes plugin used for?

A) To count Pod resources
B) To enable or configure A record generation for Pods
C) To restart Pods
D) To scale Pods

---

### Question 124
[HARD]

How can you verify DNS resolution from within a Pod?

A) kubectl dns
B) Using nslookup or dig from within the Pod
C) kubectl describe dns
D) Checking the API server logs

---

### Question 125
[HARD]

What is the impact of setting `dnsPolicy: None` without `dnsConfig`?

A) Uses cluster DNS
B) Uses node DNS
C) The Pod will have no DNS configuration and may not resolve names
D) An error prevents Pod creation

---

## kube-proxy and Service Discovery

### Question 126
[MEDIUM]

What is the primary function of kube-proxy?

A) To proxy API requests
B) To implement Service networking rules on each node
C) To manage container networking
D) To schedule Pods

---

### Question 127
[MEDIUM]

Which kube-proxy mode is the default in most modern Kubernetes clusters?

A) userspace
B) iptables
C) ipvs
D) nftables

---

### Question 128
[MEDIUM]

What happens when a Service ClusterIP is accessed?

A) The request goes directly to a Pod
B) kube-proxy forwards it to a backend Pod
C) Network rules redirect traffic to an endpoint Pod
D) The API server routes the request

---

### Question 129
[MEDIUM]

How does kube-proxy learn about Services and Endpoints?

A) By reading iptables rules
B) By watching the Kubernetes API
C) By polling the CNI plugin
D) By reading local configuration files

---

### Question 130
[MEDIUM]

What is the userspace mode of kube-proxy?

A) The most efficient mode
B) A legacy mode where kube-proxy acts as an actual proxy in userspace
C) A mode for user applications
D) The default mode

---

### Question 131
[MEDIUM-HARD]

What is the main advantage of IPVS mode over iptables mode?

A) Simpler configuration
B) Better performance at scale with O(1) complexity for lookups
C) More secure
D) Better Windows support

---

### Question 132
[MEDIUM-HARD]

What load balancing algorithms does IPVS mode support?

A) Only round-robin
B) Round-robin, least connections, destination hashing, source hashing, and more
C) Only least connections
D) Random only

---

### Question 133
[MEDIUM-HARD]

Where is kube-proxy configuration typically stored?

A) In a Secret
B) In a ConfigMap in kube-system namespace
C) In /etc/kube-proxy/
D) In etcd directly

---

### Question 134
[MEDIUM-HARD]

How does kube-proxy handle Service IP changes?

A) It doesn't; Services have static IPs
B) It updates the network rules to reflect the new IP
C) It restarts affected Pods
D) It requires manual intervention

---

### Question 135
[MEDIUM-HARD]

What is the purpose of EndpointSlices?

A) To replace Services
B) To provide more scalable and efficient endpoint tracking
C) To slice network traffic
D) To manage storage endpoints

---

### Question 136
[HARD]

In iptables mode, which iptables chain handles DNAT for Services?

A) INPUT
B) FORWARD
C) KUBE-SVC-* chains
D) OUTPUT

---

### Question 137
[HARD]

What is the `--proxy-mode` flag used for?

A) To enable proxy authentication
B) To select the kube-proxy mode (iptables, ipvs, etc.)
C) To configure proxy protocols
D) To set proxy timeout

---

### Question 138
[HARD]

How does kube-proxy implement session affinity in iptables mode?

A) Using cookies
B) Using the recent match module to track client IPs
C) Session affinity is not supported in iptables mode
D) Using connection tracking

---

### Question 139
[HARD]

What happens to existing connections when kube-proxy updates iptables rules?

A) They are immediately terminated
B) Existing connections continue; new connections use updated rules
C) All traffic stops briefly
D) Connections are migrated

---

### Question 140
[HARD]

What is the `conntrack` table used for in Kubernetes networking?

A) To track connection attempts
B) To track established connections for stateful packet inspection
C) To store DNS records
D) To track Pod connections

---

### Question 141
[HARD]

How can you verify what rules kube-proxy has created?

A) kubectl get iptables
B) Running iptables-save or ipvsadm on the node
C) kubectl describe kube-proxy
D) Checking the API server

---

### Question 142
[HARD]

What is the `--cluster-cidr` flag in kube-proxy used for?

A) To define the Service CIDR
B) To configure rules related to Pod CIDR for certain features
C) To set the node CIDR
D) To define external CIDRs

---

### Question 143
[HARD]

What is the purpose of `healthzBindAddress` in kube-proxy config?

A) To configure health check endpoints for kube-proxy itself
B) To check Pod health
C) To configure Service health checks
D) To bind to specific node addresses

---

### Question 144
[HARD]

How does IPVS mode handle Service VIPs?

A) Using iptables NAT
B) By binding VIPs to a dummy interface and using IPVS rules
C) By modifying routing tables
D) Using userspace proxying

---

### Question 145
[HARD]

What is the nftables mode in kube-proxy?

A) A deprecated mode
B) A newer mode using nftables instead of iptables for better performance
C) A mode for network filtering
D) A mode specific to Windows

---

## Advanced Networking Concepts

### Question 146
[MEDIUM]

What is the purpose of Pod CIDR?

A) To define Service IP ranges
B) To define the IP range for Pod addresses
C) To configure external IPs
D) To set node IP ranges

---

### Question 147
[MEDIUM]

Can Pods communicate with other Pods in the cluster by default?

A) No, Network Policies are required
B) Yes, Kubernetes has a flat network model
C) Only within the same namespace
D) Only within the same node

---

### Question 148
[MEDIUM]

What is the Kubernetes network model requirement for Pod-to-Pod communication?

A) All Pods must use NAT
B) All Pods can reach all other Pods without NAT
C) Pods must use Services
D) Pods must be in the same namespace

---

### Question 149
[MEDIUM-HARD]

What is a network overlay in Kubernetes?

A) A graphical network interface
B) An encapsulation technique that creates a virtual network over the physical network
C) A security layer
D) A DNS configuration

---

### Question 150
[MEDIUM-HARD]

What is the difference between VXLAN and IPIP encapsulation?

A) VXLAN is faster
B) VXLAN encapsulates at Layer 2 (UDP), IPIP encapsulates at Layer 3
C) IPIP is more secure
D) There is no difference

---

### Question 151
[MEDIUM-HARD]

What is the purpose of the host network mode (`hostNetwork: true`)?

A) To isolate the Pod network
B) To share the node's network namespace with the Pod
C) To enable faster networking
D) To use the host's DNS

---

### Question 152
[HARD]

What are the security implications of using hostNetwork: true?

A) None; it's the recommended approach
B) The Pod can see all network traffic on the node and bind to node ports
C) It disables network policies
D) It prevents Pod communication

---

### Question 153
[HARD]

What is the purpose of `hostPort` in a container spec?

A) To expose the container on a specific port on the host
B) To configure the host's firewall
C) To set the container port
D) To enable host networking

---

### Question 154
[HARD]

How does traffic flow when accessing a ClusterIP Service from a Pod on the same node as a backend Pod?

A) Always through the network
B) The CNI may short-circuit traffic locally
C) Through the API server
D) Through kube-proxy's userspace mode

---

### Question 155
[HARD]

What is the purpose of `externalIPs` in a Service specification?

A) To configure external DNS
B) To make the Service available on specific node IPs
C) To configure load balancer IPs
D) To set up external authentication

---

### Question 156
[HARD]

What happens when you set `externalIPs` on a Service?

A) A load balancer is created
B) Traffic to those IPs (on the Service port) is routed to the Service
C) The Service becomes accessible from the internet
D) DNS records are updated

---

### Question 157
[HARD]

What is the Service topology feature (now deprecated) replaced by?

A) Endpoint slices
B) Topology-aware hints
C) Network policies
D) Service mesh

---

### Question 158
[HARD]

What are topology-aware hints used for?

A) To optimize routing based on network topology
B) To configure DNS
C) To set up load balancing hints
D) To define node topology

---

### Question 159
[HARD]

What is the `internalTrafficPolicy` field used for?

A) To control how internal traffic is routed (Local vs Cluster)
B) To define internal security policies
C) To configure internal load balancing
D) To set internal DNS

---

### Question 160
[HARD]

What happens when `internalTrafficPolicy: Local` is set?

A) External traffic is blocked
B) Internal traffic is only routed to Pods on the same node
C) All traffic becomes internal
D) Load balancing is disabled

---

## Service Mesh and Advanced Topics

### Question 161
[MEDIUM]

What is a service mesh?

A) A network of physical servers
B) An infrastructure layer for handling service-to-service communication
C) A type of CNI plugin
D) A load balancer

---

### Question 162
[MEDIUM]

Which of the following is a popular service mesh for Kubernetes?

A) Calico
B) Istio
C) Flannel
D) CoreDNS

---

### Question 163
[MEDIUM]

What is the sidecar pattern in service meshes?

A) A backup container
B) A proxy container injected alongside the application container
C) A logging container
D) A storage container

---

### Question 164
[MEDIUM]

What is mTLS in the context of service mesh?

A) Multi-tier Load Balancing Service
B) Mutual TLS for encrypting pod-to-pod communication
C) Managed TLS certificates
D) Micro TLS protocol

---

### Question 165
[MEDIUM]

What is the data plane in a service mesh?

A) The control components
B) The sidecar proxies that handle actual traffic
C) The storage layer
D) The monitoring system

---

### Question 166
[MEDIUM-HARD]

What is the control plane in a service mesh?

A) The proxy containers
B) The components that configure and manage the data plane
C) The networking hardware
D) The Kubernetes control plane

---

### Question 167
[MEDIUM-HARD]

What is traffic management in service mesh?

A) Monitoring network usage
B) Controlling request routing, retries, timeouts, and traffic splitting
C) Managing bandwidth
D) Filtering malicious traffic

---

### Question 168
[MEDIUM-HARD]

What is circuit breaking in service mesh?

A) A security feature
B) A pattern to prevent cascading failures by stopping requests to failing services
C) A network isolation technique
D) A debugging tool

---

### Question 169
[MEDIUM-HARD]

What is traffic mirroring (shadowing)?

A) Encrypting traffic
B) Duplicating traffic to a secondary service for testing
C) Reflecting attacks
D) Creating traffic backups

---

### Question 170
[MEDIUM-HARD]

What observability features do service meshes typically provide?

A) Only logging
B) Distributed tracing, metrics, and logging
C) Only metrics
D) Only tracing

---

### Question 171
[HARD]

How does Istio inject sidecar proxies?

A) Manually by users
B) Using mutating admission webhooks
C) Through the CNI plugin
D) By modifying container images

---

### Question 172
[HARD]

What is an Envoy proxy?

A) A Kubernetes component
B) A high-performance proxy used as the data plane in many service meshes
C) A type of load balancer
D) A DNS server

---

### Question 173
[HARD]

What is the VirtualService resource in Istio?

A) A virtual machine service
B) A configuration for request routing rules
C) A type of Kubernetes Service
D) A storage abstraction

---

### Question 174
[HARD]

What is the DestinationRule resource in Istio?

A) A firewall rule
B) A configuration for policies applied to traffic after routing
C) A routing destination
D) A DNS rule

---

### Question 175
[HARD]

How does a service mesh handle canary deployments?

A) By modifying Deployments
B) By splitting traffic percentages between service versions
C) By using separate clusters
D) By DNS-based routing

---

### Question 176
[HARD]

What is the difference between iptables-based and eBPF-based service meshes?

A) No difference
B) eBPF operates in kernel space with better performance; iptables uses netfilter
C) iptables is more modern
D) eBPF is user-space only

---

### Question 177
[HARD]

What is Cilium Service Mesh's approach compared to traditional sidecars?

A) Uses more sidecars
B) Uses eBPF to reduce or eliminate sidecar overhead
C) Uses hardware acceleration
D) Uses userspace networking

---

### Question 178
[HARD]

What is the purpose of PeerAuthentication in Istio?

A) To authenticate users
B) To configure mTLS requirements between workloads
C) To authenticate API requests
D) To configure RBAC

---

### Question 179
[HARD]

How do service meshes handle retries and timeouts differently than application code?

A) They don't; it's the same
B) They handle it at the proxy layer, removing the need for application-level implementation
C) They use kernel-level handling
D) They require application changes

---

### Question 180
[HARD]

What is the Gateway API and how does it relate to service mesh?

A) A replacement for Kubernetes API
B) A standard API for advanced traffic management that service meshes can implement
C) A specific service mesh implementation
D) A deprecated API

---

## Troubleshooting and Diagnostics

### Question 181
[MEDIUM]

What command can you use to test connectivity to a Service from within a Pod?

A) kubectl connect
B) curl or wget to the Service name/IP
C) kubectl test-connection
D) ping only

---

### Question 182
[MEDIUM]

How can you check if a Service has endpoints?

A) kubectl get endpoints <service-name>
B) kubectl describe pod
C) kubectl logs
D) kubectl get nodes

---

### Question 183
[MEDIUM]

What might cause a Service to have no endpoints?

A) The Service is too new
B) No Pods match the Service's selector or Pods aren't ready
C) The cluster is overloaded
D) DNS is not configured

---

### Question 184
[MEDIUM]

What tool can you use to debug DNS resolution in a Pod?

A) kubectl dns-debug
B) nslookup, dig, or host commands from within the Pod
C) kubectl describe dns
D) The Kubernetes dashboard

---

### Question 185
[MEDIUM]

How can you verify that kube-proxy is running and healthy?

A) kubectl get pods -n kube-system | grep kube-proxy
B) kubectl get services
C) kubectl describe nodes
D) kubectl logs apiserver

---

### Question 186
[MEDIUM-HARD]

What might cause DNS resolution to fail for Services?

A) Service doesn't exist
B) CoreDNS Pods are not running or misconfigured
C) Too many Services
D) Node is overloaded

---

### Question 187
[MEDIUM-HARD]

How can you test network policies are working correctly?

A) kubectl describe networkpolicy
B) Attempting connections from allowed and denied sources
C) kubectl get networkpolicy
D) Checking the API server logs

---

### Question 188
[MEDIUM-HARD]

What is the purpose of an ephemeral debug container?

A) To store temporary data
B) To attach a debugging container to a running Pod for troubleshooting
C) To run tests
D) To collect metrics

---

### Question 189
[MEDIUM-HARD]

How can you capture network traffic from a Pod?

A) kubectl capture
B) Using tcpdump in the Pod or a debug container
C) From the Kubernetes dashboard
D) Using kubectl logs

---

### Question 190
[MEDIUM-HARD]

What might cause intermittent connectivity issues between Pods?

A) DNS caching
B) Network policy changes, Pod rescheduling, or CNI issues
C) Too many namespaces
D) API server load

---

### Question 191
[HARD]

How can you diagnose iptables-related networking issues?

A) kubectl describe iptables
B) Running iptables -L -n -v on the node and checking KUBE-* chains
C) Checking CoreDNS logs
D) Using kubectl debug

---

### Question 192
[HARD]

What tool can help visualize network policies in a cluster?

A) kubectl visualize
B) Tools like Cilium's Hubble, NetworkPolicy Editor, or similar visualization tools
C) The Kubernetes dashboard
D) kube-proxy

---

### Question 193
[HARD]

How can you identify if packet loss is occurring between Pods?

A) kubectl get packet-loss
B) Using ping, iperf, or packet capture tools
C) Checking the API server
D) Reviewing kubelet logs

---

### Question 194
[HARD]

What might cause high latency for Service requests?

A) Too many labels
B) Network congestion, long proxy chains, or backend Pod issues
C) Too many namespaces
D) Large ConfigMaps

---

### Question 195
[HARD]

How can you trace the network path of a packet in Kubernetes?

A) kubectl trace
B) Using traceroute, packet captures, and examining iptables/IPVS rules
C) kubectl describe path
D) Using the Kubernetes API

---

### Question 196
[HARD]

What is the purpose of the `kubectl port-forward` command?

A) To permanently expose a Service
B) To create a temporary tunnel from local machine to a Pod/Service for debugging
C) To configure port mappings
D) To forward ports between Pods

---

### Question 197
[HARD]

How can you debug a network policy that seems to be blocking expected traffic?

A) Delete the policy
B) Check policy selectors, verify Pod labels, and test with explicit allow rules
C) Restart kube-proxy
D) Restart the CNI

---

### Question 198
[HARD]

What information does `kubectl describe service` provide for debugging?

A) Network traffic statistics
B) Service configuration, endpoints, and events
C) Pod logs
D) Node status

---

### Question 199
[HARD]

How can you verify that the CNI plugin is functioning correctly?

A) kubectl get cni
B) Check CNI Pod logs, verify Pod IP assignment, and test Pod connectivity
C) kubectl describe cni
D) Check the API server

---

### Question 200
[HARD]

What is the recommended approach for debugging complex networking issues in production?

A) Restart all components
B) Systematic isolation: check DNS, endpoints, network policies, CNI, and kube-proxy sequentially
C) Delete and recreate all Services
D) Scale down to one node

---
