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




# Custom Encryption
## Flag:
picoCTF{custom_d2cr0pt6d_dc499538}
I felt this was a reverse engineering question rather than a cryptography question.
Step 1: Now this particular challenge was really tough and I even had to refer to a video to solve it as I just could not solve it after alot of tries, so to get started 2 files were provided one containing 2 values(a and b) and a ciphertext which was an array of values.
The second file was of course a python script which had alot of functions for decrypting some cipher text.

Step 2:
Now I realized that an decryption algorithm had to be made because all that this script was doing was encrypting some cipher text and not decrypting it and that was the change that had to be made.
Now I had the basic idea on what to do.
Firstly I copied the encrypt function and made another one which was the decrypt function which took the values as parameters which were returned by the encrypt function.

Basically the changes/calculations that were happening in the encrypt function had to be reversed in the decrypt function.
~~~
def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(ord(char) * key * 311)
    return cipher


def decrypt(ciphertext, key):
    plain = ""
    for num in ciphertext:
        decrypted_num = int(num / key / 311)
        plain += chr(decrypted_num)
    return plain
~~~

Like here the decrypt function took the cipher text returned by the encrypt function and returned a plain text which undid the changes(multiplying the number by the key and that by 311) and added those characters in the plain text.

Step 3:

Then there was a xor function of course an encrypted one, so a decrypted one had to be made as well.
~~~
def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def dynamic_xor_decrypt(ciphertext, text_key):
    plain_text = ""
    key_length = len(text_key)
    for i, char in enumerate(ciphertext):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        plain_text += decrypted_char
    return plain_text
~~~

In the decrypt function it again took the ciphertext as parameter which was returned by the above decrypt function and iterating through the characters of the ciphertext and then xor'ing the ascii values of char and keychar and storing them in plaintext and returning that.
Then the values of a and b had to be substituted as well as substituting the array in the message variable to make the code run.

~~~
message = [33588, 276168, 261240, 302292, 343344, 328416, 242580, 85836, 82104, 156744, 0, 
               309756, 78372, 18660, 253776, 0, 82104, 320952, 3732, 231384, 89568, 100764, 
               22392, 22392, 63444, 22392, 97032, 190332, 119424, 182868, 97032, 26124, 44784, 63444]

~~~

![image](https://github.com/user-attachments/assets/c9f8d470-3c62-4d5c-ad2c-3264e5a9f391)

This was the output recieved when the code was debugged as it had alot of errors initially.

Learnings:
1) Now as stated above this was rather a question of rev eng as a whole new algorithm of decryption had to be created.
2) Learnt how to make a new decryption algorithm for complex questions.
3) I had the basic idea on what to do but for fine tuning I had to refer to a video for making the code work as it had errors.

The following is the whole modified script:

~~~
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(ord(char) * key * 311)
    return cipher


def decrypt(ciphertext, key):
    plain = ""
    for num in ciphertext:
        decrypted_num = int(num / key / 311)
        plain += chr(decrypted_num)
    return plain


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    return v <= 1


def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text


def dynamic_xor_decrypt(ciphertext, text_key):
    plain_text = ""
    key_length = len(text_key)
    for i, char in enumerate(ciphertext):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        plain_text += decrypted_char
    return plain_text


def test(cipher_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) or not is_prime(g):
        print("Enter prime numbers")
        return
    a = 89  
    b = 27  
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)  
    v = generator(g, b, p)  
    key = generator(v, a, p)  
    b_key = generator(u, b, p)  

    if key == b_key:
        print("Shared key established successfully!")
        shared_key = key
    else:
        print("Invalid key")
        return

    
    semi_cipher = decrypt(cipher_text, shared_key)
    plain = dynamic_xor_decrypt(semi_cipher, text_key)
    print(f'Plaintext is: {plain[::-1]}')


if __name__ == "__main__":
    message = [33588, 276168, 261240, 302292, 343344, 328416, 242580, 85836, 82104, 156744, 0, 
               309756, 78372, 18660, 253776, 0, 82104, 320952, 3732, 231384, 89568, 100764, 
               22392, 22392, 63444, 22392, 97032, 190332, 119424, 182868, 97032, 26124, 44784, 63444]
    test(message, "trudeau")
~~~




Incorrect Methods:
1) Couldnt really come up with the whole decryption algorithm(for the xor function)
2) Tried to run the code with the existing functions with no decryption algo(i dont now why)


References:
1) https://www.youtube.com/watch?v=3cPnX_9bLPs&t=231s&ab_channel=MartinCarlisle



               

