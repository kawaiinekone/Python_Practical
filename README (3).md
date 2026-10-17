# Programming Using Python - Practical Record

**Name:** Shubhi Rai
**Course:** B.Sc. (Hons.) Computer Science
**Semester:** I
**Roll Number:** 26570059
**Subject:** Programming Using Python

This repository contains my solutions to Practicals 01 to 15 of Programming Using Python. Each practical has the problem statement, the code, and a sample test.

## How to run

Install Python 3, save a program as a `.py` file, and run it from the terminal:

```bash
python practical_01_quadratic_roots.py
```

On some systems you may need to use `python3` instead of `python`.

## Contents

1. Quadratic equation
2. Prime numbers
3. Star pyramids
4. Character classification
5. String operations
6. Swap prefixes of two strings
7. Substring indices
8. Cubes of even integers
9. File handling
10. Dictionary of cubes
11. Tuple operations
12. Employee class and object counting
13. Class Point2D
14. Inheritance: class Point3D
15. Exception handling for a name

---

## Practical 01 - Roots of a Quadratic Equation

**Problem:** Write a program to find the roots of the quadratic equation ax^2 + bx + c = 0. Use the discriminant D = b^2 - 4ac to decide whether the roots are real and distinct, real and equal, or complex.

```python
import math

a = float(input("Enter a: "))
b = float(input("Enter b: "))
c = float(input("Enter c: "))

if a == 0:
    print("Not a quadratic equation")
else:
    d = b**2 - 4*a*c

    if d > 0:
        r1 = (-b + math.sqrt(d)) / (2*a)
        r2 = (-b - math.sqrt(d)) / (2*a)
        print("Two distinct real roots:", r1, r2)
    elif d == 0:
        print("Equal roots:", -b / (2*a))
    else:
        real = -b / (2*a)
        imag = math.sqrt(-d) / abs(2*a)
        print(f"Complex roots: {real} ± {imag}i")
```

**Sample test:** a = 1, b = -5, c = 6 gives roots 3.0 and 2.0.

**Note:** The check `a == 0` avoids division by zero and rejects equations that are not quadratic.

---

## Practical 02 - Prime Numbers

**Problem:** Write programs to:

- (a) check whether an integer is prime
- (b) generate all primes up to n
- (c) generate the first n primes

```python
from math import isqrt


def is_prime(n):
    """Return True if n is prime, otherwise False."""
    if n < 2:
        return False

    for divisor in range(2, isqrt(n) + 1):
        if n % divisor == 0:
            return False

    return True


# (a) Check whether a number is prime
number = int(input("Enter an integer to check: "))
print("Prime" if is_prime(number) else "Not prime")


# (b) All primes up to n
limit = int(input("Generate primes up to: "))
for number in range(2, limit + 1):
    if is_prime(number):
        print(number, end=" ")
print()


# (c) First n primes
n = int(input("How many prime numbers? "))
number = 2
count = 0

while count < n:
    if is_prime(number):
        print(number, end=" ")
        count += 1
    number += 1
print()
```

**Sample test:**

- 17 -> Prime
- 1 -> Not prime
- Primes up to 10 -> 2 3 5 7
- First 5 primes -> 2 3 5 7 11

**Note:** Only divisors up to the square root of n need to be checked. The same `is_prime()` function is used in all three parts.

---

## Practical 03 - Star Pyramids

**Problem:** Write a program to print a pyramid of `*` and a reverse pyramid.

```python
n = int(input("Enter number of rows: "))

print("Pyramid:")
for i in range(1, n + 1):
    print(" " * (n - i) + "* " * i)

print("Reverse pyramid:")
for i in range(n, 0, -1):
    print(" " * (n - i) + "* " * i)
```

**Sample output (n = 3):**

```text
Pyramid:
  *
 * *
* * *

Reverse pyramid:
* * *
 * *
  *
```

---

## Practical 04 - Character Classification

**Problem:** Accept one character and:

