# Networking - 100 MCQ Questions (Part B)

**Domain:** Container Orchestration (28%)
**Competency:** Networking
**Difficulty Distribution:** 25% Medium | 28% Medium-Hard | 47% Hard

---

## CNI Fundamentals

### Question 1
[MEDIUM]

Which of the following is the primary responsibility of a CNI plugin?

A) Managing container images
B) Providing network connectivity to Pods
C) Scheduling Pods to nodes
D) Managing persistent storage

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The primary responsibility of a CNI plugin is to provide network connectivity to Pods by allocating IP addresses and setting up network interfaces, routes, and any necessary network namespaces.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

</details>

---

### Question 2
[MEDIUM]

What happens when a Pod is created in terms of CNI?

A) The API server directly configures the network
B) The kubelet calls the CNI plugin to set up networking
C) The scheduler assigns the IP address
D) etcd stores the network configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Pod is created, the kubelet on that node invokes the CNI plugin to set up the Pod's network namespace, assign an IP address, and configure routing so the Pod can communicate with other Pods and services.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

</details>

---

### Question 3
[MEDIUM-HARD]

What is the purpose of overlay networking in Kubernetes?

A) To improve network security
B) To enable Pod communication across nodes without requiring physical network changes
C) To reduce network latency
D) To provide DNS services

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Overlay networking encapsulates Pod traffic within the underlying physical network, allowing Pods on different nodes to communicate using their Pod IP addresses without requiring the physical network infrastructure to understand Pod addressing.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 4
[MEDIUM-HARD]

Which CNI plugin is built around eBPF as its primary dataplane from the ground up?

A) Flannel
B) Weave
C) Cilium
D) Bridge

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Cilium was designed from the ground up to use eBPF as its primary dataplane for networking, security, and observability. While other CNI plugins like Calico also support eBPF as an optional dataplane, Cilium's architecture is fundamentally built around eBPF.

**Source:** [Introduction to Cilium | Cilium Documentation](https://docs.cilium.io/en/stable/overview/intro/)

</details>

---

### Question 5
[MEDIUM-HARD]

In a multi-node cluster, what ensures that Pod IP addresses don't conflict?

A) The kube-scheduler assigns IPs during scheduling
B) Per-node PodCIDR allocation plus CNI IPAM within each node's range
C) The API server's validation webhook
D) etcd's unique key constraints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When node CIDR allocation is enabled, the kube-controller-manager allocates a unique PodCIDR range to each node from the cluster's Pod network CIDR. The CNI plugin's IPAM then assigns IPs from that node-local range. This two-tier approach prevents conflicts without requiring cluster-wide IP coordination for every Pod. Some CNI plugins manage IP allocation independently.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 6
[HARD]

When node CIDR allocation is enabled, how does Kubernetes allocate Pod IP ranges to nodes?

A) Each node requests IPs from a central DHCP server
B) The kube-controller-manager assigns a PodCIDR range to each node
C) The API server randomly assigns IPs to Pods
D) Pods share IP addresses using NAT

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When node CIDR allocation is enabled (--allocate-node-cidrs), the kube-controller-manager's node controller allocates a unique PodCIDR range to each node from --cluster-cidr. The CNI plugin then assigns individual Pod IPs from this node-specific range. Some CNI plugins handle IP allocation independently without relying on node PodCIDRs.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 7
[HARD]

When does the kubelet invoke the CNI plugin?

A) When the API server creates a Pod object
B) When the container runtime creates the Pod sandbox
C) After the container starts running
D) When the scheduler assigns a node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet invokes the CNI plugin when the container runtime creates the Pod sandbox (network namespace). The CNI plugin configures the network interface, assigns an IP, and sets up routing before application containers start.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

</details>

---

## Kubernetes Services - ClusterIP

### Question 8
[MEDIUM]

What is the primary purpose of a ClusterIP Service?

A) Expose the application to the internet
B) Provide internal cluster communication
C) Load balance traffic across nodes
D) Map to an external DNS name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A ClusterIP Service provides a stable internal IP address for communication between Pods within the cluster, enabling service discovery and load balancing without exposing the service externally.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 9
[MEDIUM]

Which port field in a Service specification refers to the port the Service listens on?

A) targetPort
B) nodePort
C) port
D) containerPort

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The "port" field specifies the port on which the Service is exposed and receives traffic, while "targetPort" specifies the port on the backend Pods where traffic is forwarded.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 10
[MEDIUM-HARD]

If a Service's `targetPort` is not specified, what happens?

A) The Service fails to create
B) It defaults to the same value as `port`
C) It defaults to port 80
D) It uses the first exposed container port

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When targetPort is not specified, Kubernetes defaults it to the same value as the Service port, assuming the backend Pods listen on the same port number as the Service exposes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 11
[MEDIUM-HARD]

Which command directly lists the Endpoints resource for a Service?

A) kubectl get pods
B) kubectl get endpoints <name>
C) kubectl get services
D) kubectl logs service/<name>

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "kubectl get endpoints <name>" command directly queries the Endpoints resource, showing the IP addresses and ports of all Pods currently selected by the Service.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 12
[MEDIUM-HARD]

Which sessionAffinity option uses client IP for sticky sessions?

A) Cookie
B) ClientIP
C) Header
D) Session

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes supports "ClientIP" as the session affinity type, which uses the client's source IP address to consistently route requests to the same Pod. Cookie-based affinity is not natively supported at the Service level.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 13
[HARD]

