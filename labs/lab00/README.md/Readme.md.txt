# Lab00 — Inventory Your Own Machine

Driver first half: Maksut
Machine: 
Date: 10.10.2026

What I did

1. CPU model, cores, and threads

Command:

....powershell
Get-CimInstance Win32_Processor |
    Select-Object Name, NumberOfCores, NumberOfLogicalProcessors |
    Format-List


Result:


Name                      : Intel(R) Core(TM) 5 210H
NumberOfCores             : 8
NumberOfLogicalProcessors : 12


2. Installed memory

Command:

....powershell
Get-CimInstance Win32_PhysicalMemory |
    Select-Object DeviceLocator,
        @{Name="CapacityGB";Expression={[math]::Round($_.Capacity / 1GB, 2)}},
        Speed, Manufacturer, PartNumber |
    Format-Table -AutoSize


Result: Two 8 GB Samsung memory modules, each reporting a speed of 5600 MHz. Total installed RAM: 16 GB.

3. Physical disk and free space

Commands:

....powershell
Get-PhysicalDisk |
    Select-Object FriendlyName, MediaType, BusType,
        @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}} |
    Format-Table -AutoSize

Get-Volume |
    Where-Object DriveLetter |
    Select-Object DriveLetter, FileSystemLabel,
        @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}},
        @{Name="FreeSpaceGB";Expression={[math]::Round($_.SizeRemaining / 1GB, 2)}} |
    Format-Table -AutoSize


Result: Micron MTFDKCD1T0QGN-1BN1AABLA, an NVMe SSD. The C: volume has approximately 797.33 GB free.

4. Firmware and virtualization

Commands:

....powershell
(Get-ComputerInfo).BiosFirmwareType

Get-CimInstance Win32_BIOS |
    Select-Object Manufacturer, SMBIOSBIOSVersion, ReleaseDate

systeminfo | Select-String "Hyper-V","Virtualization","hypervisor"

Get-CimInstance Win32_Processor |
    Select-Object Name, VMMonitorModeExtensions,
        VirtualizationFirmwareEnabled,
        SecondLevelAddressTranslationExtensions

5. Used AI a bit to format some entries, but mainly did everything myself, asking sometimes from AI to identify errors, or functions of individual commands. 

Result: Firmware type is UEFI. The BIOS manufacturer is Lenovo, version QDCN24WW, released on 5 March 2025. Windows reported that a hypervisor had been detected. The processor CIM properties returned False.



| What | Value | Where I got it |
|---|---|---|
| CPU model | Intel Core 5 210H | `Get-CimInstance Win32_Processor` |
| Cores / threads | 8 / 12 | `Get-CimInstance Win32_Processor` |
| Total RAM | 16 GB | `Get-CimInstance Win32_PhysicalMemory` |
| RAM modules / speed | 2 / 5600 MHz each | `Get-CimInstance Win32_PhysicalMemory` |
| Disk model | Micron MTFDKCD1T0QGN-1BN1AABLA | `Get-PhysicalDisk` |
| Disk type | NVMe SSD | `Get-PhysicalDisk` |
| Free space (VM volume) | Approximately 797.33 GB on C: | `Get-Volume` |
| Firmware type | UEFI | `(Get-ComputerInfo).BiosFirmwareType` |
| Firmware version / date | QDCN24WW / 05.03.2025 | `Get-CimInstance Win32_BIOS` |
| Virtualization | Windows reports a hypervisor detected; processor CIM properties returned False | `systeminfo`; `Get-CimInstance Win32_Processor` |

#What did not work the first time

- I initially used the path `labs/lab00-inventory`, although my repository uses `labs/lab00`. PowerShell reported that the directory did not exist. I corrected the paths to `labs/lab00`.
- I initially split the `Out-File -Encoding utf8` command across lines incorrectly, so PowerShell treated `utf8` as a separate command. I corrected the command syntax and successfully saved the memory evidence.
- I initially tried piping directly from a `switch` statement, which produced a parser error. I changed the approach to assign the result to a variable before saving the evidence.
- My first Git commit failed because Git did not have an author identity configured. I configured my Git name and email. The first push was also rejected because the remote contained commits I had not pulled. After pulling the remote changes, I pushed my lab files to GitHub successfully

## Evidence

- [evidence/cpu.txt](evidence/cpu.txt) — CPU model, core count, and logical processor count.
- [evidence/memory.txt](evidence/memory.txt) — installed RAM modules, capacity, speed, and total memory.
- [evidence/disk.txt](evidence/disk.txt) — physical disk model, type, capacity, and volume free space.
- [evidence/system.txt](evidence/system.txt) — firmware details, BIOS version and date, and virtualization checks.
"@
