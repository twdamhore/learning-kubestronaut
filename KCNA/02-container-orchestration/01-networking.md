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

**Explanation:** CNI stands for Container Network Interface, a specification and set of libraries for configuring network interfaces in Linux containers, enabling Kubernetes to use various networking solutions through a standardized plugin architecture.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** The primary responsibility of a CNI plugin is to provide network connectivity to Pods by allocating IP addresses and setting up network interfaces, routes, and any necessary network namespaces.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** Calico is widely used in cloud environments because it supports network policies natively without requiring additional components, and can operate in both overlay and non-overlay modes with BGP routing capabilities.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** When a Pod is created, the kubelet on that node invokes the CNI plugin to set up the Pod's network namespace, assign an IP address, and configure routing so the Pod can communicate with other Pods and services.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** CNI plugin configuration files are stored in /etc/cni/net.d/ on each node, where the kubelet reads them to determine which CNI plugin to use and how to configure it.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** Flannel's default backend is VXLAN, which encapsulates Layer 2 Ethernet frames within UDP packets to create an overlay network, allowing Pod traffic to traverse the underlying physical network.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

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

**Explanation:** IPAM (IP Address Management) in a CNI configuration defines how IP addresses are allocated to Pods, specifying the subnet range, gateway, and allocation method (such as host-local or DHCP).

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** Cilium leverages eBPF (extended Berkeley Packet Filter) to implement networking, security, and observability directly in the Linux kernel, providing high-performance packet processing without relying on iptables.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** BGP (Border Gateway Protocol) support allows CNI plugins like Calico to advertise Pod network routes directly to the physical network infrastructure, enabling native routing without overlay encapsulation overhead.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 10
[MEDIUM-HARD]

In a multi-node cluster, what ensures that Pod IP addresses don't conflict?

A) The kube-scheduler assigns IPs during scheduling
B) Per-node PodCIDR allocation plus CNI IPAM within each node's range
C) The API server's validation webhook
D) etcd's unique key constraints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kube-controller-manager allocates a unique PodCIDR range to each node from the cluster's Pod network CIDR. The CNI plugin's IPAM then assigns IPs from that node-local range. This two-tier approach (cluster-level CIDR allocation + node-local IPAM) prevents conflicts without requiring cluster-wide IP coordination for every Pod.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

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

**Explanation:** Calico's IPIP mode uses IP-in-IP encapsulation (IP protocol 4), which wraps the original IP packet inside another IP header, providing a lightweight overlay with less overhead than VXLAN.

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

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

**Explanation:** In CNI plugin configurations, the "subnet" field within the IPAM section specifies the network range from which Pod IP addresses will be allocated.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** CNI ADD creates the network namespace, assigns an IP, and sets up routing for a container, while CNI DEL reverses these operations by releasing the IP and removing the network configuration when the container stops.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** Chained CNI plugins are executed sequentially, with each plugin handling a specific networking task such as creating the interface (bridge), assigning an IP (IPAM), or applying bandwidth limits, allowing modular and composable network configurations.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** CNI plugin configurations are written in JSON format, stored in /etc/cni/net.d/ with a .conf or .conflist extension, and parsed by the kubelet when invoking CNI operations.

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

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

**Explanation:** ClusterIP is the default Service type in Kubernetes, providing an internal virtual IP that is only reachable from within the cluster for pod-to-pod communication.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** A ClusterIP Service provides a stable internal IP address for communication between Pods within the cluster, enabling service discovery and load balancing without exposing the service externally.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** Services use label selectors to identify which Pods should receive traffic, matching Pods based on their labels rather than names or IPs, allowing dynamic endpoint discovery as Pods are created or destroyed.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** The "port" field specifies the port on which the Service is exposed and receives traffic, while "targetPort" specifies the port on the backend Pods where traffic is forwarded.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** ClusterIP addresses are allocated from the Service CIDR range, which is configured via the --service-cluster-ip-range flag on the kube-apiserver and is separate from the Pod CIDR.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** When targetPort is not specified, Kubernetes defaults it to the same value as the Service port, assuming the backend Pods listen on the same port number as the Service exposes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 22
[MEDIUM-HARD]

What happens to existing connections when a Pod backing a Service is terminated?

A) They are immediately dropped
B) They are guaranteed to be gracefully drained
C) They are migrated to another Pod
D) They continue until the Pod stops or the client closes the connection

<details>
<summary>Show Answer</summary>

**Answer:** D

**Explanation:** Kubernetes stops routing new connections when endpoints are removed, but existing connections are not automatically drained. They continue until the Pod exits, the client closes the connection, or client timeout occurs. Graceful draining requires application-level handling using preStop hooks or readiness probe manipulation.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** The "kubectl get endpoints" command directly shows the IP addresses and ports of all Pods that are currently selected by a Service, making it the most direct way to verify endpoint associations.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** Session affinity (also called sticky sessions) ensures that all requests from a particular client are routed to the same backend Pod, which is useful for applications that store session state locally.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** Kubernetes supports "ClientIP" as the session affinity type, which uses the client's source IP address to consistently route requests to the same Pod. Cookie-based affinity is not natively supported at the Service level.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** The default session affinity timeout is 10800 seconds (3 hours), after which the affinity mapping expires and subsequent requests may be routed to a different Pod. This can be customized via sessionAffinityConfig.clientIP.timeoutSeconds.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** Setting publishNotReadyAddresses to true causes the Service to include Pod IPs in DNS responses and endpoints even when Pods are not ready, which is useful for headless Services in StatefulSets where Pods need to discover each other during startup.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** Services are namespace-scoped resources and can only select Pods within their own namespace. To route traffic across namespaces, you would need to use ExternalName Services or create Services in each namespace.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** In iptables mode, kube-proxy creates DNAT (Destination NAT) rules in the KUBE-SERVICES and KUBE-SVC-* chains that redirect traffic destined for ClusterIP addresses to the actual Pod endpoints.

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

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

