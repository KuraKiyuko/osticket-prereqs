
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Windows 10 (Virtual Machine)
- Remote Desktop (RDP)
- Internet Information Services (IIS)
- osTicket
- MySQL
- HeidiSQL
- PHP Manager for IIS

<h2>Step 1: Create a Windows 10 Virtual Machine in Microsoft Azure</h2>

<p>
Go to the Azure Portal, go to Virtual Machines, and then create a new Virtual Machine. (Windows 10, 4 vCPUs)
</p>
<p>
<img <img width="1617" height="587" alt="Screenshot 2025-07-17 022601" src="https://github.com/user-attachments/assets/59ec2f3a-4bd8-4426-b685-f8cf86e3fcda" />
<img width="1913" height="986" alt="Screenshot 2025-07-17 022625" src="https://github.com/user-attachments/assets/235b407f-d754-4051-ba8f-cb8e013dc4d6" />
</p>
<p>
You will be required to create a resource group and give the Virtual Machine a name. For this guide, I went with naming the group os-ticket, and the VM os-ticket-vm, but you can name it whatever you please.
</p>
<p>
<img width="832" height="161" alt="image" src="https://github.com/user-attachments/assets/69fbffcb-38c3-4571-a261-268fe2d0a5ff" />
</p>
<p>
  <img width="937" height="464" alt="image" src="https://github.com/user-attachments/assets/962e8b3d-39fe-47d0-85c9-b302c1989f25" />
</p>
<p>
Make sure you choose the size and create a username and password for the Virtual Machine like so. 
</p>
<p>
<img width="942" height="655" alt="image" src="https://github.com/user-attachments/assets/17109d63-ab83-4a97-9a4f-092ae5c98ba0" />
</p>
<p>
Make sure you check the box next to licensing at the very bottom of the screen.
</p>
<p>
<img width="450" height="159" alt="image" src="https://github.com/user-attachments/assets/888ef490-1419-4983-9e26-cfb661c40454" />
</p>
<p>
Once you're done, click Next to go to Disks, then click Next again to go to Networking. Since we're only going to have one Virtual Machine for this guide, you can leave everything as is and let it create the default network.
</p>
<p>
<img width="1911" height="936" alt="image" src="https://github.com/user-attachments/assets/cc7b41da-5b7f-497e-8359-2d8bb22c2f6d" />
</p>
<p>
Click review and create, then wait for it to validate before finally clicking create again to finalize the process.
</p>
<p>
<img width="1903" height="941" alt="image" src="https://github.com/user-attachments/assets/a137cb2a-de0e-42ac-ac84-1b07aa0acbb7" />
</p>
<p>
After clicking create, it will have to create the Virtual Machine, which will typically take a few minutes.
</p>
<p>
<img width="1919" height="949" alt="image" src="https://github.com/user-attachments/assets/51791570-6829-4ce4-b810-cece6bf62806" />
</p>
<p>
Once it's finally finished deploying the machine, we can move on to Step 2!
</p>
<p>
<img width="1919" height="946" alt="image" src="https://github.com/user-attachments/assets/5769ae23-b96a-40c6-8a7d-4cb8a48c6005" />
</p>
<br />
<h2>Step 2: Using Remote Desktop Protocol to log in to your VM</h2>
<p>
First things first, we have to get the Public IP Address for your newly created Virtual machine. We can do this by going to the Azure Portal and going to Virtual Machines.
<p>
<img width="1915" height="938" alt="image" src="https://github.com/user-attachments/assets/f7fecc73-b6b7-45d3-9941-2e4949ccbd47" />
</p>
<p>
Click on the "os-ticket-vm" Virtual Machine we created, then copy the Public IP Address of the machine.
</p>
<p>
<img width="1918" height="936" alt="image" src="https://github.com/user-attachments/assets/197b3229-7fa3-4d67-b0bd-266b1678338d" />
<p>
Then, on your computer, go to your Start Menu in the bottom left corner and type "RDP" or "Remote Desktop Connection" and run it.
</p>
<p>
<img width="848" height="792" alt="image" src="https://github.com/user-attachments/assets/4b5aabf0-f30b-4a20-9271-c0f6d931b5c2" />
</p>
<p>
  Enter the Public IP Address of your Virtual Machine into the Computer box, then click Connect.
