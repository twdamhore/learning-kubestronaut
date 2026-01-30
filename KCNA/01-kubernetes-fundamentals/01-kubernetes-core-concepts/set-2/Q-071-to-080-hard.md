# Kubernetes Core Concepts - Q71-Q80 [Hard]

**Domain:** Kubernetes Fundamentals (46%)
**Competency:** Kubernetes Core Concepts
**Set:** 2
**Difficulty:** Hard
**Questions:** Q71-Q80

---

### Question 71
[HARD]

A team is deploying a distributed database (such as Cassandra) on Kubernetes using a StatefulSet. Each database node must be individually addressable by other nodes in the cluster for peer-to-peer replication. The team creates a Service but finds that the Service's single ClusterIP does not meet their needs. What type of Service should they create, and what is the key characteristic that enables individual Pod addressing?

A) A LoadBalancer Service, which assigns an external IP to each Pod individually
B) A headless Service with `clusterIP: None`, which causes DNS to return A records for each individual Pod IP instead of a single virtual IP
C) A NodePort Service, which maps a unique port on each node directly to a specific Pod
D) A ClusterIP Service with `publishNotReadyAddresses: true`, which exposes all Pod IPs through the single ClusterIP

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** A headless Service is created by setting `clusterIP: None` in the Service spec. Unlike a standard ClusterIP Service that provides a single virtual IP with kube-proxy load balancing, a headless Service causes the Kubernetes DNS server to return individual A records for each backing Pod. When combined with a StatefulSet, this creates predictable DNS entries in the form `<pod-name>.<service-name>.<namespace>.svc.cluster.local`, enabling direct peer-to-peer communication. This is essential for stateful workloads like databases where each node must be individually reachable.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#headless-services

</details>

---

### Question 72
[HARD]

A company is migrating from on-premises to Kubernetes. During the transition, some services still run outside the cluster on legacy infrastructure at `legacy-api.corp.example.com`. The team wants Kubernetes Pods to access this external service using a consistent in-cluster DNS name (`legacy-api.prod.svc.cluster.local`) without creating proxy Pods. Which approach achieves this?

A) Create a ClusterIP Service with a selector matching legacy-api labels and manually add Endpoints
B) Create an ExternalName Service that sets `type: ExternalName` and `externalName: legacy-api.corp.example.com`, which returns a DNS CNAME record
C) Create an Ingress resource with a backend pointing to the external hostname
D) Create a headless Service and add the external server's IP to the EndpointSlice manually

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** An ExternalName Service maps a Service name to a DNS CNAME record rather than to a set of Pod IPs. When a Pod queries `legacy-api.prod.svc.cluster.local`, the cluster DNS returns a CNAME record pointing to `legacy-api.corp.example.com`, which the client then resolves through normal DNS resolution. No proxying or forwarding occurs at the network level -- it is purely a DNS-level redirection. This makes it ideal for bridging in-cluster service discovery to external endpoints during migrations. Option D would work for IP-based access but the question specifies a hostname-based external service and asks for no proxy Pods.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#externalname

</details>

---

### Question 73
[HARD]

A platform engineer is troubleshooting a large Kubernetes cluster with a Service that has 5,000 backing Pods. They notice that updates to the Endpoints object are causing significant load on the API server and etcd because every Pod addition or removal rewrites the entire Endpoints object. Which Kubernetes resource was introduced to address this scalability problem, and how does it solve the issue?

A) EndpointSlices, which partition endpoints into smaller chunks (default 100 endpoints per slice), so that changes to individual Pods only trigger updates to the affected slice rather than the entire set
B) ServiceTopology, which limits endpoint visibility to only same-zone Pods, reducing the total object size
C) InternalTrafficPolicy, which restricts traffic to node-local endpoints and avoids creating cross-node endpoint entries
D) EndpointSlices, which cache endpoint data locally on each node so that the API server is never queried for endpoint information

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** EndpointSlices were introduced to address the scalability limitations of the Endpoints API. A single Endpoints object stores all IP addresses for a Service, meaning any change (such as adding or removing a Pod) requires the entire object to be rewritten and transmitted to all watching nodes. EndpointSlices break this data into smaller, manageable pieces (each holding up to 100 endpoints by default), so a single Pod change only requires updating the specific slice containing that endpoint. This dramatically reduces API server and etcd load in large clusters. The data is still served by the API server -- it is not cached locally to bypass the API server.

**Source:** https://kubernetes.io/docs/concepts/services-networking/endpoint-slices/

</details>

---

### Question 74
[HARD]

A cluster administrator is evaluating kube-proxy modes for a new cluster that will host over 10,000 Services. They need the best possible performance for rule lookup when routing traffic. The current default mode uses iptables. What is the key performance advantage of switching to IPVS mode in this scenario?

