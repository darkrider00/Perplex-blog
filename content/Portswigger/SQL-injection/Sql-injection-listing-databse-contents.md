+++
title = 'Sql Injection Listing Databse Contents'
date = 2024-07-19T16:33:29+05:30
slug = "portswigger-SQL-database-listing-oracle-databse"
categories = ["portswigger","SQL injection","listing databsse contents","noracle databases"]
+++

![](https://drive.google.com/file/d/1kuZlSVsjSzOXGfzAQsJ2lFMtj06Xjn8t/view?usp=sharing)

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
![](https://drive.google.com/file/d/1hTXnHV4PR25oVskjiNCc9SUZbk6T1G_t/view?usp=sharing)

we now know that both are of same text we can inject our paylaoads

From the cheat sheet since it's a oracle database

 `'+UNION+SELECT+table_name,NULL+FROM+all_tables--`
will list all the 

![](https://drive.google.com/file/d/1Yz9UNl-zPh0-TPgsYiI5pSejr7Ps2ny_/view?usp=sharing)

we've got some table listed let's go through tables and find what we r looking for

![](https://drive.google.com/file/d/1PLfTEXZG7QA3iuTp8_Pfz7H4qYUZ1i3r/view?usp=sharing)

we've got our username table now let's view that table
username table : USERS_QFTLRV

to view the details of username table 

'+UNION+SELECT+column_name,NULL+FROM+all_tab_columns+WHERE+table_name='USERS_QFTLRV'--

![](https://drive.google.com/file/d/1WObxck8XXFdHdnPVweqP3TLiDjfPvgcv/view?usp=sharing)

password table : PASSWORD_KSZHEB
username : USERNAME_PNBHKP
now  let's retrieve the details 

payload will be 

'+UNION+SELECT+USERNAME_PNBHKP,+PASSWORD_KSZHEB+FROM+USERS_QFTLRV--

![](https://drive.google.com/file/d/1YB4HwPcAl-PMkDrWAovMaF6fDuLMvgwV/view?usp=sharing)

we got the administrator details let's login to our account to solve the lab 

![](https://drive.google.com/file/d/1c5ByQyUmDfaKQlCPaBL29a8U8ptrwLt3/view?usp=sharing)