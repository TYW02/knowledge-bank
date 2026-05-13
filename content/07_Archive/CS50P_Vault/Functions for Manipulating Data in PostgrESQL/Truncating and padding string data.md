

# Removing whitespace from strings

```postgresql
TRIM([leading | trailing | both] [characters] from string)
```

- First parameter: [leading | trailing | both]
- Second parameter: [characters]
- Third parameter: from string

```postgresql
SELECT TRIM('  padded   ');
```


```postgresql
SELECT RTRIM('   padded   ')
```

```postgresql
SELECT LTRIM('   padded   ');
```

The LTRIM and RTRIM functions are analogous to TRIM but only remove characters from either the beginning OR the end of the string, not both.



# Padding strings with character data
```postgresql
SELECT LPAD('padded', 10, '#');
```

```postgresql
=--------------+
| LPAD         |
| ####padded   |
+--------------+
```


# Padding strings with whitespace
```postgresql
SELECT LPAD('padded', 10);
```

```postgresql
SELECT LPAD('padded', 5);
```


```postgresql
SELECT RPAD('padded', 10, '#');
```

































