<h2 align="center">👨🏻‍💻 MR. ROBOT CTF 👨🏻‍💻</h2>

- Can you **Root** this Mr. Robot styled machine? 
- This is a virtual machine meant for **beginners/intermediate users.**
- There are **3 hidden keys** located on the machine, can you find them?

---

> - [ MR. ROBOT CTF ](https://tryhackme.com/room/mrrobot)
- [ ] What is key 1?
- [ ] What is key 2?
- [ ] What is key 3?

---
Mr. Robot has three keys hidden in different locations. The main goal is to find all three tokens hidden in the system. Each key is progressively difficult to find. Breaking into it isn’t too difficult. There isn’t any advanced exploitation or reverse engineering. The level is considered beginner-intermediate.

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot.png" alt="Sample Image"></div>

- To deploy the Mr. Robot virtual machine, you will first need to connect to our network.
- Connect to our network using OpenVPN with Kali linux.
---
### Steps to Test after deploy the Machine.

| -- | Contents |
|---| ---------- |
| 1 | Machine Deploy |
| 2 | Network Scanning |
| 3 |
| 4 |
| 2 | |
| 2 | |
| 2 | |
| 2 | |
| 2 | |
| 2 | |
| 2 | |

---
## Machine Deployed
You can deploy the machine by an option in right. **{ Start Machine }**
- After start the machine you got a Ip address.
> - x.x.xx.x (Random IP)

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-1.png" alt="Sample Image"></div>

---
## Network Scanning
Nmap the well known network scanner, I used it to get the open ports so I can design my plan for attacking the machine.

**All the process of testing done by Kali Linux.**
- Now **Start the Kali Linux**
- Scan the Ip address
> - cmd - **nmap –A –p- x.x.xx.xx**

After Scanning the network, I found **Open Ports.**
It shows **Three** open Ports
- [ ] ssh - 22/tcp ( OpenSSH)
- [ ] http - 80/tcp (Apache Httpd)
- [ ] ssl/http - 443/tcp (Apache Httpd)

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-2.png" alt="Sample Image"></div>

---
##  1. Web Server
With both http and https we get presented with a cool animation of a linux terminal booting up and Mr Robot logging in.
> - http://x.x.xx.xx **(Web Server)**

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-3.png" alt="Sample Image"></div>

**Nice website....**
- At the prompt the only commands that work are the **6 listed** above.
- Took **note of each page** just in case i needed it later.

---
## Directory Finding
I use **Dirb** for Directory finding.

- **(DIRB) Directory Buster - Directory Finding Tool**
> - cmd - **dirb http://x.x.xx.x**

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-4.png" alt="Sample Image"></div>

We got a important directory after scan.
 > - **http://x.x.xx.xx/robots.txt**

---
## Open Directory in Web server
Searched - *http://x.x.xx.xx/robots.txt*
- ! Boom ! Found Key !
> - **fsocity.dic**
> - **key-1-of-3.txt**

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-5.png" alt="Sample Image"></div>

---
## Opening First Key
Searched - *http://x.x.xx.xx/key-1-of-3.txt*

   - [ ] **073403c8a58a1f80d943455fb30724b9** *( First Key )*

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-6.png" alt="Sample Image"></div>

---
## Enter Keys in TryHackMe
- What is key 1?
- [ ] **073403c8a58a1f80d943455fb30724b9** *( First Key )*
      
<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-7.png" alt="Sample Image"></div>

---
## Login Page Found
When we done Dirb Scan, There is a login directory.
- I quickly found the **Word Press login page** 
 > - http://x.x.xx.xx/wp-login.php

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-8.png" alt="Sample Image"></div>

---
## Username & Password Finding
When we done Dirb Scan, There is a **directory of license.**
> - http://x.x.xx.xx/license
- When i scroll down the page, i got a **Hash key**.
- [ ] ZWxsaW900kVSMjgtMDY1Mgo=

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-9.png" alt="Sample Image"></div>

---
## Hash Decryption
A website used for descrypting the hash.
Go on [ CyberChef ](https://gchq.github.io/CyberChef/)

- Recipe - **From base64**
- Hash Key in Input- **ZWxsaW900kVSMjgtMDY1Mgo=**
- Decrypt Key - **elliot : ER28-0652**
  
<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-10.png" alt="Sample Image"></div>

---
## Wordpress Page Logged in 
This is interface/dashboard of the logged in website.

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-11.png" alt="Sample Image"></div>

---
## Upload shell
Steps to go for Editing
- [ ] **Appearance ➡️ Editor ➡️ 404 Template ➡️ Clear the text**

The used shell is PentestMonkey
Now Copy code of **Monkey pentest reverse shell**
- [ ] Go on [ Reverse Shell Code ](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)

- **Paste the code in 404 Template**
  > - Change the default IP to your Linix IP.
  > - Change Port to listen & connection

---
## Set up Listener
Once this is Done and saved, I open Kali terminal 
> - cmd : **nc-nvlp 8888**
- Listen for connection attempt from the target machine.

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-12.png" alt="Sample Image"></div>

---
## Refresh the page for Connection
Go to this page
> - Address - **https://x.x.xx.xx/wp-content/themes/twentyfifteen/404.php**
- **When we enter this page, reverse connection initiated**

<div ><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-13.png" alt="Sample Image"></div>

---
## Connection Recieved

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-14.png" alt="Sample Image"></div>
