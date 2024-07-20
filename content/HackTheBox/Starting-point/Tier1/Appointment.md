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
![](https://drive.google.com/file/d/1qvfCjsr3bht4uEqGMwK0DDQ07_prHS27/view?usp=sharing)

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
![](https://drive.google.com/file/d/16DY2OInJuMK1yWwRXXCi7uZRNs583zxm/view?usp=sharing)

the website
	in the hint they mentioned that add a comment in username field so the payload will be 
	`admin'#` and give random password and login page will be bypassed 
	for more information about thus vulnerability refer to SQL injection vulnerability allowing login bypass

![](https://drive.google.com/file/d/1p1GgUSDNF_fyHGu9G25YUQKIHb0ZaWq9/view?usp=sharing)

we logged in and got the roor flag too

Submit root flag
ans: e3d0796d002a****************

