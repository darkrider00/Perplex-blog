+++
title = 'Keeper'
date = 2024-07-19T15:17:35+05:30
slug = "HTB-Keeper"
categories = ["hackthebox","Keeper","linux","Easy"]
+++

Starting with a nmap scan we have this result 
![keeper 1](https://dl.dropbox.com/scl/fi/jmse8qqsnep6pm7toq5kd/Pasted-image-20240331145343.png?rlkey=za8vmpe5bvjpyibud396og19f&st=n3yqhzjf&dl=0)

When we access the IP address on port 80 via a browser, we can see there is just one link which redirects to `tickets.keeper.htb/rt`. But in order to do that we need to add this IP to our `/etc/hosts` file

10.129.122.221  tickets.keeper.htb  
10.129.122.221  keeper.htb

![keeper 2](https://dl.dropbox.com/scl/fi/imgu3dnru0tm17wg3lto9/Pasted-image-20240331145837.png?rlkey=vuxp9nitvwr4e18o095lkj8e4&st=b8ww9rmk&dl=0)

i've ried some default passweords and dource code but it wasn't helpful

i've googled and searched in exploit db but found no exploit mentioned in the web page 
![keeper 3](https://dl.dropbox.com/scl/fi/q3gm1mcdiih9mqbrlbct3/Pasted-image-20240331145751.png?rlkey=wpius0po5x4ql721cwz2ntxkl&st=adf44gh8&dl=0)

so i searched for default creds for Request tracker 

![keeper 4](https://dl.dropbox.com/scl/fi/xbwu3ue6ga0ru1m56mysz/Pasted-image-20240331150124.png?rlkey=b4qq3tztx0uch3jiu6wz3bca2&st=4ckqvyhx&dl=0)

![keeper 5](https://dl.dropbox.com/scl/fi/occlaa23exayalkkhc6u3/Pasted-image-20240331151500.png?rlkey=us6mbq6zsyne75fhvurm2rp4i&st=vltvmlw1&dl=0)

i got loggedin using the default credentials

in the users section i've found lnorgaard user and also a intial password Welcome2023!

![keeper 6](https://dl.dropbox.com/scl/fi/46k7qu0r4ugfmlnvf3rxf/Pasted-image-20240331151804.png?rlkey=25kakxp5m1rqtngos7n0x8znu&st=fwp9lebu&dl=0)

![keeper 7](https://dl.dropbox.com/scl/fi/cn7d8xo826gqff2bm6w4x/Pasted-image-20240331151945.png?rlkey=xnbwhrnhwwmw0s1ssrpr819pu&st=16zo85n1&dl=0)

so i logged into ssh and found the user flag 
![keeper 8](https://dl.dropbox.com/scl/fi/27n6il4e1uhgqhbk98tfl/Pasted-image-20240331152158.png?rlkey=dywcjyhrfq1iecb64h4kzs9mt&st=x9fasupx&dl=0)

after that we can see a zip file if we extract we get 2 files
![keeper 9](https://dl.dropbox.com/scl/fi/zkeklac6hkeqxjwlimn2m/Pasted-image-20240331152542.png?rlkey=4uedx7qimd9zdbtgjgxmovcer&st=j1ryat2a&dl=0)

a simple google search led me to this vulnerability
![keeper 10](https://dl.dropbox.com/scl/fi/lakoq11x3bx3hehej6ju9/Pasted-image-20240331152515.png?rlkey=iywrl60qoim2tnjmipwndztn3&st=g8dnmjso&dl=0)



in the repo we can see this
![keeper 11](https://dl.dropbox.com/scl/fi/r1co0eb9rdb0e42p7o0se/Pasted-image-20240331152725.png?rlkey=di3vu1vlwtpy2480vh8dkturq&st=8e98qszq&dl=0)

to install .net refer here
https://learn.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual#scripted-install

![keeper 12](https://dl.dropbox.com/scl/fi/mbrm8bl5snbxuflteto6r/Pasted-image-20240331153718.png?rlkey=5uqcg7z0e5l6v4kl95bsgytk0&st=chzom3pr&dl=0)
after using dotnet run dmp file i got the  password 
**dgrød med fløde**.’

after searching this password in google  evry result contained rod med flode so the password must be tht 
![keeper 13](https://dl.dropbox.com/scl/fi/n0t9fhgi76t8bsq0md0wu/Pasted-image-20240331164248.png?rlkey=dkvgmhuyvnbwx3jsit7ju8yck&st=mto9meze&dl=0)

after installing keypass2 in my windows i open passwords.kdbx file with keypass2 
 with password rød med fløde
![keeper 14](https://dl.dropbox.com/scl/fi/h7msw2jys13vi7fc35vcn/Pasted-image-20240331164429.png?rlkey=jhl1ajaexo7t24nu3ueo1hjtn&st=02j33t19&dl=0)

i got logged in 
![keeper 15](https://dl.dropbox.com/scl/fi/wqdav1tewr5h2pqaql0y7/Pasted-image-20240331164516.png?rlkey=8hy22cfwnfspk1h8ww9osp9q8&st=gn152zl3&dl=0)


here after refering to root user notes i found 
![keeper 16](https://dl.dropbox.com/scl/fi/1nz2vpx0erxy32jw2hpht/Pasted-image-20240331170848.png?rlkey=3qgvqrtzjx5r90wo5d1ta5g70&st=8q5pg02f&dl=0)


Instead of Passkey2 we can use kpcli 

which is a putty user file  by searching in google Putty-User-Key-File-3
i found this website 
https://www.baeldung.com/linux/ssh-key-types-convert-ppk

![keeper 17](https://dl.dropbox.com/scl/fi/g4bgniz3qgs7mpcoigrxr/Pasted-image-20240331171010.png?rlkey=sdkmdhwztfbryb5i00do9oukf&st=csz6g6jj&dl=0)

![keeper 18](https://dl.dropbox.com/scl/fi/wvr9rmhd2n2ra7mgiug6r/Pasted-image-20240331171137.png?rlkey=m3grpmb79ddny7fdg532te6kw&st=sfvgdwjy&dl=0)

.ppk file can be converted into id_rsa private key through which we can login ssh with this key 


![keeper 19](https://dl.dropbox.com/scl/fi/7rcb6yuzuyf8v1u9qshe1/Pasted-image-20240331170807.png?rlkey=wjyn0hfkvvmo7mc8y7v8k3e23&st=balddtgi&dl=0)


i got the root access key is present in root.txt

![keeper 20](https://dl.dropbox.com/scl/fi/aukbjwlk4hn9e2fdojku6/Pasted-image-20240331171331.png?rlkey=4zki4yvfpjc9nwfrtjcw1yily&st=tk6lv4m8&dl=0)

machine is pwned 


For using Kpcli refer to 
https://github.com/rebkwok/kpcli
https://kpcli.sourceforge.io/
https://youtu.be/0AafRQIaWmQ?feature=shared

from here you can get the same putty- user key i got with  keypass2 and convert this into rsa private key gen file and log in to ssh and get root access