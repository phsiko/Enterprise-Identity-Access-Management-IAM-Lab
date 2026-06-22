# Enterprise Identity & Access Management (IAM) Lab

## Objective
Architected a simulated corporate IT infrastructure to demonstrate proficiency in Windows Server administration, centralized identity management,
and endpoint security enforcement. This project showcases the ability to provision enterprise users, route virtual networks, and deploy Group Policy Objects (GPOs) to maintain a secure and automated end-user environment.

## Technology Stack
*   **Hypervisor:** Oracle VirtualBox (Custom NAT Networking)
*   **Servers:** Windows Server 2022 (Domain Controller, DNS, DHCP)
*   **Endpoints:** Windows 10 Enterprise
*   **Identity & Access:** Active Directory Domain Services (AD DS)
*   **Automation & Security:** Group Policy Management Console (GPMC)

---

## 1. Directory Infrastructure & Role-Based Access
Architected a logical Active Directory hierarchy. Created custom Organizational Units (OUs)
to segment users by department rather than utilizing default containers, allowing for targeted Group Policy application based on role.

<img width="1013" height="847" alt="Screenshot 2026-06-22 155250" src="https://github.com/user-attachments/assets/1a1c017d-6dc4-4c2f-8686-cdb1b7a8ea7b" />
<img width="1002" height="767" alt="Screenshot 2026-06-22 155232" src="https://github.com/user-attachments/assets/953ccac6-cd00-4b6a-bd55-50071599d882" />
<img width="910" height="685" alt="Screenshot 2026-06-22 155015" src="https://github.com/user-attachments/assets/e4909198-855d-40d2-90cc-b5148fddec30" />



## 2. Centralized DNS & Endpoint Enrollment
Successfully routed the client endpoint to the Windows Server for DNS resolution and authenticated 
the machine to the local domain, establishing the server as the centralized identity provider.

<img width="1013" height="856" alt="Screenshot 2026-06-22 154625" src="https://github.com/user-attachments/assets/b2152ba2-4a6d-4e98-8070-2d79aa3bc4ce" />
<img width="1008" height="841" alt="Screenshot 2026-06-22 154325" src="https://github.com/user-attachments/assets/936466ec-e877-4a68-a2a1-617f474787e9" />

## 3. Endpoint Security & Data Loss Prevention (DLP)
Engineered and linked Group Policy Objects (GPOs) to the Company Users OU. Enforced endpoint data loss prevention
by restricting mounting privileges for all external removable storage devices.
<img width="901" height="605" alt="Screenshot 2026-06-22 160043" src="https://github.com/user-attachments/assets/1b018060-9134-4a96-9299-6194cf482ac8" />
<img width="977" height="767" alt="Screenshot 2026-06-22 155956" src="https://github.com/user-attachments/assets/f1ba3649-918d-4c7e-8b27-a65f35fe2b46" />


## 4. Resource Automation via Group Policy Preferences
Streamlined end-user onboarding by utilizing Group Policy Preferences to automatically map localized network file shares 
upon user authentication, ensuring immediate access to department resources. Addressed and resolved underlying NTFS security permissions to ensure accurate read/execute access.

<img width="1008" height="772" alt="Screenshot 2026-06-22 160456" src="https://github.com/user-attachments/assets/7cf8fb62-9499-4a29-aaea-b1223b22984c" />


## 5. Policy Validation & End-User Experience
Verified GPO propagation on the client endpoint via forced policy updates (`gpupdate /force`). Demonstrated successful 
automated mounting of network resources and active restriction of localized hardware peripherals on the client desktop.
<img width="1008" height="772" alt="Screenshot 2026-06-22 160456" src="https://github.com/user-attachments/assets/033d975a-bbe1-4358-9e8b-fcb337ebef15" />