- (a) say whether it is a letter, a digit, or a special character
- (b) if it is a letter, say whether it is uppercase or lowercase
- (c) if it is a digit, print its name in words (for example 9 -> NINE)

```python
ch = input("Enter one character: ")

if len(ch) != 1:
    print("Please enter exactly one character")
elif ch.isalpha():
    print("Letter")
    if ch.isupper():
        print("Uppercase")
    else:
        print("Lowercase")
elif ch.isdigit() and ch.isascii():
    words = [
        "ZERO", "ONE", "TWO", "THREE", "FOUR",
        "FIVE", "SIX", "SEVEN", "EIGHT", "NINE"
    ]
    print("Numeric digit")
    print(words[int(ch)])
else:
    print("Special character")
```

**Sample test:**

- A -> Letter, Uppercase
- m -> Letter, Lowercase
- 9 -> Numeric digit, NINE
- @ -> Special character

---

## Practical 05 - String Operations

**Problem:** Write programs to:

- (a) find the frequency of a character in a string
- (b) replace a character with another character
- (c) remove the first occurrence of a character
- (d) remove all occurrences of a character

```python
# (a) Frequency of a character
s = input("Enter a string: ")
ch = input("Character to count: ")
print("Frequency:", s.count(ch))


# (b) Replace a character
s = input("Enter a string: ")
old = input("Character to replace: ")
new = input("Replacement character: ")
print("Updated string:", s.replace(old, new))


# (c) Remove the first occurrence
s = input("Enter a string: ")
ch = input("Character to remove: ")
print("Result:", s.replace(ch, "", 1))


# (d) Remove all occurrences
s = input("Enter a string: ")
ch = input("Character to remove: ")
print("Result:", s.replace(ch, ""))
```

**Sample test:** For the string `banana` and the character `a`:

- Frequency -> 3
- Remove first occurrence -> bnana
- Remove all occurrences -> bnn

**Note:** Strings are immutable, so `replace()` returns a new string and the original is unchanged.

---

## Practical 06 - Swap the First n Characters of Two Strings

**Problem:** Write a program to exchange the first n characters of two strings and keep the remaining characters as they are.

```python
s1 = input("Enter first string: ")
s2 = input("Enter second string: ")
n = int(input("Enter n: "))

if n < 0 or n > len(s1) or n > len(s2):
    print("Invalid value of n")
else:
    prefix1 = s1[:n]
    prefix2 = s2[:n]

    result1 = prefix2 + s1[n:]
    result2 = prefix1 + s2[n:]

    print("First string:", result1)
    print("Second string:", result2)
```

**Sample test:** Strings `abcdef` and `123456`, n = 2

```text
First string: 12cdef
Second string: ab3456
```

---

## Practical 07 - Find All Indices of a Substring

**Problem:** Write a function that takes two strings and returns a list of all starting indices where the second string occurs in the first. Return -1 if it does not occur.

```python
def find_indices(s, sub):
    if sub == "":
        return -1

    indices = []
    start = 0

    while True:
        index = s.find(sub, start)

        if index == -1:
            break

        indices.append(index)
        start = index + 1  # allows overlapping matches

    return indices if indices else -1


text = input("Enter the main string: ")
substring = input("Enter the substring: ")

print(find_indices(text, substring))
```

**Sample test:**

```text
Main string: banana
Substring: ana
Result: [1, 3]
```

If the substring is `xyz`, the function returns -1.

**Note:** Moving `start` forward by one (instead of the length of the substring) lets overlapping matches be found.

---

## Practical 08 - Cubes of Even Integers in a List

**Problem:** Given a list that may contain elements of different types, create a new list with the cubes of only the even integers, using:

- (a) a `for` loop
- (b) list comprehension

**(a) Using a for loop**

```python
import ast

items = ast.literal_eval(input("Enter a list: "))
result = []

for x in items:
    if type(x) is int and x % 2 == 0:
        result.append(x ** 3)

print(result)
```

