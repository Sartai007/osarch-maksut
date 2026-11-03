# Build Guide — Linux and Windows Test Machines

## 1. Purpose

This guide explains how to create two isolated virtual machines using VMware Workstation Pro:

- Ubuntu Server Linux
- Windows 11

The purpose is to provide a developer with separate environments for testing software without directly affecting the host computer.

The instructions are written for someone who has never created a virtual machine before.

**Important:** The virtual machines used for this ticket already existed. Their configurations were reused and tested. This document describes how to reproduce the environment from scratch.

## 2. Host Computer Requirements and Resource Planning

### Reference host specifications

| Component | Specification |
|---|---|
| CPU | Intel Core 5 210H |
| Physical cores | 8 |
| Logical processors | 12 |
| Installed RAM | 16 GB |
| Available disk space (measured) | Approximately 725.25 GiB |
| Hypervisor | VMware Workstation Pro |

### Planned virtual machine resources

| Resource | Ubuntu Server | Windows 11 |
|---|---:|---:|
| RAM | 4 GB | 6 GB |
| CPU cores | 2 | 2 |
| Virtual disk capacity | 40 GB | 64 GB |
| Network adapter | NAT | NAT |

The guests use 10 GB of RAM combined, leaving approximately 6 GB for the host. Two CPU cores per guest provide sufficient processing capacity for basic development and testing.

The combined virtual disk capacity is 104 GB. This is the maximum capacity assigned to the virtual disks, not necessarily their current physical storage usage.

Before starting, ensure that the host has enough free disk space and that the required installation ISO files are available.

## 3. Create the Ubuntu Server Virtual Machine

### Step 1 — Open VMware Workstation

1. Start VMware Workstation Pro.
2. Select **Create a New Virtual Machine**.
3. Choose **Typical (recommended)**.
4. Click **Next**.

The Typical wizard provides a straightforward configuration process suitable for a standard test machine.

*Screenshot to capture: VMware's new virtual machine wizard.*

### Step 2 — Select the installation media

1. Select **Installer disc image file (ISO)**.
2. Browse to the Ubuntu Server ISO file.
3. Select the ISO and click **Next**.
4. If VMware offers an Easy Install option, review the displayed settings before continuing.

The ISO contains the operating system installation files required to install Ubuntu inside the virtual machine.

*Screenshot to capture: Selected Ubuntu Server ISO.*

### Step 3 — Name the virtual machine

1. Enter `lab01-ubuntu` as the virtual machine name.
2. Choose a location with sufficient free storage.
3. Click **Next**.

A descriptive name makes the machine easier to identify and manage.

*Screenshot to capture: VM name and storage location.*

### Step 4 — Configure the virtual disk

1. Set the maximum disk capacity to **40 GB**.
2. Select **Store virtual disk as a single file**, if offered.
3. Continue to the next screen.

A 40 GB virtual disk provides room for the Ubuntu operating system, development tools, and test files. A single virtual disk file is simpler to manage, although splitting it into multiple files may be useful for file-system or portability constraints.

*Screenshot to capture: Ubuntu virtual disk capacity and storage option.*

### Step 5 — Configure hardware resources

Before finishing the wizard, open **Customize Hardware**.

Set the following values:

| Setting | Value |
|---|---:|
| Memory | 4 GB |
| Processors | 2 |
| Network Adapter | NAT |

Leave other settings at their defaults unless the installation requires a change.

The 4 GB RAM allocation is sufficient for a basic Ubuntu Server environment. Two processor cores provide resources for ordinary testing while leaving capacity for the host.

NAT allows the guest to access the internet through the host's network connection.

*Screenshot to capture: Ubuntu memory, processor, and network settings.*

### Step 6 — Install Ubuntu Server

1. Finish the wizard.
2. Select the Ubuntu VM and click **Power on**.
3. Follow the Ubuntu Server installation instructions.
4. Select the required language and keyboard layout.
5. Configure networking using the available default settings.
6. Select the installation storage and confirm the disk changes.
7. Create a username and password.
8. Complete the installation and restart when prompted.

The installer configures the operating system inside the virtual disk rather than modifying the host operating system.

*Screenshot to capture: Ubuntu installation screen and completed installation.*

### Step 7 — Verify Ubuntu

Log in to the new Ubuntu virtual machine and run:

```bash
uname -a
ip -br addr
```

The first command displays the kernel and architecture information. The second displays the network interfaces and their IP addresses.