In a Service definition, what does `publishNotReadyAddresses: true` do?

A) Publishes the Service to external DNS
B) Includes Pod IPs in endpoints even if readiness probes fail
C) Makes the Service available before the cluster is ready
D) Allows traffic to unscheduled Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting publishNotReadyAddresses to true causes the Service to include Pod IPs in DNS responses and endpoints even when Pods are not ready, which is useful for headless Services in StatefulSets where Pods need to discover each other during startup.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 14
[HARD]

How does kube-proxy implement ClusterIP Services in iptables mode?

A) By creating virtual interfaces
B) By programming iptables NAT rules
C) By modifying the routing table
D) By intercepting packets in userspace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In iptables mode, kube-proxy creates DNAT (Destination NAT) rules in the KUBE-SERVICES and KUBE-SVC-* chains that redirect traffic destined for ClusterIP addresses to the actual Pod endpoints.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

## Kubernetes Services - NodePort

### Question 15
[MEDIUM]

On which IP addresses is a NodePort Service accessible?

A) Only the ClusterIP
B) Only the node's external IP
C) All node IPs on the specified port
D) Only the master node IP

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A NodePort Service is accessible on the same port across all nodes in the cluster, regardless of which nodes are running the backend Pods. Traffic can enter through any node and be routed to the appropriate Pod.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 16
[MEDIUM]

How can you specify a particular NodePort number?

A) It's always automatically assigned
B) Using the `nodePort` field in the Service spec
C) Using an annotation
D) Through a ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** You can specify a specific NodePort number using the nodePort field within the ports section of the Service spec. If not specified, Kubernetes automatically assigns an available port from the NodePort range.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 17
[MEDIUM-HARD]

How does traffic flow when accessing a NodePort Service from external?

A) External -> NodePort -> Pod (via kube-proxy DNAT)
B) External -> Pod directly
C) External -> LoadBalancer -> NodePort -> Pod
D) External -> Ingress -> NodePort -> Pod

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** External traffic hits the NodePort on any cluster node. kube-proxy's rules then DNAT the traffic directly to one of the backend Pod endpoints. While a ClusterIP is allocated, traffic doesn't literally pass through it—kube-proxy routes directly to endpoints.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 18
[MEDIUM-HARD]

What is the effect of setting `externalTrafficPolicy: Local`?

A) All traffic goes to the local node only
B) Traffic is only routed to Pods on the receiving node, preserving client IP
C) Traffic is encrypted locally
D) The Service becomes unavailable externally

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With externalTrafficPolicy: Local, kube-proxy only routes traffic to Pods running on the same node that received the traffic. This preserves the original client IP (no SNAT) but may result in uneven load distribution.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 19
[HARD]

What is the benefit of using `externalTrafficPolicy: Cluster` (default)?

A) Better client IP preservation
B) More even load distribution across all Pods
C) Lower latency
D) Reduced network hops

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With externalTrafficPolicy: Cluster, traffic can be forwarded to any Pod in the cluster regardless of which node receives it, resulting in more even distribution but at the cost of an extra network hop and SNAT that obscures the client IP.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 20
[HARD]

What iptables chain does kube-proxy use for NodePort DNAT rules?

A) INPUT
B) KUBE-SERVICES
C) KUBE-NODEPORTS
D) PREROUTING

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** kube-proxy creates a KUBE-NODEPORTS chain that handles DNAT rules specifically for NodePort Services, which is jumped to from the KUBE-SERVICES chain for traffic that doesn't match ClusterIP addresses.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

## Kubernetes Services - LoadBalancer

### Question 21
[MEDIUM]

What cloud resource is typically provisioned when creating a LoadBalancer Service?

A) Virtual machine
B) Cloud load balancer (e.g., AWS ELB, GCP Load Balancer)
C) DNS record
D) Storage volume

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When creating a LoadBalancer Service, the cloud-controller-manager provisions a cloud-specific load balancer (like AWS ELB/NLB, GCP Load Balancer, or Azure Load Balancer) that routes external traffic to the cluster nodes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 22
[MEDIUM]

Which components are created by default when a LoadBalancer Service is provisioned?

A) LoadBalancer only
B) ClusterIP and NodePort only
C) ClusterIP, NodePort, and external LoadBalancer
D) External LoadBalancer only

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** By default, a LoadBalancer Service includes all three components: a ClusterIP for internal access, a NodePort for node-level exposure, and an external load balancer. Note: NodePort allocation can be disabled by setting `allocateLoadBalancerNodePorts: false`.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 23
[MEDIUM-HARD]

How do you configure a LoadBalancer Service to use an internal (private) load balancer?

A) Set type: InternalLoadBalancer
B) Use cloud-provider-specific annotations
C) Set internalTrafficPolicy: Local
D) Use a ClusterIP Service instead

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Internal load balancer configuration is done through cloud-provider-specific annotations on the Service. Each cloud provider defines its own annotation keys and values for this purpose; consult your cloud provider's documentation.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 24
[HARD]

What is the purpose of `loadBalancerSourceRanges` in a LoadBalancer Service?

A) To specify the IP ranges of backend Pods
B) To restrict which client IPs can access the load balancer
C) To define the load balancer's IP pool
D) To configure source NAT ranges

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The loadBalancerSourceRanges field specifies CIDR ranges that are allowed to access the load balancer, implementing IP-based access control at the load balancer level to restrict which clients can reach the Service.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 25
[HARD]

