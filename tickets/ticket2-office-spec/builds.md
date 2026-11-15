# Ticket 2 — Four workstation builds

**Price-check dates:** 14–15 November 2026
**Main component vendor:** Shop.kz (Beliy Veter)
**Monitor vendors:** Technodom for the three Neo monitors; Shop.kz for the AOC designer monitor
**Budget ceiling:** 3,000,000 KZT

> Workloads are planning assumptions. Prices are dated online catalogue prices, not formal quotations. The actual Kazakhstan purchase models and prices below are authoritative for the budget. PCPartPicker comparison substitutions are listed separately in `evidence/pcpartpicker-links.md`.

## 1. Accountant — 480,730 ₸

**Load:** Accounting software, spreadsheets, browser tabs, PDF invoices and document handling.

**Bottleneck:** Memory capacity and everyday responsiveness matter more than graphics performance. The workload does not justify a discrete GPU. 16 GB RAM meets the stated minimum and keeps the entry-level system affordable.

**Trade-off:** A Ryzen 5 5500GT with integrated graphics is used instead of a more expensive CPU/GPU combination. The budget is directed toward a 1 TB SSD, a monitor and a Windows licence.

| Component | Actual planned model |
|---|---|
| CPU | AMD Ryzen 5 5500GT AM4 OEM |
| Motherboard | Gigabyte A520M H ARGB |
| RAM | GeIL Orion 16GB (2×8GB) DDR4-3200, GOG416GB3200C16BDC |
| SSD | AGI AI828 1TB M.2 PCIe 4.0 TLC |
| CPU cooler | ID-Cooling SE-214-XT V2 |
| PSU | Thermaltake TR2 S 550W |
| Case | PCCooler MA100 MESH BK |
| Monitor | Neo SO24FIW14NB, 24-inch FHD IPS |
| OS | Microsoft Windows 11 Home 64-bit USB retail licence |

**Compatibility notes:** AM4 CPU and motherboard platform; check the exact A520M H ARGB revision and BIOS CPU-support list. The board uses DDR4 and has an M.2 slot; the Gen4 SSD will operate at the board's supported link speed. The 152 mm cooler fits the MA100's 160 mm cooler clearance. The 550 W PSU is ample for the integrated-graphics system. Connect the monitor to the motherboard video output.

## 2. Sales — 601,720 ₸

**Load:** CRM in a browser, approximately 30–40 tabs, Excel and frequent video calls, sometimes simultaneously.

**Bottleneck:** RAM capacity. Many browser tabs, CRM, spreadsheets and video conferencing can create memory pressure. 32 GB is a more appropriate target than spending extra on a high-end CPU.

**Trade-off:** The Ryzen 5 5600GT is a mid-range APU with integrated graphics. A discrete GPU is omitted and the budget is used for 32 GB RAM, storage, monitor and licensed OS.

| Component | Actual planned model |
|---|---|
| CPU | AMD Ryzen 5 5600GT AM4 OEM |
| Motherboard | Gigabyte B550M GAMING X WIFI6 |
| RAM | GeIL Pristine 32GB (2×16GB) DDR4-3200, GP432GB3200C22DC |
| SSD | AGI AI828 1TB M.2 PCIe 4.0 TLC |
| CPU cooler | ID-Cooling SE-214-XT V2 |
| PSU | Thermaltake TR2 S 550W |
| Case | PCCooler MA100 MESH BK |
| Monitor | Neo SO24FIW14NB, 24-inch FHD IPS |
| OS | Microsoft Windows 11 Home 64-bit USB retail licence |

**Compatibility notes:** AM4 platform; verify the exact B550M board revision and BIOS CPU support for the 5600GT. The board supports DDR4; exact QVL status for the GeIL kit is not claimed. With the 5600GT, the SSD may operate at Gen3 speeds in the CPU-connected M.2 path. The 152 mm cooler fits the MA100's 160 mm limit. Integrated graphics drive the monitor from the motherboard output.

## 3. Web Developer — 582,010 ₸

**Load:** IDEs, browser testing, local development servers, databases and software builds (moderate development workload).

**Bottleneck:** Parallel CPU work and memory when several tools/services run together. 32 GB RAM provides headroom for a moderate development stack.

**Trade-off:** The Intel Core i5-14400 and 32 GB RAM are prioritised over a dedicated GPU. The non-F i5-14400 includes integrated graphics, avoiding the cost and power draw of a discrete graphics card.

