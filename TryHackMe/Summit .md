
**Summit (Challenge)**


I access <https://10-10-130-58.p.thmlabs.com/> 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.001.png)

it seems that there is 4 mails

first mail, it tells me to scan the file ‘sample1.exe’ using ‘Malware Sandbox’ tool

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.002.png)

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.003.png)

for our first flag, I add the MD5 to the BlockList 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.004.png)

—-----------

for sample2.exe, it seems like the first one : 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.005.png)

but it has an extra network section: 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.006.png)

to get the second flag, i use the firewall rules, the malware makes a http request to http://154.35.10.113:4444/uvLk8YI32

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.007.png)

—-------

for sample3.exe , we have these sections, i can see that a new dns requests is showing : 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.008.png)

and this domain looks malicious ‘emudyn.bresonicz.info’ , so i will block it : 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.009.png)

—-------------

for sample4.exe, i got an extra section called Registry Activity : 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.010.png)

and this event looks malicious : 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.011.png)

i got to ‘Sigma Rule Builder’ , ‘sysmon Event logs’ , ‘Registry Modifications’.

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.012.png)

—-------------

for sample5.exe, 

i’m seeing a problem with the domain ‘bababa10la” and its ip ‘ 51.102.10.19’

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.013.png)

but , i will be investigating the ‘outgoing\_connections.log’ file

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.014.png)

I can see that every 30 minutes , there is a connection that is happening, I can create a Sigma Rule , but now ‘Network Connection’

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.015.png)

—--------------

for sample6.exe, i got the commands.log file : 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.016.png)

i am seeing exflitr8.log file

%temp%\exfiltr8.log

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.017.png)

i  add another rule in Sigma: 

![](Aspose.Words.8f471e59-09cb-4049-a8af-9d26a625bc8a.018.png)

and i finished and got the 6 flags
