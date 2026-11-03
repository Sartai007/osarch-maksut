# Ticket 1 — New Developer Test Machine

## 1. What Was Asked

> Hi, we have someone starting on Monday and he needs a test computer set up. Nothing special, just so he can try things without breaking anything. Can you write down how to do it so I can do the next one myself? Thanks

**Requester:** Aigerim T. (Office Manager)

## 2. What Was Actually Needed

The request describes a need for a safe testing environment but does not specify the operating system, hardware resources, virtualization software, networking requirements, or recovery method.

I interpreted the request as requiring two virtual machines:

- Ubuntu Server Linux
- Windows 11

I chose two operating systems to provide separate Linux and Windows testing environments. Virtual machines allow a developer to experiment without directly modifying the host operating system.

The following assumptions were made:

- VMware Workstation Pro would be used as the hypervisor.
- Both operating systems would be useful to the developer.
- Both guests should have internet access.
- Both guests should be able to communicate with each other.
- NAT networking would be sufficient.
- Snapshots would provide recovery points if an experiment damaged a guest.

The requester should ideally clarify:

- Does the developer need Linux, Windows, or both?
- Which development tools and applications will be used?
- Is administrator access required?
- Do the virtual machines need access to internal company resources?
- Is there a specific storage or performance requirement?

I reused two existing virtual machines instead of installing new operating systems. This allowed me to verify the working environment, but it meant I could not capture screenshots of the original creation wizard.

## 3. What I Did

### Step 1 — Inspected the host computer

I recorded the host's hardware specifications and available storage before evaluating the virtual machine allocations.

| Component | Specification |
|---|---|
| CPU | Intel Core 5 210H |
| Physical cores | 8 |
| Logical processors | 12 |
| Installed RAM | 16 GB |
| C: drive capacity | Approximately 953.75 GiB |
| C: drive free space | Approximately 725.25 GiB |

The available storage was checked using PowerShell:

```powershell
Get-PSDrive C
```

### Step 2 — Reviewed the virtual machine configurations

I reused the existing Ubuntu and Windows virtual machines and recorded their resource allocations.

| Resource | Ubuntu Server | Windows 11 |
|---|---:|---:|
| RAM | 4 GB | 6 GB |
| CPU cores | 2 | 2 |
| Virtual disk capacity | 40 GB | 64 GB |
| Network | NAT | NAT |

The two VMs allocate 10 GB of the host's 16 GB RAM, leaving approximately 6 GB for the host when both are running.

I allocated two CPU cores to each guest to provide processing capacity while retaining resources for the host.

The combined virtual disk capacity is 104 GB. This is the maximum capacity assigned to the virtual disks, not necessarily the amount of physical storage currently occupied. The host had approximately 725.25 GiB of free space, which is sufficient for the assigned virtual disk capacities.

### Step 3 — Verified the Ubuntu guest

I accessed the Ubuntu Server virtual machine and ran:

```bash
uname -a
ip -br addr
```

The first command displayed the Linux kernel and system architecture. The second displayed the network interfaces and their IP addresses.

The Ubuntu IP address was:

`192.168.208.129`

The system information was saved in `evidence/04-guest-uname.txt`.

### Step 4 — Verified the Windows guest

I accessed the Windows 11 virtual machine and used Command Prompt:

```cmd
systeminfo
ipconfig
```

These commands displayed the operating system information and network configuration.

The Windows IP address was:

`192.168.208.130`

### Step 5 — Tested network connectivity

Both virtual machines use NAT networking. NAT allows guests to access the internet through the host's network connection without requiring them to appear as separate devices on the physical network.

Both guests were on the `192.168.208.0/24` subnet.

I tested communication between the guests:

From Ubuntu:

```bash
ping -c 4 192.168.208.130
```

From Windows:

```cmd
ping 192.168.208.129
```

Both tests returned four successful replies with no packet loss.

I then tested internet connectivity.

From Ubuntu:

```bash
ping -c 4 8.8.8.8
```

From Windows:

```cmd
ping 8.8.8.8
ping google.com
```

Ubuntu received all four replies. Windows initially experienced packet loss, but the repeated test succeeded. The domain-name test also succeeded, confirming DNS resolution.

### Step 6 — Checked the recovery snapshots

Both virtual machines already had baseline snapshots. I confirmed their existence and captured separate screenshots of their snapshot lists.

Snapshots provide recovery points that allow a VM to return to a previously saved state.

I did not create new snapshots during this ticket because suitable snapshots already existed.

### Step 7 — Recorded a connectivity problem and its resolution

During the first Windows-to-internet connectivity test, `ping 8.8.8.8` returned three replies out of four, resulting in 25% packet loss.

I repeated the test without changing the network configuration, and all four packets were received successfully. I also tested `ping google.com`, which successfully resolved the domain name and received all four replies.

The initial packet loss was temporary and could not be reproduced during the retests. I recorded both the initial unsuccessful attempt and the successful results rather than reporting only the final test.

## 4. Evidence

| Evidence file | Description |
|---|---|
| `evidence/04-guest-uname.txt` | Ubuntu kernel and system information from `uname -a`. |
| `evidence/05-ping-between-guests.txt` | Summary of IP addresses and connectivity test results. |
| `evidence/05-ping-ubuntu.png` | Ubuntu terminal screenshot showing connectivity tests. |
| `evidence/05-ping-windows.txt` | Windows ping results, including the initial packet loss and successful retests. |
| `evidence/06-snapshot-ubuntu.png` | Ubuntu snapshot list. |
| `evidence/06-snapshot-windows.png` | Windows snapshot list. |
| `evidence/07-host-disk-space.txt` | Host C: drive capacity and available free space. |

The original VM creation wizard screenshots are unavailable because the virtual machines were created before this ticket and were reused. I have not presented screenshots of existing settings as screenshots of the original creation process.

## 5. What I Would Do Differently

If I repeated this task, I would clarify the developer's intended workload before allocating resources. For example, software development involving large IDEs, databases, or multiple services could require more RAM and disk space.

I would also document each configuration screen during the initial VM creation process instead of relying on existing machines. This would provide clearer evidence of the original configuration choices and make the build process easier for another person to reproduce.

Finally, I would perform and record network tests immediately after configuring both guests, so that any temporary connectivity problems could be identified and documented.