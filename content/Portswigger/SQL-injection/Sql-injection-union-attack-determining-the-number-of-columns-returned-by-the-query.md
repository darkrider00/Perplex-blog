+++
title = 'Sql Injection Union Attack Determining the Number of Columns Returned by the Query'
date = 2024-07-20T12:19:33+05:30
slug = "portswigger-SQL-database-union-attack"
categories = ["portswigger","SQL injection","Union Attack","MYSQL","no of columns"]
+++

![](https://dl.dropbox.com/scl/fi/fndnuoaou7bzqlilzwrwe/Pasted-image-20240528170339.png?rlkey=sdn7ot4w4edipnqt4m1f009ba&st=qqse52we&dl=0)

from the lab description 
we know that there is SQL vulnerability in product category filter , to solve the lab we need to perform a union attack that determine number of columns

let's access the lab
The website

![](https://dl.dropbox.com/scl/fi/7ie5zbvucnz2cgrqqbz8u/Pasted-image-20240528170956.png?rlkey=sj1ch85se6r7a4amdpga4jgsg&st=e6zd146a&dl=0)

to display null values we need to use the payload
'+UNION+SELECT+NULL--  if 1 column in ther if 2 colums are there then we need tp use 2 NULLs so on 

![](https://dl.dropbox.com/scl/fi/uxmvkpzl2ys028fz7tjav/Pasted-image-20240528171412.png?rlkey=fkkxemzfuhhkbt1pakpr9w07y&st=smmysjnu&dl=0)

i've started with null value and i got internal server error let's try 2

![](https://dl.dropbox.com/scl/fi/v85l88t8dv07fuv6ex9sz/Pasted-image-20240528171452.png?rlkey=t1njhne2wym5ihlduiaqbio32&st=04t6669w&dl=0)

same result let's go for three

![](https://dl.dropbox.com/scl/fi/ci48lppdrzudtqg9aemio/Pasted-image-20240528171523.png?rlkey=2sn803ysczppknpe4nmztbgc0&st=xiop9pcl&dl=0)

and the error disappeared so we determined the number of columns are three and we solved the lab 

![](https://dl.dropbox.com/scl/fi/0sr6ku8d4ze7v0y5d0qyx/Pasted-image-20240528171607.png?rlkey=rio366muuem85sj8g1ft6ktuh&st=r9h76b16&dl=0)