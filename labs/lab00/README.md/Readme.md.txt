What i did: 

Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Users\user\Documents\GitHub\osarch-maksut> get-location

Path
----
C:\Users\user\Documents\GitHub\osarch-maksut


PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_Processor |
>>   Select-Object Name, NumberOfCores, NumberOfLogicalProcessors |
>>   Format-List


Name                      : Intel(R) Core(TM) 5 210H
NumberOfCores             : 8
NumberOfLogicalProcessors : 12



PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_Processor |
>>   Select-Object Name, NumberOfCores, NumberOfLogicalProcessors |
>>   Format-List |
>>   Tee-Object -FilePath "labs/lab00/evidence/cpu.txt"


Name                      : Intel(R) Core(TM) 5 210H
NumberOfCores             : 8
NumberOfLogicalProcessors : 12



PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-Content "labs/lab00-inventory/evidence/cpu.txt"
Get-Content : Не удается найти путь "C:\Users\user\Documents\GitHub
\osarch-maksut\labs\lab00-inventory\evidence\cpu.txt", так как он н
е существует.
строка:1 знак:1
+ Get-Content "labs/lab00-inventory/evidence/cpu.txt"
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\user\D...v
   idence\cpu.txt:String) [Get-Content], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Co
   mmands.GetContentCommand

PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-Content "labs/lab00/evidence/cpu.txt"


Name                      : Intel(R) Core(TM) 5 210H
NumberOfCores             : 8
NumberOfLogicalProcessors : 12



PS C:\Users\user\Documents\GitHub\osarch-maksut> $ram = Get-CimInstance Win32_PhysicalMemory
>>
>> $ram |
>>   Select-Object DeviceLocator,
>>     @{Name="CapacityGB";Expression={[math]::Round($_.Capacity / 1GB, 2)}},
>>     Speed, Manufacturer, PartNumber |
>>   Format-Table -AutoSize
>>
>> "Total installed RAM: $([math]::Round(($ram | Measure-Object Capacity -Sum).Sum / 1GB, 2)) GB"
>> "Installed module count: $($ram.Count)"

DeviceLocator              CapacityGB Speed Manufacturer PartNumber
-------------              ---------- ----- ------------ ----------
Controller0-ChannelA                8  5600 Samsung      M425R1G...
Controller1-ChannelA-DIMM0          8  5600 Samsung      M425R1G...


Total installed RAM: 16 GB
Installed module count: 2
PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_PhysicalMemory | Select-Object BankLabel, Manufacturer,
>> Capacity, Speed, ConfiguredClockSpeed | Format-Table | Out-File -Encoding
>> utf8 evidence\memory.txt
Out-File : Отсутствует аргумент для параметра "Encoding". Укажите п
араметр типа "System.String" и повторите попытку.
строка:2 знак:65
+ ... city, Speed, ConfiguredClockSpeed | Format-Table | Out-File -
Encoding
+                                                                 ~
~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Out-File], Par
   ameterBindingException
    + FullyQualifiedErrorId : MissingArgument,Microsoft.PowerShell
   .Commands.OutFileCommand

utf8 : Имя "utf8" не распознано как имя командлета, функции, файла
сценария или выполняемой программы. Проверьте правильность написани
я имени, а также наличие и правильность пути, после чего повторите
попытку.
строка:3 знак:1
+ utf8 evidence\memory.txt
+ ~~~~
    + CategoryInfo          : ObjectNotFound: (utf8:String) [], Co
   mmandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\user\Documents\GitHub\osarch-maksut> -Encoding utf8
-Encoding : Имя "-Encoding" не распознано как имя командлета, функц
ии, файла сценария или выполняемой программы. Проверьте правильност
ь написания имени, а также наличие и правильность пути, после чего
повторите попытку.
строка:1 знак:1
+ -Encoding utf8
+ ~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (-Encoding:String) [
   ], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\user\Documents\GitHub\osarch-maksut> ^C
PS C:\Users\user\Documents\GitHub\osarch-maksut> Encoding uft8
Encoding : Имя "Encoding" не распознано как имя командлета, функции
, файла сценария или выполняемой программы. Проверьте правильность
написания имени, а также наличие и правильность пути, после чего по
вторите попытку.
строка:1 знак:1
+ Encoding uft8
+ ~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Encoding:String) []
   , CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\user\Documents\GitHub\osarch-maksut>
