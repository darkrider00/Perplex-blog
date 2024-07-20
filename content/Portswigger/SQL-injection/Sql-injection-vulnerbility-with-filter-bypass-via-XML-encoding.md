+++
title = 'Sql Injection Vulnerbility With Filter Bypass via XML Encoding'
date = 2024-07-20T12:34:30+05:30
slug = "portswigger-SQL-injection-vulnerbility-bypass-XML-encoding"
categories = ["portswigger","SQL injection","XML encoding"]
+++

![](https://drive.google.com/file/d/1270pepJqssVhmOKOZ8Jxjvqx2RxBb4MU/view?usp=sharing)

The above image is lab description
from the above description 
-  we know that there is a database that contains username and password 
- to solve the lab we have to retrieve the username and password and login to their account.

Let's take a look at the hint 
## hint
`A web application firewall (WAF) will block requests that contain obvious signs of a SQL injection attack. You'll need to find a way to obfuscate your malicious query to bypass this filter. We recommend using the [Hackvertor](https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100) extension to do this.`

the website :

![](https://drive.google.com/file/d/1sV72o-t9d4DBYuCWxAfHECgUOb2XPfUZ/view?usp=sharing)

I've turned on the burp proxy now let's navigate through the website.
let's check for inputs fields in the website for sql injection 

![](https://drive.google.com/file/d/1Dwih_iWh-pO1Vamkgv0rVrHpO3JjCRFp/view?usp=sharing)

here there is a input field if we click on view details of any product 

now let's take a look at http history that is recorded in the burpsuite

![](https://drive.google.com/file/d/1BXQ1cOHx5mBNpdDCENXSN0JgjfsB2i3b/view?usp=sharing)

here the server is requesting the product id and it is communicating with back so let's send this to repeater .

![](https://drive.google.com/file/d/14dLiwrQghdHzbIB5wSAOdIa6wi6HGjTE/view?usp=sharing)


![](https://drive.google.com/file/d/1qGzar8NT13Azx98U48hff25_swAO1JYv/view?usp=sharing)

here's when we click on check stock then we are getting the number units present at that location we can definitely inject some payloads here
 let's send this to repeater too 
 
![](https://drive.google.com/file/d/1LLrYnkqSgoJAcIrv0CjNzpeHiVOIr_SR/view?usp=sharing)

in this when we input the product id we are getting number of units present
 let's add `UNION SELECT NULL` to product id to determine number of columns.

![](https://drive.google.com/file/d/1aRpq4kEkhM4M0PtBaepvyw7TqmAG76iO/view?usp=sharing)

we got attack detected that's why they gave us a hint about WAF in the hint section

- we need to obfusacate the input so that it will bypass the firewall , we need to install hackvetor extension to install hackvector extension  go to extensions tab and go to bwapp store and search for hackvector extension as mentioned in [[SQL injection with filter bypass via XML encoding#hint]]
or you can encode manually refer  to the last section 

![](https://drive.google.com/file/d/1jK6Qn0tVoZ4eXVUXVvlMKM0NpIK_nFXo/view?usp=sharing)

- click on install to install the hack vector extension 
- for more information on the hack vector extension refer [[Hackvector extension]]

![](https://drive.google.com/file/d/1vXsB4UamHAZBVrBVbhX5vcazd3HRlzqk/view?usp=sharing)

as we can see hack vector extension has been installed and loaded we can see it in the repeater section
- to use the hackvector select the payload you've already written and right click on it and select extensions and select encode using hex entities and then send the request.

![](https://drive.google.com/file/d/1X9hzTmHDj3-Ti-7czo75NvoHnuucHKLT/view?usp=sharing)

as you can see hex entities tags are added to the payload we've selected 

![](https://drive.google.com/file/d/1_6z3y-D2ugrYeUot0LbgdHIIfo3pre9g/view?usp=sharing)

and Boom !

![](https://drive.google.com/file/d/1p5PMa_C5LkQ15g7sNlBqcPA6YVu6igU4/view?usp=sharing)

we dind't get any attack detected in the response tab 
we successfully bypassed the WAF with this extension 
- now let's add another null to the statement to see if there are 2 columns 
- we can add ORDER by 2 or ORDER by 3 to determine the colums 

![](https://drive.google.com/file/d/13LX4LNRMV79PSf8QTfBMJ7lUfHh_9pW0/view?usp=sharing)

![](https://drive.google.com/file/d/15z71JLBPPtOngwMZt63p14bqZwakVI6w/view?usp=sharing)


![](https://drive.google.com/file/d/1PQg_OWubXMgHSdcs4dMd28gimXwGtX8V/view?usp=sharing)
we got 0 units that means only one column is present in the table 

let's build  a payload now to retrieve the username and password table 

`1 UNION SELECT username || '~' || password FROM users`

- let's breakdown this payload we've built union select is used to select and we are selecting username 
-  **`||`**: This is the string concatenation operator in SQL (specifically in databases like SQLite and PostgreSQL). It concatenates two or more strings.
- **`'~'`**: This is a tilde character being used as a delimiter (to separate username and password)
- and passwords from table users

![](https://drive.google.com/file/d/1a8qgKWDu-GToWSaUHYiuWn3JII0eGryr/view?usp=sharing)

we got our username and passwords 

in this lab we are looking for admin account so let's login with these details 

![](https://drive.google.com/file/d/1EFRIrhC4WoWRy0hOl7PtV7A7UgNwbHns/view?usp=sharing)

we are logged in and we solved the lab 

for more detailed walkthrough : https://youtu.be/2iqMm0gMyHk


## Alternative encoding
in this encoding we use online tools like cyberchef 
maybe something like this 
![](https://drive.google.com/file/d/1wmtVYkEVrkApxSxrN24zj5gTJ9wEJcUj/view?usp=sharing)

