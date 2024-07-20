+++
title = 'Academy'
date = 2024-07-19T14:09:37+05:30
slug = "HTB-Academy"
categories = ["hackthebox","Academy","linux","Easy"]
+++


Starting with Nmap
![academy 1](https://dl.dropbox.com/scl/fi/fqp4hq89ijjlcifcw6gol/Pasted-image-20240331223815.png?rlkey=oyet4dj9nvzfsmqij9i10ls8d&st=yha42nhs&dl=0)


we won't be able to connect to the website using only ip address so we can access the website after adiing the website in /etc/hosts

![academyn 2](https://dl.dropbox.com/scl/fi/w3e7n2yngicpzlj14lkar/Pasted-image-20240331223953.png?rlkey=6gvnlxl5ll9m4wxrevdsvvh30&st=ap403fdm&dl=0)

The POST request to register a new user is interesting:

![](https://dl.dropbox.com/scl/fi/3ydotg5te40jtunqco2iz/Pasted-image-20240331225045.png?rlkey=l3h0i9qs0qggx7parjvcu28s8&st=rwq9dg95&dl=0)


While the `uid` (user id) and double password fields are expected, `roleid` is interesting. I’ll register again, but this time I’ll use Burp proxy to intercept the POST and change `roleid` to 1.

![academy 3](https://dl.dropbox.com/scl/fi/vllspoynhb84wbuiq7qbm/Pasted-image-20240331225505.png?rlkey=iexfkh89h3x5d9aep398y64vq&st=5v3pxdka&dl=0)

after changing the role everythign works same but this time it logged in to admin panel 

here's the homepage of dev-staging-01
![academy 4](https://dl.dropbox.com/scl/fi/hp8pvnduywaou84pz7zjx/Pasted-image-20240331230121.png?rlkey=igx80780zip64fg115479pweu&st=50v6jgrv&dl=0)


![academy 5](https://dl.dropbox.com/scl/fi/57okovykk1m1av8fu6vu9/Pasted-image-20240331230200.png?rlkey=s3lok1bs9ne5828beuqwie7xz&st=5xwdnu74&dl=0)

we found the app name and app key 

google search about larvel exploit led e to this
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/laravel

there are exploits in github where we can clone them and exploit them on the ip directly

after a bit of research i've found this 
https://www.rapid7.com/db/modules/exploit/unix/http/laravel_token_unserialize_exec/

i fired up msfconsole ot use the exploit
![academy 6](https://dl.dropbox.com/scl/fi/xpjkef41t15nirzi4bx2y/Pasted-image-20240331232245.png?rlkey=6z7akybumyh9ftok3n7hg78n2&st=6jqbvauu&dl=0)

after setting Rhost Lhost options and running we got a terminal
![academy 7](https://dl.dropbox.com/scl/fi/u4cq5a2l8j8e47b1807ne/Pasted-image-20240331233056.png?rlkey=diuzhxh6qel7zsmwdv3kdlyf8&st=c629ddfe&dl=0)

we used python3 -c 'import pty;pty.spawn("bash")' to beautify the terminal 

![academy 8](https://dl.dropbox.com/scl/fi/3j8qygrm6c6yqpq3krcah/Pasted-image-20240331233910.png?rlkey=rpo8grrschi4arf56kbwch8wt&st=5j6do7me&dl=0)

from the above we can login with user cry0l1t3
`cr0l1t3` user was a member of the `adm` group. On a typical Linux system, this group is responsible for system administration and, notably, monitoring.
so loggedin with cry0l1t3 user and got the user flag
![academy 9](https://dl.dropbox.com/scl/fi/al16mvqc0frimdn1stmox/Pasted-image-20240331235258.png?rlkey=zm49m7f4zyp4iy17298d6p14b&st=y6d1i765&dl=0)

using log inspection tool using the `aureport` tool I was able to find credentials for the `mrb3n` user

![academy 10](https://dl.dropbox.com/scl/fi/terkqw2c38ej6s1cmg3kj/Pasted-image-20240331234551.png?rlkey=i0s660hwoemxthbsnjq4x1z1l&st=gch5s653&dl=0)


i logged in with mrb3n user and run the comamnds

TF=$(mktemp -d)
echo '{"scripts":{"x":"/bin/sh -i 0<&3 1>&3 2>&3"}}' >$TF/composer.json
sudo composer --working-dir=$TF run-script x

/bin/sh -i 0<&3 1>&3 2>&3

i got root access and got the rootflag

![academy 11](https://dl.dropbox.com/scl/fi/ddeawmahlyieh29wrf2sc/Pasted-image-20240331235459.png?rlkey=kx83umn6ytorjakg880r3hztt&st=6gedqq9b&dl=0)


i pwned the machine 

