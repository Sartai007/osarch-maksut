# Ticket 2 — We are kitting out the new office

## 1. What was asked

The director requested four computers for a new office: one each for an accountant, a sales employee, a web developer and a designer. The total budget is **3,000,000 ₸**, including monitors. The director also asked whether buying four identical computers would be appropriate and requested systems that should last for a few years.

The minimum technical requirements are:

- At least 16 GB RAM per computer.
- At least one 1 TB SSD per computer.
- A licensed operating system for each computer.
- One monitor for each employee.

The director also needs a justified recommendation, not simply a list of computer components. The recommendation must explain the workload each workstation is intended for, its likely bottleneck and the trade-off accepted to remain within budget. It must also compare custom-built systems with pre-built alternatives and answer the three questions about future upgrades, likely performance complaints and the advantages and disadvantages of buying pre-built systems.

## 2. What was actually needed

The request leaves several important decisions unspecified. These had to be interpreted before choosing components.

**Four identical computers would not meet the different needs equally well.** An accountant mainly working with spreadsheets and accounting software does not need the same graphics hardware as a designer. A developer may benefit more from CPU performance and memory capacity, while a designer may need a dedicated graphics card and more video memory. Buying identical systems could waste money on some roles while limiting others.

**The actual workloads were not specified.** The request does not name the accounting software, CRM, development tools, design applications, project sizes or number of applications employees use simultaneously. I therefore used reasonable planning assumptions:

- Accountant: accounting software, spreadsheets, browsers and PDF invoices.
- Sales: CRM, many browser tabs, Excel and video calls.
- Web Developer: IDEs, code editors, browser testing, local development services and software builds.
- Designer: graphics applications and moderate 3D work.

These are assumptions, not confirmed employee requirements. The applications and typical project sizes should be checked with the employees before purchasing.

**"Budget for everything" is ambiguous.** The brief does not specify whether keyboards, mice, assembly, delivery or paid specialist software licences must be included. I treated the 3,000,000 ₸ ceiling as covering the four computers, four monitors and four Windows licences. The current component budget does not include keyboards, mice, assembly, delivery or paid specialist application licences. These expenses are outside the current budget scope, as agreed for this proposal. If the director later requires them to be included in the 3,000,000 ₸ ceiling, the budget must be recalculated.

**The monitor requirement is incomplete.** The director requested monitors but did not specify size, resolution or panel type. I selected standard 24-inch Full HD IPS monitors for the Accountant, Sales and Web Developer, and a 27-inch WQHD IPS monitor for the Designer.

**The expected service life is not precisely defined.** "Last a few years" does not specify a number of years or future workload growth. I interpreted it as choosing components that meet the assumed current workloads while leaving some scope for future upgrades. The proposed configurations are not a guarantee that no upgrades or repairs will be needed.

**Operating-system decision:** Windows 11 Home is sufficient for the intended office use and is the edition included in the budget.

## 3. What I did

I designed four different workstations around the assumed workloads, checked the component combinations at specification level, compared the proposed builds with pre-built systems available from a Kazakhstan retailer, and calculated the total using dated component prices in tenge.

### Proposed workstations

| Role | Main configuration | Workload bottleneck addressed | Total |
|---|---|---|---:|
| Accountant | Ryzen 5 5500GT, 16 GB DDR4, integrated graphics | Office multitasking and spreadsheets; a discrete GPU is unnecessary for the assumed workload | 480,730 ₸ |
| Sales | Ryzen 5 5600GT, 32 GB DDR4, integrated graphics | Browser tabs, CRM, Excel and video calls; additional memory helps reduce memory pressure | 601,720 ₸ |
| Web Developer | Core i5-14400, 32 GB DDR4, integrated graphics | IDE use, browser testing, local services and software builds benefit from CPU cores and memory | 582,010 ₸ |
| Designer | Ryzen 5 7500F, RTX 5060 Ti 16 GB, 32 GB DDR5, WQHD monitor | Graphics acceleration, video memory and a higher-resolution display for creative work | 1,250,510 ₸ |