**Explanation:** The ipFamilyPolicy field controls dual-stack behavior with values like SingleStack, PreferDualStack, or RequireDualStack, determining whether the Service gets IPv4 only, IPv6 only, or both address families.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** The default NodePort range is 30000-32767, which can be changed using the --service-node-port-range flag on the kube-apiserver. This range is chosen to avoid conflicts with well-known ports.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** A NodePort Service is accessible on the same port across all nodes in the cluster, regardless of which nodes are running the backend Pods. Traffic can enter through any node and be routed to the appropriate Pod.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** When you create a NodePort Service, Kubernetes automatically creates a ClusterIP for the Service as well, providing both internal cluster access (via ClusterIP) and external access (via NodePort).

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** You can specify a specific NodePort number using the nodePort field within the ports section of the Service spec. If not specified, Kubernetes automatically assigns an available port from the NodePort range.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** NodePorts are unique across the cluster. If you specify a NodePort that is already allocated to another Service, the API server rejects the Service creation with a conflict error.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** External traffic hits the NodePort on any cluster node, which then gets DNATed to the Service's ClusterIP, and finally to one of the backend Pod endpoints through kube-proxy's iptables or IPVS rules.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** The externalTrafficPolicy field determines whether external traffic is load balanced across all Pods cluster-wide (Cluster) or only to Pods on the node receiving the traffic (Local), affecting both load distribution and client IP preservation.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** With externalTrafficPolicy: Local, kube-proxy only routes traffic to Pods running on the same node that received the traffic. This preserves the original client IP (no SNAT) but may result in uneven load distribution.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 39
[HARD]

When `externalTrafficPolicy: Local` is set, what happens if no local Pods exist on a node receiving traffic?

A) Traffic is forwarded to another node
B) For LoadBalancer Services, the node fails health checks; for direct NodePort access, traffic is dropped
C) The request hangs until a Pod is scheduled
D) A 503 error is immediately returned

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** With `externalTrafficPolicy: Local`, traffic is only routed to Pods on the same node. For LoadBalancer Services, the cloud provider's health check removes the node from the load balancer target pool. However, for direct NodePort access (bypassing the LB), traffic to a node with no local Pods is simply dropped since there's no health check mechanism.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

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

**Explanation:** With externalTrafficPolicy: Cluster, traffic can be forwarded to any Pod in the cluster regardless of which node receives it, resulting in more even distribution but at the cost of an extra network hop and SNAT that obscures the client IP.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 41
[HARD]

How can you change the default NodePort range in a Kubernetes cluster?

A) Modify the Service specification
B) Update kube-apiserver's --service-node-port-range flag
C) Edit the kube-proxy ConfigMap
D) Change the CNI configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The NodePort range is controlled by the --service-node-port-range flag on the kube-apiserver, which validates and allocates NodePorts. Changing this requires modifying the API server configuration.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 42
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

### Question 43
[HARD]

In a cloud environment, why might NodePort Services be less preferred than LoadBalancer?

A) NodePort is slower
B) NodePort exposes all nodes and requires external load balancing
C) NodePort doesn't support TCP
D) NodePort Services cost more

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** NodePort Services expose ports on all cluster nodes, requiring you to manage external load balancing yourself. LoadBalancer Services automatically provision a cloud load balancer that handles health checking and routing to healthy nodes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Kubernetes Services - LoadBalancer

### Question 44
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

### Question 45
[MEDIUM]

What happens when you create a LoadBalancer Service in a bare-metal cluster without a cloud provider?

A) A software load balancer is automatically created
B) The Service remains in Pending state
C) It falls back to NodePort automatically
D) An error is thrown

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Without a cloud provider or load balancer controller (like MetalLB), the Service will remain in Pending state indefinitely because there is no component to provision the external load balancer and assign an external IP.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 46
[MEDIUM]

Which components are created when a LoadBalancer Service is provisioned?

A) LoadBalancer only
B) ClusterIP and NodePort only
C) ClusterIP, NodePort, and external LoadBalancer
D) External LoadBalancer only

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** A LoadBalancer Service is a superset that includes all three components: a ClusterIP for internal access, a NodePort for node-level exposure, and an external load balancer that forwards traffic to the NodePort on cluster nodes.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 47
[MEDIUM-HARD]

How does MetalLB enable LoadBalancer Services in bare-metal clusters?

A) By deploying cloud provider APIs
B) By announcing Service IPs via ARP/BGP protocols
C) By creating virtual machines
D) By proxying through the master node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** MetalLB provides LoadBalancer functionality in bare-metal clusters by assigning external IPs from a configured pool and announcing them using either Layer 2 (ARP/NDP) or BGP protocols to make them reachable from the external network.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 48
[MEDIUM-HARD]

What annotation is commonly used to specify an internal load balancer in cloud environments?

A) service.kubernetes.io/load-balancer-internal
B) cloud.google.com/load-balancer-type: "Internal" or similar cloud-specific annotation
C) kubernetes.io/internal-lb: "true"
D) loadbalancer.kubernetes.io/internal

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Internal load balancer annotations are cloud-specific. For example, GCP uses cloud.google.com/load-balancer-type: "Internal", AWS uses service.beta.kubernetes.io/aws-load-balancer-internal: "true", and Azure uses service.beta.kubernetes.io/azure-load-balancer-internal: "true".

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 49
[MEDIUM-HARD]

What is the purpose of the `loadBalancerIP` field in a Service specification?

A) To get the assigned load balancer IP
B) To request a specific IP address for the load balancer
C) To configure the backend IP
D) To set the ClusterIP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The loadBalancerIP field allows you to request a specific IP address for the external load balancer, which is useful when you need a stable, pre-determined external IP. Support depends on the cloud provider.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 50
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

### Question 51
[HARD]

How does the cloud-controller-manager interact with LoadBalancer Services?

A) It doesn't; kube-proxy handles everything
B) It watches for LoadBalancer Services and provisions cloud resources
C) It only handles node registration
D) It manages Pod scheduling

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The cloud-controller-manager watches for Services of type LoadBalancer and interacts with the cloud provider's API to provision external load balancers, configure health checks, and assign external IPs.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 52
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

### Question 53
[HARD]

When using AWS NLB (Network Load Balancer) in instance target mode, what is required to preserve the client IP end-to-end?

A) Only the NLB annotation; client IP is automatically preserved
B) Set externalTrafficPolicy: Local on the Service to prevent kube-proxy SNAT
C) Enable proxy protocol on both NLB and application
D) Client IP preservation is not possible with instance target mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** While AWS NLB preserves the client IP at Layer 4, kube-proxy with the default `externalTrafficPolicy: Cluster` will SNAT the traffic when forwarding to Pods on other nodes. To preserve the client IP end-to-end, you must set `externalTrafficPolicy: Local` on the Service, which prevents kube-proxy from masquerading the source IP.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 54
[HARD]

What is the difference between a Layer 4 and Layer 7 load balancer in Kubernetes context?

