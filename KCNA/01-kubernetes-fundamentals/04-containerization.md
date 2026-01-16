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

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

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

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

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

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

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

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

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

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

## Container Image Best Practices

### Question 51
Why should you use specific image tags instead of 'latest' in production?

A) 'latest' images are slower
B) Specific tags ensure reproducibility and prevent unexpected changes
C) 'latest' is not supported in Kubernetes
D) Specific tags are more secure

<details><summary>Answer</summary>

**B) Specific tags ensure reproducibility and prevent unexpected changes**

Using specific tags (like v1.2.3) ensures you always deploy the same image version. The 'latest' tag can point to different images over time, leading to unexpected changes, broken deployments, or security issues. Specific tags make deployments reproducible and rollbacks reliable.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 52
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

### Question 53
Why are minimal base images like Alpine or distroless recommended?

A) They are easier to debug
B) They reduce attack surface and image size
C) They include more features
D) They are required by Kubernetes

<details><summary>Answer</summary>

**B) They reduce attack surface and image size**

Minimal base images contain only essential components, reducing the attack surface (fewer packages with potential vulnerabilities) and image size (faster pulls and less storage). Alpine is ~5MB vs ~100MB+ for full OS images. Distroless images are even smaller, containing only the application runtime.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 54
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

### Question 55
How can you reduce the number of layers in a container image?

A) Use more FROM statements
B) Combine multiple RUN commands using && in a single RUN instruction
C) Add more COPY instructions
D) Use larger base images

<details><summary>Answer</summary>

**B) Combine multiple RUN commands using && in a single RUN instruction**

Each Dockerfile instruction creates a layer. Combining commands with `&&` in a single RUN instruction reduces layers and image size. For example: `RUN apt-get update && apt-get install -y pkg && rm -rf /var/lib/apt/lists/*` is better than separate RUN commands.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 56
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

### Question 57
What Dockerfile instruction creates a non-root user?

A) ADDUSER
B) RUN useradd or RUN adduser
C) CREATEUSER
D) NEWUSER

<details><summary>Answer</summary>

**B) RUN useradd or RUN adduser**

To create a non-root user, use the RUN instruction with standard Linux commands: `RUN useradd -r -u 1001 appuser` (for most distros) or `RUN adduser -D appuser` (for Alpine). Then use `USER appuser` to switch to that user for subsequent instructions.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 58
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

### Question 59
Why should sensitive data like secrets never be included in container images?

A) It slows down image builds
B) Images can be inspected, and secrets would be exposed in layer history
C) Secrets are not supported in containers
D) It increases image size

<details><summary>Answer</summary>

**B) Images can be inspected, and secrets would be exposed in layer history**

Container images store all layers, and even if you delete a secret in a later layer, it remains in the previous layer's history. Anyone with access to the image can inspect layers and extract secrets. Use Kubernetes Secrets, environment variables at runtime, or secret management tools instead.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 60
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

### Question 61
How can you verify the security of container images?

A) Check the image size
B) Scan images for vulnerabilities using security scanning tools
C) Verify the image is from Docker Hub
D) Check the number of layers

<details><summary>Answer</summary>

**B) Scan images for vulnerabilities using security scanning tools**

Use vulnerability scanners like Trivy, Grype, Clair, or Snyk to analyze images for known CVEs in packages and dependencies. Integrate scanning into CI/CD pipelines to catch vulnerabilities before deployment. Registry-integrated scanning (like Harbor or cloud registries) provides continuous monitoring.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 62
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

### Question 63
What is image signing and verification?

A) Adding watermarks to images
B) Cryptographically signing images to verify their authenticity and integrity
C) Encrypting image contents
D) Compressing images for security

<details><summary>Answer</summary>

**B) Cryptographically signing images to verify their authenticity and integrity**

Image signing uses cryptographic signatures to verify that an image comes from a trusted source and hasn't been tampered with. Tools like cosign (Sigstore) create signatures that can be verified before deployment, preventing supply chain attacks and ensuring image integrity.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 64
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

### Question 65
What is the purpose of a Software Bill of Materials (SBOM) for container images?

A) To list all running containers
B) To provide a comprehensive inventory of all components, libraries, and dependencies in an image
C) To track container costs
D) To monitor container performance

<details><summary>Answer</summary>

**B) To provide a comprehensive inventory of all components, libraries, and dependencies in an image**

An SBOM is a detailed list of all software components in a container image, including libraries, packages, and their versions. It enables vulnerability tracking, license compliance, and supply chain security. Tools like Syft and SPDX generate SBOMs that can be attached to images.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

## Container Lifecycle

### Question 66
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

### Question 67
What does the 'Waiting' container state indicate?

A) The container is running but idle
B) The container is not yet running, possibly pulling images or waiting for dependencies
C) The container is paused
D) The container is being debugged

<details><summary>Answer</summary>

**B) The container is not yet running, possibly pulling images or waiting for dependencies**

The Waiting state means the container hasn't started yet. Common reasons include: ContainerCreating (setting up), ErrImagePull/ImagePullBackOff (image issues), or waiting for init containers to complete. The reason field provides details about why it's waiting.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 68
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

### Question 69
What does the 'Terminated' container state indicate?

A) The container is temporarily paused
B) The container ran to completion or failed
C) The container is being restarted
D) The container is waiting for resources

<details><summary>Answer</summary>

**B) The container ran to completion or failed**

