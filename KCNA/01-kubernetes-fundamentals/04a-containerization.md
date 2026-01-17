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

### Question 3
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

### Question 4
What happens when multiple containers share the same base image layers?

A) Each container gets a complete copy of all layers
B) The layers are shared, saving disk space
C) Containers cannot share image layers
D) Only the first container uses the layers

<details><summary>Answer</summary>

**B) The layers are shared, saving disk space**

Container images are built from layers, and these layers are cached on nodes. When multiple containers use the same base image, the shared layers are stored only once on disk, reducing storage usage. Subsequent image pulls avoid re-downloading layers that already exist locally, speeding up container creation.

**Source:** [Images | Kubernetes](https://kubernetes.io/docs/concepts/containers/images/)

</details>

### Question 5
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

## Container Runtimes

### Question 6
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

### Question 7
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

### Question 8
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

### Question 9
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

### Question 10
What is the purpose of the OCI Image specification?

A) To define how containers should be networked
B) To define the format and structure of container images
C) To specify container security requirements
D) To outline container orchestration patterns

<details><summary>Answer</summary>

**B) To define the format and structure of container images**

The OCI Image Specification defines how container images are structured, including the image manifest, filesystem layers, and configuration. This standard ensures that images built with one tool can run on any OCI-compliant runtime, enabling portability across different platforms.

**Source:** [Container Runtimes | Kubernetes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

</details>

## Container Images and Registries

### Question 11
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

### Question 12
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

### Question 13
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

### Question 14
What is a private container registry?

A) A registry that only stores encrypted images
B) A registry that requires authentication to access images
C) A registry that runs on-premises only
D) A registry that stores only proprietary images

<details><summary>Answer</summary>

**B) A registry that requires authentication to access images**

A private container registry requires authentication to pull or push images. This protects proprietary code and ensures only authorized users can access images. Private registries can be cloud-hosted (ECR, GCR, ACR) or self-hosted (Harbor, Nexus). Authentication is typically via username/password or tokens.

**Source:** [Pull an Image from a Private Registry | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

</details>

### Question 15
What is an ImagePullSecret?

A) A password stored in the image
B) A Kubernetes Secret containing registry credentials
C) An encrypted image layer
D) A token embedded in the container

<details><summary>Answer</summary>

**B) A Kubernetes Secret containing registry credentials**

An ImagePullSecret is a Kubernetes Secret of type `kubernetes.io/dockerconfigjson` that contains registry authentication credentials. It stores the registry URL, username, password, and email in a format compatible with Docker's config.json. Pods reference this secret to pull images from private registries.

**Source:** [Pull an Image from a Private Registry | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

</details>

### Question 16
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

### Question 17
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

### Question 18
How can you configure a default imagePullPolicy for all containers in a namespace using built-in Kubernetes features?

A) Using a namespace annotation
B) Using an AlwaysPullImages admission controller
C) Using a ConfigMap
D) It cannot be configured at the namespace level with built-in features

<details><summary>Answer</summary>

**D) It cannot be configured at the namespace level with built-in features**

Kubernetes does not provide a built-in mechanism to set a default imagePullPolicy at the namespace level. The AlwaysPullImages admission controller forces `imagePullPolicy: Always` but operates cluster-wide, not per-namespace. For namespace-level control, you would need external policy engines like Kyverno, Gatekeeper, or ValidatingAdmissionPolicy with custom rules.

**Source:** [Admission Controllers Reference | Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/)

</details>

## Building Container Images

### Question 19
Which Dockerfile instruction sets the base image for subsequent instructions?

A) BASE
B) IMAGE
C) FROM
D) SOURCE

<details><summary>Answer</summary>

**C) FROM**

The FROM instruction specifies the base image for the build. It must be the first instruction in a Dockerfile (except for ARG). You can use FROM with an image name and tag (e.g., `FROM alpine:3.18`) or with `FROM scratch` to build from an empty image.

**Source (non-Kubernetes exception):** [SPDX Specifications | SPDX](https://spdx.dev/specifications/)

</details>

### Question 20
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

### Question 21
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

### Question 22
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

### Question 23
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

### Question 24
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

### Question 25
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

## Container Image Best Practices

### Question 26
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

### Question 27
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

### Question 28
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

### Question 29
What Dockerfile instruction specifies the user a container should run as?

A) RUN useradd or RUN adduser
B) USER
C) WORKDIR
D) ENTRYPOINT

