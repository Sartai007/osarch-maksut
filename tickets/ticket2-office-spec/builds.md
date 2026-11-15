# Ticket 2 — Custom workstation builds and compatibility

**Price-check dates:** 14–15 November 2026  
**Component vendor:** Shop.kz (Beliy Veter)  
**Monitor vendors:** Technodom (three Neo office monitors) and Shop.kz (AOC designer monitor)  
**Total ceiling:** 3,000,000 KZT

> Workloads are planning assumptions. Confirm each employee's actual applications before purchase. Prices are catalogue prices, not formal quotations. The updated 32 GB GeIL DDR4 kits were found at 139,990 KZT each; RAM rows in `budget.csv` now use exact product pages. Other prices remain as originally checked on 14 November.

## Compatibility summary

| Workstation | CPU / board | RAM | SSD | Cooler / case | Power / graphics / display | Overall |
|---|---|---|---|---|---|---|
| Accountant | Ryzen 5 5500GT is listed for A520M H ARGB; verify exact board revision and BIOS with seller | 2×8 GB DDR4-3200 matches board generation/speed; exact QVL not independently confirmed | Gen4 SSD will run at board's Gen3 x4 M.2 limit | AM4 cooler; 152 mm height fits MA100's 160 mm limit | 550 W ample for iGPU system; board HDMI/DP connect to Neo via HDMI | **Compatible on published specs; BIOS/QVL confirmation pending** |
| Sales | Ryzen 5 5600GT belongs to board's supported Ryzen 5000 G-series; verify exact revision/BIOS | 2×16 GB DDR4-3200 matches; exact QVL not independently confirmed | With 5600GT, CPU M.2 path is Gen3; Gen4 drive downshifts | AM4 cooler; 152 mm fits 160 mm case limit | 550 W ample for iGPU system; HDMI/DP available | **Compatible on published specs; BIOS/QVL confirmation pending** |
| Web developer | B760M D3HP DDR4 supports 14th-gen Intel; i5-14400 is LGA1700; CPU support table lists F1 baseline | 2×16 GB DDR4-3200 matches board | Board has PCIe 4.0 x4 M.2; SSD matches | LGA1700 cooler; 152 mm fits 160 mm case limit | 550 W ample without discrete GPU; use motherboard HDMI/DP | **Compatible on published specs; exact RAM QVL pending** |
| Designer | Ryzen 5 7500F is AM5 / Ryzen 7000; A620M board supports Ryzen 7000 | 2×16 GB DDR5-5600 matches DDR5 board; 5600 is memory OC profile; exact QVL pending | Gen4 x4 M.2 matches; check whether AI828 listing is heatsink version before installing under M.2 Thermal Guard | AM5 cooler; 152 mm fits 170 mm case limit | Palit GPU is 262.1 mm; case supports 425 mm. GPU needs one 8-pin and recommends 600 W; selected Lian Li 650 W has adequate rated capacity. Confirm exact PCIe cable in box. | **Compatible on published specs; confirm RAM QVL and PSU cable** |

### Compatibility details and important limits

