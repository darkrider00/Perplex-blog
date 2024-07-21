+++
title = 'Crafty'
date = 2024-07-19T16:11:07+05:30
slug = "HTB-crafty"
categories = ["hackthebox","crafty","windows","Easy"]
+++


machine IP : 10.10.11.249
startign with the nmap scan 
![crafty 1](https://dl.dropbox.com/scl/fi/t5ccmlx0ipwkmkqbwfufc/Pasted-image-20240507083146.png?rlkey=u712vex7qf9sdmjltshjb9g48&st=rvey4qyy&dl=0)

let's do another namp scan with all ports to see if we can get any info

![crafty 2](https://dl.dropbox.com/scl/fi/1ed6l8e6p9m0owfoy9tep/Pasted-image-20240507084552.png?rlkey=jkntjmerp3qtjyc5r193dv408&st=3m1x5j2y&dl=0)
we've found that 25565 port is open let's focus on gathering more info 

add the ip to /etc/hosts to access the ip 
![crafty 3](https://dl.dropbox.com/scl/fi/byem7bahsbde3mwdxzzhn/Pasted-image-20240507083257.png?rlkey=xii73wshvbyol9fkama7thmkx&st=beh13iot&dl=0)

![crafty 4](https://dl.dropbox.com/scl/fi/tg2qzuyz7fh0ah53ljhxp/Pasted-image-20240507083404.png?rlkey=1xp72ehwv97fcpi4ejcgrilil&st=gqwu2tos&dl=0)

the above result is the result of wappalyzer extension for the website 
let's explore the website 

![crafty 5](https://dl.dropbox.com/scl/fi/1nn5pa6zl5tx6uod8a496/Pasted-image-20240507083459.png?rlkey=93tq9zemwkpzqbjh52kgcscfw&st=8kftnd9d&dl=0)

website dashboard 
every option we click is being redirected to comming soon webpage 
we've have dound another subdomain play.crafty.htb let's do subdomain enum to find any sub domains

![crafty 6](https://dl.dropbox.com/scl/fi/dztzrtkzv5a4afucr5lii/Pasted-image-20240507083543.png?rlkey=4k2hedof62t6ue9zvvn54b7u9&st=1pwp5wk9&dl=0)

I haven't found anything intresting in the home page of that website but in the coming soon webpage i've found 

![crafty 7](https://dl.dropbox.com/scl/fi/q6632g6glq5snj39exa70/Pasted-image-20240507083832.png?rlkey=en1u94dxtxeoxxzfii42yqusf&st=sfi7cnsh&dl=0)

![crafty 8](https://dl.dropbox.com/scl/fi/pubrjh9tks86ozirpimmk/Pasted-image-20240507084653.png?rlkey=cp28ecwa8vb8fw9h6nc80y0yp&st=cb0wg4nr&dl=0)

the abpve result is a gobsuter scan result we haven't found anything intresting let's try some directories since we've found some info in comments 

![crafty 9](https://dl.dropbox.com/scl/fi/unubwbvutk355jhku1wg5/Pasted-image-20240507085116.png?rlkey=4ph24vc4ubnyausuz1potw7a9&st=gk2cjbw0&dl=0)

Intresting , we've got 403 error saying we don't have access to go that directory

when i searched about port 25565 i got the result saying it's minecraft default port

![crafty 10](https://dl.dropbox.com/scl/fi/je8poght61r53weui1e1d/Pasted-image-20240507085321.png?rlkey=b6en9qkskeo7n09mskqb8ky7w&st=4qbgj3ri&dl=0)

since we got a port let's connect to multiplayer with the machine ip and port number and see what happens

from the nmap scan result i searched for Minecraft vulnerabilities of that version and i found this

![crafty 11](https://dl.dropbox.com/scl/fi/ktq8pxrzuqpddj7hh8wmv/Pasted-image-20240507092437.png?rlkey=3mvtflfrmqk79rnloyjw4ht5n&st=ufb49crl&dl=0)

![crafty 12](https://dl.dropbox.com/scl/fi/tof526wcwy1jm1lx3sf64/Pasted-image-20240507095552.png?rlkey=b8ol5k4sqqfl55534h09x0o9a&st=bkps411h&dl=0)

![crafty 13](https://dl.dropbox.com/scl/fi/nzxk31bggu3uy1nb91z37/Pasted-image-20240507103801.png?rlkey=gn6jumg3ydta69jrsuz8k35a6&st=43ccypks&dl=0)

![crafty 14](https://dl.dropbox.com/scl/fi/svv0fcublcusivcumg386/Pasted-image-20240507104237.png?rlkey=dczchc2sb79zvmhafuiaqkspm&st=bhkw157f&dl=0)

