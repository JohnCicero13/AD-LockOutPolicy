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
- Windows Server 2022
- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services

## 📂 Implementation Steps

### 1️⃣ Launch Group Policy Management
Log into a Domain Controller.
```plaintext
Start Menu → type 'gpmc.msc' → and press enter
```
<p align="center"> <img src="https://i.imgur.com/ipcoMQU.png" alt="GPMC"/> </p>

### 2️⃣ Create or Edit a GPO
```plaintext
Navigate to 'Group Policy Objects' → Right-click to 'create a new GPO' or select an existing one to 'edit' → Give it a name like "Account Lockout Policy"
```
<p align="center"> <img src="https://i.imgur.com/Ep9d6Uo.png" alt="Rename"/> </p>

### 3️⃣ Navigate to Account Lockout Settings  
```plaintext
Expand: Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
```
<p align="center"> <img src="https://i.imgur.com/kEPOXyX.png" alt="Acc lockout policy"/> </p>

### 4️⃣ Configure Account Lockout Policy
Set the following values:
```
Account Lockout Duration: Check 'Define this policy setting' → Set desired lockout duration → Click Apply
```
<p align="center"> <img src="https://i.imgur.com/I5G0Ilu.png" alt="Desired lockout duration"/> </p>

```
A "Suggested Value Changes" window will pop up based on the set value of 'Account lockout duration', suggested values will be set for 'Account lockout threshold' and 'Reset account lockout counter after' → Click OK
```

<p align="center"> <img src="https://i.imgur.com/DNF6XeN.png" alt="Acc lockout policy"/> </p>

```
Click OK again
```
<p align="center"> <img src="https://i.imgur.com/cjUwybR.png" alt="Acc lockout policy"/> </p>

```
Account Lockout Threshold: Set 'Account will lockout after:' to desired value of 'invalid logon attempts' → Click OK
```
<p align="center"> <img src="https://i.imgur.com/OPeOEnp.png" alt="Acc lockout policy"/> </p>

```
A "Suggested Value Changes" window may pop up based on the set value of 'Account lockout threshold', 'Allow Administrator account lockout' may be set from Disabled to Enabled → Click OK
```
<p align="center"> <img src="https://i.imgur.com/8qqeRjZ.png" alt="Acc lockout policy"/> </p>

```
Reset Account Lockout Counter After: Set 'Reset account lockout counter after' to desired value → Click OK
```
<p align="center"> <img src="https://i.imgur.com/Zv1Y2ef.png" alt="Acc lockout policy"/> </p>

### 5️⃣ Link the GPO
```
Right-click your target 'Organizational Unit (OU)' or domain → Select 'Link an Existing GPO' → Choose your policy → Click OK.
```
<p align="center"> <img src="https://i.imgur.com/jeXjkMb.png" alt="Acc lockout policy"/> </p>

<p align="center"> <img src="https://i.imgur.com/VOlupQ7.png" alt="Acc lockout policy"/> </p>

### 6️⃣ Apply Group Policy
To force-update policies:
```bash
Run 'CMD' → Enter command 'gpupdate /force'
```
<p align="center"> <img src="https://i.imgur.com/cVX0bKP.png" alt="Acc lockout policy"/> </p>

### 7️⃣ Validate GPO's Effectiveness on Domain Users Account
```
Atempt 5 logons to Domain Controller with invalid password to trigger account lockout. The Remote Desktop connection used to connect to the Domain Controllers VM displayed this message of the GPO's effective lockout policy
```
<p align="center"> <img src="https://i.imgur.com/lNSnr8s.png" alt="Acc lockout policy"/> </p>

```
Sign into different Admin user on Domain controller → Open 'Active Directory Users and Computers' → Find locked out user → Right click on user → Click Properties → Click Account → On Unlock account check box, "This account is currently locked out" message should appear.
```
<p align="center"> <img src="https://i.imgur.com/5dsKNwD.png" alt="Acc lockout policy"/> </p>

```
An alternate method of viewing various events such as user lockouts is by typing 'eventvwr.msc' in the start menu
```
<p align="center"> <img src="https://i.imgur.com/fnpe1Ug.png" alt="Acc lockout policy"/> </p>

```
Navigate to 'Windows Logs' → Right click on 'Security' → Click 'Find'
```
<p align="center"> <img src="https://i.imgur.com/k4fyqBw.png" alt="Acc lockout policy"/> </p>

```
Search the user locked out of Domain Controller → Click 'Find Next'
```
<p align="center"> <img src="https://i.imgur.com/b7Hk2vF.png" alt="Acc lockout policy"/> </p>

```
The most recent event should be an 'Account Lockout' Double click on the event to view all details of the event
```
<p align="center"> <img src="https://i.imgur.com/1Mtz9VN.png" alt="Acc lockout policy"/> </p>
