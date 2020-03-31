# Understanding ELF(Executable and linkable format)

Below is the sample code `mem_layout.c` which is used to investigate the memory layout in a ELF file. 

```c
  int global_unintialized;
  int global_initialized = 66;
  static int static_unintialized;
  static int static_initialized = 77;

  int main(){
        int a = 123;
        int b = 456;
        return 0;
  }
```

First, compile and assemble  `mem_layout.c` using `gcc -c mem_layout.c`.  And we get the result as below. `COM` indicates that the uninitialized global variable `global_unintialized` is indexed `COMMON`. As a matter of fact, together with `UNDEF` and `ABS`, they are three kinds of sections that will only appear in the object file rather than the executable. What's more, there is no entry for them in the header table.

```bash
Symbol table '.symtab' contains 13 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS mem_layout.c
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1
     3: 0000000000000000     0 SECTION LOCAL  DEFAULT    2
     4: 0000000000000000     0 SECTION LOCAL  DEFAULT    3
     5: 0000000000000000     4 OBJECT  LOCAL  DEFAULT    3 static_unintialized
     6: 0000000000000004     4 OBJECT  LOCAL  DEFAULT    2 static_initialized
     7: 0000000000000000     0 SECTION LOCAL  DEFAULT    5
     8: 0000000000000000     0 SECTION LOCAL  DEFAULT    6
     9: 0000000000000000     0 SECTION LOCAL  DEFAULT    4
    10: 0000000000000004     4 OBJECT  GLOBAL DEFAULT  COM global_unintialized
    11: 0000000000000000     4 OBJECT  GLOBAL DEFAULT    2 global_initialized
    12: 0000000000000000    25 FUNC    GLOBAL DEFAULT    1 main
```

Another way to get the symbol table is to execute`objdump -t mem_layout.o` and we have the following output. From two symbol table we can see that for Enum `Ndx`, `1` means `.text`, `2` means `.data` and `3` means `.bss` etc. 

```bash
mem_layout.o:     file format elf64-x86-64

SYMBOL TABLE:
0000000000000000 l    df *ABS*  0000000000000000 mem_layout.c
0000000000000000 l    d  .text  0000000000000000 .text
0000000000000000 l    d  .data  0000000000000000 .data
0000000000000000 l    d  .bss   0000000000000000 .bss
0000000000000000 l     O .bss   0000000000000004 static_unintialized
0000000000000004 l     O .data  0000000000000004 static_initialized
0000000000000000 l    d  .note.GNU-stack        0000000000000000 .note.GNU-stack
0000000000000000 l    d  .eh_frame      0000000000000000 .eh_frame
0000000000000000 l    d  .comment       0000000000000000 .comment
0000000000000004       O *COM*  0000000000000004 global_unintialized
0000000000000000 g     O .data  0000000000000004 global_initialized
0000000000000000 g     F .text  0000000000000019 main
```

Some may wrongly think that the `symbol table` only comes with the `-g` flag, which is clearly not the case as demonstrated above. The `symbol table` is actually quite different from the symbol table used by the compiler, as there are no local variables included.

Below is part of the section layout of `mem_layout.o`, which is generated using  `objdump -D mem_layout.o`, We can therefore have the conclusion:

For a given variable `a`,

- If `a` is a`static` variable (another keyword that seems a little confusing, it would be better to choose `private`in the first place), then it is clear that it will locate in `.bss` if it is uninitialized, in `.data` if it is initialized.
- if `a` is a `global`variable, then `a` will be a weak definition if it is uninitialized, thus the compiler would have hard time finding the correct declaration before the linking stage, in which case it will be placed in `COMMON `. `a` will be in `.data` if it is properly initialized. 

```bash
mem_layout.o:     file format elf64-x86-64
Disassembly of section .text:
0000000000000000 <main>:
   0:   55                      push   %rbp
   1:   48 89 e5                mov    %rsp,%rbp
   4:   c7 45 f8 7b 00 00 00    movl   $0x7b,-0x8(%rbp)
   b:   c7 45 fc c8 01 00 00    movl   $0x1c8,-0x4(%rbp)
  12:   b8 00 00 00 00          mov    $0x0,%eax
  17:   5d                      pop    %rbp
  18:   c3                      retq

Disassembly of section .data:
0000000000000000 <global_initialized>:
   0:   42 00 00                rex.X add %al,(%rax)
0000000000000004 <static_initialized>:
   4:   4d 00 00                rex.WRB add %r8b,(%r8)

Disassembly of section .bss:
0000000000000000 <static_unintialized>:
   0:   00 00                   add    %al,(%rax)
```

Next, we want to see the header table of section. By executing `objdump -h mem_layout.o`, we have the following output. As we mentioned before, there is no entry for `.COM`, `.UNDEF`, `.ABS`.

```bash
mem_layout.o:     file format elf64-x86-64
mem_layout.o
architecture: i386:x86-64, flags 0x00000011:
HAS_RELOC, HAS_SYMS
start address 0x0000000000000000

Sections:
Idx Name          Size      VMA               LMA               File off  Algn
  0 .text         00000019  0000000000000000  0000000000000000  00000040  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
  1 .data         00000008  0000000000000000  0000000000000000  0000005c  2**2
                  CONTENTS, ALLOC, LOAD, DATA
  2 .bss          00000004  0000000000000000  0000000000000000  00000064  2**2
                  ALLOC
  3 .comment      0000002a  0000000000000000  0000000000000000  00000064  2**0
                  CONTENTS, READONLY
  4 .note.GNU-stack 00000000  0000000000000000  0000000000000000  0000008e  2**0
                  CONTENTS, READONLY
  5 .eh_frame     00000038  0000000000000000  0000000000000000  00000090  2**3
                  CONTENTS, ALLOC, LOAD, RELOC, READONLY, DATA
```

Tips:

- when using `objdump`, add flag `-D` for displaying assembler contents of all sections(I haven't figure it out why the `header table` and `symbol table` are missing), add `-x` to display both `header table` and `symbol table`.





