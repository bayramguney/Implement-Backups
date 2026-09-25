# Implement-Backups

# Applied Lab: Implement Backups

## Overview

This lab demonstrates the importance of **data protection, backup strategies, and recovery processes** in cybersecurity environments.

As a security team member at **Structureality Inc.**, I configured Windows Server backup solutions, created backup storage, restored deleted files, and used **Volume Shadow Copy Service (VSS)** to recover previous file versions.

This lab supports the concept of **resilience and recovery in security architecture**, which is a critical responsibility for cybersecurity professionals.

---

# Lab Scenario

Organizations must protect critical data against:

- Accidental deletion
- Data corruption
- System failures
- Security incidents
- Ransomware attacks

In this lab, I performed backup and recovery operations using:

- Windows Server Backup
- Disk Management / DiskPart
- Volume Shadow Copy Service (VSS)

---

# Environment

| Component | Details |
|---|---|
| Computer | PC10 |
| Operating System | Windows Server 2019 |
| User Account | Jaime |
| Backup Target Drive | Backup01 (F:) |
| Backup Tool | Windows Server Backup |
| Recovery Technology | Volume Shadow Copy Service |

---

# CompTIA Security+ Objective

## Security+ SY0-701 Objective 3.4

**Explain the importance of resilience and recovery in security architecture.**

Skills practiced:

- Backup planning
- Data recovery
- Storage preparation
- File restoration
- Business continuity concepts
- Disaster recovery fundamentals

---

# Lab Tasks Completed

## 1. Prepare Backup Storage

### Objective

Create a dedicated storage location to use as backup media.

A secondary disk was configured as:

```
Disk 1 → Backup01 → Drive F:
```

---

## DiskPart Commands Used

Opened Command Prompt as Administrator and launched DiskPart:

```cmd
diskpart
```

Selected the backup disk:

```cmd
select disk 1
```

Enabled the disk:

```cmd
online disk
```

Cleared read-only attribute:

```cmd
attribute disk clear readonly
```

Created a primary partition:

```cmd
create partition primary
```

Formatted the volume:

```cmd
format fs=ntfs label="Backup01" quick
```

Assigned drive letter:

```cmd
assign letter=f
```

Exited DiskPart:

```cmd
exit
```

---

# 2. Create Test Files for Backup

Created sample files to test backup and restoration.

Copied:

```
C:\SETUP\NetworkMiner\Fingerprints\oui.txt
```

into:

```
C:\Users\Jaime\Documents
```

Created:

```
document01.txt
document02.txt
document03.txt
```

Also created:

```
C:\Users\Public\document04.txt
```

---

# 3. Configure Windows Server Backup

## Backup Configuration

Created a one-time backup using:

```
Windows Server Backup
```

Backup source:

```
C:\Users
```

Backup destination:

```
Backup01 (F:)
```

---

## Backup Process

Steps performed:

1. Opened Windows Server Backup
2. Selected Local Backup
3. Started Backup Once Wizard
4. Selected Custom Backup
5. Added:

```
C:\Users
```

6. Selected:

```
Backup01 (F:)
```

7. Completed backup operation

---

# Backup Purpose

Backups provide protection against:

- Accidental file deletion
- Hardware failure
- Malware damage
- Data loss
- Ransomware incidents

---

# 4. Restore Deleted File from Backup

## File Deletion Test

Deleted:

```
C:\Users\Jaime\Documents\document01.txt
```

The Recycle Bin was emptied to simulate permanent deletion.

---

## Recovery Process

Used:

```
Windows Server Backup → Recover
```

Selected:

```
This server (PC10)
```

Recovery type:

```
Files and folders
```

Restored:

```
C:\Users\Jaime\Documents\document01.txt
```

Recovery location:

```
Original location
```

---

## Result

The deleted file was successfully restored.

This demonstrates how backups support:

- Data recovery
- Incident response
- Business continuity

---

# 5. Configure Volume Shadow Copy Service (VSS)

## What is VSS?

Volume Shadow Copy Service creates snapshots of files and allows users to restore previous versions.

VSS is useful for:

- Recovering modified files
- Restoring previous file states
- Protecting against accidental changes

---

# Enable VSS on Drive C:

Enabled Shadow Copies:

```
Disk Management
→ C: Properties
→ Shadow Copies
→ Enable
```

---

# Force a Shadow Copy

Opened Command Prompt as Administrator.

Executed:

```cmd
wmic shadowcopy call create Volume=c:\
```

Verified:

```
Method execution successful
```

---

# 6. Restore Previous File Version Using VSS

## Modify File

Changed:

```
C:\Users\Public\document04.txt
```

Added:

```
changed
```

as the first line.

---

## Restore Previous Version

Used:

```
Right-click document04.txt
→ Restore previous versions
```

Selected the latest version.

Clicked:

```
Restore
```

---

## Result

The file was restored to its previous state.

The added text:

```
changed
```

was removed.

---

# Backup vs Volume Shadow Copy

| Feature | Backup | Volume Shadow Copy |
|---|---|---|
| Protects deleted files | Yes | No |
| Restores previous versions | Yes | Yes |
| Requires backup storage | Yes | No |
| Used for disaster recovery | Yes | Limited |
| Protects against hardware failure | Yes | No |

---

# Security Concepts Learned

## Backup Strategy

A strong backup strategy includes:

- Regular backups
- Offline copies
- Secure storage
- Recovery testing
- Access controls

---

## Recovery and Resilience

Cybersecurity teams must prepare for:

- Data loss
- System compromise
- Hardware failure
- Ransomware attacks

Recovery planning reduces downtime and improves organizational resilience.

---

# Real-World Cybersecurity Applications

Backup and recovery knowledge is important for:

### SOC Analysts

- Investigating ransomware incidents
- Validating recovery points
- Supporting incident response

### Security Administrators

- Managing backup permissions
- Protecting backup systems
- Testing recovery procedures

### Incident Response Teams

- Restoring compromised systems
- Recovering deleted evidence
- Maintaining business operations

---

# Skills Demonstrated

✅ Windows Server Backup configuration  
✅ DiskPart storage management  
✅ Backup media preparation  
✅ File restoration  
✅ Volume Shadow Copy Service (VSS)  
✅ Data recovery concepts  
✅ Security resilience principles  
✅ Disaster recovery fundamentals  

---

# Key Takeaways

- Backups are a critical security control.
- Recovery procedures must be tested regularly.
- VSS provides quick file version recovery but is not a replacement for backups.
- Organizations need layered recovery strategies to maintain availability.

---

# Conclusion

This lab provided hands-on experience with Windows Server backup and recovery technologies.

By creating backups, restoring deleted files, and using Volume Shadow Copy Service, I gained practical knowledge of how cybersecurity professionals maintain **availability, resilience, and data protection** in enterprise environments.
