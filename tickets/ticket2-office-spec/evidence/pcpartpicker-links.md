# Compatibility-list evidence — Ticket 2

PCPartPicker lists are used as **comparison/compatibility evidence**. They are not Kazakhstan price quotations and do not replace the actual component models and prices in `budget.csv`.

Some exact Kazakhstan purchase models were not available in the PCPartPicker catalogue. Where a substitute was selected, it is identified below. The substitute is a catalogue proxy only; the actual planned purchase remains the model in `builds.md` and `budget.csv`.

## Saved configurations

| Role | PCPartPicker share link | Screenshot/result noted |
|---|---|---|
| Accountant | https://pcpartpicker.com/list/V96Xh9 | Green compatibility banner shown. [Screenshot](pcpartpicker/accountant.png). Some local case/monitor models were represented by catalogue alternatives. |
| Sales | https://pcpartpicker.com/list/KF7hYX | Latest saved version includes Windows 11 Home Retail USB; green compatibility banner shown. [Screenshot](pcpartpicker/sales.png). |
| Web Developer | https://pcpartpicker.com/list/NXjcyF | Green compatibility banner shown; estimated wattage 257 W. [Screenshot](pcpartpicker/web-developer.png). |
| Designer | https://pcpartpicker.com/list/qbWXh9 | Green compatibility banner shown; estimated wattage 373 W. [Screenshot](pcpartpicker/designer.png). |

## Known catalogue substitutions

| Role | PCPartPicker comparison selection | Actual Kazakhstan-budget component | Reason |
|---|---|---|---|
| Accountant | ID-Cooling SE-214-XT V2 ARGB / catalogue-equivalent cooler; case and monitor catalogue equivalents | ID-Cooling SE-214-XT V2; PCCooler MA100 MESH BK; Neo SO24FIW14NB | Exact local variants were not all present in the catalogue. Confirm socket and physical clearances from manufacturer specifications. |
| Sales | DeepCool CC360 ARGB case; AOC 24G2SP monitor | PCCooler MA100 MESH BK; Neo SO24FIW14NB | Catalogue alternatives used to test a Micro-ATX case and monitor. The actual budget models remain the Shop.kz/Technodom items. |
| Web Developer | DeepCool AG400 cooler; Kingston FURY Beast 32GB DDR4-3200; DeepCool CC360 ARGB case; AOC 24G2SP monitor | ID-Cooling SE-214-XT V2; GeIL Pristine 32GB DDR4-3200; PCCooler MA100 MESH BK; Neo SO24FIW14NB | Exact local GeIL/case/cooler/monitor variants were not all matched in the catalogue. Kingston/DeepCool/AOC are comparison proxies only. |
| Designer | DeepCool AG400 cooler; Kingston FURY Beast 32GB DDR5-5600; DeepCool CC360 ARGB case; Gigabyte GS27QA monitor | ID-Cooling SE-214-XT V2; Apacer Panther RGB 32GB DDR5-5600; Ocypus Gamma C52 BK ARGB; AOC Q27B36X | Exact local variants were not all matched in the catalogue. The actual components and Kazakhstan prices remain in `budget.csv`. |

## How to interpret the results

- A green PCPartPicker compatibility banner means no incompatibility was detected by the checks it ran for the selected catalogue entries. It does not prove physical assembly, BIOS version, exact RAM QVL status, Windows activation or local availability.
- PCPartPicker prices and merchants may be outside Kazakhstan. Do not copy those prices into `budget.csv`.
- For the actual purchase, use the exact Kazakhstan retailer product pages and dated KZT prices in `budget.csv`.
- The actual Designer monitor is AOC Q27B36X (1440p/144 Hz); Gigabyte GS27QA is only the PCPartPicker comparison monitor.
- The actual Sales and Web Developer RAM is GeIL Pristine 32GB DDR4-3200; Kingston FURY Beast is only a comparison selection.
- The actual Designer RAM is Apacer Panther RGB 32GB DDR5-5600; Kingston FURY Beast is only a comparison selection.

## Manufacturer compatibility references

- Gigabyte A520M H ARGB: https://www.gigabyte.com/Motherboard/A520M-H-ARGB-rev-11/support
- Gigabyte B550M GAMING X WIFI6: https://www.gigabyte.com/Motherboard/B550M-GAMING-X-WIFI6-rev-10-11/support
- Gigabyte B760M D3HP DDR4: https://www.gigabyte.com/Motherboard/B760M-D3HP-DDR4/support
- Gigabyte A620M GAMING X AX: https://www.gigabyte.com/Motherboard/A620M-GAMING-X-AX-rev-10/support
- ID-Cooling SE-214-XT V2: https://www.idcooling.com/product/detail?id=560&name=SE-214-XT+V2
- AGI AI828 datasheet: https://agi-gear.com/wp-content/uploads/2026/01/Datasheet_AI828_0128.pdf
- Ocypus Gamma C52 ARGB: https://ocypus.com/specification/case/gamma-c52-argb--0.html
- Palit RTX 5060 Ti White OC 16 GB: https://www.palit.com/palit/vgapro.php?id=5735&lang=en&tab=sp
- Lian Li RB PSU: https://lian-li.com/product/rb-psu/
- Thermaltake TR2 S 550W: https://thermaltake.com/products/tr2-s-550w-dc-to-dc-version

## Saved evidence

- [x] Four PCPartPicker share links recorded.
- [x] Four screenshots saved in pcpartpicker/ and linked in the table above.
- [x] Manufacturer compatibility references recorded.
- [ ] Formal vendor quotations were not obtained. The pre-built comparison uses dated public online catalogue prices, not formal quotations.
