# Ticket 1 — New Developer Test Machine

## 1. What Was Asked

> Hi, we have someone starting on Monday and he needs a test computer set up. Nothing special, just so he can try things without breaking anything. Can you write down how to do it so I can do the next one myself? Thanks

**Requester:** Aigerim T. (Office Manager)

## 2. What Was Actually Needed

The request did not specify the operating system, hardware resources, virtualization software, networking requirements, or how the test environment should be protected.

I interpreted the request as requiring two virtual machines:

- Ubuntu Server Linux
- Windows 11

Virtual machines provide isolated environments in which a developer can experiment without directly changing the host operating system.

I made the following assumptions:

- VMware Workstation Pro would be used as the hypervisor.
- Both guests should have internet access.
- Both guests should be able to communicate with each other.
- NAT networking would be used.
- Snapshots would provide recovery points if an experiment damaged a guest.

The requester should ideally clarify what development tools the new employee will use, whether administrator access is required, and whether the machines need to connect to internal company resources.

I reused two existing virtual machines instead of installing new operating systems. This allowed me to verify the working environment, but it meant I could not capture screenshots of the original creation wizard.

## 3. What I Did

### Host computer

- CPU: Intel Core 5 210H
- Physical cores: 8
- Logical processors: 12
- Installed RAM: 16 GB
- C: drive capacity: approximately 953.75 GiB
- C: drive free space: approximately 725.25 GiB

### Virtual machine allocation

| Resource | Ubuntu Server | Windows 11 |
|---|---:|---:|
| RAM | 4 GB | 6 GB |
| CPU cores | 2 | 2 |
| Virtual disk capacity | 40 GB | 64 GB |
| Network | NAT | NAT |

The two VMs allocate 10 GB of the host's 16 GB RAM, leaving approximately 6 GB for the host when both are running.

I allocated two CPU cores to each guest to provide processing capacity while retaining resources for the host.

The combined virtual disk capacity is 104 GB. This is the maximum capacity assigned to the virtual disks, not necessarily the amount of physical storage currently occupied. The host had approximately 725.25 GiB of free space, which is sufficient for the assigned virtual disk capacities.

### Networking

Both virtual machines use NAT networking. NAT allows guests to access the internet through the host's network connection without requiring them to appear as separate devices on the physical network.

The configured IP addresses were:

- Ubuntu: `192.168.208.129`
- Windows: `192.168.208.130`

Both guests were on the `192.168.208.0/24` subnet.

The following connectivity tests were performed:

| Test | Result |
|---|---|
| Ubuntu to Windows | 4 received, 0% loss |
| Windows to Ubuntu | 4 received, 0% loss |
| Ubuntu to internet | 4 received, 0% loss |
| Windows to internet (retest) | 4 received, 0% loss |
| Windows to google.com | 4 received, 0% loss |

### Snapshots

Both virtual machines already had baseline snapshots. I confirmed their existence and captured separate screenshots of their snapshot lists.

Snapshots provide recovery points that allow a VM to return to a previously saved state.

### Troubleshooting

During the first Windows-to-internet connectivity test, `ping 8.8.8.8` returned 3 replies out of 4, resulting in 25% packet loss.

I repeated the test without changing the network configuration, and all 4 packets were received successfully. I also tested `ping google.com`, which successfully resolved the domain name and received all 4 replies.

The initial packet loss was temporary and could not be reproduced during the retests. I recorded both the initial unsuccessful attempt and the successful results.

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

Finally, I would perform and record network tests immediately after configuring both guests, so that any temporary connectivity problems could be identified and documented at the time.