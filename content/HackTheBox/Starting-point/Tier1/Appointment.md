+++
title = 'Appointment'
date = 2024-07-19T15:49:30+05:30
slug = "HTB-Appointment"
categories = ["hackthebox","Appointment","linux","very Easy","Starting point","tier 1"]
+++



**TASK 1**

What does the acronym SQL stand for?

Ans: Structured Query language

**TASK 2**

What is one of the most common type of SQL vulnerabilities?
Ans: SQL Injection

**TASK 3**

What is the 2021 OWASP Top 10 classification for this vulnerability?
searching on google will give us the answer
ANS: **A03:2021**-Injection

What does Nmap report as the service and version that are running on port 80 of the target?
- to know the service on port 80 we need to run nmap scan on port 80 
![appointment 1](https://dl.dropbox.com/scl/fi/gkrn445j9c61xfzcz0cm3/Pasted-image-20240531100158.png?rlkey=mtf3ko33w151lqs1qmjmjne4s&st=15j21gwp&dl=0)

Apache httpd 2.4.38 ((Debian)) service is running on port 80 

What is the standard port used for the HTTPS protocol?
Ans: 443

What is a folder called in web-application terminology?
Ans: directory

What is the HTTP response code is given for 'Not Found' errors?
Ans: 404

Gobuster is one tool used to brute force directories on a webserver. What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?
Ans: -dir

What single character can be used to comment out the rest of a line in MySQL?
Ans: #

If user input is not handled carefully, it could be interpreted as a comment. Use a comment to login as admin without knowing the password. What is the first word on the webpage returned?
Ans: Congratulations!
![appointment 2](https://dl.dropbox.com/scl/fi/ohptivmouwwpju24e00ek/Pasted-image-20240531100537.png?rlkey=ed4lbe3yyc7x8rxhhrzhythjp&st=fq5m9663&dl=0)

the website
	in the hint they mentioned that add a comment in username field so the payload will be 
	`admin'#` and give random password and login page will be bypassed 
	for more information about thus vulnerability refer to SQL injection vulnerability allowing login bypass

![appointment 3](https://dl.dropbox.com/scl/fi/uqj9wiugv315n708bw57k/Pasted-image-20240531101049.png?rlkey=5y77ng4ng601kqifi2swe8ty9&st=6p1nhj5z&dl=0)

we logged in and got the roor flag too

Submit root flag
ans: e3d0796d002a****************

