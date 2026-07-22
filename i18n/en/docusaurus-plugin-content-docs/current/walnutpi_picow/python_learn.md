---
sidebar_position: 3
---

# Python3 Basics

::::tip Note

This chapter is for reference only. If you already have MicroPython or Python basics, feel free to skip it.

::::

Since Python is the foundation of learning MicroPython, and to accommodate those without Python experience, we have been thinking about what kind of tutorial to provide. There are plenty of Python books and learning materials available online, so here we have compiled a classic Python3 quick learning reference — you can even use it as a Python dictionary!

\[10-Minute Quick Introduction to Python3, Original by Louie Dinh, Translated by Geoff Liu\]
```python
# Single-line comments start with a hash character

""" Multi-line strings are wrapped with three quotation marks,
    and are often used as multi-
    line comments
"""
```
## Primitive Data Types and Operators

```python
####################################################
## 1. Primitive Data Types and Operators
####################################################

# Integers
3  # => 3

# Arithmetic works as expected
1 + 1  # => 2
8 - 1  # => 7
10 * 2  # => 20

# Division automatically converts to float
35 / 5  # => 7.0
5 / 3  # => 1.6666666666666667

# Integer division floors the result
5 // 3     # => 1
5.0 // 3.0 # => 1.0 # works with floats too
-5 // 3  # => -2
-5.0 // 3.0 # => -2.0

# Float operations produce float results
3 * 2.0 # => 6.0

# Modulo
7 % 3 # => 1

# x to the power of y
2**4 # => 16

# Use parentheses to control precedence
(1 + 3) * 2  # => 8

# Boolean values
True
False

# Negate with 'not'
not True  # => False
not False  # => True

# Logical operators, note that 'and' and 'or' are lowercase
True and False # => False
False or True # => True

# Integers can be used as booleans
0 and 2 # => 0
-5 or 0 # => -5
0 == False # => True
2 == True # => False
1 == True # => True

# Equality with ==
1 == 1  # => True
2 == 1  # => False

# Inequality with !=
1 != 1  # => False
2 != 1  # => True

# Comparison
1 < 10  # => True
1 > 10  # => False
2 <= 2  # => True
2 >= 2  # => True

# Comparisons can be chained!
1 < 2 < 3  # => True
2 < 3 < 2  # => False

# Strings can use single or double quotes
"This is a string"
'This is also a string'

# Concatenate strings with plus
"Hello " + "world!"  # => "Hello world!"

# A string can be treated as a list of characters
"This is a string"[0]  # => 'T'

# Use .format to format strings
"{} can be {}".format("strings", "interpolated")

# You can repeat arguments to save time
"{0} be nimble, {0} be quick, {0} jump over the {1}".format("Jack", "candle stick")
# => "Jack be nimble, Jack be quick, Jack jump over the candle stick"

# If you don't want to count arguments, use keywords
"{name} wants to eat {food}".format(name="Bob", food="lasagna")
# => "Bob wants to eat lasagna"

# If your Python3 program also needs to run in Python 2.5 or below, you can use the old-style formatting
"%s can be %s the %s way" % ("strings", "interpolated", "old")

# None is an object
None  # => None

# When comparing with None, don't use ==, use 'is'. 'is' compares whether two variables point to the same object.
"etc" is None  # => False
None is None  # => True

# None, 0, empty string, empty list, empty dict all evaluate to False
# All other values are True
bool(0)  # => False
bool("")  # => False
bool([]) # => False
bool({}) # => False
```

## Variables and Collections

