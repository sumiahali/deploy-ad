# Active Directory Setup in Azure

This tutorial will guide you through installing and configuring Active Directory (AD) in a lab environment. You’ll set up a Domain Controller (DC), create a Domain Admin, and join a client machine to the domain.

---

## Environments and Technologies Used

- **Microsoft Azure**
- **Windows Server 2022** (Domain Controller VM)
- **Windows 11** (Client VM)
- **Active Directory Domain Services (AD DS)**
- **Active Directory Users and Computers (ADUC)**

---

## Operating Systems Used

- **Windows Server 2022** – Domain Controller (DC-1)
- **Windows 11** – Client machine (Client-1)

---

## Deployment and Configuration Steps

## 1. Install and Configure Active Directory Domain Services
1. Log in to **dc-1**.
2. Install **Active Directory Domain Services (AD DS)**.
   - *Why?:* AD DS is the Windows role that allows the server to function as a Domain Controller, managing authentication, users, groups, and policies.
<p>
  <img width="1318" height="709" alt="image" src="https://github.com/user-attachments/assets/3a03d2b1-a3b8-45f4-b0d6-77ad1d3b6031" />
  <img width="783" height="556" alt="image" src="https://github.com/user-attachments/assets/2133890e-2cee-49e5-8486-b9061df31b5b" />
  <img width="774" height="555" alt="image" src="https://github.com/user-attachments/assets/b7634c96-7622-4123-b3a9-a5463f4130ce" />
  <img width="817" height="553" alt="image" src="https://github.com/user-attachments/assets/7e082e89-debd-4707-8e66-6bbb811902b3" />
  <img width="767" height="548" alt="image" src="https://github.com/user-attachments/assets/f3dcc8eb-1f4b-4132-b98a-56250d728a87" />
</p>
3. Promote the server as a **Domain Controller**:
   - Create a new forest: `mydomain.com`.
   - *Why?:* A “forest” is the top-level container for Active Directory. Since this is the first DC, it must create a new forest and domain namespace.
<p>
  <img width="1288" height="677" alt="image" src="https://github.com/user-attachments/assets/f011ccd7-e339-4065-b2a2-2a4dd7cd4e49" />
  <img width="757" height="558" alt="image" src="https://github.com/user-attachments/assets/6dec1b11-fb0d-4f65-b063-f7acd3652118" />
  <img width="759" height="559" alt="image" src="https://github.com/user-attachments/assets/1b75c779-692e-430f-a569-bd4849b846a8" />
  <img width="696" height="514" alt="image" src="https://github.com/user-attachments/assets/724894b7-1d3f-4813-af2b-26accc0da0c9" />
  <img width="679" height="181" alt="image" src="https://github.com/user-attachments/assets/8f348608-57e0-4cc4-969f-55253a49ca70" />

</p>
4. Restart DC-1 and Log back in as: mydomain.com\labuser
<p>
  <img width="1438" height="859" alt="image" src="https://github.com/user-attachments/assets/a24e8fc9-067a-4db3-8283-d837f80e169b" />
</p>

## 2. Create Organizational Units (OUs) and Admin Account
1. Open **Active Directory Users and Computers (ADUC)**.
<p>
  <img width="592" height="584" alt="image" src="https://github.com/user-attachments/assets/af54bacf-6428-4cf8-b373-fe2015ff3b0d" />
  <img width="750" height="528" alt="image" src="https://github.com/user-attachments/assets/69b5e6c7-1154-4535-bb37-21ee98f158c5" />
</p>
2. Create the following OUs:
- `_EMPLOYEES`
- `_ADMINS`
- *Why?:* OUs organize objects (users, groups, computers) and make it easier to apply Group Policies later. Using `_EMPLOYEES` and `_ADMINS` separates regular users from admins.
<p>
  <img width="1504" height="1056" alt="image" src="https://github.com/user-attachments/assets/ea94f673-09f7-4912-a548-f5fbfe784d9c" />
  <img width="870" height="754" alt="image" src="https://github.com/user-attachments/assets/379ef102-ef3d-43d3-9939-ca3d95cf4069" />
  <img width="872" height="756" alt="image" src="https://github.com/user-attachments/assets/4e3b7bb9-d9bd-4cb2-b02f-d3be31fad001" />
</p>
3. Create a new employee account:
- Name: **Jane Doe**
- Username: `jane_admin`
- Password: `Cyberlab123!`
- *Why?:* This gives you a dedicated domain admin account instead of relying on the built-in Administrator account, which is best practice for security.
<p>
  <img width="1502" height="1052" alt="image" src="https://github.com/user-attachments/assets/960023c5-d504-4604-b1d0-e92fb62fa57a" />
  <img width="870" height="752" alt="image" src="https://github.com/user-attachments/assets/75e0534f-f2ca-4bf2-8a10-8ac1c3168131" />
  <img width="864" height="752" alt="image" src="https://github.com/user-attachments/assets/d3feeef3-d3b0-4d47-bef0-2164679f5e84" />
