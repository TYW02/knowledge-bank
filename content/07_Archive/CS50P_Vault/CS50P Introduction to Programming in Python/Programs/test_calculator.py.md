Tags: [[Lecture 5 - Unit Tests]]


# calculator.py
```python
def main():
	x = int(input("What's x? "))
	print("x squared is", square(x))


def square(n):
	return n + n

if __name__ == "__main__"
	main()
```




```python
from calculator import square

def main():
	test_square()

def test_square():
	if square(2) != 4:
		print("2 squared was not 4")
	if square(3) != 9:
		print("3 squared was not 9")

if __name__ == "__main__":
	main()


> Output:
> 3 squared was not 9
```
- The "2 squared was not 4" error did not go off because 2 + 2 = 4 



## assert
```python
from calculator import square

def main():
	test_square()

def test_square():
	assert square(2) == 4
	assert square(3) == 9

if __name__ == "__main__":
	main()

> AssertionError
```



## Using try except
```python
from calculator import square

def main():
	test_square()

def test_square():
	try:
		assert square(2) == 4
	except AssertionError:
		print("2 squared was not 4")
	try:
		assert square(3) == 9
	except AssertionError:
		print("3 squared was not 9 ")

if __name__ == "__main__":
	main()

> Output: 3 squared was not 9

----------------------------------------------------------------------------------------



from calculator import square

def main():
	test_square()

def test_square():
	try:
		assert square(2) == 4
	except AssertionError:
		print("2 squared was not 4")
	try:
		assert square(3) == 9
	except AssertionError:
		print("3 squared was not 9 ")
	try:
		assert square(-2) == 4
	except AssertionError:
		print("-2 squared was not 4")
	try:
		assert square(-3) == 9
	except AssertionError:
		print("-3 squared was not 9 ")
	try:
		assert square(0) == 0
	except AssertionError:
		print("0 squared was not 0 ")

if __name__ == "__main__":
	main()

> Output:
3 squared was not 9
-2 squared was not 4
-3 squared was not 9
```



## Using pytest
```python
from calculator import sqaure

def test_square():
	assert square(2) == 4
	assert square(3) == 9 
	assert square(-2) == 4
	assert square(-3) == 9
	assert square(0) == 0 

$ pytest test_calculator.py

test_calculator.py F                                                                                             [100%]

====================================FAILURES============================================
___________________________________test_square__________________________________________

    def test_square():
        assert square(2) == 4
>       assert square(3) == 9
E       assert 6 == 9
E        +  where 6 = square(3)

test_calculator.py:9: AssertionError
==============================short test summary info===================================
FAILED test_calculator.py::test_square - assert 6 == 9
==================================1 failed in 0.24s ====================================

```
- The 2nd E line is the actual value VS what you are asserting against.



## Improving pytest design
```python
from calculator import sqaure

def test_positive():
	assert square(2) == 4
	assert square(3) == 9 

def test_negative():
	assert square(-2) == 4
	assert square(-3) == 9

def test_zero():
	assert square(0) == 0 

$ pytest test_calculator.py

test_calculator.py FF.                                                                                           [100%]

================================== FAILURES ============================================
___________________________________ test_positive ______________________________________
    def test_positive():
        assert square(2) == 4
>       assert square(3) == 9
E    assert 6 == 9
E     +  where 6 = square(3)

test_calculator.py:11: AssertionError
_______________________________________ test_negative _________________________________

    def test_negative():
>       assert square(-2) == 4
E    assert -4 == 4
E     +  where -4 = square(-2)

test_calculator.py:14: AssertionError
================================= short test summary info ==============================
FAILED test_calculator.py::test_positive - assert 6 == 9
FAILED test_calculator.py::test_negative - assert -4 == 4
================================ 2 failed, 1 passed in 0.24s ===========================
```


## Testing user input
```python
import pytest
from calculator import sqaure

def test_positive():
	assert square(2) == 4
	assert square(3) == 9 

def test_negative():
	assert square(-2) == 4
	assert square(-3) == 9

def test_zero():
	assert square(0) == 0 

def test_str():
	with pytest.raises(TypeError):
		square("cat")

$ pytest test_calculator.py

test_calculator.py ....                                                                                          [100%]

=================================== 4 passed in 0.03s ==================================

```



















































