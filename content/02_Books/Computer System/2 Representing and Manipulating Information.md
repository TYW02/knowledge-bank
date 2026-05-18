Modern computers store and process information represented as two-valued signals called binary digits, or *bits* and they form the basis of the digital revolution.

2-values signals can readily be represented, stored, and transmitted.
For example:
- Presence or absence of a hole in a punched card
- High or low voltage on a wire
- Magnetic domain oriented clockwise or counterclockwise

We consider the 3 most important representations of numbers. 
*Unsigned* encodings are based on traditional binary notation, representing numbers greater than or equal to 0.
*Two's-Complement* encoding are the most common way to represent **signed** integers, numbers that may be either positive or negative.
*Floating-point* encodings are a base-2 version of scientific notation for representing real numbers


# 2.1 Information Storage
Rather than accessing individual bits in memory, most computers use blocks of 8 bits, or bytes as the smallest addressable unit of memory. 
A machine-level program views memory as a very large array of bytes called *virtual memory*. Every byte of memory is identified by a unique number, known as its *address* and the set of all possible addresses is known as the *virtual address space* 

A single byte consists of 8 bits. In binary notation, its values ranges from 00000000 to 11111111. When viewed as a decimal integer, its values ranges from 0 to 255. Neither notation is very convenient for describing bit patterns.

Instead, we write bit patterns as base-16 or hexadecimal numbers, where the value of a single bytes can range from 00 to FF.

A common task in working with machine-level programs is to manually convert between decimal, binary and hexadecimal is straightforward, since it can be performed 1 hexadecimal digit at a time.


# 2.1.2 Data Sizes
Every computer has a *word size* indicating the nominal size of pointer data. Since a virtual address is encoded by such a word, the most important system parameter determined by the word size is the maximum size of the virtual addresses can range from $0 to 2^w - 1$.

A 32-bit word size limits the virtual address space to 4GB while scaling up to a 64-bit word size leads to a virtual address space of 16 exabytes

Most 64-bit machines can also run programs compiled for use on 32-bit machines, a form of backward compatibility
### Examples
```linux
gcc -m32 prog.c
```
this program will run correctly on either a 32-bit or a 64-bit machine. On the other hand, a program compiled with the directive
```linux
gcc -m64 prog.c
```

will only run on a 64-bit machine. Therefore we refer to programs as being either "32-bit programs" or "64-bit programs" since the distinction lies in how a program is compiled rather than the type of machine it runs on.

# 2.1.3 Addressing and Byte Ordering