Terminated means the container finished execution. The state includes exit code (0 for success, non-zero for failure), reason (Completed, Error, OOMKilled, etc.), and timestamps for when it started and finished. The container may be restarted based on restartPolicy.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 70
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

### Question 71
What happens when restartPolicy is set to 'Always'?

A) Containers are never restarted
B) Containers are restarted regardless of exit status
C) Containers are only restarted on failure
D) Containers are restarted once per day

<details><summary>Answer</summary>

**B) Containers are restarted regardless of exit status**

With `restartPolicy: Always` (the default for Pods), containers are restarted whether they exit successfully (code 0) or fail. This is appropriate for long-running services that should always be running. Used by Deployments, StatefulSets, and DaemonSets.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 72
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

### Question 73
What is the purpose of restartPolicy 'Never'?

A) To ensure containers always restart
B) To prevent any container restarts, typically used for one-time jobs
C) To restart containers on a schedule
D) To restart only on specific errors

<details><summary>Answer</summary>

**B) To prevent any container restarts, typically used for one-time jobs**

`Never` prevents any container restarts regardless of exit status. This is used for one-time tasks where you want to see the final state, or when retry logic is handled externally. Common in debugging scenarios or when running ad-hoc commands.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 74
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

### Question 75
What is the maximum backoff delay for container restarts?

A) 1 minute
B) 5 minutes
C) 10 minutes
D) 30 minutes

<details><summary>Answer</summary>

**B) 5 minutes**

The maximum backoff delay is capped at 5 minutes (300 seconds). The exponential backoff (10s, 20s, 40s, 80s, 160s, 300s) stops increasing at 5 minutes. After that, restart attempts continue every 5 minutes until the container starts successfully.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

## Container Probes

### Question 76
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

### Question 77
What happens when a liveness probe fails?

A) The container is marked as not ready
B) The kubelet kills the container, and it is restarted based on the restart policy
C) The Pod is deleted
D) Traffic is redirected to other Pods

<details><summary>Answer</summary>

**B) The kubelet kills the container, and it is restarted based on the restart policy**

When a liveness probe fails (after failureThreshold attempts), the kubelet kills the container. The container is then restarted according to the Pod's restartPolicy. This is more aggressive than readiness probe failure, which only removes traffic.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 78
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

### Question 79
What happens when a readiness probe fails?

A) The container is restarted
B) The container's Pod IP is removed from Service endpoints
C) The Pod is deleted
D) The node is marked as unhealthy

<details><summary>Answer</summary>

**B) The container's Pod IP is removed from Service endpoints**

When a readiness probe fails, the Pod is marked as not ready and its IP is removed from all Service endpoints. Traffic stops being routed to this Pod. The container keeps running and the probe continues checking. When the probe succeeds again, the Pod is added back to endpoints.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 80
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

### Question 81
How does a startup probe interact with liveness and readiness probes?

A) They all run simultaneously
B) Liveness and readiness probes are disabled until the startup probe succeeds
C) Startup probe replaces liveness probe
D) They are mutually exclusive

<details><summary>Answer</summary>

**B) Liveness and readiness probes are disabled until the startup probe succeeds**

When a startup probe is defined, liveness and readiness probes are disabled until the startup probe succeeds. Once the startup probe passes, it's never run again and the regular liveness/readiness probes take over.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 82
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

### Question 83
How does an HTTP probe work?

A) It sends a TCP packet to a port
B) It performs an HTTP GET request to a specified path and port
C) It executes a command inside the container
D) It checks DNS resolution

<details><summary>Answer</summary>

**B) It performs an HTTP GET request to a specified path and port**

HTTP probes send an HTTP GET request to a specified path and port on the container. You configure the path, port, host, HTTP headers, and scheme (HTTP/HTTPS). The probe succeeds if the response status code is between 200 and 399.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 84
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

### Question 85
How does a TCP probe work?

A) It sends an HTTP request
B) It attempts to open a TCP connection to a specified port
C) It executes a command inside the container
D) It checks UDP connectivity

<details><summary>Answer</summary>

**B) It attempts to open a TCP connection to a specified port**

TCP probes attempt to establish a TCP connection to the specified port. If the connection succeeds (the port is open and accepting connections), the probe passes. This is useful for services that don't expose HTTP endpoints, like databases or message queues.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 86
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

### Question 87
What determines success for an exec probe?

A) The command produces output
B) The command exits with status code 0
C) The command runs within the timeout
D) The command doesn't produce errors

<details><summary>Answer</summary>

**B) The command exits with status code 0**

An exec probe succeeds when the command exits with status code 0 (standard Unix success code). Any non-zero exit code is considered a failure. The command's output (stdout/stderr) is ignored for success determination.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 88
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

### Question 89
What is the periodSeconds parameter in a probe configuration?

A) The initial delay before probing
B) How often to perform the probe
C) The timeout for each probe
D) The total probe duration

<details><summary>Answer</summary>

**B) How often to perform the probe**

periodSeconds specifies how frequently the probe is executed. Default is 10 seconds. The probe runs every periodSeconds after the initial delay. Setting this too low increases overhead; too high means slower detection of problems.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 90
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

### Question 91
What is the failureThreshold parameter in a probe configuration?

A) The number of times a probe can fail before taking action
B) The percentage of acceptable failures
C) The maximum number of probe attempts
D) The error code threshold

<details><summary>Answer</summary>

**A) The number of times a probe can fail before taking action**

failureThreshold specifies how many consecutive probe failures are needed before taking action (restart for liveness, mark unready for readiness). Default is 3. This prevents transient failures from triggering actions.

