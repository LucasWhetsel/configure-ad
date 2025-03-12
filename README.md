<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)



<h2>Deployment and Configuration Steps</h2>

First, we will create two virtual machines within the same virtual network. One will be a Domain Controller(dc-1), the other will be a Client machine(client-1). Second, we will set the Domain Controller's NIC private Ip address to be static. This means the Ip address will not change and will allow the client VM to use that private ip addresss also.  Client machine will be joined to the domain. We will control the DNS settings on the client machine, the client machine will use the DC as its DNS server.

![image](https://github.com/user-attachments/assets/902499d4-3164-4b2d-84b0-2e5ecfb5b7fe)

Next, we will connect to both virtual machines using remote desktop and attempt to ping the domain controller from the client machine. The ping was successful. Now type ipconfig /all so we can see if the client machine is using the domain controller's private ip, which it is (10.0.0.4).


![image](https://github.com/user-attachments/assets/aad56bfd-6a85-474a-b178-87650ce90322)

Now, we install active directory domain services to the DC-1 virtual machine using server manager. We will configure DC-1 to be our domain controller using mydomain.com. Next, we will create a domain admin user within the domain using active directory users and computers. We create a user jane_admin and add her as the domain admin. Next, we restart the VM and login using her credentials mydomain.com\jane_admin.

![image](https://github.com/user-attachments/assets/b5362473-6e06-41bc-8ef1-d33b426483a4)

We will add client 1 to the domain, mydomain.com. We can verify this by checking the computers on the domain controller. Add organizational unit _CLIENTS and add the client computer to that OU. 

![image](https://github.com/user-attachments/assets/52f83270-51dc-404d-a58a-a5f08b97a072)


