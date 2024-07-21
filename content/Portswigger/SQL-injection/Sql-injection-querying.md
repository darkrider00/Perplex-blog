+++
title = 'Sql Injection Querying'
date = 2024-07-19T16:38:06+05:30
slug = "portswigger-SQL-database-querying-non-oracle"
categories = ["portswigger","SQL injection","querying databases","MYSQL","Microsoft"]
+++


![](https://dl.dropbox.com/scl/fi/qdlft70gxecratknh54ol/Pasted-image-20240528145236.png?rlkey=jytybzujrgxyfixelzh723fbj&st=xgfqma9d&dl=0)

From the lab description we know that There is SQL vulnerability in product category filter. To solve the lab we need to display the database version string 

Here the database is My SQL ,
Let's head over to SQL cheat sheet for payloads refer to sql sheet for here 

![](https://dl.dropbox.com/scl/fi/l7zb5ez6udlxgng3qy2s3/Pasted-image-20240528150258.png?rlkey=t6kbcp7rhlg5pywkg3b75y2m2&st=u1pt11bp&dl=0)

here are the available list of payloads we can use for different types of databases

Let's access the lab 

![](https://dl.dropbox.com/scl/fi/9scvlpz2pym7cy04a1vkt/Pasted-image-20240528151802.png?rlkey=l72wnvf2ok0579vgvbngkqyfq&st=fnp8evk5&dl=0)

the same thing we have here it will refine your search based on the category you select for detail walkthrough refer to 

so let's generate the payload here 

`'UNION SELECT @@version, NULL#`

let's inject out payload in request we captured

![](https://dl.dropbox.com/scl/fi/y275oi6tg3bsumsei0g64/Pasted-image-20240528152458.png?rlkey=i1uzgwkslgcspl7ahkc2nawzm&st=hwjq4v7d&dl=0)

if we inject order by 3 we get internal sever error so number of columns is 2 itself and to check weather both columns are same data type or not to fulfill the conditions of union attack 
`UNION SELECT 'a','a'#`

![](https://dl.dropbox.com/scl/fi/o6exu503cawat1f9ykw9e/Pasted-image-20240528154319.png?rlkey=uqmam0empnaaacocujkk0ph1x&st=vvcjhxxl&dl=0)

since they are same data type we can inject our payload from SQL cheat sheet

![](https://dl.dropbox.com/scl/fi/mop4d535gdygn1b17ae6t/Pasted-image-20240528154551.png?rlkey=sij3ss2wjltbneae7l7i3pjt1&st=xnet00hc&dl=0)

![](https://dl.dropbox.com/scl/fi/2azp3ztke3nse6v1jfq9m/Pasted-image-20240528154631.png?rlkey=woqcrnlkcf18o7upwtzz3wx66&st=k0xn8lu0&dl=0)



