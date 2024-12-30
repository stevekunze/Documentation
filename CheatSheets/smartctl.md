---
tags:
  - smart
  - harddrive
  - hdd
  - PVE
---
	
| **command**                                  | **explenation**                                 |
| -------------------------------------------- | ----------------------------------------------- |
| smartctl -a /dev/sdx                         | prints all smart informations                   |
| smartctl -a /dev/sdx \| grep "SMART support" | only show if smartsupport available and enabled |
