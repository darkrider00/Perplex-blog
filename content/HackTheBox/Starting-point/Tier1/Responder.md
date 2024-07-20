+++
title = 'Responder'
date = 2024-07-19T16:00:53+05:30
slug = "HTB-responder"
categories = ["hackthebox","Sequel","linux","very Easy","Starting point","tier 1"]
+++


![](https://drive.google.com/file/d/1_aJQCZYM7CQs-h3jhnnCmV8Lz2hKMTkR/view?usp=sharing)

nmap scan 

![](https://drive.google.com/file/d/1czHKOUgHL_l7G838LrcfHUNjXUoVQ58b/view?usp=sharing)

unika.htb

Which scripting language is being used on the server to generate webpages?

![](https://drive.google.com/file/d/1Od87KjjpS0F2kv8DEf_osP-QKV7amelP/view?usp=sharing)
PHP

What is the name of the URL parameter which is used to load different language versions of the webpage?

Ans: page

Which of the following values for the `page` parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"

url : http://unika.htb/index.php?page=/../../../../../../../windows/system32/drivers/etc/hosts

![](https://drive.google.com/file/d/1m7YYdv0bVKkWNokAEnumCoGbIj-1PAnT/view?usp=sharing)



Which of the following values for the `page` parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"



What does NTLM stand for?

New Technology Lan Manager

Which flag do we use in the Responder utility to specify the network interface?

![](https://drive.google.com/file/d/1xovlBKXifNrHRiq5zp32WyT629wHsOQ_/view?usp=sharing)

let's clone this repo

-I is used to specify the flag

There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?.

John the ripper

What is the password for the administrator user?

using JTR tool : badminton 

We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?

![](https://drive.google.com/file/d/1O9u2bzeysb4-p3RG_kYZJPSm2xkN0H6X/view?usp=sharing)

5985


![](https://drive.google.com/file/d/1oM6VurDRSa_5wKb06uFems0y2kIGD3vp/view?usp=sharing)

we got our flag 
Submit root flag