- **CPU support / BIOS:** The A520M H ARGB support page lists the AM4 Ryzen 5000 G-series family; the CPU-support information the user previously checked listed Ryzen 5 5500GT. For the exact Shop.kz board revision, have the seller confirm the shipped BIOS before purchase. The B550M GAMING X WIFI6 supports Ryzen 5000 G-series; its CPU support table lists Ryzen 5 5600GT on the relevant revision family from FA1, but confirm the exact revision on the delivered board. The B760M D3HP DDR4 supports Intel 14th/13th/12th Gen CPUs and the i5-14400 is listed from BIOS F1. A620M GAMING X AX supports Ryzen 7000/8000/9000; the 7500F is a Ryzen 7000 CPU. Board revision must match the support page.
- **RAM:** Exact retail links and part numbers are now recorded in `budget.csv`. General board specifications match DDR generation and data rate. A general specification match is not the same as an exact QVL listing; QVL status is marked unconfirmed unless the exact part number is visible on Gigabyte's memory list.
- **SSD:** AGI AI828 is M.2 2280 PCIe Gen4 x4. A520M H ARGB is Gen3 x4; B550M with the 5600GT APU runs its CPU-connected M.2 slot at Gen3; B760M and A620M provide Gen4 x4 M.2. PCIe is backward compatible, so the SSD works at the host slot's maximum negotiated speed.
- **SSD heatsink:** AGI's AI828 datasheet lists versions with and without a heatsink. Check which version Shop.kz supplies. On the A620M board, use the SSD heatsink or the motherboard M.2 Thermal Guard according to the manuals; do not stack them.
- **CPU cooler:** ID-Cooling SE-214-XT V2 supports AM4, AM5 and LGA1700 and is 152 mm tall. PCCooler MA100 MESH BK clearance is 160 mm; Ocypus Gamma C52 ARGB clearance is 170 mm.
- **Designer GPU:** Palit RTX 5060 Ti White OC 16 GB is 262.1 mm long, two slots thick, 180 W board power, one 8-pin auxiliary connector, and Palit recommends a 600 W system PSU. Ocypus Gamma C52 supports GPUs up to 425 mm. Lian Li RB0650B is a 650 W ATX 3.1 80 PLUS Bronze PSU. Confirm the exact Shop.kz PSU model and native PCIe 6+2-pin cable; do not use SATA-to-PCIe adapters.
- **Monitor connections:** Neo monitor is connected by HDMI from each motherboard. The 5500GT and 5600GT have integrated Radeon graphics; i5-14400 has Intel UHD 730. The designer's Ryzen 5 7500F has no integrated graphics, so connect the AOC monitor to the RTX 5060 Ti, preferably DisplayPort for 1440p/144 Hz.
- **Operating system:** Windows 11 Home is supported on these modern platforms. Enable UEFI, Secure Boot and firmware TPM (AMD fTPM / Intel PTT). Confirm each retail licence is genuine and activated; Home may be insufficient if the organisation later requires domain join or advanced business management features.

---

## Accountant — 480,730 KZT

- CPU: AMD Ryzen 5 5500GT (6 cores / 12 threads, integrated Radeon Vega 7)
- Motherboard: Gigabyte A520M H ARGB
- RAM: GeIL Orion 16 GB (2×8 GB) DDR4-3200, GOG416GB3200C16BDC
- SSD: AGI AI828 1 TB M.2 PCIe 4.0 TLC
- Cooler: ID-Cooling SE-214-XT V2
- PSU: Thermaltake TR2 S 550 W
- Case: PCCooler MA100 MESH BK
- Monitor: Neo SO24FIW14NB, 24-inch FHD IPS
- OS: Windows 11 Home 64-bit USB retail licence

**Load:** Accounting software, spreadsheets, browser, PDF invoices and document storage.  
**Likely bottleneck:** 16 GB RAM if large spreadsheets, many browser tabs and accounting applications are open simultaneously.  
**Trade-off:** No dedicated graphics card and only the mandatory 16 GB RAM. Both memory slots are occupied, so a future upgrade means replacing the kit rather than adding another pair.

## Sales — 588,720 KZT

- CPU: AMD Ryzen 5 5600GT (6 cores / 12 threads, integrated Radeon Vega 7)
- Motherboard: Gigabyte B550M GAMING X WIFI6
- RAM: GeIL Pristine 32 GB (2×16 GB) DDR4-3200, GP432GB3200C22DC
- SSD: AGI AI828 1 TB M.2 PCIe 4.0 TLC
- Cooler: ID-Cooling SE-214-XT V2
- PSU: Thermaltake TR2 S 550 W
- Case: PCCooler MA100 MESH BK
- Monitor: Neo SO24FIW14NB, 24-inch FHD IPS
- OS: Windows 11 Home 64-bit USB retail licence

**Load:** CRM in a browser, approximately 30–40 tabs, Excel and frequent video calls, potentially at the same time.  
**Likely bottleneck:** Memory capacity if CRM/browser usage expands significantly; 32 GB is a safer starting point than 16 GB.  
**Trade-off:** Spend on 32 GB RAM rather than a discrete GPU or higher-tier CPU. Integrated graphics are adequate for CRM and video calls.

## Web developer — 569,010 KZT

- CPU: Intel Core i5-14400 (10 cores / 16 threads, Intel UHD 730)
- Motherboard: Gigabyte B760M D3HP DDR4
- RAM: GeIL Pristine 32 GB (2×16 GB) DDR4-3200, GP432GB3200C22DC
- SSD: AGI AI828 1 TB M.2 PCIe 4.0 TLC
- Cooler: ID-Cooling SE-214-XT V2
- PSU: Thermaltake TR2 S 550 W
- Case: PCCooler MA100 MESH BK
- Monitor: Neo SO24FIW14NB, 24-inch FHD IPS
- OS: Windows 11 Home 64-bit USB retail licence

