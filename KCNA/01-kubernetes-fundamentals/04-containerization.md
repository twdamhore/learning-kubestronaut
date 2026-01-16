# KCNA Containerization MCQs

## Container Fundamentals

### Question 1
What is a container in the context of cloud-native computing?

A) A physical server dedicated to running a single application
B) A lightweight, standalone executable package that includes everything needed to run software
C) A virtual machine with a complete operating system
D) A network storage device for application data

<details><summary>Answer</summary>

**B) A lightweight, standalone executable package that includes everything needed to run software**

Containers are lightweight, portable units that package an application along with its dependencies, libraries, and configuration files. Unlike VMs, containers share the host OS kernel, making them more efficient and faster to start. They provide process isolation while being much more resource-efficient than traditional virtual machines.

</details>

### Question 2
Which technology provides the foundation for container isolation in Linux?

A) Virtual machines and hypervisors
B) Namespaces and cgroups
C) Firewalls and network segmentation
D) File system encryption

<details><summary>Answer</summary>

**B) Namespaces and cgroups**

Linux namespaces provide isolation of system resources (PID, network, mount, user, etc.) while cgroups (control groups) limit and account for resource usage (CPU, memory, I/O). Together, these kernel features form the foundation of container technology, enabling process isolation without the overhead of full virtualization.

</details>

### Question 3
What is the primary difference between a container and a virtual machine?

A) Containers are larger and require more resources
B) Containers share the host OS kernel while VMs have their own OS
C) Virtual machines are faster to start
D) Containers require a hypervisor

<details><summary>Answer</summary>

**B) Containers share the host OS kernel while VMs have their own OS**

The key difference is that containers share the host operating system's kernel, making them lightweight and fast to start. Virtual machines include a complete guest OS with its own kernel, requiring a hypervisor and more resources. Containers typically start in seconds while VMs take minutes.

</details>

### Question 4
Which Linux kernel feature allows containers to have isolated views of system resources like PIDs and network interfaces?

A) cgroups
B) Namespaces
C) SELinux
D) AppArmor

<details><summary>Answer</summary>

**B) Namespaces**

Linux namespaces provide isolated views of system resources. There are several namespace types: PID (process IDs), NET (network interfaces), MNT (mount points), UTS (hostname), IPC (inter-process communication), and USER (user IDs). Each container can have its own isolated view of these resources. Cgroups, by contrast, limit resource usage rather than provide isolation.

</details>

### Question 5
What is a container image?

A) A running instance of an application
B) A read-only template used to create containers
C) A backup of container data
D) A network configuration file

<details><summary>Answer</summary>

**B) A read-only template used to create containers**

A container image is an immutable, read-only template containing the application code, runtime, libraries, and dependencies needed to run a container. When you run an image, it becomes a container (running instance). Images are built in layers and stored in registries for distribution.

</details>

### Question 6
How are container image layers structured?

A) As a single monolithic file
B) As a stack of read-only layers with a writable layer on top
C) As separate executable files
D) As encrypted partitions

<details><summary>Answer</summary>

**B) As a stack of read-only layers with a writable layer on top**

Container images use a union file system with stacked layers. Each layer represents a set of filesystem changes (added, modified, or deleted files). The layers are read-only, and when a container runs, a thin writable layer is added on top for runtime changes. This layered approach enables efficient storage and sharing of common base layers.

</details>

### Question 7
What happens when multiple containers share the same base image layers?

A) Each container gets a complete copy of all layers
B) The layers are shared, saving disk space
C) Containers cannot share image layers
D) Only the first container uses the layers

<details><summary>Answer</summary>

**B) The layers are shared, saving disk space**

When multiple containers use the same base image, the shared layers are stored only once on disk. Each container gets its own thin writable layer on top, but the underlying read-only layers are shared. This copy-on-write mechanism significantly reduces disk usage and speeds up container creation.

</details>

### Question 8
What is the purpose of a container runtime?

A) To compile container applications
B) To manage the lifecycle of containers including creation, running, and deletion
C) To design container images
D) To monitor network traffic

<details><summary>Answer</summary>

**B) To manage the lifecycle of containers including creation, running, and deletion**

A container runtime is software responsible for running containers. It handles pulling images, creating container instances, managing their lifecycle (start, stop, restart, delete), and interacting with the kernel for isolation and resource management. Examples include containerd, CRI-O, and runc.

</details>

### Question 9
Which component in Kubernetes is responsible for pulling container images and running containers?

A) kube-apiserver
B) kube-scheduler
C) kubelet
D) kube-controller-manager

<details><summary>Answer</summary>

**C) kubelet**

The kubelet is the primary node agent that runs on each worker node. It communicates with the container runtime (via CRI) to pull images and manage container lifecycle. The kubelet receives Pod specifications from the API server and ensures the containers are running as specified.

</details>

### Question 10
What is the Container Runtime Interface (CRI) in Kubernetes?

A) A graphical interface for managing containers
B) A plugin interface that allows kubelet to use different container runtimes
C) A container image format
D) A network protocol for container communication

<details><summary>Answer</summary>

**B) A plugin interface that allows kubelet to use different container runtimes**

CRI is a plugin interface that enables the kubelet to work with any container runtime that implements the interface. It uses gRPC for communication and defines operations like pulling images, creating/starting/stopping containers. This abstraction allows Kubernetes to support multiple runtimes (containerd, CRI-O) without code changes.

</details>

## Container Runtimes

### Question 11
Which of the following is NOT a CRI-compliant container runtime?

A) containerd
B) CRI-O
C) Docker Engine (dockershim)
D) containerd with CRI plugin

<details><summary>Answer</summary>

**C) Docker Engine (dockershim)**

Docker Engine itself does not implement CRI natively. Kubernetes used dockershim as an adapter to communicate with Docker, but this was deprecated and removed in Kubernetes 1.24. containerd and CRI-O are native CRI implementations. Docker uses containerd under the hood, which is CRI-compliant.

</details>

### Question 12
What is containerd?

A) A container orchestration platform
B) An industry-standard container runtime focused on simplicity and portability
C) A container image registry
D) A Kubernetes distribution

<details><summary>Answer</summary>

**B) An industry-standard container runtime focused on simplicity and portability**

containerd is a CNCF graduated project that serves as an industry-standard container runtime. It manages the complete container lifecycle including image transfer, container execution, and storage. Originally part of Docker, it was extracted as a standalone runtime and is now used by Docker, Kubernetes, and other platforms.

</details>

### Question 13
How does CRI-O differ from containerd?

A) CRI-O is designed specifically for Kubernetes, while containerd is more general-purpose
B) CRI-O does not support OCI images
C) containerd cannot run in Kubernetes
D) CRI-O requires Docker to function

<details><summary>Answer</summary>

**A) CRI-O is designed specifically for Kubernetes, while containerd is more general-purpose**

