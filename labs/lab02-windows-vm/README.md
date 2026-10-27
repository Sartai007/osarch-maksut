# Lab 2 — Windows VM, Networking, and Memory Overcommit

## 1. Objective

Install a Windows 11 virtual machine, configure networking between Windows and Ubuntu, verify connectivity, and observe host memory pressure when running both virtual machines.

## 2. Environment

- Host OS: Windows
- Host physical RAM: 16 GB
- Hypervisor: VMware Workstation Pro
- Windows guest: Windows 11 Enterprise Evaluation
- Ubuntu guest: Ubuntu Server
- Network mode: NAT for both virtual machines

### VM memory allocations

| Machine | Allocated memory |
|---|---:|
| Ubuntu (`lab01-ubuntu`) | 8 GB |
| Windows 11 (`lab02-win11`) | 10 GB |
| Combined allocation | 18 GB |
| Host physical memory | 16 GB |

The combined virtual-machine allocation exceeds the host's physical RAM. This is memory overcommit.

## 3. Network configuration

Both virtual machines use VMware NAT networking. NAT was selected because it provides internet connectivity while allowing the two guests to communicate through the same virtual network.

### Network diagram

```text
                 Internet
                    |
             VMware NAT (VMnet8)
                    |
          Virtual network / switch
              /             \
             /               \
    Ubuntu Server         Windows 11
    192.168.208.129       192.168.208.130
```

### IP address evidence

- Ubuntu IPv4 address: `192.168.208.129`
- Windows IPv4 address: `192.168.208.130`
- Both addresses are on the same subnet.

See:
- `evidence/ip-addr-linux.txt`
- `evidence/ipconfig-windows.txt`

## 4. Connectivity tests

The following tests were performed:

| Test | Result |
|---|---|
| Windows → Ubuntu ping | Passed; 0% packet loss |
| Ubuntu → Windows ping, before firewall change | Failed; 100% packet loss |
| Ubuntu → Windows ping, after firewall change | Passed; 0% packet loss |
| Windows → Internet (`8.8.8.8`) | Passed; 0% packet loss |
| Ubuntu → Internet (`8.8.8.8`) | Passed; 0% packet loss |

### Windows Firewall configuration

Initially, Ubuntu could not ping Windows because inbound ICMP echo requests were blocked by Windows Defender Firewall.

The following rule was added in an elevated PowerShell session to allow ICMPv4 echo requests from the local subnet:

```powershell
New-NetFirewallRule -DisplayName "Lab02 - allow ping (ICMPv4 echo)" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -RemoteAddress LocalSubnet -Action Allow
```

After adding the rule, Ubuntu could ping Windows successfully. The rule is restricted to the local subnet and ICMPv4 echo requests.

Detailed results are recorded in `evidence/ping-both-ways.txt`.

## 5. Host memory observations

The host has 16 GB of physical RAM. Both VMs were initially configured with 4 GB each and were later configured with 8 GB for Ubuntu and 10 GB for Windows.

### Before running both VMs

With both VMs powered off, Task Manager showed approximately:

- In use: 9.3 GB
- Available: 6.3 GB
- Committed: 18.7 GB
- Cached: 3.3 GB

See `evidence/host-memory-before.png`.

### After starting both VMs

With both VMs running and Microsoft Edge tabs open inside the Windows guest, the host's available memory fell to approximately 200 MB.

See `evidence/host-memory-after.png`.

This demonstrated substantial host memory pressure while the combined VM memory allocation was 18 GB on a 16 GB host.

**Limitation:** The Ubuntu `stress-ng` memory stress test was not run. The observed memory pressure resulted from running both VMs and opening Edge tabs in the Windows guest. The screenshots document the observed state; they do not establish the results of a `stress-ng` test.

## 6. Evidence files

- `evidence/ip-addr-linux.txt` — Ubuntu network configuration
- `evidence/ipconfig-windows.txt` — Windows network configuration
- `evidence/ping-both-ways.txt` — Connectivity and internet ping results
- `evidence/host-memory-before.png` — Host memory before the experiment
- `evidence/host-memory-after.png` — Host memory while both VMs were running

## 7. Conclusion

Both virtual machines were installed and configured to use NAT networking. Bidirectional guest connectivity and internet connectivity were verified. An inbound Windows Firewall rule was required to permit Ubuntu-to-Windows ICMP echo requests.

The memory observations showed that running both VMs with 18 GB of combined configured RAM on a 16 GB host reduced available host memory to approximately 200 MB. The experiment was not pushed further with `stress-ng` because of the risk of making the host unresponsive.