```python

####################################################
## 2. Variables and Collections
####################################################

# print is the built-in print function
print("I'm Python. Nice to meet you!")

# No need to declare variables before assignment
# Traditional variable naming is lowercase, with underscores separating words
some_var = 5
some_var  # => 5

# Accessing an unassigned variable raises an exception
# See the flow control section to learn about exception handling
some_unknown_var  # Raises NameError

# Use list to store sequences
li = []
# You can also assign elements when creating a list
other_li = [4, 5, 6]

# Use append to add an element to the end of the list
li.append(1)    # li is now [1]
li.append(2)    # li is now [1, 2]
li.append(4)    # li is now [1, 2, 4]
li.append(3)    # li is now [1, 2, 4, 3]
# Use pop to remove from the end of the list
li.pop()        # => 3 and li is now [1, 2, 4]
# Put 3 back
li.append(3)    # li is back to [1, 2, 4, 3]

# List access is like an array
li[0]  # => 1
# Get the last element
li[-1]  # => 3

# Out-of-bounds access causes IndexError
li[4]  # Raises IndexError

# Lists have slicing syntax
li[1:3]  # => [2, 4]
# Take the tail
li[2:]  # => [4, 3]
# Take the head
li[:3]  # => [1, 2, 4]
# Take every other element
li[::2]   # =>[1, 4]
# Reverse the list
li[::-1]   # => [3, 4, 2, 1]
# Any combination of the three arguments can be used for slicing
# li[start:end:step]

# Use del to delete any element
del li[2]   # li is now [1, 2, 3]

# Lists can be added together
# Note: li and other_li remain unchanged
li + other_li   # => [1, 2, 3, 4, 5, 6]

# Use extend to concatenate lists
li.extend(other_li)   # li is now [1, 2, 3, 4, 5, 6]

# Use 'in' to test if a list contains a value
1 in li   # => True

# Use len to get the length of a list
len(li)   # => 6


# Tuples are immutable sequences
tup = (1, 2, 3)
tup[0]   # => 1
tup[0] = 3  # Raises TypeError

# Most list operations also work on tuples
len(tup)   # => 3
tup + (4, 5, 6)   # => (1, 2, 3, 4, 5, 6)
tup[:2]   # => (1, 2)
2 in tup   # => True

# You can unpack tuples (or lists) into variables
a, b, c = (1, 2, 3)     # now a is 1, b is 2, c is 3
# Parentheses around tuples can be omitted
d, e, f = 4, 5, 6
# Swapping two variables is this easy
e, d = d, e     # now d is 5, e is 4


# Use dict to represent mappings
empty_dict = {}
# Initialize a dictionary
filled_dict = {"one": 1, "two": 2, "three": 3}

# Access values with []
filled_dict["one"]   # => 1


# Use keys to get all keys.
# Since keys returns an iterable, wrap it in list here. We'll cover iterables in detail later.
# Note: dictionary key order is not guaranteed, your results may differ.
list(filled_dict.keys())   # => ["three", "two", "one"]


# Use values to get all values. Like keys, wrap in list; order may also differ.
list(filled_dict.values())   # => [3, 2, 1]


# Use 'in' to test if a dictionary contains a key
"one" in filled_dict   # => True
1 in filled_dict   # => False

# Accessing a non-existent key causes KeyError
filled_dict["four"]   # KeyError

# Use get to avoid KeyError
filled_dict.get("one")   # => 1
filled_dict.get("four")   # => None
# get can return a default value when the key doesn't exist
filled_dict.get("one", 4)   # => 1
filled_dict.get("four", 4)   # => 4

# setdefault inserts a value only when the key doesn't exist
filled_dict.setdefault("five", 5)  # filled_dict["five"] is set to 5
filled_dict.setdefault("five", 6)  # filled_dict["five"] is still 5

# Dictionary assignment
filled_dict.update({"four":4}) # => {"one": 1, "two": 2, "three": 3, "four": 4}
filled_dict["four"] = 4  # Another way to assign

# Use del to delete
del filled_dict["one"]  # Remove 'one' from filled_dict


# Use set to represent sets
empty_set = set()
# Initialize a set, syntax is similar to dictionaries.
some_set = {1, 1, 2, 2, 3, 4}   # some_set is now {1, 2, 3, 4}

# You can assign a set to a variable
filled_set = some_set

# Add elements to a set
filled_set.add(5)   # filled_set is now {1, 2, 3, 4, 5}

# & for intersection
other_set = {3, 4, 5, 6}
filled_set & other_set   # => {3, 4, 5}

# | for union
filled_set | other_set   # => {1, 2, 3, 4, 5, 6}

# - for difference
{1, 2, 3, 4} - {2, 3, 5}   # => {1, 4}

# 'in' tests if a set contains an element
2 in filled_set   # => True
10 in filled_set   # => False

```

