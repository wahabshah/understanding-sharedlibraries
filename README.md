
# Displays the contents of the file’s relocation section, if it has one.

```sh
readelf -r clientApp/clientApp

Relocation section '.rela.dyn' at offset 0x528 contains 9 entries:
  Offset          Info           Type           Sym. Value    Sym. Name + Addend
000000200db8  000000000008 R_X86_64_RELATIVE                    760
000000200dc0  000000000008 R_X86_64_RELATIVE                    720
000000201028  000000000008 R_X86_64_RELATIVE                    201028
000000200fd0  000100000006 R_X86_64_GLOB_DAT 0000000000000000 _ITM_deregisterTMClone + 0
000000200fd8  000300000006 R_X86_64_GLOB_DAT 0000000000000000 __libc_start_main@GLIBC_2.2.5 + 0
000000200fe0  000400000006 R_X86_64_GLOB_DAT 0000000000000000 __gmon_start__ + 0
000000200fe8  000500000006 R_X86_64_GLOB_DAT 0000000000000000 _Jv_RegisterClasses + 0
000000200ff0  000600000006 R_X86_64_GLOB_DAT 0000000000000000 _ITM_registerTMCloneTa + 0
000000200ff8  000700000006 R_X86_64_GLOB_DAT 0000000000000000 __cxa_finalize@GLIBC_2.2.5 + 0

Relocation section '.rela.plt' at offset 0x600 contains 1 entries:
  Offset          Info           Type           Sym. Value    Sym. Name + Addend
000000201018  000200000007 R_X86_64_JUMP_SLO 0000000000000000 shlib_function + 0
```

# Displays the information contained in the file’s section headers, if it has any.

* Relocation information by linker for symbol `shlib_function` is embedded at address `000000201018`, which the loader is expected to operate during runtime to resolve the symbol. 
* This belongs to the section `.got.plt` between address `0000000000201000` and `0000000000201020`:-

```sh
  [24] .got.plt          PROGBITS        0000000000201000 001000 000020 08  WA  0   0  8
```