CRI-O was built from the ground up specifically for Kubernetes, implementing only what's needed for the CRI. containerd is a more general-purpose runtime that can be used in various contexts beyond Kubernetes. Both support OCI images and work well with Kubernetes.

</details>

### Question 14
What is the relationship between Docker and containerd?

A) Docker and containerd are completely separate projects
B) containerd was extracted from Docker and is now used as Docker's core runtime
C) Docker is a plugin for containerd
D) containerd replaced Docker entirely

<details><summary>Answer</summary>

**B) containerd was extracted from Docker and is now used as Docker's core runtime**

containerd was originally developed as part of Docker and was later extracted as a standalone project donated to the CNCF. Docker Engine still uses containerd as its core container runtime. When you run `docker run`, Docker uses containerd to actually run the container, which in turn uses runc.

</details>

### Question 15
Which container runtime is specifically designed and optimized for Kubernetes?

A) Docker Engine
B) rkt
C) CRI-O
D) LXC

<details><summary>Answer</summary>

**C) CRI-O**

CRI-O (Container Runtime Interface - OCI) was specifically designed for Kubernetes. It implements only the features required by the Kubernetes CRI, making it lightweight and focused. It supports OCI-compliant images and runtimes, and is optimized for Kubernetes workloads.

</details>

### Question 16
What is runc?

A) A container orchestration tool
B) A low-level container runtime that implements the OCI runtime specification
C) A container registry
D) A container networking plugin

<details><summary>Answer</summary>

**B) A low-level container runtime that implements the OCI runtime specification**

runc is a lightweight, low-level container runtime that spawns and runs containers according to the OCI Runtime Specification. It's the reference implementation of the OCI runtime spec and is used by higher-level runtimes like containerd and CRI-O to actually create and run containers.

</details>

### Question 17
What role does the OCI (Open Container Initiative) play in containerization?

A) It provides cloud hosting for containers
B) It defines industry standards for container formats and runtimes
C) It manages Kubernetes clusters
D) It provides container security scanning

<details><summary>Answer</summary>

**B) It defines industry standards for container formats and runtimes**

The OCI is a Linux Foundation project that creates open industry standards for container formats and runtimes. It maintains specifications including the Runtime Specification (how to run containers), Image Specification (container image format), and Distribution Specification (how to distribute images). These standards ensure interoperability across different tools and platforms.

</details>

### Question 18
Which OCI specification defines how to run a container?

A) Image Specification
B) Runtime Specification
C) Distribution Specification
D) Network Specification

<details><summary>Answer</summary>

**B) Runtime Specification**

The OCI Runtime Specification defines how to run a "filesystem bundle" that is unpacked from an image. It specifies the configuration, execution environment, and lifecycle of a container. runc is the reference implementation of this specification.

</details>

### Question 19
What is the purpose of the OCI Image specification?

A) To define how containers should be networked
B) To define the format and structure of container images
C) To specify container security requirements
D) To outline container orchestration patterns

<details><summary>Answer</summary>

**B) To define the format and structure of container images**

The OCI Image Specification defines how container images are structured, including the image manifest, filesystem layers, and configuration. This standard ensures that images built with one tool can run on any OCI-compliant runtime, enabling portability across different platforms.

</details>

### Question 20
How does Kubernetes communicate with container runtimes?

A) Through direct API calls to Docker
B) Through the Container Runtime Interface (CRI) using gRPC
C) Through REST APIs
D) Through shared file systems

<details><summary>Answer</summary>

**B) Through the Container Runtime Interface (CRI) using gRPC**

Kubernetes uses CRI to communicate with container runtimes. The kubelet makes gRPC calls to the runtime through the CRI interface, which defines operations for managing images and containers. This abstraction allows Kubernetes to work with any CRI-compliant runtime without modification.

</details>

## Container Images and Registries

### Question 21
What is a container registry?

A) A log of all container activities
B) A storage and distribution system for container images
C) A container orchestration tool
D) A container security scanner

<details><summary>Answer</summary>

**B) A storage and distribution system for container images**

A container registry is a repository for storing, managing, and distributing container images. Registries can be public (like Docker Hub) or private (like Harbor, AWS ECR, GCR). They allow teams to share images and provide versioning through tags and digests.

</details>

### Question 22
Which of the following is the default container registry for Docker images?

A) Google Container Registry
B) Amazon ECR
C) Docker Hub
D) Quay.io

<details><summary>Answer</summary>

**C) Docker Hub**

Docker Hub is the default public registry for Docker images. When you pull an image without specifying a registry (e.g., `nginx`), Docker automatically looks for it on Docker Hub. It hosts millions of public images and also offers private repositories.

</details>

### Question 23
What is the purpose of image tags?

A) To encrypt container images
B) To identify specific versions of an image
C) To compress image layers
D) To specify runtime configurations

<details><summary>Answer</summary>

**B) To identify specific versions of an image**

Image tags are human-readable labels that point to specific image versions. Common tagging conventions include version numbers (v1.0.0), semantic versions (1.2.3), git commit SHAs, or descriptive names. Tags make it easier to reference and deploy specific versions of an image.

</details>

### Question 24
What does the 'latest' tag signify for a container image?

A) The most recently pushed image to the repository
B) The most stable version of the image
C) The image with the highest version number
D) Simply a tag name with no special meaning guaranteed

<details><summary>Answer</summary>

**D) Simply a tag name with no special meaning guaranteed**

The 'latest' tag has no special meaning in registries - it's just a conventional tag name. It doesn't automatically point to the newest image; it only updates when someone explicitly tags an image as 'latest'. Many assume it means the most recent version, but this is not guaranteed, which is why using specific version tags is recommended.

</details>

### Question 25
What is an image digest?

A) A compressed version of the image
B) A content-addressable identifier (SHA256 hash) that uniquely identifies an image
C) A summary of image contents
D) An encrypted image tag

<details><summary>Answer</summary>

**B) A content-addressable identifier (SHA256 hash) that uniquely identifies an image**

An image digest is a SHA256 hash of the image manifest, providing an immutable identifier for an exact image version. Unlike tags which can be moved to point to different images, digests are computed from the image content and never change. Format: `image@sha256:abc123...`

</details>

### Question 26
Why are image digests preferred over tags for production deployments?

A) Digests are shorter and easier to remember
B) Digests are immutable and guarantee the exact same image content
C) Digests allow for automatic updates
D) Digests are required by Kubernetes

<details><summary>Answer</summary>

**B) Digests are immutable and guarantee the exact same image content**

Digests are preferred in production because they're immutable - the same digest always refers to the exact same image content. Tags can be changed to point to different images, which could cause unexpected behavior or security issues. Using digests ensures reproducibility and prevents supply chain attacks.

</details>

### Question 27
What is a private container registry?

A) A registry that only stores encrypted images
B) A registry that requires authentication to access images
C) A registry that runs on-premises only
D) A registry that stores only proprietary images

