1a. The computer in front of you



|Figure|This computer|Command it came from|
|-|-|-|
|OS and version|Майкрософт Windows 11 Pro 10.0.26200|systeminfo|
|CPU model|Intel(R) Core(TM) 5 210H|Get-CimInstance Win32\_Processor|
|Cores / logical processors|NumberOfCores                           : 8<br />NumberOfEnabledCore                     : 8<br />NumberOfLogicalProcessors               : 12<br /><br />(ThreadCount                             : 12)<br /><br />ProcessorType                           : 3<br />Revision                                :<br />SocketDesignation                       : U3E1<br />Version                                 :<br />VoltageCaps                             :<br />Caption                                 : Intel64 Family 6 Model 186 Stepping 2<br />Description                             : Intel64 Family 6 Model 186 Stepping 2<br />InstallDate                             :<br />Name                                    : Intel(R) Core(TM) 5 210H|Get-CimInstance Win32\_Processor \| Format-List \*|
|Hardware virtualization:  supported? enabled in firmware?|Требования Hyper-V:                      Обнаружена низкоуровневая оболочка. Функции, необходимые для Hyper-V, отображены не будут.	systeminfo<br />Memory : total / available now	Полный объем физической памяти:          16 045 МБ<br />Доступная физическая память:             3 737 МБ<br />Виртуальная память: максимальный размер: 29 869 МБ<br />Виртуальная память: доступна:            10 637 МБ<br />Виртуальная память: используется:        19 232 МБ|systeminfo|
|System disk:  size, free space, SSD or HDD|Micron MTFDKCD1T0QGN-1BN1AABLA 00A0\_7501\_4DCA\_1507. SSD<br /><br /><br />DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining     Size<br />----------- ------------ -------------- --------- ------------ ----------------- -------------     ----<br />                         FAT32          Fixed     Healthy      OK                     53.59 MB    96 MB<br />C           Windows 11   NTFS           Fixed     Healthy      OK                     713.8 GB ...75 GB|Get-Volume<br />Get-PhysicalDisk \| Format-List \*|
|Partition style of the system disk|UEFI|$env:firmware\_type|





&#x09;







1b. A machine you have never seen: a thin-and-light laptop





|Part|Specification|remaining|
|-|-|-|
|CPU|	2 cores / 12 threads, 1.1 GHz; AMD-V supported and enabled|cpu 8, |
|Memory|16 gb total, 2+6 used for ubuntu and win11vm|ram 8 gb|
|Storage|775.64 gb total, used for vms: 25+64 gb|686.6 free|
|OS|Windows 11 pro||



&#x20;

&#x09;

1. RAM gets loaded if i run both of them. my sysrem requires 9 gb for working, and if for example i open youtube, chrome tabt, it gets upto 10-11. and vms take 8, so it is either full 16, or exceeding that. I reckon CPU will not have issues. after 2+2 treads spent on vms, 8 threads are remaining 
2. I would lower allocated cpu, for win11vm, i would make it 4 gb, to prevent overheating.

&#x09;	

