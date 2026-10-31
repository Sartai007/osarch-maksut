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

