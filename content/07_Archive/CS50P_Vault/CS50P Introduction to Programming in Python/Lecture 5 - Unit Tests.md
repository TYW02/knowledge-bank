Python Program: [[test_calculator.py]], [[test_hello.py]]
Topic Covered: 
Current Status:
> [!INFO]
> | Name | Status | Timestamp |
> | -----| -----| -----|
> | Not Started | <input type="checkbox">| |
> | Started | <input type="checkbox" > |   |
> | Completed | <input type="checkbox" checked> | |  

Youtube link: [Here](https://www.youtube.com/watch?v=tIrcxwLqzjQ&list=PLhQjrBD2T3817j24-GogXmWqO5Q5vYy0V&index=10)

----


# assert
- What does it do ?
	- The ==assert== keyword is used when debugging code.
	- The ==assert== keyword lets you test if a condition in your code returns True, if not, the program will raise an AssertionError.
	- You can write a message to be written if the code returns False.


#### Example
```python
x = "hello"

# if condition returns True, then nothing happens:
assert x == "hello"

# if condition returns False, AssertionError is raised:
assert x == "goodbye"

```


## Documents
Click [[test_calculator.py#assert|Code Example]]

Click [Documents](https://www.w3schools.com/python/ref_keyword_assert.asp)


----



# pytest

- What does it do ?
	- The ==pytest== framework makes it easy to write small, readable test, and can scale to support complex functional testing for applications and libraries

## Features
- Detailed info on failing assert statements 
- Auto-discorvery of test modules and functions
- Modular fixtures for managning small or parameterized long-lived test resources
- Can run unittest and nose test suites out of the box


## Documents
Click [[test_calculator.py#Using pytest|Code Example]]

Click [Documents](https://docs.pytest.org/en/7.2.x/)


----