What is the `allocateLoadBalancerNodePorts` field used for?

A) To allocate more ports for the load balancer
B) To control whether NodePorts are allocated for LoadBalancer Services
C) To specify the number of load balancer instances
D) To configure port mapping

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting allocateLoadBalancerNodePorts to false prevents automatic NodePort allocation for LoadBalancer Services, useful when the load balancer can route traffic directly to Pods without needing NodePorts.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 26
[HARD]

What is the difference between a Layer 4 and Layer 7 load balancer in Kubernetes context?

A) Layer 4 is faster, Layer 7 is more secure
B) Layer 4 operates at TCP/UDP level, Layer 7 operates at HTTP level
C) Layer 4 is internal, Layer 7 is external
D) Layer 4 is cloud-only, Layer 7 is on-premises

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Layer 4 load balancers (like NLB) route based on IP and port information, while Layer 7 load balancing inspects HTTP headers, paths, and content for sophisticated routing. In Kubernetes, Ingress is the API for defining L7 routing rules, and Ingress controllers (like NGINX or HAProxy) implement the actual L7 load balancing.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Kubernetes Services - ExternalName and Headless

### Question 27
[MEDIUM]

What makes a Service "headless"?

A) Setting type: Headless
B) Setting clusterIP: None
C) Removing all selectors
D) Setting replicas: 0

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A headless Service is created by setting clusterIP: None, which tells Kubernetes not to allocate a virtual IP, and instead DNS queries return the individual Pod IPs directly.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 28
[MEDIUM-HARD]

What is a common use case for headless Services?

A) Load balancing HTTP traffic
B) StatefulSet Pod discovery and direct Pod access
C) External service exposure
D) SSL termination

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Headless Services are commonly used with StatefulSets to provide stable DNS names for each Pod, enabling peer discovery and direct Pod-to-Pod communication for distributed databases and clustered applications.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 29
[MEDIUM-HARD]

Can an ExternalName Service have a selector?

A) Yes, it's required
B) Yes, but it's optional
C) No, ExternalName Services cannot have selectors
D) Only if targeting internal services

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** ExternalName Services map to external DNS names rather than Pod endpoints, so they cannot have selectors since there are no Pods to select.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 30
[HARD]

How can you manually define endpoints for a headless Service without a selector?

A) Create an Endpoints or EndpointSlice resource with the same name
B) Add IPs to the Service annotations
C) Use a ConfigMap
D) Define them in a separate YAML file

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** For Services without selectors, you must manually create an Endpoints resource (or the preferred EndpointSlice) with the same name as the Service, specifying the IP addresses and ports that the Service should route traffic to.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 31
[HARD]

What field in a StatefulSet specification links it to a headless Service?

A) serviceName
B) headlessService
C) serviceRef
D) linkedService

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The serviceName field in a StatefulSet spec specifies the name of the headless Service that governs the network identity of the Pods, enabling stable DNS names like pod-0.service-name.namespace.svc.cluster.local.

**Source:** [StatefulSets | Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

</details>

---

## Ingress Controllers and Gateway API Comparison

### Question 32
[MEDIUM]

What must be installed in a cluster for Ingress resources to work?

A) kube-proxy
B) An Ingress controller
C) CoreDNS
D) A CNI plugin

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ingress resources are just configuration objects; an Ingress controller (like nginx-ingress or Traefik) must be deployed to watch these resources and implement the actual routing rules.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 33
[MEDIUM]

What type of routing does Ingress support?

A) TCP routing only
B) UDP routing only
C) HTTP/HTTPS routing based on host and path
D) ICMP routing

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** The standard Kubernetes Ingress API is designed for HTTP/HTTPS Layer 7 routing, supporting host headers and URL paths to direct traffic to different backend Services.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 34
[MEDIUM-HARD]

What is the purpose of the `ingressClassName` field?

A) To name the Ingress resource
B) To specify which Ingress controller should handle this Ingress
C) To define the class of traffic
D) To set priority

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ingressClassName field references an IngressClass resource that identifies which Ingress controller should process the Ingress, enabling multiple controllers to coexist in a cluster.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 35
[MEDIUM-HARD]

What type of Secret is used for Ingress TLS configuration?

A) Opaque
B) kubernetes.io/tls
C) kubernetes.io/ssh-auth
D) kubernetes.io/dockerconfigjson

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ingress TLS configuration requires a Secret of type kubernetes.io/tls, which must contain tls.crt (certificate) and tls.key (private key) fields.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 36
[MEDIUM-HARD]

What is the difference between `pathType: Prefix` and `pathType: Exact`?

A) Prefix is faster than Exact
B) Prefix matches the path and all subpaths, Exact matches only the specific path
C) Prefix is for HTTP, Exact is for HTTPS
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Prefix matching routes requests where the URL path starts with the specified prefix (e.g., /api matches /api/users), while Exact requires an exact path match with no trailing content.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 37
[HARD]

How is rate limiting typically configured for Ingress resources?

A) Using the rateLimiting field in Ingress spec
B) Through controller-specific annotations or configuration
C) Rate limiting is not possible with Ingress
D) Using Network Policies

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Rate limiting is not part of the Ingress API specification. Ingress controllers implement rate limiting through their own controller-specific annotations or configuration mechanisms. Consult your Ingress controller's documentation.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 38
[HARD]

How do Ingress controllers discover Ingress resources?

