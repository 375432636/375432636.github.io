---
title: Python Data Structures
date: 2019-09-23 11:37:35
tags: python
---

There is 6 data structures available, The Builtins data structures are: lists, tuples, dictionaries, strings, sets and frozensets.

|--|--|
|Type|Feature|
|--|--|
|lists|可变,可排序,可增减,可包含任意对象|
|tuples|不可变,不可排序,不可增减,可包含任意对象,节省内存|
|sets|mutable,unordered|
|frozensets|immutable,unordered|

## 1. List

### 1.1 Difference between append() and extend()

List have several methodes amongst which the append() and extend() methods. the former appends an object to the end of the list (e.g., another list) while the later appends each element of the iterable object (e.g., another list) to the end of the list.

For example, we can append an object (here the characteer `c`) to the end of a simple list as follows:

```
>>> stack = ['a', 'b']
>>> stack.append('c')
>>> stack
['a', 'b', 'c']
```

However, if we want to append several objects contained in a list, the result as expected (or not...) is:

```
>>> stack.append(['d', 'e', 'f'])
>>> stack
['a', 'b', 'c', ['d', 'e', 'f']]
```


The object ['d', 'e', 'f'] has been appended to the existing list. However, it happens that some times what we want is to append the elements one by one of a given list rather the list itself. You can do that manually of course, but a better solution is to use the extend() method as follows:

```
>>> stack = ['a', 'b', 'c']
>>> stack.extend(['d', 'e', 'f'])
>>> stack
['a', 'b', 'c', 'd', 'e', 'f']
```

### 1.2 Other list methods

#### 1.2.1 index

The index() methods searches for an element in a list. For instance:

```
>>> my_list = ['a', 'b', 'c', 'b', 'a']
>>> my_list.index('b')
1
```

It returns the index of the first and only occurrence of `b`. If you want to specify a range of valid index, you can indicate the start and stop indices:

```
>>> my_list = ['a', 'b', 'c', 'b', 'a']
>>> my_list.index('b',2)
3
```
#### 1.2.2 remove
Similarly, you can remove the first occurrence of an element as follows:

```
>>> my_list.remove('a')
>>> my_list
['b', 'c', 'b', 'a']
```

#### 1.2.3 insert

You can remove element but also insert element wherever you want in a list:

```
>>> my_list.insert(2,'a')
>>> my_list
['b', 'c', 'a', 'b']
```

#### 1.2.4 pop

Or remove the last element of a list by using:

```
>>> my_list.pop()
'a'
>>> my_list
['b', 'c', 'b']
```

which also returns the value that has been removed.

#### 1.2.5 count

You can count the number of element of a kind:

```
>>> my_list.count('b')
2
```

#### 1.2.6 sort
There is a sort() method that performs an in-place sorting:

```
>>> my_list.sort()
>>> my _list
['a', 'b', 'b', 'c']
```

Here, it is quite simple since the elements are all characters. For standard types, the sorting works well. Imagine now that you have some non-standard types. You can overwrite the function used to perform the comparison as the first argument of the sort() method.

There is the possiblity to sort in the reverse order:

```
>>> my_list.sort(reverse=Ture)
>>> my_list
['c','b','b','a']
```

#### 1.2.7 reverse

Finally, you can reverse the element in-place

```
>>> my_list = ['a', 'c', 'b']
>>> my_list.reverse()
>>> my_list
['b', 'c', 'a']
```

### 1.3 Operators

The + operator can be used to *extend* a list:

```
>>> my_list = [1]
>>> my_list =+= [2]
>>> my_list
[1, 2]
>>> my_list += [3, 4]
>>> my_list
[1, 2, 3, 4]
```

The * operator ease the creation of list with similar values

```
>>> my_list = [1, 2]
>>> my_list = my_list * 2
>>> my_list
[1, 2, 1, 2]
```
### 1.4 Slicing[切片]

Slicing uses the symbol: to access to part of a list:

