---
title: "Introduction to using Python"
teaching: 30
exercises: 0
questions:
- "What is Python?"
- "How do I use the Python interpreter?"
- "How do I use variables?"
objectives:
- "Explain the benefits of Python."
- "Assign values to variables."
- "Use properties and methods on variable 'objects'."
- "Convert Python variables to other variable types."
keypoints:
- "Python is an interpreted, dynamically typed language."
- "Run the interpreter from the command line by typing `python`."
- "Use `variable = value` to assign a value to a variable in order to record it in memory."
- "Variables are created on demand whenever a value is assigned to them."
- "Use `print(something)` to display the value of `something`."
- "`None` as an empty variable value has its own type."
- "Convert a variable to another types by using `new_type_name(variable)`."
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

First, we need to make sure Anaconda's version of Python will be loaded. Start a terminal and use an editor to look at the `/home/ubuntu/.bashrc` file (replacing `ubuntu` with your home directory, and add the following lines:

~~~
export PATH=/usr/local/anaconda3/bin:/usr/local/pycharm-community-2019.2.3:$PATH
~~~
{: .language-bash}

Every new terminal shell you open should now be able to run the correct version of Python. For the shell you currently have open, type the following to load these changes:

~~~
source /home/ubuntu/.bashrc
python
~~~
{: .language-bash}

We next need to download the training materials from the GitHub code repository online. Go to `https://github.com/sabs-r3/module01_se_day1` and select the green `Clone or download` button, and then select `Download ZIP`. This will download all the files within a single archive file. After it's finished downloading, we need to extract all files from the archive. Start a terminal, and assuming the file has downloaded to e.g. `/home/user/Downloads`, do the following within the shell:

~~~
cd /home/user/Downloads
unzip module01_se_day1-gh-pages.zip
~~~
{: .language-bash}

This will unpack the archive in the `Downloads` directory within a directory called `module01_se_day1-gh-pages`. Change to the `code` directory within that new directory:

~~~
cd module01_se_day1-gh-pages/code
~~~
{: .language-bash}

Then start the Python interpreter from the shell with:

~~~
python
~~~
{: .language-bash}

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

Note that in terms of naming variables, Python's variables must begin with a letter.

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

So we can now develop a better understanding of our labels and boxes: each box is a piece of space (an address) in computer memory. Each label (variable) is a reference to such a place.

When the number of labels on a box ("variables referencing an address") gets down to zero, then the data in the box cannot be found any more.

After a while, the language's "Garbage collector" will wander by, notice a box with no labels, and throw the data away, making that box available for more data.

Older languages like C and Fortran don't have Garbage collectors. So a memory address with no references to it still takes up memory, and the computer can more easily run out.

So when I write:

~~~
number = 1
number = 2
~~~
{: .language-python}

The following things happen:

1. A new integer object '2' is created, and an address in memory is found for it.
1. The variable "number" is moved to refer to that address.
1. The old address, containing '1', now has no labels.
1. The garbage collector frees the memory at the old address.


## Objects and Types

An object, like name, has a type. We can use `type()` to tell us the type of the variable. For our variable above:

~~~
type(number)
~~~
{: .language-python}

Note we don't need to use `print` - the Python interpreter will just output the result:

~~~
<class 'int'>
~~~
{: .output}

Depending on its type, an object can have different properties: data fields *inside* the object.

Consider a Python complex number for example:

~~~
z = 3+1j
~~~
{: .language-python}

We can see what properties and methods an object has available using the dir function:

~~~
dir(z)
~~~
{: .language-python}

~~~
['__abs__',
 '__add__',
 '__bool__',
 '__class__',
 '__delattr__',
 '__dir__',
 '__divmod__',
 '__doc__',
 '__eq__',
 '__float__',
 '__floordiv__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getnewargs__',
 '__gt__',
 '__hash__',
 '__init__',
 '__int__',
 '__le__',
 '__lt__',
 '__mod__',
 '__mul__',
 '__ne__',
 '__neg__',
 '__new__',
 '__pos__',
 '__pow__',
 '__radd__',
 '__rdivmod__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__rfloordiv__',
 '__rmod__',
 '__rmul__',
 '__rpow__',
 '__rsub__',
 '__rtruediv__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__sub__',
 '__subclasshook__',
 '__truediv__',
 'conjugate',
 'imag',
 'real']
~~~
{: .output}

You can see that there are several methods whose name starts and ends with `__` (e.g. `__init__`): these are special methods that Python uses internally, and we will discuss some of them later on in this course. The others (in this case, conjugate, `img` and `real`) are the methods and fields through which we can interact with this object.

~~~
type(z)
~~~
{: .language-python}

~~~
<class 'complex'>
~~~
{: .output}

~~~
z.real
~~~
{: .language-python}

~~~
3.0
~~~
{: .output}

~~~
z.imag
~~~
{: .language-python}

~~~
1.0
~~~
{: .output}

A property of an object is accessed with a dot. The jargon is that the "dot operator" is used to obtain a property of an object.


## Other Basic Python Data Types

Since we're not declaring the type of a variable, how does it work it out?

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

Here we use the `+` operator to concatenate strings together.

~~~
"Joe Frederick 'Bloggs'"
~~~
{: .output}

With quotes, the main thing is to be consistent in how you use them (i.e. not like we've used them above!).

We've looked at properties on objects. But many objects can also have *methods* (types of functions) associated with them, which we can use to perform operations on the object.

For strings, we also can do things like:

~~~
given.upper()
~~~
{: .language-python}

Which returns the upper case version of the string.

~~~
'JOE'
~~~
{: .output}

Note it isn't changing the object

~~~
'    Hello'.strip()
~~~
{: .language-python}

~~~
'Hello'
~~~
{: .output}

We'll be looking at classes and objects in more detail later today.

### Booleans

We can use boolean variables to capture `True` or `False`, useful in conditionals and loops, e.g.:

~~~
is_joe = (given == 'Joe')
flag = False
print(is_joe, flag)
~~~
{: .language-python}

~~~
True False
~~~
{: .output}

### No Value?

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

`None` is the special Python value for a no-value variable.

If that's the output, what's the type of `nothing`?

~~~
type(nothing)
~~~
{: .language-python}

~~~
<class 'NoneType'>
~~~
{: .output}

Python also supports complex (imaginary) numbers, if you're interested.

### Converting Between Types

With floats, ints and strings, we can use in-built functions to convert between types:

~~~
age, house_number = 30, '76'
print(str(age), float(age), int(house_number), float(house_number))
~~~
{: .language-python}

~~~
30 30.0 76 76.0
~~~
{: .output}

{% include links.md %}