## Flow Control and Iterators
```python
####################################################
## 3. Flow Control and Iterators
####################################################

# Let's define a variable
some_var = 5

# This is an if statement. Note that indentation is significant in Python.
# Prints "some_var is smaller than 10"
if some_var > 10:
    print("some_var is greater than 10")
elif some_var < 10:    # elif clause is optional
    print("some_var is smaller than 10")
else:                  # else is also optional
    print("some_var is exactly 10")


"""
Use for loops to iterate over lists
Prints:
    dog is a mammal
    cat is a mammal
    mouse is a mammal
"""
for animal in ["dog", "cat", "mouse"]:
    print("{} is a mammal".format(animal))

"""
"range(number)" returns a list of numbers from 0 to the given number
Prints:
    0
    1
    2
    3
"""
for i in range(4):
    print(i)

"""
while loop runs until the condition is no longer satisfied
Prints:
    0
    1
    2
    3
"""
x = 0
while x < 4:
    print(x)
    x += 1  # Shorthand for x = x + 1

# Handle exceptions with try/except blocks
try:
    # Raise an exception with raise
    raise IndexError("This is an index error")
except IndexError as e:
    pass    # pass is a no-op, but you should handle the error here
except (TypeError, NameError):
    pass    # You can handle different types of errors at once
else:   # else clause is optional, must come after all excepts
    print("All good!")   # Only runs if the try block completes without errors


# Python provides a basic abstraction called iterable. An iterable is an object that can be
# treated as a sequence. For example, the object returned by range is iterable.

filled_dict = {"one": 1, "two": 2, "three": 3}
our_iterable = filled_dict.keys()
print(our_iterable) # => dict_keys(['one', 'two', 'three']), an object implementing the iterable interface

# Iterables can be looped over
for i in our_iterable:
    print(i)    # Prints one, two, three

# But cannot be randomly accessed
our_iterable[1]  # Raises TypeError

# Iterables know how to create iterators
our_iterator = iter(our_iterable)

# An iterator is an object that remembers its position during traversal
# Use __next__ to get the next element
our_iterator.__next__()  # => "one"

# Calling __next__ again remembers the position
our_iterator.__next__()  # => "two"
our_iterator.__next__()  # => "three"

# When all elements in the iterator are exhausted, StopIteration is raised
our_iterator.__next__() # Raises StopIteration

# Use list to get all elements from an iterator at once
list(filled_dict.keys())  # => Returns ["one", "two", "three"]
```

## Functions
```python

####################################################
## 4. Functions
####################################################

# Define new functions with def
def add(x, y):
    print("x is {} and y is {}".format(x, y))
    return x + y    # Return a value with the return statement

# Call a function
add(5, 6)   # => Prints "x is 5 and y is 6" and returns 11

# You can also call functions with keyword arguments
add(y=6, x=5)   # Keyword arguments can be in any order


# We can define a variadic function
def varargs(*args):
    return args

varargs(1, 2, 3)   # => (1, 2, 3)


# We can also define a keyword variadic function
def keyword_args(**kwargs):
    return kwargs

# Let's see the result:
keyword_args(big="foot", loch="ness")   # => {"big": "foot", "loch": "ness"}


# These two variadic types can be mixed
def all_the_args(*args, **kwargs):
    print(args)
    print(kwargs)
"""
all_the_args(1, 2, a=3, b=4) prints:
    (1, 2)
    {"a": 3, "b": 4}
"""

# When calling variadic functions, you can do the opposite — use * to unpack sequences and ** to unpack dictionaries.
args = (1, 2, 3, 4)
kwargs = {"a": 3, "b": 4}
all_the_args(*args)   # Equivalent to foo(1, 2, 3, 4)
all_the_args(**kwargs)   # Equivalent to foo(a=3, b=4)
all_the_args(*args, **kwargs)   # Equivalent to foo(1, 2, 3, 4, a=3, b=4)


# Function scope
x = 5

def setX(num):
    # Local scope x is different from global x
    x = num # => 43
    print (x) # => 43

def setGlobalX(num):
    global x
    print (x) # => 5
    x = num # Now the global x is assigned
    print (x) # => 6

setX(43)
setGlobalX(6)

# Functions are first-class citizens in Python
def create_adder(x):
    def adder(y):
        return x + y
    return adder

add_10 = create_adder(10)
add_10(3)   # => 13

# There are also anonymous functions
(lambda x: x > 2)(3)   # => True

# Built-in higher-order functions
map(add_10, [1, 2, 3])   # => [11, 12, 13]
filter(lambda x: x > 5, [3, 4, 5, 6, 7])   # => [6, 7]

# List comprehensions can simplify mapping and filtering. The return value is another list.
[add_10(i) for i in [1, 2, 3]]  # => [11, 12, 13]
[x for x in [3, 4, 5, 6, 7] if x > 5]   # => [6, 7]

```

