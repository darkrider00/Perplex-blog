+++
title = 'Crafty'
date = 2024-07-19T16:11:07+05:30
slug = "HTB-crafty"
categories = ["hackthebox","crafty","windows","Easy"]
+++


machine IP : 10.10.11.249
startign with the nmap scan 
![](https://drive.google.com/file/d/1dCxQBM7ZfSkuKbAhwQYfLhO3geAZyqcQ/view?usp=sharing)

let's do another namp scan with all ports to see if we can get any info

![](https://drive.google.com/file/d/1g7dIaCGwwR0zObna-wzR5SHla7H7OZCl/view?usp=sharing)
we've found that 25565 port is open let's focus on gathering more info 

add the ip to /etc/hosts to access the ip 
![](https://drive.google.com/file/d/1YgCUztSUxnt8WjKlBqpYV_TFNluMC3lD/view?usp=sharing)

![](https://drive.google.com/file/d/11TlX19Cz_B7xWxoAlP2mI4V_FZ30QMUs/view?usp=sharing)

the above result is the result of wappalyzer extension for the website 
let's explore the website 

![](https://drive.google.com/file/d/1xtX_mXulp45kHHcMNiRXnc4Aa9Ri1Pq0/view?usp=sharing)

website dashboard 
every option we click is being redirected to comming soon webpage 
we've have dound another subdomain play.crafty.htb let's do subdomain enum to find any sub domains

![](https://drive.google.com/file/d/1o2bgl6Qra9E67vu2qYoBrnoHXOBwKLh5/view?usp=sharing)

I haven't found anything intresting in the home page of that website but in the coming soon webpage i've found 
![](https://drive.google.com/file/d/1-7J1pd-mHAZZ_Q8abLefrNP5yearhxdd/view?usp=sharing)

![](https://drive.google.com/file/d/1Hkf2ouoPcYWvRh-pEJS3p1840k89ASBj/view?usp=sharing)

the abpve result is a gobsuter scan result we haven't found anything intresting let's try some directories since we've found some info in comments 
![](https://drive.google.com/file/d/1kij_j5a4y6UdN6X4UwXxWqHs8tKE-4fD/view?usp=sharing)

Intresting , we've got 403 error saying we don't have access to go that directory

when i searched about port 25565 i got the result saying it's minecraft default port
![](https://drive.google.com/file/d/1OHme-jYbkIKne0OO09g6MlGeDMd068fw/view?usp=sharing)

since we got a port let's connect to multiplayer with the machine ip and port number and see what happens

from the nmap scan result i searched for Minecraft vulnerabilities of that version and i found this
![](https://drive.google.com/file/d/1UNGVdmTp7SnII19wBI_3kytAnVj_EmSt/view?usp=sharing)

![](https://drive.google.com/file/d/1dY7O6rFrXUXNCt7lAttCLSsR2kEr1EWv/view?usp=sharing)

![](https://drive.google.com/file/d/1kCdDdTvfjqpPTOtcd4Ybfsrg3_f28l3x/view?usp=sharing)

![](https://drive.google.com/file/d/1rlCsaex8ljrfjQp7t9ikzxrhidDX1h6_/view?usp=sharing)