```sh
readelf --sections --wide clientApp/clientApp

There are 36 section headers, starting at offset 0x22b8:

Section Headers:
  [Nr] Name              Type            Address          Off    Size   ES Flg Lk Inf Al
  [ 0]                   NULL            0000000000000000 000000 000000 00      0   0  0
  [ 1] .interp           PROGBITS        0000000000000238 000238 00001c 00   A  0   0  1
  [ 2] .note.ABI-tag     NOTE            0000000000000254 000254 000020 00   A  0   0  4
  [ 3] .note.gnu.build-id NOTE            0000000000000274 000274 000024 00   A  0   0  4
  [ 4] .gnu.hash         GNU_HASH        0000000000000298 000298 000038 00   A  5   0  8
  [ 5] .dynsym           DYNSYM          00000000000002d0 0002d0 000138 18   A  6   1  8
  [ 6] .dynstr           STRTAB          0000000000000408 000408 0000e0 00   A  0   0  1
  [ 7] .gnu.version      VERSYM          00000000000004e8 0004e8 00001a 02   A  5   0  2
  [ 8] .gnu.version_r    VERNEED         0000000000000508 000508 000020 00   A  6   1  8
  [ 9] .rela.dyn         RELA            0000000000000528 000528 0000d8 18   A  5   0  8
  [10] .rela.plt         RELA            0000000000000600 000600 000018 18  AI  5  24  8
  [11] .init             PROGBITS        0000000000000618 000618 000017 00  AX  0   0  4
  [12] .plt              PROGBITS        0000000000000630 000630 000020 10  AX  0   0 16
  [13] .plt.got          PROGBITS        0000000000000650 000650 000008 00  AX  0   0  8
  [14] .text             PROGBITS        0000000000000660 000660 0001d2 00  AX  0   0 16
  [15] .fini             PROGBITS        0000000000000834 000834 000009 00  AX  0   0  4
  [16] .rodata           PROGBITS        0000000000000840 000840 000004 04  AM  0   0  4
  [17] .eh_frame_hdr     PROGBITS        0000000000000844 000844 00003c 00   A  0   0  4
  [18] .eh_frame         PROGBITS        0000000000000880 000880 00010c 00   A  0   0  8
  [19] .init_array       INIT_ARRAY      0000000000200db8 000db8 000008 08  WA  0   0  8
  [20] .fini_array       FINI_ARRAY      0000000000200dc0 000dc0 000008 08  WA  0   0  8
  [21] .jcr              PROGBITS        0000000000200dc8 000dc8 000008 00  WA  0   0  8
  [22] .dynamic          DYNAMIC         0000000000200dd0 000dd0 000200 10  WA  6   0  8
  [23] .got              PROGBITS        0000000000200fd0 000fd0 000030 08  WA  0   0  8
  [24] .got.plt          PROGBITS        0000000000201000 001000 000020 08  WA  0   0  8
  [25] .data             PROGBITS        0000000000201020 001020 000010 00  WA  0   0  8
  [26] .bss              NOBITS          0000000000201030 001030 000008 00  WA  0   0  1
  [27] .comment          PROGBITS        0000000000000000 001030 00002d 01  MS  0   0  1
  [28] .debug_aranges    PROGBITS        0000000000000000 00105d 000030 00      0   0  1
  [29] .debug_info       PROGBITS        0000000000000000 00108d 000356 00      0   0  1
  [30] .debug_abbrev     PROGBITS        0000000000000000 0013e3 000102 00      0   0  1
  [31] .debug_line       PROGBITS        0000000000000000 0014e5 0000d2 00      0   0  1
  [32] .debug_str        PROGBITS        0000000000000000 0015b7 0002b0 01  MS  0   0  1
  [33] .symtab           SYMTAB          0000000000000000 001868 0006d8 18     34  52  8
  [34] .strtab           STRTAB          0000000000000000 001f40 00022c 00      0   0  1
  [35] .shstrtab         STRTAB          0000000000000000 00216c 00014c 00      0   0  1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  l (large), p (processor specific)
```

# Disassembling the Binary Files 

The call to function `shlib_function` is implemented as a call to `shlib_function@plt`.
The functions with the suffix "@plt" are automatically generated by the compiler to aid the implementation of the PIC concept.

