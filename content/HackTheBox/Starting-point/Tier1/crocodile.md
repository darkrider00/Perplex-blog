+++
title = 'Crocodile'
date = 2024-07-19T15:55:23+05:30
slug = "HTB-crocodile"
categories = ["hackthebox","Crocodile","linux","very Easy","Starting point","tier 1"]
+++


What Nmap scanning switch employs the use of default scripts during a scan?
Ans: -sC

![crocodile 1](https://dl.dropbox.com/scl/fi/ulqn1alfy4xxapy4vx2eh/Pasted-image-20240531124729.png?rlkey=ig2ogybxtjw474kqt8btgstdi&st=h63tl26d&dl=0)

What service version is found to be running on port 21?
Ans: vsftpd 3.0.3

What FTP code is returned to us for the "Anonymous FTP login allowed" message?
Ans: 230

After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?
Ans: anonymous

After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?

![crocodile 2](https://dl.dropbox.com/scl/fi/zcrhwpeq75uztelq300f2/Pasted-image-20240531125348.png?rlkey=3hrih52p5hrth1731st1fa883&st=llf2riwz&dl=0)

we can use get command

What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?

![crocodile 3](https://dl.dropbox.com/scl/fi/bwjlo1d8fe3xdhh0qw9cq/Pasted-image-20240531125707.png?rlkey=pyp5l5j7oazecukoefduwdhss&st=fslhe3cf&dl=0)
Ans: Admin

What version of Apache HTTP Server is running on the target host?
from the nmap scan
Apache httpd 2.4.41

What switch can we use with Gobuster to specify we are looking for specific filetypes?
Ans:-x

Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?

![crocodile 4](https://dl.dropbox.com/scl/fi/k73k70kf5a6jsb7nt2xkw/Pasted-image-20240531130728.png?rlkey=1m8doxncujn4j1tzfp0ufq9us&st=mybv7caz&dl=0)
we have got login.php let's navigate to login.php in website



![crocodile 5](https://dl.dropbox.com/scl/fi/i3buwtpybr9mittjhsmrz/Pasted-image-20240531131114.png?rlkey=lmjh9uzitg0wn06zlttokm872&st=u6e2aciu&dl=0)

let's login with our details

![crocodile 6](https://dl.dropbox.com/scl/fi/pik319289q484bid3n2og/Pasted-image-20240531131034.png?rlkey=xnyhju3s1uz8gfw7ggse35i28&st=0m3ehe7y&dl=0)

we've got our flag 
Submit root flag
c7110277ac44d*********************