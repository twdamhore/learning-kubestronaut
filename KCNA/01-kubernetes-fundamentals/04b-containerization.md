# KCNA Containerization MCQs

## Container Fundamentals

### Question 1
Which technology provides the foundation for container isolation in Linux?

A) Virtual machines and hypervisors
B) Namespaces and cgroups
C) Firewalls and network segmentation
D) File system encryption

<details><summary>Answer</summary>

**B) Namespaces and cgroups**

Linux namespaces provide isolation of system resources (PID, network, mount, user, etc.) while cgroups (control groups) limit and account for resource usage (CPU, memory, I/O). Together, these kernel features form the foundation of container technology, enabling process isolation without the overhead of full virtualization.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 2
Which Linux kernel feature allows containers to have isolated views of system resources like PIDs and network interfaces?

A) cgroups
B) Namespaces
C) SELinux
D) AppArmor

<details><summary>Answer</summary>

**B) Namespaces**

Linux namespaces provide isolated views of system resources. There are several namespace types: PID (process IDs), NET (network interfaces), MNT (mount points), UTS (hostname), IPC (inter-process communication), and USER (user IDs). Each container can have its own isolated view of these resources. Cgroups, by contrast, limit resource usage rather than provide isolation.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 3
How are container image layers structured?

A) As a single monolithic file
B) As a stack of read-only layers with a writable layer on top
C) As separate executable files
D) As encrypted partitions

<details><summary>Answer</summary>

**B) As a stack of read-only layers with a writable layer on top**

Container images use a union file system with stacked layers. Each layer represents a set of filesystem changes (added, modified, or deleted files). The layers are read-only, and when a container runs, a thin writable layer is added on top for runtime changes. This layered approach enables efficient storage and sharing of common base layers.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 4
What is the purpose of a container runtime?

A) To compile container applications
B) To manage the lifecycle of containers including creation, running, and deletion
C) To design container images
D) To monitor network traffic

<details><summary>Answer</summary>

**B) To manage the lifecycle of containers including creation, running, and deletion**

A container runtime is software responsible for running containers. It handles pulling images, creating container instances, managing their lifecycle (start, stop, restart, delete), and interacting with the kernel for isolation and resource management. Examples include containerd, CRI-O, and runc.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

### Question 5
What is the Container Runtime Interface (CRI) in Kubernetes?

A) A graphical interface for managing containers
B) A plugin interface that allows kubelet to use different container runtimes
C) A container image format
D) A network protocol for container communication

<details><summary>Answer</summary>

**B) A plugin interface that allows kubelet to use different container runtimes**

CRI is a plugin interface that enables the kubelet to work with any container runtime that implements the interface. It uses gRPC for communication and defines operations like pulling images, creating/starting/stopping containers. This abstraction allows Kubernetes to support multiple runtimes (containerd, CRI-O) without code changes.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

## Container Runtimes

### Question 6
What is containerd?

A) A container orchestration platform
B) An industry-standard container runtime focused on simplicity and portability
C) A container image registry
D) A Kubernetes distribution

<details><summary>Answer</summary>

**B) An industry-standard container runtime focused on simplicity and portability**

containerd is a CNCF graduated project that serves as an industry-standard container runtime. It manages the complete container lifecycle including image transfer, container execution, and storage. Originally part of Docker, it was extracted as a standalone runtime and is now used by Docker, Kubernetes, and other platforms.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

### Question 7
What is the relationship between Docker and containerd?

A) Docker and containerd are completely separate projects
B) containerd was extracted from Docker and is now used as Docker's core runtime
C) Docker is a plugin for containerd
D) containerd replaced Docker entirely

<details><summary>Answer</summary>

**B) containerd was extracted from Docker and is now used as Docker's core runtime**

containerd was originally developed as part of Docker and was later extracted as a standalone project donated to the CNCF. Docker Engine still uses containerd as its core container runtime. When you run `docker run`, Docker uses containerd to actually run the container, which in turn uses runc.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

### Question 8
What is runc?

A) A container orchestration tool
B) A low-level container runtime that implements the OCI runtime specification
C) A container registry
D) A container networking plugin

<details><summary>Answer</summary>

**B) A low-level container runtime that implements the OCI runtime specification**

runc is a lightweight, low-level container runtime that spawns and runs containers according to the OCI Runtime Specification. It's the reference implementation of the OCI runtime spec and is used by higher-level runtimes like containerd and CRI-O to actually create and run containers.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

### Question 9
Which OCI specification defines how to run a container?

A) Image Specification
B) Runtime Specification
C) Distribution Specification
D) Network Specification

<details><summary>Answer</summary>

**B) Runtime Specification**

The OCI Runtime Specification defines how to run a "filesystem bundle" that is unpacked from an image. It specifies the configuration, execution environment, and lifecycle of a container. runc is the reference implementation of this specification.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

### Question 10
How does Kubernetes communicate with container runtimes?

A) Through direct API calls to Docker
B) Through the Container Runtime Interface (CRI) using gRPC
C) Through REST APIs
D) Through shared file systems

<details><summary>Answer</summary>

**B) Through the Container Runtime Interface (CRI) using gRPC**

Kubernetes uses CRI to communicate with container runtimes. The kubelet makes gRPC calls to the runtime through the CRI interface, which defines operations for managing images and containers. This abstraction allows Kubernetes to work with any CRI-compliant runtime without modification.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

## Container Images and Registries

### Question 11
Which of the following is the default container registry for Docker images?

A) Google Container Registry
B) Amazon ECR
C) Docker Hub
D) Quay.io

<details><summary>Answer</summary>

**C) Docker Hub**

Docker Hub is the default public registry for Docker images. When you pull an image without specifying a registry (e.g., `nginx`), Docker automatically looks for it on Docker Hub. It hosts millions of public images and also offers private repositories.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 12
What does the 'latest' tag signify for a container image?

A) The most recently pushed image to the repository
B) The most stable version of the image
C) The image with the highest version number
D) Simply a tag name with no special meaning guaranteed

<details><summary>Answer</summary>

**D) Simply a tag name with no special meaning guaranteed**

The 'latest' tag has no special meaning in registries - it's just a conventional tag name. It doesn't automatically point to the newest image; it only updates when someone explicitly tags an image as 'latest'. Many assume it means the most recent version, but this is not guaranteed, which is why using specific version tags is recommended.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 13
Why are image digests preferred over tags for production deployments?