```sh
objdump -d -S -M intel clientApp/clientApp

clientApp/clientApp:     file format elf64-x86-64


Disassembly of section .init:

0000000000000618 <_init>:
 618:   48 83 ec 08             sub    rsp,0x8
 61c:   48 8b 05 bd 09 20 00    mov    rax,QWORD PTR [rip+0x2009bd]        # 200fe0 <__gmon_start__>
 623:   48 85 c0                test   rax,rax
 626:   74 02                   je     62a <_init+0x12>
 628:   ff d0                   call   rax
 62a:   48 83 c4 08             add    rsp,0x8
 62e:   c3                      ret    

Disassembly of section .plt:

0000000000000630 <.plt>:
 630:   ff 35 d2 09 20 00       push   QWORD PTR [rip+0x2009d2]        # 201008 <_GLOBAL_OFFSET_TABLE_+0x8>
 636:   ff 25 d4 09 20 00       jmp    QWORD PTR [rip+0x2009d4]        # 201010 <_GLOBAL_OFFSET_TABLE_+0x10>
 63c:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]

0000000000000640 <shlib_function@plt>:
 640:   ff 25 d2 09 20 00       jmp    QWORD PTR [rip+0x2009d2]        # 201018 <shlib_function>
 646:   68 00 00 00 00          push   0x0
 64b:   e9 e0 ff ff ff          jmp    630 <.plt>

Disassembly of section .plt.got:

0000000000000650 <.plt.got>:
 650:   ff 25 a2 09 20 00       jmp    QWORD PTR [rip+0x2009a2]        # 200ff8 <__cxa_finalize@GLIBC_2.2.5>
 656:   66 90                   xchg   ax,ax

Disassembly of section .text:

0000000000000660 <_start>:
 660:   31 ed                   xor    ebp,ebp
 662:   49 89 d1                mov    r9,rdx
 665:   5e                      pop    rsi
 666:   48 89 e2                mov    rdx,rsp
 669:   48 83 e4 f0             and    rsp,0xfffffffffffffff0
 66d:   50                      push   rax
 66e:   54                      push   rsp
 66f:   4c 8d 05 ba 01 00 00    lea    r8,[rip+0x1ba]        # 830 <__libc_csu_fini>
 676:   48 8d 0d 43 01 00 00    lea    rcx,[rip+0x143]        # 7c0 <__libc_csu_init>
 67d:   48 8d 3d 0c 01 00 00    lea    rdi,[rip+0x10c]        # 790 <main>
 684:   ff 15 4e 09 20 00       call   QWORD PTR [rip+0x20094e]        # 200fd8 <__libc_start_main@GLIBC_2.2.5>
 68a:   f4                      hlt    
 68b:   0f 1f 44 00 00          nop    DWORD PTR [rax+rax*1+0x0]

0000000000000690 <deregister_tm_clones>:
 690:   48 8d 3d 99 09 20 00    lea    rdi,[rip+0x200999]        # 201030 <__TMC_END__>
 697:   48 8d 05 99 09 20 00    lea    rax,[rip+0x200999]        # 201037 <__TMC_END__+0x7>
 69e:   55                      push   rbp
 69f:   48 29 f8                sub    rax,rdi
 6a2:   48 89 e5                mov    rbp,rsp
 6a5:   48 83 f8 0e             cmp    rax,0xe
 6a9:   76 15                   jbe    6c0 <deregister_tm_clones+0x30>
 6ab:   48 8b 05 1e 09 20 00    mov    rax,QWORD PTR [rip+0x20091e]        # 200fd0 <_ITM_deregisterTMCloneTable>
 6b2:   48 85 c0                test   rax,rax
 6b5:   74 09                   je     6c0 <deregister_tm_clones+0x30>
 6b7:   5d                      pop    rbp
 6b8:   ff e0                   jmp    rax
 6ba:   66 0f 1f 44 00 00       nop    WORD PTR [rax+rax*1+0x0]
 6c0:   5d                      pop    rbp
 6c1:   c3                      ret    
 6c2:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]
 6c6:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 6cd:   00 00 00 

00000000000006d0 <register_tm_clones>:
 6d0:   48 8d 3d 59 09 20 00    lea    rdi,[rip+0x200959]        # 201030 <__TMC_END__>
 6d7:   48 8d 35 52 09 20 00    lea    rsi,[rip+0x200952]        # 201030 <__TMC_END__>
 6de:   55                      push   rbp
 6df:   48 29 fe                sub    rsi,rdi
 6e2:   48 89 e5                mov    rbp,rsp
 6e5:   48 c1 fe 03             sar    rsi,0x3
 6e9:   48 89 f0                mov    rax,rsi
 6ec:   48 c1 e8 3f             shr    rax,0x3f
 6f0:   48 01 c6                add    rsi,rax
 6f3:   48 d1 fe                sar    rsi,1
 6f6:   74 18                   je     710 <register_tm_clones+0x40>
 6f8:   48 8b 05 f1 08 20 00    mov    rax,QWORD PTR [rip+0x2008f1]        # 200ff0 <_ITM_registerTMCloneTable>
 6ff:   48 85 c0                test   rax,rax
 702:   74 0c                   je     710 <register_tm_clones+0x40>
 704:   5d                      pop    rbp
 705:   ff e0                   jmp    rax
 707:   66 0f 1f 84 00 00 00    nop    WORD PTR [rax+rax*1+0x0]
 70e:   00 00 
 710:   5d                      pop    rbp
 711:   c3                      ret    
 712:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]
 716:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 71d:   00 00 00 

0000000000000720 <__do_global_dtors_aux>:
 720:   80 3d 09 09 20 00 00    cmp    BYTE PTR [rip+0x200909],0x0        # 201030 <__TMC_END__>
 727:   75 27                   jne    750 <__do_global_dtors_aux+0x30>
 729:   48 83 3d c7 08 20 00    cmp    QWORD PTR [rip+0x2008c7],0x0        # 200ff8 <__cxa_finalize@GLIBC_2.2.5>
 730:   00 
 731:   55                      push   rbp
 732:   48 89 e5                mov    rbp,rsp
 735:   74 0c                   je     743 <__do_global_dtors_aux+0x23>
 737:   48 8b 3d ea 08 20 00    mov    rdi,QWORD PTR [rip+0x2008ea]        # 201028 <__dso_handle>
 73e:   e8 0d ff ff ff          call   650 <.plt.got>
 743:   e8 48 ff ff ff          call   690 <deregister_tm_clones>
 748:   5d                      pop    rbp
 749:   c6 05 e0 08 20 00 01    mov    BYTE PTR [rip+0x2008e0],0x1        # 201030 <__TMC_END__>
 750:   f3 c3                   repz ret 
 752:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]
 756:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 75d:   00 00 00 

0000000000000760 <frame_dummy>:
 760:   48 8d 3d 61 06 20 00    lea    rdi,[rip+0x200661]        # 200dc8 <__JCR_END__>
 767:   48 83 3f 00             cmp    QWORD PTR [rdi],0x0
 76b:   75 0b                   jne    778 <frame_dummy+0x18>
 76d:   e9 5e ff ff ff          jmp    6d0 <register_tm_clones>
 772:   66 0f 1f 44 00 00       nop    WORD PTR [rax+rax*1+0x0]
 778:   48 8b 05 69 08 20 00    mov    rax,QWORD PTR [rip+0x200869]        # 200fe8 <_Jv_RegisterClasses>
 77f:   48 85 c0                test   rax,rax
 782:   74 e9                   je     76d <frame_dummy+0xd>
 784:   55                      push   rbp
 785:   48 89 e5                mov    rbp,rsp
 788:   ff d0                   call   rax
 78a:   5d                      pop    rbp
 78b:   e9 40 ff ff ff          jmp    6d0 <register_tm_clones>

0000000000000790 <main>:
#include <stdio.h>
#include "shlibexports.h"
int main(int argc, char* argv[])
{ 
 790:   55                      push   rbp
 791:   48 89 e5                mov    rbp,rsp
 794:   48 83 ec 20             sub    rsp,0x20
 798:   89 7d ec                mov    DWORD PTR [rbp-0x14],edi
 79b:   48 89 75 e0             mov    QWORD PTR [rbp-0x20],rsi
    int nRetValue = shlib_function();
 79f:   e8 9c fe ff ff          call   640 <shlib_function@plt>
 7a4:   89 45 fc                mov    DWORD PTR [rbp-0x4],eax
    // purposefully calling second time
    nRetValue += shlib_function();
 7a7:   e8 94 fe ff ff          call   640 <shlib_function@plt>
 7ac:   01 45 fc                add    DWORD PTR [rbp-0x4],eax
    return nRetValue;
 7af:   8b 45 fc                mov    eax,DWORD PTR [rbp-0x4]
 7b2:   c9                      leave  
 7b3:   c3                      ret    
 7b4:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 7bb:   00 00 00 
 7be:   66 90                   xchg   ax,ax

00000000000007c0 <__libc_csu_init>:
 7c0:   41 57                   push   r15
 7c2:   41 56                   push   r14
 7c4:   41 89 ff                mov    r15d,edi
 7c7:   41 55                   push   r13
 7c9:   41 54                   push   r12
 7cb:   4c 8d 25 e6 05 20 00    lea    r12,[rip+0x2005e6]        # 200db8 <__frame_dummy_init_array_entry>
 7d2:   55                      push   rbp
 7d3:   48 8d 2d e6 05 20 00    lea    rbp,[rip+0x2005e6]        # 200dc0 <__init_array_end>
 7da:   53                      push   rbx
 7db:   49 89 f6                mov    r14,rsi
 7de:   49 89 d5                mov    r13,rdx
 7e1:   4c 29 e5                sub    rbp,r12
 7e4:   48 83 ec 08             sub    rsp,0x8
 7e8:   48 c1 fd 03             sar    rbp,0x3
 7ec:   e8 27 fe ff ff          call   618 <_init>
 7f1:   48 85 ed                test   rbp,rbp
 7f4:   74 20                   je     816 <__libc_csu_init+0x56>
 7f6:   31 db                   xor    ebx,ebx
 7f8:   0f 1f 84 00 00 00 00    nop    DWORD PTR [rax+rax*1+0x0]
 7ff:   00 
 800:   4c 89 ea                mov    rdx,r13
 803:   4c 89 f6                mov    rsi,r14
 806:   44 89 ff                mov    edi,r15d
 809:   41 ff 14 dc             call   QWORD PTR [r12+rbx*8]
 80d:   48 83 c3 01             add    rbx,0x1
 811:   48 39 dd                cmp    rbp,rbx
 814:   75 ea                   jne    800 <__libc_csu_init+0x40>
 816:   48 83 c4 08             add    rsp,0x8
 81a:   5b                      pop    rbx
 81b:   5d                      pop    rbp
 81c:   41 5c                   pop    r12
 81e:   41 5d                   pop    r13
 820:   41 5e                   pop    r14
 822:   41 5f                   pop    r15
 824:   c3                      ret    
 825:   90                      nop
 826:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 82d:   00 00 00 

0000000000000830 <__libc_csu_fini>:
 830:   f3 c3                   repz ret 

Disassembly of section .fini:

0000000000000834 <_fini>:
 834:   48 83 ec 08             sub    rsp,0x8
 838:   48 83 c4 08             add    rsp,0x8
 83c:   c3                      ret    
 ```