</details>

### Question 92
What is the successThreshold parameter in a probe configuration?

A) The number of successes needed to mark a container as healthy after a failure
B) The percentage of successful probes required
C) The response time threshold
D) The minimum uptime requirement

<details><summary>Answer</summary>

**A) The number of successes needed to mark a container as healthy after a failure**

successThreshold specifies how many consecutive successful probes are needed before the container is considered healthy again (after being marked unhealthy). Default is 1. For liveness and startup probes, this must be 1. For readiness probes, it can be set higher.

</details>

### Question 93
Which probe type supports gRPC health checking?

A) Only httpGet
B) Only exec
C) grpc (native gRPC health checking)
D) gRPC is not supported in probes

<details><summary>Answer</summary>

**C) grpc (native gRPC health checking)**

Kubernetes 1.24+ supports native gRPC health checking as a probe type. You specify the port and optional service name. The probe calls the standard gRPC health checking protocol (grpc.health.v1.Health). This is more efficient than using exec with grpc_health_probe.

</details>

### Question 94
What is a common mistake when configuring liveness probes?

A) Using HTTP probes
B) Setting too aggressive timing that restarts containers during normal operation
C) Probing on port 80
D) Using the same probe for multiple containers

<details><summary>Answer</summary>

**B) Setting too aggressive timing that restarts containers during normal operation**

A common mistake is setting initialDelaySeconds too low or failureThreshold too low, causing containers to be restarted during slow startups or temporary high load. This can create restart loops and cascading failures. Always tune probe timing based on actual application behavior and startup time.

</details>

### Question 95
Why should readiness probes not have the same endpoint as liveness probes?

A) It's technically not allowed
B) Different checks may be needed - readiness for dependencies, liveness for process health
C) It causes probe conflicts
D) It increases network traffic

<details><summary>Answer</summary>

**B) Different checks may be needed - readiness for dependencies, liveness for process health**

Readiness and liveness probes serve different purposes. Liveness checks if the process is alive and should be restarted if it fails. Readiness checks if the app can handle traffic, including verifying dependencies like databases. A failing readiness check (e.g., database down) shouldn't restart the container - it should just stop routing traffic until the issue resolves.

</details>

## Multi-Container Pods

### Question 96
What is a sidecar container?

A) The main application container
B) A helper container that runs alongside the main container to provide supporting features
C) A container that runs before the main container
D) A backup container

<details><summary>Answer</summary>

**B) A helper container that runs alongside the main container to provide supporting features**

A sidecar container runs alongside the main application container in the same Pod, providing supporting functionality. Common use cases include logging agents, proxies (like Envoy in service mesh), file synchronization, and configuration management. Sidecars share the Pod's network and storage resources.

</details>

### Question 97
What is a common use case for sidecar containers?

A) Running the primary application
B) Log collection, proxying, or syncing data
C) Database hosting
D) Load balancing across clusters

<details><summary>Answer</summary>

**B) Log collection, proxying, or syncing data**

Common sidecar use cases include: log collection (Fluentd, Filebeat) to ship logs from the main container, service mesh proxies (Envoy) to handle traffic routing and security, syncing configuration or data from external sources, and providing TLS termination or authentication services.

</details>

### Question 98
What is an init container?

A) A container that runs continuously alongside the main container
B) A container that runs to completion before the main containers start
C) The first container listed in the Pod spec
D) A container that initializes the cluster

<details><summary>Answer</summary>

**B) A container that runs to completion before the main containers start**

Init containers are specialized containers that run before app containers start. They run to completion (exit with status 0) in order. Use cases include waiting for dependencies, setting up configuration files, cloning git repos, or performing database migrations. Main containers won't start until all init containers succeed.

</details>

### Question 99
How do init containers differ from regular containers?

A) Init containers don't have resource limits
B) Init containers run to completion sequentially before app containers start
C) Init containers share the same image as app containers
D) Init containers can access host resources directly

<details><summary>Answer</summary>

**B) Init containers run to completion sequentially before app containers start**

Key differences: init containers run sequentially (one at a time), must complete successfully (exit 0) before the next starts, don't support probes, and are defined in a separate `initContainers` field. They can have different images and access different secrets than app containers. If an init container fails, the Pod restarts (subject to restartPolicy).

</details>

### Question 100
In what order do init containers execute?

A) In parallel for faster startup
B) Sequentially in the order they are defined
C) In alphabetical order by name
D) In random order

<details><summary>Answer</summary>

**B) Sequentially in the order they are defined**

Init containers execute one at a time in the exact order they're listed in the Pod spec's `initContainers` array. Each must complete successfully before the next begins. This sequential execution ensures proper dependency ordering - for example, waiting for a service before downloading configuration that depends on it.

</details>

### Question 101
What happens if an init container fails?

A) The Pod continues with remaining init containers
B) The Pod is restarted (init containers run again) based on restartPolicy
C) Only the failed init container is restarted
D) The Pod is deleted immediately

<details><summary>Answer</summary>

**B) The Pod is restarted (init containers run again) based on restartPolicy**

When an init container fails, Kubernetes restarts the Pod according to its restartPolicy. All init containers run again from the beginning (they must be idempotent). If the Pod has `restartPolicy: Never`, the Pod is marked as Failed. This ensures the Pod enters a consistent state before main containers start.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 102
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

### Question 103
What is the adapter container pattern?

A) A pattern for database connections
B) A pattern where a sidecar transforms or adapts output from the main container
C) A pattern for hardware abstraction
D) A pattern for network configuration

