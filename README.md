# AD-HomeLab
Active Directory Home Lab Setup
# Active Directory Home Lab

Built a fully functional Active Directory environment in VirtualBox for hands-on learning and cybersecurity skill development.

## Lab Architecture

| Component | OS | Role | IP |
|-----------|-----|------|-----|
| Domain Controller | Windows Server 2022 | AD DS, DNS | 192.168.1.10 |
| Client Workstation | Windows 11 Pro | Domain-joined | 192.168.1.20 |

## What I Built

- [x] Windows Server 2022 Domain Controller
- [x] Active Directory Domain Services (AD DS)
- [x] DNS server configuration
- [x] Windows 11 Pro domain-joined client
- [x] Static IP configuration on internal network
- [x] Domain user authentication

## Key Skills Demonstrated

- VirtualBox VM configuration & networking
- Windows Server administration
- Active Directory deployment
- DNS configuration
- Domain joining & authentication
- TCP/IP networking on isolated internal network

## Tools Used

- VirtualBox
- Windows Server 2022 Evaluation
- Windows 11 Pro
- Active Directory Users and Computers
- Server Manager

## Troubleshooting Log

| Issue | Error Message | Root Cause | Solution |
|-------|---------------|------------|----------|
| VM won't start | "VT-x is disabled in the BIOS" | Hardware virtualization disabled | Enabled VT-x in BIOS/UEFI settings |
| VM aborts | "Not in a hypervisor partition" | Hyper-V conflicting with VirtualBox | Disabled Hyper-V via Windows Features |
| Windows 11 reinstall | Automatically installs Home edition | Previous installation cached | Deleted VHD and recreated VM from scratch |
| Domain join fails | "Specified username is invalid" | Used forward slash instead of backslash | Changed `DBC/Admin` to `DBC\Administrator` |
| Domain option greyed out | Can't select "Domain" radio button | Windows 11 Home doesn't support domain join | Reinstalled Windows 11 Pro |

## Lessons Learned

### Virtualization Setup
- **Always check BIOS first** - VT-x/AMD-V must be enabled before any VM work
- **Hyper-V conflicts** - Windows 11 has Hyper-V features enabled by default that block VirtualBox; disable them
- **Promiscuous mode** - Leave on "Deny" for basic AD labs; only enable for packet sniffing

### Windows Server Configuration
- **Desktop Experience** - Choose GUI version for learning; Core is command-line only
- **DNS setup** - Point DNS to `127.0.0.1` (loopback) on the domain controller itself
- **Forest vs Tree** - First domain controller = new forest, not child domain
- **Delegation warning** - Normal for new forests; no action required

### Windows 11 Client
- **Edition matters** - Home edition cannot join domains; must use Pro/Enterprise/Education
- **Force Pro selection** - Use `Shift+F10` → `regedit` → add `BypassNRO` DWORD during setup
- **Username format** - Always use `DOMAIN\Username` (backslash, not forward slash)
- **Network settings** - Set DNS to domain controller IP before attempting domain join

### Active Directory
- **Built-in accounts** - Administrator and Guest are created automatically; Guest is disabled by default
- **Domain join credentials** - Use `DBC\Administrator` not just `admin` or `administrator`
- **Internal network** - Isolated network prevents conflicts; no internet needed for basic AD

## Next Steps

- [ ] Create organizational units (OUs)
- [ ] Deploy Group Policy objects
- [ ] Set up file sharing & permissions
- [ ] Practice user/group management
- [ ] Explore AD security features
- [ ] Document Group Policy configurations

## Screenshots

![Server Manager - AD DS Installed](screenshots/WinServerAD.png)
*Server Manager showing Active Directory Domain Services installed and running*

![Active Directory Users and Computers](screenshots/Win11IP.png)
*Active Directory Users and Computers console with DBC.local domain*

![Windows 11 Domain Properties](screenshots/Win11IP.png)
*Windows 11 System Properties showing successful domain join to DBC.local*

![Network Configuration - Server](screenshots/serverIPConfig.png)
*Static IP configuration on Windows Server 2022 Domain Controller*

![Network Configuration - Client](screenshots/Finishedconnect.png)
*DNS settings on Windows 11 client pointing to domain controller*

---

**Built:** March 2026  
**Purpose:** Cybersecurity skill development & job interview preparation