</p>
4. Add `jane_admin` to the **Domain Admins** Security Group.
- *Why?:* Membership in Domain Admins grants full control over the domain. This ensures Jane can manage users, groups, and policies.
<p>
  <img width="1476" height="982" alt="image" src="https://github.com/user-attachments/assets/d5f1769f-a90a-4016-b4c5-de538bd4a83a" />
  <img width="742" height="976" alt="image" src="https://github.com/user-attachments/assets/a8b98e1c-a712-4a64-b7b9-7e475fd2e69a" />
  <img width="894" height="490" alt="image" src="https://github.com/user-attachments/assets/d38c6428-ae60-47d3-8047-1569e9f23a78" />
  <img width="744" height="972" alt="image" src="https://github.com/user-attachments/assets/f7b45539-6acd-4a8c-af40-1392adbcde57" />
</p>
5. Log out of DC-1 and Log back in as mydomain.com\jane_admin
<p>
  <img width="868" height="468" alt="image" src="https://github.com/user-attachments/assets/cf6b5e8f-4a7b-4654-aa37-a6acaa8c026e" />
</p>

## 3. Configure client-1 for the Domain
1. Log in to **client-1** as the **local admin (labuser)**.
2. Join client-1 to the domain:
- *Why?:* Joining the domain allows the computer to be centrally managed by the Domain Controller. Users can now log in using domain accounts.
- Go to **System → About → Advanced System Settings**
- In System Properties → Computer Name, click Change….
- Select Domain and enter the domain name: `mydomain.com`.
- Enter domain credentials (e.g., mydomain\jane_admin).
- Restart when prompted.
<p>
  <img width="470" height="371" alt="image" src="https://github.com/user-attachments/assets/d02ffd0c-6bc8-4979-ace2-2c4839d008f1" />
  <img width="640" height="735" alt="image" src="https://github.com/user-attachments/assets/b3eb60e3-cfe2-4291-974f-75a71954e61e" />
  <img width="632" height="774" alt="image" src="https://github.com/user-attachments/assets/9bc21a4d-eb74-4225-9124-ab52dfa7e42d" />
  <img width="896" height="716" alt="image" src="https://github.com/user-attachments/assets/eb1be846-50aa-404a-98a3-5261f016cadd" />
  <img width="590" height="298" alt="image" src="https://github.com/user-attachments/assets/198d9445-6cae-4a2a-908c-8fb50874dc3a" />
</p>
---

## 4. Verify Client-1 in Active Directory
1. Log back into the **Domain Controller (DC-1)** as `jane_admin`.
<p>
  <img width="508" height="488" alt="image" src="https://github.com/user-attachments/assets/697535ef-6e57-44f5-a12a-2284ee853c43" />
</p>
2. Open **ADUC** and confirm that **Client-1** appears under the Computers container.
- *Why?:* This verifies that the domain join worked correctly and that Client-1 is now registered in Active Directory.
<p>
  <img width="748" height="522" alt="image" src="https://github.com/user-attachments/assets/4d47ff8d-58da-4dbe-a583-cf2848f495d6" />
</p>
3. Create a new OU:
- `_CLIENTS`
<p>
  <img width="866" height="752" alt="image" src="https://github.com/user-attachments/assets/1812b896-9a93-4dfb-a731-17aa514cce79" />
</p>
4. Move **client-1** into the `_CLIENTS` OU.
- *Why?:* Organizing client computers into their own OU makes it easier to apply policies later.
<p>
  <img width="748" height="527" alt="image" src="https://github.com/user-attachments/assets/049bd1c8-d322-4ce0-9972-6492991acec8" />
</p>
---

### 5. Setup Remote Desktop for non-administrative users on Client-1

1. Log into client-1 as:
   mydomain.com\jane_admin
2. Open **System Properties → Remote Desktop**.
<p>
   <img width="1020" height="634" alt="image" src="https://github.com/user-attachments/assets/c5ed4727-d0b0-4da9-a2c8-a2b6f650240c" />
</p>
3. Allow access for:
- `Domain Users`
<p>
   <img width="750" height="660" alt="image" src="https://github.com/user-attachments/assets/bbdc8a84-99f4-413d-96bd-e9756c64e195" />
   <img width="906" height="502" alt="image" src="https://github.com/user-attachments/assets/47dbb35d-5f29-4bd5-8c63-aa5e0729c2b6" />
</p>

---

### 6. Bulk User Creation with PowerShell

1. On **dc-1**, log in as `jane_admin`.
2. Open **PowerShell ISE** as Administrator.
3. Paste this [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into a new file and run: 
<p>
   <img width="640" height="391" alt="image" src="https://github.com/user-attachments/assets/67533531-22c5-4d42-9c5e-7163e5a313f7" />
   <img width="640" height="393" alt="image" src="https://github.com/user-attachments/assets/9e76bd3d-c853-4ab0-acb3-637549e4b252" />
</p>
4. In ADUC, verify that new accounts are created in the _EMPLOYEES OU.
<p>
   <img width="716" height="836" alt="image" src="https://github.com/user-attachments/assets/452e8ddb-15c8-4f67-8507-96879433388b" />
</p>
5. Attempt to log into Client-1 with one of the new accounts.
<p>
   <img width="487" height="725" alt="image" src="https://github.com/user-attachments/assets/ce82d42c-bec0-4a90-ab1d-fcf45d6b4e4b" />
   <img width="420" height="66" alt="image" src="https://github.com/user-attachments/assets/97b025b7-53d2-4029-9e48-e10ddb3e791b" />
</p>