**(b) Using list comprehension**

```python
import ast

items = ast.literal_eval(input("Enter a list: "))

result = [x ** 3 for x in items if type(x) is int and x % 2 == 0]

print(result)
```

**Sample test:**

Input: `[2, 3, 4, 5, 6, "hello", 2.5, True]`

Output: `[8, 64, 216]`

**Note:** `type(x) is int` is used instead of `isinstance` so that Boolean values are left out, since `bool` is a subclass of `int` in Python. `ast.literal_eval()` is used to read the list safely from input.

---

## Practical 09 - File Handling

**Problem:** Write a program to read a file and:

- (a) count the total number of characters, words, and lines
- (b) find the frequency of every character using a dictionary
- (c) print the words in reverse order
- (d) copy the even-numbered lines to `File1` and the odd-numbered lines to `File2`

```python
from collections import Counter

filename = input("Enter input filename: ")

try:
    with open(filename, "r", encoding="utf-8") as file:
        text = file.read()

    # (a) Count characters, words and lines
    print("Characters:", len(text))
    print("Words:", len(text.split()))
    print("Lines:", len(text.splitlines()))

    # (b) Frequency of each character
    frequency = Counter(text)
    print("Character frequency:", dict(frequency))

    # (c) Words in reverse order
    words = text.split()
    print("Words in reverse order:", " ".join(words[::-1]))

    # (d) Even lines to File1, odd lines to File2
    lines = text.splitlines()

    with open("File1", "w", encoding="utf-8") as f1, \
         open("File2", "w", encoding="utf-8") as f2:
        for line_number, line in enumerate(lines, start=1):
            if line_number % 2 == 0:
                f1.write(line + "\n")
            else:
                f2.write(line + "\n")

    print("Even lines copied to File1.")
    print("Odd lines copied to File2.")

except FileNotFoundError:
    print("Input file not found.")
```

**Example:** If the input file contains:

```text
Python is fun
Files are useful
Learn every day
```

then File1 (even lines) contains:

```text
Files are useful
```

and File2 (odd lines) contains:

```text
Python is fun
Learn every day
```

**Note:** The character count and frequency include spaces and newline characters. `splitlines()` does not count a trailing newline as an extra line.

---

## Practical 10 - Dictionary of Cubes

**Problem:** Write a function that returns a dictionary whose keys are the integers 1 to 5 and whose values are the cubes of the keys.

**Using a loop**

```python
def cube_dict():
    cubes = {}

    for i in range(1, 6):
        cubes[i] = i ** 3

    return cubes


print(cube_dict())
```

**Using dictionary comprehension**

```python
def cube_dict():
    return {i: i**3 for i in range(1, 6)}


print(cube_dict())
```

**Output:**

```text
{1: 1, 2: 8, 3: 27, 4: 64, 5: 125}
```

---

## Practical 11 - Tuple Operations

**Problem:** Given the tuple `t1 = (1, 2, 5, 7, 9, 2, 4, 6, 8, 10)`, write a program to:

- (a) print half of the values on one line and the other half on the next line
- (b) create a tuple containing only the even values
- (c) concatenate `t2 = (11, 13, 15)` with `t1`
- (d) find the maximum and minimum values

```python
t1 = (1, 2, 5, 7, 9, 2, 4, 6, 8, 10)

# (a) Print the two halves
mid = len(t1) // 2
print("First half:", t1[:mid])
print("Second half:", t1[mid:])

# (b) Tuple of even values
even = tuple(x for x in t1 if x % 2 == 0)
print("Even values:", even)

# (c) Concatenate t2 with t1
t2 = (11, 13, 15)
t3 = t1 + t2
print("Concatenated tuple:", t3)

# (d) Maximum and minimum
print("Maximum:", max(t1))
print("Minimum:", min(t1))
```

**Output:**

