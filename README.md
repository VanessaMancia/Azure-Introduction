![image](https://user-images.githubusercontent.com/109401839/230745596-57cee9bd-687c-427d-b0db-d1080df77f7e.png)

<h1>Azure Preparation </h1>

<h1/> We will create our Subcription and Resources, then go over Failed Authentication and Log Observation , and finally
Azure Active Directory Overview (Users, Groups, and Access Management)<h1/>

<h3>Environments and Technologies Used</h3>

- Microsoft Azure

<h3>Operating Systems Used </h3>

- VM Windows 10 (21H2)

<div>
<h2>Resources & SQL Server Vulnerabilties<h2>
<details close>

---

</summary>
<h3>Actions and Observations</h3>

- ```Create Windows 10 Pro Virtual Machine```
- Name the Resource Group: RG-Cyber-Lab

![gtxtw3z5](https://user-images.githubusercontent.com/109401839/230747447-40c9b360-38e2-4d8d-b4b2-7ea0bb12ae0f.png)

- Name the Virtual Network. NAME IT “Lab-VNet”

![hjl0rzkf](https://user-images.githubusercontent.com/109401839/230747449-be2118b3-a451-4d32-a756-d4082055ae31.png)

Now, double check the VM settings and create ! 

![image](https://user-images.githubusercontent.com/109401839/230747537-211a32a7-9525-4572-a455-0a250278c604.png)

- Configure Network Security Group (Layer 4 Firewall) to allow all traffic inbound

A mini firewall that will be configured for our virutal machine to allow all traffic in. We want to make this firewall look enticing to allow threat actors such as hackers, bots , and attackers to try to get into our virtual machine. 

In resource groups, we will go inside it, we can see all the things associated with the VM being created. 
We will edit, the network security group, either by search or in the resource groups. 
Based on the traffic coming into the network we can see the priorty categorised in Azzure based on the set rules/protocols. 
Create Inbound Security Rule , Any, Name it "DangerAllInBound" 

![nsg danger inbound](https://user-images.githubusercontent.com/109401839/230748062-20cb8a7d-768c-4d8b-b548-dad98fdef095.png)

Now try to ping the IP Address of the VM in CMD...
Did it work? 

![ping](https://i.imgur.com/ZnVQuDB.png)

No it didnt because we need to remote in, and change the firewall setting within the VM as well. 

- Remote Into the VM

Now remote in, on Windows 10 we will use  "Remote Desktop Connection" 

![e](https://i.imgur.com/8RQ9xpu.png)

- Turn off Windows Firewall
 
Once you are logged in, search "wf.msc" in the start menu to execute the program "Windows Defender Firewall Advanced Security.
Click on "Windows Defender Firewall Properties" 
On each tab, turn off the "Firewall State" 
Ignore IPSEC Settings for now.

![3](https://i.imgur.com/pBzKoId.png)

Now observe the changes in CMD: 

![image](https://user-images.githubusercontent.com/109401839/230748490-8588cf7e-e3b4-4739-befd-f4695ba665ce.png)


- Install SQL Server Evaluation

[Download here](https://www.microsoft.com/en-us/evalcenter/download-sql-server-2022)

Install .exe file, Download Media, ISO option, Open Folder, and Mount Media

It will show as a disk file under "This PC" side panel: 

![image](https://user-images.githubusercontent.com/109401839/230748771-4fd4e778-626d-4baa-8403-b1acf1389bdb.png)

![image](https://user-images.githubusercontent.com/109401839/230748852-edba2194-ebb1-4e15-932f-243d6cce6fac.png)

- Install SSMS (SQL Server Management Studio)

![sql install](https://user-images.githubusercontent.com/109401839/230748997-ad8f84d1-9bf7-4125-b7e5-0cd2f490b62b.png)

![mstsc_Kc9i9HCW3n](https://user-images.githubusercontent.com/109401839/230749050-cdeedde3-6773-48a1-852b-415ea114cfc6.png)

![mstsc_sGtz3qU3M2](https://user-images.githubusercontent.com/109401839/230749062-0bd9eaeb-9c0d-43c2-93a5-c9641bf2285e.png)

''' Select "Mixed Mode", this is important becayse with Windows Authentication Mode, we will only be able to login with an online acount, where as with a mixed mode, we can login online and locally into the SQL Server. '''

Add current user, and enter your password. 

Now Finish Install ! Now we can connect to our SQL Database.  

Next we will download [Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16)

![image](https://user-images.githubusercontent.com/109401839/230749437-dfc8f934-0360-4bc8-949f-a99371c0ba40.png)

![image](https://user-images.githubusercontent.com/109401839/230749591-15fffab9-3651-418b-8694-bd763492a9fb.png)


[Configure](https://learn.microsoft.com/en-us/sql/relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log?view=sql-server-ver16) the audit object access setting in Windows using auditpol

- Enable logging for SQL Server to be ported into Windows Event Viewer 

Open a command prompt with administrative permissions.

From the Start menu, navigate to Command Prompt, and then select Run as administrator.

If the User Account Control dialog box opens, select Continue.

Execute the following statement to enable auditing from SQL Server.

Windows Command Prompt

Copy
'''auditpol /set /subcategory:"application generated" /success:enable /failure:enable'''
Close the command prompt window.

![2](https://i.imgur.com/LCjKjIg.png)

Now RegEdit and explore:
 ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\EventLog\Security```

![image](https://user-images.githubusercontent.com/109401839/230749756-e9139c85-9cd7-4756-a400-307b02a4c81a.png)

Restart SQL Management, Disconnect Connection, Reconnect, and Choose SQL Managements Authentication Method. 

Now, Intentionally enter the wrong user name and password to do a failed login attempt. 

![image](https://user-images.githubusercontent.com/109401839/230749821-c108d8bb-e77e-4826-9b93-0a6f2afde4f4.png)

- Test SQL logging to make sure it’s working properly

Enter Event Viewer, Select Application, and View SQL Management Logs Entries: 

![image](https://user-images.githubusercontent.com/109401839/230749908-b20fe934-00b7-498a-a8f6-1f9554e38aed.png)

Here we can see the failed login attempt and the reason. That concludes the first lab. 


<div>
<h2/>Precursor to Security Operations (Failed Authentication and Log Observation)<h2/>
<details close>

---

</summary>
We will create a VM in the cloud that will be our target of attack, and we will observe logs and see what they look like. 
The ultimate goal of this lab is to differentiate between false negatives, false positives, true positives, and true negatives. 
  
<h3>Actions and Observations</h3>

We are creating an attack vm the goal is to have a different region so it looks like a threat is attacking our previous vm. 

![OUTSIDE](https://user-images.githubusercontent.com/112146207/230785143-b12ea9d9-8f3d-4fca-a73b-3d54374c3611.png)


```Now we have to name the VNet Lab-VNet-Attacker```

![image](https://user-images.githubusercontent.com/112146207/230785775-a4c5d027-71cd-4341-8927-faa552ff0cd4.png)

First thing we will do is get the attack-VM public IP adddress. Then go to remote desktop connection and enter in your attack VM information. 

![image](https://user-images.githubusercontent.com/112146207/230786468-787b9479-4b0b-42b4-beb0-f627f6c02125.png)

- Get the windows-vm ```public IP address```` and go to RDP and from there go to the start menu and search remote desktop and enter the ``` IP address ```. 
- We will now generate some failed RDP (remote desktop protocol) logs against the windows-vm from the attacker vm. 
- We will attempt this 5 times with the wrong username and password.

![image](https://user-images.githubusercontent.com/112146207/230787466-11cc67e0-4833-4a61-a7b3-f6d250abf75e.png)

We then go to event viewer and see all the failed login attempts

![image](https://user-images.githubusercontent.com/112146207/230790854-d6bd81a6-4629-4a4d-ab39-681c7b013451.png)


- Finally, from “attack-vm”, actually log into “windows-vm” with the correct username and password.


- Generated some failed MS SQL Auth logs against “windows-vm”
- Still within “attack-vm”, install SSMS if not already installed
- Attempt to connect to the SQL Server on “windows-vm” with a bad password
- Log out of “attack-vm”, now you are back to your own computer

- Admin Mode (pretend you are normal admin):
- From your own computer, RDP back into “windows-vm”
- Inspect the failures and successes (Security Log for RDP, Application Log for SQL)
- Take note of the EventIDs, messaging, Source IP Addresses, etc.

<div>
<h2/>Azure Active Directory Overview (Users, Groups, and Access Management)<h2/>
<details close>

---

</summary>
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


  *Welcome to Cybersecurity*, your journey starts here! 
On our next set of [labs](https://github.com/fnabeel/Logging-and-Monitoring), we woll go over Logging and Monitoring. 

