+++
title = 'Dancing'
date = 2024-07-19T15:37:07+05:30
slug = "HTB-Dancing"
categories = ["hackthebox","Dancing","linux","very Easy","Starting point","tier 0"]
+++

![dancing 1](https://dl.dropbox.com/scl/fi/aw4dimz4g712yzx4eru7y/Pasted-image-20240531160951.png?rlkey=zx4i61aol0yfiypt3ov489nvb&st=gv739cbf&dl=0)

What does the 3-letter acronym SMB stand for?

****** ******* ****k

What port does SMB use to operate at?

445

What is the service name for port 445 that came up in our Nmap scan?
microsoft-ds

What is the 'flag' or 'switch' that we can use with the smbclient utility to 'list' the available shares on Dancing?

-L

How many shares are there on Dancing?

4

What is the name of the share we are able to access in the end with a blank password?

workshares

What is the command we can use within the SMB shell to download the files we find?

get

Submit root flag
5f61c10dff************