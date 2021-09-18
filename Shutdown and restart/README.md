<img src=images/1.PNG  alt="alt text" width="950" height="550">
<img src=images/2.PNG  alt="alt text" width="950" height="550">
```python
#!/usr/bin/python
import time
import sys 
import socket
import os

s = socket.socket()
port = 8080
host = input (str("Please enter the server address : "))


s.connect((host,port))

print (" ")
print (" Connected to the server successfully")
print (" ")



#Connection has been completed 
#command receiving and execution 
while 1:
    
    command = s.recv(5000)
    command = command.decode()
    print (" ")

    if command == "shutdown":
        print(" ")
        print("shutdown command")
        s.send("Command revcieved".encode())
        os.system("shutdown.bat")

    elif command == "restart":
        print(" ")
        print("restart command")
        s.send("Command revcieved".encode())
        os.system("restart.bat")
           
    else:
        print (" ")
        print (" command not recognised")
       
  ```
  

<img src=images/3.PNG  alt="alt text" width="950" height="550">
<img src=images/4.PNG  alt="alt text" width="950" height="550">
<img src=images/5.PNG  alt="alt text" width="950" height="550">
<img src=images/6.PNG  alt="alt text" width="950" height="550">