<details><summary>Answer</summary>

**B) USER**

The `USER` instruction sets the username or UID used to run the container's main process. You can specify a numeric UID (and optional GID) or a username that exists in the image. Use `RUN useradd ...` (or `RUN adduser ...`) to create the user, then `USER appuser` to run as that account.

**Source (non-Kubernetes exception):** [Dockerfile reference | Docker](https://docs.docker.com/engine/reference/builder/)

</details>

### Question 30
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

### Question 31
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

### Question 32
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

### Question 33
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

### Question 34
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

### Question 35
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

### Question 36
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

### Question 37
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

### Question 38
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

### Question 39
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

### Question 40
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

### Question 41
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

### Question 42
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

### Question 43
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

### Question 44
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

### Question 45
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

### Question 46
What is the failureThreshold parameter in a probe configuration?

A) The number of times a probe can fail before taking action
B) The percentage of acceptable failures
C) The maximum number of probe attempts
D) The error code threshold

<details><summary>Answer</summary>

**A) The number of times a probe can fail before taking action**

failureThreshold specifies how many consecutive probe failures are needed before taking action (restart for liveness, mark unready for readiness). Default is 3. This prevents transient failures from triggering actions.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 47
Which probe type supports gRPC health checking?

A) Only httpGet
B) Only exec
C) grpc (native gRPC health checking)
D) gRPC is not supported in probes

<details><summary>Answer</summary>

**C) grpc (native gRPC health checking)**

Kubernetes 1.24+ supports native gRPC health checking as a probe type. You specify the port and optional service name. The probe calls the standard gRPC health checking protocol (grpc.health.v1.Health). This is more efficient than using exec with grpc_health_probe.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

### Question 48
Why should readiness probes not have the same endpoint as liveness probes?

A) It's technically not allowed
B) Different checks may be needed - readiness for dependencies, liveness for process health
C) It causes probe conflicts
D) It increases network traffic

<details><summary>Answer</summary>

**B) Different checks may be needed - readiness for dependencies, liveness for process health**

Readiness and liveness probes serve different purposes. Liveness checks if the process is alive and should be restarted if it fails. Readiness checks if the app can handle traffic, including verifying dependencies like databases. A failing readiness check (e.g., database down) shouldn't restart the container - it should just stop routing traffic until the issue resolves.

**Source:** [Configure Liveness, Readiness and Startup Probes | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

</details>

## Multi-Container Pods

### Question 49
What is a common use case for sidecar containers?

A) Running the primary application
B) Log collection, proxying, or syncing data
C) Database hosting
D) Load balancing across clusters

<details><summary>Answer</summary>

**B) Log collection, proxying, or syncing data**

Common sidecar use cases include: log collection (Fluentd, Filebeat) to ship logs from the main container, service mesh proxies (Envoy) to handle traffic routing and security, syncing configuration or data from external sources, and providing TLS termination or authentication services.

**Source:** [Sidecar Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/)

</details>

### Question 50
How do init containers differ from regular containers?

A) Init containers don't have resource limits
B) Init containers run to completion sequentially before app containers start
C) Init containers share the same image as app containers
D) Init containers can access host resources directly

<details><summary>Answer</summary>

**B) Init containers run to completion sequentially before app containers start**

Key differences: init containers run sequentially (one at a time), must complete successfully (exit 0) before the next starts, don't support probes, and are defined in a separate `initContainers` field. They can have different images and access different secrets than app containers. If an init container fails, the Pod restarts (subject to restartPolicy).

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 51
What happens if an init container fails?

A) The Pod continues with remaining init containers
B) The entire Pod restarts from the beginning
C) Only the failed init container is restarted until it succeeds
D) The Pod is deleted immediately

<details><summary>Answer</summary>

**C) Only the failed init container is restarted until it succeeds**

When an init container fails, the kubelet repeatedly restarts only that specific init container until it succeeds. The Pod does not restart from the beginning and already-completed init containers are not re-run. However, if `restartPolicy: Never` is set, the Pod is marked as Failed without restart attempts. Init containers must be idempotent since they may be restarted.

**Source:** [Init Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/init-containers/)

</details>