```text
First half: (1, 2, 5, 7, 9)
Second half: (2, 4, 6, 8, 10)
Even values: (2, 2, 4, 6, 8, 10)
Concatenated tuple: (1, 2, 5, 7, 9, 2, 4, 6, 8, 10, 11, 13, 15)
Maximum: 10
Minimum: 1
```

**Note:** Tuples are immutable, so slicing, filtering, and concatenation create new tuples instead of changing `t1`.

---

## Practical 12 - Employee Class and Object Counting

**Problem:** Define a class `Employee` to store employee number, name, department, basic salary, DA, and HRA. The class should:

- keep a count of employee objects
- initialize the details using `__init__()`
- stop execution if Basic, DA, or HRA is negative
- return the total salary using `salary()`
- decrease the object count using `__del__()`
- display the details and salary using `__str__()`

**Version 1 - Syllabus-based solution**

```python
class Employee:
    count = 0

    def __init__(self, emp_no, name, dept, basic, da, hra):
        if basic < 0 or da < 0 or hra < 0:
            raise SystemExit("Salary components cannot be negative.")

        self.emp_no = emp_no
        self.name = name
        self.dept = dept
        self.basic = basic
        self.da = da
        self.hra = hra

        Employee.count += 1

    def salary(self):
        return self.basic + self.da + self.hra

    def __str__(self):
        return (
            f"Employee No: {self.emp_no}\n"
            f"Name: {self.name}\n"
            f"Department: {self.dept}\n"
            f"Basic: {self.basic:.2f}\n"
            f"DA: {self.da:.2f}\n"
            f"HRA: {self.hra:.2f}\n"
            f"Total Salary: {self.salary():.2f}"
        )

    def __del__(self):
        Employee.count -= 1


e1 = Employee(101, "Aarav", "IT", 30000, 5000, 3000)
e2 = Employee(102, "Meera", "HR", 25000, 4000, 2500)

print(e1)
print()
print(e2)
print("\nEmployee objects created:", Employee.count)
```

**Sample output:**

```text
Employee No: 101
Name: Aarav
Department: IT
Basic: 30000.00
DA: 5000.00
HRA: 3000.00
Total Salary: 38000.00

Employee No: 102
Name: Meera
Department: HR
Basic: 25000.00
DA: 4000.00
HRA: 2500.00
Total Salary: 31500.00

Employee objects created: 2
```

**Version 2 - Alternative with more reliable counting**

Python does not guarantee when `__del__()` runs, so a counter decreased inside it can become inaccurate. This version uses `weakref.WeakSet` to track live objects. An object is removed from the set automatically once it is garbage-collected.

```python
import weakref


class Employee:
    _instances = weakref.WeakSet()

    def __init__(self, emp_no, name, dept, basic, da, hra):
        if basic < 0 or da < 0 or hra < 0:
            raise ValueError("Salary components cannot be negative.")

        self.emp_no = emp_no
        self.name = name
        self.dept = dept
        self.basic = basic
        self.da = da
        self.hra = hra

        Employee._instances.add(self)

    def salary(self):
        return self.basic + self.da + self.hra

    def __str__(self):
        return (
            f"Employee No: {self.emp_no}\n"
            f"Name: {self.name}\n"
            f"Department: {self.dept}\n"
            f"Total Salary: {self.salary():.2f}"
        )

    @classmethod
    def object_count(cls):
        return len(cls._instances)


e1 = Employee(101, "Aarav", "IT", 30000, 5000, 3000)
e2 = Employee(102, "Meera", "HR", 25000, 4000, 2500)

print(e1)
print()
print(e2)
print("Live Employee objects:", Employee.object_count())
```

**Output (last line):** `Live Employee objects: 2`

**Notes:**

- `self` refers to the current object.
- `Employee.count` is a class attribute shared by all objects.
- `__str__()` gives the readable string form of an object.
- `__del__()` is a finalizer and its timing is not guaranteed.

---

## Practical 13 - Class Point2D