A) By polling the API server periodically
B) By watching Ingress resources via the Kubernetes API
C) By reading from etcd directly
D) By receiving push notifications from kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ingress controllers use the Kubernetes watch API to monitor Ingress resources in real-time, automatically updating their configuration when Ingress resources are created, modified, or deleted.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 39
[HARD]

How are URL path rewrites typically handled in Ingress?

A) Through a rewritePath field in the Ingress spec
B) Through controller-specific annotations or configuration
C) URL rewrites are not possible with Ingress
D) Through the pathType field

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** URL path rewriting is not part of the core Ingress API specification. Ingress controllers implement path rewriting through their own controller-specific annotations or configuration, allowing modification of the URL path before forwarding to the backend.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 40
[HARD]

What is the IngressClass resource used for?

A) To define the Ingress API version
B) To define parameters and controller references for Ingress controllers
C) To classify traffic types
D) To group Ingress resources

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** IngressClass resources define the controller that should implement Ingress resources and can include additional parameters, allowing different Ingress controllers to be specified for different Ingress resources.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 41
[HARD]

What is the difference between Ingress and Gateway API?

A) Ingress is newer than Gateway API
B) Gateway API provides more expressive routing and role-oriented design
C) Ingress supports more protocols
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Gateway API is a more expressive, extensible, and role-oriented successor to Ingress, supporting advanced routing, multiple protocols (HTTP, TCP, gRPC), and clearer separation between infrastructure and application concerns.

**Source:** [Gateway API | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/gateway/)

</details>

---

## Network Policies

### Question 42
[MEDIUM]

Which component enforces Network Policies?

A) kube-proxy
B) The CNI plugin (if it supports Network Policies)
C) kube-controller-manager
D) The API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policies are enforced by the CNI plugin (like Calico, Cilium, or Weave), which programs the underlying network rules. CNI plugins that don't support Network Policies (like basic Flannel) will ignore them.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 43
[MEDIUM]

What is the default network policy behavior when no policies are applied to a Pod?

A) All traffic is denied
B) All traffic is allowed
C) Only ingress is allowed
D) Only egress is allowed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, Kubernetes Pods are non-isolated and accept traffic from any source. Network Policies are additive, and isolation only occurs when at least one policy selects a Pod.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 44
[MEDIUM]

Which CNI plugins support Network Policies?

A) Flannel (without extensions)
B) CNI plugins with NetworkPolicy support like Calico or Cilium
C) Bridge CNI only
D) All CNI plugins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policy support requires CNI plugins that can implement the policy rules. Plugins like Calico and Cilium natively support Network Policies, while basic Flannel does not without additional components.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 45
[MEDIUM-HARD]

How do you specify allowed source Pods in an ingress rule?

A) Using sourceSelector
B) Using from with podSelector
C) Using allowedPods
D) Using ingressPods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In a Network Policy ingress rule, the "from" field contains a list of sources, and podSelector within a from entry specifies which Pods are allowed to send traffic to the selected Pods.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 46
[MEDIUM-HARD]

What is the scope of a Network Policy?

A) Cluster-wide
B) Namespace-scoped
C) Node-scoped
D) Pod-scoped

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policies are namespace-scoped resources that only select Pods within their own namespace. To apply policies across namespaces, you must create policies in each namespace or use cluster-scoped alternatives from CNI plugins.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 47
[HARD]

How do you create a Network Policy that allows traffic only from a specific CIDR block?

A) Using cidrSelector
B) Using ipBlock with cidr field
C) Using ipRange
D) Using sourceIP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ipBlock field in a from or to entry allows specifying CIDR ranges (e.g., 10.0.0.0/8) for allowing traffic from or to specific IP address blocks, useful for external traffic sources.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 48
[HARD]

How can you deny all egress traffic from Pods except DNS?

A) It's not possible
B) Create a policy with egress rules allowing only port 53
C) Use a default deny policy with no exceptions
D) Configure kube-proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To deny all egress except DNS, create a Network Policy with policyTypes: [Egress] and an egress rule allowing only UDP/TCP port 53 to the cluster DNS service or kube-dns namespace.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 49
[HARD]

How do you allow traffic from Pods matching BOTH a podSelector AND namespaceSelector?

A) Put them in the same from entry
B) Create two separate from entries
C) Use the AND operator
D) Use a composite selector

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** When podSelector and namespaceSelector are placed in the same `from` entry, they act as an AND condition, meaning traffic is only allowed from Pods that match both the Pod labels AND are in namespaces matching the namespace labels.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 50
[HARD]

Can Network Policies block traffic between Pods on the same node?

A) No, local traffic is always allowed
B) Yes, if the CNI plugin supports it
C) Only with specific annotations
D) Only in host network mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policies can block traffic between Pods on the same node if the CNI plugin enforces policies at the Pod network namespace level, which most policy-supporting CNI plugins like Calico and Cilium do.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 51
[HARD]

How do you specify that a Network Policy applies to both ingress and egress?

A) Create two separate policies
B) Set policyTypes to include both Ingress and Egress
C) It's automatic
D) Use the bidirectional field

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** To apply a Network Policy to both ingress and egress traffic, you must explicitly include both "Ingress" and "Egress" in the policyTypes array, enabling the policy to control traffic in both directions.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

## DNS in Kubernetes

### Question 52
[MEDIUM]

What is the default fully qualified domain name (FQDN) format for a Service?

