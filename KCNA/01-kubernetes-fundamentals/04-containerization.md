# KCNA Containerization MCQs

## Container Fundamentals

### Question 1
What is a container in the context of cloud-native computing?

### Question 2
Which technology provides the foundation for container isolation in Linux?

### Question 3
What is the primary difference between a container and a virtual machine?

### Question 4
Which Linux kernel feature allows containers to have isolated views of system resources like PIDs and network interfaces?

### Question 5
What is a container image?

### Question 6
How are container image layers structured?

### Question 7
What happens when multiple containers share the same base image layers?

### Question 8
What is the purpose of a container runtime?

### Question 9
Which component in Kubernetes is responsible for pulling container images and running containers?

### Question 10
What is the Container Runtime Interface (CRI) in Kubernetes?

## Container Runtimes

### Question 11
Which of the following is NOT a CRI-compliant container runtime?

### Question 12
What is containerd?

### Question 13
How does CRI-O differ from containerd?

### Question 14
What is the relationship between Docker and containerd?

### Question 15
Which container runtime is specifically designed and optimized for Kubernetes?

### Question 16
What is runc?

### Question 17
What role does the OCI (Open Container Initiative) play in containerization?

### Question 18
Which OCI specification defines how to run a container?

### Question 19
What is the purpose of the OCI Image specification?

### Question 20
How does Kubernetes communicate with container runtimes?

## Container Images and Registries

### Question 21
What is a container registry?

### Question 22
Which of the following is the default container registry for Docker images?

### Question 23
What is the purpose of image tags?

### Question 24
What does the 'latest' tag signify for a container image?

### Question 25
What is an image digest?

### Question 26
Why are image digests preferred over tags for production deployments?

### Question 27
What is a private container registry?

### Question 28
How does Kubernetes authenticate to private container registries?

### Question 29
What is an ImagePullSecret?

### Question 30
Which field in a Pod spec references credentials for pulling private images?

### Question 31
What is the purpose of the imagePullPolicy field in a container spec?

### Question 32
When is an image pulled if imagePullPolicy is set to 'IfNotPresent'?

### Question 33
What imagePullPolicy is automatically applied when using the 'latest' tag?

### Question 34
What happens when imagePullPolicy is set to 'Never'?

### Question 35
How can you configure a default imagePullPolicy for all containers in a namespace?

## Building Container Images

### Question 36
What is a Dockerfile?

### Question 37
Which Dockerfile instruction sets the base image for subsequent instructions?

### Question 38
What is the purpose of the RUN instruction in a Dockerfile?

### Question 39
How does the COPY instruction differ from ADD in a Dockerfile?

### Question 40
What is the purpose of the ENTRYPOINT instruction?

### Question 41
How does CMD differ from ENTRYPOINT in a Dockerfile?

### Question 42
What happens when both ENTRYPOINT and CMD are specified?

### Question 43
What is the purpose of the WORKDIR instruction?

### Question 44
How does the ENV instruction work in a Dockerfile?

### Question 45
What is a multi-stage build in Docker?

### Question 46
What is the primary benefit of multi-stage builds?

### Question 47
What is the purpose of the ARG instruction in a Dockerfile?

### Question 48
How does ARG differ from ENV in a Dockerfile?

### Question 49
What is the purpose of the EXPOSE instruction?

### Question 50
What is a .dockerignore file used for?

## Container Image Best Practices

### Question 51
Why should you use specific image tags instead of 'latest' in production?

### Question 52
What is the recommended practice for base image selection?

### Question 53
Why are minimal base images like Alpine or distroless recommended?

### Question 54
What is a distroless container image?

### Question 55
How can you reduce the number of layers in a container image?

### Question 56
Why should you avoid running containers as root?

### Question 57
What Dockerfile instruction creates a non-root user?

### Question 58
What is the purpose of the USER instruction in a Dockerfile?

### Question 59
Why should sensitive data like secrets never be included in container images?

### Question 60
What is the recommended approach for handling secrets in containers?

