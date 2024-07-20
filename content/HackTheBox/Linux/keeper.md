+++
title = 'Keeper'
date = 2024-07-19T15:17:35+05:30
slug = "HTB-Keeper"
categories = ["hackthebox","Keeper","linux","Easy"]
+++

Starting with a nmap scan we have this result 
![](https://drive.google.com/file/d/1gfZmm746r0M7ReG_13L6nuSyq8JnrdzG/view?usp=sharing)

When we access the IP address on port 80 via a browser, we can see there is just one link which redirects to `tickets.keeper.htb/rt`. But in order to do that we need to add this IP to our `/etc/hosts` file

10.129.122.221  tickets.keeper.htb  
10.129.122.221  keeper.htb

![](https://drive.google.com/file/d/1Y9ir6hnhiKsthcjVWRmTKT-GNogXgoyc/view?usp=sharing)

i've ried some default passweords and dource code but it wasn't helpful

i've googled and searched in exploit db but found no exploit mentioned in the web page 
![](https://drive.google.com/file/d/1oQ64F-EfFNm0E_IKF-KcRYCtKYd5wrbW/view?usp=sharing)

so i searched for default creds for Request tracker 

![](https://drive.google.com/file/d/1oQ64F-EfFNm0E_IKF-KcRYCtKYd5wrbW/view?usp=sharing)

![](https://drive.google.com/file/d/1sDWPxVk29JZysa8z7WjbsQPzNJAXDvET/view?usp=sharing)

i got loggedin using the default credentials

in the users section i've found lnorgaard user and also a intial password Welcome2023!

![](https://drive.google.com/file/d/1Hqe9dAg9I7xKsgOZxWpyOHmxuLrc8Ou0/view?usp=sharing)

![](https://drive.google.com/file/d/13oX7PzgjJlpTgf85B0ei4aIna9GOWodR/view?usp=sharing)

so i logged into ssh and found the user flag 
![](https://drive.google.com/file/d/1YLU0rdQlYb5k2xiOL3l2Nd7k4DOCV-ZM/view?usp=sharing)

after that we can see a zip file if we extract we get 2 files
![](https://drive.google.com/file/d/14_On5zCgm-gRP3o4Bk6mbJToK_eI10WZ/view?usp=sharing)

a simple google search led me to this vulnerability
![](https://drive.google.com/file/d/15VaJcYH9ewl8W7FkeyEyXVxnMu7V0nHH/view?usp=sharing)



in the repo we can see this
![](https://drive.google.com/file/d/1hYtUtwmBnue0dIdLI4MlvzN_cfTNk7n5/view?usp=sharing)

to install .net refer here
https://learn.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual#scripted-install

![](https://drive.google.com/file/d/14zD88e6G7VdwFsiuzzl5WGhblRijzdsj/view?usp=sharing)
after using dotnet run dmp file i got the  password 
**dgrød med fløde**.’

after searching this password in google  evry result contained rod med flode so the password must be tht 
![](https://drive.google.com/file/d/17BKaTVQwPfHuVOMKq0u2ozLfOPcWy0qu/view?usp=sharing)

after installing keypass2 in my windows i open passwords.kdbx file with keypass2 
 with password rød med fløde
![](https://drive.google.com/file/d/1mlZ6GT4omyLwh4sO2-B4ItaRRkBKWetu/view?usp=sharing)

i got logged in 
![](https://drive.google.com/file/d/1kPT35Ua4nh3EXBKAvj7Z-2T207JVCvUN/view?usp=sharing)


here after refering to root user notes i found 
![](https://drive.google.com/file/d/1A3WtIJ3xavg_8JETT9YksvruVLMBMo6t/view?usp=sharing)


Instead of Passkey2 we can use kpcli 

which is a putty user file  by searching in google Putty-User-Key-File-3
i found this website 
https://www.baeldung.com/linux/ssh-key-types-convert-ppk

![](https://drive.google.com/file/d/1Wm81J2OrNqf3Duc9sU5ngfL5wHP21z7f/view?usp=sharing)

![](https://drive.google.com/file/d/1sPg-qOGfkR6XZbk1FxVtkxcFi8-0EcUs/view?usp=sharing)

.ppk file can be converted into id_rsa private key through which we can login ssh with this key 


![](https://drive.google.com/file/d/1g3sAu6b94oTqUl_C3dAyIN2ydzQT5CPp/view?usp=sharing)


i got the root access key is present in root.txt

![](https://drive.google.com/file/d/1Bzf1sN5LOcihBtYRh4Gm5mofAZvMUc04/view?usp=sharing)

machine is pwned 


For using Kpcli refer to 
https://github.com/rebkwok/kpcli
https://kpcli.sourceforge.io/
https://youtu.be/0AafRQIaWmQ?feature=shared

from here you can get the same putty- user key i got with  keypass2 and convert this into rsa private key gen file and log in to ssh and get root access