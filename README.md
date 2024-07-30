<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>








- Azure Virtual Machine Install 

- Internet Information Services (IIS)           
- PHP Manager
  
- Rewrite Module
- VC Redist
- MySQL
- Heidi SQL
- osTicket v1.15.8

  ______________________________________________________________________________________________________________________
<h2>Installation Steps</h2>


  ______________________________________________________________________________________________________________________

1.) The first thing you are going to want to do is create a virtual machine by going to https://portal.azure.com/. Setup your virtual machine with Windows 10 Pro, version 22H2. Note, you will want to create a virtual machine with atleast 2 vcpus and 16 gbs of memory.

2.) Once you have created your virtual machine you will want to conncet to it by using the public ip address the vm is setup with. You will connect using the remote desktop connection app.




![image](https://github.com/user-attachments/assets/dce79b6e-c1cf-4c5b-916b-3fd5a1f6d234)


![image](https://github.com/user-attachments/assets/00133656-8e6a-4339-a4c1-72d734797bde)

3.) Once you have connected to your virtual machine you will want to go to your control panel. From the control panel open up programs. Select, Turn Windows features on and off.


![image](https://github.com/user-attachments/assets/c54ed961-6722-45d0-865a-3791017e3fb4)

![image](https://github.com/user-attachments/assets/39a79c54-54d9-41b6-b153-29dfdfd0aed5)

4.) You will want to install / enable IIS in Windows with CGI and Common HTTP Features

   - World Wide Web Services -> Application Development Features -> [X] CGI [X] Common HTTP Features


![image](https://github.com/user-attachments/assets/f4886607-4b69-4fa6-92e8-2f57b1536d8c)


![image](https://github.com/user-attachments/assets/9a3588ad-c823-4196-8aa8-7894826472c0)


NOTE: Make sure all Common HTTP Features are checked.

To make sure the IIS is installed / enabled go to a browser of your choice and search for 127.0.0.1 It should look something like this.

![Screenshot 2024-07-30 163342](https://github.com/user-attachments/assets/4d164f98-7749-403f-996b-bf689b802621)




5.) Now that the IIS is enabled, From the Installation Files, download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi) Go through the install wizard and complete the install.

6.) Next from the Installation Files, download and install the Rewrite Module (rewrite_amd64_en-US.msi)

7.) Create a folder in the C drive called PHP.

8.) From the Installation Files, download PHP 7.3.8 (php-7.3.88-nts-Win32-VC15-x866.zip) and unzip the contents into C:\PHP

!! ATTENTION !! If this appears, choose to “Keep” the file:



![image](https://github.com/user-attachments/assets/38a51484-10e6-4b3a-94d7-de45681259b2)

![image](https://github.com/user-attachments/assets/03f6ef17-52eb-4296-a787-81be1ac005a0)

9.) Once you have downloaded and extracted the zip file into the PHP folder on the C drive, download and install the VC_redist.x86.exe from the installation files. Go through the setup wizard to finish setting up and installing the VC_redist.x86.exe.

10.) Download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi) Run the setup wizard: Typical Setup -> Launch Configuration Wizard (after install) -> Standard Configuration ->

Make the new root password: Password1