<details><summary>Answer</summary>

**B) A pattern where a sidecar transforms or adapts output from the main container**

The adapter pattern uses a sidecar to transform output from the main container into a standardized format. Common examples include log format conversion (transforming app-specific logs to JSON for centralized logging) or metrics adaptation (converting proprietary metrics to Prometheus format). This enables heterogeneous systems to present uniform interfaces.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 104
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

### Question 105
What resources can containers in the same Pod share?

A) Only network namespace
B) Network namespace, IPC namespace, and volumes
C) All namespaces including PID by default
D) Nothing, containers are fully isolated

<details><summary>Answer</summary>

**B) Network namespace, IPC namespace, and volumes**

Containers in a Pod share the network namespace (same IP, localhost communication), IPC namespace (can use shared memory and semaphores), and can mount the same volumes. PID namespace is not shared by default (each container has its own process view), though this can be enabled with `shareProcessNamespace: true`.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 106
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

### Question 107
How is a native sidecar container defined in Kubernetes?

A) Using a special sidecar field in the Pod spec
B) As an init container with restartPolicy: Always
C) Using a Sidecar custom resource
D) Through a sidecar annotation

<details><summary>Answer</summary>

**B) As an init container with restartPolicy: Always**

Native sidecars are defined in the `initContainers` section with `restartPolicy: Always`. This tells Kubernetes the container should run continuously rather than running to completion. The sidecar starts before main containers and remains running throughout the Pod's lifecycle, but doesn't block main container startup.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 108
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

### Question 109
What is an ephemeral container?

A) A container with limited resources
B) A temporary container added to a running Pod for debugging
C) A container that runs for a short time
D) A container without persistent storage

<details><summary>Answer</summary>

**B) A temporary container added to a running Pod for debugging**

Ephemeral containers are special containers added to running Pods for debugging purposes. They're useful when `kubectl exec` is insufficient - for example, when the container lacks debugging tools or has crashed. Added via `kubectl debug`, ephemeral containers can include debugging utilities not present in production images.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

### Question 110
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

### Question 111
What are container resource requests in Kubernetes?

A) The maximum resources a container can use
B) The minimum resources guaranteed to a container for scheduling purposes
C) The current resource usage
D) The default resource allocation

<details><summary>Answer</summary>

**B) The minimum resources guaranteed to a container for scheduling purposes**

Resource requests specify the minimum resources guaranteed to a container. The scheduler uses requests to decide which node has enough capacity to run the Pod. Requests affect QoS class assignment and are used in eviction decisions. A container can use more than its request (up to its limit) if resources are available.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 112
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

### Question 113
How does Kubernetes use resource requests for scheduling?

A) Requests are ignored during scheduling
B) The scheduler ensures the node has enough allocatable resources to meet requests
C) Requests are used only for billing
D) Requests determine Pod priority

<details><summary>Answer</summary>

**B) The scheduler ensures the node has enough allocatable resources to meet requests**

The kube-scheduler uses resource requests to find a suitable node for the Pod. It calculates each node's available capacity (allocatable minus sum of existing Pod requests) and only schedules to nodes with sufficient resources. This ensures Pods can get their requested resources and prevents overcommitment at the scheduling level.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 114
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

### Question 115
What happens when a container exceeds its CPU limit?

A) The container is terminated
B) The container is CPU-throttled
C) CPU is borrowed from other containers
D) The Pod is evicted

<details><summary>Answer</summary>

**B) The container is CPU-throttled**

When a container attempts to use more CPU than its limit, it gets throttled - the kernel simply doesn't allocate more CPU time. The container continues running but performs slower. This is different from memory, where exceeding limits causes termination. CPU is a "compressible" resource that can be throttled.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 116
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

### Question 117
What are the units for CPU resources in Kubernetes?

A) Percentage only
B) Cores or millicores (m)
C) GHz
D) Threads

<details><summary>Answer</summary>

**B) Cores or millicores (m)**

CPU resources in Kubernetes are specified in cores or millicores. One core equals 1000 millicores (m). For example, `500m` means half a CPU core, `2` means 2 full cores. This unit is consistent across cloud providers regardless of the underlying CPU type.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 118
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

### Question 119
What are the units for memory resources in Kubernetes?

A) Percentage only
B) Bytes, Ki, Mi, Gi (powers of 2) or K, M, G (powers of 10)
C) Pages
D) Sectors

<details><summary>Answer</summary>

**B) Bytes, Ki, Mi, Gi (powers of 2) or K, M, G (powers of 10)**

Memory can be specified in bytes or with suffixes. Binary suffixes (Ki, Mi, Gi, Ti) use powers of 1024 (kibibytes, mebibytes, etc.). Decimal suffixes (K, M, G, T) use powers of 1000. For example, 128Mi = 128 * 1024 * 1024 bytes, while 128M = 128 * 1000 * 1000 bytes.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 120
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

### Question 121
What is a QoS class in Kubernetes?

A) A network quality setting
B) A classification that affects scheduling and eviction priority
C) A storage performance tier
D) A service level agreement

<details><summary>Answer</summary>

**B) A classification that affects scheduling and eviction priority**

QoS (Quality of Service) classes are automatically assigned to Pods based on their resource requests and limits. There are three classes: Guaranteed, Burstable, and BestEffort. QoS class determines eviction priority when nodes are under resource pressure - BestEffort Pods are evicted first.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 122
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