A) IPVS mode bypasses the kernel entirely and processes packets in userspace, which is faster for high Service counts
B) IPVS mode uses hash-based data structures in the kernel for O(1) connection routing lookups, whereas iptables uses sequential chain traversal with O(n) complexity as rules grow
C) IPVS mode eliminates the need for kube-proxy entirely by offloading all routing decisions to the API server
D) IPVS mode compresses iptables rules into a single consolidated rule, reducing memory usage but maintaining the same lookup mechanism

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** IPVS (IP Virtual Server) mode uses hash tables in the Linux kernel for storing and looking up Service-to-endpoint mappings, providing O(1) time complexity for connection routing regardless of the number of Services. In contrast, iptables mode creates a linear chain of rules that must be traversed sequentially, resulting in O(n) lookup complexity that degrades as the number of Services increases. For clusters with thousands of Services, this difference becomes significant. Both modes operate in kernel space -- IPVS does not use userspace processing. Additionally, IPVS supports multiple load balancing algorithms (round-robin, least connections, etc.) that iptables mode does not natively offer.

**Source:** https://kubernetes.io/docs/reference/networking/virtual-ips/#proxy-mode-ipvs

</details>

---

### Question 75
[HARD]

A developer creates a Pod with a custom `/etc/resolv.conf` configuration by setting `dnsPolicy: None` and providing `dnsConfig` with specific nameservers. However, their colleague's Pod uses the default `dnsPolicy: ClusterFirst`. The colleague's Pod can resolve both in-cluster Service names and external hostnames. What happens differently when the first developer's Pod tries to resolve an in-cluster Service name like `my-svc.default.svc.cluster.local`?

A) The resolution succeeds because all Pods automatically inherit cluster DNS regardless of dnsPolicy
B) The resolution fails because `dnsPolicy: None` requires the Pod to explicitly include the cluster DNS server IP in its `dnsConfig` nameservers; without it, only the custom nameservers are used
C) The resolution succeeds because `dnsPolicy: None` still prepends the cluster DNS server before the custom nameservers
D) The resolution fails because `dnsPolicy: None` disables all DNS resolution entirely and no nameservers are configured

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** When `dnsPolicy` is set to `None`, Kubernetes does not inject any DNS configuration automatically -- the Pod's DNS settings are entirely determined by the `dnsConfig` field. If the developer does not explicitly include the cluster DNS server (typically CoreDNS at an IP like `10.96.0.10`) in the `dnsConfig.nameservers` list, the Pod will have no way to resolve in-cluster Service DNS names. In contrast, `ClusterFirst` (the default) configures the Pod's `/etc/resolv.conf` to point to the cluster DNS server, which resolves in-cluster names first and forwards external queries upstream. `dnsPolicy: None` does not disable DNS entirely -- it simply gives full control to the user via `dnsConfig`.

**Source:** https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/#pod-s-dns-policy

</details>

---

### Question 76
[HARD]

A team is debugging why a newly deployed Pod cannot discover a Service called `backend` in the same Namespace. The Pod was created before the `backend` Service existed. The Pod's application relies on environment variables (not DNS) for service discovery. After the Service is created, the Pod still cannot find `BACKEND_SERVICE_HOST`. What is the root cause, and what would fix it?

A) Environment variable-based service discovery is deprecated and no longer injected; switch to DNS-based discovery
B) Service environment variables are only injected into Pods at creation time; since the Pod was created before the Service, it lacks the variables -- the Pod must be recreated or the application should use DNS instead
C) Environment variables are only injected for Services of type LoadBalancer; the team should change the Service type
D) The environment variables use the format `SVC_BACKEND_HOST` not `BACKEND_SERVICE_HOST`; the Pod has the variables but the application is using the wrong name

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Kubernetes injects environment variables for active Services into a Pod only at the time the Pod is created. If the Service does not exist when the Pod starts, the corresponding `{SVCNAME}_SERVICE_HOST` and `{SVCNAME}_SERVICE_PORT` environment variables are never set. This is a key limitation of environment variable-based service discovery -- it requires Services to exist before the Pods that depend on them. DNS-based discovery does not have this ordering constraint because DNS lookups happen at runtime. Recreating the Pod after the Service exists would also resolve the issue, as the new Pod would receive the injected variables at startup.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#environment-variables

</details>

---

### Question 77
[HARD]

A platform team needs to expose multiple HTTP-based microservices externally. They want path-based routing (`/api` to one service, `/web` to another), TLS termination at the edge, and host-based virtual hosting -- all through a single external IP. A colleague suggests using individual LoadBalancer Services per microservice. Why is an Ingress resource with an Ingress controller a better architectural choice in this scenario?

A) Ingress operates at L4 (TCP/UDP) and is more efficient than LoadBalancer Services which operate at L7
B) Ingress operates at L7 (HTTP/HTTPS) and can perform path-based routing, host-based routing, and TLS termination through a single entry point, whereas each LoadBalancer Service operates at L4, requires a separate external IP, and cannot perform content-based routing
C) Ingress eliminates the need for Services entirely by routing traffic directly to Pod IPs
D) Ingress automatically provisions SSL certificates from Let's Encrypt, while LoadBalancer Services cannot use TLS at all

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** Ingress resources operate at Layer 7 (the application layer) and provide HTTP-aware features such as path-based routing, host-based virtual hosting, and TLS termination. A single Ingress can consolidate routing for many backend Services behind one external IP address. In contrast, LoadBalancer Services typically operate at Layer 4, meaning each Service gets its own external IP and cannot make routing decisions based on HTTP paths or hostnames. Using individual LoadBalancer Services for each microservice is wasteful (one external IP per service) and lacks the content-based routing flexibility that Ingress provides. Note that Ingress still routes to backend Services -- it does not bypass them.

