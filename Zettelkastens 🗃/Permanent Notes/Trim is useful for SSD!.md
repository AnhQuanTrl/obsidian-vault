---
up: 
created: 2025-01-21
tags:
---
 When a file is deleted on most file systems, the operating system doesn’t erase its data immediately. Instead, it marks the file’s data blocks as “unused” or available for new data. However, the storage device itself (such as an HDD or SSD) doesn’t inherently know which sectors (in HDDs) or pages (in SSDs) are truly free or still contain valid data. This means that when the OS writes new data to these “unused” addresses, the storage device interprets it as overwriting existing data.

## HDDs vs SSDs: Handling Overwrites

• **HDDs (Hard Disk Drives):** There’s no distinction between writing to an empty sector and overwriting an existing one. The drive simply writes the new data to the physical location.

• **SSDs (Solid-State Drives):** SSDs cannot overwrite data directly in a page. Instead, they write the new data to a different, empty page. If there are no empty pages available, the SSD must erase entire blocks of data (since SSDs erase data in blocks, not pages) before it can write the new data. This erasure process can trigger additional writes to consolidate valid data, a phenomenon known as [Write Amplification](https://thessdguy.com/what-is-write-amplification/). Write amplification reduces the SSD’s performance and lifespan over time.

## The Role of TRIM

The **TRIM** command helps address this issue by notifying the SSD’s controller about which pages in a block are no longer in use after files are deleted. With this information, the SSD can optimize its **Garbage Collection** process, which involves:

1. Organizing and consolidating valid data into fewer blocks.

2. Erasing blocks with invalid pages to free up space.

By using TRIM, the SSD avoids unnecessary writes and erasures, minimizing write amplification and maintaining optimal performance and durability.