# Day 1
Day 1 was fairly easy as it served as a tutorial of sorts, firstly I learnt how to connect to the virtual machine which also how to start the attackbox.
This VM was going to serve as the machine which on which the tasks were going to be done and the terminal was going to be accessed.
Step 1:
I was given the IP address of a website to access the website.
The website was a youtube video(mp4) to mp3 convertor which seemed safe at first glance but had hidden secrets once a person deep dived into the website and downloaded the converted file.
Step 2:
When I converted and downloaded the file it gave me 2 files which were both mp3, one song.mp3 and the other somg.mp3.
Now this is where it gets interesting.
Step 3:
Opened the terminal and used the exiftool command line application for the first time, this gave me the characteristics of the file, such as the relative path, the working directory etc.
Step 4:
Now the song file was safe but the malware was hidden in the somg file, now when th exiftool was used it also revealed the github link to the user who uploaded the malware and could be inspected further.
Turns out it was uploaded by MM or Mayor Malware.
Step 5:
This was when the tasks were done and all I had to do were answer the questions asked by the website.


![image](https://github.com/user-attachments/assets/83f77fd7-d9a2-480b-80b3-ce1723af852c)

1) The author was revealed with the use of the exiftool.
2) The URL of the C2 server was revealed on the github user page where the malware script was uploaded.

Learnings:
1) Learnt the use of a virtual machine.
2) Learnt aboout the command line application exiftool and how it is used.
3) Learnt what is OPSEC
   