A) Layer 4 is faster, Layer 7 is more secure
B) Layer 4 operates at TCP/UDP level, Layer 7 operates at HTTP level
C) Layer 4 is internal, Layer 7 is external
D) Layer 4 is cloud-only, Layer 7 is on-premises

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Layer 4 load balancers (like NLB) route based on IP and port information, while Layer 7 load balancers (like ALB or Ingress) can inspect HTTP headers, paths, and content for more sophisticated routing decisions.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Kubernetes Services - ExternalName and Headless

### Question 55
[MEDIUM]

What is an ExternalName Service used for?

A) To expose internal services externally
B) To create a CNAME alias to an external DNS name
C) To assign external IPs to Pods
D) To configure external authentication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An ExternalName Service maps a Service name to an external DNS name by returning a CNAME record, allowing Pods to access external services using a consistent internal Service name.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 56
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

### Question 57
[MEDIUM]

What is returned when you do a DNS lookup for a headless Service?

A) The ClusterIP
B) The IP addresses of all backing Pods
C) Nothing; DNS is disabled
D) The node IPs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DNS queries for a headless Service return A records for all Pod IPs in the endpoint list, allowing clients to perform their own load balancing or connect to specific Pods.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 58
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

### Question 59
[MEDIUM-HARD]

For an ExternalName Service, what type of DNS record is created?

A) A record
B) AAAA record
C) CNAME record
D) SRV record

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** ExternalName Services create a CNAME DNS record that aliases the Service name to the specified external hostname, redirecting DNS queries to the external target.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 60
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

### Question 61
[HARD]

What happens when a headless Service has a selector defined?

A) Endpoints are automatically populated with Pod IPs
B) The Service becomes a ClusterIP Service
C) An error occurs
D) Only the first Pod is selected

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** When a headless Service has a selector, Kubernetes automatically creates Endpoints containing the IPs of all Pods matching the selector, and DNS returns these Pod IPs directly.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 62
[HARD]

How can you manually define endpoints for a headless Service without a selector?

A) Create an Endpoints resource with the same name
B) Add IPs to the Service annotations
C) Use a ConfigMap
D) Define them in a separate YAML file

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** For Services without selectors, you must manually create an Endpoints resource with the same name as the Service, specifying the IP addresses and ports that the Service should route traffic to.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 63
[HARD]

What is the DNS format for StatefulSet Pods with a headless Service?

A) pod-ip.service.namespace.svc.cluster.local
B) pod-name.service-name.namespace.svc.cluster.local
C) pod-ip-dashed.namespace.pod.cluster.local
D) service-name.pod-name.namespace.svc.cluster.local

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** For StatefulSet Pods using a headless Service, the DNS format is `<pod-name>.<service-name>.<namespace>.svc.cluster.local`. For example, a StatefulSet named "web" with serviceName "nginx" creates Pods addressable as `web-0.nginx.default.svc.cluster.local`. This predictable naming enables stable network identities for stateful workloads.

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 64
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

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 65
[HARD]

Can an ExternalName Service point to another Kubernetes Service?

A) Yes, by using the full DNS name
B) No, it can only point to external names
C) Only within the same namespace
D) Only with specific annotations

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** An ExternalName Service can point to any DNS name including internal Kubernetes Service names (e.g., my-service.other-namespace.svc.cluster.local), enabling cross-namespace service aliasing.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Ingress and Ingress Controllers

### Question 66
[MEDIUM]

What is the primary purpose of an Ingress resource?

A) To create internal Services
B) To manage external HTTP/HTTPS access to Services
C) To configure network policies
D) To manage Pod networking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ingress provides HTTP/HTTPS routing from outside the cluster to Services inside, offering features like host-based routing, path-based routing, and TLS termination.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 67
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

### Question 68
[MEDIUM]

Which of the following is a popular Ingress controller?

A) kube-proxy
B) nginx-ingress-controller
C) flannel
D) coredns

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The nginx-ingress-controller is one of the most widely used Ingress controllers, using NGINX as the reverse proxy to route external HTTP/HTTPS traffic to backend Services.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 69
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

### Question 70
[MEDIUM]

How do you specify the backend Service for an Ingress rule?

A) Using labels
B) Using the service name and port
C) Using the Pod IP
D) Using annotations only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In an Ingress rule, the backend is specified using the Service name and port number (or port name), and the Ingress controller routes matching traffic to that Service.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 71
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

### Question 72
[MEDIUM-HARD]

How do you configure TLS termination in an Ingress?

A) Using the tls section with a Secret reference
B) Using annotations only
C) TLS is always automatic
D) Using a ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** TLS termination is configured in the Ingress spec's tls section by specifying the hosts and referencing a Secret containing the TLS certificate and private key.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 73
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

### Question 74
[MEDIUM-HARD]

What is path-based routing in Ingress?

A) Routing based on the URL path to different Services
B) Routing based on file system paths
C) Routing based on node paths
D) Routing based on network paths

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Path-based routing allows an Ingress to route requests to different backend Services based on the URL path, such as /api going to one Service and /web to another.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 75
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

### Question 76
[HARD]

What happens when multiple Ingress rules match the same host and path?

A) All rules are applied simultaneously
B) Behavior is controller-specific; the Ingress spec does not define precedence
C) The Kubernetes API rejects duplicate rules
D) An error occurs and no traffic is routed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Ingress specification does not define how controllers should handle overlapping rules. Different Ingress controllers implement their own precedence logic—many use longest path match, some use creation timestamp, others use alphabetical ordering. Always consult your specific Ingress controller's documentation for conflict resolution behavior.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 77
[HARD]

How can you implement rate limiting in nginx-ingress-controller?

A) Using the rateLimiting field in Ingress spec
B) Using annotations like nginx.ingress.kubernetes.io/limit-rps
C) Rate limiting is not supported
D) Using a separate ConfigMap

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The nginx-ingress-controller supports rate limiting through annotations like nginx.ingress.kubernetes.io/limit-rps (requests per second) and nginx.ingress.kubernetes.io/limit-connections to control traffic.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 78
[HARD]

What is the purpose of a default backend in an Ingress?

A) To specify the primary service
B) To handle requests that don't match any rules
C) To provide health checks
D) To store default configurations

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The default backend is a fallback Service that receives requests when no Ingress rules match, typically returning a 404 page or redirecting users.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 79
[HARD]

How does the nginx Ingress controller discover Ingress resources?

A) By polling the API server
B) By watching Ingress resources via the Kubernetes API
C) By reading from etcd directly
D) By receiving push notifications from kubelet

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The nginx Ingress controller uses the Kubernetes watch API to monitor Ingress resources in real-time, automatically updating its NGINX configuration when Ingress resources are created, modified, or deleted.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 80
[HARD]

