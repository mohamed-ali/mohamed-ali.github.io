---
layout: post
title:  "Useful python tips"
author: mohamed-ali
image: assets/images/16.jpg
categories: [ scientific-conference, machine-learning, deep-learning ]
featured: true
hidden: true
---

#### What is cls variable in Python?
It's a styling choice, used for class methods.

> Function and Method Arguments
Always use self for the first argument to instance methods.
Always use cls for the first argument to class methods.

Relevant SO discussion: <a href="https://stackoverflow.com/questions/4613000/what-is-the-cls-variable-used-for-in-python-classes">What is the 'cls' variable used for in Python classes?</a>
<hr>
#### Reversing a list or a string in Python:

Python provides several built-in elegant ways to reverse lists or strings (lists of characters):

```python
l = list(range(10))
# l = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
# 1. First method to reverse a list
# ------------------------------
reversed(l)
# Gives an iterator over the reversed list: <listreverseiterator at 0x10c5d4c10>
# To get the it the reversed list, do the following:
list(reversed(l))
# [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
# You can always iterate through the reversed list using a for loop
# for i in reversed(l):
#   # do something. 
# 2. Second method to reverse a list
# ------------------------------
l[::-1]
# Returns the reversed list
# [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
# 3. Reversing a string:
# ----------------------
# A string is considered as a list of characters. So it can be reversed
# in the same way we reverse a list
# st = "Hello World!
st[::-1]
# Result -> '!dlroW olleH'
reversed(st)
# Result -> <reversed at 0x10c618890>
list(reversed(st))
# Result -> ['!', 'd', 'l', 'r', 'o', 'W', ' ', 'o', 'l', 'l', 'e', 'H']
# Notice how reversed returns a list of characters! which you can join
# back to a string using "".join(reversed(st))
```
Let's check the relative performance of these two methods:
```bash
$ python -m timeit 'range(100)[::-1]'
1000000 loops, best of 3: 1.25 usec per loop
$ python -m timeit 'range(100)[::-1]'
1000000 loops, best of 3: 1.19 usec per loop
$ python -m timeit 'reversed(range(100))'
1000000 loops, best of 3: 0.905 usec per loop
$ python -m timeit 'reversed(range(1000))'
100000 loops, best of 3: 6.81 usec per loop
$ python -m timeit 'range(1000)[::-1]'
100000 loops, best of 3: 9.34 usec per loop
```
We can see that there is a small variation between benchmarks, but in all experiments `reversed` seem to be faster.
