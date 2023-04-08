![image](https://user-images.githubusercontent.com/109401839/230745596-57cee9bd-687c-427d-b0db-d1080df77f7e.png)

<h1>Azure Preparation </h1>
<b/> We will create our **Subcription and Resources** , then go over **Failed Authentication and Log Observation** , and finally
**Azure Active Directory Overview (Users, Groups, and Access Management)** <br />

---

<h2> Subscriptions and Resources<h2>

<h3>Environments and Technologies Used</h3>

- Microsoft Azure

<h3>Operating Systems Used </h3>

- VM Windows 10 (21H2)

<h3>Actions and Observations</h3>

- Create Windows 10 Pro Virtual Machine
- Name the Resource Group: RG-Cyber-Lab
- Name the Virtual Network. NAME IT “Lab-VNet”
- Configure Network Security Group (Layer 4 Firewall) to allow all traffic inbound
- Install SQL Server and Create Vulnerabilities
- Remote Into the VM
- Turn off Windows Firewall
- Install SQL Server Evaluation
- Install SSMS (SQL Server Management Studio)
- Enable logging for SQL Server to be ported into Windows Event Viewer 
- Test SQL logging to make sure it’s working properly



---
  
<H2>Precursor to Security Operations (Failed Authentication and Log Observation)<H2>
  
- Admin Mode (pretend you are normal admin):
- Create another Windows VM in a region outside the US and NAME IT “attack-vm”
- Name the Resource Group RG-Cyber-Lab-Attacker
- Name the VNet Lab-VNet-Attacker
- Log into the VM to make sure it works
- Retrieve the public IP address of “windows-vm” from the Azure Portal, save it for the next steps

- Attacker Mode (pretend you are an attacker):
- Generated some failed RDP logs against “windows-vm”
- From within of “attack-vm”, attempt to RDP into “windows-vm” with the wrong credentials
- Repeat this step 5 times with the wrong username and password
- Finally, from “attack-vm”, actually log into “windows-vm” with the correct username and password.
- Generated some failed MS SQL Auth logs against “windows-vm”
- Still within “attack-vm”, install SSMS if not already installed
- Attempt to connect to the SQL Server on “windows-vm” with a bad password
- Log out of “attack-vm”, now you are back to your own computer

- Admin Mode (pretend you are normal admin):
- From your own computer, RDP back into “windows-vm”
- Inspect the failures and successes (Security Log for RDP, Application Log for SQL)
- Take note of the EventIDs, messaging, Source IP Addresses, etc.

  ---
  
  *Welcome to Cybersecurity* your journey starts here! 

