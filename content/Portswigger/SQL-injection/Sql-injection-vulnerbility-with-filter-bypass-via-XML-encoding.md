+++
title = 'Sql Injection Vulnerbility With Filter Bypass via XML Encoding'
date = 2024-07-20T12:34:30+05:30
slug = "portswigger-SQL-injection-vulnerbility-bypass-XML-encoding"
categories = ["portswigger","SQL injection","XML encoding"]
+++

![](https://dl.dropbox.com/scl/fi/y8zqmanromsgx4p640qut/Pasted-image-20240527125758.png?rlkey=8qxh6t75jde05zy0zwbkuxibn&st=swjqpwf9&dl=0)

The above image is lab description
from the above description 
-  we know that there is a database that contains username and password 
- to solve the lab we have to retrieve the username and password and login to their account.

Let's take a look at the hint 
## hint
`A web application firewall (WAF) will block requests that contain obvious signs of a SQL injection attack. You'll need to find a way to obfuscate your malicious query to bypass this filter. We recommend using the [Hackvertor](https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100) extension to do this.`

the website :

![](https://dl.dropbox.com/scl/fi/mi7yr7gvnizdyxmd3cbhb/Pasted-image-20240527125821.png?rlkey=a3ioeswaga7tvy3afbmvldtn2&st=yhor7rk6&dl=0)

I've turned on the burp proxy now let's navigate through the website.
let's check for inputs fields in the website for sql injection 

![](https://dl.dropbox.com/scl/fi/pgd2ofal3jstk3s8momuv/Pasted-image-20240527125921.png?rlkey=8a5zlstj1t2abzohyg3rjejys&st=5wqq8r04&dl=0)

here there is a input field if we click on view details of any product 

now let's take a look at http history that is recorded in the burpsuite

![](https://dl.dropbox.com/scl/fi/2nkdb56fb6ijmm617v1xw/Pasted-image-20240527114009.png?rlkey=x8i2e03jp1xclkb66264yg9vt&st=82r5ttiv&dl=0)

here the server is requesting the product id and it is communicating with back so let's send this to repeater .

![](https://dl.dropbox.com/scl/fi/d1ohzs6b2xxtawbpk28xh/Pasted-image-20240527114215.png?rlkey=yvf1awvwmu71yr3q2p28ky2yg&st=8t018h82&dl=0)


![](https://dl.dropbox.com/scl/fi/84ugjxvfljxp6ehy84mhy/Pasted-image-20240527114334.png?rlkey=yk5hxpatfon1msyzrzdvsssx7&st=hdno3ph4&dl=0)

here's when we click on check stock then we are getting the number units present at that location we can definitely inject some payloads here
 let's send this to repeater too 
 
![](https://dl.dropbox.com/scl/fi/45jxdnosu05hm4nty28rs/Pasted-image-20240527115321.png?rlkey=tnfnva2q0zql2puhrj6gjxswq&st=szz0g9yl&dl=0)

in this when we input the product id we are getting number of units present
 let's add `UNION SELECT NULL` to product id to determine number of columns.

![](https://dl.dropbox.com/scl/fi/ao9v53aoxfr01mnevflab/Pasted-image-20240527115659.png?rlkey=afkjjwbmlab6eih07ifrmwyro&st=nd36beue&dl=0)

we got attack detected that's why they gave us a hint about WAF in the hint section

- we need to obfusacate the input so that it will bypass the firewall , we need to install hackvetor extension to install hackvector extension  go to extensions tab and go to bwapp store and search for hackvector extension as mentioned in [[SQL injection with filter bypass via XML encoding#hint]]
or you can encode manually refer  to the last section 

![](https://dl.dropbox.com/scl/fi/wrsyi7elseqb0ditxi2zx/Pasted-image-20240527120459.png?rlkey=ogqp378ct7n5kans24r9b8oer&st=uaepk5rr&dl=0)

- click on install to install the hack vector extension 
- for more information on the hack vector extension refer [[Hackvector extension]]

![](https://dl.dropbox.com/scl/fi/mvrslhfbooabif1nki5fp/Pasted-image-20240527121136.png?rlkey=zbb99leilf6zlfjnudcx3loum&st=bvmayoes&dl=0)

as we can see hack vector extension has been installed and loaded we can see it in the repeater section
- to use the hackvector select the payload you've already written and right click on it and select extensions and select encode using hex entities and then send the request.

![](https://dl.dropbox.com/scl/fi/tt13eoyyakfj53a0k1slf/Pasted-image-20240527121548.png?rlkey=q6ew7arx5p7xjaft7f53uq44b&st=iq7qfy4q&dl=0)

as you can see hex entities tags are added to the payload we've selected 

![](https://dl.dropbox.com/scl/fi/ci669n9iyb8d8bnt62ob1/Pasted-image-20240527121619.png?rlkey=r0fjm3jg0ozmx9xxyk9r7y8lq&st=3yc0eos3&dl=0)

and Boom !

![](https://dl.dropbox.com/scl/fi/go5m887ptdoybuni0ht8l/Pasted-image-20240527122135.png?rlkey=4hrf7oxrmayhbnvjmehnlwbtw&st=biq1d89x&dl=0)

we dind't get any attack detected in the response tab 
we successfully bypassed the WAF with this extension 
- now let's add another null to the statement to see if there are 2 columns 
- we can add ORDER by 2 or ORDER by 3 to determine the colums 

![](https://dl.dropbox.com/scl/fi/osfbdosez2qkvrwiqpbbz/Pasted-image-20240527123937.png?rlkey=0gf9d1gtaumfjaix3eseny755&st=rhr8fpj7&dl=0)

![](https://dl.dropbox.com/scl/fi/barmwisjc6v7pgg41be4t/Pasted-image-20240527124037.png?rlkey=saer2mtkimn84hx0aubbsxblu&st=qce7n2i2&dl=0)


![](https://dl.dropbox.com/scl/fi/q0zqxo54p31glrnpsu9cg/Pasted-image-20240527122405.png?rlkey=h3e0qnmj7kxbgpg5ocnn052hz&st=5g1v80vo&dl=0)

we got 0 units that means only one column is present in the table 

let's build  a payload now to retrieve the username and password table 

`1 UNION SELECT username || '~' || password FROM users`

- let's breakdown this payload we've built union select is used to select and we are selecting username 
-  **`||`**: This is the string concatenation operator in SQL (specifically in databases like SQLite and PostgreSQL). It concatenates two or more strings.
- **`'~'`**: This is a tilde character being used as a delimiter (to separate username and password)
- and passwords from table users

![](https://dl.dropbox.com/scl/fi/24zbfcsj4pbxtr2x39yyy/Pasted-image-20240527122849.png?rlkey=31o7o7oqdz1j2xelyq130ayr1&st=2n2fwe24&dl=0)

we got our username and passwords 

in this lab we are looking for admin account so let's login with these details 

![](https://dl.dropbox.com/scl/fi/g6mpo93n9buroiua1fgck/Pasted-image-20240527123358.png?rlkey=rudg9g8xs8e8m9g26uvi12kg0&st=elnj3r32&dl=0)

we are logged in and we solved the lab 

for more detailed walkthrough : https://youtu.be/2iqMm0gMyHk


## Alternative encoding
in this encoding we use online tools like cyberchef 
maybe something like this 

![](https://dl.dropbox.com/scl/fi/0izimf7m3hjcmen8hdoau/Pasted-image-20240527131254.png?rlkey=xjyn3dov9r2amewn93pqk1cva&st=28sm5ko2&dl=0)

