---
title: Information is Bits + Context
tags:
  - Bits
---
A program is a sequence of bits, each with a value of 0 or 1, organized in **8-bit** chunks called **bytes**.

Most modern systems represent text characters using the ASCII standard that represents each character with a unique byte-sized integer value.

```c
#include <stdio.h>

int main(){
	printf("hello, world\n");
}
```

| #   | i   | n   | c   | l   | u   | d   | e   | \<sp> | <   | s   |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- |
| 35  | 105 | 110 | 99  | 108 | 117 | 100 | 101 | 32    | 60  | 115 |

## Programs are translated by other programs into different forms
The `hello.c` program begins as a high-level C program because it can be read and understood by human beings.

However, in order to run `hello.c` on the system the individual C statement must be translated into a sequence of low-level machine-language instruction. 
These instructions are then packaged in a form called an `executable object` program and stored in a binary disk file

On Unix system the translation from source file to object file is performed by a complier driver:
```unix
gcc -o hello hello.c
```

![[Pasted image 20260514082437.png]]

GCC compiler driver reads the source file `hello.c` and translates it into an executable object file `hello`. Translation is performed in 4 phases.
The programs that perform the 4 phases (preprocessor, compiler, assembler, linker) are known collectively as the `compilation system`

### Preprocessing Phase
The preprocessor (cpp) modifies the original C program according to directives that begin with `#` so the statement `# include <stdio.h>` tells the preprocessor to read the contents of the system header filer and insert it **directly** into the program text. 
This results in another C program, typically with the .i suffix

### Compilation Phase
The compiler (cc1) translates the text file `hello.i` into the text file `hello.s` which contains an assembly-language program. 
Each statement in assembly-language exactly describes 1 low-level machine-language instruction in a standard text form.

Assembly is useful because it provides a common output language for different compilers for different high-level language.

### Assembly Phase
The assembler (as) translates `hello.s` into machine-language instructions, packages them in a form known as *relocatable object program* and stores it as `hello.o`. It is a binary file whose bytes encode machine language instructions rather than characters. If we were to view `hello.o` with a text editor, it would appear to be gibberish.

### Linking Phase
Our `hello.c` calls the `printf` function which is part of the standard C library provided by every C compiler. The `printf` function exists in a separate precompiled object file called `printf.o` which needs to be merged with our `hello.o` program.
The linker (ld) handles this merging. The result is the `hello` file, which is an executable object file that is ready to be loaded into memory and executed by the system.