### Question 61
How can you verify the security of container images?

### Question 62
What is container image scanning?

### Question 63
What is image signing and verification?

### Question 64
What tool does Kubernetes use for image signature verification?

### Question 65
What is the purpose of a Software Bill of Materials (SBOM) for container images?

## Container Lifecycle

### Question 66
What are the possible states of a container in Kubernetes?

### Question 67
What does the 'Waiting' container state indicate?

### Question 68
What causes a container to be in the 'Running' state?

### Question 69
What does the 'Terminated' container state indicate?

### Question 70
What is the container restart policy in Kubernetes?

### Question 71
What happens when restartPolicy is set to 'Always'?

### Question 72
When would you use restartPolicy 'OnFailure'?

### Question 73
What is the purpose of restartPolicy 'Never'?

### Question 74
How does Kubernetes handle container restart backoff?

### Question 75
What is the maximum backoff delay for container restarts?

## Container Probes

### Question 76
What is the purpose of a liveness probe?

### Question 77
What happens when a liveness probe fails?

### Question 78
What is the purpose of a readiness probe?

### Question 79
What happens when a readiness probe fails?

### Question 80
What is the purpose of a startup probe?

### Question 81
How does a startup probe interact with liveness and readiness probes?

### Question 82
What are the three types of probe mechanisms in Kubernetes?

### Question 83
How does an HTTP probe work?

### Question 84
What constitutes a successful HTTP probe response?

### Question 85
How does a TCP probe work?

### Question 86
What is an exec probe?

### Question 87
What determines success for an exec probe?

### Question 88
What is the initialDelaySeconds parameter in a probe configuration?

### Question 89
What is the periodSeconds parameter in a probe configuration?

### Question 90
What is the timeoutSeconds parameter in a probe configuration?

### Question 91
What is the failureThreshold parameter in a probe configuration?

### Question 92
What is the successThreshold parameter in a probe configuration?

### Question 93
Which probe type supports gRPC health checking?

### Question 94
What is a common mistake when configuring liveness probes?

### Question 95
Why should readiness probes not have the same endpoint as liveness probes?

## Multi-Container Pods

### Question 96
What is a sidecar container?

### Question 97
What is a common use case for sidecar containers?

### Question 98
What is an init container?

### Question 99
How do init containers differ from regular containers?

### Question 100
In what order do init containers execute?

### Question 101
What happens if an init container fails?

### Question 102
What is the ambassador container pattern?

### Question 103
What is the adapter container pattern?

### Question 104
How do containers within the same Pod communicate?

### Question 105
What resources can containers in the same Pod share?

### Question 106
What is a sidecar container in Kubernetes 1.28+?

### Question 107
How is a native sidecar container defined in Kubernetes?

### Question 108
What is the lifecycle behavior of native sidecar containers?

### Question 109
What is an ephemeral container?

### Question 110
When would you use an ephemeral container?

## Container Resources

### Question 111
What are container resource requests in Kubernetes?

### Question 112
What are container resource limits in Kubernetes?

### Question 113
How does Kubernetes use resource requests for scheduling?

### Question 114
What happens when a container exceeds its memory limit?

### Question 115
What happens when a container exceeds its CPU limit?

### Question 116
What is the difference between CPU and memory limit enforcement?

### Question 117
What are the units for CPU resources in Kubernetes?

### Question 118
What does '500m' mean for CPU resources?

### Question 119
What are the units for memory resources in Kubernetes?

### Question 120
What is the difference between Mi and M for memory units?

### Question 121
What is a QoS class in Kubernetes?

### Question 122
When is a Pod assigned the 'Guaranteed' QoS class?

### Question 123
When is a Pod assigned the 'Burstable' QoS class?

### Question 124
When is a Pod assigned the 'BestEffort' QoS class?

### Question 125
How does QoS class affect eviction priority?

## Container Configuration

### Question 126
How can you pass environment variables to a container?

### Question 127
What is a ConfigMap in Kubernetes?