A) service.namespace.cluster.local
B) service.namespace.svc.cluster.local
C) namespace.service.svc.cluster.local
D) service.svc.namespace.cluster.local

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The FQDN format for a Kubernetes Service is `<service-name>.<namespace>.svc.cluster.local`, where "svc" indicates it's a Service record and "cluster.local" is the default cluster domain suffix.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 53
[MEDIUM]

What DNS record type is created for a regular ClusterIP Service?

A) CNAME
B) A record (or AAAA for IPv6)
C) SRV
D) TXT

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A regular ClusterIP Service gets an A record (for IPv4) or AAAA record (for IPv6) that resolves to the Service's ClusterIP address, enabling DNS-based service discovery.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 54
[MEDIUM]

What is the default domain suffix for Services in Kubernetes?

A) kubernetes.local
B) cluster.local
C) svc.local
D) k8s.local

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The default domain suffix "cluster.local" is the standard cluster domain used in Kubernetes DNS, forming the base for all Service and Pod DNS names within the cluster.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 55
[MEDIUM-HARD]

What is the DNS format for discovering named ports on a Service?

A) port.protocol.service.namespace.svc.cluster.local
B) _port._protocol.service.namespace.svc.cluster.local (SRV record)
C) service.port.namespace.svc.cluster.local
D) Named ports don't have DNS records

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Named ports on Services get SRV records in the format `_<port-name>._<protocol>.<service>.<namespace>.svc.cluster.local`, allowing clients to discover both the port number and the target hostname.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 56
[MEDIUM-HARD]

What is the purpose of the `dnsConfig` field in a Pod spec?

A) To completely override DNS settings
B) To customize DNS settings alongside the policy
C) To disable DNS
D) To set the DNS server IP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The dnsConfig field allows customizing DNS settings like nameservers, search domains, and options, which are merged with settings from the selected dnsPolicy to provide fine-grained DNS configuration.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 57
[HARD]

How can you optimize DNS resolution for Pods making many external DNS queries?

A) Increase ndots value
B) Decrease ndots value or use FQDNs
C) Disable DNS caching
D) Use IP addresses only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Reducing ndots (e.g., to 2) or using fully qualified domain names with a trailing dot prevents unnecessary search domain lookups for external domains, reducing DNS query overhead and latency.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 58
[HARD]

What happens to DNS resolution for Pods using the default dnsPolicy (ClusterFirst) if CoreDNS Pods are not running?

A) DNS continues working from cache
B) All DNS resolution fails (both internal and external names)
C) External DNS is used instead automatically
D) The cluster automatically restarts CoreDNS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For Pods using dnsPolicy: ClusterFirst (the default), all DNS resolution fails when CoreDNS is down—both internal Service names and external domain names—because CoreDNS handles all queries and forwards external ones to upstream resolvers. Pods using dnsPolicy: Default or None with custom nameservers can still resolve external names via node or custom resolvers.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 59
[HARD]

How does DNS work for StatefulSet Pods?

A) Same as regular Pods
B) Each Pod gets a predictable DNS entry: pod-name.service-name.namespace.svc.cluster.local
C) StatefulSet Pods don't have DNS
D) Only the first Pod gets a DNS entry

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** StatefulSet Pods with a headless Service get predictable DNS entries in the format `<pod-name>.<service-name>.<namespace>.svc.cluster.local`, providing stable network identities that persist across Pod rescheduling.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 60
[HARD]

How can you verify DNS resolution from within a Pod?

A) kubectl dns
B) Using nslookup or dig from within the Pod
C) kubectl describe dns
D) Checking the API server logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Running nslookup, dig, or host commands from within a Pod directly queries the DNS server configured in the Pod's /etc/resolv.conf, allowing you to verify Service name resolution and troubleshoot DNS issues.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

## kube-proxy and Service Discovery

### Question 61
[MEDIUM]

Which kube-proxy mode is the default in most modern Kubernetes clusters?

A) userspace
B) iptables
C) ipvs
D) nftables

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The iptables mode is the default in most Kubernetes installations, programming iptables NAT rules for Service routing. While IPVS mode offers better performance at scale, iptables remains the widely-used default.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 62
[MEDIUM]

How does kube-proxy learn about Services and Endpoints?

A) By reading iptables rules
B) By watching the Kubernetes API
C) By polling the CNI plugin
D) By reading local configuration files

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-proxy uses the Kubernetes watch API to receive real-time updates about Service and Endpoint/EndpointSlice changes, automatically updating the network rules whenever the cluster state changes.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 63
[MEDIUM-HARD]

What is the main advantage of IPVS mode over iptables mode?

A) Simpler configuration
B) Better performance at scale with O(1) complexity for lookups
C) More secure
D) Better Windows support

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** IPVS mode uses hash tables for O(1) lookup complexity compared to iptables' O(n) linear chain traversal, making it significantly more efficient for clusters with thousands of Services or endpoints.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 64
[MEDIUM-HARD]

How does kube-proxy receive its configuration?

A) From a Secret only
B) Via command-line flags or a configuration file (--config)
C) Directly from the API server at runtime
D) From environment variables only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-proxy can be configured via command-line flags or a configuration file specified with --config. In kubeadm-managed clusters, the config file is typically stored in a ConfigMap and mounted into the kube-proxy DaemonSet Pods.

**Source:** [kube-proxy | Kubernetes](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/)

</details>

---

### Question 65
[MEDIUM-HARD]

What is the purpose of EndpointSlices?

