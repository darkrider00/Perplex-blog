+++
title = 'Sql Injection Vulnerbility in Where Clause Allowing Retrieval of Hidden Data'
date = 2024-07-20T12:31:38+05:30
slug = "portswigger-SQL-injection-vulnerbility-where-clause"
categories = ["portswigger","SQL injection","Where clause","hidden data"]
+++


![](https://dl.dropbox.com/scl/fi/ccx89eq1j0xommfb0ygdp/Pasted-image-20240527134517.png?rlkey=fsgtg7cok87g85f5fdnpq1e0e&st=5ga22iwl&dl=0)

in this description it's saying that there is a SQL vuln in product category filter ,
to solve this lab we need to perform a SQL injection that causes application to display unreleases products

![](https://dl.dropbox.com/scl/fi/ln9soojpjwdekisuzm1io/Pasted-image-20240527134547.png?rlkey=8nz42gw645muo0okire6vxzz4&st=4s1016g0&dl=0g)

this is the website dashboard 
since it's mentioned that there is a vulnerability in product category let's select the product category and capture the request in burp suite

SELECT * FROM products WHERE category = 'Gifts' AND released = 1
- here we are selecting products where category = gifts And Released =1 so we gave to exploit the category here

![](https://dl.dropbox.com/scl/fi/vjgfpjjjagocb0ti4wmsg/Pasted-image-20240527135154.png?rlkey=3jqy0t5e143j1uhobv0yirrh8&st=12nrh2lm&dl=0)

we've selected category and got a request we can modify this request to view the unreleased products

so let's send this to repeater and inject a payload and see what happens

![](https://dl.dropbox.com/scl/fi/iiwcxut5qkj29uxrhblq7/Pasted-image-20240527135642.png?rlkey=5ykmk81dtlv3axyd67mmb0imt&st=zeazk2ht&dl=0)

SQL injection vulnerability in WHERE clause allowing retrieval of hidden data we got this 

![](https://dl.dropbox.com/scl/fi/th058iyxl4wvw709gmp68/Pasted-image-20240527135818.png?rlkey=y6vfndlnb9jdnr7l675xt9bhn&st=3f4cwavw&dl=0)

i added '  at the end of the url to check for sql injection and i got internal server error
if we set category field to '' instead of adding ' we won't get error

- so we can add category = ' 'Or 1=1-- and encode it in the request and we solved the lab 

![](https://dl.dropbox.com/scl/fi/kji9sgdt095gnwrfwnlqc/Pasted-image-20240527140259.png?rlkey=mz325h4mldzmimw49bue256bp&st=tlkeukp4&dl=0)