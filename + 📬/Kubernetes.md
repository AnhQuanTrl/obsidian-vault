Kubernetes, developed by Google and later contributed to the Cloud Native Computing Foundation (CNCF), is an open-source technology for container orchestration. It was built from scratch, drawing on Google’s experience with Borg, their internal solution.

**Container**: 
In the past, applications are deployed together in *Virtual machines*. There are three main downsides with this deployment architecture:

> [!note]- Overhead of managing compatibility and dependency.
> Deployed services might require specific versions of the OS, development toolchains, libraries, and dependencies. One service may depend on a particular version of a library, while another requires a different version. Administrators must constantly address these compatibility issues as software components are upgraded to meet new feature and security requirements.

> [!note]- Long environment setup time.
> Setting up a development environment or spinning up a new production VM can involve a long list of instructions and take considerable time. To avoid compatibility issues, we must also ensure that these new environments use the correct OS and the appropriate versions of all deployed components and their dependencies.

> [!note]- Difference in Dev / Test / Prod environments. 
> Due to the complex process of setting up new environments, configuration mismatch among them might occur. Moreover, developers and QA engineers might prefer one OS to another. It is difficult to guarantee that the applications we are building would run the same in different environments.

**Docker** as a *container* technology promises to address these issues. 
>[!info] 
>Containers are not a new concept with Docker, as various container technologies like LXC and LXD existed long before it. What Docker brings to the table is a high-level toolchain that simplifies the process of setting up container environments, including tasks like creating container images, managing image registries, pulling images, starting containers from images, and more.

Each piece of software runs in its own *container*, bundled with all the libraries and dependencies it requires. The software configuration only needs to be built once, allowing all developers to start a container from this configuration. This ensures the software behaves consistently across different environments.

**Container vs Virtual Machine**
![[Container vs VM.excalidraw|100%]]

|                      | Virtual Machine                                                                                            | Container                                                                                                                                                           |
| -------------------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Isolation            | Complete isolation from each other                                                                         | Decent but not as strong as VM as more resources are shared between containers such as the OS kernel                                                                |
| Resource utilization | High since there are multiple OS and kernels running. Consume more disk space.                             | Lightweight, consume less resources and disk space.                                                                                                                 |
| Spin-up time         | Slow as it needs to boot the entire OS.                                                                    | Faster. Starting a container under the hood only require setting up kernel features such as namespace, cgroup, etc and `chroot`-ing the container image filesystem. |
| Flexibility          | Can run different OS kernels such as Window or Mac or Linux on the same hardware.                          | Can only run Linux containers on Linux kernel.                                                                                                                      |
| Snapshot             | Most VM technologies support snapshots. VM snapshots consume more disk space.                              | Docker images are lightweight. Containers started from images are guaranteed to be the same.                                                                        |
| Configuration        | Often not supported out of the box. Requires us to use Configuration-as-code technologies such as Ansible. | Supported out of the box with Dockerfile.                                                                                                                           |

---
**Reference**: 