### Question 123
When is a Pod assigned the 'Burstable' QoS class?

A) When no resources are specified
B) When at least one container has a request or limit, but doesn't meet Guaranteed criteria
C) When CPU limits exceed requests
D) When using ephemeral storage

<details><summary>Answer</summary>

**B) When at least one container has a request or limit, but doesn't meet Guaranteed criteria**

Burstable QoS is assigned when at least one container has CPU or memory requests/limits set, but the Pod doesn't qualify for Guaranteed. This includes Pods where requests don't equal limits, or where only some containers have resource specifications. Burstable Pods can burst beyond their requests up to their limits.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 124
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

### Question 125
How does QoS class affect eviction priority?

A) QoS has no effect on eviction
B) BestEffort Pods are evicted first, then Burstable, then Guaranteed
C) Guaranteed Pods are evicted first
D) Eviction is random regardless of QoS

<details><summary>Answer</summary>

**B) BestEffort Pods are evicted first, then Burstable, then Guaranteed**

When a node faces resource pressure, the kubelet evicts Pods based on QoS class. BestEffort Pods are evicted first as they have no guarantees. Burstable Pods are evicted next, based on their resource usage relative to requests. Guaranteed Pods are evicted last and only if system services need resources.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

## Container Configuration

### Question 126
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

### Question 127
What is a ConfigMap in Kubernetes?

A) A network configuration resource
B) An API object for storing non-confidential configuration data as key-value pairs
C) A storage volume type
D) A deployment strategy

<details><summary>Answer</summary>

**B) An API object for storing non-confidential configuration data as key-value pairs**

ConfigMaps store non-sensitive configuration data as key-value pairs. They decouple configuration from container images, allowing the same image to be used with different configurations. ConfigMaps can store individual values, entire configuration files, or JSON/YAML documents.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 128
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

### Question 129
What is a Secret in Kubernetes?

A) An encrypted ConfigMap
B) An object for storing sensitive data like passwords, tokens, and keys
C) A hidden volume
D) An authentication mechanism

<details><summary>Answer</summary>

**B) An object for storing sensitive data like passwords, tokens, and keys**

Secrets are Kubernetes objects designed for storing sensitive information like passwords, OAuth tokens, TLS certificates, and SSH keys. Unlike ConfigMaps, Secrets are base64-encoded and can be encrypted at rest. Access to Secrets can be restricted via RBAC for better security.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 130
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

### Question 131
How can Secret data be exposed to containers?

A) Only as environment variables
B) As environment variables or mounted as files in a volume
C) Only as files
D) Secrets cannot be exposed to containers

<details><summary>Answer</summary>

**B) As environment variables or mounted as files in a volume**

Like ConfigMaps, Secrets can be exposed as environment variables or volume mounts. When mounted as a volume, Secrets are stored in tmpfs (memory-based filesystem) so they're not written to disk on the node. Volume mounts are generally preferred over environment variables as they're more secure.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 132
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

### Question 133
How can you reference a specific key from a ConfigMap as an environment variable?

A) Using configMapRef
B) Using configMapKeyRef in the valueFrom field
C) Using configMapValue
D) Using configKey

<details><summary>Answer</summary>

**B) Using configMapKeyRef in the valueFrom field**

To reference a specific key from a ConfigMap, use `valueFrom.configMapKeyRef` in the env entry. You specify the ConfigMap name and the key to extract. Example: `valueFrom: {configMapKeyRef: {name: "my-config", key: "database-url"}}`. For Secrets, use `secretKeyRef` instead.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 134
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

### Question 135
How do you mount a ConfigMap as a volume?

A) Using a hostPath volume
B) Using a configMap volume type and mounting it at a container path
C) Using a configMount field
D) Using an emptyDir volume

<details><summary>Answer</summary>

**B) Using a configMap volume type and mounting it at a container path**

To mount a ConfigMap as a volume: 1) Define a volume with `configMap` type in the Pod spec, 2) Mount the volume at a path using `volumeMounts`. Each key in the ConfigMap becomes a file in the mounted directory. You can optionally select specific keys with `items`.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 136
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

### Question 137
What is the args field in a container spec?

A) The entrypoint command
B) Arguments passed to the command (entrypoint), overriding CMD
C) Environment variables
D) Volume mount options

<details><summary>Answer</summary>

**B) Arguments passed to the command (entrypoint), overriding CMD**

The `args` field provides arguments to the container's command (entrypoint). It overrides the Docker image's CMD. If `args` is specified without `command`, the image's ENTRYPOINT is used with the new args. The args array is passed directly to the entrypoint executable.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 138
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

### Question 139
What is a container's working directory?

A) The directory where logs are stored
B) The current directory when the container's process starts
C) The directory where the image is stored
D) The mount point for volumes

<details><summary>Answer</summary>

**B) The current directory when the container's process starts**

The working directory is the current directory (pwd) when the container's process starts. It's set by the image's WORKDIR instruction or can be overridden with the `workingDir` field in Kubernetes. Commands and relative paths in the container are resolved from this directory.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 140
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

### Question 141
What is a SecurityContext in Kubernetes?

A) A firewall configuration
B) Settings that define privilege and access control for Pods and containers
C) A network policy
D) An authentication token

<details><summary>Answer</summary>

**B) Settings that define privilege and access control for Pods and containers**

SecurityContext defines security settings for Pods and containers, including user/group IDs, Linux capabilities, filesystem permissions, and privilege escalation. It can be set at Pod level (applies to all containers) or container level (overrides Pod settings for that container).

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 142
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

