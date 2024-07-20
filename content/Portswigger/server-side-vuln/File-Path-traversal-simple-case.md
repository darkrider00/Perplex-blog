+++
title = 'File Path Traversal Simple Case'
date = 2024-07-19T16:19:46+05:30
slug = "portswigger-filepath-traversal"
categories = ["portswigger","traversal","simple case"]
+++

Lab URL :
https://0ac7003b03b289fd80483a4d00050045.web-security-academy.net/

![](https://drive.google.com/file/d/1cVhoXynIx_MmY7AIf6VmE_sF3f7SZBEY/view?usp=sharing)

This lab objective is to  read /etc/passwd file from the url 
![](https://drive.google.com/file/d/1cFT6Q5TIxWtKnmxRSr16Y0-JDpU9E6x-/view?usp=sharing))

![](https://drive.google.com/file/d/1QjVMxr-joGVVO-7Qv6pAk-BanSQP05AO/view?usp=sharing)

we can click on view item to get the more details about the product and if we look at the url :
```
https://0ac7003b03b289fd80483a4d00050045.web-security-academy.net/product?productId=1
```
but the parameter should be filename if we want to inject the payload so let's open a image in new tab 
![](https://drive.google.com/file/d/1QjVMxr-joGVVO-7Qv6pAk-BanSQP05AO/view?usp=sharing)

if we look at the url now :
```
https://0ac7003b03b289fd80483a4d00050045.web-security-academy.net/image?filename=38.jpg
```
since we have a filename as a parameter we can use ../../../etc/passwd 
but before that let's change the file number and see if can we get a different image 
![](https://drive.google.com/file/d/1X2E0ZsJGVlXB86bZIuORLD4Ygv9uecDI/view?usp=sharing)

here we changed the filename from 38.jpg to 30.jpg here we can access another files by changing the parameter values in the URL

so now let's try our payload `../../../etc/passwd` to read the password file 
![](https://drive.google.com/file/d/1ZbFmiOHUkcWC20bZ-OLVQs43NTAvt537/view?usp=sharing)

we got nothing so there might be some kind of input sanitization here so instead of giving a indirect path to the file let's directly specify `/etc/passed` to get access to the file

![](https://drive.google.com/file/d/1KQ_9nP4NuqjC2u8qcg384m1jXIsofgi1/view?usp=sharing)

if we want to view the file we need to intercept this request using burp suite

![](https://drive.google.com/file/d/1txfPxzsIY_TJ2PCsLNtood25TakEoCUd/view?usp=sharing)

we have our request captured in the burpsuite repeater
let's inject our payload

![](https://drive.google.com/file/d/1MKQn-ikvv9N2x1a96PWr9OAQqQ9aJIe0/view?usp=sharing)

as we can see we are able to view all files that we shouldn't access

for more information refer : https://youtu.be/Wt0gk05MBz0