Record the actual output of `uname -a` in `evidence/04-guest-uname.txt`.

*Screenshot to capture: Ubuntu terminal showing the verification commands.*

## 4. Create the Windows 11 Virtual Machine

### Step 1 — Start the creation wizard

1. Return to VMware Workstation.
2. Select **Create a New Virtual Machine**.
3. Choose **Typical (recommended)**.
4. Click **Next**.

Using the same wizard type for both guests keeps the process consistent and makes the guide easier to follow.

*Screenshot to capture: Windows VM creation wizard.*

### Step 2 — Select the Windows installation media

1. Select **Installer disc image file (ISO)**.
2. Browse to the Windows 11 ISO file.
3. Select the ISO and click **Next**.
4. If VMware detects the operating system automatically, check that it identifies Windows 11 or the appropriate Windows 64-bit version.

The ISO provides the installation files for the Windows guest.

*Screenshot to capture: Selected Windows 11 ISO.*

### Step 3 — Configure the operating system and name

1. If prompted, select **Microsoft Windows** as the guest operating system.
2. Select the appropriate Windows 11 64-bit version if available.
3. Name the virtual machine `lab02-win11`.
4. Choose a location with sufficient free storage.
5. Click **Next**.

A separate name and VM directory make the Windows guest easy to distinguish from the Ubuntu guest.

*Screenshot to capture: Windows guest operating system and VM name.*

### Step 4 — Configure the virtual disk

1. Set the maximum disk capacity to **64 GB**.
2. Select **Store virtual disk as a single file**, if offered.
3. Continue to the next screen.

Windows 11 requires more storage than the basic Ubuntu Server installation. The 64 GB allocation provides space for Windows, updates, and basic development tools.

*Screenshot to capture: Windows virtual disk capacity and storage option.*

### Step 5 — Configure hardware resources

Open **Customize Hardware** before finishing the wizard.

Set the following values:

| Setting | Value |
|---|---:|
| Memory | 6 GB |
| Processors | 2 |
| Network Adapter | NAT |

For a Windows 11 installation, also check the virtual machine's firmware and security requirements. Use UEFI firmware, enable Secure Boot where supported, and provide a virtual TPM 2.0 if required by the Windows installer. VMware may require the VM to be encrypted before a virtual TPM can be added.

Leave other settings at their defaults unless Windows installation requires a change.

The 6 GB RAM allocation gives Windows more memory than the Ubuntu guest because the desktop operating system has a higher resource requirement.

*Screenshot to capture: Windows memory, processor, network, firmware, and security settings.*

### Step 6 — Install Windows 11

1. Finish the wizard.
2. Select the Windows VM and click **Power on**.
3. Follow the Windows installation instructions.
4. Select the language, time, and keyboard settings.
5. Choose **Install Windows**.
6. Select the installation disk created for the VM.
7. Follow the remaining installation prompts.
8. Complete the initial Windows setup and create or sign in with the required account.

The installation takes place inside the virtual disk. It does not replace or modify the host's Windows installation.

*Screenshot to capture: Windows installation and initial setup.*

### Step 7 — Verify Windows

Open **Command Prompt** inside the Windows guest and run:

```cmd
systeminfo
ipconfig
```

`systeminfo` displays operating system and hardware information. `ipconfig` displays the network configuration and assigned IP address.

Record the Windows VM's IP address for the network tests in Section 5.

*Screenshot to capture: Windows Command Prompt showing the verification commands.*

## 5. Configure and Test Networking

### Step 1 — Check the network adapter settings

1. Shut down each guest if necessary.
2. Open its virtual machine settings in VMware Workstation.
3. Select **Network Adapter**.
4. Confirm that **NAT** is selected.
5. Repeat for the other guest.

NAT allows both virtual machines to access external networks through the host. It is appropriate for this setup because the guests do not need to appear as separate devices on the physical network.

*Screenshot to capture: NAT network adapter settings for each VM.*

### Step 2 — Check internet connectivity

Inside Ubuntu, run:

```bash
ping -c 4 8.8.8.8
ping -c 4 google.com
```

Inside Windows Command Prompt, run:

```cmd
ping 8.8.8.8
ping google.com
```

The first test checks connectivity to an external IP address. The second also checks whether DNS can resolve a domain name.

Successful replies indicate that the guest can reach the internet. If the IP test works but the domain-name test fails, investigate DNS configuration.

*Screenshot to capture: Successful internet connectivity tests in both guests.*

### Step 3 — Test communication between the guests

