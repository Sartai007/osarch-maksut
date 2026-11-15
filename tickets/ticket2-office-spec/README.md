# Ticket 2 — We are kitting out the new office

## 1. Requirements and interpretation

The office needs four workstations: Accountant, Sales, Web Developer and Designer. The combined budget ceiling is **3,000,000 KZT**, including monitors and licensed operating systems.

Every workstation must have:
- At least 16 GB RAM
- At least 1 TB SSD storage
- A licensed operating system
- A monitor

The director's assumption that all four machines should be identical is incorrect. The employees have different workloads: accounting and sales are mainly office/browser tasks, development uses IDEs and local services/containers, and design includes 2D applications plus moderate 3D work. Identical PCs would either waste money on office roles or under-specify the designer/developer machines.

The workload descriptions are planning assumptions and should be confirmed with employees before purchasing.

## 2. Proposed workstation allocation

| Role | Main design choice | Estimated total |
|---|---|---:|
| Accountant | Ryzen 5 5500GT integrated graphics, 16 GB RAM | 480,730 ₸ |
| Sales | Ryzen 5 5600GT integrated graphics, 32 GB RAM | 588,720 ₸ |
| Web Developer | Core i5-14400, 32 GB RAM | 569,010 ₸ |
| Designer | Ryzen 5 7500F, RTX 5060 Ti 16 GB, 32 GB DDR5, WQHD monitor | 1,250,510 ₸ |

Detailed components, workloads, bottlenecks, trade-offs and compatibility notes are in `builds.md`. Product links and price dates are in `budget.csv`.

## 3. Budget

| Item | Amount |
|---|---:|
| Four workstations including monitors and Windows licences | **2,888,970 ₸** |
| Budget ceiling | 3,000,000 ₸ |
| Remaining | **111,030 ₸** |

The remainder must cover keyboards, mice, assembly, delivery, application licences and any price changes. Prices are catalogue checks, not formal vendor quotations. The updated RAM product links and the two revised GeIL kit prices are recorded in `budget.csv`.

## 4. Decisions and answers

### Why should the PCs not be identical?

The accountant's work is light and does not require a dedicated GPU, so integrated graphics and 16 GB RAM are cost-effective. Sales needs 32 GB because CRM, many browser tabs, Excel and video calls may run simultaneously. The developer needs a multi-core CPU and 32 GB RAM for IDEs, builds and containers. The designer needs a dedicated GPU with 16 GB VRAM and a WQHD display for 2D/3D work.

### Which machine is most likely to be upgraded first after 18 months, and why?

**Designer workstation — increase system RAM from 32 GB to 64 GB.** Larger Photoshop files, multiple Adobe applications and 3D scenes can use more than 32 GB. The board has four DDR5 slots, so the upgrade can be made by adding a matched kit if the memory configuration and QVL support it. This is a forecast based on the assumed design workload, not a certainty.

### Which employee may complain about performance within the first month, and about what?

**Web developer** is the most likely to notice limitations first if the real workload includes several Docker containers, local databases, IDEs and many browser tabs at once. The likely complaint would be memory pressure or slower parallel builds. If their actual workload is lighter, the 32 GB / i5-14400 build should be adequate. Confirm their development stack before ordering.

### Pre-built vendor comparison

The equivalent Shop.kz pre-built package totals **3,619,500 ₸**, including monitors and the two extra Windows licences required by the listings that ship without an OS. This is **730,530 ₸ more** than the custom proposal. The Designer pre-built is cheaper but has an RTX 5060 Ti with 8 GB VRAM instead of the custom build's 16 GB. The Developer pre-built includes an unnecessary RTX 3050 for the assumed workload. The HP office PCs include Windows 11 Home SL and keyboard/mouse.

The comparison is not perfectly like-for-like: the custom budget excludes keyboards/mice, while the HP package includes them. The i5-14400 pre-built listing also incorrectly reports six CPU cores; confirm its actual CPU specification with the vendor. Full prices, links, differences and caveats are recorded in `evidence/vendor-quotes/prebuilt-comparison.md`.

## 5. Compatibility, procurement and remaining evidence

The proposed parts are compatible at the published specification level:
- The four CPU/motherboard combinations use the correct sockets and supported CPU generations. Confirm the exact board revision and installed BIOS with Shop.kz before ordering, especially for the two AM4 builds.
- All RAM kits match the motherboard DDR generation and general speed support. Exact module QVL approval has not been independently confirmed; the exact retail part numbers and links are now in `budget.csv`.
- The AGI AI828 Gen4 SSD works in all four boards. It will run at Gen3 speeds in the Accountant and Sales systems; it can run at Gen4 speeds in the Developer and Designer systems.
- The ID-Cooling SE-214-XT V2 supports AM4, AM5 and LGA1700. Its 152 mm height fits both selected cases.
- The Designer RTX 5060 Ti fits the Ocypus case and its 650 W Lian Li PSU exceeds Palit's 600 W recommendation. Confirm the PSU includes the native 8-pin PCIe cable.
- The Designer SSD may have an optional heatsink. Confirm the supplied version and do not stack its heatsink with the motherboard M.2 Thermal Guard.
- Windows 11 Home licences are included in the budget. Confirm licence authenticity, activation and whether Home edition meets the organisation's management requirements.

### Evidence checklist

- [x] Exact local product links recorded for all budget rows, including the updated RAM listings.
- [x] Compatibility review for all four workstations recorded in `builds.md`.
- [ ] Four PCPartPicker share URLs and screenshots / warning checks.
- [x] Four role-based pre-built comparisons researched from Shop.kz; save formal vendor quotations/screenshots before submission.
- [ ] Final vendor confirmation of motherboard revision, BIOS, exact RAM kit and Designer PSU cable.
- [ ] Confirm assembly, delivery, keyboard and mouse costs fit within the remaining 111,030 KZT.

See `pcpartpicker-links.md` for the compatibility-list evidence status. Do not submit placeholder links as completed evidence.