What is the purpose of the `nginx.ingress.kubernetes.io/rewrite-target` annotation?

A) To rewrite the response body
B) To rewrite the URL path before forwarding to the backend
C) To rewrite the Host header
D) To rewrite the client IP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The rewrite-target annotation modifies the URL path before forwarding the request to the backend, commonly used to strip path prefixes so the backend receives requests at its expected paths.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 81
[HARD]

How can you configure sticky sessions in nginx-ingress?

A) Using sessionAffinity in the Service
B) Using nginx.ingress.kubernetes.io/affinity annotation
C) Sticky sessions are not supported
D) Using a Cookie header in the request

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The nginx-ingress-controller supports sticky sessions via the nginx.ingress.kubernetes.io/affinity annotation set to "cookie", which uses cookies to maintain session affinity to specific backend Pods.

</details>

---

### Question 82
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

</details>

---

### Question 83
[HARD]

How can you set an IngressClass as the default for the cluster?

A) Using the default: true field
B) Using the ingressclass.kubernetes.io/is-default-class annotation
C) Setting it in kube-controller-manager
D) It's automatic for the first IngressClass created

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Setting the ingressclass.kubernetes.io/is-default-class annotation to "true" on an IngressClass makes it the default, so Ingress resources without an ingressClassName will use this controller.

</details>

---

### Question 84
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

</details>

---

### Question 85
[HARD]

How can you configure client certificate authentication (mTLS) in nginx-ingress?

A) Using TLS secrets only
B) Using annotations like nginx.ingress.kubernetes.io/auth-tls-secret
C) mTLS is not supported
D) Using a sidecar container

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nginx-ingress supports mTLS through annotations like nginx.ingress.kubernetes.io/auth-tls-secret (CA certificate for client verification) and nginx.ingress.kubernetes.io/auth-tls-verify-client to enforce client certificate authentication.

</details>

---

## Network Policies

### Question 86
[MEDIUM]

What is a Network Policy used for?

A) To define routing rules
B) To control traffic flow to and from Pods
C) To configure DNS
D) To manage Service endpoints

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policies are Kubernetes resources that define rules to control which Pods can communicate with each other and with external endpoints, acting as a Pod-level firewall.

</details>

---

### Question 87
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

</details>

---

### Question 88
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

</details>

---

### Question 89
[MEDIUM]

What happens when you create a Network Policy that selects a Pod?

A) All traffic to that Pod is allowed
B) Only traffic matching the policy rules is allowed (default deny for selected direction)
C) The Pod is isolated from all traffic
D) Nothing changes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Once a Network Policy selects a Pod for a traffic direction (ingress/egress), that Pod becomes isolated in that direction, and only traffic explicitly allowed by some policy's rules is permitted.

</details>

---

### Question 90
[MEDIUM]

Which CNI plugins support Network Policies?

A) Flannel (without extensions)
B) Calico, Cilium, Weave
C) Bridge CNI only
D) All CNI plugins

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policy support requires CNI plugins that can implement the policy rules. Calico, Cilium, and Weave natively support Network Policies, while basic Flannel does not without additional components.

</details>

---

### Question 91
[MEDIUM-HARD]

What does `podSelector: {}` in a Network Policy mean?

A) Select no Pods
B) Select all Pods in the namespace
C) Select Pods with empty labels
D) Invalid syntax

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An empty podSelector ({}) matches all Pods in the Network Policy's namespace, commonly used for creating default deny policies that affect all Pods.

</details>

---

### Question 92
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

</details>

---

### Question 93
[MEDIUM-HARD]

Can Network Policies restrict traffic based on ports?

A) No, only IP-based filtering
B) Yes, using the ports field
C) Only for egress
D) Only for TCP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network Policies support port-based filtering through the ports field in ingress and egress rules, allowing you to specify allowed protocols (TCP, UDP, SCTP) and port numbers.

</details>

---

### Question 94
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

</details>

---

### Question 95
[MEDIUM-HARD]

How do you allow traffic from all Pods in a specific namespace?

A) Using namespaceSelector with matching labels
B) Using allowNamespace field
C) Using fromNamespace field
D) Network Policies can't filter by namespace

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The namespaceSelector in a from entry allows traffic from Pods in namespaces matching the label selector. Namespaces must have labels applied for this selector to match them.

</details>

---

### Question 96
[HARD]

What is the effect of an empty ingress rule (ingress: []) in a Network Policy?

A) Allow all ingress traffic
B) Deny all ingress traffic
C) No effect on ingress
D) Invalid syntax

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An empty ingress array (ingress: []) means no ingress rules are defined, so no traffic matches, effectively denying all ingress traffic to the selected Pods. To allow all traffic, you would use ingress: [{}].

</details>

---

### Question 97
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

</details>

---

### Question 98
[HARD]

What is the purpose of the `except` field in an ipBlock?

A) To add exceptions to the policy
B) To exclude specific IPs from the allowed CIDR range
C) To handle exception errors
D) To specify fallback IPs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The except field in an ipBlock allows you to exclude specific CIDR ranges from the allowed block, for example allowing 10.0.0.0/8 except for 10.0.0.0/24.

</details>

---

### Question 99
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

</details>

---

### Question 100
[HARD]

What happens when multiple Network Policies select the same Pod?

A) Only the first policy applies
B) Only the last policy applies
C) The union of all policies applies (additive)
D) An error occurs

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Network Policies are additive - when multiple policies select the same Pod, the allowed traffic is the union of all their rules. Traffic is allowed if any policy permits it, and policies never conflict.

</details>

---

### Question 101
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

</details>

---

### Question 102
[HARD]

What is the difference between putting selectors in the same `from` entry vs separate entries?

A) No difference
B) Same entry = AND logic, separate entries = OR logic
C) Same entry = OR logic, separate entries = AND logic
D) Separate entries are not allowed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When selectors are in the same `from` entry, they are combined with AND logic (both must match). When in separate entries, they use OR logic (traffic is allowed if either condition matches), providing flexible policy composition.

</details>

---

### Question 103
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

</details>

---

### Question 104
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

</details>

---

### Question 105
[HARD]

What is the behavior if policyTypes is not specified but ingress rules are defined?

A) Only Ingress type is assumed
B) Both Ingress and Egress are assumed
C) The policy is invalid
D) Default deny for all

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** If policyTypes is not specified but ingress rules are defined, Kubernetes automatically assumes policyTypes: [Ingress], applying the policy only to incoming traffic while leaving egress unrestricted.