# Run time analysis

```sh
cd  clientApp
gdb clientApp


GNU gdb (Debian 7.12-6) 7.12.0.20161007-git
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from clientApp...done.
(gdb) break main
Breakpoint 1 at 0x79f: file main.c, line 5.
(gdb) run
Starting program: /home/wahab/compilation-understanding/clientApp/clientApp 

Breakpoint 1, main (argc=1, argv=0x7fffffffdb88) at main.c:5
5           int nRetValue = shlib_function();
(gdb) set disassembly-flavor intel
(gdb) disassemble /m
Dump of assembler code for function main:
4       { 
   0x0000555555554790 <+0>:     push   rbp
   0x0000555555554791 <+1>:     mov    rbp,rsp
   0x0000555555554794 <+4>:     sub    rsp,0x20
   0x0000555555554798 <+8>:     mov    DWORD PTR [rbp-0x14],edi
   0x000055555555479b <+11>:    mov    QWORD PTR [rbp-0x20],rsi

5           int nRetValue = shlib_function();
=> 0x000055555555479f <+15>:    call   0x555555554640 <shlib_function@plt>
   0x00005555555547a4 <+20>:    mov    DWORD PTR [rbp-0x4],eax

6           // purposefully calling second time
7           nRetValue += shlib_function();
   0x00005555555547a7 <+23>:    call   0x555555554640 <shlib_function@plt>
   0x00005555555547ac <+28>:    add    DWORD PTR [rbp-0x4],eax

---Type <return> to continue, or q <return> to quit---
8           return nRetValue;
   0x00005555555547af <+31>:    mov    eax,DWORD PTR [rbp-0x4]

9       }   0x00005555555547b2 <+34>:   leave  
   0x00005555555547b3 <+35>:    ret    

End of assembler dump.
(gdb) stepi
0x0000555555554640 in shlib_function@plt ()
(gdb) disassemble /m
Dump of assembler code for function shlib_function@plt:
=> 0x0000555555554640 <+0>:     jmp    QWORD PTR [rip+0x2009d2]        # 0x555555755018
   0x0000555555554646 <+6>:     push   0x0
   0x000055555555464b <+11>:    jmp    0x555555554630
End of assembler dump.
(gdb) display /x *0x555555755018
1: /x *0x555555755018 = 0x55554646
(gdb) stepi
0x0000555555554646 in shlib_function@plt ()
1: /x *0x555555755018 = 0x55554646
(gdb) stepi
0x000055555555464b in shlib_function@plt ()
1: /x *0x555555755018 = 0x55554646
(gdb) stepi
0x0000555555554630 in ?? ()
1: /x *0x555555755018 = 0x55554646
(gdb) stepi
0x0000555555554636 in ?? ()
1: /x *0x555555755018 = 0x55554646
(gdb) stepi
_dl_runtime_resolve_xsavec () at ../sysdeps/x86_64/dl-trampoline.h:71
71      ../sysdeps/x86_64/dl-trampoline.h: No such file or directory.
1: /x *0x555555755018 = 0x55554646
(gdb) step
shlib_function () at shlib.c:4
4       {
1: /x *0x555555755018 = 0xf7bd7640
(gdb) finish
Run till exit from #0  shlib_function () at shlib.c:4
0x00005555555547a4 in main (argc=1, argv=0x7fffffffdb88) at main.c:5
5           int nRetValue = shlib_function();
1: /x *0x555555755018 = 0xf7bd7640
Value returned is $1 = 10
 ```

 # The .got.plt Variable 

 ```sh
ps -ef | grep clientApp

wahab    15866 12831  0 21:36 pts/5    00:00:00 gdb clientApp
wahab    15868 15866  0 21:36 pts/5    00:00:00 /home/wahab/compilation-understanding/clientApp/clientApp
wahab    16072 15888  0 21:46 pts/8    00:00:00 grep clientApp
 ```


