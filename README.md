# Enterprise Identity & Access Management (IAM) Lab

## Objective
The goal of this project was to build a simulated corporate IT infrastructure from scratch. It demonstrates hands-on experience with Windows Server administration, network configuration, and centralized identity management. By setting up a Domain Controller and a Windows 10 client, I was able to provision users, configure file share permissions, and deploy Group Policy Objects (GPOs) to secure and automate the end-user experience.

## Technology Stack
*   **Hypervisor:** Oracle VirtualBox (Custom NAT Networking)
*   **Servers:** Windows Server 2022 (Domain Controller, DNS, DHCP)
*   **Endpoints:** Windows 10 Enterprise
*   **Identity & Access:** Active Directory Domain Services (AD DS)
*   **Automation & Security:** Group Policy Management Console (GPMC)

---

## 1. Centralized DNS & Endpoint Enrollment
To get the lab communicating properly, the first major hurdle was networking. I set up a shared NAT network in VirtualBox so both virtual machines were on the same local switch. I configured a static IP address (`10.0.2.10`) on the Windows Server to act as the primary DNS server. On the Windows 10 client, I changed the IPv4 adapter settings to point its DNS directly to the server's IP. Once the networking was solid, I successfully joined the Windows 10 machine to the `raytech.local` domain, officially making the server the central authority.

<img width="1013" height="856" alt="Screenshot 2026-06-22 154625" src="https://github.com/user-attachments/assets/b2152ba2-4a6d-4e98-8070-2d79aa3bc4ce" />
<img width="1008" height="841" alt="Screenshot 2026-06-22 154325" src="https://github.com/user-attachments/assets/936466ec-e877-4a68-a2a1-617f474787e9" />

## 2. Directory Infrastructure & Role-Based Access
With the domain established, I needed to set up the company structure. Using Active Directory Users and Computers (ADUC), I moved away from the default Windows folders and created custom Organizational Units (OUs) for "Company Users" and an "IT Department" sub-folder. This makes it much easier to apply specific security policies later. Inside the IT OU, I created a new user account, set up a temporary password, and checked the box requiring the user to change their password on the first login to simulate a real Help Desk onboarding process.

<img width="1013" height="847" alt="Screenshot 2026-06-22 155250" src="https://github.com/user-attachments/assets/1a1c017d-6dc4-4c2f-8686-cdb1b7a8ea7b" />
<img width="1002" height="767" alt="Screenshot 2026-06-22 155232" src="https://github.com/user-attachments/assets/953ccac6-cd00-4b6a-bd55-50071599d882" />
<img width="910" height="685" alt="Screenshot 2026-06-22 155015" src="https://github.com/user-attachments/assets/e4909198-855d-40d2-90cc-b5148fddec30" />

## 3. Endpoint Security & Data Loss Prevention (DLP)
Next, I wanted to lock down the environment for security. I opened the Group Policy Management Console and created a new Group Policy Object (GPO) called "Disable_USB". I linked this policy directly to the Company Users OU so it would affect my test user. Inside the GPO editor, I navigated through the Administrative Templates to the Removable Storage Access settings and enabled the rule to deny read and write access to all removable storage classes. This prevents users from plugging in unauthorized flash drives.

<img width="901" height="605" alt="Screenshot 2026-06-22 160043" src="https://github.com/user-attachments/assets/1b018060-9134-4a96-9299-6194cf482ac8" />
<img width="977" height="767" alt="Screenshot 2026-06-22 155956" src="https://github.com/user-attachments/assets/f1ba3649-918d-4c7e-8b27-a65f35fe2b46" />

## 4. Resource Automation via Group Policy Preferences
For this step, I wanted to automate something users ask for all the time: access to company files. I created a folder called `SharedData` on the server's C: drive. To make sure it worked properly, I configured both the Sharing permissions and the underlying NTFS Security permissions so "Domain Users" had Read & Execute access. Then, I went back into Group Policy and created a new GPO using Drive Maps Preferences. I set it up so that anytime a user logs in, the server automatically maps that shared folder to their Z: drive.

<img width="1008" height="772" alt="Screenshot 2026-06-22 160456" src="https://github.com/user-attachments/assets/7cf8fb62-9499-4a29-aaea-b1223b22984c" />

## 5. Policy Validation & End-User Experience
Finally, I needed to prove that everything I built on the server actually worked on the employee's computer. I logged into the Windows 10 client as my test user. I opened the Command Prompt and ran `gpupdate /force` to command the computer to pull down the latest rules from the Domain Controller. When I opened File Explorer, the Z: drive was automatically mapped and fully accessible, confirming both the GPO and the network folder permissions were configured perfectly.

<img width="1008" height="772" alt="Screenshot 2026-06-22 160456" src="https://github.com/user-attachments/assets/033d975a-bbe1-4358-9e8b-fcb337ebef15" />
