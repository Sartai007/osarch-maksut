\# Lab 3 — Teardown Without a Screwdriver



\## 1. Laptop Identification



\- \*\*Manufacturer:\*\* Lenovo

\- \*\*Model:\*\* IdeaPad Slim 3 15IRH10R

\- \*\*Machine Type:\*\* 83K4

\- \*\*Processor:\*\* Intel Core 5 210H

\- \*\*Installed RAM:\*\* 16 GB

\- \*\*Storage:\*\* 1 TB Micron NVMe SSD



\### Documentation



\- \[Lenovo Hardware Maintenance Manual (PDF)](https://gzhls.at/blob/ldb/2/4/9/7/65c8362a20383713f5490cb12017b4fbb7e5.pdf)

\- \[Lenovo Official Product Specifications (PSREF)](https://psref.lenovo.com/)

\- \[Lenovo Parts Lookup](https://support.lenovo.com/partslookup)



The laptop model was identified using Windows PowerShell commands. The Hardware Maintenance Manual covers the IdeaPad Slim 3 15IRH10R, including machine type 83K4.



\## 2. Internal Components



The exploded view is located on PDF page 29 (printed manual page 23).



!\[Lenovo IdeaPad Slim 3 exploded view](evidence/manual-figures/exploded-view.png)



| No. | Component | Function |

|---|---|---|

| 1 | LCD module | Displays visual output |

| 2 | Upper case | Upper chassis structure |

| 3 | I/O board | Provides input/output connections |

| 4 | I/O board cable | Connects the I/O board |

| 5 | Wi-Fi card | Provides wireless connectivity |

| 6 | SSD | Stores the operating system and files |

| 7 | SSD thermal pad | Transfers heat away from the SSD |

| 8 | Touchpad cable | Connects the touchpad |

| 9 | Speaker | Produces audio |

| 10 | Battery pack | Supplies power when unplugged |

| 11 | Lower case | Bottom chassis cover |

| 12 | Fan | Moves air for cooling |

| 13 | Heat sink | Transfers heat away from components |

| 14 | Memory module | Provides temporary working memory |

| 15 | DDR absorber | Absorbs/cushions around the memory assembly |

| 16 | System board | Main board connecting components |



\## 3. Upgrade Possibilities



| Component | Findings | Verdict |

|---|---|---|

| RAM | 8 GB soldered memory + one removable SODIMM slot. Lenovo lists configurations up to 24 GB (8 GB soldered + 16 GB SODIMM). | Upgradeable |

| SSD | Removable M.2 2242 PCIe 4.0 ×4 SSD. Lenovo specifications list two M.2 slots and tested configurations up to 1 TB per drive. | Replaceable / expandable |

| CPU | Intel Core 5 210H. The maintenance manual documents system-board replacement but does not provide a separate CPU replacement procedure. | No separate CPU upgrade documented |



\### RAM



The Hardware Maintenance Manual describes releasing two socket latches to remove the memory module. Lenovo Parts Lookup lists 8 GB and 16 GB DDR5-5600 SODIMM replacement modules.



Windows reports 16 GB of installed memory, with one 8 GB device identified as a SODIMM. The official Lenovo specifications describe 8 GB soldered memory and one SODIMM slot.



\### SSD



The manual describes removing the SSD by removing one screw and pulling the drive out of its slot. Windows identifies the installed drive as a 1 TB Micron NVMe SSD.



Lenovo's product specifications list M.2 2242 PCIe 4.0 ×4 storage slots.



\### CPU



Windows identifies the processor as Intel Core 5 210H. The maintenance manual documents replacement of the system board, but not a separate CPU replacement procedure. Therefore, a CPU upgrade is not documented as a standalone replacement option.



\## 4. Hardware Evidence from Windows



Hardware information was collected using PowerShell and saved in:



`evidence/windows-specs.txt`



| Hardware | Windows result |

|---|---|

| Manufacturer | LENOVO |

| Model | 83K4 |

| System family | IdeaPad Slim 3 15IRH10R |

| CPU | Intel Core 5 210H |

| CPU cores | 8 |

| Logical processors | 12 |

| Total RAM | Approximately 16 GB |

| RAM configured speed | 4800 MT/s |

| Storage | Micron NVMe SSD |

| Storage capacity | Approximately 1 TB |

| System board product | LNVNB161216 |



\## 5. Sources



1\. Lenovo IdeaPad Slim 3 15IRH10R Hardware Maintenance Manual, especially the exploded view and component removal procedures.

2\. Lenovo Product Specifications Reference (PSREF).

3\. Lenovo Parts Lookup.

4\. Windows PowerShell hardware inventory (`evidence/windows-specs.txt`).




Comparison: 
### 8. Comparison of Hardware Information Across Two Operating Systems

| Hardware fact         | Windows (physical laptop)                                                                    | Linux (Ubuntu VMware VM)                                                                                                       |
| --------------------- | -------------------------------------------------------------------------------------------- |
| CPU model             | `Win32_Processor – Name`: Intel Core 5 210H                                                  | `lscpu – Model name`: Intel Core 5 210H                                                                                        |
| Physical cores        | `Win32_Processor – NumberOfCores`: 8                                                         | `lscpu – Core(s) per socket`: 1 (2 virtual sockets; physical core count unavailable)                                           |
| Logical CPUs          | `Win32_Processor – NumberOfLogicalProcessors`: 12                                            | `lscpu – CPU(s)`: 2                                                                                                            |
| Total memory          | `Win32_ComputerSystem – TotalPhysicalMemory`: 16,824,262,656 bytes (approximately 15.67 GiB) | `free -h – Mem: total`: 7.2 GiB                                                                                                |
| Memory type and speed | `Win32_PhysicalMemory – SMBIOSMemoryType`: DDR5; `ConfiguredClockSpeed`: 4800 MT/s           | `dmidecode -t memory – Type`: EDO DIMM; speed unavailable (virtual DMI data, unreliable)                                       |
| Disk type             | `Get-PhysicalDisk – MediaType`: SSD                                                          | `lsblk – MODEL`: VMware Virtual S; 40 GB virtual disk                                                                          |
| Disk interface        | `Get-PhysicalDisk – BusType`: NVMe                                                           | `lsblk – TRAN`: spi (reported by the virtual device)                                                                           |
| Motherboard           | `Win32_BaseBoard – Manufacturer/Product`: LENOVO LNVNB161216                                 | `dmidecode -t baseboard – Manufacturer/Product Name`: Intel Corporation 440BX Desktop Reference Platform (virtual motherboard) |

Explanation:

The Windows and Linux outputs show some differences because they were collected from two different environments: Windows runs directly on the physical Lenovo laptop, while Ubuntu runs inside a VMware virtual machine. Although both systems report the same CPU model (Intel Core 5 210H), Ubuntu detects only two virtual CPUs and 7.2 GiB of allocated memory, whereas Windows detects the laptop's full 12 logical processors and approximately 15.67 GiB of physical memory.
The differences in memory type, disk interface, and motherboard information are also caused by virtualization. Ubuntu reports virtual hardware provided by VMware rather than the laptop's actual components. Therefore, the Windows results represent the physical hardware more accurately, while the Linux results demonstrate how an operating system detects hardware inside a virtual machine.