A) Digests are shorter and easier to remember
B) Digests are immutable and guarantee the exact same image content
C) Digests allow for automatic updates
D) Digests are required by Kubernetes

<details><summary>Answer</summary>

**B) Digests are immutable and guarantee the exact same image content**

Digests are preferred in production because they're immutable - the same digest always refers to the exact same image content. Tags can be changed to point to different images, which could cause unexpected behavior or security issues. Using digests ensures reproducibility and prevents supply chain attacks.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 14
How does Kubernetes authenticate to private container registries?

A) Using SSH keys stored in Pods
B) Using imagePullSecrets referenced in Pod specifications
C) Through automatic cloud provider integration only
D) Private registries are not supported

<details><summary>Answer</summary>

**B) Using imagePullSecrets referenced in Pod specifications**

Kubernetes authenticates to private registries using imagePullSecrets, which reference Kubernetes Secrets containing registry credentials. These secrets are attached to Pods or ServiceAccounts. Cloud providers may also offer automatic authentication through workload identity or instance metadata.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 15
Which field in a Pod spec references credentials for pulling private images?

A) registryCredentials
B) imageSecrets
C) imagePullSecrets
D) pullCredentials

<details><summary>Answer</summary>

**C) imagePullSecrets**

The `imagePullSecrets` field in a Pod spec is an array of references to Secrets containing registry credentials. It can also be configured on a ServiceAccount to automatically apply to all Pods using that ServiceAccount.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 16
When is an image pulled if imagePullPolicy is set to 'IfNotPresent'?

A) Always, on every Pod start
B) Only if the image is not already present on the node
C) Never, images must be pre-loaded
D) Only during cluster initialization

<details><summary>Answer</summary>

**B) Only if the image is not already present on the node**

With `IfNotPresent`, the kubelet checks if the image exists locally before pulling. If cached, the local image is used; if not, it's pulled from the registry. This is the default policy for images with specific tags (not `latest`) and improves startup time.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 17
What happens when imagePullPolicy is set to 'Never'?

A) The image is pulled on every Pod start
B) The kubelet never pulls the image and uses only locally available images
C) The Pod fails if the image is not cached
D) Both B and C are correct

<details><summary>Answer</summary>

**D) Both B and C are correct**

With `imagePullPolicy: Never`, the kubelet never attempts to pull the image from a registry. It only uses images that already exist locally on the node. If the image isn't present, the container fails with an ErrImageNeverPull error. This is useful for air-gapped environments or when using pre-loaded images.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

## Building Container Images

### Question 18
What is a Dockerfile?

A) A running container configuration
B) A text file containing instructions for building a container image
C) A container log file
D) A registry configuration file

<details><summary>Answer</summary>

**B) A text file containing instructions for building a container image**

A Dockerfile is a text file containing a series of instructions for building a container image. Each instruction (FROM, RUN, COPY, etc.) creates a layer in the image. Docker reads the Dockerfile and executes the instructions sequentially to produce the final image.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 19
What is the purpose of the RUN instruction in a Dockerfile?

A) To start the container
B) To execute commands during the image build process
C) To define the container's entry point
D) To copy files into the image

<details><summary>Answer</summary>

**B) To execute commands during the image build process**

The RUN instruction executes commands in a new layer on top of the current image and commits the results. It's commonly used to install packages, download files, or configure the environment. Each RUN instruction creates a new layer in the image.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 20
What is the purpose of the ENTRYPOINT instruction?

A) To set the working directory
B) To configure the container to run as an executable
C) To expose network ports
D) To define environment variables

<details><summary>Answer</summary>

**B) To configure the container to run as an executable**

ENTRYPOINT configures the container to run as an executable, defining the main command that runs when the container starts. Unlike CMD, ENTRYPOINT arguments are not easily overridden at runtime (you need `--entrypoint` flag). It's typically used to set the main application or script to run.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 21
What happens when both ENTRYPOINT and CMD are specified?

A) CMD is ignored
B) ENTRYPOINT is ignored
C) CMD provides default arguments to ENTRYPOINT
D) The build fails

<details><summary>Answer</summary>

**C) CMD provides default arguments to ENTRYPOINT**

When both ENTRYPOINT and CMD are specified, the CMD values are appended to the ENTRYPOINT as default arguments. For example, `ENTRYPOINT ["python"]` with `CMD ["app.py"]` results in running `python app.py`. Runtime arguments replace CMD but not ENTRYPOINT.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 22
How does the ENV instruction work in a Dockerfile?

A) It sets environment variables that persist in the built image
B) It only sets variables during build time
C) It encrypts sensitive data
D) It imports environment from the host

<details><summary>Answer</summary>

**A) It sets environment variables that persist in the built image**

ENV sets environment variables that are available both during the build process and when the container runs. These variables persist in the final image and can be overridden at runtime using `-e` or `--env`. Common uses include setting application configuration, paths, and versions.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 23
What is the primary benefit of multi-stage builds?

A) Faster build times
B) Smaller final images by excluding build tools and dependencies
C) Better security through encryption
D) Automatic versioning

<details><summary>Answer</summary>

**B) Smaller final images by excluding build tools and dependencies**

Multi-stage builds produce smaller final images by separating the build environment from the runtime environment. Build tools, compilers, and intermediate files stay in the build stage and are not included in the final image. Only the compiled artifacts are copied to a minimal runtime image.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 24
How does ARG differ from ENV in a Dockerfile?

A) ARG values persist in the final image, ENV values do not
B) ARG is available only during build, ENV persists in the running container
C) They are interchangeable
D) ARG is for secrets, ENV is for configuration

<details><summary>Answer</summary>

**B) ARG is available only during build, ENV persists in the running container**

ARG values are only available during the image build process and are not saved in the final image. ENV values persist in the built image and are available both during build and at container runtime. If you need a build-time value at runtime, you can use `ENV VAR=${ARG_VAR}` to transfer it.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 25
What is a .dockerignore file used for?

A) To list images that should not be pulled
B) To exclude files and directories from the build context
C) To ignore certain Dockerfile instructions
D) To prevent container execution

<details><summary>Answer</summary>

**B) To exclude files and directories from the build context**

A .dockerignore file specifies patterns for files and directories that should be excluded from the build context sent to the Docker daemon. This speeds up builds, reduces image size, and prevents sensitive files (like .git, node_modules, or secrets) from accidentally being included in images.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

## Container Image Best Practices

### Question 26
What is the recommended practice for base image selection?

