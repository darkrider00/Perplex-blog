+++
title = 'Sql Injection Querying Oracle'
date = 2024-07-19T16:42:59+05:30
slug = "portswigger-SQL-database-querying-oracle"
categories = ["portswigger","SQL injection","querying databases","MYSQL","Microsoft"]
+++

![](https://dl.dropbox.com/scl/fi/zr2psydu1suf4gzl7vmzh/Pasted-image-20240528110905.png?rlkey=slionxwxgkzbbqpfz1zwwhq82&st=r1siyj6f&dl=0)

From the lab description we know that there is SQL vulnerability in product category and to solve this lab we need to display database version string

And this is a ORACLE database

Refer to SQL cheatsheet here

https://portswigger.net/web-security/sql-injection/cheat-sheet

TO retrieve the database version and contents these are the payloads available here

![](https://dl.dropbox.com/scl/fi/w81634fm5rwb361kn4kyc/Pasted-image-20240528111334.png?rlkey=lrn8p3cs5tus982ydfdzoa038&st=mt7kh3an&dl=0)

Now let's access the website

![](https://dl.dropbox.com/scl/fi/wnnjfjeksnp9budwdf445/Pasted-image-20240528111621.png?rlkey=j9ri37dpdqqfbraj3uuzx6n4j&st=0zame2s0&dl=0)

From the website if we select the different categories mentioned  here by selecting different categories the website is refining our search 

if we observe we are getting the product and it's details so first we have to determine the number of columns in the table 

to determine the number of problems in the table we can use ORDER BY and see result 

![](https://dl.dropbox.com/scl/fi/ga6tdkl9xsf4ww3sp48ls/Pasted-image-20240528112029.png?rlkey=25qf0lhe33ujpgtqrp62yvpd0&st=bdkqo7wg&dl=0)

We've intercepted our request and we'll send it to repeater and inject our payload

### ABOUT ORDER BY:

' ORDER BY 1-- ' ORDER BY 2-- ' ORDER BY 3-- etc.
used to determine the number of columns

`The ORDER BY position number 3 is out of range of the number of items in the select list.`

- The column in an `ORDER BY` clause can be specified by its index, so you don't need to know the names of any columns.
- When the specified column index exceeds the number of actual columns in the result set, the database returns an error, such as:

Since we know at least 2 columns are present in the table let's try order by 3

use ctrl + u for url encoding

![](https://dl.dropbox.com/scl/fi/mz1bx13gq4g17b2y3kgk3/Pasted-image-20240528112609.png?rlkey=sp7v30fo5b9ia9l6tc2vn0cu0&st=kbaasmem&dl=0)

we got a internal server error that means only 2 columns are present now let's focus on retrieving version number  

Let's explore union attacks a bit 

- results of the query are returned within the application's responses, you can use the `UNION` keyword to retrieve data from other tables within the database. This is commonly known as a SQL injection UNION attack.
- The `UNION` keyword enables you to execute one or more additional `SELECT` queries and append the results to the original query

`SELECT a, b FROM table1 UNION SELECT c, d FROM table2`

This SQL query returns a single result set with two columns, containing values from columns `a` and `b` in `table1` and columns `c` and `d` in `table2`.

For a `UNION` query to work, two key requirements must be met:

- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.

since the product and description is i strings format we can perform a union attack here  , let's focus on building a payload now 

SELECT banner FROM v$version

so our payload will be `'UNION SELECT banner, NULL FROM v$version--`

so i injected my payload and boom!

![](https://dl.dropbox.com/scl/fi/akvly9ts8mm9x4r0mcbke/Pasted-image-20240528113754.png?rlkey=bgcicoqoes065af78dcdya966&st=ppl8wew0&dl=0)

we displayed the version number on the website

![](https://dl.dropbox.com/scl/fi/s5sn15s9w3tqcw2n8y5ye/Pasted-image-20240528113833.png?rlkey=b9ua2edm8a9cjbbxgz5fsvzp5&st=6o5h7ssj&dl=0)