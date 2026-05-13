
# Substring
```postgresql
SELECT LEFT ('abcde', 2) -- first 2 character
	RIGHT('abcde', 2); --LAST 2 CHARACTER
```

```postgresql
SELECT LEFT('abc', 10),
	length(left('abc', 10));
```

```postgresql
SELECT substring(string FROM start FOR length);
```

```postgresql
SELECT substring('abcdef' FROM 2 FOR 3);
```

```postgresql
SELECT substr('abcdef', 2, 3);
```


# Splitting on a delimiter
```postgresql
SELECT split_part(string, delimiter, part);
```

```postgresql
SELECT split_part('a,bc,d', ',', 2);
```




# Splitting on a delimiter
```postgresql
SELECT split_part('cats and dogs and fish' , '   and   ', 1);
```



# Concatenating text
```postgresql
SELECT concat('a', 2, 'cc');
```

```postgresql
SELECT 'a' || 2 || 'cc';
```

```postgresql
SELECT concat('a', NULL, 'cc');
```

```postgresql
SELECT 'a' || NULL || 'cc';
```











