* the `shlibFirst` got loaded at the address range starting at the address `0x7ffff7bd7000`

 ```sh
 cat /proc/15868/maps

555555554000-555555555000 r-xp 00000000 08:10 1150846                    /home/wahab/compilation-understanding/clientApp/clientApp
555555754000-555555755000 r--p 00000000 08:10 1150846                    /home/wahab/compilation-understanding/clientApp/clientApp
555555755000-555555756000 rw-p 00001000 08:10 1150846                    /home/wahab/compilation-understanding/clientApp/clientApp
7ffff7838000-7ffff79cd000 r-xp 00000000 08:10 232083                     /lib/x86_64-linux-gnu/libc-2.24.so
7ffff79cd000-7ffff7bcd000 ---p 00195000 08:10 232083                     /lib/x86_64-linux-gnu/libc-2.24.so
7ffff7bcd000-7ffff7bd1000 r--p 00195000 08:10 232083                     /lib/x86_64-linux-gnu/libc-2.24.so
7ffff7bd1000-7ffff7bd3000 rw-p 00199000 08:10 232083                     /lib/x86_64-linux-gnu/libc-2.24.so
7ffff7bd3000-7ffff7bd7000 rw-p 00000000 00:00 0 
7ffff7bd7000-7ffff7bd8000 r-xp 00000000 08:10 1150845                    /home/wahab/compilation-understanding/shlibFirst/libfirst.so.1.0.0
7ffff7bd8000-7ffff7dd7000 ---p 00001000 08:10 1150845                    /home/wahab/compilation-understanding/shlibFirst/libfirst.so.1.0.0
7ffff7dd7000-7ffff7dd8000 r--p 00000000 08:10 1150845                    /home/wahab/compilation-understanding/shlibFirst/libfirst.so.1.0.0
7ffff7dd8000-7ffff7dd9000 rw-p 00001000 08:10 1150845                    /home/wahab/compilation-understanding/shlibFirst/libfirst.so.1.0.0
7ffff7dd9000-7ffff7dfc000 r-xp 00000000 08:10 232055                     /lib/x86_64-linux-gnu/ld-2.24.so
7ffff7fd7000-7ffff7fd9000 rw-p 00000000 00:00 0 
7ffff7ff4000-7ffff7ff7000 rw-p 00000000 00:00 0 
7ffff7ff7000-7ffff7ffa000 r--p 00000000 00:00 0                          [vvar]
7ffff7ffa000-7ffff7ffc000 r-xp 00000000 00:00 0                          [vdso]
7ffff7ffc000-7ffff7ffd000 r--p 00023000 08:10 232055                     /lib/x86_64-linux-gnu/ld-2.24.so
7ffff7ffd000-7ffff7ffe000 rw-p 00024000 08:10 232055                     /lib/x86_64-linux-gnu/ld-2.24.so
7ffff7ffe000-7ffff7fff000 rw-p 00000000 00:00 0 
7ffffffdd000-7ffffffff000 rw-p 00000000 00:00 0                          [stack]

```