A) Always use the largest image for completeness
B) Use official, minimal, and regularly updated base images
C) Build base images from scratch for every project
D) Use the same base image for all applications

<details><summary>Answer</summary>

**B) Use official, minimal, and regularly updated base images**

Best practice is to use official images from trusted sources that are minimal (smaller attack surface) and regularly updated with security patches. Examples include official language runtime images, Alpine-based images, or distroless images. This reduces vulnerabilities and image size.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 27
What is a distroless container image?

A) An image without any operating system
B) An image containing only the application and its runtime dependencies, without package managers or shells
C) An image that works on any Linux distribution
D) An uncompressed image format

<details><summary>Answer</summary>

**B) An image containing only the application and its runtime dependencies, without package managers or shells**

Distroless images (from Google) contain only the application and its necessary runtime dependencies. They exclude package managers, shells, and other OS utilities. This significantly reduces attack surface - attackers can't use common tools even if they compromise the container.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 28
Why should you avoid running containers as root?

A) Root containers are slower
B) It minimizes the potential damage from container breakout or compromise
C) Root is not supported in Kubernetes
D) Root containers use more memory

<details><summary>Answer</summary>

**B) It minimizes the potential damage from container breakout or compromise**

Running as root inside a container means if an attacker compromises the container, they have root privileges. If there's a container escape vulnerability, they could get root on the host. Running as non-root follows the principle of least privilege and limits potential damage.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 29
What is the purpose of the USER instruction in a Dockerfile?

A) To authenticate with a registry
B) To set the user (and optionally group) for running subsequent instructions and the container
C) To create user directories
D) To set file permissions

<details><summary>Answer</summary>

**B) To set the user (and optionally group) for running subsequent instructions and the container**

The USER instruction sets the user (and optionally group) for subsequent RUN, CMD, and ENTRYPOINT instructions, and for the running container. Format: `USER username` or `USER uid:gid`. The user must already exist in the image.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 30
What is the recommended approach for handling secrets in containers?

A) Embed them in environment variables in the Dockerfile
B) Use Kubernetes Secrets or external secret management systems
C) Store them in a ConfigMap
D) Include them in the image with encryption

<details><summary>Answer</summary>

**B) Use Kubernetes Secrets or external secret management systems**

Secrets should be injected at runtime, not built into images. Use Kubernetes Secrets (mounted as volumes or environment variables), or external systems like HashiCorp Vault, AWS Secrets Manager, or Azure Key Vault. This keeps secrets separate from images and allows rotation without rebuilding.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 31
What is container image scanning?

A) Converting images to different formats
B) Analyzing images for known vulnerabilities, misconfigurations, and compliance issues
C) Compressing image layers
D) Validating image signatures

<details><summary>Answer</summary>

**B) Analyzing images for known vulnerabilities, misconfigurations, and compliance issues**

Image scanning examines container images to identify known vulnerabilities (CVEs) in OS packages and application dependencies, detect misconfigurations, check for secrets, and verify compliance with security policies. It's a critical part of container security and shift-left security practices.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 32
What tool does Kubernetes use for image signature verification?

A) Docker Content Trust
B) Notary
C) Sigstore/cosign with policy controllers like Kyverno or OPA Gatekeeper
D) GPG

<details><summary>Answer</summary>

**C) Sigstore/cosign with policy controllers like Kyverno or OPA Gatekeeper**

Kubernetes doesn't have built-in signature verification. Instead, policy controllers like Kyverno, OPA Gatekeeper, or Connaisseur enforce signature verification using cosign (from Sigstore project). These admission controllers verify signatures before allowing Pods to run with specific images.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

## Container Lifecycle

### Question 33
What are the possible states of a container in Kubernetes?

A) Starting, Running, Stopping
B) Waiting, Running, Terminated
C) Created, Active, Deleted
D) Init, Execute, Complete

<details><summary>Answer</summary>

**B) Waiting, Running, Terminated**

Kubernetes containers have three possible states: Waiting (not yet running, e.g., pulling image), Running (executing with PID), and Terminated (finished execution, either successfully or with failure). These states are visible in `kubectl describe pod` output.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 34
What causes a container to be in the 'Running' state?

A) The container image has been pulled
B) The container has been created and its main process is executing
C) The container is scheduled to a node
D) The container has completed its task

<details><summary>Answer</summary>

**B) The container has been created and its main process is executing**

A container is Running when it has been successfully created and its main process (defined by ENTRYPOINT/CMD or command/args) is executing. The state includes the startedAt timestamp showing when execution began.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 35
What is the container restart policy in Kubernetes?

A) A setting that controls how often containers are updated
B) A policy that determines when and if Kubernetes should restart a failed container
C) A schedule for container maintenance
D) A backup policy for container data

<details><summary>Answer</summary>

**B) A policy that determines when and if Kubernetes should restart a failed container**

The restartPolicy field in Pod spec controls restart behavior. It applies to all containers in the Pod and determines whether and when containers should be restarted after termination. Options are Always, OnFailure, and Never.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 36
When would you use restartPolicy 'OnFailure'?

A) For long-running services
B) For batch jobs that should retry on failure but not restart on success
C) For containers that should never restart
D) For init containers

<details><summary>Answer</summary>

**B) For batch jobs that should retry on failure but not restart on success**

`OnFailure` restarts containers only when they exit with a non-zero exit code. This is ideal for Jobs that should retry on failure but complete when successful. Unlike `Always`, successful completion (exit code 0) doesn't trigger a restart.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 37
How does Kubernetes handle container restart backoff?

A) Immediate restarts without delay
B) Exponential backoff starting at 10 seconds, doubling with each restart
C) Fixed 30-second delay between restarts
D) Random delay between restarts

<details><summary>Answer</summary>

**B) Exponential backoff starting at 10 seconds, doubling with each restart**

Kubernetes uses exponential backoff for container restarts: 10s, 20s, 40s, 80s, etc. This prevents crash loops from overwhelming the system. The backoff resets after the container runs successfully for 10 minutes. You see "CrashLoopBackOff" status during this delay.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

## Container Probes

### Question 38
What is the purpose of a liveness probe?

A) To check if the application is ready to serve traffic
B) To determine if the container is running and should be restarted if unhealthy
C) To validate container configuration
D) To measure container performance

<details><summary>Answer</summary>

**B) To determine if the container is running and should be restarted if unhealthy**