>> $ram = Get-CimInstance Win32_PhysicalMemory
>>
>> "=== RAM MODULES ===" |
>>   Set-Content "labs/lab00-inventory/evidence/memory.txt"
>>
>> $ram |
>>   Select-Object DeviceLocator,
>>     @{Name="CapacityGB";Expression={[math]::Round($_.Capacity / 1GB, 2)}},
>>     Speed, Manufacturer, PartNumber |
>>   Format-Table -AutoSize |
>>   Out-String -Width 200 |
>>   Tee-Object -FilePath "labs/lab00-inventory/evidence/memory.txt" -Append
>>
>> "=== SUMMARY ===" |
>>   Tee-Object -FilePath "labs/lab00-inventory/evidence/memory.txt" -Append
>>
>> "Total installed RAM: $([math]::Round(($ram | Measure-Object Capacity -Sum).Sum / 1GB, 2)) GB" |
>>   Tee-Object -FilePath "labs/lab00-inventory/evidence/memory.txt" -Append
>>
>> "Installed module count: $($ram.Count)" |
>>   Tee-Object -FilePath "labs/lab00-inventory/evidence/memory.txt" -Append
>>
Set-Content : Не удалось найти часть пути "C:\Users\user\Documents\
GitHub\osarch-maksut\labs\lab00-inventory\evidence\memory.txt".
строка:5 знак:3
+   Set-Content "labs/lab00-inventory/evidence/memory.txt"
+   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\user\D...e
   nce\memory.txt:String) [Set-Content], DirectoryNotFoundExcepti
  on
    + FullyQualifiedErrorId : GetContentWriterDirectoryNotFoundErr
   or,Microsoft.PowerShell.Commands.SetContentCommand

out-file : Не удалось найти часть пути "C:\Users\user\Documents\Git
Hub\osarch-maksut\labs\lab00-inventory\evidence\memory.txt".
строка:7 знак:1
+ $ram |
+ ~~~~~~
    + CategoryInfo          : OpenError: (:) [out-file], Directory
   NotFoundException
    + FullyQualifiedErrorId : FileOpenFailure,Microsoft.PowerShell
   .Commands.OutFileCommand

out-file : Не удалось найти часть пути "C:\Users\user\Documents\Git
Hub\osarch-maksut\labs\lab00-inventory\evidence\memory.txt".
строка:15 знак:1
+ "=== SUMMARY ===" |
+ ~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : OpenError: (:) [out-file], Directory
   NotFoundException
    + FullyQualifiedErrorId : FileOpenFailure,Microsoft.PowerShell
   .Commands.OutFileCommand

