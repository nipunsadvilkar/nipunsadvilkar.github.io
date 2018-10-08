---
layout: post
title:  "Code Walkthrough: Tablib, a Python Module for Tabular Datasets"
date:   2017-10-08 21:00:00
comments: true
categories: blog
description: Reading Great Code and it's benefits. Code walkthrough of tablib python module by Nipun Sadvilkar
---
<hr>

<h1 style="font-size: 30px;">Motivation</h1>

Oftentimes, I like to dive into open source projects to learn best practices and know how programming pundits use to do things correctly and optimally. In addition, [Peter Norvig](https://en.wikipedia.org/wiki/Peter_Norvig) has also said in his famous blog post [Teach Yourself Programming in Ten Years](http://norvig.com/21-days.html)

> *Talk with other programmers; read other programs. This is more important than any book or training course.*

I am big advocate of it. This blog post is to emphasize - how reading open source code helps you identify and understand efficient patterns and coding constructs.

<h1 style="font-size: 30px;">Tablib</h1>

I admire [Kenneth Reitz](https://github.com/kennethreitz) very much. Do read and follow his [The Hitchhiker’s Guide to Python!](https://docs.python-guide.org) to be a a great Python programmer. Lesson from this book - [Reading Great Code](https://docs.python-guide.org/writing/reading/?highlight=tablib#reading-great-code) - is the main reason why I decided to give a go at reading source code of [Tablib](https://github.com/kennethreitz/tablib). Reading source code is initially daunting because of certain constructs which are obscure or you may not be familiar with it, and which is natural. Despite such hurdles, if you keep con oncentrating you will find lot of "Aha!" moments by identifying useful patterns. Here is my experience, I came across a very simple yet useful code snippet which is very important and widely used task in data cleaning i.e., removing duplicates.

[Source code: tablib removing_duplicates menthod:](http://docs.python-tablib.org/en/master/_modules/tablib/core/#Dataset.remove_duplicates)

```python
def remove_duplicates(self):
    """Removes all duplicate rows from the :class:`Dataset` object
    while maintaining the original order."""
    seen = set()
    self._data[:] = [row for row in self._data if not (tuple(row) in seen or seen.add(tuple(row)))]
```

Check the `if ` statement followed by [_generator expression_](https://dbader.org/blog/python-generator-expressions). If you look closely inside generator expression the technique used to check for duplicate rows is called [_short circuit technique_](https://www.geeksforgeeks.org/short-circuiting-techniques-python/) implemented in python.


[Short circuit explained by official docs](https://docs.python.org/2/library/stdtypes.html#boolean-operations-and-or-not):

|Operation|Result|Notes|
|---|---|---|
|`x or y` |if x is false, then y, else x| Only evaluates the second argument(`y`) if the first one is `False`.|
|`x and y`|if x is false, then x, else y| Only evaluates the second argument(`y`) if the first one(`x`) is `True`.|
|`not x`|if x is false, then True, else False|`not` has a lower priority than non-Boolean operators|

<br>
`remove_duplicates` method uses 1st and 3rd Operation from above table.

Key thing to remember is:

**The evaluation of expression takes place from left to right.**

Explained with toy example:
```python
>>> _data = [[1, 2, 3], [4, 5, 6], [1, 2, 3]]
>>> seen = set()
>>> data_deduplicated = [row for row in _data if not (tuple(row) in seen or seen.add(tuple(row)))]

>>> print(data_deduplicated)
# [[1, 2, 3], [4, 5, 6]]
```

To put it into words, within list comprehension - iterate over data row by row and check if given row is present within `seen` _set_. If it's not present, meaning
```python
tuple(row) in seen
```
evaluates to `False` and as per 1st operation from the table, evaluate second argument which is to add given row in `seen` _set_. Furthermore, `if not ()` condition gets satisfied and given row is added to outer list. Subsequently, if the same row occurs then we know it's already in `seen` _set_ and hence that row will not be added to outer list. In overall, resulting into removing of duplicate rows.

If you are more of a visual learning person, following demonstartion using [Python tutor tool](http://pythontutor.com/) built by an outstanding academic and prolific blogger - [Philip Guo](http://pgbovine.net) - would help*:
> *If below IFrame is not visible please enable `load unsecure script` of your browser. Don't worry! it's saying unsecure because of http protocol used by [Python tutor](http://pythontutor.com/) and not *https*.

<iframe width="820" height="650" frameborder="1.5" src="http://pythontutor.com/iframe-embed.html#code=_data%20%3D%20%5B%5B1,2,3%5D,%20%5B4,5,6%5D,%20%5B1,2,3%5D%5D%0Aseen%20%3D%20set%28%29%0Adata_deduplicated%20%3D%20%5Brow%20for%20row%20in%20_data%20if%20not%20%28tuple%28row%29%20in%20seen%20or%20seen.add%28tuple%28row%29%29%29%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=6&heapPrimitives=nevernest&origin=opt-frontend.js&py=2&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

I hope by now you have understood [_short circuit technique_](https://www.geeksforgeeks.org/short-circuiting-techniques-python/) and importance of reading open source code. So keep exploring and do share your experience with me. Thank you! :)