A) To replace Services
B) To provide more scalable and efficient endpoint tracking
C) To slice network traffic
D) To manage storage endpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** EndpointSlices provide more scalable endpoint tracking by splitting endpoints into smaller groups (default 100 endpoints per slice), reducing API server and kube-proxy load when Services have many backend Pods.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 66
[HARD]

What is the `--proxy-mode` flag used for?

A) To enable proxy authentication
B) To select the kube-proxy backend implementation
C) To configure proxy protocols
D) To set proxy timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The --proxy-mode flag specifies which kube-proxy implementation to use. The stable modes are "iptables" (default) and "ipvs" (better performance at scale). The legacy "userspace" mode is deprecated and rarely used.

**Source:** [kube-proxy | Kubernetes](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/)

</details>

---

### Question 67
[HARD]

What is the `conntrack` table used for in Kubernetes networking?

A) To track connection attempts
B) To track established connections for stateful packet inspection
C) To store DNS records
D) To track Pod connections

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The conntrack (connection tracking) table maintains state for established connections, enabling stateful packet inspection and ensuring that reply packets are correctly routed back through NAT rules.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 68
[HARD]

What is the `--cluster-cidr` flag in kube-proxy used for?

A) To define the Service CIDR
B) To configure rules related to Pod CIDR for certain features
C) To set the node CIDR
D) To define external CIDRs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The --cluster-cidr flag tells kube-proxy the Pod CIDR range, which is used for features like masquerading outbound traffic and distinguishing cluster-internal from external traffic sources.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 69
[HARD]

How does IPVS mode handle Service VIPs?

A) Using iptables NAT
B) By binding VIPs to a dummy interface and using IPVS rules
C) By modifying routing tables
D) Using userspace proxying

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In IPVS mode, kube-proxy binds Service VIPs to a dummy interface (kube-ipvs0), then creates IPVS virtual server entries that load balance traffic to real server (Pod endpoint) entries.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

## Cluster Networking

### Question 70
[MEDIUM]

Can Pods communicate with other Pods in the cluster by default?

A) No, Network Policies are required
B) Yes, Kubernetes has a flat network model
C) Only within the same namespace
D) Only within the same node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes has a flat network model where all Pods can communicate with each other by default without Network Policies. Every Pod gets a unique cluster-wide IP address and can reach any other Pod directly.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 71
[MEDIUM-HARD]

What is a key trade-off of using overlay networking vs native routing?

A) Overlay is faster but less secure
B) Overlay adds encapsulation overhead but works without physical network changes
C) Native routing is simpler to configure
D) Overlay requires special hardware

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Overlay networking adds encapsulation overhead (extra headers, CPU for encap/decap) but works without requiring the underlying physical network to understand Pod addressing. Native routing has less overhead but requires the physical network to route Pod CIDRs.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 72
[HARD]

What are the security implications of using hostNetwork: true?

A) None; it's the recommended approach
B) The Pod shares the node's network namespace and can bind to node ports
C) It disables network policies
D) It prevents Pod communication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Using `hostNetwork: true` places the Pod in the node's network namespace, allowing it to bind to any port on the node's IP addresses. This bypasses Pod network isolation and should be used cautiously, typically only for system components like CNI plugins.

**Source:** [Pod networking | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/#pod-networking)

</details>

---

## Advanced Service Configuration

### Question 73
[HARD]

How does traffic flow when accessing a ClusterIP Service from a Pod on the same node as a backend Pod?

A) Always routed through an external network hop
B) kube-proxy DNATs to a backend; if the endpoint is local, traffic stays on-node
C) Through the API server
D) The CNI bypasses kube-proxy for local traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Service VIPs are typically implemented by kube-proxy (or a replacement like Cilium's eBPF-based implementation). In iptables/IPVS mode, the Service IP is DNATed to a backend Pod IP. If the selected endpoint is on the same node, traffic stays local after the NAT.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 74
[HARD]

What happens when you set `externalIPs` on a Service?

A) A load balancer is created
B) Traffic to those IPs (on the Service port) is routed to the Service
C) The Service becomes accessible from the internet
D) DNS records are updated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When `externalIPs` is configured, kube-proxy creates rules to intercept traffic destined for those IP addresses on the Service port and route it to the Service's backend Pods, without creating a load balancer or modifying DNS.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 75
[HARD]

What is the purpose of the `healthCheckNodePort` field in a LoadBalancer Service?

A) To specify a custom health check endpoint
B) To define a port for external load balancer health checks when using externalTrafficPolicy: Local
C) To configure internal health monitoring
D) To set the kubelet health check port

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When using externalTrafficPolicy: Local, the healthCheckNodePort specifies a port on each node where the cloud load balancer can check if local endpoints exist. This allows the load balancer to only send traffic to nodes that have healthy Pods.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 76
[HARD]

What happens when `internalTrafficPolicy: Local` is set?

A) External traffic is blocked
B) Internal traffic is only routed to Pods on the same node
C) All traffic becomes internal
D) Load balancing is disabled

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `internalTrafficPolicy: Local`, kube-proxy only includes endpoints running on the same node, reducing network hops and latency but potentially causing connection failures if no local endpoints are available.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Service Mesh and Advanced Topics

### Question 77
[MEDIUM]

Which of the following is a popular service mesh for Kubernetes?

A) Calico
B) Istio
C) Flannel
D) CoreDNS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Istio is one of the most popular service mesh implementations for Kubernetes, providing advanced traffic management, security, and observability features, while Calico and Flannel are CNI plugins and CoreDNS is a DNS server.