</details>

---

## DNS in Kubernetes

### Question 106
[MEDIUM]

What is the default DNS server in most Kubernetes clusters?

A) BIND
B) dnsmasq
C) CoreDNS
D) Unbound

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** CoreDNS is the default DNS server in Kubernetes clusters since version 1.13, replacing kube-dns. It provides service discovery by watching the Kubernetes API and responding to DNS queries for Services and Pods.

</details>

---

### Question 107
[MEDIUM]

What is the fully qualified domain name (FQDN) format for a Service?

A) service.namespace.cluster.local
B) service.namespace.svc.cluster.local
C) namespace.service.svc.cluster.local
D) service.svc.namespace.cluster.local

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The FQDN format for a Kubernetes Service is `<service-name>.<namespace>.svc.cluster.local`, where "svc" indicates it's a Service record and "cluster.local" is the default cluster domain suffix.

</details>

---

### Question 108
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

</details>

---

### Question 109
[MEDIUM]

Where is the cluster DNS server IP configured in Pods?

A) /etc/hosts
B) /etc/resolv.conf
C) Environment variables
D) /etc/dns.conf

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The kubelet configures /etc/resolv.conf in each Pod with the cluster DNS server IP (typically the kube-dns Service ClusterIP) and search domains, enabling automatic DNS resolution for Services.

</details>

---

### Question 110
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

</details>

---

### Question 111
[MEDIUM-HARD]

What happens when you query a Service name without the full domain from within the same namespace?

A) The query fails
B) The search domains append the namespace and cluster domain
C) It returns all Service IPs
D) It returns the node IP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When a Pod queries a short Service name, the search domains configured in /etc/resolv.conf (like `<namespace>.svc.cluster.local`) are automatically appended, allowing simple names like "my-service" to resolve within the same namespace.

</details>

---

### Question 112
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

</details>

---

### Question 113
[MEDIUM-HARD]

What Pod DNS policy uses the node's DNS settings?

A) ClusterFirst
B) Default
C) None
D) NodeLocal

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The "Default" dnsPolicy inherits the DNS settings from the node where the Pod is running, using the node's /etc/resolv.conf configuration instead of the cluster DNS.

</details>

---

### Question 114
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

</details>

---

### Question 115
[MEDIUM-HARD]

How does CoreDNS know about Services in the cluster?

A) By reading /etc/hosts
B) By watching the Kubernetes API for Service and Endpoint changes
C) By querying external DNS
D) From ConfigMap updates only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** CoreDNS uses the Kubernetes plugin to watch the API server for Service and Endpoint changes, automatically updating its DNS records in real-time as cluster resources are created, modified, or deleted.

</details>

---

### Question 116
[HARD]

What is the purpose of the `ndots` option in resolv.conf?

A) To set the number of DNS servers
B) To determine when to use absolute vs relative DNS queries
C) To configure DNS caching
D) To set query timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The ndots option (default 5 in Kubernetes) specifies how many dots must be in a name before it's considered absolute. Names with fewer dots trigger search domain lookups first, which can cause extra DNS queries.

</details>

---

### Question 117
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

</details>

---

### Question 118
[HARD]

What is NodeLocal DNSCache?

A) A DNS caching layer running on each node for improved performance
B) A replacement for CoreDNS
C) A caching plugin for kube-proxy
D) A node-level DNS configuration

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** NodeLocal DNSCache runs a DNS caching agent on each node as a DaemonSet, reducing latency and load on CoreDNS by serving cached responses locally and avoiding conntrack issues with UDP DNS traffic.

</details>

---

### Question 119
[HARD]

How can you configure CoreDNS to forward specific domains to external DNS servers?

A) Using the forward plugin in CoreDNS ConfigMap
B) By editing /etc/resolv.conf on nodes
C) Through the API server
D) Using Network Policies

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The CoreDNS Corefile can be edited via its ConfigMap to add forward plugin directives, specifying which domains should be forwarded to which external DNS servers for resolution.

</details>

---

### Question 120
[HARD]

What happens to DNS resolution if CoreDNS Pods are not running?

A) DNS continues working from cache
B) Pods cannot resolve Service names
C) External DNS is used instead
D) The cluster automatically restarts CoreDNS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Without CoreDNS running, Pods cannot resolve Service names to IP addresses, causing service discovery failures. Pods can still communicate using direct IP addresses, but name resolution will fail.

</details>

---

### Question 121
[HARD]

What is the purpose of the `autopath` plugin in CoreDNS?

A) To automatically configure paths
B) To optimize search path resolution for Pod queries
C) To set up routing paths
D) To configure file paths

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The autopath plugin in CoreDNS optimizes DNS resolution by automatically determining the correct search path for Pod queries, reducing the number of DNS lookups needed to resolve cluster-internal names.

</details>

---

### Question 122
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

</details>

---

### Question 123
[HARD]

What is the `pods` directive in CoreDNS Kubernetes plugin used for?

A) To count Pod resources
B) To enable or configure A record generation for Pods
C) To restart Pods
D) To scale Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `pods` directive in the CoreDNS Kubernetes plugin controls whether and how A records are created for individual Pods, with options like "verified" to only create records for existing Pods or "insecure" for all Pod IP patterns.

</details>

---

### Question 124
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

</details>

---

### Question 125
[HARD]

What is the impact of setting `dnsPolicy: None` without `dnsConfig`?

A) Uses cluster DNS
B) Uses node DNS
C) The Pod will have no DNS configuration and may not resolve names
D) An error prevents Pod creation

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** Setting dnsPolicy: None without providing dnsConfig results in an empty /etc/resolv.conf, leaving the Pod unable to resolve any DNS names since no nameservers or search domains are configured.

</details>

---

## kube-proxy and Service Discovery

### Question 126
[MEDIUM]

What is the primary function of kube-proxy?

A) To proxy API requests
B) To implement Service networking rules on each node
C) To manage container networking
D) To schedule Pods

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-proxy's primary function is to implement Service networking by programming iptables, IPVS, or nftables rules on each node that redirect traffic destined for Service ClusterIPs to the appropriate backend Pod endpoints.

</details>

---

### Question 127
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

</details>

---

### Question 128
[MEDIUM]

What happens when a Service ClusterIP is accessed?

A) The request goes directly to a Pod
B) kube-proxy forwards it to a backend Pod
C) Network rules redirect traffic to an endpoint Pod
D) The API server routes the request

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** When a Pod accesses a Service ClusterIP, the kernel's netfilter (iptables) or IPVS rules installed by kube-proxy intercept the packet and redirect it to one of the backend Pod endpoint IPs using DNAT.

