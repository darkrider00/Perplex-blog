+++
title = 'Sequel'
date = 2024-07-19T16:05:20+05:30
slug = "HTB-sequel"
categories = ["hackthebox","Sequel","linux","very Easy","Starting point","tier 1"]
+++

TASK 1

During our scan, which port do we find serving MySQL?

![sequel 1](https://dl.dropbox.com/scl/fi/t5duqtvdnpasbz5oqq2jp/Pasted-image-20240531104612.png?rlkey=fizgb9d6sotjzmor3soo63t4s&st=58ynm0gg&dl=0)

on port 3306 mysql is running 


TASK 2

What community-developed MySQL version is the target running?
Ans: Maria DB

TASK 3

When using the MySQL command line client, what switch do we need to use in order to specify a login username?

![sequel 2](hhttps://dl.dropbox.com/scl/fi/ulmglojj2n5zvh8b1fbu3/Pasted-image-20240531105451.png?rlkey=fcue3ns9p5um2ue2duuvxzcnn&st=j7tr55xd&dl=0)

![sequel 3](https://dl.dropbox.com/scl/fi/xpmy0mwzgvijc7ij3yvg9/Pasted-image-20240531105851.png?rlkey=48712sbyhda6nngbub85grlgl&st=ta9e6l23&dl=0)

using the mysql manual page now we know that -h is used to connect to a host  and -u used to specify the username

TASK 4

Which username allows us to log into this MariaDB instance without providing a password?
Ans: root

TASK 5

In SQL, what symbol can we use to specify within the query that we want to display everything inside a table?
Ans : *

TASK 6

In SQL, what symbol do we need to end each query with?
Ans: ;

TASK 7

There are three databases in this MySQL instance that are common across all MySQL instances. What is the name of the fourth that's unique to this host?
https://www.mysqltutorial.org/mysql-cheat-sheet/ refer to this for more detailed information

![sequel 4](https://dl.dropbox.com/scl/fi/v3n8esak1i5vrkln6hu47/Pasted-image-20240531123043.png?rlkey=zhwrwk6oac0kc8rdetu7ziih4&st=cq0ps4s6&dl=0)

we are in now let's continue

![sequel 5](https://dl.dropbox.com/scl/fi/ntglot928koxpl1sqp5a8/Pasted-image-20240531123247.png?rlkey=bt70hvfe3ccmti524kk2j8puq&st=udyf179j&dl=0)

the database unique to this host is htb let's use htb 

![sequel 6](https://dl.dropbox.com/scl/fi/ibhuunvmrfk09jqo9maux/Pasted-image-20240531123547.png?rlkey=tig2xku0smxzgbu23nph1vra7&st=32h2olwf&dl=0)

Submit root flag
Ans: 7b4bec00dla39************