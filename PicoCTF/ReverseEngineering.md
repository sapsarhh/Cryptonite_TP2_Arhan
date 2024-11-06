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
A)learnt how to use the gdb compiler and about how to disassemble the code.

Incorrect Methods:
1) tried to use gdb debugger0_a without the wget command and that didnt work out.

References:
https://www.linkedin.com/pulse/disassembly-fungame-gdb-brian-warner/

used the above link to learn how to disassemble main.




