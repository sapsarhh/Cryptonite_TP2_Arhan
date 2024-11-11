## Forensics
## Trivial Flag Transfer Protocol
## Flag
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}

Step 1:
Had a lot to learn in this challenge.
Learnt about many new useful stuff in this challenge such as steghide and wireshark.
So firstly in the challenge I got a file download by the name with an extension of pcapng.
Didnt know anything about this extension so searched a little and got to know that this type of file can be opened with wireshark.
Step 2:
Opened the file with wireshark, still didnt know what to do with the file.
Researched a little and learnt how to extract objects using wireshark(reference given below).
Step 3:
Exported the objects in the tftp section.
Opened the different files and found 2 txt files and they had some not really comprehendible data.
Opened cyberchef and decided to decode the data.
Step 4:
To my luck they were encoded with ROT13 and got out what they meant.
TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBA

IUSEDTHEPROGRAMANDHIDITWITH-

DUEDILIGENCE.

CHECKOUTTHEPHOTOS
Gave me the following decoded data.
Step 5:
Now again I didnt know what to do went through the pictures but didnt find anything.
Researched on what to do with bmp files, and got to know about steghide which is a command which is used to extract hidden data from bmp files.
Step 6:
Did that with the following command: 
steghide extract -sf picture1.bmp
and entered the passphrase as DUEDILIGENCE as there was no other clue.
The 1st and 2nd file didnt work but the 3rd one did and a flag.txt was created in the same folder which contained the flag.



![image](https://github.com/user-attachments/assets/8980086c-902a-4f1a-8ad6-c49a744bfc9f)
![image](https://github.com/user-attachments/assets/cffa011b-84e8-41bb-b97e-a372d883aa6b)

Learnings:
1) As said above learnt alot of things in this one such as the steghide command and wireshark, steghide is basically a steganographic tool which is used to embed some hidden data from an image or an audio file.

References:
https://abdurrehmanrehan.medium.com/immersive-labs-cyber-million-packet-analysis-wireshark-wireshark-stream-object-extraction-f4f76d4c28cc#:~:text=Extracting%20objects,object%20type%20from%20the%20list.
https://www.youtube.com/watch?v=Fn__yRYW6Wo&ab_channel=ChrisGreer




