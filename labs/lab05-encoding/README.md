# Lab 05 — Encoding Forensics

## 1. Objective

The objective of this laboratory was to investigate a text file containing incorrectly displayed characters, identify its original character encoding and line-ending format, convert it to UTF-8, and verify the corrected file in different applications.

## 2. Original File Diagnosis

The original file was `staff-broken.csv`.

The file was examined before making any modifications.

### Encoding identification

Several candidate encodings were tested:

- CP1251
- CP866
- KOI8-R
- RK1048
- PT154

CP866 and KOI8-R produced incorrectly decoded text. CP1251, RK1048, and PT154 produced similar Russian text, so the Kazakh-specific characters were used to distinguish between them.

The RK1048 candidate displayed both Russian and Kazakh characters correctly when compared in Windows Notepad.

**Identified original encoding: RK1048.**

### Line endings

The original file was examined using:

```bash
file staff-broken.csv
```

The result identified CRLF line terminators.

A byte-level check confirmed:

- CR characters: 26
- LF characters: 26
- Line-ending format: CRLF (`\r\n`)

### BOM detection

The original file did not contain a UTF-8 BOM.

### Original checksum

The SHA-256 checksum was recorded before conversion:

```text
919027f1f8c71d85cba3f12ad0f6c927d4e0450cfb2a2d63378a69f14cab270
```

The original file was preserved unchanged.

## 3. Hexadecimal Analysis

The first 16 bytes of the original file:

```text
00000000: d2e0 e12e b93b d4c8 ce3b c4ee ebe6 edee
```

Byte interpretation using RK1048:

| Bytes | Character | Meaning |
|---|---|---|
| `D2 E0 E1` | Таб | First column header |
| `2E` | `.` | Full stop |
| `B9` | № | Number symbol |
| `3B` | `;` | Field separator |
| `D4 C8 CE` | ФИО | Name field |
| `3B` | `;` | Field separator |
| `C4 EE EB E6 ED EE` | Должность | Position field |

This byte-level analysis supported the encoding investigation.

## 4. Conversion and Fix

The file was converted from RK1048 to UTF-8 using `iconv`.

The conversion script is located at:

`scripts/fix.sh`

The script:

1. Reads the original `staff-broken.csv`.
2. Converts its contents from RK1048 to UTF-8.
3. Adds a UTF-8 BOM (`EF BB BF`) for application compatibility.
4. Writes the result to `evidence/staff-fixed.csv`.

The original CRLF line endings were preserved.

The fixed file was validated using:

```bash
iconv -f UTF-8 -t UTF-8 evidence/staff-fixed.csv > /dev/null
```

The validation completed successfully.

The first three bytes of the corrected file were:

```text
EF BB BF
```

These bytes represent the UTF-8 BOM.

## 5. Application Verification

The corrected CSV was tested in Microsoft Excel, LibreOffice Calc, and the Ubuntu terminal.

### Microsoft Excel

The corrected file was opened in Excel.

Verification:
- Kazakh characters displayed correctly.
- Russian characters displayed correctly.
- All six columns were separated correctly.
- Dates were readable.

**Result: Successful.**

### LibreOffice Calc

The corrected file was opened in LibreOffice Calc. The import dialog detected Unicode (UTF-8), and the default import settings were used.

Verification:
- Kazakh characters displayed correctly.
- Russian characters displayed correctly.
- All six columns were separated correctly.
- Dates were readable.

**Result: Successful.**

### Ubuntu Terminal

The corrected file was inspected using:

```bash
cat evidence/staff-fixed.csv
```

UTF-8 validation passed. However, some Kazakh characters were not rendered correctly in the terminal because of font limitations.

This was a display issue rather than an encoding-conversion failure. The corrected file displayed properly in Excel and LibreOffice Calc.

**Result: UTF-8 validation successful; terminal font rendering partially unsuccessful.**

## 6. Conclusion

The original file used RK1048 encoding and CRLF line endings, with no UTF-8 BOM.

The file was successfully converted to UTF-8 with a BOM while preserving its original line endings. The original file remained unchanged, and its checksum was recorded.

The corrected file was verified successfully in Microsoft Excel and LibreOffice Calc. Ubuntu also passed UTF-8 validation, although some Kazakh characters were limited by terminal font support.

The investigation demonstrates the importance of identifying encoding, line endings, and BOM information before modifying a text file.

## 7. Evidence

The `evidence/` directory contains:

- `staff-broken.csv` — original file
- `staff-fixed.csv` — corrected UTF-8 file
- `checksum-before.txt` — original SHA-256 checksum
- `file-before.txt` — original file identification
- `file-after.txt` — corrected file identification
- `hexdump-before.txt` — original hexadecimal analysis
- `opens-correctly.png` — application verification screenshot
- `staff-CP1251.txt` — CP1251 candidate
- `staff-RK1048.txt` — RK1048 candidate
- `staff-PT154.txt` — PT154 candidate

## 8. Software Versions

Record the exact versions used during verification:

## 8. Software Versions

- **Microsoft Excel LTSC:** Version 2610, Build 16.0.20527.20150 (64-bit)
- **LibreOffice Calc:** Version 26.8.3.1 (X86_64)
- **Operating System:** Ubuntu 26.04.1 LTS