<details><summary>Answer</summary>

**B) A registry that requires authentication to access images**

A private container registry requires authentication to pull or push images. This protects proprietary code and ensures only authorized users can access images. Private registries can be cloud-hosted (ECR, GCR, ACR) or self-hosted (Harbor, Nexus). Authentication is typically via username/password or tokens.

</details>

### Question 28
How does Kubernetes authenticate to private container registries?

A) Using SSH keys stored in Pods
B) Using imagePullSecrets referenced in Pod specifications
C) Through automatic cloud provider integration only
D) Private registries are not supported

<details><summary>Answer</summary>

**B) Using imagePullSecrets referenced in Pod specifications**

Kubernetes authenticates to private registries using imagePullSecrets, which reference Kubernetes Secrets containing registry credentials. These secrets are attached to Pods or ServiceAccounts. Cloud providers may also offer automatic authentication through workload identity or instance metadata.

</details>

### Question 29
What is an ImagePullSecret?

A) A password stored in the image
B) A Kubernetes Secret containing registry credentials
C) An encrypted image layer
D) A token embedded in the container

<details><summary>Answer</summary>

**B) A Kubernetes Secret containing registry credentials**

An ImagePullSecret is a Kubernetes Secret of type `kubernetes.io/dockerconfigjson` that contains registry authentication credentials. It stores the registry URL, username, password, and email in a format compatible with Docker's config.json. Pods reference this secret to pull images from private registries.

</details>

### Question 30
Which field in a Pod spec references credentials for pulling private images?

A) registryCredentials
B) imageSecrets
C) imagePullSecrets
D) pullCredentials

<details><summary>Answer</summary>

**C) imagePullSecrets**

The `imagePullSecrets` field in a Pod spec is an array of references to Secrets containing registry credentials. It can also be configured on a ServiceAccount to automatically apply to all Pods using that ServiceAccount.

</details>

### Question 31
What is the purpose of the imagePullPolicy field in a container spec?

A) To specify the registry URL
B) To control when the kubelet should pull the container image
C) To set image compression options
D) To define image security policies

<details><summary>Answer</summary>

**B) To control when the kubelet should pull the container image**

The imagePullPolicy determines when the kubelet pulls the container image. Options are: `Always` (pull every time), `IfNotPresent` (pull only if not cached locally), and `Never` (use only locally cached images). This affects startup time and ensures you're running the expected image version.

</details>

### Question 32
When is an image pulled if imagePullPolicy is set to 'IfNotPresent'?

A) Always, on every Pod start
B) Only if the image is not already present on the node
C) Never, images must be pre-loaded
D) Only during cluster initialization

<details><summary>Answer</summary>

**B) Only if the image is not already present on the node**

With `IfNotPresent`, the kubelet checks if the image exists locally before pulling. If cached, the local image is used; if not, it's pulled from the registry. This is the default policy for images with specific tags (not `latest`) and improves startup time.

</details>

### Question 33
What imagePullPolicy is automatically applied when using the 'latest' tag?

A) Never
B) IfNotPresent
C) Always
D) OnFailure

<details><summary>Answer</summary>

**C) Always**

When using the `latest` tag (or no tag at all), Kubernetes defaults to `imagePullPolicy: Always`. This ensures you get the most recent version of the image, since 'latest' can change over time. For other specific tags, the default is `IfNotPresent`.

</details>

### Question 34
What happens when imagePullPolicy is set to 'Never'?

A) The image is pulled on every Pod start
B) The kubelet never pulls the image and uses only locally available images
C) The Pod fails if the image is not cached
D) Both B and C are correct

<details><summary>Answer</summary>

**D) Both B and C are correct**

With `imagePullPolicy: Never`, the kubelet never attempts to pull the image from a registry. It only uses images that already exist locally on the node. If the image isn't present, the container fails with an ErrImageNeverPull error. This is useful for air-gapped environments or when using pre-loaded images.

</details>

### Question 35
How can you configure a default imagePullPolicy for all containers in a namespace?

A) Using a namespace annotation
B) Using an AlwaysPullImages admission controller
C) Using a ConfigMap
D) It cannot be configured at the namespace level

<details><summary>Answer</summary>

**B) Using an AlwaysPullImages admission controller**

The AlwaysPullImages admission controller can be enabled to force all Pods to use `imagePullPolicy: Always`. While this is cluster-wide, it ensures images are always verified against the registry. There's no built-in namespace-level default, but policy engines like Kyverno or Gatekeeper can enforce specific policies per namespace.

</details>

## Building Container Images

### Question 36
What is a Dockerfile?

A) A running container configuration
B) A text file containing instructions for building a container image
C) A container log file
D) A registry configuration file

<details><summary>Answer</summary>

**B) A text file containing instructions for building a container image**

A Dockerfile is a text file containing a series of instructions for building a container image. Each instruction (FROM, RUN, COPY, etc.) creates a layer in the image. Docker reads the Dockerfile and executes the instructions sequentially to produce the final image.

</details>

### Question 37
Which Dockerfile instruction sets the base image for subsequent instructions?

A) BASE
B) IMAGE
C) FROM
D) SOURCE

<details><summary>Answer</summary>

**C) FROM**

The FROM instruction specifies the base image for the build. It must be the first instruction in a Dockerfile (except for ARG). You can use FROM with an image name and tag (e.g., `FROM alpine:3.18`) or with `FROM scratch` to build from an empty image.

</details>

### Question 38
What is the purpose of the RUN instruction in a Dockerfile?

A) To start the container
B) To execute commands during the image build process
C) To define the container's entry point
D) To copy files into the image

<details><summary>Answer</summary>

**B) To execute commands during the image build process**

The RUN instruction executes commands in a new layer on top of the current image and commits the results. It's commonly used to install packages, download files, or configure the environment. Each RUN instruction creates a new layer in the image.

</details>

### Question 39
How does the COPY instruction differ from ADD in a Dockerfile?

A) COPY is deprecated in favor of ADD
B) COPY only copies local files, while ADD can also extract archives and fetch URLs
C) ADD only works with text files
D) They are identical in functionality

<details><summary>Answer</summary>

**B) COPY only copies local files, while ADD can also extract archives and fetch URLs**

COPY is a straightforward file copy from the build context to the image. ADD has additional features: it can automatically extract tar archives and fetch files from URLs. Best practice is to use COPY unless you specifically need ADD's extra features, as COPY is more transparent.

</details>

### Question 40
What is the purpose of the ENTRYPOINT instruction?

A) To set the working directory
B) To configure the container to run as an executable
C) To expose network ports
D) To define environment variables

<details><summary>Answer</summary>

**B) To configure the container to run as an executable**

ENTRYPOINT configures the container to run as an executable, defining the main command that runs when the container starts. Unlike CMD, ENTRYPOINT arguments are not easily overridden at runtime (you need `--entrypoint` flag). It's typically used to set the main application or script to run.

