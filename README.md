<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (22H2)

<h2>List of Prerequisites</h2>
<ol>
  <li>Set up an Azure Virtual Machine (VM) environment (Windows 10 4 vCPUs Recommended)</li>
  <li><a href = "https://drive.google.com/drive/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">osTicket Installation Files</a> (Download these files on your Azure Virtual Machine) </li>
  <li>Enable IIS in I.S.S.</li>
  <li>Install Web Platform Installer</li>
  <li>Install MySQL and set up username and password</li>
    <ul>
    <li>For this tutorial, we will set up our username and password as such:</li>
      <ul>
      <li>username: root</li>
      <li>password: Password1</li>
      </ul>
    </ul>
  <li>Install C++ Redistributable</li>
  <li>Configure permissions and install osTicket</li>
</ol>

<h2>Installation Steps</h2>

<p>
  <ul>
    <li>In the VM, go to the <b>Control Panel</b> and head to <b>Programs</b></li>
    <li>Under <b>Program and Features</b> click on <b>Turn Windows features on or off</b></li>
    <li>Navigate the list and check the box for <b>Internet Information Services</b></li>
    <li>Expand the list for <b>Internet Information Services</b>, navigate to <b>World Wide Web Services</b> then expand that to find <b>Application Development Features</b>, expand that and check the box for <b>CGI</b></li>
    <li>Before closing, make sure the boxes under <b>Common HTTP Features</b> in World Wide Web Services are checked.</li>
      <ul>
        <li><b>Check these boxes in Turn Windows Features on or off</b></li>
        <br>
        <img <img width="500" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/7322d2a2-db72-4f76-a438-d3c5e860f178">
        </br>
      </ul>
    <li>To confirm everything is set correctly, go to your browser in your VM and type in <b>127.0.0.1</b>, it should load the page to Internet Information Services</li>
      <ul>
        <br>
        <img width="800" alt="ISS 127 0 0 1 Screenshot" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/3a351e96-d63a-44cc-a27c-224ed7e0cbb9">
        </br>
      </ul>
  </ul>
</p>

<br />

<h3>Installing Files for osTicket</h3>

<p>
  <ul>
    <li><b>NOTE:</b> Depending on your VM CPU and Google Drive's virus scanning system, downloads will be rather <i>slow</i></li>
    <li>From the Installation Files, download <b>PHP Manager</b> (PHPManagerForIIS_V1.5.0.msi) and <b>Rewrite Module</b> (rewrite_amd64_en-US.msi) </li>
    <li>Create a Folder in your VM's C Drive and name it <b>PHP</b></li>
      <br>
      <img width="800" alt="Creating PHP File in C Drive" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/e4502cf1-aaaf-4569-8a4d-ee6b5a016420">
      </br>
    <li>From the Installation Files, download the zip file <b>PHP 7.3.8</b> (php-7.3.8-nts-Win32-VC15-x86.zip) then unzip the contents into the PHP folder we've made (C:\ PHP)</li>
      <ul>
        <li><b>NOTE:</b> If a warning sign appears in the downloading icon in your browser, it means the Microsoft Defender Smartscreen in your VM is preventing you from downloading the zip file. If this happens, navigate to the file in your downloads and click on <b>Keep</b></li>
      <br>
      <img width="400" alt="PHP Troubleshoot" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/7e18421d-38f9-402f-8826-1000e280767f">
      </br>
      </ul>
    <li>From the Installation Files, download and install <b>VC_redist.x86.exe</b></li>
    <li>From the Installation Files, download and install <b>MySQL 5.5.62</b> (mysql-5.5.62-win32.msi)</li>
      <ul>
        <li>After installing, launch the <b>Configuration Wizard</b></li>
        <li>Check <b>Install As Window Service</b>, for this tutorial our Service Name will stay as <b>MySQL</b></li>
        <li>Check <b>Modify Security Settings</b> and for this tutorial we'll set the password as <b>Password1</b></li>
      </ul>
  </ul>
</p>

<br />

<h3>Setting up IIS and PHP</h3>

<p>
  <ul>
    <li>Open <b>Internet Information Services (IIS) Manager</b> and run it as Administrator</li>
    <ul>
      <li><b>PHP Manager</b> and <b>URL Rewrite</b> should be found in our IIS Manager due to the PHP Manager and Rewrite Modules files we have downloaded initially </li>
      <br>
      <img width="800" alt="PHP Manager   Rewrite" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/c8cd4f16-85ab-4669-ac93-a05d1bfcae78">
      </br>
    </ul>
    <li>Go to <b>PHP Manager</b> and click on <b>Register new PHP Version</b>, set the directory to the <b>php-cgi</b> file found in the PHP folder we've set in C Drive (C:\PHP)</li>
      <br>
      <img width="834" alt="PHP-CGI" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/b7383cee-423b-4599-9dfc-79e6b66e65c9">
      </br>
    <li>Optional but Recommened: Refresh the IIS Manager Server by going to <b>Actions</b> and under <b>Manage Server</b> click on <b>Restart</b></li>
  </ul>