### Question 52
What is the adapter container pattern?

A) A pattern for database connections
B) A pattern where a sidecar transforms or adapts output from the main container
C) A pattern for hardware abstraction
D) A pattern for network configuration

<details><summary>Answer</summary>

**B) A pattern where a sidecar transforms or adapts output from the main container**

The adapter pattern uses a sidecar to transform output from the main container into a standardized format. Common examples include log format conversion (transforming app-specific logs to JSON for centralized logging) or metrics adaptation (converting proprietary metrics to Prometheus format). This enables heterogeneous systems to present uniform interfaces.

**Source:** [Sidecar Containers | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/)

</details>

### Question 53
What resources can containers in the same Pod share?

A) Only network namespace
B) Network namespace, IPC namespace, and volumes
C) All namespaces including PID by default
D) Nothing, containers are fully isolated

<details><summary>Answer</summary>

**B) Network namespace, IPC namespace, and volumes**

Containers in a Pod share the network namespace (same IP, localhost communication), IPC namespace (can use shared memory and semaphores), and can mount the same volumes. PID namespace is not shared by default (each container has its own process view), though this can be enabled with `shareProcessNamespace: true`.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

### Question 54
How is a sidecar container defined in Kubernetes?

A) Using a special sidecar field in the Pod spec
B) As an additional container in the Pod's containers array
C) Using a Sidecar custom resource
D) Through a sidecar annotation

<details><summary>Answer</summary>

**B) As an additional container in the Pod's containers array**

Sidecar containers are defined as regular containers in the Pod's `containers` array alongside the main application container. They run for the entire lifetime of the Pod and provide supporting functionality like logging, monitoring, or proxying. There is no special "sidecar" field - the sidecar pattern is implemented by adding multiple containers to a Pod.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

### Question 55
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

## Container Resources

### Question 56
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

### Question 57
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

### Question 58
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

### Question 59
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

### Question 60
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

### Question 61
What is a QoS class in Kubernetes?

A) A network quality setting
B) A classification that determines Pod eviction priority under resource pressure
C) A storage performance tier
D) A service level agreement

<details><summary>Answer</summary>

**B) A classification that determines Pod eviction priority under resource pressure**

QoS (Quality of Service) classes are automatically assigned to Pods based on their resource requests and limits. The three classes are: Guaranteed, Burstable, and BestEffort. QoS class determines eviction priority when nodes are under resource pressure—BestEffort Pods are evicted first, then Burstable, and Guaranteed last. Note: QoS class does not affect scheduling; scheduling decisions use resource requests instead.

**Source:** [Configure Quality of Service for Pods | Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/)

</details>

### Question 62
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

### Question 63
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

### Question 64
What is a ConfigMap in Kubernetes?

A) A network configuration resource
B) An API object for storing non-confidential configuration data as key-value pairs
C) A storage volume type
D) A deployment strategy

<details><summary>Answer</summary>

**B) An API object for storing non-confidential configuration data as key-value pairs**

ConfigMaps store non-sensitive configuration data as key-value pairs. They decouple configuration from container images, allowing the same image to be used with different configurations. ConfigMaps can store individual values, entire configuration files, or JSON/YAML documents.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

### Question 65
What is a Secret in Kubernetes?

A) An encrypted ConfigMap
B) An object for storing sensitive data like passwords, tokens, and keys
C) A hidden volume
D) An authentication mechanism

<details><summary>Answer</summary>

**B) An object for storing sensitive data like passwords, tokens, and keys**

Secrets are Kubernetes objects designed for storing sensitive information like passwords, OAuth tokens, TLS certificates, and SSH keys. Unlike ConfigMaps, Secrets are base64-encoded and can be encrypted at rest. Access to Secrets can be restricted via RBAC for better security.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

### Question 66
How can Secret data be exposed to containers?

A) Only as environment variables
B) As environment variables or mounted as files in a volume
C) Only as files
D) Secrets cannot be exposed to containers

<details><summary>Answer</summary>

**B) As environment variables or mounted as files in a volume**

Like ConfigMaps, Secrets can be exposed as environment variables or volume mounts. When mounted as a volume, Secrets are stored in tmpfs (memory-based filesystem) so they're not written to disk on the node. Volume mounts are generally preferred over environment variables as they're more secure.

