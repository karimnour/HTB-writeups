### It was an easy machine from *Hack The Box*

first thing lets use **nmap** to check ip 10.10.10.181
`nmap -sC -sV 10.10.10.181` 

![nmap](https://user-images.githubusercontent.com/36403473/81315494-a9fc6b00-908a-11ea-9d23-782adf27af6a.png)
I found http on port 80 and ssh on port 22.
use should have password to conncet server so lets see http 
i opend source code i found this comment 
`
		<!--Some of the best web shells that you might need ;)-->`

![Screenshot from 2020-05-07 17-49-56](https://user-images.githubusercontent.com/36403473/81316540-feecb100-908b-11ea-94d2-a4b602e0a7b6.png)
 the first thing i do i bruteforce http dircetory by Wfuzz but it take much time , i googled on this comment i found differnt web shells on :
https://github.com/TheBinitGhimire/Web-Shells" 
reading smevk.php
we can login http://10.10.10.181/smevk.php
username:**admin**
password:**admin**

now lets go to this  directory  **/home/webadmin/.ssh** 
![Screenshot from 2020-05-07 18-23-38](https://user-images.githubusercontent.com/36403473/81319780-745a8080-9090-11ea-800a-f18601cdc38f.png)
i could to upload ssh autherizeed key 
to generate ssh keys  
i used  **`ssh-keygen`** tool on linux 
![sshgenerat](https://user-images.githubusercontent.com/36403473/81320041-da470800-9090-11ea-93d7-6956bc5bfdc0.png)
and uplad an autherized key on the server 

so now lets try to login to server:
**`ssh-i id_rsa webadmin@10.10.10.181`**

![serverlogin](https://user-images.githubusercontent.com/36403473/81354095-1303d300-90cb-11ea-8390-6c0b34e6e995.png)


![echo_note](https://user-images.githubusercontent.com/36403473/81354623-61fe3800-90cc-11ea-8ccc-92a912176868.png)
two files was the solution to take user acess **note.txt** & **bash-history**
okey the olny thing we will do write simple lua script and save it on file
**echo 'os.execute(" /bin/bash -i ")' >>block.lua ** 
save it on **block.lua file**

![note script](https://user-images.githubusercontent.com/36403473/81354540-2cf1e580-90cc-11ea-8b80-ff368637bbfb.png)
 okey lets try to acess sysadmin  by block.lua
` sudo -u sysadmin /home/sysadmin/luvit block.lua
`
 go back to home directory 
![acces_system_admin](https://user-images.githubusercontent.com/36403473/81355358-983cb700-90ce-11ea-8a26-2eec59305606.png)
  
now i have access on sysadmin 
checking files `ls -al `

![acces_system_admin](https://user-images.githubusercontent.com/36403473/81357137-287cfb00-90d3-11ea-874e-160c7a63cca7.png)

now i have user access `user.txt`

the last step is to get root access so i searched all files i didnt get any thing 
so i use **`ps -aus`** commmnd  to provide information about the currently running processes .
i notice this directory **` /etc/update-motd.d/`**
going to this directory ckeck all details **`ls -al`**
![not2root](https://user-images.githubusercontent.com/36403473/81357368-ba850380-90d3-11ea-9e74-9ceedefe51cc.png)


