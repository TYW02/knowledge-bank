---
title: C Bit-Wise Operators
tags:
  - Bits
---
```C
int main() 
{
	// BITWISE OPERATORS = Special operators used in bit level programming
	
	// & = AND
	// | = OR
	// ^ = XOR
	// << = Left Shift
	// >> = Right Shift
	// ~ = Complement
	
	int x = 6;  // 6 = 00000110
	int y = 12; //12 = 00001100
	int z = 0;  // 0 = 00000000
	
	z = x & y; // 4 = 00000100
	printf("AND = %d\n", z);
	
	z = x | y; // 14 = 00001110
	printf("OR = %d\n", z);
	
	z = x ^ y; // 10 = 00001010
	printf("XOR = %d\n", z);
	
	z = x << 1; // 12 = 00001100
	printf("SHIFT LEFT = %d\n", z); // Every time you shift left the number doubles
	
	z = x >> 1; // 3 = 00000011
	printf("SHIFT RIGHT = %d\n", z); // Shift right and the number halves

	
}
```
