out-file : Не удалось найти часть пути "C:\Users\user\Documents\Git
Hub\osarch-maksut\labs\lab00-inventory\evidence\memory.txt".
строка:18 знак:25
+ ... lled RAM: $([math]::Round(($ram | Measure-Object Capacity -Su
m).Sum / ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
~~~~~~~~
    + CategoryInfo          : OpenError: (:) [out-file], Directory
   NotFoundException
    + FullyQualifiedErrorId : FileOpenFailure,Microsoft.PowerShell
   .Commands.OutFileCommand

out-file : Не удалось найти часть пути "C:\Users\user\Documents\Git
Hub\osarch-maksut\labs\lab00-inventory\evidence\memory.txt".
строка:21 знак:28
+ "Installed module count: $($ram.Count)" |
+                            ~~~~~~~~~~
    + CategoryInfo          : OpenError: (:) [out-file], Directory
   NotFoundException
    + FullyQualifiedErrorId : FileOpenFailure,Microsoft.PowerShell
   .Commands.OutFileCommand

PS C:\Users\user\Documents\GitHub\osarch-maksut> $ram = Get-CimInstance Win32_PhysicalMemory
>>
>> "=== RAM MODULES ===" |
>>   Set-Content "labs/lab00/evidence/memory.txt"
>>
>> $ram |
>>   Select-Object DeviceLocator,
>>     @{Name="CapacityGB";Expression={[math]::Round($_.Capacity / 1GB, 2)}},
>>     Speed, Manufacturer, PartNumber |
>>   Format-Table -AutoSize |
>>   Out-String -Width 200 |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append
>>
>> "=== SUMMARY ===" |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append
>>
>> "Total installed RAM: $([math]::Round(($ram | Measure-Object Capacity -Sum).Sum / 1GB, 2)) GB" |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append
>>
>> "Installed module count: $($ram.Count)" |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append

DeviceLocator              CapacityGB Speed Manufacturer PartNumber 
-------------              ---------- ----- ------------ ---------- 
Controller0-ChannelA                8  5600 Samsung      M425R1GB4PB0-CWMT3
Controller1-ChannelA-DIMM0          8  5600 Samsung      M425R1GB4PB0-CWMOL



=== SUMMARY ===
Total installed RAM: 16 GB
Installed module count: 2
PS C:\Users\user\Documents\GitHub\osarch-maksut> $ram = Get-CimInstance Win32_PhysicalMemory
>>
>> "=== RAM MODULES ===" |
>>   Set-Content "labs/lab00/evidence/memory.txt"
>>
>> $ram |
>>   Select-Object DeviceLocator,
>>     @{Name="CapacityGB";Expression={[math]::Round($_.Capacity / 1GB, 2)}},
>>     Speed, Manufacturer, PartNumber |
>>   Format-Table -AutoSize |
>>   Out-String -Width 200 |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append
>>
>> "=== SUMMARY ===" |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append
>>
>> "Total installed RAM: $([math]::Round(($ram | Measure-Object Capacity -Sum).Sum / 1GB, 2)) GB" |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append
>>
>> "Installed module count: $($ram.Count)" |
>>   Tee-Object -FilePath "labs/lab00/evidence/memory.txt" -Append

DeviceLocator              CapacityGB Speed Manufacturer PartNumber 
-------------              ---------- ----- ------------ ---------- 
Controller0-ChannelA                8  5600 Samsung      M425R1GB4PB0-CWMT3
Controller1-ChannelA-DIMM0          8  5600 Samsung      M425R1GB4PB0-CWMOL



=== SUMMARY ===
Total installed RAM: 16 GB
Installed module count: 2
PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-PhysicalDisk |
>>   Select-Object FriendlyName, MediaType, BusType,
>>     @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}} |
>>   Format-Table -AutoSize |
>>   Out-String -Width 200 |
>>   Set-Content "labs/lab00/evidence/disks.txt"
PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_Processor |
>>   Select-Object Name, NumberOfCores, NumberOfLogicalProcessors,
>>     @{Name="MaxClockSpeedMHz";Expression={$_.MaxClockSpeed}} |
>>   Format-List |
>>   Out-String |
>>   Set-Content "labs/lab00/evidence/cpu.txt"
PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_OperatingSystem |
>>   Select-Object Caption, Version, BuildNumber, OSArchitecture,
>>     @{Name="InstalledRAM_GB";Expression={[math]::Round($_.TotalVisibleMemorySize / 1MB, 2)}} |
>>   Format-List |
>>   Out-String |
>>   Set-Content "labs/lab00/evidence/system.txt"
PS C:\Users\user\Documents\GitHub\osarch-maksut>
>> Get-PhysicalDisk |
>>   Select-Object FriendlyName, MediaType, BusType,
>>     @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}} |
>>   Format-Table -AutoSize
>>

FriendlyName                   MediaType BusType SizeGB
------------                   --------- ------- ------
Micron MTFDKCD1T0QGN-1BN1AABLA SSD       NVMe    953,87


PS C:\Users\user\Documents\GitHub\osarch-maksut>
>> Get-Volume |
>>   Where-Object DriveLetter |
>>   Select-Object DriveLetter, FileSystemLabel,
>>     @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}},
>>     @{Name="FreeSpaceGB";Expression={[math]::Round($_.SizeRemaining / 1GB, 2)}} |
>>   Format-Table -AutoSize
>>

DriveLetter FileSystemLabel SizeGB FreeSpaceGB
----------- --------------- ------ -----------
          C Windows 11      953,75      797,29


PS C:\Users\user\Documents\GitHub\osarch-maksut> "=== PHYSICAL DISKS ===" |
>>   Set-Content "labs/lab00/evidence/disk.txt"
>>
>> Get-PhysicalDisk |
>>   Select-Object FriendlyName, MediaType, BusType,
>>     @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}} |
>>   Format-Table -AutoSize |
>>   Out-String -Width 200 |
>>   Tee-Object -FilePath "labs/lab00/evidence/disk.txt" -Append
>>
>> "=== VOLUME SPACE ===" |
>>   Tee-Object -FilePath "labs/lab00/evidence/disk.txt" -Append
>>
>> Get-Volume |
>>   Where-Object DriveLetter |
>>   Select-Object DriveLetter, FileSystemLabel,
>>     @{Name="SizeGB";Expression={[math]::Round($_.Size / 1GB, 2)}},
>>     @{Name="FreeSpaceGB";Expression={[math]::Round($_.SizeRemaining / 1GB, 2)}} |
>>   Format-Table -AutoSize |
>>   Out-String -Width 200 |
>>   Tee-Object -FilePath "labs/lab00/evidence/disk.txt" -Append