### Question 143
What does the runAsNonRoot field enforce?

A) Running as user ID 0
B) That the container must run as a non-root user (UID != 0)
C) Using a non-root filesystem
D) Disabling privileged mode

<details><summary>Answer</summary>

**B) That the container must run as a non-root user (UID != 0)**

When `runAsNonRoot: true`, Kubernetes validates that the container doesn't run as UID 0 (root). If the image is configured to run as root and no `runAsUser` is specified, the container fails to start. This prevents accidental root execution and is a security best practice.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 144
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

### Question 145
What are Linux capabilities in the context of containers?

A) Hardware features
B) Fine-grained privileges that can be granted or removed from processes
C) Container resource limits
D) Network permissions

<details><summary>Answer</summary>

**B) Fine-grained privileges that can be granted or removed from processes**

Linux capabilities divide root privileges into distinct units that can be independently enabled or disabled. Instead of running as full root, containers can have specific capabilities like NET_BIND_SERVICE (bind to low ports) or NET_RAW (raw sockets). Dropping unnecessary capabilities reduces attack surface.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 146
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

### Question 147
What capability is required to bind to ports below 1024?

A) NET_RAW
B) NET_BIND_SERVICE
C) SYS_ADMIN
D) NET_ADMIN

<details><summary>Answer</summary>

**B) NET_BIND_SERVICE**

The NET_BIND_SERVICE capability allows binding to privileged ports (below 1024) without running as root. This is useful for services like web servers that need port 80 or 443. Instead of running as root, you can run as a non-root user with just this capability added.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 148
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

### Question 149
Why should privileged containers be avoided?

A) They are slower
B) They can compromise the host system if the container is compromised
C) They use more memory
D) They are deprecated

<details><summary>Answer</summary>

**B) They can compromise the host system if the container is compromised**

Privileged containers break container isolation - if compromised, an attacker gains near-root access to the host. They can mount host filesystems, load kernel modules, access all devices, and escape to other containers. Use specific capabilities or host paths instead of privileged mode when possible.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 150
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

### Question 151
What is the purpose of the seccompProfile field?

A) To set SELinux options
B) To define a seccomp profile that filters system calls
C) To configure AppArmor
D) To set resource limits

<details><summary>Answer</summary>

**B) To define a seccomp profile that filters system calls**

The `seccompProfile` field configures seccomp (secure computing mode) to restrict which system calls a container can make. Options include RuntimeDefault (use the container runtime's default profile), Localhost (use a custom profile), or Unconfined (no restrictions). Seccomp adds defense-in-depth against container escapes.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 152
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

### Question 153
What is AppArmor in the context of container security?

A) A container runtime
B) A Linux security module that restricts program capabilities with profiles
C) A Kubernetes admission controller
D) A network policy

<details><summary>Answer</summary>

**B) A Linux security module that restricts program capabilities with profiles**

AppArmor is a Linux security module that restricts what files, networks, and capabilities programs can access. It uses profiles that define allowed operations. In Kubernetes, AppArmor profiles can be applied to containers to limit file access, network activity, and other operations beyond what seccomp provides.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 154
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

### Question 155
What is SELinux in the context of container security?

A) A container format
B) A mandatory access control system that enforces security policies
C) A Kubernetes feature
D) A container runtime

<details><summary>Answer</summary>

**B) A mandatory access control system that enforces security policies**

SELinux (Security-Enhanced Linux) is a mandatory access control system that enforces security policies beyond traditional Linux permissions. It labels processes and files with security contexts and controls interactions based on policies. In Kubernetes, SELinux options can be set to control container access to files and processes.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 156
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

### Question 157
What is a Pod Security Standard?

A) A performance benchmark
B) A set of policies defining security best practices at different levels
C) A container format specification
D) A network security protocol

<details><summary>Answer</summary>

**B) A set of policies defining security best practices at different levels**

Pod Security Standards (PSS) define three security policy levels for Pods: Privileged, Baseline, and Restricted. They specify which security settings are required or forbidden. Pod Security Admission enforces these standards at the namespace level, replacing the deprecated PodSecurityPolicy.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 158
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

### Question 159
What does the Privileged Pod Security Standard allow?

A) Only non-root containers
B) Unrestricted policy, allowing known privilege escalations
C) No network access
D) Read-only filesystems only

<details><summary>Answer</summary>

**B) Unrestricted policy, allowing known privilege escalations**

The Privileged level is an unrestricted policy that allows everything, including privileged containers, host namespaces, and all capabilities. It's intended for system-level and infrastructure workloads managed by trusted users. It provides no security guarantees and should only be used when necessary.

**Source:** [Configure a Security Context for a Pod or Container | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

</details>

### Question 160
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

### Question 161
What network namespace do containers in a Pod share?

A) Each container has its own network namespace
B) All containers share the same network namespace
C) Only init containers share the namespace
D) Network namespaces are optional

<details><summary>Answer</summary>

**B) All containers share the same network namespace**

All containers in a Pod share the same network namespace, meaning they share the same IP address and port space. They can communicate via localhost. This is fundamental to the Pod model and enables tightly-coupled containers to communicate efficiently without network overhead.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 162
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

### Question 163
What is the pause container?

A) A container that pauses other containers
B) An infrastructure container that holds the network namespace for the Pod
C) A debugging container
D) A resource-saving container

<details><summary>Answer</summary>

**B) An infrastructure container that holds the network namespace for the Pod**

