# GOAD Lab Build and Troubleshooting Report

## Objective

Build and configure the Game of Active Directory (GOAD) lab using VirtualBox, Vagrant, and Kali Linux, and prepare the environment for Active Directory attack simulation.

---

## Phase 1: Initial Setup

### Actions

* Installed VirtualBox on Windows
* Installed Kali Linux VM
* Cloned GOAD repository into WSL:

```bash
~/labs/GOAD-main
```

* Attempted to run:

```bash
vagrant up
```

### Issue: Environment Mismatch

* GOAD files located in WSL
* Vagrant installed on Windows
* VirtualBox installed on Windows

### Impact

* Path inconsistencies
* Permission errors
* Vagrant unable to manage VMs correctly

---

## Phase 2: Network Configuration and Troubleshooting

### Initial State

* All VMs configured with NAT
* No reliable communication between machines

---

### Action: Created NAT Network

* Configured all VMs to use a shared NAT network
* Ensured consistent adapter configuration

---

### Issue: Kali Network Not Assigning IPv4

* Interface present, but no IPv4 address

#### Attempted Fix

```bash
sudo dhclient -v eth0
```

#### Result

* Command not available

---

### Resolution

* Rebooted Kali VM
* DHCP assigned IP:

```text
192.168.56.5
```

---

### Issue: One-Way Connectivity

* SRV02 to Kali: successful
* Kali to SRV02: failed

---

### Root Cause

* Inconsistent gateway configuration
* Multiple network adapters causing routing conflicts

---

### Resolution

* Disabled secondary adapters on all VMs
* Ensured:

  * Single adapter per VM
  * Same network across all machines

---

### Result

```bash
nmap -sn 192.168.56.0/24
```

* Multiple hosts successfully discovered

---

## Phase 3: Enumeration Attempts

### SMB Enumeration

```bash
smbclient -L //192.168.56.7 -N
```

### Result

* NT_STATUS_CONNECTION_RESET
* NT_STATUS_ACCESS_DENIED

---

### Additional Enumeration Attempts

```bash
nmap -p 88,135,139,389,445 192.168.56.7
```

```bash
nmap --script smb-protocols,smb-os-discovery -p445 192.168.56.7
```

```bash
nmap -p 389 192.168.56.7
```

---

### Analysis

* SMBv1 disabled
* Anonymous access blocked
* LDAP not available

---

### Conclusion

Active Directory services were not running. The environment was not yet provisioned.

---

## Phase 4: Vagrant and Provisioning Issues

### Issue: Vagrant Not Found

```bash
vagrant: command not found
```

### Root Cause

* Vagrant installed on Windows, not in WSL

---

### Issue: Permission Errors

```text
Errno::EACCES
```

### Root Cause

* Windows Vagrant attempting to write to WSL filesystem

---

### Resolution

Moved GOAD project to Windows filesystem:

```text
C:\Users\mahon\Desktop\GOAD-main
```

---

## Phase 5: VirtualBox Conflicts

### Issues Encountered

#### NAT Rule Conflicts

* Duplicate port forwarding rules

#### VM Name Conflicts

* Existing VM names prevented creation

#### Ghost VM Registrations

* VMs registered without corresponding disk files

#### Directory Conflicts

* Existing folders prevented VM grouping

---

### Resolution Steps

#### Remove Vagrant State

```powershell
Remove-Item -Recurse -Force .\.vagrant
vagrant global-status --prune
```

---

#### Check VirtualBox VMs

```powershell
& "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" list vms
```

---

#### Remove VirtualBox VM Registrations

```powershell
& "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" unregistervm "GOAD-Light-DC01"
& "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" unregistervm "GOAD-Light-DC02"
& "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" unregistervm "GOAD-Light-SRV02"
```

---

#### Remove Stale VM Files

Deleted from:

```text
C:\Users\mahon\VirtualBox VMs\
```

Removed:

* GOAD-Light-DC01
* GOAD-Light-DC02
* GOAD-Light-SRV02
* GOAD folder

---

## Phase 6: Clean Rebuild

### Execution

```powershell
vagrant up
```

---

### Result

* VMs successfully initialized
* DC01 boot sequence started
* WinRM connection established

---

### Observed Configuration

* Adapter 1: NAT
* Adapter 2: Host-only

---

### Key Insight

The Vagrantfile defines the intended network architecture. Manual network modifications introduced conflicts.

---

## Current Status

* Vagrant environment aligned with Windows
* VirtualBox cleaned of stale state
* VMs rebuilding successfully
* Awaiting provisioning completion

---

## Lessons Learned

### Environment Consistency

Mixing WSL and Windows for Vagrant introduces avoidable complexity.

---

### Service Validation

A running VM does not imply services are configured. Always verify:

```bash
nmap -p 88,135,139,389,445 <target>
```

---

### VirtualBox State Persistence

VM registrations and disk references persist beyond visible UI state.

---

### Network Simplicity

Multiple adapters introduce routing issues. Follow lab-defined configurations.

---

### Troubleshooting Approach

* Validate assumptions
* Identify root causes
* Reset environment when necessary

---

## Next Phase

After provisioning completes:

* Validate Active Directory services
* Identify domain name
* Begin enumeration:

```bash
nmap -p 88,135,139,389,445 <dc-ip>
```

---

## Future Work

This report will be extended with:

* Domain architecture mapping
* Enumeration techniques
* Initial access methods
* Attack chain documentation