</p>

<br />

<h3>Installing osTicket</h3>

<p>
  <ul>
    <li>From the Installation Files, download and install <b>osTicket v1.15.8.zip</b></li>
    <li>Extract the <b>upload</b> folder from the zip file and copy the folder into the directory <b>C:\inetpub\wwwroot</b> in your VM</li>
      <br>
      <img width="1000" alt="Upload to inetpub folder" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/37c0233b-f289-4231-9cbf-8cdfea88ee55">
      </br>
    <li>Rename the upload folder we've copied into wwwroot to <b>osTicket</b>, then reload IIS Manager</li>
    <li>In IIS Manager, expand the connection <b>Sites</b> then <b>Default Web Site</b> to click and highlight <b>osTicket</b>. Then, navigate to <b>Browse Folder</b> and click on <b>Browser*.80 (http)</b></li>
    <li>The page for osTicket Installer should now pop up, if it does not, check your directories of your files and folders</li>
      <br>
      <img width="700" alt="osTicket Install Page" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/76a10475-5a45-4e83-bbbb-e0c7b5ceb1c5">
      </br>
    <li>In IIS Manager, go to <b>osTicket</b> and click on <b>PHP Manager</b> and click on <b>Enable or disable extensions</b> and enable the following extensions</li>
      <ul>
        <li>php_imap.dll</li>
        <li>php_intl.dll</li>
        <li>php_opcache.dll</li>
      </ul>
        </br>
        <img width="700" alt="Enable PHP Extensions" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/8830917f-6df5-4e28-b322-01317c0ed1a4">
        </br>
    <li>Refresh osTicket Installer on your browser to see <b>PHP IMAP Extension</b> and <b>Intl Extensions</b> are checked signifying the extensions are installed</li>
    <li>After configurations, locate the php file <b>ost-sampleconfig.php</b> inside the directory <b>C:\inetpub\wwwroot\osTicket\include\</b> and rename it to <b>ost-config.php</b> because osTicket Installer needs to interact with this file</li>
    <li>Now go to the <b>Properties</b> of the ost-config file and go to the <b>Advanced</b> settings in <b>Security</b> and <b>Disable Inheritance</b> to remove all inheritance permissions from the file (essentially making a "clean" object)</li>
    <li>Now add a new Permission, then click on <b>Select a principal</b> and for a new object type "everyone" the click on <b>Check Names</b> to set the Group and click OK. Then check all the boxes on Basic Permissions and then click OK. Now everyone using osTicket should have full permission to use it</li>
      <br>
      <img width="700" alt="osTicket Permissions" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/ddd0b921-f5ec-4ece-b64d-c83dd48ae4c1">
      </br>
    <li>Now, head to osTicket on your browser and click on <b>Continue</b> then set your <b>System Settings</b> and <b>Admin User</b> until you get to <b>Database Settings</b></li>
      <li>For login information, you can set it to a fake email such as "yourname@helper.com", again it is recommended to have a notepad to keep your usernames and passwords on the standby</li>
    <li>From the Installation Files, download and install <b>HeidiSQL</b></li>
      <li>Go through basic setup then launch HeidiSQL and create a New Session using the username "root" and password "Password1"</li>
        <br>
        <img width="700" alt="HeidiSQL Login" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/71ee76ed-5c2b-4812-802a-c3326980bdb2">
        </br>
    <li>You should see this once you're connected</li>
      <br>
      <img width="850" alt="HeidiSQL Success Login" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/4a431eac-e8d5-465b-a57e-b50fd2a73ef5">
      </br>
    <li>Create a Database and name it <b>osTicket</b></li>
    <li>Once connected, go back to osTicket Installer type in our username and password into the respected fields in Database Settings</li>
      <li>MySQL Database: osTicket</li>
      <li>MySQL Username: root</li> 
      <li>MySQL Password: Password1</li>
    <li>Click <b>Install Now</b>, osTicket should now be fully installed on your VM!</li>
      <br>
      <img width="700" alt="osTicket Congratulations!" src="https://github.com/landonbmartin/osticket-prereqs/assets/148168629/0d1dbab6-7d0a-4f11-872b-a309125f487c">
      </br>
  </ul>
</p>

<h3>Clean Up</h3>

<p>
  <ul>
    <li>Delete the <b>setup</b> folder inside your osTicket folder inside wwwroot (C:\inetpub\wwwroot\osTicket\setup)</li>
    <li>Set the permissions of <b>ost-config.php</b> to "read only" (have only the Read and Read and Execute boxes checked)</li>
  </ul>
</p>

<br />

<h3 align = "right">Next Tutorial - <a href="https://github.com/landonbmartin/post-install-config">osTicket - Post-Install Configuration</a></h3>
