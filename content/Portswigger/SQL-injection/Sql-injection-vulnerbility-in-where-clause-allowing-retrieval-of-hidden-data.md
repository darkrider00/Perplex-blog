+++
title = 'Sql Injection Vulnerbility in Where Clause Allowing Retrieval of Hidden Data'
date = 2024-07-20T12:31:38+05:30
slug = "portswigger-SQL-injection-vulnerbility-where-clause"
categories = ["portswigger","SQL injection","Where clause","hidden data"]
+++


![](https://drive.google.com/file/d/1i8vJ7VcP5swj4Ui1Anb8MEuX3V5NHcFR/view?usp=sharing)

in this description it's saying that there is a SQL vuln in product category filter ,
to solve this lab we need to perform a SQL injection that causes application to display unreleases products

![](https://drive.google.com/file/d/1pqZnd13-2BalonNIpuXngC0VKcdtRPI4/view?usp=sharing)

this is the website dashboard 
since it's mentioned that there is a vulnerability in product category let's select the product category and capture the request in burp suite

SELECT * FROM products WHERE category = 'Gifts' AND released = 1
- here we are selecting products where category = gifts And Released =1 so we gave to exploit the category here

![](https://drive.google.com/file/d/1xCvw9Re8pp8OyMR5NYAME-gn1BUSjMcs/view?usp=sharing)

we've selected category and got a request we can modify this request to view the unreleased products

so let's send this to repeater and inject a payload and see what happens

![](https://drive.google.com/file/d/1AbQizgcqVocWSn5yXjyZn2huWce5r4RQ/view?usp=sharing)

SQL injection vulnerability in WHERE clause allowing retrieval of hidden data we got this 

![](https://drive.google.com/file/d/1J8UioI7j1_Bi7Hxc2DNj_-bkjRyu27Zb/view?usp=sharing)

i added '  at the end of the url to check for sql injection and i got internal server error
if we set category field to '' instead of adding ' we won't get error

- so we can add category = ' 'Or 1=1-- and encode it in the request and we solved the lab 

![](https://drive.google.com/file/d/1y1weNU29GxlDNgMQe0YLlVCgxVNb9-24/view?usp=sharing)