FriendlyName                   MediaType BusType SizeGB
------------                   --------- ------- ------
Micron MTFDKCD1T0QGN-1BN1AABLA SSD       NVMe    953,87



=== VOLUME SPACE ===

DriveLetter FileSystemLabel SizeGB FreeSpaceGB
----------- --------------- ------ -----------
          C Windows 11      953,75       797,3



PS C:\Users\user\Documents\GitHub\osarch-maksut>
>> "=== FIRMWARE TYPE ==="
>>
>> $fw = (Get-ItemProperty `
>>   "HKLM:\SYSTEM\CurrentControlSet\Control").PEFirmwareType
>>
>> switch ($fw) {
>>   1 { "Firmware type: BIOS (Legacy)" }
>>   2 { "Firmware type: UEFI" }
>>   default { "Firmware type: Unknown or unavailable" }
>> }
>>
>> "=== BIOS VERSION AND DATE ==="
>>
>> Get-CimInstance Win32_BIOS |
>>   Select-Object Manufacturer, SMBIOSBIOSVersion, ReleaseDate |
>>   Format-List
>>
=== FIRMWARE TYPE ===
Firmware type: Unknown or unavailable
=== BIOS VERSION AND DATE ===


Manufacturer      : LENOVO
SMBIOSBIOSVersion : QDCN24WW
ReleaseDate       : 05.03.2025 5:00:00



PS C:\Users\user\Documents\GitHub\osarch-maksut> <CodeBlock language="powershell">
>> Get-CimInstance Win32_Processor |
>>   Select-Object Name,
>>     VMMonitorModeExtensions,
>>     VirtualizationFirmwareEnabled,
>>     SecondLevelAddressTranslationExtensions |
>>   Format-List
>> </CodeBlock>
< : Имя "<" не распознано как имя командлета, функции, файла сценар
ия или выполняемой программы. Проверьте правильность написания имен
и, а также наличие и правильность пути, после чего повторите попытк
у.
строка:1 знак:1
+ <CodeBlock language="powershell">
+ ~
    + CategoryInfo          : ObjectNotFound: (<:String) [], Comma
   ndNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException



Name                                    : Intel(R) Core(TM) 5 210H
VMMonitorModeExtensions                 : False
VirtualizationFirmwareEnabled           : False
SecondLevelAddressTranslationExtensions : False



< : Имя "<" не распознано как имя командлета, функции, файла сценар
ия или выполняемой программы. Проверьте правильность написания имен
и, а также наличие и правильность пути, после чего повторите попытк
у.
строка:8 знак:1
+ </CodeBlock>
+ ~
    + CategoryInfo          : ObjectNotFound: (<:String) [], Comma
   ndNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_Processor |
>>   Select-Object Name,
>>     VMMonitorModeExtensions,
>>     VirtualizationFirmwareEnabled,
>>     SecondLevelAddressTranslationExtensions |
>>   Format-List


Name                                    : Intel(R) Core(TM) 5 210H
VMMonitorModeExtensions                 : False
VirtualizationFirmwareEnabled           : False
SecondLevelAddressTranslationExtensions : False



PS C:\Users\user\Documents\GitHub\osarch-maksut> $path = "labs/lab00-inventory/evidence/system.txt"
>> "=== FIRMWARE TYPE ===" | Set-Content $path
>> $fw = (Get-ItemProperty `
>>   "HKLM:\SYSTEM\CurrentControlSet\Control").PEFirmwareType
>> switch ($fw)
>>
строка:5 знак:13
+ switch ($fw)
+             ~
В операторе switch отсутствует ''{''.
    + CategoryInfo          : ParserError: (:) [], ParentContainsE
   rrorRecordException
    + FullyQualifiedErrorId : MissingCurlyBraceInSwitchStatement

PS C:\Users\user\Documents\GitHub\osarch-maksut>
>> $evidence = "labs/lab00/evidence"
>> New-Item -ItemType Directory -Force -Path $evidence | Out-Null
>>
>> $path = "$evidence/system.txt"
>>
>> "=== FIRMWARE TYPE ===" | Set-Content $path
>>
>> $fw = (Get-ItemProperty `
>>   "HKLM:\SYSTEM\CurrentControlSet\Control").PEFirmwareType
>>
>> switch ($fw) {
>>   1 { "Firmware type: BIOS (Legacy)" }
>>   2 { "Firmware type: UEFI" }
>>   default { "Firmware type: Unknown or unavailable" }
>> } | Tee-Object -FilePath $path -Append
>>
>> "`n=== BIOS INFORMATION ===" |
>>   Tee-Object -FilePath $path -Append
>>
>> Get-CimInstance Win32_BIOS |
>>   Select-Object Manufacturer, SMBIOSBIOSVersion, ReleaseDate |
>>   Format-List |
>>   Out-String |
>>   Tee-Object -FilePath $path -Append
>>
>> "`n=== VIRTUALIZATION ===" |
>>   Tee-Object -FilePath $path -Append
>>
>> Get-CimInstance Win32_Processor |
>>   Select-Object Name, VMMonitorModeExtensions,
>>     VirtualizationFirmwareEnabled,
>>     SecondLevelAddressTranslationExtensions |
>>   Format-List |
>>   Out-String |
>>   Tee-Object -FilePath $path -Append
>>
>> Write-Host "`nSaved firmware and virtualization evidence to $path"
>>
строка:16 знак:3
+ } | Tee-Object -FilePath $path -Append
+   ~
Пустой элемент канала не допускается.
    + CategoryInfo          : ParserError: (:) [], ParentContainsE
   rrorRecordException
    + FullyQualifiedErrorId : EmptyPipeElement

PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-PhysicalDisk | Select-Object FriendlyName, MediaType, BusType, Size |
>> Format-List | Out-File
Out-File : Не удается обработать аргумент, так как значением аргуме
нта "path" является NULL. Укажите для аргумента "path" значение, от
личное от NULL.
строка:2 знак:15
+ Format-List | Out-File
+               ~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Out-File], PSA
   rgumentNullException
    + FullyQualifiedErrorId : ArgumentNull,Microsoft.PowerShell.Co
   mmands.OutFileCommand

PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-PhysicalDisk | Select-Object FriendlyName, MediaType, BusType, Size

FriendlyName                   MediaType BusType          Size
------------                   --------- -------          ----
Micron MTFDKCD1T0QGN-1BN1AABLA SSD       NVMe    1024209543168


PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-Volume | Select-Object DriveLetter, FileSystemLabel, Size, SizeRemaining
>> | Format-Table
строка:2 знак:1
+ | Format-Table
+ ~
Пустой элемент канала не допускается.
    + CategoryInfo          : ParserError: (:) [], ParentContainsE
   rrorRecordException
    + FullyQualifiedErrorId : EmptyPipeElement

PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-Volume | Select-Object DriveLetter, FileSystemLabel, Size, SizeRemaining                                                                               DriveLetter FileSystemLabel          Size SizeRemaining             ----------- ---------------          ---- -------------
                                100663296      56210432
C           Windows 11      1024086503424  856109903872


PS C:\Users\user\Documents\GitHub\osarch-maksut> [math]::Round((Get-Volume -DriveLetter C).SizeRemaining / 1GB, 1)
>>
797,3
PS C:\Users\user\Documents\GitHub\osarch-maksut> Get-CimInstance Win32_BIOS | Select-Object Manufacturer, SMBIOSBIOSVersion,
>> ReleaseDate

Manufacturer SMBIOSBIOSVersion ReleaseDate
------------ ----------------- -----------
LENOVO       QDCN24WW          05.03.2025 5:00:00


PS C:\Users\user\Documents\GitHub\osarch-maksut> (Get-ComputerInfo).BiosFirmwareType
>>
Uefi
PS C:\Users\user\Documents\GitHub\osarch-maksut> Confirm-SecureBootUEFI
>>
False
PS C:\Users\user\Documents\GitHub\osarch-maksut> systeminfo | Select-String "Hyper-V","Virtualization","hypervisor"
>>

Требования Hyper-V:                      Обнаружена низкоуровневая
оболочка. Функции, необходимые для Hyper-V, отображены не будут.


PS C:\Users\user\Documents\GitHub\osarch-maksut>

