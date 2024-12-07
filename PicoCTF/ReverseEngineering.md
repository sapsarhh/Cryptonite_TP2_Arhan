## Reverse Engineering
# GDB Baby Step 1

## Flag
picoCTF{549698}

Step 1:
In the following challenge, I was given a file which I downloaded, didnt know what to do with the file as I couldnt access the file.
Step 2:
In the hint, I was told to use the gdb compiler in the bash terminal.
Copied the link of the file and used the wget terminal, to download the gdb compiler.
wget https://artifacts.picoctf.net/c/512/debugger0_a
Step 3:
when this was done I used gdb debugger0_a command and then was kinda confused on how to proceed.
Step 4:
A hint was given that I had to dissassemble the main didnt know how to do that.
Step 5:
After googling a bit realized on what I command I had to use and got the eax assembler code and converted that to decimal and got the flag.

Code and Terminal Output:
~~~
gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
debugger0_a: No such file or directory.
(gdb) exit
saps@LAPTOP-KKUS7K8J:~$ wget https://artifacts.picoctf.net/c/512/debugger0_a
--2024-11-06 23:10:27--  https://artifacts.picoctf.net/c/512/debugger0_a
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 18.155.99.118, 18.155.99.57, 18.155.99.60, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|18.155.99.118|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 16472 (16K) [application/octet-stream]
Saving to: ‘debugger0_a’

debugger0_a                   100%[=================================================>]  16.09K  --.-KB/s    in 0s

2024-11-06 23:10:28 (162 MB/s) - ‘debugger0_a’ saved [16472/16472]

saps@LAPTOP-KKUS7K8J:~$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) dissassemble main
Undefined command: "dissassemble".  Try "help".
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
(gdb)
~~~

![image](https://github.com/user-attachments/assets/3b3e7ba7-aeea-4a1f-8f97-8070d887e3cb)
![image](https://github.com/user-attachments/assets/b82270e9-afec-484d-8f3b-cbf61b1b329a)

Learnings:
A) learnt how to use the gdb compiler and about how to disassemble the code.

Incorrect Methods:
1) tried to use gdb debugger0_a without the wget command and that didnt work out.

References:
https://www.linkedin.com/pulse/disassembly-fungame-gdb-brian-warner/

used the above link to learn how to disassemble main.


## ARMassembly1
## Flag
picoCTF{00000d2a}

Step 1:
In the following question I was given a file named chall.s which was an assembly language code and I opened it.
in the question I was instructed that for some argument win would be printed for the numbers 79,7 and 3.
Step 2:
In the code I saw that there is a function which can either print you win or you lose depending on the arguments.
Step 3:
Then after some research and watching some resources I got to know what the symbols in assembly language mean, I got to know that w0  is 79<<7 which was stored in sp,28 then that result was divided by 3 and then finally that was subtracted with the input which the user has to input to get the required result.
Step 4:
Using the above operations an equation could be formed, which is (79*7)/3-x=0 and if solved the answer comes out to be 3370 which is the answer.
Step 5:
When this is converted to the form which is specified in the question, the flag comes out to be 00000d2a.

Learnings:
Learnt a little about what the symbols in assembly language mean.


Incorrect Methods:
Tried to execute the code which didnt work.

References:
https://www.youtube.com/playlist?list=PLMB3ddm5Yvh3gf_iev78YP5EPzkA3nPdL


## Vault Door 3
## Flag
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_1fb380}

Step 1:
Opened the java file which was given in the queestion.
Step 2:
Opened the file and there was a code written in which there was a string given which was jU5t_a_sna_3lpm18gb41_u_4_mfr340, and some transformations were made on the string inputted by the user if the string was 32 characters long.
Step 3:
Now I tried running the code through an online compiler in java itself but it kept giving me an error of access denied even when there were 32 characters.
Step 4:
Now in the code I understood that if the format was picoCTF{} some string inside the curly braces then the code should run but it wasnt.
Step 5:
Now in the code the aforesaid string had to be transformed to something which was done in the for loops and the transformed code was the flag itself.
Step 5:
So I copied the transformations happening in the code(the for loops primarily), put that inside a C file and copied the string as well and run the code.
That gave me the flag.

Code(which I wrote on C):
~~~
#include <stdio.h>
void main(){



char *password="jU5t_a_sna_3lpm18gb41_u_4_mfr340";
char buffer[32];
        int i=0;
        for (i=0; i<8; i++) {
            buffer[i] = password[i];
        }
        for (; i<16; i++) {
            buffer[i] = password[23-i];
        }
        for (; i<32; i+=2) {
            buffer[i] = password[46-i];
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password[i];
        }
        printf("%s", buffer);
        

}
~~~

![image](https://github.com/user-attachments/assets/5bf47074-394f-427b-9ce4-4a8da4f0358a)

Learnings:
No new learnings as such just learnt a little java as I have not done it earlier.

Incorrect Methods:
Tried running the code in an online java compiler which didnt work.

No references.





