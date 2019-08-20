---
title: "Introduction to using Python"
teaching: 40
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## Introduction to Python

See topic [slides](../slides/02-python-intro.html).

## Running the Python Interpreter

Normally, you write Python programs in a Python script, which is basically a file of Python commands you can run,
or within a Jupyter notebook, which is an interactive script of Python commands that gives you results of your commands as you enter them.
We'll come on to Notebooks and scripts later. But to start with, we'll take a look at the Python interpreter.
It's similar to the shell in how it works, in that you type in commands and it
gives you results back, but instead you use the Python language.

It's a really quick and convenient way to get started with Python, particularly when learning about things like how to use variables, and it's good for playing around with what you can do and quickly testing small things.
But as you progress to more interesting and complex things you need to move over to writing proper Python scripts, which we'll see later.

You start the Python interpreter from the shell by:

~~~
$ python
~~~
{:.language-bash}

And then you are presented with something like:

~~~
Python 3.4.3 |Anaconda 2.3.0 (x86_64)| (default, Mar  6 2015, 12:07:41) 
[GCC 4.2.1 (Apple Inc. build 5577)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
~~~
{: .output}

And lo and behold! You are presented with yet another prompt.
So, we're actually running a Python interpreter from the shell - it's only yet another program we can run from the shell after all.
But shell commands won't work again until we exit the interpreter.

You can exit the interpreter and get back to the shell by typing:

~~~
>>> exit()
~~~
{: .language-python}

...or alternatively pressing the Control and D keys at the same time.
Then you'll see:

~~~
$
~~~
{: .output}

So now you're back in the shell.


## Variables

Compared to some other languages such as C++ or JavaScript, variables in Python do not need to be declared before assigning something to them, for example:

~~~
six = 2*3
print(six)
~~~
{: .language-python}

~~~
6
~~~
{: .output}

If we look for a variable that hasn't ever been defined, we get an error telling us so:

~~~
print(seven)
~~~
{: .language-python}

~~~
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'seven' is not defined
~~~
{: .output}

You can also assign an arbitrary number of variables on the same line:

~~~
one, two = 1, 2
~~~
{: .language-python}

> ## Sorting out references
>
> What does the following program print out?
>
> ~~~
> first, second = 1, 2
> third, fourth = second, first
> print(third, fourth)
> ~~~
> {: .language-python}
>
> > ## Solution
> > ~~~
> > 2 1
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

Although we commonly refer to `variables` even in Python (because it is the common terminology), we really mean `names` or `identifiers`. In Python, `variables` are name tags for values, not labelled boxes that contain a value.


## Determining a Variable's Type

We can use `type()` to tell us the type of the variable. For our variable above:

~~~
type(six)
~~~
{: .language-python}

Note we don't need to use `print` - the Python interpreter will just output the result:

~~~
<class 'int'>
~~~
{: .output}

So if we're not declaring the type of a variable, how does it work it out?


## Other Python Data Types

Python is an interpreted language that is *dynamically typed*, which means the type of a variable is determined and *bound* to the variable at runtime from its given value. So when we assign a floating point number, for example, it's type is inferred:

### Floats

~~~
weight_kg = 55
weight_lb = 2.2 * weight_kg
print('Weight in kg', weight_lb)
~~~
{: .language-python}

For a float, a number after a point is optional. But the *dot* makes it a float.

~~~
Weight in kg 121.00000000000001
~~~
{: .output}

So the thing with floats is that they are *representation* of a real number. Representing a third or the root of 2 would be impossible for a computer, so these are really approximations of real numbers using an ubiquitous standard (IEEE-754).

As the example above shows, we can print several things at once by separating them with commas.

An important thing to remember, particularly in numerical analyses, is that a `float` in Python is double precision.

> ## What's inside the box?
>
> Draw diagrams showing what variables refer to what values after each statement
> in the following program:
>
> ~~~
> weight = 70.5
> age = 35
> weight = weight * 1.14
> age = age + 20
> ~~~
{: .challenge}


### Strings

Note that before, we also used a `string` in our use of `print`. In Python, we can use either single quotes or double quotes, or even both if we need to include quotes within a string, e.g.:

~~~
given = 'Joe'
middle = "Frederick"
family = "'Bloggs'"
full = given + " " + middle + " " + family
print(full)
~~~
{: .language-python}

~~~
"Joe Frederick 'Bloggs'"
~~~
{: .output}


### Booleans

~~~

~~~
{: .language-python}

### No value?

We can also assign variable with no value:

~~~
nothing = None
print(nothing)
~~~
{: .language-python}

~~~
None
~~~
{: .output}

If that's the output, what's the type of `nothing`?

~~~
type(nothing)
~~~
{: .language-python}

~~~
<class 'NoneType'>
~~~
{: .output}

`None` is the special Python value for a no-value variable.

Python also supports complex (imaginary) numbers, if you're interested.


## Containers

### Lists

One of the most fundamental data structures in any language is the array, used to hold many values at once. Python doesn’t have a native array data structure, but it has the list which is much more general and can be used as a multidimensional array quite easily.

A list in python is just an ordered collection of items which can be of any type. By comparison an array is an ordered collection of items of a single type - so a list is more flexible than an array. We can also add and delete elements from a Python list at any time.

To define a list we simply write a comma separated list of items in square brackets:




### Tuples

### Sets

> ## Mutability
>
> An important thing to remember is that Python variables are simply *references* to values, and also that they fall into two distinct types:
>
> * Immutable types: value changes by referencing a newly created value, e.g. when changing a letter in a string
> * Mutable types: values can be changed 'in place', e.g. changing or adding an item in a list
>
> This matters when you are 'copying' variables or passing them as arguments to functions.
{: .callout}


## Dictionaries

{% include links.md %}

