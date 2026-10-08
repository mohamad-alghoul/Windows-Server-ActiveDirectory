# Windows-Server-ActiveDirectory
# Windows Server Enterprise Infrastructure & Active Directory Deployment Lab

An end-to-end hands-on deployment of a highly available, secure, and resilient Active Directory Domain Infrastructure (TEST.LOCAL). This lab simulates a real-world enterprise environment incorporating Domain Controllers (PDC & ADC Core), Group Policies (GPOs), DHCP Failover, DNS Load Balancing, Hyper-V Replication, and Automated Server Backups.

---

## Infrastructure Topology & Overview

- Domain Name: TEST.LOCAL
- Primary Domain Controller (PDC): Full GUI Installation (IP: 192.168.1.2/24, Gateway: 192.168.1.254)
- Additional Domain Controller (ADC): Windows Server Core (IP: 192.168.1.3/24, Gateway: 192.168.1.254)
- Network Services Scope: 192.168.1.40 to 192.168.1.230/24 (Lease Duration: 10 Days)

---

## Key Implementation Steps & Technical Features

### 1. Active Directory Domain Services (AD DS) & Core Setup
- Deployed Primary Domain Controller (PDC) and promoted Additional Domain Controller (ADC) on Windows Server Core for high availability.
- Structure implemented with dedicated Organizational Units (OUs) for departments: HR, Sales, Dev, and IT.
- Configured user accounts and department-specific security groups.
- Enabled Active Directory Recycle Bin for active object recovery.

### 2. Group Policy Management & Security Policies (GPO)
- Password Policy: Enforced 60-day password change interval, minimum length of 6 characters, complex password enforcement, and history memory of the last 3 passwords.
- Account Lockout Policy: Configured 1-hour account lockout after 4 consecutive failed login attempts.
- System Hardening & Restrictions:
  - Blocked access to external storage devices, Task Manager, and Control Panel.
  - Enabled Remote Desktop across domain computers via GPO.
  - Configured Remote Assistance allowing members of the IT Group to act as helpers.

### 3. Network Services (DHCP, DNS & Web Hosting)
- DHCP Configuration: Configured DHCP scope (192.168.1.40 – 192.168.1.230/24) excluding the range 192.168.1.80 to 192.168.1.85.
- DHCP High Availability: Implemented DHCP Failover between PDC and ADC (Server Core).
- Web & DNS Load Balancing: Installed IIS Web Server on PDC and ADC, utilizing DNS Round-Robin load balancing for www.test.local pointing to 192.168.1.2 and 192.168.1.3.

### 4. Enterprise Storage, Mapped Drives & Quota Management
- Departmental File Shares: Provisioned shared folders for Dev and HR with create/edit permissions while prohibiting deletion.
- File Screening (FSRM): Restricted users from storing audio, video, and executable (.exe) files within shared folders.
- Mapped Network Drives & Quotas:
  - Automatically mapped network drives for Dev and HR departments.
  - Configured a Public shared folder mapped drive for all domain users with a strict 2 GB quota.

### 5. Network Printing & Client Onboarding
- Added domain-wide network printer restricted to black & white printing, with active availability schedules between 9:00 AM and 4:00 PM.
- Successfully joined client machines to the TEST.LOCAL domain.

### 6. Disaster Recovery
- Automated Backups: Configured full daily server backups scheduled at 11:00 PM, targeting the ADC as the backup destination.

---

## Verification

- Active Directory Users & Computers (OUs & Groups)
- Group Policy Management Console (GPOs)
- DHCP Scope & Failover Configuration
- Hyper-V Replication Status

---

## Author

Mohamad Alghoul
Fachinformatiker für Systemintegration  
Certifications: CCNA, Microsoft 365 Certified: Endpoint Administrator Associate (MD-102)
