

# Commonly used extensions
- PostGIS
- PostPic
- fuzzystrmatch
- pg_trgm



# Querying extension meta data

### Available Extensions
```postgresql
SELECT name
FROM pg_available_extensions;
```


### Installed Extensions
```postgresql
SELECT extname
FROM pg_extension;
```



```postgresql
--Enable the fuzzystrmatch exntension
CREATE EXTENSION IF NOT EXISTS fuzzystrmatch;
-- Confirm that fuzzstrmatch has been enabled
SELECT extname FROM pg_extension;
```



# Using fuzzystrmatch or fuzzy searching
```postgresql
SELECT levenshtein('GUMBO' , 'GAMBOL');
```



# Compare two strings with pg_trgm
```postgresql
SELECT similarity('GUMBO', 'GAMBOL');
```



