**Source:** [Secrets | Kubernetes](https://kubernetes.io/docs/concepts/configuration/secret/)

</details>

### Question 67
How can you reference a specific key from a ConfigMap as an environment variable?

A) Using configMapRef
B) Using configMapKeyRef in the valueFrom field
C) Using configMapValue
D) Using configKey

<details><summary>Answer</summary>

**B) Using configMapKeyRef in the valueFrom field**

To reference a specific key from a ConfigMap, use `valueFrom.configMapKeyRef` in the env entry. You specify the ConfigMap name and the key to extract. Example: `valueFrom: {configMapKeyRef: {name: "my-config", key: "database-url"}}`. For Secrets, use `secretKeyRef` instead.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

### Question 68
How do you mount a ConfigMap as a volume?

A) Using a hostPath volume
B) Using a configMap volume type and mounting it at a container path
C) Using a configMount field
D) Using an emptyDir volume

<details><summary>Answer</summary>

**B) Using a configMap volume type and mounting it at a container path**

To mount a ConfigMap as a volume: 1) Define a volume with `configMap` type in the Pod spec, 2) Mount the volume at a path using `volumeMounts`. Each key in the ConfigMap becomes a file in the mounted directory. You can optionally select specific keys with `items`.

**Source:** [ConfigMaps | Kubernetes](https://kubernetes.io/docs/concepts/configuration/configmap/)

</details>

### Question 69
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

### Question 70
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

## Container Security

### Question 71
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

### Question 72
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

### Question 73
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

### Question 74
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

### Question 75
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

### Question 76
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

### Question 77
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

### Question 78
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

### Question 79
What is a Pod Security Standard?

A) A performance benchmark
B) A set of policies defining security best practices at different levels
C) A container format specification
D) A network security protocol

<details><summary>Answer</summary>

**B) A set of policies defining security best practices at different levels**

Pod Security Standards (PSS) define three security policy levels for Pods: Privileged, Baseline, and Restricted. They specify which security settings are required or forbidden. Pod Security Admission enforces these standards at the namespace level, replacing the deprecated PodSecurityPolicy.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

### Question 80
What does the Privileged Pod Security Standard allow?

A) Only non-root containers
B) Unrestricted policy, allowing known privilege escalations
C) No network access
D) Read-only filesystems only

<details><summary>Answer</summary>

**B) Unrestricted policy, allowing known privilege escalations**

The Privileged level is an unrestricted policy that allows everything, including privileged containers, host namespaces, and all capabilities. It's intended for system-level and infrastructure workloads managed by trusted users. It provides no security guarantees and should only be used when necessary.

**Source:** [Pod Security Standards | Kubernetes](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

</details>

## Container Networking

### Question 81
What network namespace do containers in a Pod share?

A) Each container has its own network namespace
B) All containers share the same network namespace
C) Only init containers share the namespace
D) Network namespaces are optional

<details><summary>Answer</summary>

**B) All containers share the same network namespace**

All containers in a Pod share the same network namespace, meaning they share the same IP address and port space. They can communicate via localhost. This is fundamental to the Pod model and enables tightly-coupled containers to communicate efficiently without network overhead.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

### Question 82
What is the pause container?

A) A container that pauses other containers
B) An infrastructure container that holds the network namespace for the Pod
C) A debugging container
D) A resource-saving container

<details><summary>Answer</summary>

**B) An infrastructure container that holds the network namespace for the Pod**

The pause container (also called sandbox or infra container) is a minimal container that holds the network namespace for the Pod. It starts first and stays running, acting as the parent for the Pod's network namespace. Other containers join this namespace, ensuring the namespace persists even if app containers restart.

**Source:** [Pods | Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/)

</details>

### Question 83
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

### Question 84
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

### Question 85
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

## Container Logging and Debugging

### Question 86
Where do container logs go by default in Kubernetes?

A) To a central logging system
B) To stdout and stderr, captured by the container runtime
C) To a log file in the container
D) To the Kubernetes API server

<details><summary>Answer</summary>

**B) To stdout and stderr, captured by the container runtime**

Containers should write logs to stdout and stderr rather than files. The container runtime captures these streams and stores them on the node (typically under /var/log/containers/). This enables `kubectl logs` to work and allows log aggregation solutions to collect logs consistently.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

### Question 87
What happens to container logs when a container restarts?

