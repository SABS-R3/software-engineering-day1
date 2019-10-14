---
title: "Object Oriented Programming"
teaching: 40
exercises: 30
questions:
- "What is the Object Oriented paradigm?"
- "What is an object?"
- "What is encapsulation?"
- "How do I encapsulate data in Python?"
- "When should I use the Object Oriented paradigm?"
objectives:
- "Use classes to encapsulate data and behaviour"
- "Describe behaviour shared by multiple classes using inheritance"
- "Explain the difference between inheritance and composition"
keypoints:
- "Object Oriented progamming uses classes to structure data"
- "Methods are functions which implement the behaviour of an object"
- "Behaviour and data can be shared between classes using composition and inheritance"
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

Classes are one of the fundamental concepts of Object Oriented programming - acting as the template for objects which share common attributes and behaviour.

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

So how do we create and use our own class in Python?

~~~
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

alice = Academic('Alice')
print(alice.name)
~~~
{: .language-python}

~~~
Alice
~~~
{: .output}

Similar to functions, we begin by using a special keyword, in this case `class`, followed by a name, then a colon to begin a new block.
Inside this block, we define the data and behaviour that we want the class to provide.

Almost every class you define will have a `__init__` (pronounced "init" or "dunder-init") **method** which is responsible for initialising any data that the class contains.
Note that this is slightly different from the **constructor** in many other OO languages (it doesn't allocate memory for the class itself), but it's usually safe to treat it as the same.

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
> print(alice.name)
> ~~~
> {: .language-python}
>
> ~~~
> Alice
> ~~~
> {: .output}
{: .callout}

### Methods

To define the behaviour of a class we can add functions which operate on the data the class contains.
We call these functions **member functions** or **methods**.

These functions are the same as normal functions (alternatively known as **free functions**), but we have an extra first parameter `self`.
The `self` parameter is a normal variable, but when we use a method of an object, the value of `self` is automatically set to the object.

~~~
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

    def write_paper(self, title, day):
        new_paper = {
            'title': title,
            'day': day
        }

        self.papers.append(new_paper)
        return new_paper

alice = Academic('Alice')
print(alice)

paper = alice.write_paper('A new paper', 3)
print(paper)
print(alice.papers)

paper = Academic.write_paper(alice, 'Another new paper', 4)
print(paper)
print(alice.papers)
~~~
{: .language-python}

~~~
<__main__.Academic object at 0x7f4826fdff10>
{'title': 'A new paper', 'day': 3}
[{'title': 'A new paper', 'day': 3}]
[{'title': 'A new paper', 'day': 3}, {'title': 'Another new paper', 'day': 4}]
~~~
{: .output}

The second use of `write_paper` in the example above shows that we can use 

### Dunder Methods

Why is the `__init__` method not called `init`?
There are a few special method names that we can use which Python will use to provide a few common behaviours, each of which begins and ends with two underscores, hence the name **dunder method**.

The most commonly seen of the dunder methods is `__init__`, but there are a few other common ones:

~~~
class Academic:
    def __init__(self, name):
        self.name = name
        self.papers = []

    def write_paper(self, title, day):
        new_paper = {
            'title': title,
            'day': day
        }

        self.papers.append(new_paper)
        return new_paper

    def __str__(self):
        return self.name

    def __getitem__(self, index):
        return self.papers[index]

    def __len__(self):
        return len(self.papers)

alice = Academic('Alice')
print(alice)

alice.write_paper('A new paper', 3)
paper = alice[0]
print(paper)

print(len(alice))
~~~
{: .language-python}

~~~
Alice
{'title': 'A new paper', 'day': 3}
1
~~~
{: .output}

In the example above we can see:

- `__str__` - converts an object into its string representation, used when you do `str(object)` or `print(object)`
- `__getitem__` - Accesses an object by key, this is how `list[x]` and `dict[x]` are implemented
- `__len__` - gets the length of an object - usually the number of items it contains

There are many more described in the Python documentation, but it's also worth experimenting with built in Python objects to see which methods provide which behaviour.

> ## A Basic Class
>
> Implement a class to represent a book.
> Your class should:
> 
> - Have a title
> - Have an author
> - When printed, show text in the format "title by author"
>
> ~~~
> book = Book('A Book', 'Me')
>
> print(book)
> ~~~
> {: .language-python}
>
> ~~~
> A Book by Me
> ~~~
> {: .output}
>
> > ## Solution
> > ~~~
> > class Book:
> >     def __init__(self, title, author):
> >         self.title = title
> >         self.author = author
> >     
> >     def __str__(self):
> >         return self.title + ' by ' + self.author
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## Properties

The final special type of method we'll introduce is **properties**.
Properties are methods which behave like data - when we want to access them, we don't need to use brackets to call the method manually:

~~~
class Academic:
    ...

    @property
    def last_paper(self):
        return self.papers[-1]

alice = Academic('Alice')

alice.write_paper('First paper', 1)
alice.write_paper('Second paper', 2)

paper = alice.last_paper
print(paper)
~~~
{: .language-python}

The `@` syntax means that a function called `property` is being used to modify the behavior of the method - this is called a **decorator**.
In this case the `@property` decorator converts `last_paper` from a normal method into a property.

We'll see more about decorators tomorrow.

## Relationships

We now have a language construct for grouping data and behaviour related to a single conceptual object.
The next step is talking about the relationships between objects.

There are two fundamental types of relationship between objects which we need to be able to describe:
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

If we want to extend the previous example to also manage people who aren't academics we can add another class `Person`.
But `Person` will share some behaviour with `Academic` - in this case both have a name and show that name when you print them.

Since we expect all academics to be people (hopefully!), it makes sense to implement the behaviour in `Person` and then reuse it in `Academic`.

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
AttributeError: 'Person' object has no attribute 'write_paper'
~~~
{: .output}

We see in the example above that to say that a class inherits from another, we but the **parent class** (or **superclass**) in brackets after the name of the **subclass**.

There's something else we need to add as well - Python doesn't automatically call the `__init__` method on the parent class, so we need to do this manually within the `__init__` method of the subclass.

Python does however provide us with a shortcut to access the parent class.
The line `super().__init__(name)` gets the parent class, then calls the `__init__` method, providing the `name` variable that `Person.__init__` requires.

#### Multiple Inheritance

Some languages allow you to have a class inherit from multiple parent classes, which is known as **multiple inheritance**.


{% comment %}Briefly mention multiple inheritance, the "deadly diamond of death" and how Python copes with it (C3 Linearisation){% endcomment %}

### Composition vs Inheritance

When deciding how to implement a model of a particular system, you often have a choice of either composition or inheritance, where there is no obviously correct choice.
More on this later in the week!

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

> ## Building a Library
>
> Using what we've seen so far, implement two classes: `Book` (you can use the one from the earlier exercise) and `Library` which have the following behaviour:
>
> ~~~
> library = Library()
> 
> library.add_book('My First Book', 'Alice')
> library.add_book('My Second Book', 'Alice')
> library.add_book('A Different Book', 'Bob')
>
> print(len(library))
>
> book = library[2]
> print(book)
>
> books = library.by_author('Alice')
> for book in books:
>     print(book)
>
> books = library.by_author('Carol')
> ~~~
> {: .language-python}
>
> ~~~
> 3
> A Different Book by Bob
> My First Book by Alice
> My Second Book by Alice
> KeyError: 'Author does not exist'
> ~~~
> {: .output}
>
> > ## Solution
> > ~~~
> > class Book:
> >     def __init__(self, title, author):
> >         self.title = title
> >         self.author = author
> >     
> >     def __str__(self):
> >         return self.title + ' by ' + self.author
> > 
> >     
> > class Library:
> >     def __init__(self):
> >         self.books = []
> >     
> >     def add_book(self, title, author):
> >         self.books.append(Book(title, author))
> >     
> >     def __len__(self):
> >         return len(self.books)
> >     
> >     def __getitem__(self, key):
> >         return self.books[key]
> >     
> >     def by_author(self, author):
> >         matches = []
> >         for book in self.books:
> >             if book.author == author:
> >                 matches.append(book)
> >
> >         if not matches:
> >             raise KeyError('Author does not exist')
> >         
> >         return matches
> > ~~~
> > {: .output}
> {: .solution}
>
> Extend the class so that we can get the list of all authors and titles.
> If an author appears multiple times, they should only appear once in the list of authors:
>
> ~~~
> print(library.titles)
> print(library.authors)
> ~~~
> {: .language-python}
>
> ~~~
> ['My First Book', 'My Second Book', 'A Different Book']
> ['Alice', 'Bob']
> ~~~
> {: .output}
>
> > ## Solution
> > ~~~
> > class Book:
> >     def __init__(self, title, author):
> >         self.title = title
> >         self.author = author
> >     
> >     def __str__(self):
> >         return self.title + ' by ' + self.author
> > 
> >     
> > class Library:
> >     def __init__(self):
> >         self.books = []
> >     
> >     def add_book(self, title, author):
> >         self.books.append(Book(title, author))
> >     
> >     def __len__(self):
> >         return len(self.books)
> >     
> >     def __getitem__(self, key):
> >         return self.books[key]
> >     
> >     def by_author(self, author):
> >         matches = []
> >         for book in self.books:
> >             if book.author == author:
> >                 matches.append(book)
> >
> >         if not matches:
> >             raise KeyError('Author does not exist')
> >         
> >         return matches
> > 
> >     @property
> >     def titles(self):
> >         titles = []
> >         for book in self.books:
> >             titles.append(book.title)
> > 
> >         return titles
> >
> >     @property
> >     def authors(self):
> >         authors = []
> >         for book in self.books:
> >             if book.author not in authors:
> >                 authors.append(book.author)
> > 
> >         return authors
> > ~~~
> > {: .output}
> {: .solution}
>
> The built in `set` class has a `set.union` method which takes two sets (one of which is `self`) and returns a new set containing all of the members of both sets, with no duplicates.
>
> Extend your library model with a `union` method which behaves the same way - it should return a new `Library` containing all the books of the two provided libraries.
>
> To do this you might need to create a `Book.__eq__` method.
> The `__eq__` dunder method should take two objects (one of which is `self`) and return `True` if the two objects should be considered equal - otherwise return `False`.
>
> > ## Solution
> > ~~~
> > class Book:
> >     def __init__(self, title, author):
> >         self.title = title
> >         self.author = author
> >     
> >     def __str__(self):
> >         return self.title + ' by ' + self.author
> > 
> > def __eq__(self, other):
> >         return self.title == other.title and self.author == other.author
> > 
> >     
> > class Library:
> >     def __init__(self):
> >         self.books = []
> >     
> >     def add_book(self, title, author):
> >         self.books.append(Book(title, author))
> >     
> >     def __len__(self):
> >         return len(self.books)
> >     
> >     def __getitem__(self, key):
> >         return self.books[key]
> >     
> >     def by_author(self, author):
> >         matches = []
> >         for book in self.books:
> >             if book.author == author:
> >                 matches.append(book)
> >
> >         if not matches:
> >             raise KeyError('Author does not exist')
> >         
> >         return matches
> > 
> >     @property
> >     def titles(self):
> >         titles = []
> >         for book in self.books:
> >             titles.append(book.title)
> > 
> >         return titles
> >
> >     @property
> >     def authors(self):
> >         authors = []
> >         for book in self.books:
> >             if book.author not in authors:
> >                 authors.append(book.author)
> > 
> >         return authors
> > 
> >     def union(self, other):
> >         books = []
> >         for book in self.books:
> >             if book not in books:
> >                 books.append(book)
> >                 
> >         for book in other.books:
> >             if book not in books:
> >                 books.append(book)
> >                 
> >         return Library(books)
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

{% include links.md %}

