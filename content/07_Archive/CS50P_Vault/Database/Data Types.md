

----

# SQL Data Types

- When a table is created, a data type must be indicated for each field
- Different types of data are stored differently and take up different amounts of storage space
- Some operations only apply to certain data types.

## Strings

- Sequence of characters such as letters or punctuation.
- Storing short strings in a small data type saves storage space
    - VARCHAR is more flexible and can store small or large strings
    - Up to thousands of characters

## Integers

- Integer data types store whole numbers
- INT, a common SQL integer data type, can store numbers from less than negative two billion to more than positive two billion!

## Floats

- Float data types store numbers that include a fractional part
- SQL also offers several float data types depending on how many digits the numbers in the field are expected to be

- NUMERIC data type can store floats which have up to 38 digits total

## Schemas

- Schemas are often referred to as "blueprints" of databases.
- A schema shows a database's design, such as what tables are included in the database and any relationships between its tables.
- A schema also lets the reader know what data type each field can hold.

## Database Storage

- The information we find in a database table is physically stored on the hard disk of a server.
- Servers are centralized computers that perform services via requests made over a network.

---