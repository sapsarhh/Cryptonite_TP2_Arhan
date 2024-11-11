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
