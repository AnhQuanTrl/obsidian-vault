---
up:
  - "[[Container MOC]]"
created: 2025-04-13
tags:
---
There are 3 downsides of traditional methods of deploying applications on bare metals or virtual machines:
- Compatibility / Dependency: "The Matrix From Hell".
- Long setup time.
- Difference in Dev / Test / Prod environments. 
![[Pre-container deployment.png]]
Docker solve these challenges by:
- Providing isolated environments that run processes, services, network interfaces, and file system mounts.
- Guarantee that the same container is built when using an identical Docker image.
- Accelerating spin-up time due to the lightweight nature of containers.
- Shifting some deployment responsibility to the developer: Developers now define the application environment within a `Dockerfile`. This eliminate the "work on my machine" problem.