```
>>> list[first index:last index:step]
>>> list[:]
```

```
>>> a = [0, 1, 2, 3, 4, 5]
[0, 1, 2, 3, 4, 5]
>>> a[2:]
[2, 3, 4, 5]
>>> a[:2]
[0, 1]
>>> a[2:-1]
[2, 3, 4]
```

By default the first index is 0, the last index is the last one..., and the step is 1. The step is optional. So the following slicing are equivalent:

```
>>> a = [1, 2, 3, 4, 5, 6, 7, 8]
>>> a[:]
[1, 2, 3, 4, 5, 6, 7, 8]
>>> a[::1]
[1, 2, 3, 4, 5, 6, 7, 8]
>>> a[0::]
[1, 2, 3, 4, 5, 6, 7, 8]
```

### 1.5 List comprehension

Traditionally, a piece of code that loops over a sequence could be written as follows:

```
>>> evens = []
>>> for i in range(10):
...     if i % 2 == 0:
...         evens.append(i)
>>> evens
[0, 2, 4, 6, 8]
```

This may work, but it actually makes things slower for Python because the interpreter works on each loop to determine what part of the sequence has to be changed. 

A *list comprehension* is the correct answer:

```
>>> [i for i in range(10) if i % 2 == 0]
[0, 2, 4, 6, 8]
```

Besides the fact that it is more efficient, it is also shorter and involves fewer elements.

### 1.6 Filtering Lists

```
>>> li = [1, 2]
>>> [elem*2 for elem in li if elem > 1]
[4]
```

### 1.7 Lists as Stacks

The Python documentation gives an example of how to use lists as stacks, that is a last-in, first-out data structures (LIFO).

An item can be added to a list by using the *append()* method. The last item can be removed from the list by using the *pop()* method without passing any index to it. 

```
>>> stack = ['a', 'b', 'c', 'd']
>>> stack.append('e')
>>> stack.append('f')
>>> stack
['a', 'b', 'c', 'd', 'e', 'f']
>>> stack.pop()
'f'
>>> stack
['a', 'b', 'c', 'd', 'e']
```

### 1.8 Lists as Queues

Another usage of list, again presented in Python documentation is to use lists as queues, that is first in - first out (*FIFO*).

```
>>> queue = ['a', 'b', 'c', 'd']
>>> queue.append('e')
>>> queue.append('f')
>>> queue
['a', 'b', 'c', 'd', 'e', 'f']
>> queue.pop(0)
'a'
```

### 1.9 How to copy a list

There are three ways to copy a list:

```
>>> l2 = list(l)
>>> l2 = l[:]
>>> import copy
>>> l2 = copy.copy(l)
```

##### Warning: Don't do l2 = l, which is refrence, not a copy.
'

#### 1.9.1 Inserting items into a sorted list

The bisect module provides tools to manipulate sorted lists.

```
>>> x = [4, 1]
>>> x.sort()
>>> import bisect
>>> bisect.insort(x, 2)
>>> x
[1, 2, 4]
```

To know where the index where the value would have been inserted, you could have use(预测将要数字在里面会处在哪个位置):

```
>>> x = [4, 1]
>>> x.sort()
>>> import bisect
>>> bisect.bisect(x, 2)
2
```


## 2. Tuples

In Python, *tuples* are part of the standard language. This is a data sturcture very similar to the *list* data strue. The main difference being that tuple manipulation are faster than list because tuples are immutable.

### 2.1 Constructing tuples [构造元组]

To create a tuple, place values within breackets:

```
>>> l = (1, 2, 3)
>>> l[0]
1
```

It is also possible to create a tuple without parentheses, by using commas:

```
>>> l = 1, 2
>>> l
(1, 2)
```

If you want to create a tuple with a single element, you must use the comma:

```
>>> singleton = (1, )
```

You can repeat a tuples by multiplying a tuple by a number:

```
>>> (1, ) * 5
(1, 1, 1, 1, 1)
``

Note that you can concatenate tuples 
