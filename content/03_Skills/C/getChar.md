---
title: getChar
---

Used from standard library
```C
#include <stdio.h>
int main() {
	int character;
	character = getchar();
	
	printf("The entered character is: %c", character)
}
```

# What it does
Reads one character at a time from standard input stream.
Define in stdio.h file

# Return Value
- Returns entered character as an integer representing its ASCII value
- Returns EOF if input stream is reached or input error occurs

