\# Lab 1 — First Virtual Machine



Nurmukhammad Maksut 

Machine: Windows host, VMware Workstation Pro, Ubuntu Server guest  

Date: 17-18.10.2026



\# What I did



1\. Downloaded ubuntu. Created a VMware virtual machine named 'lab01-ubuntu'.

2\. Installed Ubuntu Server 26.04.1 LTS from the ISO.

3\. Configured networking and OpenSSH Server.

4\. Checked the operating system, hostname, memory, disk space and SSH service.

5\. Created a VMware snapshot named 'clean-install'.

6\. Deleted '/etc/hostname' to demonstrate a broken hostname configuration.

7\. Used 'cat /etc/hostname' and 'hostnamectl' to verify the broken state.

8\. Restored the 'clean-install' snapshot and verified that the hostname returned to 'lab01'.



\# Result



Ubuntu Server is working and boots successfully. After restoring the snapshot, '/etc/hostname' contains 'lab01'. SSH is active and running. The root filesystem is approximately 19 GB, with approximately 11 GB available.



\# Resource justification



The host has an Intel Core 5 210H processor with 8 cores and 12 logical processors, 16 GB RAM, and approximately 770 GB free on drive C:. I allocated 2 vCPUs, 4 GB of memory and a 40 GB virtual disk to the VM. These settings were chosen to allow Ubuntu Server to run while leaving resources for Windows and future lab work. The host had limited free RAM at the time of measurement, so the allocation should remain modest. At the same time I'm thinking about decreasing its 4 GB memory to 3 or even lower. Because, windows is taking 11.5 out of 16 total, and ubuntu is taking 4, so the laptop has almost no free space, and I don't like it.



\# What did not work the first time



The file '/etc/hostname' was deliberately removed as part of the failure experiment. After rebooting, 'cat /etc/hostname' returned 'No such file or directory', and 'hostnamectl' showed that the static hostname was unset. I captured the broken state, restored the snapshot, and confirmed that the hostname returned to lab01. Also, I created the clean-install snapshot before turning it off. But it worked. Additionally, first time i tried to connect the ip,output was 'error', i fixed it. 



\# Evidence



\- \[evidence/vm-settings.png](evidence/vm-settings.png) — virtual machine settings.

\- \[evidence/guest-release.txt](evidence/guest-release.txt) — Ubuntu release information collected through SSH.

\- \[evidence/broken.png](evidence/broken.png) — broken hostname state.

\- \[evidence/snapshot-list.png](evidence/snapshot-list.png) — VMware snapshot list.

\- \[evidence/restored.png](evidence/restored.png) — Ubuntu after restoration.

\- \[evidence/ssh\_status.png](evidence/ssh\_status.png) — SSH service status.

\- \[evidence/system\_info.png](evidence/system\_info.png) — system information.

\- \[evidence/memory.png](evidence/memory.png) — memory information.



