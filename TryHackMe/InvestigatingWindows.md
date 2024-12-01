Investigating Windows Tryhackme 01/12/2024 (This is a personal writeup to be consulted later)  

we will investigate a windows machine  
we connect via rdp (rdesktop @ip)  
![image](https://github.com/user-attachments/assets/befab8fa-811b-4343-a7c6-1854cb094520)  
Username: Administrator  
Password: letmein123!  

we got in successfully :   
![image](https://github.com/user-attachments/assets/44248b4e-9ad8-484f-b1cb-a847ada51fa6)
we need to know the version and year of the windows machine?  
i will continue with the attackbox because I got connectivity issues.  
# Flag1  
our first flag is simple , the version of the machine , we found it in the settings :  
![image](https://github.com/user-attachments/assets/4f34d35f-9975-43a4-bea0-a01672213e08)   
# Flag2   
we need to know the last user who logged in .  
if use the command 'query user' in the cmd , we find the users that logged in :  
![image](https://github.com/user-attachments/assets/72282999-e4fc-44cb-a644-7bcb5f0fc377)  
# Flag3  
this flags mentions that it wants the time that john is logged in , but i only see 1 user which is the administrator  
Now I will switch to PowerShell  
type 'Get-ComputerInfo for flag1'  
type 'Get-LocalUser' to list users for flag2 then type 'Net user Jenny' or 'Net user Administrator' to know who last log on , or simply time 'Net user Administrator | findstr "last" '  
for the flag3 :  
![image](https://github.com/user-attachments/assets/c6a8361f-ad38-4d21-8eeb-f4cfafd7c2bc)  
# Flag4  
we need to know which IP@ does the server connects to when it starts  
we go to cmd again and open the hosts file  
![image](https://github.com/user-attachments/assets/31b56f29-cfec-4e7b-bb72-7b38decb3ea5)  
I didn't find anything, but I see that a lot of websites are pointed to local , even google, so maybe I'm seeing a DNS poisoning  
then I will go to Registry to investigate more  
![image](https://github.com/user-attachments/assets/c35657da-f2bf-4cdb-a17e-983c30db1f86)  
we follow this path HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > Run  
![image](https://github.com/user-attachments/assets/75b96717-dfb2-45bf-aef1-7db09ed15de3)  
and I find the IP @ that the system connects to when it starts  
# Flag5  
to see who has admin privileges , first I need to know the groups located in our system using 'Get-LocalGroup' , then I search for members inside the admin group using 'Get-LocalGroupMember'  
![image](https://github.com/user-attachments/assets/a79988aa-723b-489c-bc61-41210c39fb9a)  
# Flag6  
now I need to figure out the malicious scheduled task , it is simple , I just type 'Get-ScheduledTask'  
as I see , the 'clean file system' task is malicious  
![image](https://github.com/user-attachments/assets/836c5c8e-484e-4567-a9b4-c5b54c54a07f)  
# Flag7 + Flag8 
now I need to know what's inside this task and what it trying to run daily  
$task = Get-ScheduledTask | Where TaskName -EQ "Clean file system"  
 $task.Actions  
![image](https://github.com/user-attachments/assets/22b90807-12c6-4eac-9b69-4a31130e2721)  
# Flag9 
jenny last logon like flag2 
# Flag10 + Flag11  
we open the event viewer  
we create a custom view to see what happened during that day  
![image](https://github.com/user-attachments/assets/a6883f63-f55a-43d4-94f8-4b672018a34b)  
![image](https://github.com/user-attachments/assets/92fc2eac-a91a-4c56-8464-4d5a2abf23e1)  
I look for 'Security Group Management' to find the change on privileges to new logon  
![image](https://github.com/user-attachments/assets/6626fa84-9405-437d-8347-cdbde1dad4d2)  
# Flag12  
I need to find the tool that is used to get windows password , there is a window that keeps popping up , I will see what's behind it  
I find the output file, and I find the tool name  
![image](https://github.com/user-attachments/assets/2e083299-0167-445b-ad62-e94f6cf0ec5f)  
# Flag13  
find the attacker ip , i remember i opened the hosts file and saw some weird configurations  
![image](https://github.com/user-attachments/assets/68d70d9e-93cd-459a-8685-28ba5a10ae19)  
I see the google has a waird IP , it can the hidden server C2  
# Flag 14 