The pause container (also called sandbox or infra container) is a minimal container that holds the network namespace for the Pod. It starts first and stays running, acting as the parent for the Pod's network namespace. Other containers join this namespace, ensuring the namespace persists even if app containers restart.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 164
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

### Question 165
How do containers expose ports in Kubernetes?

A) Ports are automatically exposed
B) Through the containerPort field in the container spec
C) Through firewall rules
D) Through the Service object only

<details><summary>Answer</summary>

**B) Through the containerPort field in the container spec**

The `containerPort` field in the container spec documents which ports the container listens on. While containers can listen on any port (containerPort is primarily informational), declaring ports helps with documentation and allows Services to target specific ports. It doesn't actually open or close ports.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 166
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

### Question 167
What is the hostPort field used for?

A) To expose container ports only within the Pod
B) To map a container port directly to a port on the host node
C) To configure Service ports
D) To set DNS resolution

<details><summary>Answer</summary>

**B) To map a container port directly to a port on the host node**

`hostPort` maps a container port to a port on the node's IP address. Traffic to `<nodeIP>:<hostPort>` is forwarded to the container. This bypasses the Service abstraction and is used in special cases like DaemonSets that need to receive traffic directly on each node.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 168
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

### Question 169
What is the protocol field in containerPort?

A) The application protocol
B) The network protocol (TCP, UDP, or SCTP) for the port
C) The authentication protocol
D) The encryption protocol

<details><summary>Answer</summary>

**B) The network protocol (TCP, UDP, or SCTP) for the port**

The `protocol` field specifies the network protocol for the port: TCP (default), UDP, or SCTP. This must match the protocol used by the application. Services also use this to route traffic correctly. Most web applications use TCP, while DNS and some streaming services use UDP.

**Source:** [Containers | Kubernetes](https://kubernetes.io/docs/concepts/containers/)

</details>

### Question 170
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

### Question 171
Where do container logs go by default in Kubernetes?

A) To a central logging system
B) To stdout and stderr, captured by the container runtime
C) To a log file in the container
D) To the Kubernetes API server

<details><summary>Answer</summary>

**B) To stdout and stderr, captured by the container runtime**

Containers should write logs to stdout and stderr rather than files. The container runtime captures these streams and stores them on the node (typically under /var/log/containers/). This enables `kubectl logs` to work and allows log aggregation solutions to collect logs consistently.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 172
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

### Question 173
What happens to container logs when a container restarts?

A) Logs are preserved indefinitely
B) Previous logs can be viewed with --previous flag, current container gets new logs
C) All logs are deleted
D) Logs are automatically backed up

<details><summary>Answer</summary>

**B) Previous logs can be viewed with --previous flag, current container gets new logs**

When a container restarts, its log file is rotated. The current container's logs start fresh, but logs from the previous instance are preserved temporarily. Use `kubectl logs --previous` to view the terminated container's logs, helpful for debugging crash loops.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 174
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

### Question 175
What is the recommended logging approach for containers?

A) Write logs to files inside the container
B) Write logs to stdout/stderr for collection by the logging infrastructure
C) Send logs directly to an external system
D) Store logs in a database

<details><summary>Answer</summary>

**B) Write logs to stdout/stderr for collection by the logging infrastructure**

The twelve-factor app methodology recommends writing logs to stdout/stderr. This allows the platform to handle log collection and aggregation. Containers shouldn't be concerned with log storage or routing - this is handled by the container runtime and logging infrastructure like Fluentd, Filebeat, or cloud logging services.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 176
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

### Question 177
How can you debug a running container?

A) Restart the container
B) Use kubectl exec to run commands or kubectl debug for troubleshooting
C) Check the Dockerfile
D) Redeploy the Pod

<details><summary>Answer</summary>

**B) Use kubectl exec to run commands or kubectl debug for troubleshooting**

For running containers, use `kubectl exec` to run commands inside the container, or `kubectl debug` to add ephemeral debug containers. You can also use `kubectl logs`, `kubectl describe`, and `kubectl port-forward` for different debugging scenarios.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 178
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

### Question 179
How can you get an interactive shell in a container?

A) kubectl run
B) kubectl exec -it <pod> -- /bin/sh (or /bin/bash)
C) kubectl shell
D) kubectl connect

<details><summary>Answer</summary>

**B) kubectl exec -it <pod> -- /bin/sh (or /bin/bash)**

To get an interactive shell, use `kubectl exec -it <pod-name> -- /bin/sh` (or `/bin/bash` if available). The `-i` flag enables stdin, `-t` allocates a TTY. The `--` separates kubectl arguments from the command to run. Use `-c container` for multi-container Pods.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 180
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

### Question 181
How can you debug a container that crashes immediately?

A) Only by checking logs
B) Using kubectl debug to add a debug container or creating a copy with different commands
C) By increasing resource limits
D) By changing the restart policy

<details><summary>Answer</summary>

**B) Using kubectl debug to add a debug container or creating a copy with different commands**

For crash-looping containers, use `kubectl debug --copy-to` to create a copy with a different command (like `sleep infinity`) to keep it running. Or use `kubectl debug` to add an ephemeral container that shares namespaces with the crashing container. Also check logs with `kubectl logs --previous`.

**Source:** [Ephemeral Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/)

</details>

### Question 182
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

### Question 183
How can you inspect container resource usage?

A) Using kubectl describe only
B) Using kubectl top pod (requires metrics-server)
C) Using kubectl resources
D) Using kubectl monitor