</p>
<p>
<img width="399" height="240" alt="image" src="https://github.com/user-attachments/assets/c221df56-666e-49a4-b536-4f31155c6976" />
</p>
<p>
If it automatically fills in the username, make sure to click "More Choices", then click use a different account. Then type in the username and password that you gave the Virtual Machine when you created it.
</p>
<p>
<img width="449" height="434" alt="image" src="https://github.com/user-attachments/assets/c56ed5fe-f6cb-4d56-8789-b4238451617e" />
</p>
<p>
Click yes to allow the connection.
</p>
<p>
<img width="386" height="393" alt="image" src="https://github.com/user-attachments/assets/b49e572e-65ee-4772-be7d-55a008a2845f" />
</p>
<p>
Once you're connected and logged in, we can move on to Step 3!
</p>
<br />

<h2> Step 3: Install/Enable IIS in Windows with CGI</h2>
<p>
Inside of your VM, go ahead and open up your internet browser and copy/paste this link to download a folder: https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD. This folder contains a all of the necessary files to install osTicket and some of it's dependencies.
</p>
<p>
<img width="1920" height="1040" alt="image" src="https://github.com/user-attachments/assets/6733f556-a93a-4b09-8a58-714bcab40f41" />
</p>
<p>
Move the "osTicket-Installation-Files" folder onto your desktop, then right-click and extract it there.
</p>
<p>
 <img width="1919" height="1041" alt="image" src="https://github.com/user-attachments/assets/b4a37c21-a24e-417a-9d14-df8a75728ed4" />
</p>
<p>
  Click "Extract All" then "Extract" and once it's finished it will place an unzipped version of the folder on your desktop.
</p>
<p>
<img width="1918" height="1038" alt="image" src="https://github.com/user-attachments/assets/b5b09183-0c60-4249-9e9b-42898aaabd0c" />
</p>
<p>
Now we need to install/Enable IIS (Internet Information Services). To do this, go to your Windows Start Panel -> Type Control Panel -> Programs -> Turn Windows featues on or off -> Find and Check "Internet Information Services -> Expand Internet Information Services by clicking the + -> Expand World Wide Services by clicking the + -> Expand Application Development Features the same way -> Find and Check "CGI" -> Click "OK"
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a0eccc43-c6b2-40a6-b78f-182bce737170" />
<img width="501" height="198" alt="image" src="https://github.com/user-attachments/assets/cf947e5b-280b-4404-b20c-98713e5dcf55" />
<img width="1116" height="146" alt="image" src="https://github.com/user-attachments/assets/f34de5bb-4961-4ac7-b2e4-967fdf0b476c" />
<img width="1114" height="629" alt="image" src="https://github.com/user-attachments/assets/fe3c1a1d-bae2-4349-9e83-8c3f3e95b023" />
<img width="1109" height="633" alt="image" src="https://github.com/user-attachments/assets/6bea0a77-02f9-4970-ab57-32fcdec062cc" />
</p>
<p>
After clicking "OK" it will install the Web Server, so wait for it to complete.
</p>
<p>
<img width="667" height="488" alt="image" src="https://github.com/user-attachments/assets/42276ed0-d026-4b7a-91b3-3de9e666e5a2" />
</p>
<p>
Congrats! Your Virtual Machine is now technically a Web Server, and we can move on to Step 4!
</p>
<br />