</details>

---

### Question 129
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

</details>

---

### Question 130
[MEDIUM]

What is the userspace mode of kube-proxy?

A) The most efficient mode
B) A legacy mode where kube-proxy acts as an actual proxy in userspace
C) A mode for user applications
D) The default mode

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Userspace mode is the original, legacy kube-proxy implementation where kube-proxy itself acts as a TCP/UDP proxy, forwarding traffic through userspace. It's significantly slower than kernel-based modes and rarely used today.

</details>

---

### Question 131
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

</details>

---

### Question 132
[MEDIUM-HARD]

What load balancing algorithms does IPVS mode support?

A) Only round-robin
B) Round-robin, least connections, destination hashing, source hashing, and more
C) Only least connections
D) Random only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** IPVS supports multiple load balancing algorithms including round-robin (rr), least connections (lc), destination hashing (dh), source hashing (sh), shortest expected delay (sed), and never queue (nq).

</details>

---

### Question 133
[MEDIUM-HARD]

Where is kube-proxy configuration typically stored?

A) In a Secret
B) In a ConfigMap in kube-system namespace
C) In /etc/kube-proxy/
D) In etcd directly

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** kube-proxy configuration is typically stored in a ConfigMap named "kube-proxy" in the kube-system namespace, which is mounted into kube-proxy Pods and contains settings like mode, cluster CIDR, and various tuning parameters.

</details>

---

### Question 134
[MEDIUM-HARD]

What happens to a Service's ClusterIP during its lifetime?

A) It remains stable; ClusterIP is immutable once assigned
B) It changes dynamically based on cluster load
C) It rotates periodically for security
D) It changes when Pods are rescheduled

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** A Service's ClusterIP is immutable once assigned and remains stable for the Service's entire lifetime. The only way to change it is to delete and recreate the Service. kube-proxy watches for Service changes and updates network rules accordingly, but the ClusterIP itself never changes without Service recreation.

</details>

---

### Question 135
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

</details>

---

### Question 136
[HARD]

In iptables mode, which iptables chain handles DNAT for Services?

A) INPUT
B) FORWARD
C) KUBE-SVC-* chains
D) OUTPUT

<details>
<summary>Show Answer</summary>

**Answer:** C

**Explanation:** In iptables mode, kube-proxy creates KUBE-SVC-* chains for each Service, which contain DNAT rules that redirect traffic from the Service ClusterIP to one of the backend Pod endpoints using probability-based load balancing.

</details>

---

### Question 137
[HARD]

What is the `--proxy-mode` flag used for?

A) To enable proxy authentication
B) To select the kube-proxy mode (iptables, ipvs, etc.)
C) To configure proxy protocols
D) To set proxy timeout

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The --proxy-mode flag specifies which kube-proxy implementation to use: "iptables" (default), "ipvs" for better performance at scale, or "nftables" as a newer alternative to iptables.

</details>

---

### Question 138
[HARD]

How does kube-proxy implement session affinity in iptables mode?

A) Using cookies
B) Using the recent match module to track client IPs
C) Session affinity is not supported in iptables mode
D) Using connection tracking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** In iptables mode, kube-proxy uses the iptables "recent" match module to track client source IPs for session affinity, maintaining a mapping that directs subsequent requests from the same client to the same backend Pod.

</details>

---

### Question 139
[HARD]

What happens to existing connections when kube-proxy updates iptables rules?

A) They are immediately terminated
B) Existing connections continue; new connections use updated rules
C) All traffic stops briefly
D) Connections are migrated

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When kube-proxy updates iptables rules, existing established connections tracked by conntrack continue to flow to their original destination, while only new connections use the updated rules, providing graceful transitions.

</details>

---

### Question 140
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

</details>

---

### Question 141
[HARD]

How can you verify what rules kube-proxy has created?

A) kubectl get iptables
B) Running iptables-save or ipvsadm on the node
C) kubectl describe kube-proxy
D) Checking the API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Running `iptables-save` (for iptables mode) or `ipvsadm -ln` (for IPVS mode) on a cluster node shows all the rules kube-proxy has created, including KUBE-SERVICES, KUBE-SVC-*, and KUBE-SEP-* chains.

</details>

---

### Question 142
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

</details>

---

### Question 143
[HARD]

What is the purpose of `healthzBindAddress` in kube-proxy config?

A) To configure health check endpoints for kube-proxy itself
B) To check Pod health
C) To configure Service health checks
D) To bind to specific node addresses

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The healthzBindAddress configures the address and port where kube-proxy exposes its health check endpoint (/healthz), which can be used by monitoring systems to verify kube-proxy is running correctly.

</details>

---

### Question 144
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

</details>

---

### Question 145
[HARD]

What is the nftables mode in kube-proxy?

A) A deprecated mode
B) A newer mode using nftables instead of iptables for better performance
C) A mode for network filtering
D) A mode specific to Windows

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** nftables mode is a newer kube-proxy implementation that uses the nftables framework (successor to iptables), offering better performance, atomic rule updates, and a cleaner rule structure than the legacy iptables mode.

</details>

---

## Advanced Networking Concepts

### Question 146
[MEDIUM]

What is the purpose of Pod CIDR?

A) To define Service IP ranges
B) To define the IP range for Pod addresses
C) To configure external IPs
D) To set node IP ranges

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Pod CIDR defines the IP address range from which Pod IP addresses are allocated, typically configured via --pod-network-cidr during cluster initialization and divided into per-node subnets.

</details>

---

### Question 147
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

</details>

---

### Question 148
[MEDIUM]

What is the Kubernetes network model requirement for Pod-to-Pod communication?

A) All Pods must use NAT
B) All Pods can reach all other Pods without NAT
C) Pods must use Services
D) Pods must be in the same namespace

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Kubernetes network model requires that all Pods can communicate with each other without NAT, meaning each Pod sees the same source IP that other Pods see, enabling transparent network communication across the cluster.

</details>

---

### Question 149
[MEDIUM-HARD]

What is a network overlay in Kubernetes?

A) A graphical network interface
B) An encapsulation technique that creates a virtual network over the physical network
C) A security layer
D) A DNS configuration

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A network overlay creates a virtual network layer on top of the physical infrastructure by encapsulating Pod traffic, allowing Pod IPs to be routed across nodes that may not have direct Layer 2 or Layer 3 connectivity.

</details>

---

### Question 150
[MEDIUM-HARD]

What is the difference between VXLAN and IPIP encapsulation?