</details>

### Question 41
How does CMD differ from ENTRYPOINT in a Dockerfile?

A) CMD cannot be overridden at runtime
B) CMD provides default arguments that can be overridden, while ENTRYPOINT defines the main executable
C) ENTRYPOINT is deprecated
D) They serve identical purposes

<details><summary>Answer</summary>

**B) CMD provides default arguments that can be overridden, while ENTRYPOINT defines the main executable**

CMD specifies default arguments for the container that can be easily overridden by providing arguments at runtime. ENTRYPOINT defines the main executable and is harder to override. When both are used together, CMD provides default arguments to the ENTRYPOINT command.

</details>

### Question 42
What happens when both ENTRYPOINT and CMD are specified?

A) CMD is ignored
B) ENTRYPOINT is ignored
C) CMD provides default arguments to ENTRYPOINT
D) The build fails

<details><summary>Answer</summary>

**C) CMD provides default arguments to ENTRYPOINT**

When both ENTRYPOINT and CMD are specified, the CMD values are appended to the ENTRYPOINT as default arguments. For example, `ENTRYPOINT ["python"]` with `CMD ["app.py"]` results in running `python app.py`. Runtime arguments replace CMD but not ENTRYPOINT.

</details>

### Question 43
What is the purpose of the WORKDIR instruction?

A) To mount a volume
B) To set the working directory for subsequent instructions
C) To define the container's home directory
D) To specify the build context

<details><summary>Answer</summary>

**B) To set the working directory for subsequent instructions**

WORKDIR sets the working directory for subsequent RUN, CMD, ENTRYPOINT, COPY, and ADD instructions. If the directory doesn't exist, it's created automatically. Using WORKDIR is preferred over `RUN cd /path` because it affects all subsequent instructions and makes the Dockerfile more readable.

</details>

### Question 44
How does the ENV instruction work in a Dockerfile?

A) It sets environment variables that persist in the built image
B) It only sets variables during build time
C) It encrypts sensitive data
D) It imports environment from the host

<details><summary>Answer</summary>

**A) It sets environment variables that persist in the built image**

ENV sets environment variables that are available both during the build process and when the container runs. These variables persist in the final image and can be overridden at runtime using `-e` or `--env`. Common uses include setting application configuration, paths, and versions.

</details>

### Question 45
What is a multi-stage build in Docker?

A) Building multiple images in parallel
B) A build using multiple FROM statements to create intermediate images and copy artifacts
C) Building images across multiple registries
D) A distributed build system

<details><summary>Answer</summary>

**B) A build using multiple FROM statements to create intermediate images and copy artifacts**

Multi-stage builds use multiple FROM statements in a single Dockerfile. Each FROM starts a new build stage. You can selectively copy artifacts from one stage to another using `COPY --from=stage`. This allows you to build in one stage (with build tools) and copy only the final artifacts to a clean runtime stage.

</details>

### Question 46
What is the primary benefit of multi-stage builds?

A) Faster build times
B) Smaller final images by excluding build tools and dependencies
C) Better security through encryption
D) Automatic versioning

<details><summary>Answer</summary>

**B) Smaller final images by excluding build tools and dependencies**

Multi-stage builds produce smaller final images by separating the build environment from the runtime environment. Build tools, compilers, and intermediate files stay in the build stage and are not included in the final image. Only the compiled artifacts are copied to a minimal runtime image.

</details>

### Question 47
What is the purpose of the ARG instruction in a Dockerfile?

A) To define arguments passed to CMD
B) To define build-time variables that can be passed using --build-arg
C) To specify command-line arguments
D) To set runtime environment variables

<details><summary>Answer</summary>

**B) To define build-time variables that can be passed using --build-arg**

ARG defines variables that users can pass at build-time using `docker build --build-arg NAME=value`. ARG values are only available during the build, not at runtime. They're useful for parameterizing builds with versions, configurations, or credentials (though secrets should be handled carefully).

</details>

### Question 48
How does ARG differ from ENV in a Dockerfile?

A) ARG values persist in the final image, ENV values do not
B) ARG is available only during build, ENV persists in the running container
C) They are interchangeable
D) ARG is for secrets, ENV is for configuration

<details><summary>Answer</summary>

**B) ARG is available only during build, ENV persists in the running container**

ARG values are only available during the image build process and are not saved in the final image. ENV values persist in the built image and are available both during build and at container runtime. If you need a build-time value at runtime, you can use `ENV VAR=${ARG_VAR}` to transfer it.

</details>

### Question 49
What is the purpose of the EXPOSE instruction?

A) To open ports on the host system
B) To document which ports the container listens on
C) To configure firewall rules
D) To enable network connectivity

<details><summary>Answer</summary>

**B) To document which ports the container listens on**

EXPOSE is primarily documentation - it indicates which ports the container listens on but doesn't actually publish them. To make ports accessible, you must use `-p` flag at runtime or publish them via Kubernetes Services. EXPOSE helps users understand which ports the application uses.

</details>

### Question 50
What is a .dockerignore file used for?

A) To list images that should not be pulled
B) To exclude files and directories from the build context
C) To ignore certain Dockerfile instructions
D) To prevent container execution

<details><summary>Answer</summary>

**B) To exclude files and directories from the build context**

A .dockerignore file specifies patterns for files and directories that should be excluded from the build context sent to the Docker daemon. This speeds up builds, reduces image size, and prevents sensitive files (like .git, node_modules, or secrets) from accidentally being included in images.

</details>

## Container Image Best Practices

### Question 51
Why should you use specific image tags instead of 'latest' in production?

A) 'latest' images are slower
B) Specific tags ensure reproducibility and prevent unexpected changes
C) 'latest' is not supported in Kubernetes
D) Specific tags are more secure

### Question 52
What is the recommended practice for base image selection?

A) Always use the largest image for completeness
B) Use official, minimal, and regularly updated base images
C) Build base images from scratch for every project
D) Use the same base image for all applications

### Question 53
Why are minimal base images like Alpine or distroless recommended?

A) They are easier to debug
B) They reduce attack surface and image size
C) They include more features
D) They are required by Kubernetes

### Question 54
What is a distroless container image?

A) An image without any operating system
B) An image containing only the application and its runtime dependencies, without package managers or shells
C) An image that works on any Linux distribution
D) An uncompressed image format

### Question 55
How can you reduce the number of layers in a container image?

A) Use more FROM statements
B) Combine multiple RUN commands using && in a single RUN instruction
C) Add more COPY instructions
D) Use larger base images

### Question 56
Why should you avoid running containers as root?

A) Root containers are slower
B) It minimizes the potential damage from container breakout or compromise
C) Root is not supported in Kubernetes
D) Root containers use more memory

### Question 57
What Dockerfile instruction creates a non-root user?

A) ADDUSER
B) RUN useradd or RUN adduser
C) CREATEUSER
D) NEWUSER