* `shlibfunction` is at offset `0x640`
* If we add we it gets loaded in memory + offset = `0x7ffff7bd7000` + `0x640` = `0x7ffff7bd7640`

```sh
objdump -d -S -M intel shlibFirst/libfirst.so.1.0.0


shlibFirst/libfirst.so.1.0.0:     file format elf64-x86-64


Disassembly of section .init:

0000000000000508 <_init>:
 508:   48 83 ec 08             sub    rsp,0x8
 50c:   48 8b 05 cd 0a 20 00    mov    rax,QWORD PTR [rip+0x200acd]        # 200fe0 <__gmon_start__>
 513:   48 85 c0                test   rax,rax
 516:   74 02                   je     51a <_init+0x12>
 518:   ff d0                   call   rax
 51a:   48 83 c4 08             add    rsp,0x8
 51e:   c3                      ret    

Disassembly of section .plt:

0000000000000520 <.plt>:
 520:   ff 35 e2 0a 20 00       push   QWORD PTR [rip+0x200ae2]        # 201008 <_GLOBAL_OFFSET_TABLE_+0x8>
 526:   ff 25 e4 0a 20 00       jmp    QWORD PTR [rip+0x200ae4]        # 201010 <_GLOBAL_OFFSET_TABLE_+0x10>
 52c:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]

Disassembly of section .plt.got:

0000000000000530 <.plt.got>:
 530:   ff 25 c2 0a 20 00       jmp    QWORD PTR [rip+0x200ac2]        # 200ff8 <__cxa_finalize@GLIBC_2.2.5>
 536:   66 90                   xchg   ax,ax

Disassembly of section .text:

0000000000000540 <deregister_tm_clones>:
 540:   48 8d 3d d9 0a 20 00    lea    rdi,[rip+0x200ad9]        # 201020 <_edata>
 547:   48 8d 05 d9 0a 20 00    lea    rax,[rip+0x200ad9]        # 201027 <_edata+0x7>
 54e:   55                      push   rbp
 54f:   48 29 f8                sub    rax,rdi
 552:   48 89 e5                mov    rbp,rsp
 555:   48 83 f8 0e             cmp    rax,0xe
 559:   76 15                   jbe    570 <deregister_tm_clones+0x30>
 55b:   48 8b 05 76 0a 20 00    mov    rax,QWORD PTR [rip+0x200a76]        # 200fd8 <_ITM_deregisterTMCloneTable>
 562:   48 85 c0                test   rax,rax
 565:   74 09                   je     570 <deregister_tm_clones+0x30>
 567:   5d                      pop    rbp
 568:   ff e0                   jmp    rax
 56a:   66 0f 1f 44 00 00       nop    WORD PTR [rax+rax*1+0x0]
 570:   5d                      pop    rbp
 571:   c3                      ret    
 572:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]
 576:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 57d:   00 00 00 

0000000000000580 <register_tm_clones>:
 580:   48 8d 3d 99 0a 20 00    lea    rdi,[rip+0x200a99]        # 201020 <_edata>
 587:   48 8d 35 92 0a 20 00    lea    rsi,[rip+0x200a92]        # 201020 <_edata>
 58e:   55                      push   rbp
 58f:   48 29 fe                sub    rsi,rdi
 592:   48 89 e5                mov    rbp,rsp
 595:   48 c1 fe 03             sar    rsi,0x3
 599:   48 89 f0                mov    rax,rsi
 59c:   48 c1 e8 3f             shr    rax,0x3f
 5a0:   48 01 c6                add    rsi,rax
 5a3:   48 d1 fe                sar    rsi,1
 5a6:   74 18                   je     5c0 <register_tm_clones+0x40>
 5a8:   48 8b 05 41 0a 20 00    mov    rax,QWORD PTR [rip+0x200a41]        # 200ff0 <_ITM_registerTMCloneTable>
 5af:   48 85 c0                test   rax,rax
 5b2:   74 0c                   je     5c0 <register_tm_clones+0x40>
 5b4:   5d                      pop    rbp
 5b5:   ff e0                   jmp    rax
 5b7:   66 0f 1f 84 00 00 00    nop    WORD PTR [rax+rax*1+0x0]
 5be:   00 00 
 5c0:   5d                      pop    rbp
 5c1:   c3                      ret    
 5c2:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]
 5c6:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 5cd:   00 00 00 

00000000000005d0 <__do_global_dtors_aux>:
 5d0:   80 3d 49 0a 20 00 00    cmp    BYTE PTR [rip+0x200a49],0x0        # 201020 <_edata>
 5d7:   75 27                   jne    600 <__do_global_dtors_aux+0x30>
 5d9:   48 83 3d 17 0a 20 00    cmp    QWORD PTR [rip+0x200a17],0x0        # 200ff8 <__cxa_finalize@GLIBC_2.2.5>
 5e0:   00 
 5e1:   55                      push   rbp
 5e2:   48 89 e5                mov    rbp,rsp
 5e5:   74 0c                   je     5f3 <__do_global_dtors_aux+0x23>
 5e7:   48 8b 3d 2a 0a 20 00    mov    rdi,QWORD PTR [rip+0x200a2a]        # 201018 <__dso_handle>
 5ee:   e8 3d ff ff ff          call   530 <.plt.got>
 5f3:   e8 48 ff ff ff          call   540 <deregister_tm_clones>
 5f8:   5d                      pop    rbp
 5f9:   c6 05 20 0a 20 00 01    mov    BYTE PTR [rip+0x200a20],0x1        # 201020 <_edata>
 600:   f3 c3                   repz ret 
 602:   0f 1f 40 00             nop    DWORD PTR [rax+0x0]
 606:   66 2e 0f 1f 84 00 00    nop    WORD PTR cs:[rax+rax*1+0x0]
 60d:   00 00 00 

0000000000000610 <frame_dummy>:
 610:   48 8d 3d 19 08 20 00    lea    rdi,[rip+0x200819]        # 200e30 <__JCR_END__>
 617:   48 83 3f 00             cmp    QWORD PTR [rdi],0x0
 61b:   75 0b                   jne    628 <frame_dummy+0x18>
 61d:   e9 5e ff ff ff          jmp    580 <register_tm_clones>
 622:   66 0f 1f 44 00 00       nop    WORD PTR [rax+rax*1+0x0]
 628:   48 8b 05 b9 09 20 00    mov    rax,QWORD PTR [rip+0x2009b9]        # 200fe8 <_Jv_RegisterClasses>
 62f:   48 85 c0                test   rax,rax
 632:   74 e9                   je     61d <frame_dummy+0xd>
 634:   55                      push   rbp
 635:   48 89 e5                mov    rbp,rsp
 638:   ff d0                   call   rax
 63a:   5d                      pop    rbp
 63b:   e9 40 ff ff ff          jmp    580 <register_tm_clones>

0000000000000640 <shlib_function>:
#include "shlibexports.h"

int shlib_function(void)
{
 640:   55                      push   rbp
 641:   48 89 e5                mov    rbp,rsp
 return 10;
 644:   b8 0a 00 00 00          mov    eax,0xa
 649:   5d                      pop    rbp
 64a:   c3                      ret    

Disassembly of section .fini:

000000000000064c <_fini>:
 64c:   48 83 ec 08             sub    rsp,0x8
 650:   48 83 c4 08             add    rsp,0x8
 654:   c3                      ret    
 ```