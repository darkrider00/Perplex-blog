+++
title = 'File Path Traversal Simple Case'
date = 2024-07-19T16:19:46+05:30
slug = "portswigger-filepath-traversal"
categories = ["portswigger","traversal","simple case"]
+++

Lab URL :
https://0ac7003b03b289fd80483a4d00050045.web-security-academy.net/

![file path 1](https://dl.dropbox.com/scl/fi/sbhjvs4a6qsuux87y3mgr/Pasted-image-20240514185624.png?rlkey=lpdn8fof8ux1lpgjo815qilnf&st=ec65qz7f&dl=0)

This lab objective is to  read /etc/passwd file from the url 
![file path 2](https://dl.dropbox.com/scl/fi/yrbpljg953p29tqwh0v1b/Pasted-image-20240514185739.png?rlkey=xfxsacqc9o4d95dlvegzu6e3p&st=9sezratp&dl=0)

![file path 3](https://dl.dropbox.com/scl/fi/nsht5hi4jnhnakgbro85o/Pasted-image-20240514190029.png?rlkey=t4ehh5q8lszfkoix8ghqpxsrl&st=5hgt1uen&dl=0)

we can click on view item to get the more details about the product and if we look at the url :
```
https://0ac7003b03b289fd80483a4d00050045.web-security-academy.net/product?productId=1
```
but the parameter should be filename if we want to inject the payload so let's open a image in new tab 
![file path 4](https://dl.dropbox.com/scl/fi/nfzv2hgir27rqck13mq72/Pasted-image-20240514190534.png?rlkey=tjwm9j0u4o722mragmrmyc7rv&st=g8o2d2io&dl=0)

if we look at the url now :
```
https://0ac7003b03b289fd80483a4d00050045.web-security-academy.net/image?filename=38.jpg
```
since we have a filename as a parameter we can use ../../../etc/passwd 
but before that let's change the file number and see if can we get a different image 
![file path 5](https://dl.dropbox.com/scl/fi/ykyvyr3ovmsr3ok4h0s1n/Pasted-image-20240514190736.png?rlkey=3uktgijn5zy593dqlubsosm36&st=30ko0xw0&dl=0)

here we changed the filename from 38.jpg to 30.jpg here we can access another files by changing the parameter values in the URL

so now let's try our payload `../../../etc/passwd` to read the password file 
![file path 6](https://dl.dropbox.com/scl/fi/o8tec6v067o4t19emsf8q/Pasted-image-20240514191137.png?rlkey=zhrd7ev57w1gk5ivf1wzzi89d&st=gaqggvrp&dl=0)

we got nothing so there might be some kind of input sanitization here so instead of giving a indirect path to the file let's directly specify `/etc/passed` to get access to the file

![file path 7](https://dl.dropbox.com/scl/fi/zf8zsdya2fmtmvuuds3qn/Pasted-image-20240514192015.png?rlkey=qev90wejla79fduqw26z14y6z&st=diouton0&dl=0)

if we want to view the file we need to intercept this request using burp suite

![file path 8](https://dl.dropbox.com/scl/fi/vgeds5unxu4ctbu81zc0h/Pasted-image-20240514192543.png?rlkey=rrlhpgdux00fplr94gd54bhy2&st=5xytxu2p&dl=0)

we have our request captured in the burpsuite repeater
let's inject our payload

![file path 9](https://dl.dropbox.com/scl/fi/d21tlwqw1m3j854m2qx45/Pasted-image-20240514192759.png?rlkey=ojjyrfd4avdhdriq76b9kjd7b&st=jb4duhfa&dl=0)

as we can see we are able to view all files that we shouldn't access

for more information refer : https://youtu.be/Wt0gk05MBz0