### Question 58
What is the purpose of the USER instruction in a Dockerfile?

A) To authenticate with a registry
B) To set the user (and optionally group) for running subsequent instructions and the container
C) To create user directories
D) To set file permissions

### Question 59
Why should sensitive data like secrets never be included in container images?

A) It slows down image builds
B) Images can be inspected, and secrets would be exposed in layer history
C) Secrets are not supported in containers
D) It increases image size

### Question 60
What is the recommended approach for handling secrets in containers?

A) Embed them in environment variables in the Dockerfile
B) Use Kubernetes Secrets or external secret management systems
C) Store them in a ConfigMap
D) Include them in the image with encryption

### Question 61
How can you verify the security of container images?

A) Check the image size
B) Scan images for vulnerabilities using security scanning tools
C) Verify the image is from Docker Hub
D) Check the number of layers

### Question 62
What is container image scanning?

A) Converting images to different formats
B) Analyzing images for known vulnerabilities, misconfigurations, and compliance issues
C) Compressing image layers
D) Validating image signatures

### Question 63
What is image signing and verification?

A) Adding watermarks to images
B) Cryptographically signing images to verify their authenticity and integrity
C) Encrypting image contents
D) Compressing images for security

### Question 64
What tool does Kubernetes use for image signature verification?

A) Docker Content Trust
B) Notary
C) Sigstore/cosign with policy controllers like Kyverno or OPA Gatekeeper
D) GPG

### Question 65
What is the purpose of a Software Bill of Materials (SBOM) for container images?

A) To list all running containers
B) To provide a comprehensive inventory of all components, libraries, and dependencies in an image
C) To track container costs
D) To monitor container performance

## Container Lifecycle

### Question 66
What are the possible states of a container in Kubernetes?

A) Starting, Running, Stopping
B) Waiting, Running, Terminated
C) Created, Active, Deleted
D) Init, Execute, Complete

### Question 67
What does the 'Waiting' container state indicate?

A) The container is running but idle
B) The container is not yet running, possibly pulling images or waiting for dependencies
C) The container is paused
D) The container is being debugged

### Question 68
What causes a container to be in the 'Running' state?

A) The container image has been pulled
B) The container has been created and its main process is executing
C) The container is scheduled to a node
D) The container has completed its task

### Question 69
What does the 'Terminated' container state indicate?

A) The container is temporarily paused
B) The container ran to completion or failed
C) The container is being restarted
D) The container is waiting for resources

### Question 70
What is the container restart policy in Kubernetes?

A) A setting that controls how often containers are updated
B) A policy that determines when and if Kubernetes should restart a failed container
C) A schedule for container maintenance
D) A backup policy for container data

### Question 71
What happens when restartPolicy is set to 'Always'?

A) Containers are never restarted
B) Containers are restarted regardless of exit status
C) Containers are only restarted on failure
D) Containers are restarted once per day

### Question 72
When would you use restartPolicy 'OnFailure'?

A) For long-running services
B) For batch jobs that should retry on failure but not restart on success
C) For containers that should never restart
D) For init containers

### Question 73
What is the purpose of restartPolicy 'Never'?

A) To ensure containers always restart
B) To prevent any container restarts, typically used for one-time jobs
C) To restart containers on a schedule
D) To restart only on specific errors

### Question 74
How does Kubernetes handle container restart backoff?

A) Immediate restarts without delay
B) Exponential backoff starting at 10 seconds, doubling with each restart
C) Fixed 30-second delay between restarts
D) Random delay between restarts

### Question 75
What is the maximum backoff delay for container restarts?

A) 1 minute
B) 5 minutes
C) 10 minutes
D) 30 minutes

## Container Probes

### Question 76
What is the purpose of a liveness probe?

A) To check if the application is ready to serve traffic
B) To determine if the container is running and should be restarted if unhealthy
C) To validate container configuration
D) To measure container performance

### Question 77
What happens when a liveness probe fails?

A) The container is marked as not ready
B) The kubelet kills the container, and it is restarted based on the restart policy
C) The Pod is deleted
D) Traffic is redirected to other Pods

### Question 78
What is the purpose of a readiness probe?

A) To determine if the container should be restarted
B) To determine if the container is ready to accept traffic
C) To check if the image was pulled correctly
D) To validate container security

### Question 79
What happens when a readiness probe fails?

A) The container is restarted
B) The container's Pod IP is removed from Service endpoints
C) The Pod is deleted
D) The node is marked as unhealthy

### Question 80
What is the purpose of a startup probe?

A) To check if the container started with correct arguments
B) To allow slow-starting containers time to initialize before liveness probes take over
C) To validate the container image
D) To check network connectivity

### Question 81
How does a startup probe interact with liveness and readiness probes?

A) They all run simultaneously
B) Liveness and readiness probes are disabled until the startup probe succeeds
C) Startup probe replaces liveness probe
D) They are mutually exclusive

### Question 82
What are the three types of probe mechanisms in Kubernetes?

A) HTTP, TCP, UDP
B) exec, httpGet, tcpSocket
C) REST, gRPC, WebSocket
D) ping, curl, telnet

### Question 83
How does an HTTP probe work?

A) It sends a TCP packet to a port
B) It performs an HTTP GET request to a specified path and port
C) It executes a command inside the container
D) It checks DNS resolution

### Question 84
What constitutes a successful HTTP probe response?

A) Any response from the server
B) HTTP status code between 200 and 399
C) HTTP status code 200 only
D) Response within 1 second

### Question 85
How does a TCP probe work?

A) It sends an HTTP request
B) It attempts to open a TCP connection to a specified port
C) It executes a command inside the container
D) It checks UDP connectivity

### Question 86
What is an exec probe?

A) A probe that executes an HTTP request
B) A probe that runs a command inside the container
C) A probe that checks file existence
D) A probe that monitors CPU usage

### Question 87
What determines success for an exec probe?

A) The command produces output
B) The command exits with status code 0
C) The command runs within the timeout
D) The command doesn't produce errors

### Question 88
What is the initialDelaySeconds parameter in a probe configuration?

A) The time between probe checks
B) The time to wait before starting the first probe after container start
C) The maximum probe duration
D) The delay between failed probes

### Question 89
What is the periodSeconds parameter in a probe configuration?

A) The initial delay before probing
B) How often to perform the probe
C) The timeout for each probe
D) The total probe duration

### Question 90
What is the timeoutSeconds parameter in a probe configuration?

A) The initial delay before probing
B) How long to wait for a probe response before considering it failed
C) The time between probe attempts
D) The maximum container runtime

### Question 91
What is the failureThreshold parameter in a probe configuration?

A) The number of times a probe can fail before taking action
B) The percentage of acceptable failures
C) The maximum number of probe attempts
D) The error code threshold

### Question 92
What is the successThreshold parameter in a probe configuration?

