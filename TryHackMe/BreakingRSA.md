Breaking RSA Tryhackme 09/12/2024  
(This is a personal writeup to be consulted later)    

I run nmap scan to see the number of services running to get the first question :    
![image](https://github.com/user-attachments/assets/aa708d36-9c13-45ba-9d32-5545423e48b3)  


then I run gobuster to see the hidden directory  :  
'gobuster dir -u http://10.10.163.59/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
'  
![image](https://github.com/user-attachments/assets/724e6d1f-4e81-4e15-b524-19223da0fc38)  

I access the directory and I find this : 
![image](https://github.com/user-attachments/assets/8e56c967-e627-4b77-959d-38e722e4113e)  

I download the RSA id file  
To know the length in bits of the key  
'sh-keygen -l -f id_rsa.pub ' 

TO BE CONTINUED
