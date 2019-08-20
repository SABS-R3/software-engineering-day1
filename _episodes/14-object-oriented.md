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

## Creating Classes

~~~
class Academic:
    def __init__(self, name):
        self.name = name
~~~
{: .source}

### Special Methods

Dunder methods

~~~
class Academic:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name
~~~
{: .source}

## Composition

## Inheritance
{% comment %}Briefly mention multiple inheritance{% endcomment %}

{% include links.md %}

