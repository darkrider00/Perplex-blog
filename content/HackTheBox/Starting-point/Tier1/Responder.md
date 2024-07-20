+++
title = 'Responder'
date = 2024-07-19T16:00:53+05:30
slug = "HTB-responder"
categories = ["hackthebox","Sequel","linux","very Easy","Starting point","tier 1"]
+++


![responder 1](https://dl.dropbox.com/scl/fi/2wba8o743rol1bpf5lmqb/Pasted-image-20240531132119.png?rlkey=cyhcxglb6u038yk7jdpyihu14&st=oddllpz0&dl=0)

nmap scan 

![responder 2](https://dl.dropbox.com/scl/fi/gnqce17lkpyh2jmm5zuvf/Pasted-image-20240531132142.png?rlkey=h0vydr83yh6f7pzvxpposrlvr&st=u735391h&dl=0)

unika.htb

Which scripting language is being used on the server to generate webpages?

![responder 3](https://dl.dropbox.com/scl/fi/w49lpi77xugsbzz5uz4tn/Pasted-image-20240531132806.png?rlkey=m06bg5r765v9o6kamxpcfj54d&st=bsmtwy09&dl=0)
PHP

What is the name of the URL parameter which is used to load different language versions of the webpage?

Ans: page

Which of the following values for the `page` parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"

url : http://unika.htb/index.php?page=/../../../../../../../windows/system32/drivers/etc/hosts

![responder 4](https://dl.dropbox.com/scl/fi/nvabxvjf6n7d2v5rc1ska/Pasted-image-20240531133013.png?rlkey=prd3m3ly4cija9t4i0jdqxp12&st=v3vrpmzp&dl=0)



Which of the following values for the `page` parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"



What does NTLM stand for?

New Technology Lan Manager

Which flag do we use in the Responder utility to specify the network interface?

![responder 5](https://dl.dropbox.com/scl/fi/katsxsd28wliivuywcplm/Pasted-image-20240531133759.png?rlkey=c8ay8uj612t4vq7vknd6noucy&st=vm64l5ib&dl=0)

let's clone this repo

-I is used to specify the flag

There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?.

John the ripper

What is the password for the administrator user?

using JTR tool : badminton 

We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?

![responder 6](https://dl.dropbox.com/scl/fi/vhr5nokqvywtxnxjrj06c/Pasted-image-20240531135611.png?rlkey=rve23xay7cjgeai9ugw3tpzvr&st=q7ht3ixd&dl=0)

5985


![responder 7](https://dl.dropbox.com/scl/fi/9ixw0ytt5y3rzmdjr850o/Pasted-image-20240531135923.png?rlkey=ndzu95a17iz6svwy2ozqc6nn1&st=w4aajnw9&dl=0)

we got our flag 
Submit root flag