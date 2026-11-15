# Ticket 2 — We are kitting out the new office

## 1. Requirements and interpretation

The office needs four different workstations: Accountant, Sales, Web Developer and Designer. The total budget ceiling is **3,000,000 KZT**. Each workstation must include at least 16 GB RAM, a 1 TB SSD, a licensed operating system and a monitor.

The director's suggestion to buy four identical computers is not suitable. The roles have different workloads. Giving every employee the same machine would either spend too much on office workstations or leave the developer/designer systems underpowered.

The workload descriptions below are planning assumptions. The actual applications and typical project sizes should be confirmed with each employee before purchase.

## 2. Proposed workstation allocation

| Role | Main configuration | Workload bottleneck addressed | Total |
|---|---|---|---:|
| Accountant | Ryzen 5 5500GT, 16 GB DDR4, integrated graphics | Reliable office multitasking and spreadsheets; no discrete GPU needed | 480,730 ₸ |
| Sales | Ryzen 5 5600GT, 32 GB DDR4, integrated graphics | Browser tabs, CRM, Excel and video calls make memory capacity more important than a high-end CPU | 588,720 ₸ |
| Web Developer | Core i5-14400, 32 GB DDR4, integrated graphics | IDEs, browser testing, local services and moderate containers benefit from CPU cores and 32 GB RAM | 569,010 ₸ |
| Designer | Ryzen 5 7500F, RTX 5060 Ti 16 GB, 32 GB DDR5, WQHD monitor | GPU acceleration and VRAM for design applications and moderate 3D work | 1,250,510 ₸ |

The detailed component lists, loads, bottlenecks, trade-offs and compatibility notes are in `builds.md`. Dated component prices and Kazakhstan vendor links are in `budget.csv`.

## 3. Budget summary

| Item | Amount |
|---|---:|
| Four custom workstations, including monitors and Windows licences | **2,888,970 ₸** |
| Budget ceiling | **3,000,000 ₸** |
| Remaining headroom | **111,030 ₸** |

The listed component budget includes four monitors and four Windows licences. It does **not** include keyboards, mice, assembly, delivery or paid specialist application licences. Therefore, the remaining 111,030 ₸ is a limited contingency, not proof that every possible setup expense is covered. These costs must be confirmed before ordering. Prices are dated catalogue checks, not formal quotations, and can change.

## 4. Decisions and answers to the director

### Why should the four computers not be identical?

The accountant mainly uses accounting software, spreadsheets, browsers and PDF invoices. Integrated graphics and 16 GB RAM are a cost-effective fit. Sales uses CRM, many browser tabs, Excel and frequent video calls, so 32 GB RAM reduces the risk of memory pressure. The developer runs IDEs, browser tests, local servers and possibly containers; the i5-14400 and 32 GB RAM provide more parallel processing capacity. The designer works with graphics applications and moderate 3D, so the dedicated RTX 5060 Ti with 16 GB VRAM is justified. Identical systems would waste money on some roles and constrain others.

### Which machine should be upgraded first after 18 months, and why?

**The Designer workstation should be considered first for a RAM upgrade from 32 GB to 64 GB.** Larger Photoshop documents, multiple creative applications and more complex 3D scenes can consume more memory. This is a forecast based on the assumed workload, not a guarantee that an upgrade will be needed exactly after 18 months. The exact memory configuration and motherboard support should be checked before adding modules.

### Which employee is most likely to complain about performance within the first month, and about what?

**The Web Developer is the most likely**, if their real workflow involves several Docker containers, local databases, IDEs, builds and many browser tabs running simultaneously. The likely complaint would be memory pressure, swapping or slower parallel builds. The selected 32 GB configuration should be adequate for moderate development work, but heavier workloads may justify 64 GB later. This prediction depends on the employee's actual development stack.

### What is gained and lost by buying pre-built systems instead?

The Shop.kz pre-built comparison totals **3,619,500 ₸**, including monitors and additional Windows licences where the desktop listing does not include an operating system. This is **730,530 ₸ more** than the custom proposal and exceeds the 3,000,000 ₸ ceiling by **619,500 ₸**.

Buying pre-built can provide a ready-to-use computer, one vendor contact for system-level warranty support, factory assembly and less time spent selecting and troubleshooting parts. The HP office systems in the comparison include Windows 11 Home SL and wired keyboard/mouse.

The trade-off is less control over exact components and less ability to tailor each PC to its role. The Developer pre-built includes an RTX 3050 that is not necessary for the assumed workload. The Designer pre-built has an RTX 5060 Ti with 8 GB VRAM, compared with 16 GB in the proposed custom build. The comparison is not perfectly like-for-like: HP includes keyboard and mouse while the custom budget does not. The pre-built prices and caveats are documented in `evidence/vendor-quotes/prebuilt-comparison.md`.

## 5. Compatibility, evidence and procurement limitations

The four PCPartPicker configurations are included as compatibility-comparison evidence, not as Kazakhstan price sources. PCPartPicker catalogue selections sometimes differ from the actual planned purchase because an exact local component was not available in its catalogue. `pcpartpicker-links.md` identifies every known substitution. The actual models and Kazakhstan prices remain in `budget.csv`.

The compatibility review is specification-based:
- The four CPU/motherboard combinations use the correct socket/platform families. Exact board revision and BIOS support should be checked against the manufacturer's CPU support page for the specific board revision.
- The memory generation and general speed match each motherboard. Exact QVL approval for every retail kit has not been independently established.
- The AGI AI828 is a PCIe Gen4 M.2 SSD. It is backward-compatible; the Accountant and Sales platforms may operate it at Gen3 speeds depending on the CPU and M.2 slot.
- The ID-Cooling SE-214-XT V2 supports the selected AM4, AM5 and LGA1700 platforms. Its 152 mm height fits the selected actual cases: PCCooler MA100 (160 mm limit) and Ocypus Gamma C52 (170 mm limit).
- The Designer RTX 5060 Ti 16 GB is 262.1 mm long. The Ocypus case supports up to 425 mm. The selected Lian Li 650 W PSU exceeds the GPU maker's 600 W recommendation; confirm the exact PSU model and included native PCIe 8-pin (6+2) cable.
- If the AGI SSD supplied for the Designer has its own heatsink, do not stack it with the motherboard M.2 Thermal Guard.
- Windows 11 setup requires UEFI, Secure Boot and firmware TPM to be enabled. Confirm licence authenticity and activation.

The PCPartPicker green compatibility banner is useful supporting evidence, but it does not prove local availability, exact QVL approval, BIOS version, Windows activation or that every unverified item has been physically tested.

### Evidence status

- [x] Four PCPartPicker configuration links recorded.
- [x] Kazakhstan component prices and dates recorded in `budget.csv`.
- [x] Workload, bottleneck and trade-off explained for all four roles.
- [x] Pre-built comparison and its limitations documented.
- [x] Compatibility sources and remaining verification limits documented.
- [ ] Attach screenshots or saved formal vendor quotations if available. The current pre-built comparison uses dated online listing prices, not fabricated formal quotations.
- [ ] Confirm any extra costs (peripherals, assembly and delivery) fit within the remaining budget before purchase.
