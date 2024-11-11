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


## tunnel vision
## flag
picoCTF{qu1t3_a_v13w_2020}

Step 1: Just like the last challenge got to learn alot from this one.
Step 2:
In this challenge I was given a file which wasnt opening and the only hint was, that it isnt displaying.
Step 3:
Confused, used the HxD editor which is a HxD editor to see what type of file it is.
First thing I see in the decoding is that the initials BM are written signifying that it is a bitmap file ie a bmp extension.
Step 4:
Put a .bmp extension in the file and tried to open it.
It became an bmp file but didnt open due to being corrupted.
Step 5:
Now some changes were supposed to be made in the HxD editor so what I did was I opened the bmp file format on wikipedia to try and make changes but didnt really help me out.
Step 6:
Then what I did was I opened an bmp file which was created in the last challenge to look at its source in the HxD editor and maybe use that as a reference and try and fix the file.
What I noticed was(i dont entirely understand this part) but in the 0A and 0E part there was BA D written which was supposed to be 36 and 28.
Made those changes and noticed that now the file opened but played a prank on me and told me not a flag.
Funnily enough I noticed that this maybe wasnt the whole image and it was cropped.
Step 7:
That was exactly it and extending the image height gave me the full image and also the flag.

![image](https://github.com/user-attachments/assets/8f785793-5d7b-42b8-b80a-a67ffa3dcc72)

Learnings:
A) already knew how to use HxD editor but still learnt more like how to change image height and all.

References:
No references per say.



