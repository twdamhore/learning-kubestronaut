# Networking - 100 MCQ Questions (Part A)

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

### Question 3
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

### Question 4
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

### Question 5
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

### Question 6
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

### Question 7
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

### Question 8
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

### Question 9
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

### Question 10
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

### Question 11
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

### Question 12
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

### Question 13
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

### Question 14
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

### Question 15
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

### Question 16
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

### Question 17
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

### Question 18
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

### Question 19
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

### Question 20
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

### Question 21
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

### Question 22
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

### Question 23
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

### Question 24
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

### Question 25
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

### Question 26
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

### Question 27
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

### Question 28
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

## Kubernetes Services - ExternalName and Headless

### Question 29
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

### Question 30
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

### Question 31
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

### Question 32
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

### Question 33
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

### Question 34
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

### Question 35
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

### Question 36
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

### Question 37
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

### Question 38
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

### Question 39
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

### Question 40
[HARD]

What happens when multiple Ingress rules match the same host and path?

A) All rules are applied simultaneously
B) Behavior is controller-specific; the Ingress spec does not define precedence
C) The Kubernetes API rejects duplicate rules
D) An error occurs and no traffic is routed

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The Ingress specification does not define how controllers should handle overlapping rules. Different Ingress controllers implement their own precedence logic--many use longest path match, some use creation timestamp, others use alphabetical ordering. Always consult your specific Ingress controller's documentation for conflict resolution behavior.

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 41
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

### Question 42
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

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 43
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

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

### Question 44
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

**Source:** [Ingress | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/ingress/)

</details>

---

## Network Policies

### Question 45
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 46
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 47
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 48
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 49
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 50
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 51
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 52
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 53
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 54
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

## DNS in Kubernetes

### Question 55
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 56
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 57
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 58
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 59
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 60
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 61
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 62
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 63
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 64
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

### Question 65
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

**Source:** [DNS for Services and Pods | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)

</details>

---

## kube-proxy and Service Discovery

### Question 66
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 67
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 68
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 69
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 70
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

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 71
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 72
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 73
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 74
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 75
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 76
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

## Advanced Networking Concepts

### Question 77
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 78
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 79
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 80
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 81
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 82
[HARD]

What is the purpose of `externalIPs` in a Service specification?

A) To configure external DNS
B) To expose the Service on specific external IPs routed to the cluster
C) To configure load balancer IPs
D) To set up external authentication

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** The `externalIPs` field allows you to specify IPs that are externally routed to cluster nodes. These don't have to be actual node interface IPs--they can be any IPs your network routes to the cluster. kube-proxy installs rules to accept traffic destined for these IPs and DNAT it to the Service's backend Pods.

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 83
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

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

### Question 84
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

**Source:** [Service | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/)

</details>

---

## Service Mesh and Advanced Topics

### Question 85
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 86
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 87
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 88
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 89
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 90
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 91
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 92
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 93
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

### Question 94
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

**Source:** [Cluster Networking | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

</details>

---

## Troubleshooting and Diagnostics

### Question 95
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

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 96
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

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 97
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

**Source:** [Network Policies | Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

</details>

---

### Question 98
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

**Source:** [Debug Services | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)

</details>

---

### Question 99
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

**Source:** [Virtual IPs and Service Proxies | Kubernetes](https://kubernetes.io/docs/reference/networking/virtual-ips/)

</details>

---

### Question 100
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

**Source:** [Network Plugins | Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

</details>

---