**Source:** [What is Istio? | Istio](https://istio.io/latest/about/)

</details>

---

### Question 78
[MEDIUM]

What is mTLS in the context of service mesh?

A) Multi-tier Load Balancing Service
B) Mutual TLS for encrypting pod-to-pod communication
C) Managed TLS certificates
D) Micro TLS protocol

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Mutual TLS (mTLS) requires both the client and server to present certificates and verify each other's identity, providing encrypted communication and strong authentication between services in the mesh.

**Source:** [Security | Istio](https://istio.io/latest/docs/concepts/security/)

</details>

---

### Question 79
[MEDIUM-HARD]

What is the control plane in a service mesh?

A) The proxy containers
B) The components that configure and manage the data plane
C) The networking hardware
D) The Kubernetes control plane

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The control plane manages and configures the data plane proxies, handling tasks like certificate issuance, policy distribution, and service discovery configuration, allowing centralized management of the mesh.

**Source:** [Architecture | Istio](https://istio.io/latest/docs/ops/deployment/architecture/)

</details>

---

### Question 80
[MEDIUM-HARD]

What is circuit breaking in service mesh?

A) A security feature
B) A pattern to prevent cascading failures by stopping requests to failing services
C) A network isolation technique
D) A debugging tool

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Circuit breaking monitors the health of service connections and stops sending requests to a failing service after a threshold of failures, preventing cascading failures and allowing the failing service time to recover.

**Source:** [Circuit Breaking | Istio](https://istio.io/latest/docs/tasks/traffic-management/circuit-breaking/)

</details>

---

### Question 81
[MEDIUM-HARD]

What observability features do service meshes typically provide?

A) Only logging
B) Distributed tracing, metrics, and logging
C) Only metrics
D) Only tracing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Service meshes provide comprehensive observability through distributed tracing (tracking requests across services), metrics (latency, error rates, traffic volume), and logging, giving visibility into service-to-service communication without application code changes.

**Source:** [Observability | Istio](https://istio.io/latest/docs/tasks/observability/)

</details>

---

### Question 82
[HARD]

What is an Envoy proxy?

A) A Kubernetes component
B) A high-performance proxy used as the data plane in many service meshes
C) A type of load balancer
D) A DNS server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Envoy is a high-performance, open-source edge and service proxy designed for cloud-native applications, serving as the data plane in service meshes like Istio, Consul Connect, and AWS App Mesh.

**Source:** [Architecture | Istio](https://istio.io/latest/docs/ops/deployment/architecture/)

</details>

---

### Question 83
[HARD]

What is the DestinationRule resource in Istio?

A) A firewall rule
B) A configuration for policies applied to traffic after routing
C) A routing destination
D) A DNS rule

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DestinationRule is an Istio CRD that configures policies applied after routing decisions, including load balancing algorithms, connection pool settings, circuit breaker thresholds, and TLS settings for traffic to a destination.

**Source:** [Destination Rule | Istio](https://istio.io/latest/docs/reference/config/networking/destination-rule/)

</details>

---

### Question 84
[HARD]

What is the difference between sidecar-based and eBPF-based (sidecarless) service meshes?

A) No difference in architecture
B) Sidecar-based uses proxy containers with iptables redirection; eBPF-based operates in the kernel without sidecars
C) Sidecar-based is faster
D) eBPF-based requires more containers

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Traditional sidecar-based service meshes (like Istio) inject proxy containers into each Pod and use iptables to redirect traffic through them. eBPF-based meshes (like Cilium) implement mesh functionality directly in the Linux kernel, eliminating sidecar overhead and reducing latency.

**Source:** [Service Mesh | Cilium Documentation](https://docs.cilium.io/en/stable/network/servicemesh/)

</details>

---

### Question 85
[HARD]

What is the purpose of PeerAuthentication in Istio?

A) To authenticate users
B) To configure mTLS requirements between workloads
C) To authenticate API requests
D) To configure RBAC

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** PeerAuthentication is an Istio CRD that defines mutual TLS (mTLS) requirements for workloads, specifying whether mTLS is disabled, permissive (accepts both plaintext and mTLS), or strict (requires mTLS only).

**Source:** [PeerAuthentication | Istio](https://istio.io/latest/docs/reference/config/security/peer_authentication/)

</details>

---

## Gateway API

### Question 86
[HARD]

What is the Gateway API and how does it relate to service mesh?

A) A replacement for Kubernetes API
B) A standard API for advanced traffic management that service meshes can implement
C) A specific service mesh implementation
D) A deprecated API

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Gateway API is a Kubernetes SIG-Network project providing a standard, expressive API for advanced traffic management that service mesh implementations can adopt, offering a unified interface across different service mesh solutions.

**Source:** [Gateway API | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/gateway/)

</details>

---

## Troubleshooting and Diagnostics

### Question 87
[MEDIUM]

What is the preferred API for viewing Service endpoints in large clusters?

A) Endpoints
B) EndpointSlices
C) ServiceEndpoints
D) PodEndpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** EndpointSlices are the preferred API for viewing Service endpoints, especially in large clusters. They split endpoints into smaller groups (default 100 per slice), reducing API server load and improving scalability compared to the legacy Endpoints resource.

**Source:** [EndpointSlices | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/)

</details>

---

### Question 88
[MEDIUM]

What does the `dnsPolicy: ClusterFirst` setting do for a Pod?

