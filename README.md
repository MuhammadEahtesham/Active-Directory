# Active-Directory

## Description

### What is Active Directory ?

Active Directory is a directory service developed by Microsoft for managing and organizing resources within a networked environment. It is commonly used in Windows-based networks to centralize and control network resources, such as user accounts, computers, printers, and security policies.

### What is a Group Policy Objects (GPO)

A collection of Group Policy settings that defines what a system will look like and how it will behave for a defined group of users.

## Step-by-Step Guide

### 📒 Chapter 1 - Active Directory

Install virtual box and ISOs for given links:
VirtualBox : https://www.virtualbox.org/wiki/Downloads

Windows Server 2019 💿 : http://www.microsoft.com/en-us/evalcenter/download-windows-server-2019

Windows 10 💿 : https://www.microsoft.com/en-us/software-download/windows10

### 🌐 Installing & Configuring the virtual environment for Windows Server 2019

- Setting Up the Virtual Environment
   +This is for Windows Server 2019, all the things by defualt. Just change :
  Version to : Other Windows 64 bit,
  Network to : Add another adopter with defualt and change to internal network, &
  Choose Windows 10 standard (User Desktop Experience) & Custom Setting, when installing it.
  Its time for a coffee break ☕️

### ⚙️ Configuring Windows Server 2019

- Open Windows Server 2019, and it seeems to be flow over the brain but it is not, believe me.

 + Open the the network connection window, and change the Ethernet names for ease like:
        Path: Ethernet -> Properties -> Details
        Ethernet having home ip address like 10.?.?.? or 192.?.?.? --> Rename it to "Internet"
        Ethernet having loop back ip address like 162.?.?.? or 127.?.?.? --> Rename it to "Internal"

  Assign IPs now to the Ethernet: For Internal --
        Change IP to 172.16.0.1, mask to 255.255.255.0 & DNS to 127.0.0.1" (loopback as this server act as DNS also).

  Now change the Server name to your choice but remember it.
        Path will be Settings -> About -> Rename this PC

- Now, its time to add services on the Windows Server. 🔥

  🎯 Central/Main Path --- Server Manager -> Add Roles & Features
        
  + ### _Adding Active Directory Domain Service_

    Choose next until select service : Choose Active Directory Domain Service and then Finish.

    Wait for few minutes until its done and close the windows.

    You will see a flag with yellow object at top right corner click it & choose Post Deployment Config.
    Choose the option:

    **Add new forest & add domain name you want. <domain_name.com>**

    Write password & finish it.
    Machine will restart. Give Password you wrote in domain section.

    Now make your own admin account on Domain server you create.
    Path --- Start Menu -> AD Users & Computers

    ➡️🖱️ Domain Name & select New -> Organizational Unit
    Name this as ADC-01

    ➡️🖱️ Domain Name & select New -> Users
    Fill it as you want but uncheck 1 option & check 3 option.

    ➡️🖱️ Admin Name & select Properties -> Members Of -> Add
    Fill the blank portion with: Domain Admins
    Log out and sign as other user that you created as Domain Admin.....

    + ### _Adding NAT to connect to Internet_
      Choose next until select service : Choose Remote Access -> Next -> Routing and then Finish.
      Wait for few minutes until its done and close the windows.

      You will see Tools option at top right corner, click Routing & Remote Access.
      ➡️🖱️ Domain (local) & select Configure & Enable Routing
Choose NAT option -> then, choose public interface option and Finish.
      Green color appears.

    + ### _Adding DHCP Service_
      Choose next until select service : Choose DHCP Server then Finish.
      Wait for few minutes until its done and close the windows.

      You will see Tools option at top right corner, click DHCP .
        Drop down your domain name, then IPv4
        ➡️🖱️ IPv4 & select New Scope
        -------- Now, fill name and fill up fields:
        -------------- Start IP : 172.16.0.100
        -------------- End IP : 172.16.0.200
        -------------- Length : 24
        -------------- Mask : 255.255.255.0
        -------------- Go until when add router IP : 172.16.0.1 (our DNS IP) and ADD
        -------------- Finish & Refresh

        <Extra : Click to Local Server Configuration -> IE Enhance Security Configuration to OFF>

  - Furthermore, we should add some users.

    Path --- Windows Start -> Active Directory -> Add Users & Computers
    --- ➡️🖱️ Domain Name & select New -> Organizational Unit
    Name this as USERS

    --- ➡️🖱️ USERS & select New -> Users
    Fill it as you want but uncheck 1 option & check 3 option.

### 🌐 Installing & Configuring the virtual environment for Windows 10

  - Setting Up the Virtual Environment
        This is for Windows 10, all the things by defualt. Just change :
        Version to : Windows 64-bit,
        Network to : Change to internal network (to get IP from DHCP), &
        Choose Windows 10 PRO & Custom Setting, when installing it.
        Its time for a coffee break ☕️

### ⚙️ Configuring Windows Server 2019

   - Check for these things in Client PC:-
        + ipconfig (should be in scope)
        + try to ping

  - Connect the Client PC to the Domain you created
    Path:- System -> About -> Rename this PC (Advanced) -> Change

    + Name the PC,

    + Check the option with domain and write tour domain such as mydomain.com

     +  Username & Password you created in the domain server

  ```
  
  ********* TO CONFIRM, GO TO DOMAIN SERVER & CHECK ADDRESS LEASES ********
  ```
  
 - Login as other user with username and password and it will be done.

### 📒 Chapter 2 - Group Policy Management


# THE END
