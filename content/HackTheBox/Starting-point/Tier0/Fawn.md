+++
title = 'Fawn'
date = 2024-07-19T15:42:52+05:30
slug = "HTB-fawn"
categories = ["hackthebox","FAWN","linux","very Easy","Starting point","tier 0"]
+++

![fawn 1](https://dl.dropbox.com/scl/fi/cfdoazppb5mr38gqhru5l/Pasted-image-20240531151234.png?rlkey=r7q3m4k3iegui6hngp3uryenc&st=cqiyg7j2&dl=0)

we got the ftp files

![fawn 2](https://dl.dropbox.com/scl/fi/gx7b0zsd52qwivikig3dv/Pasted-image-20240531151825.png?rlkey=oh0rlf13b82cljyxfaywxw85w&st=cz5do3vb&dl=0)

now we got the flag 

TASK 1

What does the 3-letter acronym FTP stand for?

file transfer protocol

Which port does the FTP service listen on usually?

port 21

What acronym is used for the secure version of FTP?

SFTP

What is the command we can use to send an ICMP echo request to test our connection to the target?

Ping

From your scans, what version is FTP running on the target?

vsftpd 3.0.3

From your scans, what OS type is running on the target?

Unix

What is the command we need to run in order to display the 'ftp' client help menu?
FTP -h

What is username that is used over FTP when you want to log in without having an account?

anonymous

What is the response code we get for the FTP message 'Login successful'?

230

There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system.

ls

What is the command used to download the file we found on the FTP server?

get

Submit root flag

035db21c88152****