<h2>Step 4: Create the directory C:\PHP</h2>
<p>
Remember that folder we extracted to the desktop? Go ahead and open it up, navigate to the program named "PHPManagerForIIS_V1.5.0" and run the program. 
</p>
<p>
<img width="1915" height="1033" alt="image" src="https://github.com/user-attachments/assets/4eef267a-77ed-4e65-91db-61fa93d5300a" />
</p>
<p>
Click next and then agree to everything to install it.
<p>
<img width="491" height="401" alt="image" src="https://github.com/user-attachments/assets/1e0323ea-22c8-4d4e-8c42-889b4d0f0abd" />
<img width="494" height="412" alt="image" src="https://github.com/user-attachments/assets/b897fb46-7490-4505-b5ee-2d031e0c5e64" />
</p>
<p>
Back inside our "osTicket-Installation-Files" folder, go ahead and find and run the program "rewrite_amd64_en-US" and run it.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dd579aad-a040-421a-9393-7e51a9dc71bd" />
</p>
<p>
Click next and agree to everything once again to install.
</p>
<p>
<img width="490" height="387" alt="image" src="https://github.com/user-attachments/assets/a91f1855-961c-4ead-853d-07587917750f" />
</p>
<p>
Next, we're going create the C:\PHP directory. To do this, open another instance of File Explorer, then navigate to the C: Drive and right-click a space to create a folder. Name it "PHP".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7c8abaa7-ca3c-4e85-8f1b-99579afe7bfe" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f4f904b2-efe3-4139-88b3-60099bc4c01f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b4b5a813-6538-429e-a271-4250cd99dfa9" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76154630-7a03-49fc-be38-f352f9172b44" />
</p>
<p>
Now, go back to the "osTicket-Installation-Files" folder on our desktop and find the folder named "php-7.3.8-nts-Win32-VC15-x86". We're going to extract this into the C:\PHP directory folder we just created. To do this, right-click the folder -> Extract All -> Click Browse -> Navigate to the C: Drive -> Click the PHP folder -> Select Folder -> Extract
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7f17febd-ecf4-443b-90d5-2fff15afa071" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bf8ac28b-edde-46c2-8bba-331338b0a27d" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/81ade96e-5a3d-4c9a-a191-4e6409f0ea99" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/db73d7ac-75b3-4c0a-8acc-bf56d823b030" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/72185371-73d0-41f1-874c-e6259da5f800" />
</p>
<p>
Once it's extracted, you can close the folder that opens. Return to the "osTicket-Installation-Files" folder on the desktop once again and navigate to the program called "VC_redist.x86", run and install it like the others.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2aa95332-eb5c-48f6-9103-636a2fa8b595" />
<img width="474" height="297" alt="image" src="https://github.com/user-attachments/assets/5baf7905-05d4-461e-82f4-9903a973fec4" />
<img width="481" height="295" alt="image" src="https://github.com/user-attachments/assets/a2003d5e-9b26-4f98-bc02-2fe10d66df13" />
</p>
<p>
Then, run the program "mysql-5.5.62-win32", and install that as well.
</p>
<p>
<img width="484" height="378" alt="image" src="https://github.com/user-attachments/assets/e98e9d3f-9ff1-4614-827f-aa2bb8542b7c" />
</p>
<p>
When you get to this screen, you can just choose the "Typical" setup.
<p>  
<img width="492" height="382" alt="image" src="https://github.com/user-attachments/assets/2c9cf648-d73c-4a67-9fdd-08876533c83c" />
</p>
<p>
Click Finish and allow it to launch the "MySQL Instance Configuration Wizard".
</p>
<p>
<img width="492" height="386" alt="image" src="https://github.com/user-attachments/assets/eb61e79e-a2f9-49d4-834a-2a3e572bea08" />
</p>
<p>
Click Next, then choose the Standard Configuration.
</p>
<p>
<img width="491" height="380" alt="image" src="https://github.com/user-attachments/assets/8a43fee7-e39c-4acf-8c2b-c879ba79a45d" />
<img width="494" height="375" alt="image" src="https://github.com/user-attachments/assets/f313f0ee-52d0-4136-a394-c1e66d3ce634" />
</p>
<p>
You can leave these settings alone.
</p>
<p>
<img width="496" height="378" alt="image" src="https://github.com/user-attachments/assets/3577ff43-bf06-4368-a57c-dbac82704682" />
</p>
<p>
For the username/password part of the Wizard, just enter the word "root" for both, then click Next and execute to install the database. 
</p>
<p>
<img width="497" height="381" alt="image" src="https://github.com/user-attachments/assets/4633e11f-7c88-477e-85a2-26c52a97b3c5" />
</p>
<p>
<img width="497" height="384" alt="image" src="https://github.com/user-attachments/assets/8e62630c-19d8-4206-a684-73c9b33634b4" />
</p>
<p>
With that, we can move on to Step 5!
</p>
<br />

