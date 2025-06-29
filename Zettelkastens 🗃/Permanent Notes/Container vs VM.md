---
up:
  - "[[Container MOC]]"
created: 2025-04-13
tags:
---
![[Container vs VM.excalidraw|600]]

| Component            | Docker Container                    | Virtual Machine                          |
| -------------------- | ----------------------------------- | ---------------------------------------- |
| Base Architecture    | Host OS + Docker daemon             | Host OS + Hypervisor + Guest OS          |
| Resource Consumption | Lightweight (measured in megabytes) | Typically larger (measured in gigabytes) |
| Boot Time            | Seconds                             | Minutes                                  |
| Isolation Level      | Shares host kernel                  | Full OS isolation                        |