![image](https://github.com/user-attachments/assets/c2da8602-99f0-4905-8b20-8f55c6a26fea)


Execute the process on the next page.


![image](https://github.com/user-attachments/assets/893f0d29-e9d4-4cd8-997f-24df55ca12dd)



11.) Now that we have the files downloaded and installed we will want to search for IIS in the windows search bar. Open IIS as an administrator. The program should look like this.


![image](https://github.com/user-attachments/assets/8526661c-cff4-4f0c-b471-8e32b7f16d15)

12.) We will now want to register PHP from within IIS. Click on PHP Manager


![image](https://github.com/user-attachments/assets/2d931584-2212-4a10-8322-efb7831b4ea9)


Register new PHP version.

![image](https://github.com/user-attachments/assets/0c7b7f80-b046-4f4f-8256-69513f528c5a)


You will want to provide a path to the php executable file (php-cgi.exe)). Go to C Drive -> PHP -> click on php-cgi file.


![image](https://github.com/user-attachments/assets/433ef65a-b108-42f2-b9e2-e4ab177120ec)

Restart the IIS server.


![image](https://github.com/user-attachments/assets/35a6b7ac-c4e3-41ca-a85e-d87e60991a45)


13.) Install osTicket v1.15.8 -Download osTicket from the Installation Files Folder -Extract and copy "upload" folder to c:\inetpub\wwwroot -Within c:\inetpub\root, Rename "upload" to "osTicket"

Reload IIS again.

14.) On IIS go to sites -> Default -> osTicket -On the right, click “Browse *:80”

![image](https://github.com/user-attachments/assets/9df10a95-3e0c-42ba-b2fd-243a87f31cb5)

Some extensions are not enabled on the osTicket browser.

![image](https://github.com/user-attachments/assets/f1c08326-824c-4d5e-b570-e1551bd80382)

To enable the extensions: -Go back to IIS, sites -> Default -> osTicket -Double click PHP manager -Click "Enable or disable an extension"

![image](https://github.com/user-attachments/assets/2c4e0c19-c226-43e5-8c83-16fb502317a2)


![image](https://github.com/user-attachments/assets/c64cb3de-abce-411d-8912-f69355de57c8)


We will want to enable three extensions from here.

1.) php_imap.dll

2.) php_intl.dll

3.) php_opcache.dll

![image](https://github.com/user-attachments/assets/8a10c332-bbbc-4302-affe-fed835d41372)


15.) Once we have those extensions enabled in IIS, we are going to want to rename one of the files in our osTicket folder. Go into the file explorer and search for C;\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php

We are going to rename the ost-sampleconfig.php to ost-config.php

Now that we have renamed the files, right click on the file and go to properties. From there click security, click on advance, and disable the inheritance. We will select Remove all inherited permissions from this object.

Now we will add new permissions.

Click Add

![image](https://github.com/user-attachments/assets/d3299f6b-ef9c-4f59-a61b-a2846807b147)

Select a principal

![image](https://github.com/user-attachments/assets/908d747a-baa7-42de-a425-b32b12f0689c)

Type "Everyone" in the box.

![image](https://github.com/user-attachments/assets/8db49fe8-12bf-46ce-a0e8-0daa9bbd3a1f)

Make sure Full Control and all the other boxes are checked.

![image](https://github.com/user-attachments/assets/c6c505ef-d8cd-4961-b48c-be753be31438)

Click Apply and Ok.

![image](https://github.com/user-attachments/assets/35a0bcbb-bbef-430f-9187-2bbd8d33e8f3)

Once that is done we will continue to setup osTicket in the browser. Click Continue on the osTicket browser page. Fill out the page as required except the Database Settings at the bottom of the page. We will get to that.

We will want to download and install HeidiSQL from the Installation Files.


![image](https://github.com/user-attachments/assets/4812cba8-1fee-4bd6-9ee4-599cb637c47b)

When the program is open we will create a new session in it.


![image](https://github.com/user-attachments/assets/91a42d0c-f4f2-4fa4-a54d-f046f05959dc)

We want to make sure the username is root and the password is Password1.
![image](https://github.com/user-attachments/assets/963eef98-56cf-4bf5-9648-bae6295c35fa)

Once we are connected to the session we will go back to the browser to finish setting everything up. Under the Database Settings in the browser the username will be root and the password will be Password1.

We will now create a new database within HeidiSQL. In Heidi right click on the left side where is says "Unnamed", select "create new", and then select "database". Name the new database osTicket. Once we have the new database setup go back to the osTicket browser and under MySQL Database type in osTicket.

![image](https://github.com/user-attachments/assets/f933f359-5ae1-46f1-9f67-3daa192dbbcf)

The last step is to do some clean up. We will want to delete the setup folder in our system. -Delete: C:\inetpub\wwwroot\osTicket\setup Only delete the setup folder and nothing else.

We then will want to set the permissions back to "Read" only in the ost-config.php file.

![image](https://github.com/user-attachments/assets/a55bc9b3-da61-4b4d-a63c-65b3852843db)


![image](https://github.com/user-attachments/assets/72f11805-e765-4265-8240-e1147294f353)


The last step after that is to login to osTicket on the browser.


![image](https://github.com/user-attachments/assets/47ec67f4-e295-4d1b-af7b-c6d21a03c2f8)
