A) VXLAN is faster
B) VXLAN encapsulates at Layer 2 (UDP), IPIP encapsulates at Layer 3
C) IPIP is more secure
D) There is no difference

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** VXLAN encapsulates Layer 2 Ethernet frames within UDP packets (port 4789), creating a full Layer 2 overlay, while IPIP simply wraps IP packets in another IP header (protocol 4), resulting in lower overhead but only providing Layer 3 connectivity.

</details>

---

### Question 151
[MEDIUM-HARD]

What is the purpose of the host network mode (`hostNetwork: true`)?

A) To isolate the Pod network
B) To share the node's network namespace with the Pod
C) To enable faster networking
D) To use the host's DNS

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When `hostNetwork: true` is set, the Pod uses the node's network namespace instead of its own isolated namespace, allowing the Pod to access network interfaces, ports, and traffic as if it were a regular process on the host.

</details>

---

### Question 152
[HARD]

What are the security implications of using hostNetwork: true?

A) None; it's the recommended approach
B) The Pod can see all network traffic on the node and bind to node ports
C) It disables network policies
D) It prevents Pod communication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Using `hostNetwork: true` gives the Pod direct access to the node's network stack, allowing it to see all network traffic, bind to any port, and potentially intercept or manipulate network communications, which poses significant security risks.

</details>

---

### Question 153
[HARD]

What is the purpose of `hostPort` in a container spec?

A) To expose the container on a specific port on the host
B) To configure the host's firewall
C) To set the container port
D) To enable host networking

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The `hostPort` field exposes a container's port directly on the node's IP address, creating a direct mapping from the node's port to the container's port, similar to Docker's port publishing but limited to the specific node where the Pod runs.

</details>

---

### Question 154
[HARD]

How does traffic flow when accessing a ClusterIP Service from a Pod on the same node as a backend Pod?

A) Always routed through an external network hop
B) kube-proxy DNATs to a backend; if the endpoint is local, traffic stays on-node
C) Through the API server
D) The CNI bypasses kube-proxy for local traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** ClusterIP traffic is always handled by kube-proxy (iptables/IPVS rules), which DNATs the Service IP to a backend Pod IP. If the selected endpoint happens to be on the same node, the traffic stays local after the NAT—but it's kube-proxy making the routing decision, not the CNI.

</details>

---

### Question 155
[HARD]

What is the purpose of `externalIPs` in a Service specification?

A) To configure external DNS
B) To expose the Service on specific external IPs routed to the cluster
C) To configure load balancer IPs
D) To set up external authentication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `externalIPs` field allows you to specify IPs that are externally routed to cluster nodes. These don't have to be actual node interface IPs—they can be any IPs your network routes to the cluster. kube-proxy installs rules to accept traffic destined for these IPs and DNAT it to the Service's backend Pods.

</details>

---

### Question 156
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

</details>

---

### Question 157
[HARD]

What is the Service topology feature (now deprecated) replaced by?

A) Endpoint slices
B) Topology-aware hints
C) Network policies
D) Service mesh

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The deprecated Service topology feature was replaced by topology-aware hints (also known as topology-aware routing), which provides a more flexible and scalable approach to routing traffic to endpoints based on their topology zone.

</details>

---

### Question 158
[HARD]

What are topology-aware hints used for?

A) To optimize routing based on network topology
B) To configure DNS
C) To set up load balancing hints
D) To define node topology

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Topology-aware hints enable kube-proxy to prefer routing traffic to endpoints in the same zone or region, reducing cross-zone network latency and costs while maintaining high availability.

</details>

---

### Question 159
[HARD]

What is the `internalTrafficPolicy` field used for?

A) To control how internal traffic is routed (Local vs Cluster)
B) To define internal security policies
C) To configure internal load balancing
D) To set internal DNS

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** The `internalTrafficPolicy` field controls whether internal cluster traffic (from Pods) is routed to all endpoints cluster-wide (Cluster) or only to endpoints on the same node (Local), similar to `externalTrafficPolicy` but for internal traffic.

</details>

---

### Question 160
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

</details>

---

## Service Mesh and Advanced Topics

### Question 161
[MEDIUM]

What is a service mesh?

A) A network of physical servers
B) An infrastructure layer for handling service-to-service communication
C) A type of CNI plugin
D) A load balancer

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A service mesh is a dedicated infrastructure layer that manages service-to-service communication, providing features like traffic management, observability, and security (mTLS) without requiring changes to application code.

</details>

---

### Question 162
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

</details>

---

### Question 163
[MEDIUM]

What is the sidecar pattern in service meshes?

A) A backup container
B) A proxy container injected alongside the application container
C) A logging container
D) A storage container

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The sidecar pattern deploys a proxy container (like Envoy) alongside each application container in a Pod, intercepting all inbound and outbound traffic to provide service mesh functionality transparently to the application.

</details>

---

### Question 164
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

</details>

---

### Question 165
[MEDIUM]

What is the data plane in a service mesh?

A) The control components
B) The sidecar proxies that handle actual traffic
C) The storage layer
D) The monitoring system

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The data plane consists of all the sidecar proxies deployed alongside application containers, which handle the actual network traffic including routing, load balancing, and applying policies at runtime.

</details>

---

### Question 166
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

</details>

---

### Question 167
[MEDIUM-HARD]

What is traffic management in service mesh?

A) Monitoring network usage
B) Controlling request routing, retries, timeouts, and traffic splitting
C) Managing bandwidth
D) Filtering malicious traffic

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Traffic management in a service mesh allows fine-grained control over how requests are routed between services, including features like traffic splitting, canary deployments, retries, timeouts, and fault injection.

</details>

---

### Question 168
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

</details>

---

### Question 169
[MEDIUM-HARD]

What is traffic mirroring (shadowing)?

A) Encrypting traffic
B) Duplicating traffic to a secondary service for testing
C) Reflecting attacks
D) Creating traffic backups

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Traffic mirroring duplicates live traffic and sends copies to a secondary service for testing or analysis without affecting the primary traffic flow, enabling safe testing of new service versions with real production traffic.

</details>

---

### Question 170
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

</details>

---

### Question 171
[HARD]

How does Istio inject sidecar proxies?

A) Manually by users
B) Using mutating admission webhooks
C) Through the CNI plugin
D) By modifying container images

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Istio uses mutating admission webhooks to automatically inject Envoy sidecar proxy containers into Pods at creation time when the namespace or Pod has the appropriate injection label enabled.

</details>

---

### Question 172
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

</details>

---

### Question 173
[HARD]

