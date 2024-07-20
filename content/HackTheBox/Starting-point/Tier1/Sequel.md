+++
title = 'Sequel'
date = 2024-07-19T16:05:20+05:30
slug = "HTB-sequel"
categories = ["hackthebox","Sequel","linux","very Easy","Starting point","tier 1"]
+++

TASK 1

During our scan, which port do we find serving MySQL?

![](https://drive.google.com/file/d/12xVmrJUrgRjRNlQDS9Vlc_1xRX6wNO0q/view?usp=sharing)

on port 3306 mysql is running 


TASK 2

What community-developed MySQL version is the target running?
Ans: Maria DB

TASK 3

When using the MySQL command line client, what switch do we need to use in order to specify a login username?

![](https://drive.google.com/file/d/1vzAmlDcfz2xiF6QWlt03f4SGgG_tNuxW/view?usp=sharing)

![](https://drive.google.com/file/d/1Rayf8x3pukO-z66KV81f61cFc0v1_Nwh/view?usp=sharing)

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

![](https://drive.google.com/file/d/1_7TTz2460VohNgktz7AxX5qgZbop6CRs/view?usp=sharing)

we are in now let's continue
![](https://drive.google.com/file/d/1YOEersDEFCLJmihyzkKDnNr5tJyRUZJH/view?usp=sharing)

the database unique to this host is htb let's use htb 
![](https://drive.google.com/file/d/1n05cKRVejtVI4xp1OOVsA11r1VRLiGD0/view?usp=sharing)

Submit root flag
Ans: 7b4bec00dla39************