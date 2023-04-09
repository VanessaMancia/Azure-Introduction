![image](https://user-images.githubusercontent.com/109401839/230745596-57cee9bd-687c-427d-b0db-d1080df77f7e.png)

<h1>Azure Preparation </h1>

<h1/> We will create our Subcription and Resources, then go over Failed Authentication and Log Observation , and finally
Azure Active Directory Overview (Users, Groups, and Access Management)<h1/>

<h3>Environments and Technologies Used</h3>

- Microsoft Azure

<h3>Operating Systems Used </h3>

- VM Windows 10 (21H2)

---

<h2> Subscriptions and Resources<h2>

<h3>Actions and Observations</h3>

- Create Windows 10 Pro Virtual Machine
- Name the Resource Group: RG-Cyber-Lab

![gtxtw3z5](https://user-images.githubusercontent.com/109401839/230747447-40c9b360-38e2-4d8d-b4b2-7ea0bb12ae0f.png)

- Name the Virtual Network. NAME IT “Lab-VNet”

![hjl0rzkf](https://user-images.githubusercontent.com/109401839/230747449-be2118b3-a451-4d32-a756-d4082055ae31.png)

Now, double check the VM settings and create ! 

![image](https://user-images.githubusercontent.com/109401839/230747537-211a32a7-9525-4572-a455-0a250278c604.png)

- Configure Network Security Group (Layer 4 Firewall) to allow all traffic inbound
- Install SQL Server and Create Vulnerabilities
- Remote Into the VM
- Turn off Windows Firewall
- Install SQL Server Evaluation
- Install SSMS (SQL Server Management Studio)
- Enable logging for SQL Server to be ported into Windows Event Viewer 
- Test SQL logging to make sure it’s working properly


---

<h2/>Precursor to Security Operations (Failed Authentication and Log Observation)<h2/>
  
<h3>Actions and Observations</h3>

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

<h2/>Azure Active Directory Overview (Users, Groups, and Access Management)<h2/>

![Untitled](https://user-images.githubusercontent.com/109401839/230747442-f0a1831d-1cf0-4895-b335-372314cd5d51.png)


<h3>Actions and Observations</h3>

- Configure and Observe Tenant-Level Global Reader
- Create a user within Azure Active Directory (AAD) (username: globalreaderjohn)
- Assign Tenant-Level Global Reader
- In a new browser/incognito, log in as globalreaderjohn and observe result of being a Tenant Level “Global Reader”
- Close browser/incognito when satisfied

- Configure and Observer Subscription Reader
- Back in main browser, create another user within AAD  (username: subreaderjane)
- Assign Subscription-Level Reader 
- In a new browser/incognito, log in as subreaderjane and observe result of being a Subscription Level “Global Reader”
- Close browser/incognito when satisfied

- Configure and Observe Resource Group Contributor (like an admin)
- Back in main browser, create another user within AAD  (username: rgcontributordave)
- Create a new resource group called “Permissions-Tester”
- Assign Resource Group-level Contributor
- For our resource group (RG-Cyber-Lab), assign Contributor Permissions
- In a new browser/incognito, log in as rgcontributordave and observe result of being a Subscription Level Reader
- Observe the result of being a Resource Group Level Contributor


  *Welcome to Cybersecurity* your journey starts here! 