A) The number of successes needed to mark a container as healthy after a failure
B) The percentage of successful probes required
C) The response time threshold
D) The minimum uptime requirement

### Question 93
Which probe type supports gRPC health checking?

A) Only httpGet
B) Only exec
C) grpc (native gRPC health checking)
D) gRPC is not supported in probes

### Question 94
What is a common mistake when configuring liveness probes?

A) Using HTTP probes
B) Setting too aggressive timing that restarts containers during normal operation
C) Probing on port 80
D) Using the same probe for multiple containers

### Question 95
Why should readiness probes not have the same endpoint as liveness probes?

A) It's technically not allowed
B) Different checks may be needed - readiness for dependencies, liveness for process health
C) It causes probe conflicts
D) It increases network traffic

## Multi-Container Pods

### Question 96
What is a sidecar container?

A) The main application container
B) A helper container that runs alongside the main container to provide supporting features
C) A container that runs before the main container
D) A backup container

### Question 97
What is a common use case for sidecar containers?

A) Running the primary application
B) Log collection, proxying, or syncing data
C) Database hosting
D) Load balancing across clusters

### Question 98
What is an init container?

A) A container that runs continuously alongside the main container
B) A container that runs to completion before the main containers start
C) The first container listed in the Pod spec
D) A container that initializes the cluster

### Question 99
How do init containers differ from regular containers?

A) Init containers don't have resource limits
B) Init containers run to completion sequentially before app containers start
C) Init containers share the same image as app containers
D) Init containers can access host resources directly

### Question 100
In what order do init containers execute?

A) In parallel for faster startup
B) Sequentially in the order they are defined
C) In alphabetical order by name
D) In random order

### Question 101
What happens if an init container fails?

A) The Pod continues with remaining init containers
B) The Pod is restarted (init containers run again) based on restartPolicy
C) Only the failed init container is restarted
D) The Pod is deleted immediately

### Question 102
What is the ambassador container pattern?

A) A pattern where a container handles security
B) A pattern where a sidecar proxies network connections to external services
C) A pattern for cross-cluster communication
D) A pattern for container orchestration

### Question 103
What is the adapter container pattern?

A) A pattern for database connections
B) A pattern where a sidecar transforms or adapts output from the main container
C) A pattern for hardware abstraction
D) A pattern for network configuration

### Question 104
How do containers within the same Pod communicate?

A) Through Kubernetes Services
B) Through localhost, as they share the network namespace
C) Through external message queues
D) Through shared ConfigMaps

### Question 105
What resources can containers in the same Pod share?

A) Only network namespace
B) Network namespace, IPC namespace, and volumes
C) All namespaces including PID by default
D) Nothing, containers are fully isolated

### Question 106
What is a sidecar container in Kubernetes 1.28+?

A) A deprecated container type
B) A container with restartPolicy: Always in an init container definition
C) A container that runs in a separate Pod
D) A container managed by a DaemonSet

### Question 107
How is a native sidecar container defined in Kubernetes?

A) Using a special sidecar field in the Pod spec
B) As an init container with restartPolicy: Always
C) Using a Sidecar custom resource
D) Through a sidecar annotation

### Question 108
What is the lifecycle behavior of native sidecar containers?

A) They run only during initialization
B) They start before and run throughout the lifetime of regular containers
C) They run after main containers complete
D) They run on a schedule

### Question 109
What is an ephemeral container?

A) A container with limited resources
B) A temporary container added to a running Pod for debugging
C) A container that runs for a short time
D) A container without persistent storage

### Question 110
When would you use an ephemeral container?

A) For production workloads
B) For troubleshooting running Pods that lack debugging utilities
C) For running batch jobs
D) For init processes

## Container Resources

### Question 111
What are container resource requests in Kubernetes?

A) The maximum resources a container can use
B) The minimum resources guaranteed to a container for scheduling purposes
C) The current resource usage
D) The default resource allocation

### Question 112
What are container resource limits in Kubernetes?

A) The minimum resources required
B) The maximum resources a container is allowed to use
C) Soft limits that can be exceeded
D) Cluster-wide resource quotas

### Question 113
How does Kubernetes use resource requests for scheduling?

A) Requests are ignored during scheduling
B) The scheduler ensures the node has enough allocatable resources to meet requests
C) Requests are used only for billing
D) Requests determine Pod priority

### Question 114
What happens when a container exceeds its memory limit?

A) The container is throttled
B) The container is terminated (OOMKilled)
C) Memory is borrowed from other containers
D) The limit is automatically increased

### Question 115
What happens when a container exceeds its CPU limit?

A) The container is terminated
B) The container is CPU-throttled
C) CPU is borrowed from other containers
D) The Pod is evicted

### Question 116
What is the difference between CPU and memory limit enforcement?

A) Both are enforced the same way
B) CPU is throttled (compressible), memory excess causes termination (incompressible)
C) Memory is throttled, CPU causes termination
D) Neither is enforced strictly

### Question 117
What are the units for CPU resources in Kubernetes?

A) Percentage only
B) Cores or millicores (m)
C) GHz
D) Threads

### Question 118
What does '500m' mean for CPU resources?

A) 500 megabytes
B) 500 millicores, equivalent to 0.5 CPU cores
C) 500 minutes of CPU time
D) 500 milliwatts

### Question 119
What are the units for memory resources in Kubernetes?

A) Percentage only
B) Bytes, Ki, Mi, Gi (powers of 2) or K, M, G (powers of 10)
C) Pages
D) Sectors

### Question 120
What is the difference between Mi and M for memory units?

A) They are identical
B) Mi is mebibytes (1024^2), M is megabytes (1000^2)
C) M is larger than Mi
D) Mi is deprecated

### Question 121
What is a QoS class in Kubernetes?

A) A network quality setting
B) A classification that affects scheduling and eviction priority
C) A storage performance tier
D) A service level agreement

### Question 122
When is a Pod assigned the 'Guaranteed' QoS class?

A) When any container has resource requests
B) When every container has equal requests and limits set for both CPU and memory
C) When the Pod has high priority
D) When using premium storage

### Question 123
When is a Pod assigned the 'Burstable' QoS class?

A) When no resources are specified
B) When at least one container has a request or limit, but doesn't meet Guaranteed criteria
C) When CPU limits exceed requests
D) When using ephemeral storage

### Question 124
When is a Pod assigned the 'BestEffort' QoS class?

A) When all containers have limits
B) When no containers have resource requests or limits specified
C) When using guaranteed storage
D) When the Pod has the highest priority

### Question 125
How does QoS class affect eviction priority?

A) QoS has no effect on eviction
B) BestEffort Pods are evicted first, then Burstable, then Guaranteed
C) Guaranteed Pods are evicted first
D) Eviction is random regardless of QoS

## Container Configuration

### Question 126
How can you pass environment variables to a container?

