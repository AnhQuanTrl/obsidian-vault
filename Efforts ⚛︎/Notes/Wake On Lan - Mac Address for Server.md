---
up:
  - "[[Homelab]]"
created: 2025-01-18
tags:
---

| Machine          | Mac Address       | How to wake on Lan                                 |
| ---------------- | ----------------- | -------------------------------------------------- |
| HP Elite Mini    | 5c:60:ba:c6:dd:53 | sudo etherwake -i switch0.100 -b 5c:60:ba:c6:dd:53 |
| Proxmox Main Nas | cc:28:aa:35:ae:18 | sudo etherwake -i switch0.100 -b cc:28:aa:35:ae:18 |
|                  |                   |                                                    |