What is the VirtualService resource in Istio?

A) A virtual machine service
B) A configuration for request routing rules
C) A type of Kubernetes Service
D) A storage abstraction

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** VirtualService is an Istio CRD that defines traffic routing rules, allowing you to configure how requests are routed to services based on headers, URI paths, or percentages for canary deployments and A/B testing.

</details>

---

### Question 174
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

</details>

---

### Question 175
[HARD]

How does a service mesh handle canary deployments?

A) By modifying Deployments
B) By splitting traffic percentages between service versions
C) By using separate clusters
D) By DNS-based routing

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Service meshes enable canary deployments by routing a configurable percentage of traffic to new service versions while the majority goes to the stable version, allowing gradual rollout and quick rollback if issues are detected.

</details>

---

### Question 176
[HARD]

What is the difference between iptables-based and eBPF-based service meshes?

A) No difference
B) eBPF operates in kernel space with better performance; iptables uses netfilter
C) iptables is more modern
D) eBPF is user-space only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** eBPF-based service meshes operate directly in the Linux kernel with lower latency and overhead, while iptables-based meshes use the older netfilter framework which requires more context switches and has higher performance costs.

</details>

---

### Question 177
[HARD]

What is Cilium Service Mesh's approach compared to traditional sidecars?

A) Uses more sidecars
B) Uses eBPF to reduce or eliminate sidecar overhead
C) Uses hardware acceleration
D) Uses userspace networking

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Cilium Service Mesh uses eBPF programs running in the Linux kernel to implement service mesh features, reducing or eliminating the need for sidecar proxies and their associated resource overhead and latency.

</details>

---

### Question 178
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

</details>

---

### Question 179
[HARD]

How do service meshes handle retries and timeouts differently than application code?

A) They don't; it's the same
B) They handle it at the proxy layer, removing the need for application-level implementation
C) They use kernel-level handling
D) They require application changes

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Service meshes implement retries and timeouts at the proxy layer, making these policies consistent across all services without requiring each application to implement its own retry logic, and enabling centralized configuration and updates.

</details>

---

### Question 180
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

</details>

---

## Troubleshooting and Diagnostics

### Question 181
[MEDIUM]

What command can you use to test connectivity to a Service from within a Pod?

A) kubectl connect
B) curl or wget to the Service name/IP
C) kubectl test-connection
D) ping only

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Using curl or wget from within a Pod allows you to test HTTP connectivity to a Service by its DNS name or ClusterIP, verifying that the Service is reachable and responding correctly.

</details>

---

### Question 182
[MEDIUM]

How can you check if a Service has endpoints?

A) kubectl get endpoints <service-name>
B) kubectl describe pod
C) kubectl logs
D) kubectl get nodes

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Running `kubectl get endpoints <service-name>` displays the IP addresses and ports of all Pods currently selected by the Service, making it easy to verify whether the Service has any backend targets.

</details>

---

### Question 183
[MEDIUM]

What might cause a Service to have no endpoints?

A) The Service is too new
B) No Pods match the Service's selector or Pods aren't ready
C) The cluster is overloaded
D) DNS is not configured

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A Service will have no endpoints if no Pods match the Service's label selector, if matching Pods exist but their readiness probes are failing, or if matching Pods are in a terminating state.

</details>

---

### Question 184
[MEDIUM]

What tool can you use to debug DNS resolution in a Pod?

A) kubectl dns-debug
B) nslookup, dig, or host commands from within the Pod
C) kubectl describe dns
D) The Kubernetes dashboard

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DNS debugging tools like nslookup, dig, or host can be run from within a Pod (using kubectl exec) to test whether DNS resolution for Service names is working correctly through CoreDNS.

</details>

---

### Question 185
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

</details>

---

### Question 186
[MEDIUM-HARD]

What might cause DNS resolution to fail for Services?

A) Service doesn't exist
B) CoreDNS Pods are not running or misconfigured
C) Too many Services
D) Node is overloaded

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** DNS resolution failures typically occur when CoreDNS Pods are not running, have crashed, are misconfigured, or cannot reach the Kubernetes API to get Service/Endpoints information.

</details>

---

### Question 187
[MEDIUM-HARD]

How can you test network policies are working correctly?

A) kubectl describe networkpolicy
B) Attempting connections from allowed and denied sources
C) kubectl get networkpolicy
D) Checking the API server logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The most effective way to test network policies is to attempt actual connections from Pods that should be allowed and from Pods that should be denied, verifying the policy behaves as expected in practice.

</details>

---

### Question 188
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

</details>

---

### Question 189
[MEDIUM-HARD]

How can you capture network traffic from a Pod?

A) kubectl capture
B) Using tcpdump in the Pod or a debug container
C) From the Kubernetes dashboard
D) Using kubectl logs

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Network traffic can be captured using tcpdump either directly in the Pod container (if available) or by attaching an ephemeral debug container with tcpdump to inspect packets at the network interface level.

</details>

---

### Question 190
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

</details>

---

### Question 191
[HARD]

How can you diagnose iptables-related networking issues?

A) kubectl describe iptables
B) Running iptables -L -n -v on the node and checking KUBE-* chains
C) Checking CoreDNS logs
D) Using kubectl debug

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Diagnosing iptables issues requires running `iptables -L -n -v` on the node to examine the KUBE-SERVICES, KUBE-SVC-*, and KUBE-SEP-* chains that kube-proxy creates for Service routing.

</details>

---

### Question 192
[HARD]

What tool can help visualize network policies in a cluster?

A) kubectl visualize
B) Tools like Cilium's Hubble, NetworkPolicy Editor, or similar visualization tools
C) The Kubernetes dashboard
D) kube-proxy

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Tools like Cilium's Hubble provide real-time network flow visualization, while web-based NetworkPolicy editors can help visualize and validate policy configurations before applying them to the cluster.

</details>

---

### Question 193
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

</details>

---

### Question 194
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

</details>

---

### Question 195
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

</details>

---

### Question 196
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

</details>

---

### Question 197
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

</details>

---

### Question 198
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

</details>

---

### Question 199
[HARD]

How can you verify that the CNI plugin is functioning correctly?

A) kubectl get cni
B) Check CNI Pod logs, verify Pod IP assignment, and test Pod connectivity
C) kubectl describe cni
D) Check the API server

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Verifying CNI functionality involves checking CNI Pod logs for errors, confirming that new Pods receive IP addresses from the expected range, and testing basic Pod-to-Pod connectivity across nodes.

</details>

---

### Question 200
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

</details>

---