Liveness probes detect when a container is in a broken state (deadlocked, unresponsive) and needs to be restarted. If the liveness probe fails, kubelet kills the container and restarts it based on the restart policy. This helps recover from situations where the process is running but not functioning correctly.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 39
What is the purpose of a readiness probe?

A) To determine if the container should be restarted
B) To determine if the container is ready to accept traffic
C) To check if the image was pulled correctly
D) To validate container security

<details><summary>Answer</summary>

**B) To determine if the container is ready to accept traffic**

Readiness probes determine when a container is ready to serve requests. When the probe fails, the Pod's IP is removed from Service endpoints, stopping traffic to that Pod. Unlike liveness probes, readiness probe failures don't restart the container - they just remove it from load balancing.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 40
What is the purpose of a startup probe?

A) To check if the container started with correct arguments
B) To allow slow-starting containers time to initialize before liveness probes take over
C) To validate the container image
D) To check network connectivity

<details><summary>Answer</summary>

**B) To allow slow-starting containers time to initialize before liveness probes take over**

Startup probes protect slow-starting containers from being killed by liveness probes before they're ready. The liveness probe is disabled until the startup probe succeeds. This is useful for legacy applications that need significant initialization time.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 41
What are the three types of probe mechanisms in Kubernetes?

A) HTTP, TCP, UDP
B) exec, httpGet, tcpSocket
C) REST, gRPC, WebSocket
D) ping, curl, telnet

<details><summary>Answer</summary>

**B) exec, httpGet, tcpSocket**

Kubernetes supports three probe mechanisms: exec (runs a command inside the container), httpGet (sends HTTP GET request), and tcpSocket (opens TCP connection). Additionally, gRPC health checking is supported as a fourth option in newer Kubernetes versions.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 42
What constitutes a successful HTTP probe response?

A) Any response from the server
B) HTTP status code between 200 and 399
C) HTTP status code 200 only
D) Response within 1 second

<details><summary>Answer</summary>

**B) HTTP status code between 200 and 399**

An HTTP probe is successful if it receives a response with status code >= 200 and < 400. This includes all 2xx (success) and 3xx (redirect) codes. Status codes 4xx (client error) and 5xx (server error) are considered failures.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 43
What is an exec probe?

A) A probe that executes an HTTP request
B) A probe that runs a command inside the container
C) A probe that checks file existence
D) A probe that monitors CPU usage

<details><summary>Answer</summary>

**B) A probe that runs a command inside the container**

Exec probes run a specified command inside the container. The probe is successful if the command exits with status code 0. This is flexible and can check anything the command can verify, like file existence, process status, or custom health scripts.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 44
What is the initialDelaySeconds parameter in a probe configuration?

A) The time between probe checks
B) The time to wait before starting the first probe after container start
C) The maximum probe duration
D) The delay between failed probes

<details><summary>Answer</summary>

**B) The time to wait before starting the first probe after container start**

initialDelaySeconds specifies how long to wait after the container starts before performing the first probe. This gives the application time to initialize. Default is 0 seconds. With startup probes available, this parameter is less critical than before.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 45
What is the timeoutSeconds parameter in a probe configuration?

A) The initial delay before probing
B) How long to wait for a probe response before considering it failed
C) The time between probe attempts
D) The maximum container runtime

<details><summary>Answer</summary>

**B) How long to wait for a probe response before considering it failed**

timeoutSeconds specifies how long to wait for a probe response before considering it failed. Default is 1 second. If the probe doesn't respond within this time, it counts as a failure. This should be set based on expected response time of your health endpoint.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 46
What is the successThreshold parameter in a probe configuration?

A) The number of successes needed to mark a container as healthy after a failure
B) The percentage of successful probes required
C) The response time threshold
D) The minimum uptime requirement

<details><summary>Answer</summary>

**A) The number of successes needed to mark a container as healthy after a failure**

successThreshold specifies how many consecutive successful probes are needed before the container is considered healthy again (after being marked unhealthy). Default is 1. For liveness and startup probes, this must be 1. For readiness probes, it can be set higher.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 47
What is a common mistake when configuring liveness probes?

A) Using HTTP probes
B) Setting too aggressive timing that restarts containers during normal operation
C) Probing on port 80
D) Using the same probe for multiple containers

<details><summary>Answer</summary>

**B) Setting too aggressive timing that restarts containers during normal operation**

A common mistake is setting initialDelaySeconds too low or failureThreshold too low, causing containers to be restarted during slow startups or temporary high load. This can create restart loops and cascading failures. Always tune probe timing based on actual application behavior and startup time.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

## Multi-Container Pods

### Question 48
What is a sidecar container?

A) The main application container
B) A helper container that runs alongside the main container to provide supporting features
C) A container that runs before the main container
D) A backup container

<details><summary>Answer</summary>

**B) A helper container that runs alongside the main container to provide supporting features**

A sidecar container runs alongside the main application container in the same Pod, providing supporting functionality. Common use cases include logging agents, proxies (like Envoy in service mesh), file synchronization, and configuration management. Sidecars share the Pod's network and storage resources.

**Source:** [Sidecar Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/)

</details>

### Question 49
What is an init container?

A) A container that runs continuously alongside the main container
B) A container that runs to completion before the main containers start
C) The first container listed in the Pod spec
D) A container that initializes the cluster

<details><summary>Answer</summary>

**B) A container that runs to completion before the main containers start**

Init containers are specialized containers that run before app containers start. They run to completion (exit with status 0) in order. Use cases include waiting for dependencies, setting up configuration files, cloning git repos, or performing database migrations. Main containers won't start until all init containers succeed.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 50
In what order do init containers execute?

A) In parallel for faster startup
B) Sequentially in the order they are defined
C) In alphabetical order by name
D) In random order

<details><summary>Answer</summary>

**B) Sequentially in the order they are defined**

Init containers execute one at a time in the exact order they're listed in the Pod spec's `initContainers` array. Each must complete successfully before the next begins. This sequential execution ensures proper dependency ordering - for example, waiting for a service before downloading configuration that depends on it.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 51
What is the ambassador container pattern?

A) A pattern where a container handles security
B) A pattern where a sidecar proxies network connections to external services
C) A pattern for cross-cluster communication
D) A pattern for container orchestration

<details><summary>Answer</summary>

**B) A pattern where a sidecar proxies network connections to external services**

The ambassador pattern uses a sidecar container to proxy connections from the main container to external services. The main app connects to localhost, and the ambassador handles complexity like service discovery, connection pooling, or protocol translation. This simplifies the main application and centralizes connection logic.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 52
How do containers within the same Pod communicate?