**Problem:** Define a class `Point2D` with coordinates `x` and `y`. Create objects, print their details, and define a method to find the distance between any two points.

Distance = sqrt((x2 - x1)^2 + (y2 - y1)^2)

```python
import math


class Point2D:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    def distance(self, other):
        dx = self.x - other.x
        dy = self.y - other.y
        return math.sqrt(dx**2 + dy**2)


p1 = Point2D(2, 3)
p2 = Point2D(5, 7)

print("Point 1:", p1)
print("Point 2:", p2)
print("Distance:", p1.distance(p2))
```

**Sample output:**

```text
Point 1: (2, 3)
Point 2: (5, 7)
Distance: 5.0
```

**Note:** `distance()` takes another point as an argument, so it works for any two `Point2D` objects.

---

## Practical 14 - Inheritance: Class Point3D

**Problem:** Inherit `Point2D` to create `Point3D` with an extra coordinate `z`. Override the distance method to find the distance between two 3D points.

Distance = sqrt((x2 - x1)^2 + (y2 - y1)^2 + (z2 - z1)^2)

Both classes are in one file since `Point3D` extends `Point2D`.

```python
import math


class Point2D:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    def distance(self, other):
        dx = self.x - other.x
        dy = self.y - other.y
        return math.sqrt(dx**2 + dy**2)


class Point3D(Point2D):
    def __init__(self, x, y, z):
        super().__init__(x, y)
        self.z = z

    def __str__(self):
        return f"({self.x}, {self.y}, {self.z})"

    def distance(self, other):
        dx = self.x - other.x
        dy = self.y - other.y
        dz = self.z - other.z
        return math.sqrt(dx**2 + dy**2 + dz**2)


p1 = Point3D(1, 2, 3)
p2 = Point3D(4, 6, 3)

print("Point 1:", p1)
print("Point 2:", p2)
print("Distance:", p1.distance(p2))
```

**Sample output:**

```text
Point 1: (1, 2, 3)
Point 2: (4, 6, 3)
Distance: 5.0
```

**Notes:**

- `Point3D(Point2D)` sets up the inheritance.
- `super().__init__(x, y)` reuses the parent constructor.
- `distance()` and `__str__()` are overridden to include `z`.

---

## Practical 15 - Exception Handling for a Name

**Problem:** Write a program to accept a name and raise and handle appropriate exceptions if the input contains digits or special characters. Spaces are allowed, so a name like `Shubhi Rai` is valid.

```python
class InvalidNameError(Exception):
    pass


def validate_name(name):
    name = name.strip()

    if not name:
        raise InvalidNameError("Name cannot be empty.")

    if not all(ch.isalpha() or ch.isspace() for ch in name):
        raise InvalidNameError(
            "Name must not contain digits or special characters."
        )

    return name


try:
    name = input("Enter your name: ")
    name = validate_name(name)
    print("Valid name:", name)

except InvalidNameError as error:
    print("Invalid input:", error)
```

**Sample runs:**

```text
Enter your name: Shubhi Rai
Valid name: Shubhi Rai
```

```text
Enter your name: Shubhi123
Invalid input: Name must not contain digits or special characters.
```

```text
Enter your name:
Invalid input: Name cannot be empty.
```

**Notes:**

- `try` holds the code that may raise an exception, `raise` signals the error, and `except` handles it.
- `InvalidNameError` is a user-defined exception that inherits from `Exception`.
- The check accepts only letters and spaces, so names with apostrophes or hyphens are rejected.

---

## Topics covered

- Conditions and loops (`if`, `for`, `while`)
- Functions
- Strings (slicing, `count()`, `replace()`, `find()`)
- Lists and list comprehension
- File handling and `try`/`except`
- Dictionaries and dictionary comprehension
- Tuples
- Classes, constructors, and object counting
- Inheritance and method overriding
- User-defined exceptions

---

Shubhi Rai, B.Sc. (Hons.) Computer Science, Semester I, Roll No. 26570059
