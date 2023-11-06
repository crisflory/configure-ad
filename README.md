Simplified List provides a concise overview of the necessary steps to complete this laboratory assignment. If you wish to assess your "Technical Proficiency" in alignment with the 12 Pillars of Employment (your 12 performance metrics), I suggest reaching a point where you can execute the labs using only the simplified instructions.

Set up Resources in Azure.

Create a Domain Controller VM (Windows Server 2022) with the name "DC-1."

Make a note of the Resource Group and Virtual Network (Vnet) created during this step.

Configure the Domain Controller's NIC Private IP address to be static.
![image](https://github.com/crisflory/configure-ad/assets/147748310/6d67a004-c6f9-4aad-a214-0b4122b74c68)


Create the Client VM (Windows 10) named "Client-1" using the same Resource Group and Vnet as in Step 1.b.

Ensure that both VMs are within the same Vnet, which can be verified using Network Watcher.
Establish Connectivity between the client and the Domain Controller.

Log in to Client-1 using Remote Desktop and continuously ping DC-1's private IP address using the command: ping -t <ip address>
![image](https://github.com/crisflory/configure-ad/assets/147748310/4dd25fe7-9e0d-4adf-bd42-3029348b6063)

On the Domain Controller, enable ICMPv4 in the local Windows Firewall.
![image](https://github.com/crisflory/configure-ad/assets/147748310/bb73e342-1c47-4167-a027-eedb479da4a4)


Confirm successful ping from Client-1.
![image](https://github.com/crisflory/configure-ad/assets/147748310/acb20431-cf02-4685-9f13-f757d892771e)
Install Active Directory.

Log in to DC-1 and install Active Directory Domain Services.
![image](https://github.com/crisflory/configure-ad/assets/147748310/16734e42-9002-465b-8ece-63ede765990a)

Promote it as a Domain Controller, setting up a new forest, e.g., "mydomain.com" (you can choose any name).
![image](https://github.com/crisflory/configure-ad/assets/147748310/32c2d588-5a73-4cdf-9fd7-df4d6423fb66)

Restart and log back into DC-1 as the user "mydomain.com\labuser."


Create an Administrator and Normal User Account in AD.

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) named "_EMPLOYEES."
![image](https://github.com/crisflory/configure-ad/assets/147748310/d366d46f-ebae-463b-9861-5805f688d0ae)

Create another OU called "_ADMINS."
Create a new employee named "Jane Doe" (using the same password) with the username "jane_admin."
![image](https://github.com/crisflory/configure-ad/assets/147748310/ad4679b5-cd20-4609-81b4-eee32f1a52ef)


Add "jane_admin" to the "Domain Admins" Security Group.
Log out of the Remote Desktop connection to DC-1 and log back in as "mydomain.com\jane_admin."
Use "jane_admin" as your admin account from this point forward.
Join Client-1 to your domain (mydomain.com).

From the Azure Portal, configure Client-1's DNS settings to use the DC's Private IP address.
![image](https://github.com/crisflory/configure-ad/assets/147748310/4689af31-7f4f-4eb7-9bef-570f886a0d98)

Restart Client-1 from the Azure Portal.
![image](https://github.com/crisflory/configure-ad/assets/147748310/8afc5ac4-e009-4b20-841e-3d2ea50dc0da)

Log in to Client-1 (Remote Desktop) as the original local admin ("labuser") and join it to the domain (the computer will restart).
Log in to the Domain Controller (Remote Desktop) and confirm that Client-1 appears in Active Directory Users and Computers (ADUC) within the "Computers" container in the root of the domain.

Log in to Client-1 as "mydomain.com\jane_admin" and access system properties.

Click on "Remote Desktop" and grant "domain users" access to remote desktop, allowing normal, non-administrative user access.
![image](https://github.com/crisflory/configure-ad/assets/147748310/96f647c8-0a15-4956-a046-cf4d528a0d86)

Create multiple additional users and attempt to log into Client-1 with one of these new accounts.

Log in to DC-1 as "jane_admin."

Open PowerShell_ise as an administrator.

Create a new file and paste the contents of the script from this URL (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1).
Run the script and observe the new accounts being created.

![image](https://github.com/crisflory/configure-ad/assets/147748310/14997951-5d2a-4ab0-a0aa-81c30889d746)

After completion, check ADUC to verify the accounts are in the appropriate OU.
![image](https://github.com/crisflory/configure-ad/assets/147748310/dbc5f8a6-8661-4006-8b3e-dd47356b7c55)

Attempt to log into Client-1 using one of the newly created accounts (note the password from the script).
![image](https://github.com/crisflory/configure-ad/assets/147748310/4c326b2f-4c3e-43e6-ba18-e2620929688c)

Finish.