A) Only through ConfigMaps
B) Through env field, ConfigMaps, Secrets, or downward API
C) Only through command-line arguments
D) Environment variables cannot be passed

### Question 127
What is a ConfigMap in Kubernetes?

A) A network configuration resource
B) An API object for storing non-confidential configuration data as key-value pairs
C) A storage volume type
D) A deployment strategy

### Question 128
How can ConfigMap data be exposed to containers?

A) Only as files
B) As environment variables or mounted as files in a volume
C) Only as environment variables
D) Through command-line arguments only

### Question 129
What is a Secret in Kubernetes?

A) An encrypted ConfigMap
B) An object for storing sensitive data like passwords, tokens, and keys
C) A hidden volume
D) An authentication mechanism

### Question 130
How are Secrets different from ConfigMaps?

A) Secrets are encrypted at rest by default
B) Secrets are base64-encoded and intended for sensitive data, with optional encryption at rest
C) Secrets can only store strings
D) Secrets have size limits, ConfigMaps don't

### Question 131
How can Secret data be exposed to containers?

A) Only as environment variables
B) As environment variables or mounted as files in a volume
C) Only as files
D) Secrets cannot be exposed to containers

### Question 132
What is the envFrom field used for?

A) To export environment variables
B) To load all key-value pairs from a ConfigMap or Secret as environment variables
C) To read environment from a file
D) To copy environment between containers

### Question 133
How can you reference a specific key from a ConfigMap as an environment variable?

A) Using configMapRef
B) Using configMapKeyRef in the valueFrom field
C) Using configMapValue
D) Using configKey

### Question 134
What is a volume mount in a container?

A) A network share
B) A path in the container's filesystem where a volume is attached
C) A storage device
D) A backup location

### Question 135
How do you mount a ConfigMap as a volume?

A) Using a hostPath volume
B) Using a configMap volume type and mounting it at a container path
C) Using a configMount field
D) Using an emptyDir volume

### Question 136
What is the command field in a container spec?

A) The working directory
B) The entrypoint that overrides the image's ENTRYPOINT
C) Arguments to the entrypoint
D) A post-start command

### Question 137
What is the args field in a container spec?

A) The entrypoint command
B) Arguments passed to the command (entrypoint), overriding CMD
C) Environment variables
D) Volume mount options

### Question 138
How do command and args override Dockerfile ENTRYPOINT and CMD?

A) They don't, Dockerfile instructions take precedence
B) command overrides ENTRYPOINT, args overrides CMD
C) command overrides CMD, args overrides ENTRYPOINT
D) Both override CMD only

### Question 139
What is a container's working directory?

A) The directory where logs are stored
B) The current directory when the container's process starts
C) The directory where the image is stored
D) The mount point for volumes

### Question 140
How can you override a container's working directory in Kubernetes?

A) Using the directory field
B) Using the workingDir field in the container spec
C) Using an environment variable
D) Using a volume mount

## Container Security

### Question 141
What is a SecurityContext in Kubernetes?

A) A firewall configuration
B) Settings that define privilege and access control for Pods and containers
C) A network policy
D) An authentication token

### Question 142
What does the runAsUser field specify?

A) The container's hostname
B) The UID to run the container's entrypoint process as
C) The user that created the Pod
D) The service account name

### Question 143
What does the runAsNonRoot field enforce?

A) Running as user ID 0
B) That the container must run as a non-root user (UID != 0)
C) Using a non-root filesystem
D) Disabling privileged mode

### Question 144
What is the readOnlyRootFilesystem setting?

A) A backup option
B) A setting that mounts the container's root filesystem as read-only
C) A storage encryption option
D) A log rotation setting

### Question 145
What are Linux capabilities in the context of containers?

A) Hardware features
B) Fine-grained privileges that can be granted or removed from processes
C) Container resource limits
D) Network permissions

### Question 146
How can you drop Linux capabilities from a container?

A) Using runAsNonRoot
B) Using securityContext.capabilities.drop
C) Using privileged: false
D) Using readOnlyRootFilesystem

### Question 147
What capability is required to bind to ports below 1024?

A) NET_RAW
B) NET_BIND_SERVICE
C) SYS_ADMIN
D) NET_ADMIN

### Question 148
What is a privileged container?

A) A container with resource limits
B) A container with almost all root capabilities and access to host resources
C) A container running as root
D) A container with network access

### Question 149
Why should privileged containers be avoided?

A) They are slower
B) They can compromise the host system if the container is compromised
C) They use more memory
D) They are deprecated

### Question 150
What is allowPrivilegeEscalation?

A) A Pod priority setting
B) A setting that controls whether a process can gain more privileges than its parent
C) A resource limit
D) A network policy

### Question 151
What is the purpose of the seccompProfile field?

A) To set SELinux options
B) To define a seccomp profile that filters system calls
C) To configure AppArmor
D) To set resource limits

### Question 152
What is the RuntimeDefault seccomp profile?

A) A custom profile
B) The container runtime's default seccomp profile that blocks dangerous syscalls
C) No restrictions
D) A Kubernetes-specific profile

### Question 153
What is AppArmor in the context of container security?

A) A container runtime
B) A Linux security module that restricts program capabilities with profiles
C) A Kubernetes admission controller
D) A network policy

### Question 154
How do you apply an AppArmor profile to a container?

A) Using a securityContext field
B) Using an annotation on the Pod
C) Using a ConfigMap
D) Using a custom resource

### Question 155
What is SELinux in the context of container security?

A) A container format
B) A mandatory access control system that enforces security policies
C) A Kubernetes feature
D) A container runtime

### Question 156
How can you set SELinux options for a container?

A) Using an annotation
B) Using securityContext.seLinuxOptions
C) Using a ConfigMap
D) Using environment variables

### Question 157
What is a Pod Security Standard?

A) A performance benchmark
B) A set of policies defining security best practices at different levels
C) A container format specification
D) A network security protocol

### Question 158
What are the three Pod Security Standard levels?

A) Low, Medium, High
B) Privileged, Baseline, Restricted
C) Basic, Standard, Advanced
D) Open, Controlled, Locked

### Question 159
What does the Privileged Pod Security Standard allow?

A) Only non-root containers
B) Unrestricted policy, allowing known privilege escalations
C) No network access
D) Read-only filesystems only

### Question 160
What does the Baseline Pod Security Standard restrict?

A) All capabilities
B) Known privilege escalations while allowing common configurations
C) All root users
D) All volume mounts

## Container Networking

### Question 161
What network namespace do containers in a Pod share?

A) Each container has its own network namespace
B) All containers share the same network namespace
C) Only init containers share the namespace
D) Network namespaces are optional

### Question 162
How do containers in the same Pod communicate with each other?

A) Through Kubernetes Services
B) Through localhost, as they share the same network namespace
C) Through environment variables
D) Through shared volumes

### Question 163
What is the pause container?

A) A container that pauses other containers
B) An infrastructure container that holds the network namespace for the Pod
C) A debugging container
D) A resource-saving container

