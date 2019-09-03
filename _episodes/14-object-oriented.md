---
title: "Object Oriented Programming"
teaching: 40
exercises: 30
questions:
- "What is encapsulation?"
- "What is a class?"
- "What is an object?"
- "When should I use the Object Oriented paradigm?"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## The Object Oriented Paradigm

The Object Oriented Paradigm is based upon the Procedural Paradigm and is thus more recent than most of the other major paradigms.

In this paradigm, we shift our focus from the process of computation, to the data with which the computation is being performed.
The overarching idea here, is that data should be structured such that all data related to the same **object** should be stored together.
This is easiest to understand when thinking about the data representing a real-world, physical object, but is also applicable to more abstract concepts.

Since all of the data representing a single **object** is now stored together, it makes sense to store the code representing the **behaviour** of that object in the same place.re
So, a class is a template describing the structure of some collection of data, along with the code necessary to describe the behaviour of that data.

You may wish to think of the Object Oriented Paradigm as focussing on the **nouns** of a computation.

## Using Classes

Just like functions, we've already been using some of the classes built into Python.

~~~
my_list = [1, 2, 3]
my_dict = {1: '1', 2: '2', 3: '3'}
my_set = {1, 2, 3}

print(type(my_list))
print(type(my_dict))
print(type(my_set))
~~~
{: .language-python}

~~~
<class 'list'>
<class 'dict'>
<class 'set'>
~~~
{: .output}

Lists, dictionaries and sets are a slightly special type of class, but they behave in much the same way as a class we might define ourselves.
They each contain data, as we have seen before.
They also provide a set of functions, or **methods** which describe the **behaviours** of the data.

The behaviours we have seen previously include:
- Lists can be appended to
- Lists can be indexed (we'll get to this later)
- Lists can be sliced (we won't get to this)
- The union of two sets can be found
- The intersection of two sets can be found

## Creating Classes

~~~
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

alice = Academic('Alice')
~~~
{: .language-python}

> ## Data Classes
> Added in Python 3.7 to automatically generate some of the class structure.
> Intended for classes where the data is more important than the behaviour, but are otherwise completely normal classes.
>
> ~~~
> @dataclass
> class Academic:
>     name: str
>     papers: List[Dict] = field(default_factory=list)
>
> alice = Academic('Alice')
> ~~~
> {: .language-python}
{: .callout}

### Methods

~~~
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

    def write_paper(title, day):
        new_paper = {
            'title': title,
            'day': day
        }

        self.papers.append(new_paper)
        return new_paper

alice = Academic('Alice')
paper = alice.write_paper('A new paper', 3)

print(paper)
~~~
{: .language-python}

~~~
{'title': 'A new paper', 'day': 3}
~~~
{: .output}

### Dunder Methods

~~~
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

    def __str__(self):
        return self.name

alice = Academic('Alice')
print(alice)
~~~
{: .language-python}

~~~
Alice
~~~
{: .output}

## Relationships

We now have a language construct for grouping data and behaviour related to a single conceptual object.
The next step is talking about the relationships between objects.

There are two types of relationships between objects which are useful to be able to describe:
1. Ownership - x **has a** y - **composition**
2. Identity - x **is a** y - **inheritance**

### Composition

Composition is about ownership of an object or resource - x **has a** y.

In the case of our academics example, we can say that academics have papers.

~~~
class Paper:
    def __init__(self, title, pub_day):
        self.title = title
        self.pub_day = pub_day

    def __str__(self):
        return self.title

class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

    def write_paper(title, day):
        new_paper = Paper(title, day)

        self.papers.append(new_paper)
        return new_paper

alice = Academic('Alice')
paper = alice.write_paper('A new paper', 3)

print(paper)
~~~
{: .language-python}

~~~
A new paper
~~~
{: .output}

### Inheritance

Inheritance is about behaviour shared by classes, because they have some shared identity.

For instance

~~~
class Person:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name

class Academic(Person):
    def __init__(self, name):
        super().__init__(name)
        self.papers = []

    def write_paper(title, day):
        new_paper = Paper(title, day)

        self.papers.append(new_paper)
        return new_paper

alice = Acadmic('Alice')
print(alice)

bob = Person('Bob')
print(bob)

paper = alice.write_paper('A paper', 0)
print(paper)

paper = bob.write_paper('A different paper', 0)
print(paper)
~~~
{: .language-python}

~~~
Alice
Bob
A paper
AttributeError
~~~
{: .output}

{% comment %}Briefly mention multiple inheritance, the "deadly diamond of death" and how Python copes with it (C3 Linearisation){% endcomment %}

### Composition vs Inheritance
~~~
class Machine:
    pass

class Printer(Machine):
    pass

class Scanner(Machine):
    pass

class Copier(Printer, Scanner):
    # Copier `is a` Printer and `is a` Scanner
    pass
~~~
{: .language-python}

~~~
class Machine:
    pass

class Printer(Machine):
    pass

class Scanner(Machine):
    pass

class Copier(Machine):
    def __init__(self):
        # Copier `has a` Printer and `has a` Scanner
        self.printer = Printer()
        self.scanner = Scanner()
~~~
{: .language-python}

{% include links.md %}

