---
up:
  - "[[Operating System MOC]]"
created: 2025-01-21
tags: 
---
Trim is a families of commands that allows an Operating System to inform an SSD disk controller when blocks of memory are free to be reused. They are known as **TRIM** in ATA command set, **UNMAP** in the SCSI command set and **DEALLOCATE** in NVM Express command set. For TRIM commands to work, they must be supported by the operating system or the VM hypervisor.

[[Trim is useful for SSD!]]

Most operating systems support two methods for performing TRIM: **Continuous TRIM** and **Periodic TRIM**.
• **Continuous TRIM:** TRIM commands are issued immediately whenever files are deleted, ensuring the SSD controller is promptly updated.
• **Periodic TRIM:** The OS or hypervisor schedules TRIM commands to run at specific schedules, performing the operation across the entire filesystem during the allocated time.

## Technology-specific How-to(s)
- [[Enable SSD trim on Linux]]