A) Through Kubernetes Services
B) Through localhost, as they share the network namespace
C) Through external message queues
D) Through shared ConfigMaps

<details><summary>Answer</summary>

**B) Through localhost, as they share the network namespace**

Containers in the same Pod share the network namespace, meaning they share the same IP address and can communicate via localhost. One container can bind to port 8080 and another can connect to localhost:8080. This enables tightly-coupled containers to communicate efficiently without network overhead.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 53
What is a sidecar container in Kubernetes 1.28+?

A) A deprecated container type
B) A container with restartPolicy: Always in an init container definition
C) A container that runs in a separate Pod
D) A container managed by a DaemonSet

<details><summary>Answer</summary>

**B) A container with restartPolicy: Always in an init container definition**

Kubernetes 1.28+ introduced native sidecar containers as a feature. A native sidecar is defined in the `initContainers` array with `restartPolicy: Always`. Unlike regular init containers, sidecars start in order but don't need to complete - they run throughout the Pod's lifetime alongside main containers.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 54
What is the lifecycle behavior of native sidecar containers?

A) They run only during initialization
B) They start before and run throughout the lifetime of regular containers
C) They run after main containers complete
D) They run on a schedule

<details><summary>Answer</summary>

**B) They start before and run throughout the lifetime of regular containers**

Native sidecar containers start before main containers (in init container order) and continue running alongside main containers. They're not terminated when they become "ready" like regular init containers. When the Pod terminates, sidecars are shut down after main containers. This solves the problem of ensuring sidecars are available during and after main container execution.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 55
When would you use an ephemeral container?

A) For production workloads
B) For troubleshooting running Pods that lack debugging utilities
C) For running batch jobs
D) For init processes

<details><summary>Answer</summary>

**B) For troubleshooting running Pods that lack debugging utilities**

Use ephemeral containers when you need to debug a Pod that uses distroless or minimal images without shells or debugging tools. Common scenarios: debugging a crashed container, inspecting network issues with tcpdump, or using strace to trace system calls. They share namespaces with other containers in the Pod.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

## Container Resources

### Question 56
What are container resource limits in Kubernetes?

A) The minimum resources required
B) The maximum resources a container is allowed to use
C) Soft limits that can be exceeded
D) Cluster-wide resource quotas

<details><summary>Answer</summary>

**B) The maximum resources a container is allowed to use**

Resource limits specify the maximum resources a container can consume. The container runtime enforces these limits - CPU limits through throttling and memory limits through OOM killing. Setting appropriate limits prevents resource-hungry containers from affecting other workloads on the same node.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 57
What happens when a container exceeds its memory limit?

A) The container is throttled
B) The container is terminated (OOMKilled)
C) Memory is borrowed from other containers
D) The limit is automatically increased

<details><summary>Answer</summary>

**B) The container is terminated (OOMKilled)**

When a container tries to use more memory than its limit, the Linux OOM (Out Of Memory) killer terminates the process. The container's exit reason shows "OOMKilled". Unlike CPU, memory cannot be throttled - it's either granted or not. The Pod may restart based on its restartPolicy.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 58
What is the difference between CPU and memory limit enforcement?

A) Both are enforced the same way
B) CPU is throttled (compressible), memory excess causes termination (incompressible)
C) Memory is throttled, CPU causes termination
D) Neither is enforced strictly

<details><summary>Answer</summary>

**B) CPU is throttled (compressible), memory excess causes termination (incompressible)**

CPU and memory are treated differently because of their nature. CPU is compressible - if limited, the process just runs slower. Memory is incompressible - you either have it or you don't. When a container needs more memory than its limit, the only option is to kill it (OOMKill) as there's no way to "slow down" memory usage.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 59
What does '500m' mean for CPU resources?

A) 500 megabytes
B) 500 millicores, equivalent to 0.5 CPU cores
C) 500 minutes of CPU time
D) 500 milliwatts

<details><summary>Answer</summary>

**B) 500 millicores, equivalent to 0.5 CPU cores**

The suffix 'm' stands for millicores (milli-CPU). 500m means 500/1000 = 0.5 CPU cores. This is equivalent to writing `0.5` in the spec. Common values include 100m (10% of a core), 250m (quarter core), and 1000m (one full core).

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 60
What is the difference between Mi and M for memory units?

A) They are identical
B) Mi is mebibytes (1024^2), M is megabytes (1000^2)
C) M is larger than Mi
D) Mi is deprecated

<details><summary>Answer</summary>

**B) Mi is mebibytes (1024^2), M is megabytes (1000^2)**

Mi (mebibyte) uses binary units: 1Mi = 1024 * 1024 = 1,048,576 bytes. M (megabyte) uses decimal units: 1M = 1000 * 1000 = 1,000,000 bytes. 1Mi is about 4.9% larger than 1M. Using Mi is recommended for consistency with how operating systems report memory.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 61
When is a Pod assigned the 'Guaranteed' QoS class?

A) When any container has resource requests
B) When every container has equal requests and limits set for both CPU and memory
C) When the Pod has high priority
D) When using premium storage

<details><summary>Answer</summary>

**B) When every container has equal requests and limits set for both CPU and memory**

A Pod gets Guaranteed QoS when every container specifies both memory and CPU requests AND limits, and requests equal limits. Example: `requests: {memory: "256Mi", cpu: "500m"}` and `limits: {memory: "256Mi", cpu: "500m"}`. Guaranteed Pods are the last to be evicted under resource pressure.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 62
When is a Pod assigned the 'BestEffort' QoS class?

A) When all containers have limits
B) When no containers have resource requests or limits specified
C) When using guaranteed storage
D) When the Pod has the highest priority

<details><summary>Answer</summary>

**B) When no containers have resource requests or limits specified**

BestEffort QoS is assigned when no container in the Pod has any memory or CPU requests or limits. These Pods have the lowest priority during resource contention and are evicted first when the node is under memory pressure. They're suitable for non-critical workloads that can tolerate interruption.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

## Container Configuration

### Question 63
How can you pass environment variables to a container?

A) Only through ConfigMaps
B) Through env field, ConfigMaps, Secrets, or downward API
C) Only through command-line arguments
D) Environment variables cannot be passed

<details><summary>Answer</summary>

**B) Through env field, ConfigMaps, Secrets, or downward API**