<h2>Step 5: Register PHP from within IIS</h2>
<p>
First, we're going to open IIS as an Administrator. To do so, go ahead and go to the Start Menu in the bottom left of your VM's screen again and type "IIS". Right-click "Internet Information Services (IIS) Manager" and click "Run as administrator".
</p>
<p>
<img width="919" height="697" alt="image" src="https://github.com/user-attachments/assets/9290baa5-e2e3-403b-beba-74eab9cfff39" />
<img width="1422" height="752" alt="image" src="https://github.com/user-attachments/assets/634e1eb0-9fe4-48c7-868c-845ff0624f8e" />
</p>
<p>
Once that's open, go ahead and open "PHP Manager", click "Register new PHP version", then browse to C:\PHP and double-click the .exe file named php-cgi and then click "OK".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/43f4c067-788b-4758-90fd-76b3639ee348" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cb924477-2ee5-4644-bf7c-c138565b7111" />
</p>
<p>
Now, click on os-ticket-vm on the left side of the IIS window to return to its home screen.
</p>
<p>
<img width="1422" height="753" alt="image" src="https://github.com/user-attachments/assets/a4123dba-4ed5-49d2-b764-a7f2b7660ac4" />
<img width="1424" height="752" alt="image" src="https://github.com/user-attachments/assets/9dfb9418-ebad-459d-ba98-581975ee5b41" />
</p>
<p>
On the right side of the home screen, there should be a "Manage Server" column. We're going to restart the web server, so go ahead and just click "Restart". (Alternatively, you can just click "Stop" then click "Start")
</p>
<p>
<img width="212" height="739" alt="image" src="https://github.com/user-attachments/assets/80994ede-8676-4cbe-9d9e-be3b81832efa" />
</p>
<p>
Once you've done that, we can move on to Step 6!
</p>
<br />

<h2>Step 6: Installing osTicket</h2>
<p>
For now, go ahead and minimize the IIS window. Return to the osTicket-Installation-Files folder and find the folder named "osTicket-v1.15.8" and extract it.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3a6d4c46-e53f-4064-8652-02a1bf0496a8" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7e7dbe96-7215-4474-9cfd-ee6fec205522" />
</p>
<p>
Once it's finished extracting, it's going to open the extracted folder in a separate window. You can close this since we probably have too many windows open. Inside the osTicket-Installation-Files folder, open the newly extracted "osTicket-v1.15.8" folder. Within it, you should see an "upload" folder. Go ahead and copy it. 
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6a018e3a-6fe8-4c4a-8597-586898fe7158" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4f2e2198-6e0a-4b70-9e07-2d7ec5bfcdb2" />
</p>
<p>
With it copied, go ahead and navigate to the C: Drive. If you need to, open a new instance of File Explorer by right-clicking the icon at the bottom of your screen.
</p>
<p>
<img width="1917" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb1996ac-dcbe-43ca-8106-c49e08e82770" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1f11b08e-3961-4699-9083-e6a884cf1846" />
</p>
<p>
From here, you should see a folder named "inetpub". Go ahead and open that, then open the folder named "wwwroot" and paste the previously mentioned "upload" folder into here.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d6077602-b1f1-4fbf-a2fb-e739a9c5f81a" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/70369995-694f-4695-a1b3-e3cdf8bd206d" />
<img width="1919" height="1080" alt="image" src="https://github.com/user-attachments/assets/4748d64f-ac8d-492a-aed1-579429e36cac" />
</p>
<p>
Once the "upload" file is pasted into the "wwwroot" directory, go ahead and rename it to "osTicket".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f6f4dfb6-ebc2-4164-9c88-d929bb5f9142" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d3e8391d-1b36-4490-903d-90ce7a83140d" />
</p>
<p>
  Like in the previous step, go ahead and open up your IIS Manager again, and restart the web server once more.