### Question 164
What role does the pause container play in Pod networking?

A) It routes traffic between Pods
B) It holds the network namespace that other containers in the Pod join
C) It provides DNS services
D) It manages firewall rules

### Question 165
How do containers expose ports in Kubernetes?

A) Ports are automatically exposed
B) Through the containerPort field in the container spec
C) Through firewall rules
D) Through the Service object only

### Question 166
What is the containerPort field used for?

A) To open ports on the host
B) To document and expose the port the container listens on
C) To configure firewall rules
D) To set up port forwarding

### Question 167
What is the hostPort field used for?

A) To expose container ports only within the Pod
B) To map a container port directly to a port on the host node
C) To configure Service ports
D) To set DNS resolution

### Question 168
Why should hostPort be avoided in most cases?

A) It's deprecated
B) It limits Pod scheduling and can cause port conflicts
C) It's slower than Services
D) It doesn't work with CNI plugins

### Question 169
What is the protocol field in containerPort?

A) The application protocol
B) The network protocol (TCP, UDP, or SCTP) for the port
C) The authentication protocol
D) The encryption protocol

### Question 170
How does a Service route traffic to container ports?

A) Through hostPort
B) Through selectors matching Pod labels and targetPort mapping
C) Through direct container connections
D) Through shared volumes

## Container Logging and Debugging

### Question 171
Where do container logs go by default in Kubernetes?

A) To a central logging system
B) To stdout and stderr, captured by the container runtime
C) To a log file in the container
D) To the Kubernetes API server

### Question 172
How does kubectl logs retrieve container logs?

A) By reading files from the container
B) By requesting logs from the kubelet, which gets them from the container runtime
C) By querying a logging database
D) By accessing the API server logs

### Question 173
What happens to container logs when a container restarts?

A) Logs are preserved indefinitely
B) Previous logs can be viewed with --previous flag, current container gets new logs
C) All logs are deleted
D) Logs are automatically backed up

### Question 174
How can you view logs from a previous container instance?

A) Using kubectl logs --history
B) Using kubectl logs --previous
C) Using kubectl logs --old
D) Using kubectl logs --backup

### Question 175
What is the recommended logging approach for containers?

A) Write logs to files inside the container
B) Write logs to stdout/stderr for collection by the logging infrastructure
C) Send logs directly to an external system
D) Store logs in a database

### Question 176
What is a logging sidecar container?

A) A container that processes application logs
B) A helper container that collects and forwards logs from the main container
C) A container for log analysis
D) A container that stores log files

### Question 177
How can you debug a running container?

A) Restart the container
B) Use kubectl exec to run commands or kubectl debug for troubleshooting
C) Check the Dockerfile
D) Redeploy the Pod

### Question 178
What does kubectl exec do?

A) Creates a new container
B) Executes a command inside a running container
C) Stops a container
D) Copies files to a container

### Question 179
How can you get an interactive shell in a container?

A) kubectl run
B) kubectl exec -it <pod> -- /bin/sh (or /bin/bash)
C) kubectl shell
D) kubectl connect

### Question 180
What is kubectl debug used for?

A) Viewing logs
B) Creating ephemeral containers or debug copies of Pods for troubleshooting
C) Setting breakpoints
D) Monitoring performance

### Question 181
How can you debug a container that crashes immediately?

A) Only by checking logs
B) Using kubectl debug to add a debug container or creating a copy with different commands
C) By increasing resource limits
D) By changing the restart policy

### Question 182
What is a debug container?

A) A container with debugging tools
B) An ephemeral container added to a running Pod for troubleshooting
C) A container in debug mode
D) A test container

### Question 183
How can you inspect container resource usage?

A) Using kubectl describe only
B) Using kubectl top pod (requires metrics-server)
C) Using kubectl resources
D) Using kubectl monitor

### Question 184
What does kubectl top pod show?

A) Pod configuration
B) Current CPU and memory usage of Pods and their containers
C) Historical resource data
D) Resource requests and limits

### Question 185
How can you view container events?

A) Using kubectl events
B) Using kubectl describe pod, which shows events in the Events section
C) Using kubectl logs
D) Using kubectl get containers

## Advanced Container Concepts

### Question 186
What is a container hook in Kubernetes?

A) A network callback
B) A lifecycle event handler that runs code at specific container lifecycle points
C) A security feature
D) A monitoring probe

### Question 187
What is the PostStart hook?

A) A hook that runs after the container stops
B) A hook that runs immediately after a container is created
C) A cleanup hook
D) A scheduling hook

### Question 188
What is the PreStop hook?

A) A hook that runs before container creation
B) A hook that runs before a container is terminated
C) A startup hook
D) A pause hook

### Question 189
How are container hooks executed?

A) In a separate container
B) Inside the container using exec or HTTP handlers
C) On the host node
D) By the Kubernetes API server

### Question 190
What happens if a PostStart hook fails?

A) The container continues running
B) The container is killed
C) The hook is retried
D) The Pod is rescheduled

### Question 191
What is the terminationGracePeriodSeconds field?

A) The time a container can run
B) The time Kubernetes waits for a Pod to terminate gracefully before force-killing
C) The startup timeout
D) The probe timeout

### Question 192
What happens when a Pod is terminated?

A) Containers are killed immediately
B) SIGTERM is sent, PreStop hooks run, then SIGKILL after grace period
C) Only SIGKILL is sent
D) Containers are paused

### Question 193
What is the SIGTERM signal used for?

A) Immediate termination
B) Graceful shutdown request, allowing the process to clean up
C) Process pause
D) Resource limit notification

### Question 194
What happens after the grace period expires during Pod termination?

A) The Pod waits longer
B) SIGKILL is sent to force-terminate remaining processes
C) The Pod is rescheduled
D) An error is logged but nothing happens

### Question 195
What is container image caching?

A) Compressing images
B) Storing pulled images on nodes to avoid repeated downloads
C) Encrypting images
D) Versioning images

### Question 196
How does image garbage collection work in Kubernetes?

A) Images are never deleted
B) Kubelet removes unused images when disk usage exceeds thresholds
C) Images are deleted after each Pod
D) A separate garbage collector Pod runs

### Question 197
What is the ImagePullBackOff error?

A) An authentication error
B) A state indicating repeated failures to pull an image, with exponential backoff
C) A network timeout
D) A storage error

### Question 198
What causes ErrImagePull errors?

A) Low memory
B) Image not found, authentication failure, or network issues
C) CPU limits exceeded
D) Disk full

### Question 199
What is a container runtime sandbox?

A) A development environment
B) An isolation layer providing additional security between containers and the kernel
C) A test container
D) A resource limit

### Question 200
What is gVisor in the context of container runtimes?

A) A container orchestrator
B) A user-space kernel that provides additional isolation for containers
C) A container registry
D) A monitoring tool