**Load:** IDE, browser testing, local development servers, databases, Git tools and moderate Docker/container use.  
**Likely bottleneck:** 32 GB RAM when several containers, databases and browser sessions run together; CPU can become the limit during sustained parallel builds.  
**Trade-off:** No discrete GPU; budget goes to a modern multi-core CPU and 32 GB RAM. Consider 64 GB if the developer's container workload is heavy.

## Designer — 1,250,510 KZT

- CPU: AMD Ryzen 5 7500F (6 cores / 12 threads; no integrated graphics)
- Motherboard: Gigabyte A620M GAMING X AX
- RAM: Apacer Panther RGB 32 GB (2×16 GB) DDR5-5600, AH5U32G56C5227BAA-2
- SSD: AGI AI828 1 TB M.2 PCIe 4.0 TLC
- GPU: Palit GeForce RTX 5060 Ti White OC 16 GB
- Cooler: ID-Cooling SE-214-XT V2
- PSU: Lian Li RB0650B 650 W 80+ Bronze
- Case: Ocypus Gamma C52 BK ARGB
- Monitor: AOC Q27B36X, 27-inch WQHD IPS
- OS: Windows 11 Home 64-bit USB retail licence

**Load:** Photoshop, Illustrator and Figma, plus moderate 3D modelling and rendering.  
**Likely bottleneck:** 32 GB system RAM in larger projects; GPU/VRAM or CPU rendering performance may become limiting for more complex scenes.  
**Trade-off:** The designer receives the only dedicated GPU, with 16 GB VRAM, and the higher-resolution monitor. To stay within budget, the build uses a 6-core Ryzen 5 and a mainstream A620 motherboard rather than a more expensive platform.

---

## Budget summary

| Role | Total |
|---|---:|
| Accountant | 480,730 ₸ |
| Sales | 588,720 ₸ |
| Web developer | 569,010 ₸ |
| Designer | 1,250,510 ₸ |
| **Total** | **2,888,970 ₸** |
| **Remaining from 3,000,000 ₸** | **111,030 ₸** |

The total includes four monitors and four Windows 11 Home licences. It excludes keyboards, mice, assembly, delivery and application licences. The 111,030 KZT remainder must cover those costs and any price movement.

---

## Why the four machines should not be identical

The accountant needs an economical office PC with integrated graphics and 16 GB RAM. Sales needs 32 GB for many browser tabs and concurrent video calls. The developer needs a stronger multi-core CPU and 32 GB for builds, IDEs and containers. The designer needs a dedicated GPU, 16 GB VRAM, DDR5 and a higher-resolution IPS monitor. One identical specification would either overspend on office roles or underserve the design and development roles.

## Manufacturer compatibility references

- A520M H ARGB Rev. 1.1 specifications/support: https://www.gigabyte.com/Motherboard/A520M-H-ARGB-rev-11/support
- B550M GAMING X WIFI6 Rev. 1.0/1.1 specifications/support: https://www.gigabyte.com/Motherboard/B550M-GAMING-X-WIFI6-rev-10-11/support
- B760M D3HP DDR4 specifications/support: https://www.gigabyte.com/Motherboard/B760M-D3HP-DDR4/support
- A620M GAMING X AX Rev. 1.0 specifications/support: https://www.gigabyte.com/Motherboard/A620M-GAMING-X-AX-rev-10/support
- ID-Cooling SE-214-XT V2: https://www.idcooling.com/product/detail?id=560&name=SE-214-XT+V2
- AGI AI828 datasheet: https://agi-gear.com/wp-content/uploads/2026/01/Datasheet_AI828_0128.pdf
- Ocypus Gamma C52 ARGB: https://ocypus.com/specification/case/gamma-c52-argb--0.html
- Palit RTX 5060 Ti White OC 16 GB: https://www.palit.com/palit/vgapro.php?id=5735&lang=en&tab=sp
- Lian Li RB PSU: https://lian-li.com/product/rb-psu/
- Thermaltake TR2 S 550W: https://thermaltake.com/products/tr2-s-550w-dc-to-dc-version
