+++
title = 'Crocodile'
date = 2024-07-19T15:55:23+05:30
slug = "HTB-crocodile"
categories = ["hackthebox","Crocodile","linux","very Easy","Starting point","tier 1"]
+++


What Nmap scanning switch employs the use of default scripts during a scan?
Ans: -sC

![](https://drive.google.com/file/d/1pOWYSQ9PhvRmn7IlkfY5DEWrPCepYZ7V/view?usp=sharing)

What service version is found to be running on port 21?
Ans: vsftpd 3.0.3

What FTP code is returned to us for the "Anonymous FTP login allowed" message?
Ans: 230

After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?
Ans: anonymous

After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?
![](https://drive.google.com/file/d/1mpPu1g_J8G0mF_9NcUfUU_ndDbZZKdf5/view?usp=sharing)

we can use get command

What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?

![](https://drive.google.com/file/d/1hdJ5PVP0qdETLBxa-3cuDL92i8RhNUwo/view?usp=sharing)
Ans: Admin

What version of Apache HTTP Server is running on the target host?
from the nmap scan
Apache httpd 2.4.41

What switch can we use with Gobuster to specify we are looking for specific filetypes?
Ans:-x

Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?

![](https://drive.google.com/file/d/1hdJ5PVP0qdETLBxa-3cuDL92i8RhNUwo/view?usp=sharing)
we have got login.php let's navigate to login.php in website



![](https://drive.google.com/file/d/1KDIeMhsoQWzmmaP9Tp35tOJ5fjkmj9pg/view?usp=sharing)
let's login with our details

![](https://drive.google.com/file/d/12eTP5issyNWNz0nMIHA_00WgvzEoA4Gl/view?usp=sharing)

we've got our flag 
Submit root flag
c7110277ac44d*********************