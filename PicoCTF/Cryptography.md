# Cryptography
## MiniRSA

## Flag
picoCTF{n33d_a_lArg3r_e_606ce004}\

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
