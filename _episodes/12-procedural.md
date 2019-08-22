---
title: "Procedural Programming"
teaching: 40
exercises: 30
questions:
- "What is procedural programming?"
- "How do I define new functions?"
- "When should I use the Procedural paradigm?"
objectives:
- "Use functions to abstract details"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## The Procedural Paradigm

So far we've been writing our code as one continuous piece.
If we want to reuse some of our code, we can use loops to repeat some task, but sometimes we need to reuse code in a different location.

It would also be useful to be able to hide some of the complexity of our code once it's grown to the point where it no longer fits on a single screen.

Procedural Programming is based around the idea that code should be structured into a set of procedures.
Each procedure (optionally) takes some input, performs some computation and (optionally) returns some output.
A program can then use these procedures to perform computation, without having to be concerned with exactly how the computation is performed.

You may wish to think of the Procedural Paradigm as focussing on the **verbs** of a computation.

## Using Functions
Python has many pre-defined functions built in.
We've already met some of them.

To use, or "call", a function we use the name of the function, followed by brackets containing any **arguments** we wish to provide to the function.
All functions in Python **return** a single value as their result.

> ## Return Values
> Though all functions return a single value in Python, this value may itself be:
> - a collection of values
> - `None` - a special value that is interpreted as though nothing has been returned
{: .callout}

~~~
print(len('Python'))
~~~
{: .language-python}

~~~
6
~~~
{: .output}

## Creating Functions

~~~
def add_one(value):
    return value + 1

print(add_one(1))
~~~
{: .language-python}

~~~
2
~~~
{: .output}

~~~
def say_hello(name='World'):
    return 'Hello, ' + name + '!'

print(say_hello('Python'))
~~~
{: .language-python}

~~~
Hello, Python!
~~~
{: .output}

> ## Combining Strings
>
> "Adding" two strings produces their concatenation: `'a'` + `'b'` is `'ab'`.
> Write a short function called `fence` that takes two parameters called original and wrapper and returns a new string that has the wrapper character at the beginning and end of the original.
> A call to your function should look like this:
>
> ~~~
> print(fence('name', '*'))
> ~~~
> {: .language-python}
>
> ~~~
> *name*
> ~~~
> {: .output}
>
> > ## Solution
> >
> > ~~~
> > def fence(original, wrapper):
> >     return wrapper + original + wrapper
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## How do function parameters work?
>
> It’s important to note that even though variables defined inside a function may use the same name as variables defined outside, they don’t refer to the same thing.
> This is because of variable **scoping**.
>
> Within a function, any variables that are created (such as parameters or other variables), only exist within the **scope** of the function.
>
> For example, what would be the output from the following:
>
> ~~~
> f = 0
> k = 0
>
> def multiply_by_10(f):
>     k = f * 10
>     return k
>
> multiply_by_10(2)
> multiply_by_10(8)
>
> print(k)
> ~~~
> {: .language-python}
>
> 1. 20
> 2. 80
> 3. 0
>
> > ## Solution
> > 3 - the f and k variables defined and used within the function do not interfere with those defined outside of the function.
> >
> > This is really useful, since it means we don’t have to worry about conflicts with variable names that are defined outside of our function that may cause it to behave incorrectly.
> > This is known as variable scoping.
> {: .solution}
{: .challenge}

## Managing Academics

As a common example to illustrate each of the paradigms, we'll write some code to help manage a group of academics.

First, let's create a data structure to keep track of the papers that a group of academics are publishing.

~~~
academics = [
    {
        'name': 'Alice',
        'papers': [
            'My science paper',
            'My other science paper'
        ]
    },
    {
        'name': 'Bob',
        'papers': [
            'Bob writes about science'
        ]
    }
]
~~~
{: .language-python}

~~~
def count_papers(academics):
    count = 0

    for academic in academics:
        count = count + len(academic['papers'])

    return count

total = count_papers(academics)
print(total)
~~~
{: .language-python}

~~~
3
~~~
{: .output}

## Composing Functions
~~~
def list_papers(academics):
    papers = []

    for academic in academics:
        papers = papers + academic['papers']

    return papers
~~~
{: .language-python}

{% include links.md %}

