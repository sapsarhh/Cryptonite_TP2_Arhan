# Cryptography
## MiniRSA

## Flag
picoCTF{n33d_a_lArg3r_e_606ce004}

Step 1:
In the question I was given a file which had a small value, an exponent to be precise which had a value of 3.
and other 2 very large numbers which were c and n.
Step 2:
Here c was the ciphertext which was needed to be deciphered.
Step 3:
Didnt really understand on what to do so I took a look at the hints.
There a wiki page was given on an RSA tutorial.
Step 4:
Read the RSA tutorial and understood the maths behind obtaining the private key using N(public key) where N had to be factorised into 2 prime numbers p and q.
But this really wasnt possible because N was a very large value.
Step 5:
After giving up all hope because I didnt know what to do, looked for a RSA decipher on google and found one.
Step 6:
Used the cipher calculator to find the flag.

![image](https://github.com/user-attachments/assets/5a6a0633-c1b2-430d-9607-dadd74f21d44)


Learnings:
1) Learnt that the exponent value should be very small for accurate results.
2) Also learnt the math behind the RSA private key where N has to be factorized.


References:
1) https://ctf101.org/cryptography/overview/
2) https://www.geeksforgeeks.org/rsa-algorithm-cryptography/
3) https://www.dcode.fr/rsa-cipher


## C3

## Flag
picoCTF{adlibs}

Step 1:
Now this particular challenge annoyed me alot as it took me alot of tries to get this right as it was highly conceptual.
So in the question I was given a ciphertext which was needed to be wrapped around the encoder python code.
Step 2:
Using the wget command I installed both of the files onto my terminal.
Firstly I read the encoder file which was this:
~~~
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup1.index(char)
  out += lookup2[(cur - prev) % 40]
  prev = cur

sys.stdout.write(out)
~~~
Now this was written in python2 so that had to be used in command when used in the terminal.
I got to know this through chatgpt as I was using python3 to encode it which didnt work.

Step 3:
Now when I saw the code I was really confused on what to do as nothing was working.
Read the hint which said the following code had to be decoded firstly.
Thinking of the decoding code I realized some changes could be made which would make the code work.

~~~
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup2.index(char)
  new= lookup1[(cur + prev) % 40]
  out+=new
  prev = lookup1.index(new)

sys.stdout.write(out)
~~~

Step 4:
The changes which I made were i switched lookup 1 and lookup 2 and changed the - sign to + and created a new variable which was then used so that the prev variable could store the index of new.

Step 5:
To my surprise when I run this command it gave me another code.
~~~
 cat ciphertext.1 | python2 convert.py
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
~~~

Step 6:
Now I stored this code in another file and then wrapped the ciphertext in that file and that gave me the flag.

~~~
cat newfile.py | python2 newfile.py
a
d
l
i
b
s
~~~

Learnings:
1) Learnt that a encoder code can be further modified to act as a decoder code so that the ciphertext can be wrapped around it.
2) Learnt that some programs can only be run by python2 and not python3

Incorrect Methods:
1) Tried wrapping the ciphertext into the initial code without making the changes.
2) Used the wrong command when I recieved the output of the code which didnt work.