### Question 128
How can ConfigMap data be exposed to containers?

### Question 129
What is a Secret in Kubernetes?

### Question 130
How are Secrets different from ConfigMaps?

### Question 131
How can Secret data be exposed to containers?

### Question 132
What is the envFrom field used for?

### Question 133
How can you reference a specific key from a ConfigMap as an environment variable?

### Question 134
What is a volume mount in a container?

### Question 135
How do you mount a ConfigMap as a volume?

### Question 136
What is the command field in a container spec?

### Question 137
What is the args field in a container spec?

### Question 138
How do command and args override Dockerfile ENTRYPOINT and CMD?

### Question 139
What is a container's working directory?

### Question 140
How can you override a container's working directory in Kubernetes?

## Container Security

### Question 141
What is a SecurityContext in Kubernetes?

### Question 142
What does the runAsUser field specify?

### Question 143
What does the runAsNonRoot field enforce?

### Question 144
What is the readOnlyRootFilesystem setting?

### Question 145
What are Linux capabilities in the context of containers?

### Question 146
How can you drop Linux capabilities from a container?

### Question 147
What capability is required to bind to ports below 1024?

### Question 148
What is a privileged container?

### Question 149
Why should privileged containers be avoided?

### Question 150
What is allowPrivilegeEscalation?

### Question 151
What is the purpose of the seccompProfile field?

### Question 152
What is the RuntimeDefault seccomp profile?

### Question 153
What is AppArmor in the context of container security?

### Question 154
How do you apply an AppArmor profile to a container?

### Question 155
What is SELinux in the context of container security?

### Question 156
How can you set SELinux options for a container?

### Question 157
What is a Pod Security Standard?

### Question 158
What are the three Pod Security Standard levels?

### Question 159
What does the Privileged Pod Security Standard allow?

### Question 160
What does the Baseline Pod Security Standard restrict?

## Container Networking

### Question 161
What network namespace do containers in a Pod share?

### Question 162
How do containers in the same Pod communicate with each other?

### Question 163
What is the pause container?

### Question 164
What role does the pause container play in Pod networking?

### Question 165
How do containers expose ports in Kubernetes?

### Question 166
What is the containerPort field used for?

### Question 167
What is the hostPort field used for?

### Question 168
Why should hostPort be avoided in most cases?

### Question 169
What is the protocol field in containerPort?

### Question 170
How does a Service route traffic to container ports?

## Container Logging and Debugging

### Question 171
Where do container logs go by default in Kubernetes?

### Question 172
How does kubectl logs retrieve container logs?

### Question 173
What happens to container logs when a container restarts?

### Question 174
How can you view logs from a previous container instance?

### Question 175
What is the recommended logging approach for containers?

### Question 176
What is a logging sidecar container?

### Question 177
How can you debug a running container?

### Question 178
What does kubectl exec do?

### Question 179
How can you get an interactive shell in a container?

### Question 180
What is kubectl debug used for?

### Question 181
How can you debug a container that crashes immediately?

### Question 182
What is a debug container?

### Question 183
How can you inspect container resource usage?

### Question 184
What does kubectl top pod show?

### Question 185
How can you view container events?

## Advanced Container Concepts

### Question 186
What is a container hook in Kubernetes?

### Question 187
What is the PostStart hook?

### Question 188
What is the PreStop hook?

### Question 189
How are container hooks executed?

### Question 190
What happens if a PostStart hook fails?

### Question 191
What is the terminationGracePeriodSeconds field?

### Question 192
What happens when a Pod is terminated?

### Question 193
What is the SIGTERM signal used for?

### Question 194
What happens after the grace period expires during Pod termination?

### Question 195
What is container image caching?

### Question 196
How does image garbage collection work in Kubernetes?

### Question 197
What is the ImagePullBackOff error?

### Question 198
What causes ErrImagePull errors?

### Question 199
What is a container runtime sandbox?

### Question 200
What is gVisor in the context of container runtimes?