Environment variables can be set directly in the `env` field, loaded from ConfigMaps or Secrets using `valueFrom` or `envFrom`, or populated from Pod/container metadata using the downward API. This flexibility allows separating configuration from container images.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 64
How can ConfigMap data be exposed to containers?

A) Only as files
B) As environment variables or mounted as files in a volume
C) Only as environment variables
D) Through command-line arguments only

<details><summary>Answer</summary>

**B) As environment variables or mounted as files in a volume**

ConfigMap data can be consumed as environment variables (using `envFrom` or `valueFrom`) or mounted as files in a volume. When mounted as a volume, each key becomes a file in the mount path. Volume-mounted ConfigMaps can be updated dynamically without restarting the Pod.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 65
How are Secrets different from ConfigMaps?

A) Secrets are encrypted at rest by default
B) Secrets are base64-encoded and intended for sensitive data, with optional encryption at rest
C) Secrets can only store strings
D) Secrets have size limits, ConfigMaps don't

<details><summary>Answer</summary>

**B) Secrets are base64-encoded and intended for sensitive data, with optional encryption at rest**

Secrets are base64-encoded (not encrypted by default) and designed for sensitive data. Key differences: Secrets can be encrypted at rest (when configured), are stored in tmpfs when mounted, and have different RBAC policies. Note that base64 is encoding, not encryption - encryption at rest must be explicitly configured.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 66
What is the envFrom field used for?

A) To export environment variables
B) To load all key-value pairs from a ConfigMap or Secret as environment variables
C) To read environment from a file
D) To copy environment between containers

<details><summary>Answer</summary>

**B) To load all key-value pairs from a ConfigMap or Secret as environment variables**

`envFrom` allows you to inject all key-value pairs from a ConfigMap or Secret as environment variables in one declaration. Each key becomes an environment variable name, and its value becomes the variable value. You can optionally add a prefix to avoid naming conflicts.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 67
What is a volume mount in a container?

A) A network share
B) A path in the container's filesystem where a volume is attached
C) A storage device
D) A backup location

<details><summary>Answer</summary>

**B) A path in the container's filesystem where a volume is attached**

A volume mount specifies where a Pod's volume is attached within a container's filesystem. You define the volume at the Pod level and mount it at a specific path in each container using `volumeMounts`. This allows containers to access shared storage, configuration files, or secrets at defined paths.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 68
What is the command field in a container spec?

A) The working directory
B) The entrypoint that overrides the image's ENTRYPOINT
C) Arguments to the entrypoint
D) A post-start command

<details><summary>Answer</summary>

**B) The entrypoint that overrides the image's ENTRYPOINT**

The `command` field in a container spec overrides the Docker image's ENTRYPOINT. It's an array of strings representing the executable and its initial arguments. If specified, the image's default ENTRYPOINT is completely replaced. If not specified, the image's ENTRYPOINT is used.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 69
How do command and args override Dockerfile ENTRYPOINT and CMD?

A) They don't, Dockerfile instructions take precedence
B) command overrides ENTRYPOINT, args overrides CMD
C) command overrides CMD, args overrides ENTRYPOINT
D) Both override CMD only

<details><summary>Answer</summary>

**B) command overrides ENTRYPOINT, args overrides CMD**

Kubernetes `command` maps to Docker's ENTRYPOINT, and `args` maps to Docker's CMD. If you set command, it replaces ENTRYPOINT. If you set args, it replaces CMD. If neither is set, the image defaults are used. This allows flexible control over container startup behavior.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 70
How can you override a container's working directory in Kubernetes?

A) Using the directory field
B) Using the workingDir field in the container spec
C) Using an environment variable
D) Using a volume mount

<details><summary>Answer</summary>

**B) Using the workingDir field in the container spec**

The `workingDir` field in the container spec overrides the image's default working directory. Specify an absolute path where the container's process should start. This is useful when you need to run commands from a different directory than the image default, such as an application directory within a shared volume.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

## Container Security

### Question 71
What does the runAsUser field specify?

A) The container's hostname
B) The UID to run the container's entrypoint process as
C) The user that created the Pod
D) The service account name

<details><summary>Answer</summary>

**B) The UID to run the container's entrypoint process as**

`runAsUser` specifies the user ID (UID) for running the container's process. This overrides the USER directive in the image. For security, containers should run as non-root users (UID > 0). Combined with `runAsNonRoot: true`, this ensures the container doesn't run as root.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 72
What is the readOnlyRootFilesystem setting?

A) A backup option
B) A setting that mounts the container's root filesystem as read-only
C) A storage encryption option
D) A log rotation setting

<details><summary>Answer</summary>

**B) A setting that mounts the container's root filesystem as read-only**

`readOnlyRootFilesystem: true` mounts the container's root filesystem as read-only, preventing any writes. This limits the impact of container compromise by preventing attackers from modifying binaries or writing malicious files. Applications that need to write files must use mounted volumes for writable directories.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 73
How can you drop Linux capabilities from a container?

A) Using runAsNonRoot
B) Using securityContext.capabilities.drop
C) Using privileged: false
D) Using readOnlyRootFilesystem

<details><summary>Answer</summary>

**B) Using securityContext.capabilities.drop**

Use `securityContext.capabilities.drop` with a list of capability names to remove from the container. For maximum security, drop ALL capabilities with `drop: ["ALL"]` and then add back only the specific ones needed with `add`. This follows the principle of least privilege.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 74
What is a privileged container?

A) A container with resource limits
B) A container with almost all root capabilities and access to host resources
C) A container running as root
D) A container with network access

<details><summary>Answer</summary>

**B) A container with almost all root capabilities and access to host resources**

A privileged container (`privileged: true`) runs with all Linux capabilities and can access host devices (/dev), bypass many security restrictions, and potentially modify the host system. It's nearly equivalent to root access on the host. Privileged mode is needed for specific use cases like container runtimes but should be avoided otherwise.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 75
What is allowPrivilegeEscalation?

A) A Pod priority setting
B) A setting that controls whether a process can gain more privileges than its parent
C) A resource limit
D) A network policy

<details><summary>Answer</summary>

**B) A setting that controls whether a process can gain more privileges than its parent**

`allowPrivilegeEscalation` controls whether a process can gain more privileges than its parent process. Setting it to `false` prevents setuid binaries and other privilege escalation methods. This is a security best practice and is required when running as non-root with the Restricted Pod Security Standard.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 76
What is the RuntimeDefault seccomp profile?