A) Uses only external DNS servers
B) Queries cluster DNS first, then falls back to upstream DNS for non-cluster names
C) Disables DNS completely
D) Uses only the node's DNS settings

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With dnsPolicy: ClusterFirst (the default), the Pod uses the cluster DNS server (CoreDNS) first. Queries for cluster domain names (like service.namespace.svc.cluster.local) are resolved internally, while external names are forwarded to upstream DNS servers.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 89
[MEDIUM]

How can you verify that kube-proxy is running and healthy?

A) kubectl get pods -n kube-system | grep kube-proxy
B) kubectl get services
C) kubectl describe nodes
D) kubectl logs apiserver

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** kube-proxy runs as a DaemonSet in the kube-system namespace, so checking its Pod status with `kubectl get pods -n kube-system | grep kube-proxy` verifies that it is running on all nodes.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 90
[MEDIUM-HARD]

What is a common infrastructure cause of cluster-wide DNS resolution failures?

A) A single Service was deleted
B) CoreDNS Pods are not running or misconfigured
C) Too many Services in the cluster
D) High CPU usage on worker nodes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Cluster-wide DNS resolution failures typically occur when CoreDNS Pods are not running, have crashed, are misconfigured, or cannot reach the Kubernetes API. This affects all DNS queries, not just individual Services.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 91
[MEDIUM-HARD]

What is the purpose of an ephemeral debug container?

A) To store temporary data
B) To attach a debugging container to a running Pod for troubleshooting
C) To run tests
D) To collect metrics

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ephemeral debug containers allow you to attach a temporary container with debugging tools to a running Pod without restarting it, useful for troubleshooting when the original container lacks debugging utilities.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

---

### Question 92
[MEDIUM-HARD]

What might cause intermittent connectivity issues between Pods?

A) DNS caching
B) Network policy changes, Pod rescheduling, or CNI issues
C) Too many namespaces
D) API server load

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Intermittent connectivity issues can be caused by network policies being updated, Pods being rescheduled (changing endpoints), CNI plugin issues, node network problems, or resource exhaustion affecting network performance.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 93
[HARD]

What tool can help visualize network policies in a cluster?

A) kubectl visualize
B) CNI-specific tools like Cilium's Hubble or third-party visualization tools
C) The Kubernetes dashboard
D) kube-proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network policy visualization is typically provided by CNI-specific tools. For example, Cilium's Hubble provides real-time network flow visualization. Third-party tools and web-based editors can also help visualize and validate policy configurations.

**Source:** [Hubble | Cilium Documentation](https://docs.cilium.io/en/stable/observability/hubble/)

</details>

---

### Question 94
[HARD]

How can you identify if packet loss is occurring between Pods?

A) kubectl get packet-loss
B) Using ping, iperf, or packet capture tools
C) Checking the API server
D) Reviewing kubelet logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Packet loss between Pods can be detected using ping (ICMP) to measure loss percentage, iperf for bandwidth testing with packet statistics, or tcpdump/Wireshark to analyze captured traffic for missing packets.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 95
[HARD]

What might cause high latency for Service requests?

A) Too many labels
B) Network congestion, long proxy chains, or backend Pod issues
C) Too many namespaces
D) Large ConfigMaps

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** High Service latency can result from network congestion between nodes, multiple proxy hops in service mesh configurations, slow backend Pods, DNS resolution delays, or resource constraints on nodes affecting packet processing.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 96
[HARD]

How can you trace the network path of a packet in Kubernetes?

A) kubectl trace
B) Using traceroute, packet captures, and examining iptables/IPVS rules
C) kubectl describe path
D) Using the Kubernetes API

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Tracing network paths requires combining tools: traceroute shows the Layer 3 path, packet captures reveal actual traffic flow, and examining iptables/IPVS rules shows how kube-proxy routes traffic to backend Pods.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 97
[HARD]

What is the purpose of the `kubectl port-forward` command?

A) To permanently expose a Service
B) To create a temporary tunnel from local machine to a Pod/Service for debugging
C) To configure port mappings
D) To forward ports between Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl port-forward` creates a temporary tunnel from a local port to a Pod or Service port, allowing direct access for debugging without exposing the application through a Service or Ingress.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 98
[HARD]

How can you debug a network policy that seems to be blocking expected traffic?

A) Delete the policy
B) Check policy selectors, verify Pod labels, and test with explicit allow rules
C) Restart kube-proxy
D) Restart the CNI

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Debugging network policies involves verifying Pod labels match policy selectors, checking namespace labels for namespace selectors, testing with explicit allow rules, and temporarily removing policies to confirm they are the source of blocking.

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 99
[HARD]

What information does `kubectl describe service` provide for debugging?

A) Network traffic statistics
B) Service configuration, endpoints, and events
C) Pod logs
D) Node status

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** `kubectl describe service` shows the Service configuration (type, ports, selector), the endpoints (backend Pod IPs), and any events related to the Service, providing a comprehensive view for troubleshooting connectivity issues.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 100
[HARD]

What is the recommended approach for debugging complex networking issues in production?

A) Restart all components
B) Systematic isolation: check DNS, endpoints, network policies, CNI, and kube-proxy sequentially
C) Delete and recreate all Services
D) Scale down to one node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Systematic troubleshooting involves checking each layer sequentially: verifying DNS resolution, confirming Service endpoints exist, testing network policy rules, checking CNI plugin health, and examining kube-proxy rules, to isolate the root cause.

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---
