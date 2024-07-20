+++
title = 'Sql Injection Querying'
date = 2024-07-19T16:38:06+05:30
slug = "portswigger-SQL-database-querying-non-oracle"
categories = ["portswigger","SQL injection","querying databases","MYSQL","Microsoft"]
+++


![](https://drive.google.com/file/d/1f9HZwuKTQsOFgYF-LcmJGe6YZEklaCHk/view?usp=sharing)

From the lab description we know that There is SQL vulnerability in product category filter. To solve the lab we need to display the database version string 

Here the database is My SQL ,
Let's head over to SQL cheat sheet for payloads refer to sql sheet for here 

![](https://drive.google.com/file/d/1Bzte_wix6QNWHJSUHerkX2EzBOq4pnlB/view?usp=sharing)

here are the available list of payloads we can use for different types of databases

Let's access the lab 
![](https://drive.google.com/file/d/1iwKq-m17_tF9kfzxZy9xjrAwAlQxhVeA/view?usp=sharing)

the same thing we have here it will refine your search based on the category you select for detail walkthrough refer to [SQL injection attack, querying the database type and version on Oracle](SQL%20injection%20attack,%20querying%20the%20database%20type%20and%20version%20on%20Oracle.md)

so let's generate the payload here 

`'UNION SELECT @@version, NULL#`

let's inject out payload in request we captured
![](https://drive.google.com/file/d/1TNMN1mfri1UGhJ_UtPztZ8m5xJsxLGPN/view?usp=sharing)

if we inject order by 3 we get internal sever error so number of columns is 2 itself and to check weather both columns are same data type or not to fulfill the conditions of union attack 
`UNION SELECT 'a','a'#`

![](https://drive.google.com/file/d/1KvlB14kDEud-_e_AnN5zzwzpYTWdlicQ/view?usp=sharing)

since they are same data type we can inject our payload from SQL cheat sheet

![](https://drive.google.com/file/d/1J4_nDfCNjJKFQIIUCuBfcBc3IdCiyj2W/view?usp=sharing)

![](https://drive.google.com/file/d/1b2gwJCDQwJ0vmzNXWqEizlyBqEH4P7S3/view?usp=sharing)