The detailed component lists, individual prices, workload explanations, trade-offs and compatibility notes are in `builds.md`. The component-level budget, vendor links and price dates are in `budget.csv`.

### Budget result

| Item | Amount |
|---|---:|
| Accountant workstation | 480,730 ₸ |
| Sales workstation | 601,720 ₸ |
| Web Developer workstation | 582,010 ₸ |
| Designer workstation | 1,250,510 ₸ |
| **Total for four workstations** | **2,914,970 ₸** |
| Budget ceiling | 3,000,000 ₸ |
| **Remaining headroom** | **85,030 ₸** |

The proposed systems meet the stated minimums of 16 GB RAM, 1 TB SSD, licensed operating system and monitor for each employee. The total is 85,030 ₸ below the ceiling. However, this remaining amount is only a limited contingency; it does not establish that all excluded expenses will fit.

### Why should the four computers not be identical?

The Accountant's assumed workload is mainly office applications, spreadsheets and documents, so integrated graphics and 16 GB RAM are a cost-effective choice. Sales needs more memory for CRM, browser tabs, spreadsheets and video calls. The Developer needs CPU capacity and 32 GB RAM for IDEs, browser testing, local development services and software builds. The Designer benefits from a dedicated RTX 5060 Ti with 16 GB VRAM and a WQHD monitor.

The systems are therefore allocated according to their intended workloads rather than using the same parts for all four employees. This avoids spending on unnecessary graphics hardware for office roles while giving the Designer a more capable graphics system.

### Which machine should be upgraded first after 18 months, and why?

**The Designer workstation should be considered first for a RAM upgrade from 32 GB to 64 GB.** Larger design files, multiple creative applications and more complex 3D scenes may use more memory over time. This is a forecast based on the assumed workload, not a guarantee that an upgrade will be needed after exactly 18 months. The motherboard's supported memory configurations and the installed modules should be checked before purchasing additional RAM.

### Which employee is most likely to complain about performance within the first month, and about what?

**The Web Developer is the most likely**, if their actual workflow involves IDEs, local development services, software builds and many browser tabs running simultaneously. The likely complaint would be memory pressure or slower builds when several applications are open. The selected 32 GB configuration is intended to be adequate for moderate development work. This prediction depends on the employee's actual tools and workload.

### What is gained and lost by buying pre-built systems instead?

The pre-built comparison uses dated Shop.kz catalogue prices checked on **15 November 2026**. It totals **3,619,500 ₸**, including monitors and additional Windows licences where the desktop listing does not include an operating system. This is **704,530 ₸ (approximately 24.2%) more** than the custom proposal and exceeds the 3,000,000 ₸ budget by **619,500 ₸**.

Buying pre-built can provide a ready-to-use computer, factory assembly, less time spent selecting and troubleshooting components, and one vendor contact for system-level warranty support. The HP office systems in the comparison include Windows 11 Home SL and a wired keyboard and mouse.

The disadvantages are less control over the exact components and less ability to tailor each system to its employee. The Developer pre-built includes an RTX 3050 that is unnecessary for the assumed workload. The Designer pre-built has an RTX 5060 Ti with 8 GB VRAM, compared with 16 GB in the proposed custom build. The comparison is not perfectly like-for-like: the HP systems include keyboards and mice, while the custom budget does not. No formal vendor quotations were obtained; the comparison uses public online catalogue prices. The full comparison and its limitations are in `evidence/vendor-quotes/prebuilt-comparison.md`.

## 4. Evidence

The project evidence is organised as follows:

