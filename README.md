# 🔐 Lock & Secure: Deploying Account Lockout Policies Using GPOs

<p align="center">
<img src="https://i.imgur.com/97OPyMe.jpeg" alt="Account Lockout Screen"/>
</p>

## 📘 Overview
Fast-track Windows security with a clean walkthrough for deploying account lockout policies using Group Policy—prevent brute-force attacks with just a few clicks.

## 🎯 Objectives
- Understand the value of account lockout policies in Windows networks
- Apply lockout policy settings through Group Policy Management Console (GPMC)
- Test and validate the GPO’s effectiveness across user accounts

## 🛠️ Requirements
- Windows Server with Active Directory Domain Services (AD DS)
- Group Policy Management Console (GPMC)
- Administrative access to domain controller

## 🖥️ Systems/Environments and Technologies Used
- Windows 10 (21H2)
- Windows Server 2022
- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

## 📂 Implementation Steps

### 1️⃣ Launch Group Policy Management
Log into a Domain Controller.
```plaintext
Start Menu → type 'gpmc.msc' → and press enter
```
<p align="center"> <img src="https://i.imgur.com/ipcoMQU.png" alt="GPMC"/> </p>

### 2️⃣ Create or Edit a GPO
```plaintext
Navigate to **Group Policy Objects** → Right-click to **create a new GPO** or select an existing one to **edit** → Give it a name like `"Account Lockout Policy"`.
```
<p align="center"> <img src="https://i.imgur.com/Ep9d6Uo.png" alt="GPMC"/> </p>

### 3️⃣ Navigate to Account Lockout Settings
Expand:  
`Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy`

### 4️⃣ Configure Account Lockout Policy
Set the following values:
- **Account Lockout Duration**: Time before automatic unlock (e.g., 30 minutes)
- **Account Lockout Threshold**: Failed login attempts before lockout (e.g., 3)
- **Reset Account Lockout Counter After**: Time to reset the failed login count (e.g., 15 minutes)

> ⚙️ Double-click each setting → **Define this policy setting** → Input desired value.

### 5️⃣ Link the GPO
- Right-click your target **Organizational Unit (OU)** or domain.
- Select **Link an Existing GPO**, choose your policy, and click OK.

### 6️⃣ Apply Group Policy
To force-update policies:  
```bash
gpupdate /force