First, identify the IP address of each guest:

- Ubuntu: use `ip -br addr`.
- Windows: use `ipconfig`.

Then, from Ubuntu, ping the Windows IP address:

```bash
ping -c 4 <WINDOWS_IP>
```

From Windows, ping the Ubuntu IP address:

```cmd
ping <UBUNTU_IP>
```

Replace the placeholders with the actual addresses displayed by the guests.

Both guests should be able to exchange replies. This confirms that they can communicate over the virtual network.

*Screenshot to capture: Successful ping tests between Ubuntu and Windows.*

**Note:** If a guest does not respond, check its firewall settings before changing the VMware network configuration. Windows Firewall may block incoming ping requests by default. If necessary, enable the inbound ICMPv4 Echo Request rule for the appropriate private network profile rather than disabling the firewall entirely.

## 6. Create Recovery Snapshots

### Step 1 — Prepare the guests

1. Confirm that Ubuntu has completed installation and can log in.
2. Confirm that Windows has completed installation and can log in.
3. Check that both guests have working network connections.
4. Shut down each guest cleanly before creating its snapshot, unless your VMware version supports the intended snapshot operation while powered on.

A snapshot preserves a recoverable state of the virtual machine. It is useful when testing software or making configuration changes that might break the guest.

*Screenshot to capture: Each guest in its initial working state.*

### Step 2 — Create a snapshot for Ubuntu

1. Select the Ubuntu VM in VMware Workstation.
2. Open the **Snapshot** menu.
3. Select **Take Snapshot**.
4. Enter a descriptive name, such as `T1-Ubuntu-Initial-Working`.
5. Add a short description and confirm.

The snapshot records the working Ubuntu state before further experimentation.

*Screenshot to capture: Ubuntu snapshot list.*

### Step 3 — Create a snapshot for Windows

1. Select the Windows VM.
2. Open the **Snapshot** menu.
3. Select **Take Snapshot**.
4. Enter a descriptive name, such as `T1-Windows11-Initial-Working`.
5. Add a short description and confirm.

Keeping a separate snapshot for each guest makes it possible to restore either environment independently.

*Screenshot to capture: Windows snapshot list.*

## 7. Troubleshooting

### Problem 1 — Windows VM requires encryption for virtual TPM

**Symptom:** VMware does not allow a virtual TPM to be added or reports that encryption is required.

**Resolution:**

1. Open the Windows VM settings.
2. Locate the encryption or access-control option.
3. Follow VMware's instructions to encrypt the VM.
4. Return to the hardware settings and add the virtual TPM 2.0 device.
5. Confirm that the Windows installation can proceed.

A virtual TPM provides the security component required by supported Windows 11 configurations. Encryption is needed by VMware to protect the virtual TPM state.

### Problem 2 — Guest-to-guest ping fails

**Symptom:** One guest does not respond to ping requests from the other.

**Resolution:**

1. Check the IP address of each guest.
2. Confirm that both guests use NAT.
3. Check that both addresses belong to the same virtual subnet.
4. Check the guest firewall rules, especially Windows inbound ICMPv4 Echo Request.
5. Repeat the ping test in both directions.

This process helps distinguish a network configuration problem from a firewall rule blocking ping requests.

### Problem 3 — Internet connectivity is inconsistent

**Symptom:** A ping test loses packets or does not receive replies.

**Resolution:**

1. Repeat the test several times.
2. Test an external IP address such as `8.8.8.8`.
3. Test a domain name such as `google.com`.
4. Compare the results to determine whether the issue affects general connectivity or DNS resolution.
5. Record both unsuccessful and successful results instead of reporting only the final test.

A repeated test helps determine whether packet loss is temporary or persistent.

## 8. Final Verification Checklist

Before handing over the virtual machines, confirm the following:

- [ ] Ubuntu Server boots and accepts login.
- [ ] Windows 11 boots and accepts login.
- [ ] Ubuntu has the planned 4 GB RAM, 2 CPU cores, and 40 GB virtual disk.
- [ ] Windows has the planned 6 GB RAM, 2 CPU cores, and 64 GB virtual disk.
- [ ] Both network adapters use NAT.
- [ ] Both guests can access the internet.
- [ ] Both guests can communicate with each other.
- [ ] A recovery snapshot exists for each guest.
- [ ] The evidence files are saved in the ticket's `evidence/` directory.

The virtual machines are ready for basic development testing once all checks pass. A developer should use snapshots before major experiments so that a working environment can be restored if necessary.
