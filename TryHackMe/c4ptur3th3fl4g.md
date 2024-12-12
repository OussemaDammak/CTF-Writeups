Overpass Tryhackme 12/12/2024
(This is a personal writeup to be consulted later)

tool for leet language tranlation : https://www.dcode.fr/ecriture-1337-leet-speak?__r=1.d60d41a0f6c5654d87f53db1a699e0f8
tool for binary language translation : https://www.rapidtables.com/convert/number/binary-to-ascii.html
base32 & base64 we can decode them in linux cmd ![image](https://github.com/user-attachments/assets/db78f003-d9f3-4922-92a6-734f2cb10519) 
hexadecimal / base16 ![image](https://github.com/user-attachments/assets/ff62882e-c674-4be5-af94-549fc9a9926a)  
ROT13 + ROT47 cyberchef tool
Morse Code : Cyberchef tool ![image](https://github.com/user-attachments/assets/fd08564f-c0f9-416d-a1e5-e99f38da8818)  

to decrypt a hash that i don't know  https://hashes.com/en/decrypt/hash

85 110 112 97 99 107 32 116 104 105 115 32 66 67 68 == From Decimal

and last flag is = Base64-> Morse Code-> Binary->ROT -47 -> Decimal  , using cyberchef 
![image](https://github.com/user-attachments/assets/9bc48de9-afdd-4b49-ac56-20507d3ceb04)  

-----------------   
Now Spectrograms  :  
I will use Sonic Visualized on windows 
![image](https://github.com/user-attachments/assets/445d0580-70a8-4e07-9782-68f3fff57208)  

--------------  
for steganography , use 'steghide extract -sf' to extract hidden data in an image , video..
--------------
when i 'cat' the image , i find this inside of it : hackerchat.png and i find the text "AHH_YOU_FOUND_ME!" , well those are the flags , it is that easy