A) Logs are preserved indefinitely
B) Previous logs can be viewed with --previous flag, current container gets new logs
C) All logs are deleted
D) Logs are automatically backed up

<details><summary>Answer</summary>

**B) Previous logs can be viewed with --previous flag, current container gets new logs**

When a container restarts, its log file is rotated. The current container's logs start fresh, but logs from the previous instance are preserved temporarily. Use `kubectl logs --previous` to view the terminated container's logs, helpful for debugging crash loops.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

### Question 88
What is the recommended logging approach for containers?

A) Write logs to files inside the container
B) Write logs to stdout/stderr for collection by the logging infrastructure
C) Send logs directly to an external system
D) Store logs in a database

<details><summary>Answer</summary>

**B) Write logs to stdout/stderr for collection by the logging infrastructure**

The twelve-factor app methodology recommends writing logs to stdout/stderr. This allows the platform to handle log collection and aggregation. Containers shouldn't be concerned with log storage or routing - this is handled by the container runtime and logging infrastructure like Fluentd, Filebeat, or cloud logging services.

**Source:** [Logging Architecture | Kubernetes](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

</details>

### Question 89
How can you debug a running container?

A) Restart the container
B) Use kubectl exec to run commands or kubectl debug for troubleshooting
C) Check the Dockerfile
D) Redeploy the Pod

<details><summary>Answer</summary>

**B) Use kubectl exec to run commands or kubectl debug for troubleshooting**

For running containers, use `kubectl exec` to run commands inside the container, or `kubectl debug` to add ephemeral debug containers. You can also use `kubectl logs`, `kubectl describe`, and `kubectl port-forward` for different debugging scenarios.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

### Question 90
How can you get an interactive shell in a container?

A) kubectl run
B) kubectl exec -it <pod> -- /bin/sh (or /bin/bash)
C) kubectl shell
D) kubectl connect

<details><summary>Answer</summary>

**B) kubectl exec -it <pod> -- /bin/sh (or /bin/bash)**

To get an interactive shell, use `kubectl exec -it <pod-name> -- /bin/sh` (or `/bin/bash` if available). The `-i` flag enables stdin, `-t` allocates a TTY. The `--` separates kubectl arguments from the command to run. Use `-c container` for multi-container Pods.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

### Question 91
How can you debug a container that crashes immediately?

A) Only by checking logs
B) Using kubectl debug to add a debug container or creating a copy with different commands
C) By increasing resource limits
D) By changing the restart policy

<details><summary>Answer</summary>

**B) Using kubectl debug to add a debug container or creating a copy with different commands**

For crash-looping containers, use `kubectl debug --copy-to` to create a copy with a different command (like `sleep infinity`) to keep it running. Or use `kubectl debug` to add an ephemeral container that shares namespaces with the crashing container. Also check logs with `kubectl logs --previous`.

**Source:** [Debug Running Pods | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-application/debug-running-pod/)

</details>

### Question 92
How can you inspect container resource usage?

A) Using kubectl describe only
B) Using kubectl top pod (requires metrics-server)
C) Using kubectl resources
D) Using kubectl monitor

<details><summary>Answer</summary>

**B) Using kubectl top pod (requires metrics-server)**

`kubectl top pod` shows current CPU and memory usage for Pods and containers. It requires the metrics-server to be installed in the cluster. Use `--containers` to see per-container metrics. This provides real-time resource consumption data for debugging and capacity planning.

**Source:** [Resource Metrics Pipeline | Kubernetes](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/)

</details>

### Question 93
How can you view container events?

A) Using kubectl events
B) Using kubectl describe pod, which shows events in the Events section
C) Using kubectl logs
D) Using kubectl get containers

<details><summary>Answer</summary>

**B) Using kubectl describe pod, which shows events in the Events section**

`kubectl describe pod` displays a comprehensive view including the Events section showing recent events related to the Pod and its containers. Events include image pulls, container starts/stops, probe failures, scheduling decisions, and resource issues. You can also use `kubectl get events` for cluster-wide events.

**Source:** [kubectl describe | Kubernetes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)

</details>

## Advanced Container Concepts

### Question 94
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

### Question 95
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

### Question 96
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

### Question 97
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

### Question 98
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

### Question 99
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

### Question 100
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