A) A custom profile
B) The container runtime's default seccomp profile that blocks dangerous syscalls
C) No restrictions
D) A Kubernetes-specific profile

<details><summary>Answer</summary>

**B) The container runtime's default seccomp profile that blocks dangerous syscalls**

RuntimeDefault uses the container runtime's built-in seccomp profile, which blocks dangerous system calls like reboot, kernel module loading, and clock modifications while allowing common operations. It's a good baseline security measure that works with most applications without modification.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 77
How do you apply an AppArmor profile to a container?

A) Using a securityContext field
B) Using an annotation on the Pod
C) Using a ConfigMap
D) Using a custom resource

<details><summary>Answer</summary>

**B) Using an annotation on the Pod**

AppArmor profiles are applied via Pod annotations in the format `container.apparmor.security.beta.kubernetes.io/<container_name>: <profile>`. The profile must be loaded on the node. Common values are `runtime/default`, `localhost/<profile-name>`, or `unconfined`. Note: Kubernetes 1.30+ also supports the appArmorProfile field in securityContext.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 78
How can you set SELinux options for a container?

A) Using an annotation
B) Using securityContext.seLinuxOptions
C) Using a ConfigMap
D) Using environment variables

<details><summary>Answer</summary>

**B) Using securityContext.seLinuxOptions**

SELinux options are configured via `securityContext.seLinuxOptions`, which accepts fields like `user`, `role`, `type`, and `level`. These set the SELinux context for the container's processes. This is particularly important on SELinux-enabled systems (like RHEL/CentOS) for proper volume access and security policy enforcement.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 79
What are the three Pod Security Standard levels?

A) Low, Medium, High
B) Privileged, Baseline, Restricted
C) Basic, Standard, Advanced
D) Open, Controlled, Locked

<details><summary>Answer</summary>

**B) Privileged, Baseline, Restricted**

The three levels are: Privileged (no restrictions, allows all), Baseline (prevents known privilege escalations, suitable for most workloads), and Restricted (heavily restricted, follows Pod hardening best practices). Each level builds on the previous with more security controls.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 80
What does the Baseline Pod Security Standard restrict?

A) All capabilities
B) Known privilege escalations while allowing common configurations
C) All root users
D) All volume mounts

<details><summary>Answer</summary>

**B) Known privilege escalations while allowing common configurations**

Baseline restricts known privilege escalations like privileged containers, hostPID/hostIPC/hostNetwork, and dangerous volume types, while allowing common configurations like running as root (with restrictions). It's suitable for most workloads and balances security with ease of adoption.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

## Container Networking

### Question 81
How do containers in the same Pod communicate with each other?

A) Through Kubernetes Services
B) Through localhost, as they share the same network namespace
C) Through environment variables
D) Through shared volumes

<details><summary>Answer</summary>

**B) Through localhost, as they share the same network namespace**

Containers in the same Pod can communicate via localhost (127.0.0.1) because they share the network namespace. One container can connect to another's port using localhost:<port>. This enables patterns like sidecars where a proxy container handles traffic for the main application container.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 82
What role does the pause container play in Pod networking?

A) It routes traffic between Pods
B) It holds the network namespace that other containers in the Pod join
C) It provides DNS services
D) It manages firewall rules

<details><summary>Answer</summary>

**B) It holds the network namespace that other containers in the Pod join**

The pause container's main role is to create and hold the network namespace. When application containers start, they join this existing namespace rather than creating their own. This design ensures the network namespace survives container restarts and provides a stable network identity for the Pod.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 83
What is the containerPort field used for?

A) To open ports on the host
B) To document and expose the port the container listens on
C) To configure firewall rules
D) To set up port forwarding

<details><summary>Answer</summary>

**B) To document and expose the port the container listens on**

`containerPort` is primarily informational, documenting which port the container application uses. It's required for port naming (used in Service targetPort by name) and for certain tools to discover ports. The container can still listen on any port regardless of this declaration.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 84
Why should hostPort be avoided in most cases?

A) It's deprecated
B) It limits Pod scheduling and can cause port conflicts
C) It's slower than Services
D) It doesn't work with CNI plugins

<details><summary>Answer</summary>

**B) It limits Pod scheduling and can cause port conflicts**

Using hostPort limits Pod scheduling to nodes where that port is available, potentially causing scheduling failures. Only one Pod using a specific hostPort can run on each node. It creates tight coupling between Pods and nodes. Services or Ingress are preferred for most traffic routing needs.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 85
How does a Service route traffic to container ports?

A) Through hostPort
B) Through selectors matching Pod labels and targetPort mapping
C) Through direct container connections
D) Through shared volumes

<details><summary>Answer</summary>

**B) Through selectors matching Pod labels and targetPort mapping**

Services use label selectors to find matching Pods, then route traffic to the `targetPort` on those Pods. The Service's `port` receives traffic, which is forwarded to `targetPort` on the container. This provides load balancing across all matching Pods without exposing individual Pod IPs.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

## Container Logging and Debugging

### Question 86
How does kubectl logs retrieve container logs?

A) By reading files from the container
B) By requesting logs from the kubelet, which gets them from the container runtime
C) By querying a logging database
D) By accessing the API server logs

<details><summary>Answer</summary>

**B) By requesting logs from the kubelet, which gets them from the container runtime**

`kubectl logs` makes a request to the API server, which proxies to the kubelet on the appropriate node. The kubelet then retrieves logs from the container runtime. This chain allows centralized log access without directly connecting to nodes.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 87
How can you view logs from a previous container instance?

A) Using kubectl logs --history
B) Using kubectl logs --previous
C) Using kubectl logs --old
D) Using kubectl logs --backup

<details><summary>Answer</summary>

**B) Using kubectl logs --previous**

The `--previous` (or `-p`) flag shows logs from the previous container instance. This is essential for debugging crash loops where the current container keeps restarting. It shows whatever logs the crashed container wrote before termination.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 88
What is a logging sidecar container?

A) A container that processes application logs
B) A helper container that collects and forwards logs from the main container
C) A container for log analysis
D) A container that stores log files

<details><summary>Answer</summary>

**B) A helper container that collects and forwards logs from the main container**

A logging sidecar runs alongside the main container, collecting logs and forwarding them to a centralized logging system. It's useful when applications write logs to files instead of stdout, or when logs need transformation. Common sidecars include Fluentd, Filebeat, and Fluent Bit.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 89
What does kubectl exec do?

