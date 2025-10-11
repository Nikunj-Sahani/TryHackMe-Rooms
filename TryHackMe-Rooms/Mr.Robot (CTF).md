<h2 align="center">👨🏻‍💻 MR. ROBOT CTF 👨🏻‍💻</h2>

- Can you **Root** this Mr. Robot styled machine? 
- This is a virtual machine meant for **beginners/intermediate users.**
- There are **3 hidden keys** located on the machine, can you **find them?**

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
## Enter 1st Key on TryHackMe
- What is key 1?
- [ ] **073403c8a58a1f80d943455fb30724b9** *( First Key )*
      
<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-7.png" alt="Sample Image"></div>

---
## 2. Login Page Found
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

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-12.png" alt="Sample Image"></div>

---
## Set up Listener
Once this is Done and saved, I open Kali terminal 
> - cmd : **nc-nvlp 8888**
- Listen for connection attempt from the target machine.

<div ><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-13.png" alt="Sample Image"></div>

---
## Refresh the page for Connection
Go to this page
> - Address - **https://x.x.xx.xx/wp-content/themes/twentyfifteen/404.php**
- **When we enter this page, reverse connection initiated**

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-14.png" alt="Sample Image"></div>

---
## Connection Recieved
The connection is completed.
- This initiates the session and give limited shell access on the target with user ‘daemon’.

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-15.png" alt="Sample Image"></div>

---
## Key Finding in Daemon User
Sticking to the goal and following the same pattern of key files, 
- I quick check file system with command then i found 2 file
   > -  key-2-of-3.txt
   > -  Password.raw-md5
  
- ** key-2-of-3.txt.** It was in robot’s directory, So it not open with daemon user. 
  > - For key file — **Access denied..**

- Then open 2nd file — **Password.raw-md5**
> - c3fcd3d76192e4007dfb496cca67e13b **(A hash key Found)**

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-16.png" alt="Sample Image"></div>

---
## CrackStation (Hash Decryptor)
Enter hash Value and decrypt it.
- **Hash value :** c3fcd3d76192e4007dfb496cca67e13b
- [ ] Decrypted key : **abcdefghijklmnopqrstuvwxyz**
      
<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-17.png" alt="Sample Image"></div>

---
## Robot Login
Switch user to robot
 > - cmd : **su robot**
 > - password : **abcdefghijklmnopqrstuvwxyz**
Logged in Succesfully
- Then i try to **open Key 2.**
- cmd : *cat key-2-of-3.txt*
> -  **822c73956184f694993bede3eb39f959** *(2nd Key)*

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-18.png" alt="Sample Image"></div>

---
## Enter 2nd Key on TryHackMe
- What is key 2?
- [ ] **822c73956184f694993bede3eb39f959** *( Second Key )*

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-19.png" alt="Sample Image"></div>

---
## 3. Root Access
I found there is a vulnerability in Nmap,

- I set into interactive mode and allows you to run shell commands directly in nmap.
- Cmd used
> - **nmap --interactive**
> - **!sh**
> - **id**
Then we enter in root user
- cmd : **cd /root**  (I am now root.)
- cat key-3-of-3.txt
> - **04787ddef27c3dee1ee161b21670b4e4** *(Third Key)*

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-20.png" alt="Sample Image"></div>

---
## Enter 3rd Key on TryHackMe
- What is key 2?
- [ ] **04787ddef27c3dee1ee161b21670b4e4** *( Third Key )*

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-21.png" alt="Sample Image"></div>

---
---
## ⛳ LAB SOLVED ⛳

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-Final.png" alt="Sample Image"></div>

## 👨‍🎓 Badge Earned on TryHackMe

<div style="text-align: right;"><img src="https://github.com/Nikunj-Sahani/TryHackMe-Rooms/blob/main/Images/Robot-badge.png" alt="Sample Image"></div>