<details><summary>Answer</summary>

**B) Using kubectl top pod (requires metrics-server)**

`kubectl top pod` shows current CPU and memory usage for Pods and containers. It requires the metrics-server to be installed in the cluster. Use `--containers` to see per-container metrics. This provides real-time resource consumption data for debugging and capacity planning.

**Source:** [Resource Management for Pods and Containers | Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

</details>

### Question 184
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

### Question 185
How can you view container events?

A) Using kubectl events
B) Using kubectl describe pod, which shows events in the Events section
C) Using kubectl logs
D) Using kubectl get containers

<details><summary>Answer</summary>

**B) Using kubectl describe pod, which shows events in the Events section**

`kubectl describe pod` displays a comprehensive view including the Events section showing recent events related to the Pod and its containers. Events include image pulls, container starts/stops, probe failures, scheduling decisions, and resource issues. You can also use `kubectl get events` for cluster-wide events.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

## Advanced Container Concepts

### Question 186
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

### Question 187
What is the PostStart hook?

A) A hook that runs after the container stops
B) A hook that runs immediately after a container is created
C) A cleanup hook
D) A scheduling hook

<details><summary>Answer</summary>

**B) A hook that runs immediately after a container is created**

The PostStart hook executes immediately after a container is created. It runs asynchronously with the container's ENTRYPOINT, meaning there's no guarantee about order. Common uses include waiting for dependencies, sending notifications, or performing initialization. If it fails, the container is killed.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 188
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

### Question 189
How are container hooks executed?

A) In a separate container
B) Inside the container using exec or HTTP handlers
C) On the host node
D) By the Kubernetes API server

<details><summary>Answer</summary>

**B) Inside the container using exec or HTTP handlers**

Hooks support two handlers: exec (runs a command inside the container) and httpGet (makes an HTTP request to a container endpoint). The exec handler runs in the container's namespace and filesystem. HTTP handlers must have an endpoint the container serves.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 190
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

### Question 191
What is the terminationGracePeriodSeconds field?

A) The time a container can run
B) The time Kubernetes waits for a Pod to terminate gracefully before force-killing
C) The startup timeout
D) The probe timeout

<details><summary>Answer</summary>

**B) The time Kubernetes waits for a Pod to terminate gracefully before force-killing**

`terminationGracePeriodSeconds` (default 30 seconds) is the time allowed for graceful shutdown. During this period, PreStop hooks run and SIGTERM is sent. If containers don't exit within this period, SIGKILL is sent. Increase this for applications needing more time to drain connections or save state.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 192
What happens when a Pod is terminated?

A) Containers are killed immediately
B) SIGTERM is sent, PreStop hooks run, then SIGKILL after grace period
C) Only SIGKILL is sent
D) Containers are paused

<details><summary>Answer</summary>

**B) SIGTERM is sent, PreStop hooks run, then SIGKILL after grace period**

Pod termination sequence: 1) PreStop hooks run (concurrently with SIGTERM in older versions, before SIGTERM in newer), 2) SIGTERM is sent to container processes, 3) Grace period counts down, 4) SIGKILL is sent to any remaining processes. This allows applications to shut down gracefully.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 193
What is the SIGTERM signal used for?

A) Immediate termination
B) Graceful shutdown request, allowing the process to clean up
C) Process pause
D) Resource limit notification

<details><summary>Answer</summary>

**B) Graceful shutdown request, allowing the process to clean up**

SIGTERM (signal 15) is a termination request that allows processes to catch it and perform cleanup before exiting. Applications should handle SIGTERM to gracefully close connections, flush buffers, and save state. Unlike SIGKILL, SIGTERM can be caught and handled by the application.

**Source:** [Pod Lifecycle | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

</details>

### Question 194
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

### Question 195
What is container image caching?

A) Compressing images
B) Storing pulled images on nodes to avoid repeated downloads
C) Encrypting images
D) Versioning images

<details><summary>Answer</summary>

**B) Storing pulled images on nodes to avoid repeated downloads**

Container runtimes cache pulled images on nodes so subsequent Pod starts don't need to re-download them. This speeds up container startup and reduces network usage. The imagePullPolicy controls whether cached images are used (IfNotPresent, Never) or always pulled (Always).

**Source:** [Container Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 196
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

### Question 197
What is the ImagePullBackOff error?

A) An authentication error
B) A state indicating repeated failures to pull an image, with exponential backoff
C) A network timeout
D) A storage error

<details><summary>Answer</summary>

**B) A state indicating repeated failures to pull an image, with exponential backoff**

ImagePullBackOff occurs after repeated ErrImagePull failures. Kubernetes backs off (waits longer between attempts) to avoid overwhelming registries. Check `kubectl describe pod` for details. Common causes include image not found, authentication failures, network issues, or typos in image names.

**Source:** [Container Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 198
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

### Question 199
What is a container runtime sandbox?

A) A development environment
B) An isolation layer providing additional security between containers and the kernel
C) A test container
D) A resource limit

<details><summary>Answer</summary>

**B) An isolation layer providing additional security between containers and the kernel**

A sandbox runtime provides additional isolation between containers and the host kernel, beyond standard Linux namespaces and cgroups. Examples include gVisor (user-space kernel) and Kata Containers (lightweight VMs). They reduce kernel attack surface for untrusted workloads at the cost of some performance overhead.

**Source:** [Runtime Class | Kubernetes](https://kubernetes.io/docs/concepts/containers/runtime-class/)

</details>

### Question 200
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