A) Creates a new container
B) Executes a command inside a running container
C) Stops a container
D) Copies files to a container

<details><summary>Answer</summary>

**B) Executes a command inside a running container**

`kubectl exec` runs a command in a running container, similar to `docker exec`. Add `-it` for interactive mode with a TTY. Useful for debugging, checking configurations, running diagnostic commands, or getting a shell inside the container.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 90
What is kubectl debug used for?

A) Viewing logs
B) Creating ephemeral containers or debug copies of Pods for troubleshooting
C) Setting breakpoints
D) Monitoring performance

<details><summary>Answer</summary>

**B) Creating ephemeral containers or debug copies of Pods for troubleshooting**

`kubectl debug` adds ephemeral containers to running Pods, creates debug copies of Pods with modified settings, or creates debug Pods on nodes. It's useful for troubleshooting distroless images, crash loops, or node-level issues where `kubectl exec` isn't sufficient.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

### Question 91
What is a debug container?

A) A container with debugging tools
B) An ephemeral container added to a running Pod for troubleshooting
C) A container in debug mode
D) A test container

<details><summary>Answer</summary>

**B) An ephemeral container added to a running Pod for troubleshooting**

A debug container is an ephemeral container added to a running Pod using `kubectl debug`. It can share process, network, or IPC namespaces with other containers, providing access to debug tools (curl, strace, tcpdump) that might not be in the production image. Ephemeral containers can't be removed once added.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

### Question 92
What does kubectl top pod show?

A) Pod configuration
B) Current CPU and memory usage of Pods and their containers
C) Historical resource data
D) Resource requests and limits

<details><summary>Answer</summary>

**B) Current CPU and memory usage of Pods and their containers**

`kubectl top pod` displays current CPU usage (in millicores) and memory usage (in bytes) for Pods. It shows a snapshot of actual resource consumption, not the configured requests/limits. Use this to identify resource-heavy Pods, tune resource allocations, or debug performance issues.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

## Advanced Container Concepts

### Question 93
What is a container hook in Kubernetes?

A) A network callback
B) A lifecycle event handler that runs code at specific container lifecycle points
C) A security feature
D) A monitoring probe

<details><summary>Answer</summary>

**B) A lifecycle event handler that runs code at specific container lifecycle points**

Container hooks are lifecycle event handlers that allow you to run code when specific events occur in a container's lifecycle. Kubernetes supports two hooks: PostStart (runs after container creation) and PreStop (runs before container termination). Hooks can be exec commands or HTTP requests.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 94
What is the PreStop hook?

A) A hook that runs before container creation
B) A hook that runs before a container is terminated
C) A startup hook
D) A pause hook

<details><summary>Answer</summary>

**B) A hook that runs before a container is terminated**

The PreStop hook executes before a container is terminated (before SIGTERM is sent). It's useful for graceful shutdown tasks like deregistering from a service registry, saving state, or completing in-flight requests. The hook must complete before the grace period expires.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 95
What happens if a PostStart hook fails?

A) The container continues running
B) The container is killed
C) The hook is retried
D) The Pod is rescheduled

<details><summary>Answer</summary>

**B) The container is killed**

If a PostStart hook fails (returns non-zero exit code or HTTP error), the container is killed. The failure event is visible in `kubectl describe`. The container may be restarted based on restartPolicy. Ensure hooks are reliable, or the container will enter a crash loop.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 96
What happens when a Pod is terminated?

A) Containers are killed immediately
B) PreStop hooks run, then SIGTERM is sent, then SIGKILL after grace period
C) Only SIGKILL is sent
D) Containers are paused

<details><summary>Answer</summary>

**B) PreStop hooks run, then SIGTERM is sent, then SIGKILL after grace period**

Pod termination sequence: 1) PreStop hooks run first and must complete before SIGTERM is sent, 2) SIGTERM is sent to container processes, 3) Grace period counts down (covering both hook execution and shutdown time), 4) SIGKILL is sent to any remaining processes. The `terminationGracePeriodSeconds` covers the total time for both PreStop and container shutdown.

**Source:** [Container Lifecycle Hooks | Kubernetes](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/)

</details>

### Question 97
What happens after the grace period expires during Pod termination?

A) The Pod waits longer
B) SIGKILL is sent to force-terminate remaining processes
C) The Pod is rescheduled
D) An error is logged but nothing happens

<details><summary>Answer</summary>

**B) SIGKILL is sent to force-terminate remaining processes**

When the grace period expires, SIGKILL (signal 9) is sent to any processes still running. SIGKILL cannot be caught or ignored - it immediately terminates processes. This ensures containers don't run indefinitely and resources are released, even if applications don't handle SIGTERM properly.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 98
How does image garbage collection work in Kubernetes?

A) Images are never deleted
B) Kubelet removes unused images when disk usage exceeds thresholds
C) Images are deleted after each Pod
D) A separate garbage collector Pod runs

<details><summary>Answer</summary>

**B) Kubelet removes unused images when disk usage exceeds thresholds**

The kubelet periodically runs image garbage collection. When disk usage exceeds imageGCHighThresholdPercent (default 85%), unused images are deleted until disk falls below imageGCLowThresholdPercent (default 80%). Images used by running containers are never deleted. This prevents disk exhaustion.

**Source:** [Container Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 99
What causes ErrImagePull errors?

A) Low memory
B) Image not found, authentication failure, or network issues
C) CPU limits exceeded
D) Disk full

<details><summary>Answer</summary>

**B) Image not found, authentication failure, or network issues**

ErrImagePull occurs when Kubernetes can't pull an image. Common causes: image name typos, tag doesn't exist, private registry without imagePullSecrets, network connectivity issues, registry rate limiting, or registry downtime. Check the error message in `kubectl describe pod` for specifics.

**Source:** [Container Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 100
What is gVisor in the context of container runtimes?

A) A container orchestrator
B) A user-space kernel that provides additional isolation for containers
C) A container registry
D) A monitoring tool

<details><summary>Answer</summary>

**B) A user-space kernel that provides additional isolation for containers**

gVisor is an application kernel written in Go that implements a substantial portion of the Linux system call interface. It runs in user space and intercepts container system calls, providing strong isolation without the overhead of a full VM. gVisor is used via the runsc OCI runtime and is suitable for running untrusted code.

**Source:** [Runtime Class | Kubernetes](https://kubernetes.io/docs/concepts/containers/runtime-class/)

</details>