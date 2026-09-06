---
title: Lab 1 Bit Manipulation in C
tags:
  - BitManipulation
---
# Bit Shifting & AND comparison
```C
/ * -------------------------------------------
  * Count how many bits are set in a value
  * count_bits(0xFF) must be 8. count_bits(-1) must be 32.
  * -------------------------------------------- */
uint8_t count_bits(int value)
{
    uint8_t count = 0

    while (value) {
        count += value & 1;
        value >>= 1;
    }
    return count;
}
```

0xFF -> 255 (Hex to decimal)
> The first F is ($15 * 16^0$) and the second F is ($15 * 16^1$) = 240 so 240 + 15 = 255

1111 1111 (Binary of 255)
```C
count += value & 1
```
This take a bit from `value` and `&` compares it with `1` so if we compare `1` & `1` then we get `1` you can take the `&` as a AND gate. 
- After we increment the count by 1
- We shift value over by 1. To continue counting the no. of bits in `value`

Since we want `count_bits(-1) = 32` 
```C
#include <stdint.h>

uint8_t count_bits(int value)
{
    uint8_t count = 0;
    // Cast to uint32_t to treat the bits as unsigned and prevent an infinite loop
    uint32_t u_value = (uint32_t)value; 

    while (u_value) {
        count += u_value & 1;
        u_value >>= 1; // Logical shift: inserts 0s at the top
    }
    return count;
}

```

1. `-1` is being stored as a `int`, assuming a 16 bit size int value `-1` would be `1111111111111111` 
2. We then cast it as a `uint32_t` so we get 32 `1` 
3. Our counting logic will then work and return 32

> [!NOTE]
> We need to have the type conversion because `value` is type `int` and when we do `>>=` it will preserve the negative sign by padding the new space with `1` instead of `0` 


# Order of operations 
```C
/* ------------------------------------------------------------------
 * 3. True when the given pin's bit is CLEAR in the mask.
 *    pin_is_clear(0x24, 2) is false - bit 2 is set.
 *    pin_is_clear(0x24, 3) is true  - bit 3 is clear.
 * ------------------------------------------------------------------ */
bool pin_is_clear(uint32_t mask, unsigned pin)
{
    return (mask & 1u << pin == 0);
}
```

- 0x24 = ($2 * 16^1$) + ($2 * 16^0$) = 32 + 2 = 34
- 34 to binary = 0010 0010
- 1u means the number 1 unsigned, so in binary that's `0000 0001`


> [!Breakdown]
> The main purpose of this function is to check if a certain bit `pin` is clear.
> To do so we that `1u` which is `0000 0001` and shift it by `pin` amount and use a AND operator to compare.
> If the result is 0 we return a boolean value.
> 
> Example: input: 0x24, pin 3
> 0x24: `0010 0010` 
> 1u << pin = `0000 0001` << 3 = `0000 1000`
> 
> |  | 0010 0100|
> | --- |--- |
> | & | 0000 1000|
> | | 0000 0000|
> a
> Since we get `0000 0000` at the end and we `== 0` we return true