## Classes
```python

####################################################
## 5. Classes
####################################################


# Define a class that inherits from object
class Human(object):

    # Class attribute, shared by all instances of this class.
    species = "H. sapiens"

    # Constructor, called when an instance is initialized. Note the double underscores before and after
    # the name — this indicates that the attribute or method has special meaning to Python but
    # can still be user-defined. You should avoid this naming convention in your own code.
    def __init__(self, name):
        # Assign the argument to the instance's name attribute
        self.name = name

    # Instance method, the first parameter is always self, which is this instance object
    def say(self, msg):
        return "{name}: {message}".format(name=self.name, message=msg)

    # Class method, shared by all instances of this class. The first parameter is the class object.
    @classmethod
    def get_species(cls):
        return cls.species

    # Static method. Called without binding to an instance or class.
    @staticmethod
    def grunt():
        return "*grunt*"


# Construct an instance
i = Human(name="Ian")
print(i.say("hi"))     # Prints "Ian: hi"

j = Human("Joel")
print(j.say("hello"))  # Prints "Joel: hello"

# Call a class method
i.get_species()   # => "H. sapiens"

# Modify a shared class attribute
Human.species = "H. neanderthalensis"
i.get_species()   # => "H. neanderthalensis"
j.get_species()   # => "H. neanderthalensis"

# Call a static method
Human.grunt()   # => "*grunt*"
```

## Modules
```python

####################################################
## 6. Modules
####################################################

# Import modules with import
import math
print(math.sqrt(16))  # => 4.0

# You can also import individual values from a module
from math import ceil, floor
print(ceil(3.7))  # => 4.0
print(floor(3.7))   # => 3.0

# You can import all values from a module
# Warning: this is not recommended
from math import *

# Shorten module names like this
import math as m
math.sqrt(16) == m.sqrt(16)   # => True

# Python modules are just regular Python files. You can write your own and import them.
# The module name is the file name.

# You can list all values in a module like this
import math
dir(math)
```

## Advanced Usage

```python

####################################################
## 7. Advanced Usage
####################################################

# Use generators to conveniently write lazy evaluation
def double_numbers(iterable):
    for i in iterable:
        yield i + i

# Generators only compute the next value when needed. They generate one value per iteration
# instead of computing all values at once.
#
# The return value of range is also a generator; otherwise a list from 1 to 900,000,000 would
# take a lot of time and memory.
#
# If you want to use a Python keyword as a variable name, add an underscore to differentiate.
range_ = range(1, 900000000)
# Stops when a result >= 30 is found
# This means `double_numbers` will not generate numbers greater than 30.
for i in double_numbers(range_):
    print(i)
    if i >= 30:
        break


# Decorators
# In this example, beg decorates say.
# beg calls say first. If the returned say_please is true, beg modifies the returned string.
from functools import wraps


def beg(target_function):
    @wraps(target_function)
    def wrapper(*args, **kwargs):
        msg, say_please = target_function(*args, **kwargs)
        if say_please:
            return "{} {}".format(msg, "Please! I am poor :(")
        return msg

    return wrapper


@beg
def say(say_please=False):
    msg = "Can you buy me a beer?"
    return msg, say_please


print(say())  # Can you buy me a beer?
print(say(say_please=True))  # Can you buy me a beer? Please! I am poor :(

```
