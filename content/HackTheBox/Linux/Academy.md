+++
title = 'Academy'
date = 2024-07-19T14:09:37+05:30
slug = "HTB-Academy"
categories = ["hackthebox","Academy","linux","Easy"]
+++


Starting with Nmap
![](https://drive.google.com/file/d/1sCQX3MNkfCZ4rNc2L8K1VxFpynRx0sJu/view?usp=sharing)


we won't be able to connect to the website using only ip address so we can access the website after adiing the website in /etc/hosts

![](https://drive.google.com/file/d/1GuLKw8od2OJGeH_XvUcYMVS744OBCR_6/view?usp=sharing)

The POST request to register a new user is interesting:

![](https://drive.google.com/file/d/1QuY2o3TOeyhBcLKwFDl5PU5AhFOBcJ3F/view?usp=sharing)


While the `uid` (user id) and double password fields are expected, `roleid` is interesting. I’ll register again, but this time I’ll use Burp proxy to intercept the POST and change `roleid` to 1.

![](https://drive.google.com/file/d/1qDiMrxbu4EQy_bmL7qvNkBK6w74SufjN/view?usp=sharing)

after changing the role everythign works same but this time it logged in to admin panel 

here's the homepage of dev-staging-01
![](https://drive.google.com/file/d/1rj1LUuPLBGB-qHjWma7LobLj97oS_Miy/view?usp=sharing)


![](https://drive.google.com/file/d/1gl3FOheWe20gozr2-xwAR7_r3ELGbLly/view?usp=sharing)

we found the app name and app key 

google search about larvel exploit led e to this
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/laravel

there are exploits in github where we can clone them and exploit them on the ip directly

after a bit of research i've found this 
https://www.rapid7.com/db/modules/exploit/unix/http/laravel_token_unserialize_exec/

i fired up msfconsole ot use the exploit
![](https://drive.google.com/file/d/1wSpn7n08tOPyfHdYNrE-CDl9SWS_gRtn/view?usp=sharing)

after setting Rhost Lhost options and running we got a terminal
![](https://drive.google.com/file/d/1hDOfMNxUdd2SsCP6fO8wv8aoSU31HAvz/view?usp=sharing)

we used python3 -c 'import pty;pty.spawn("bash")' to beautify the terminal 

![](https://drive.google.com/file/d/1wEVe89Yv2mKiho5pr2AzPOf2nxix6uQm/view?usp=sharing)

from the above we can login with user cry0l1t3
`cr0l1t3` user was a member of the `adm` group. On a typical Linux system, this group is responsible for system administration and, notably, monitoring.
so loggedin with cry0l1t3 user and got the user flag
![](https://drive.google.com/file/d/1yewK6ByVWRfTcMTGx_eIFLf5Gv9_kbnY/view?usp=sharing)

using log inspection tool using the `aureport` tool I was able to find credentials for the `mrb3n` user

![](https://drive.google.com/file/d/1sDLPaaNYdUmOb0NHMd7O7NZ3mRDTzA3Z/view?usp=sharing)


i logged in with mrb3n user and run the comamnds

TF=$(mktemp -d)
echo '{"scripts":{"x":"/bin/sh -i 0<&3 1>&3 2>&3"}}' >$TF/composer.json
sudo composer --working-dir=$TF run-script x

/bin/sh -i 0<&3 1>&3 2>&3

i got root access and got the rootflag

![](https://drive.google.com/file/d/1SW2cRFumtev9anARZN5Nsx60DibBFSaw/view?usp=sharing)


i pwned the machine 

