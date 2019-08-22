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

Since all of the data representing a single **object**

You may wish to think of the Object Oriented Paradigm as focussing on the **nouns** of a computation.

## Creating Classes

~~~
class Academic:
    def __init__(self, name):
        self.name = name
~~~
{: .language-python}

### Special Methods

Dunder methods

~~~
class Academic:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name
~~~
{: .language-python}

## Composition

## Inheritance
{% comment %}Briefly mention multiple inheritance, the "deadly diamond of death" and how Python copes with it (C3 Linearisation){% endcomment %}

## Comparison of Composition and Inheritance
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