**Source:** https://kubernetes.io/docs/concepts/services-networking/ingress/

</details>

---

### Question 78
[HARD]

A developer creates a Service of type NodePort but does not specify a `nodePort` value in the spec. The Service is successfully created. Later, they attempt to create another NodePort Service and explicitly set `nodePort: 25000`. This second creation fails. What is the most likely reason for the failure?

A) NodePort Services are limited to one per Namespace, and one already exists
B) Port 25000 falls outside the default NodePort range of 30000-32767, and the cluster's `--service-node-port-range` has not been modified
C) NodePort values must be even numbers, and 25000 is even but reserved for system use
D) The first Service already consumed the maximum number of NodePort allocations allowed per node

<details>
<summary>Show Answer</summary>

**Answer:** B

**Explanation:** By default, Kubernetes allocates NodePort values from the range 30000-32767 (configurable via the `--service-node-port-range` flag on the API server). When no `nodePort` is specified, Kubernetes automatically selects an available port within this range. When a port is explicitly specified, it must fall within the configured range. Port 25000 is below the default lower bound of 30000, so the API server rejects the request. There is no limit of one NodePort Service per Namespace, and port parity is not a constraint. The administrator would need to reconfigure the API server's `--service-node-port-range` to include 25000 if that specific port is required.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport

</details>

---

### Question 79
[HARD]

A team runs a legacy web application that stores session data in-memory on the server. They deploy it as multiple Pod replicas behind a ClusterIP Service. Users report being intermittently logged out because their requests land on different Pods that do not share session state. Without modifying the application, which Kubernetes-native Service configuration can mitigate this issue, and what is its limitation?

A) Set `service.spec.sessionAffinity: ClientIP`, which configures the Service to route all requests from the same client IP to the same Pod; the limitation is that it does not work if clients are behind a shared NAT gateway
B) Set `service.spec.loadBalancerPolicy: sticky`, which pins each user session to a Pod; the limitation is it only works with LoadBalancer type Services
C) Set `service.spec.externalTrafficPolicy: Local`, which ensures all traffic stays on the same node; the limitation is it only applies to external traffic
D) Set `service.spec.sessionAffinity: Cookie`, which uses HTTP cookies for session pinning; the limitation is it requires an Ingress controller

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** Kubernetes Services support `sessionAffinity: ClientIP`, which ensures that requests from the same client IP address are consistently routed to the same backend Pod for a configurable timeout period (default 10800 seconds / 3 hours). This is the only session affinity mechanism natively supported by Kubernetes Services. The key limitation is that it relies on the source IP address -- if multiple users share the same IP (as is common behind corporate NAT gateways or load balancers), they will all be pinned to the same Pod. Kubernetes Services do not support cookie-based session affinity; that feature is available through some Ingress controllers but not at the Service level.

**Source:** https://kubernetes.io/docs/reference/networking/virtual-ips/#session-affinity

</details>

---

### Question 80
[HARD]

A team defines a Service with two ports -- one named `http` on port 80 and another named `metrics` on port 9090. During a rolling update of the Deployment, the new Pod version changes the `http` container port from 8080 to 8081 while keeping the `metrics` port unchanged. The Service uses `targetPort: http` (referencing the port by name) instead of `targetPort: 8080`. Why does referencing the port by name instead of by number matter during this rolling update?

A) Named ports allow the Service to route traffic to different container port numbers on old Pods (8080) and new Pods (8081) simultaneously during the rollout, because each Pod's named port resolves to its own containerPort value
B) Named ports are required by Kubernetes for any Service with more than one port definition, but they have no functional impact on rolling updates
C) Named ports cause kube-proxy to skip the old Pods entirely and route all traffic to the new Pods immediately
D) Named ports trigger an automatic Service reload that updates the targetPort number atomically across all Pods

<details>
<summary>Show Answer</summary>

**Answer:** A

**Explanation:** When a Service uses a named `targetPort` (e.g., `targetPort: http`), Kubernetes resolves that name to the actual container port number defined in each individual Pod's spec. During a rolling update, both old Pods (with `containerPort: 8080` named `http`) and new Pods (with `containerPort: 8081` named `http`) coexist. The Service correctly routes traffic to port 8080 on old Pods and port 8081 on new Pods because the name `http` resolves per-Pod. If the Service had used `targetPort: 8080` (a hardcoded number), traffic to new Pods would fail because they no longer listen on 8080. Named ports decouple the Service definition from specific port numbers, enabling safe port changes during rolling updates.

**Source:** https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports

</details>