- `budget.csv` — component-level prices in tenge, vendor links and dates checked.
- `builds.md` — detailed workstation specifications, workload reasoning, bottlenecks, trade-offs and component compatibility notes.
- `evidence/pcpartpicker-links.md` — four PCPartPicker configuration links, known catalogue substitutions and links to the saved screenshots.
- `evidence/pcpartpicker/` — screenshots of the four PCPartPicker configurations.
- `evidence/compatibility-sources.md` — manufacturer and component references used for the specification-based compatibility review.
- `evidence/vendor-quotes/prebuilt-comparison.md` — pre-built catalogue comparison, prices and limitations.
- `evidence/vendor-quotes/README.txt` — explanation of the pre-built price evidence.

### Compatibility and verification limitations

The four PCPartPicker configurations are supporting compatibility-comparison evidence, not sources for Kazakhstan prices. Some PCPartPicker catalogue selections differ from the actual planned purchase because an exact local component was not available in its catalogue. The known substitutions are identified in `evidence/pcpartpicker-links.md`. The actual planned models and Kazakhstan prices are recorded in `budget.csv`.

The compatibility review is specification-based:

- The four CPU and motherboard combinations use the appropriate socket/platform families. Exact board revision and BIOS support should be checked against the manufacturer's CPU support page for that revision.
- The memory generation and general speed match the selected motherboard platforms. Exact QVL approval for every retail memory kit has not been independently established.
- The AGI AI828 is a PCIe Gen4 M.2 SSD. It is backward-compatible; the Accountant and Sales platforms may operate it at Gen3 speeds depending on the CPU and M.2 slot.
- The ID-Cooling SE-214-XT V2 supports the selected AM4, AM5 and LGA1700 platforms. Its 152 mm height fits the selected actual cases: PCCooler MA100 (160 mm limit) and Ocypus Gamma C52 (170 mm limit).
- The Designer RTX 5060 Ti 16 GB is 262.1 mm long. The Ocypus case supports up to 425 mm. The selected Lian Li 650 W PSU exceeds the GPU maker's 600 W recommendation; the exact PSU model and included native PCIe 8-pin (6+2) cable should be confirmed.
- If the AGI SSD supplied for the Designer has its own heatsink, it should not be stacked with the motherboard M.2 Thermal Guard.
- Windows 11 setup requires UEFI, Secure Boot and firmware TPM to be enabled. Licence authenticity and activation must be confirmed.

The PCPartPicker green compatibility banner is useful supporting evidence, but it does not prove local availability, exact QVL approval, BIOS version, Windows activation or that every unverified item has been physically tested. Prices are dated catalogue checks, not formal quotations, and can change.

### Evidence checklist

- [x] Four PCPartPicker configuration links recorded.
- [x] Four PCPartPicker screenshots saved and linked.
- [x] Kazakhstan component prices and dates recorded in `budget.csv`.
- [x] Workload, bottleneck and trade-off explained for all four roles.
- [x] Pre-built comparison and its limitations documented.
- [x] Compatibility sources and remaining verification limits documented.
- [x] Workload descriptions treated as planning assumptions and accepted for this proposal.
- [x] Windows 11 Home confirmed as sufficient for the intended office use.
- [ ] Obtain formal vendor quotations and confirm stock and final prices.
- [x] Peripherals, assembly, delivery and specialist software explicitly excluded from the current budget.

## 5. What I would do differently

Before making a final purchase recommendation, I would interview each employee and record the exact applications they use, typical project sizes and how many demanding applications they run at once. This would help determine whether 16 GB is sufficient for the Accountant and whether 32 GB is enough for the Developer and Designer.

I would also obtain formal written quotations from Kazakhstan vendors instead of relying only on online catalogue prices. I would confirm stock, delivery, assembly costs, warranty terms, Windows edition and licence activation, and whether keyboards, mice and paid software must be included in the 3,000,000 ₸ ceiling.

Finally, I would verify the exact motherboard revisions, BIOS versions, memory support, physical clearances and PSU cables with the supplier or during assembly. If possible, I would test the Developer's real development stack and the Designer's real creative applications before deciding whether to increase memory or change any component. These checks would turn the current planning proposal into a purchase-ready specification.