| Component | Actual planned model |
|---|---|
| CPU | Intel Core i5-14400 LGA1700 OEM |
| Motherboard | Gigabyte B760M D3HP DDR4 |
| RAM | GeIL Pristine 32GB (2×16GB) DDR4-3200, GP432GB3200C22DC |
| SSD | AGI AI828 1TB M.2 PCIe 4.0 TLC |
| CPU cooler | ID-Cooling SE-214-XT V2 |
| PSU | Thermaltake TR2 S 550W |
| Case | PCCooler MA100 MESH BK |
| Monitor | Neo SO24FIW14NB, 24-inch FHD IPS |
| OS | Microsoft Windows 11 Home 64-bit USB retail licence |

**Compatibility notes:** LGA1700 platform; the B760M D3HP DDR4 CPU support list includes the i5-14400 from BIOS F1. The board uses DDR4, matching the GeIL kit's memory generation and speed; exact QVL approval is not claimed. The board supports PCIe Gen4 M.2. The 152 mm cooler fits the MA100's 160 mm clearance. The i5-14400 includes Intel UHD 730 graphics; connect the monitor to the motherboard output.

## 4. Designer — 1,250,510 ₸

**Load:** Photoshop/Illustrator/Figma and moderate 3D work. The exact application versions, file sizes and rendering requirements should be confirmed.

**Bottleneck:** GPU performance and VRAM for accelerated effects, viewports and 3D scenes; system RAM can become a later constraint as projects grow.

**Trade-off:** The Ryzen 5 7500F is paired with a dedicated RTX 5060 Ti 16 GB and 32 GB DDR5. This role receives the largest allocation because it has the most graphics-intensive workload. A 27-inch WQHD monitor is selected for workspace.

| Component | Actual planned model |
|---|---|
| CPU | AMD Ryzen 5 7500F AM5 OEM |
| Motherboard | Gigabyte A620M GAMING X AX |
| RAM | Apacer Panther RGB 32GB (2×16GB) DDR5-5600, AH5U32G56C5227BAA-2 |
| SSD | AGI AI828 1TB M.2 PCIe 4.0 TLC |
| GPU | Palit RTX 5060 Ti White OC 16GB |
| CPU cooler | ID-Cooling SE-214-XT V2 |
| PSU | Lian Li RB0650B 650W 80+ Bronze |
| Case | Ocypus Gamma C52 BK ARGB |
| Monitor | AOC Q27B36X, 27-inch WQHD IPS |
| OS | Microsoft Windows 11 Home 64-bit USB retail licence |

**Compatibility notes:** AM5 / Ryzen 7000 platform. The board uses DDR5; 5600 MT/s is within its supported memory profile specifications, but exact Apacer QVL approval is not claimed. The 152 mm cooler fits the case's 170 mm clearance. The Palit GPU is 262.1 mm long and fits within the case's 425 mm GPU clearance. The GPU has one 8-pin power connector and recommends a 600 W PSU; the selected 650 W Lian Li unit exceeds that wattage recommendation. Confirm the exact PSU model and native PCIe 6+2-pin cable. The 7500F has no integrated graphics, so the monitor must connect to the RTX 5060 Ti. Use DisplayPort for the intended WQHD/high-refresh display mode.

## Budget summary

| Role | Total |
|---|---:|
| Accountant | 480,730 ₸ |
| Sales | 601,720 ₸ |
| Web Developer | 582,010 ₸ |
| Designer | 1,250,510 ₸ |
| **Total** | **2,914,970 ₸** |
| Budget ceiling | 3,000,000 ₸ |
| **Remaining** | **85,030 ₸** |

The totals include the listed monitors and Windows licences. They exclude keyboard/mouse sets, assembly, delivery and paid specialist software. Do not describe the remaining 85,030 ₸ as sufficient for all extras until those prices are checked.

## Overall compatibility limitations

Compatibility is assessed from published specifications, not physical assembly testing. Exact RAM QVL approval is not asserted. Verify motherboard revision/BIOS, exact RAM kit number, SSD heatsink version and Designer PSU cable before purchase. Windows 11 requires UEFI, Secure Boot and firmware TPM to be enabled. Refer to `evidence/compatibility-sources.md` for manufacturer references and the detailed compatibility audit.
