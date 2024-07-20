+++
title = 'Sql Injection Union Attack Determining the Number of Columns Returned by the Query'
date = 2024-07-20T12:19:33+05:30
slug = "portswigger-SQL-database-union-attack"
categories = ["portswigger","SQL injection","Union Attack","MYSQL","no of columns"]
+++

![](https://drive.google.com/file/d/16nL-25dPLWfhcp1Z6OObZqh9m5YdrzVW/view?usp=sharing)

from the lab description 
we know that there is SQL vulnerability in product category filter , to solve the lab we need to perform a union attack that determine number of columns

let's access the lab
The website
![](https://drive.google.com/file/d/1yHp2ZPliTykelONj_ulLa9s3j_Karjfc/view?usp=sharing)

to display null values we need to use the payload
'+UNION+SELECT+NULL--  if 1 column in ther if 2 colums are there then we need tp use 2 NULLs so on 

![](https://drive.google.com/file/d/1bu_PKtZce-YvUC0TQ6_n1oki9euF7r7x/view?usp=sharing)

i've started with null value and i got internal server error let's try 2
![](https://drive.google.com/file/d/11_z-m45U2CBsrArZvEGRsDjSRtECRsXL/view?usp=sharing)

same result let's go for three

![](https://drive.google.com/file/d/1giphomRW2PVbeySP7DfelUYq2gcxZHYi/view?usp=sharing)

and the error disappeared so we determined the number of columns are three and we solved the lab 

![](https://drive.google.com/file/d/1mb5hw-2jiWTaSImK0yvSoTdLa-ck6oSl/view?usp=sharing)