</p>
<p>
<img width="211" height="750" alt="image" src="https://github.com/user-attachments/assets/e1859060-8efb-4ee5-9da7-920dff5831ef" />
</p>
<p>
Now, inside the IIS Manager, go ahead and expand the "os-ticket-vm" panel by clicking the arrow on the left-hand side of the manager. Then, expand the "Sites" panel by doing the same thing. Expand "Default Website". Then click "osTicket", then click browse on the right side of the IIS Manager.
</p>
<p>
<img width="1914" height="1080" alt="image" src="https://github.com/user-attachments/assets/d4389ebb-e538-4ab3-bbf3-d72770ac5a82" />
</p>
<p>
It should open up the osTicket installer in a browser window for you.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4a3993be-e525-4f09-b955-deb64279375f" />
</p>
<p>
Notice that some of the extensions are disabled. We're going to enable them by returning to our IIS Manager then go to -> Sites -> Default Site -> osTicket -> PHP Manager
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/87e38dd5-d14b-4a9d-b7d3-29a8f10f7fd5" />
</p>
<p>
Then, click on "Enable or disable an extension".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8af46655-a223-43f0-a2a8-5014065bbb65" />
</p>
<p>
Enable: php_imap.dll 
  + php_intl.dll
+ php_opcache.dll
</p>
<p>
<img width="1920" height="1068" alt="image" src="https://github.com/user-attachments/assets/e4acc9d4-5203-4e6c-9ebf-e2d568654291" />
<img width="1920" height="1079" alt="image" src="https://github.com/user-attachments/assets/3dd8cb5b-6725-44ec-87b4-a1c33f8858d0" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b93078f9-020d-42f1-9697-db77a12d9756" />
</p>
<p>
Once that's done, minimize IIS again and go back into the web browser with osTicket installer page. Refresh the page and you should see more of the extensions enabled now.
</p>
<p>
<img width="306" height="86" alt="image" src="https://github.com/user-attachments/assets/718558dd-2f71-4cbd-a2f6-1327e3f23f41" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/faa8a4c7-3afb-4df4-a14d-b79526080431" />
</p>
<p>
For now, go ahead and minimize the osTicket installer page and open up the C: Drive again. Go back into the "inetpub" folder. From there -> "wwwroot" -> "osTicket" -> "include" -> Find "ost-sampleconfig.php" and rename it to "ost-config.php"
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f2280f39-b4e1-4dca-ba80-23b41089c5db" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8045779d-f1b6-4eda-9f0c-ad44fefe5800" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/42affa58-88e9-4fd3-8da9-ee11bdacd99f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/55e059ae-6bd0-402c-ac7e-4d326e2eee6f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8440f693-ed45-4414-abd8-1be02993bcff" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3c796949-7197-49a3-97f7-ee923624470f" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4c8910a3-7ba7-4f14-a98f-b7938af3a871" />
</p>
<p>
Now, we have to give osTicket permissions to configure this file we just renamed. To do so, right-click the file and click properties.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2174c5c8-7501-4900-a672-7ac057f78760" />
</p>
<p>
Go to Security -> Advanced
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d79bf58e-1a30-428b-a851-791fa5cbd375" />
</p>
<p>
Disable Inheritance -> Remove all inherited permissions
</p>
<p>
<img width="1918" height="1080" alt="image" src="https://github.com/user-attachments/assets/1ba8167a-4866-4801-bb60-c39b94163f31" />
</p>
<p>
Click "Add" -> Select Principal
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b20292c8-f117-4b0d-a50e-a79a724ae591" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fc753d18-778e-4434-8347-0e80439215f1" />
</p>
<p>
Type "Everyone" -> click "Check Names" -> "OK" -> Check "Full Control" -> Click "OK"
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b6a32738-e134-4946-aaef-2ec5a26a80bd" />
<img width="1918" height="1080" alt="image" src="https://github.com/user-attachments/assets/851b2334-1b9f-4c3b-a2d0-5611e8e986b4" />
</p>
<p>
It should look like this. If it does, hit "Apply" then "OK"
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c4a71af4-3e07-44d7-a5e6-39f317fee6ac" />
</p>
<p>
Now let's go back to the osTicket Installer on the web browser and click "Continue".
</p>
<p>
<img width="1919" height="1080" alt="image" src="https://github.com/user-attachments/assets/d53678c5-42a9-4744-8945-225381fea618" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d1f59e93-38e9-46b4-a60a-60edb073eade" />
</p>
<p>
For the "Help Desk Name" you can name it whatever you want, and the email address I don't think matters for the sake of this, so just make one up or use your own. I'll just be naming it "Justin's Help Desk" for the purpose of this guide.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0e796d91-c251-4d9a-8036-4f55aec0225d" />
</p>
<p>
For the admin user, you can just put your name. The email address for that DOES have to be different then the one you just put above under the default email, so just put something else here. For the username and password, you can put whatever you want. I'll be using "adminuser" for the user and "Password1" for the password if you'd like to do the same, but you don't have to.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/be3323c6-97c9-4510-9273-833f6cc53fe7" />
</p>
<p>
Next, we have to create a database for osTicket and provide the credentials for it in order for us to finalize the installation. So, minimize the installer webpage and return to the "osTicket-Installation-Files" Folder on your desktop, run the "HeidiSQL_12.3.0.6589_Setup" program and install it.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/66a22b3e-7047-4342-ac95-65ca393375e0" />
</p>
<p>
Once it's finished, allow it to launch HeidiSQL by leaving it checked and clicking finish and skip when the window pops up.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9bce9382-473b-4a25-8070-fa39e6945bfd" />
</p>
<p>
Inside the HeidiSQL program, click "New".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dfbff7b6-4f6e-4513-ac99-1f8bc53192d6" />
</p>
<p>
On the right-hand side, you should see a "user" and "password" section. The "user" should be autofilled as "root". If you remember back in a previous step, we set the password as "root", so go ahead and enter "root" as the password. Afterwards, click open.
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e3bea699-f3ae-4b64-9099-e44dfd953675" />
<img width="931" height="595" alt="image" src="https://github.com/user-attachments/assets/ed91a071-de9f-404a-8e79-acde8bf8aef8" />
</p>
<p>
We've opened up a connection to our database, now we need to create a database called "osTicket". To do so, right-click the dolphin-looking thing titled "Unnamed" then hover over "Create New" then click "Database".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c39a1800-f6a9-40ea-bc3e-8de057f5c9cd" />
</p>
<p> 
Name it "osTicket". It needs to be spelled the same way. Then click "OK".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fc783125-6b11-452f-b557-d2f8e3690cfe" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3f9a26c4-7ae7-4aa0-883d-7b2a139d91bf" />
</p>
<p>
Finally, go back to the osTicket Installer on the browser and fill out the MySQL Database information. "osTicket" is the Database, and the username and password that we set up earlier come into play once more, being "root".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d1b95572-ce42-42e9-a922-54a3da2985af" />
</p>
<p>
Once you have that filled out, click "Install Now".
</p>
<p>
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b2f9ecfe-9ba3-44f4-aa29-fb11528e03fc" />
</p>
And congratulations! osTicket was successfully and officially installed!
