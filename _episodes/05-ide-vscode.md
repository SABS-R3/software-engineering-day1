---
title: "VSCode as an Integrated Development Environment"
teaching: 0
exercises: 40
questions:
- "What is VSCode and what are the advantages of using it?"
- "How can my scripts do different things based on data values?"
- "How can I do the same operations on many different values?"
objectives:
- "Run Python scripts from within VSCode."
- "Set up a development environment in VSCode."
- "Use if statements to conditionally process Python statements."
- "Use loops to iteratively process collections of values."
- "Use VSCode to write a Python script that uses conditionals and loops."
- "Store and retrieve Python scripts in VSCode."
keypoints:
- "Use `for variable` in sequence to process the elements of a collection one at a time."
- "The body of a for loop must be indented."
- "Use `if` condition to start a conditional statement, `elif` condition to provide additional tests, and `else` to provide a default."
- "The bodies of the branches of conditional statements must be indented."
- "Use `==` to test for equality, `!=` for inequality."
- "`X and Y` is only true if both `X` and `Y` are true."
- "`X or Y` is true if either `X` or `Y`, or both, are true."
- "Zero, the empty string, and the empty list are considered false; all other numbers, strings, and lists are considered true."
- "`True` and `False` represent truth values."
- "Python's design is such that there should only be one (ideally obvious) way to do something."
---

Using the Python interpreter directly is good for trying things out in Python, but when it comes to writing more complex programs we need a way to store these programs as files so we can rerun them. We could edit a Python script using a text editor like Notepad on Windows or Nano on Linux, but these have their limitations. Integrated Development Environments (IDEs) on the other hand, are program editors that have an array of powerful features to help us write code.

Python programs are also commonly known as *scripts*, because Python uses an *interpreter* to execute source code. Note that Python also *compiles* code into a more rapidly executed format as well, but this is an implicit process, and since Python presents itself largely as an interpreted language, it's programs can also be called scripts.


## Introduction to VSCode

Microsoft's VSCode is a lightweight IDE which is great when starting out developing programs. It not only supports Python, but also C++, C#, JavaScript, CSS, and Java, amongst others. It's also available for Mac OS, Linux, and Windows. Whilst lightweight, it's features can be readily extended for a variety of languages via installation of plugins to suit your needs, and you can even develop your own plugins for VSCode. As well as features like live debugging and context-sensitive code autocompletion, other notable features include:

- Revision/version control support: ability to work with Git source code repositories, uploading and synchronising changes to/from such repositories on e.g. GitHub. We'll be covering Git version control later in the course
- Live code development sharing: without exchanging changes using version control, you can view live changes being made by another team member collaboratively within your own VSCode editor


## Running VSCode for the First Time

If you haven't run VSCode yet, do this now. Select `Show Applications` from the grid-type icon in the lower left hand corner of the desktop, and type `vscode` into the text box at the top, and select the VSCode application that appears. You'll be presented with the VSCode interface.

The first thing we need to do is open our `se-day1/code` folder in VSCode. Select `Open Folder` from the bar on the left (or from the `File` drop down menu at the top of VSCode), and a dialogue window will appear. Select `Home` from the navigation bar on the left and then double click on `se-day1`, then double click on `code`. Finally, select `Open` in the top right of the window.


> ## Trusting Code
> 
> You may be asked whether you trust the authors of the files in this folder. Select the checkbox, and click 'Yes, I trust the authors' (although in general use some caution is recommended!)
{: .callout}

This directory is now the current working directory for VSCode, so when we run scripts from VSCode, this will be the working directory they'll run from.

If you'd like to explore VSCode in more depth than this course offers, see the [VSCode documentation](https://code.visualstudio.com/docs).


## Our First Python Standalone Script

Let's create our first Python script in VSCode and save it:

- Select `File` -> `New Text File` from the menu. A new file will appear.
- On line 1, you'll see a message about selecting a language. Click on `Select a language`, and type in `python`, and select `Python (python) Built-In`
. Select `File` > `Save As...`. You'll find yourself in the `se-day1/code` directory. Enter the filename `hello_world.py` at the top and select `Save`.

Let's start with a classic 'Hello world' script. Enter this into the editor:

~~~
print('Hello world!')
~~~
{: .language-python}

VSCode comes with Python support built-in. You'll notice that as you type, the editor is suggesting possible statements, functions (and also variables and other Python artifacts) that match what you've typed so far. When you write a function it fully recognises and understands, it will also pop-up some context-sensitive help about the function itself, including any documentation associated with it and a breakdown of the function's arguments. This is very helpful when dealing with libraries with many modules and functions. Also, for convenience, if you've only half-typed a function, variable, statement, etc. that it recognises as the only option, you can press `Tab` and it will autocomplete the rest of the typing for you.

 You may find you see a `Python - Get Started` window tab pop up that gives you some things to do next in Python. But for now, we'll keep editing our file in the `hello_world.py` tab, so select that. Once you've finished, select `File` -> `Save`.

Now let's try running our script from within VSCode. Select the `Run` icon on the far left navigation bar (it looks like an arrow pointing right with a bug in it), then select `Run and Debug`. It will ask you to `Select a debug configuration`, so select `Python File`. It will now run our script, and you should see a terminal window pop-up at the bottom, with something like the following text in it:

~~~
dtcse@dtcse-VirtualBox:~/se-day1/code$  /usr/bin/env /usr/bin/python3 /home/dtcse/.vscode/extensions/ms-python.python-2022.14.0/pythonFiles/lib/python/debugpy/launcher 38613 -- /home/dtcse/se-day1/code/hello_world.py
Hello world!
~~~
{: .language-bash}

Here, we can see that the interpreter `/usr/bin/python3` has been used to run the VSCode debugger on our `hello_world.py` script, which produces the shown 'Hello world!' output.


## Setting up a Virtual Environment

Before we start using VSCode beyond a 'Hello world' example, we should set up a new *virtual environment* for running our Python scripts. We are currently using the *global* installation of Python 3, and this is not considered good development practice.

> ## Why use a Virtual Environment, and what are they?
>
> Consider developing a number of different Python scripts that each have their own package dependencies (and versions of those dependencies) on the same machine. It could quickly become confusing as to which packages and package versions are required by each script, making it difficult for others to run your script themselves (or yourself on another machine!). Additionally, different scripts may need to use different versions of a given package.
>
> A virtual environment is a self-contained directory tree that houses a specific Python interpreter and specific versions of a number of Python packages, so as package dependencies are added to a script (or set of scripts), you can add them to this specific virtual environment. So, you can avoid a great deal of confusion by having separate virtual environments for each script.
{: .callout}

Go back to the terminal window, and exit the Python interpreter (either by typing `exit()` or pressing `Ctrl` and `D` at the same time).

In the Bash shell, type the following (whilst in the `se-day1/code` directory):

~~~
python3 -m venv venv
~~~
{: .language-bash}

This instructs Python to construct a new Python virtual environment for us. Within our `code` directory now, you should see a new `venv` directory. This will contain a localised copy of the Python3 interpreter, and any associated libraries we wish to install. But this local environment is particular to our current work; if we were to start a new project, we'd create another virtual environment for that one, and so on.

The first `venv` is the name of the tool we need to use to create a virtual environment, while the second `venv` is the name of the directory that the virtual environment will be put in.
Most people use either `venv` or `env` as the name for their virtual environment.

We can activate this virtual environment, and see what it contains, by doing:

~~~
source venv/bin/activate
pip3 list
~~~
{: .language-bash}

`source` runs a script that activates our virtual environment. `pip` is the de-facto Python package installer; in this case we're using the version for Python 3 specifically and asking it to list the packages that are currently resident in the virtual environment:

~~~
Package       Version
------------- -------
pip        22.0.2
setuptools 59.6.0
~~~
{: .output}

In addition to Python which is also installed, as we can see, we don't have any other packages installed yet, aside from `pip` itself, and `setuptools` (which contains functionality for building and distributing Python packages).

Note that this virtual environment is only active within our current terminal. If we start another terminal and want to use this virtual environment, we'd  have to activate it there as well. Also, if we were to close the terminal, the activation of this environment (not the environment itself) will be forgotten. When we want to use this virtual environment we have to remember to start it using the `source venv/bin/activate` command above from within `se-day1/code` directory each time we open a new terminal. Otherwise, by default, we will the using the global Python interpreter and not the specific environment we have created.

If we wanted to deactivate our virtual environment, and return to the globally available set of Python packages, we'd use `deactivate` on the command line (although don't do this now!).

Other languages make use of virtual environments, such as Ruby, JavaScript, and Go - it's a great way to keep your environments separate and avoid confusion over which dependencie belong with which project.


### Running the Script from the Command Line

You'll remember that we were originally running the Python interpreter directly from the command line earlier. From within the same terminal, type:

~~~
which python3
~~~
{: .language-bash}

And you should see something like:

~~~
/home/dtcse/se-day1/code/venv/bin/python3
~~~
{: .output}

Which confirms that we are using the Python 3 interpreter from within our virtual environment at `/home/dtcse/se-day1/code/venv`.

Now let's run our new script using our virtual environment from the command line:

~~~
python3 hello_world.py
~~~
{: .language-bash}

~~~
Hello world!
~~~
{: .output}

So here, we're doing a very similar thing to what VSCode was doing when running our script: we give the command line the Python interpreter to run (which will use the one in the environment we created in this case) and our script, which resides in the local directory.

## Python Control Flow

Let's look at how we can influence control flow within a Python script using loops and conditionals. We'll use VSCode to write a new script.

In VSCode, create a new script by selecting `File` and selecting `New Text File`, and save the script as`vowels.py` using `File` -> `Save As...`.

### Loops

Type the following into our new `vowels.py` file:

~~~
vowels = "aeiou"

for letter in vowels:
    print(letter)
~~~
{: .language-python}

Unlike many other languages where a `for` loop is just an incremental counter over a defined range of numbers, such as C, Python's loop is based around the higher level concept of `for value in collection`. So here, `value` is our usual loop variable and `collection` can be any collection of things, like a string is a collection of letters, or a list is a collection of objects, etc. The loop will iterate over each of them.

You'll notice the body of the loop doesn't have any traditional syntax to show its end, e.g. `}` like in C or Java. The indentation is sufficient to designate the loop body. Python's syntax has taken into account many lessons learned from decades of programming language development, and research has shown that people tend to just look at indentation to identify inner code blocks, so Python just uses that. Notice the `:` however, which indicates the start of the loop body.

Now, save our file and run it from the command line:

~~~
python3 vowels.py
~~~
{: .language-bash}

You should see:

~~~
a
e
i
o
u
~~~
{: .output}

If we want to duplicate how other traditional languages implement`for` loops, Python has a built-in function called `range()` which can generate a sequence of numbers. Create a new Python file called `range.py` and put in it, for example:

~~~
for x in range(1, 10, 2):
    print(x)
~~~
{: .language-python}

So here, the syntax is `range(start, stop, step)`, but note that `stop` is non-inclusive, so the sequence printed will not include this number. Run this on the command line just as we did for `vowels.py`:

~~~
python3 range.py
~~~
{: .language-bash}

~~~
1
3
5
7
9
~~~
{: .output}

### Conditionals

Let's go back to extending our vowels script to do something involving Python's conditional `if` statement. Select the `vowels.py` tab from the code editor, and change it to the following:

~~~
vowels = "aeiou"
sarcasm = ""

for letter in "Okay":
    if letter.lower() in vowels:
        repetition = 3
    elif letter.lower() == 'y':
        repetition = 2
    else:
        repetition = 1

    sarcasm += letter * repetition

print(sarcasm)
~~~
{: .language-python}

Note for conditional bodies, we just use indentation again.

So now we've added the following conditional actions:

1. If `letter` in lowercase is within the `vowels` string, we want to repeat the letter 3 times. Note we are able to ask about whether an element resides in our string just by doing `something in collection`.
2. If `letter` in lowercase is equal to `y`, we want to repeat the letter 2 times. Note we use `==` to designate equality. `!=` is used to designate inequality.
3. Otherwise, we just want the letter repeated once.

The script then uses a feature of Python that allows us to repeat the contents of a string as many times as we want.

Remember to right-click on the `vowels.py` file in the navigator and select `Run vowels` to run it.

~~~
'OOOkaaayy'
~~~
{: .output}

We mentioned previously that Python's `for` loop is a general one based on general collections. Try changing the `vowels` and `for` lines to use lists:

~~~
vowels = ['a', 'e', 'i', 'o', 'u']
...
for letter in ['O', 'k', 'a', 'y']:
~~~
{: .language-python}

Save and re-run it, and you'll notice the `for` loop and `letter.lower() in vowels` works exactly as it did before.

This illustrates a very important aspect of Python that helps to keep scripts simple. The design of Python's syntax aims to be minimal: there should only be one (ideally obvious) way to do something. This keeps the language simple, and is in contrast to many other languages. A notable counter-example being Perl where there are many, many ways to do anything in the language, which can make learning Perl and sharing it with others a challenge - the way you might do something in Perl might be very different to how someone else does it. In Python, at least from point of view of syntax, generally people's code tends to look the same which generally makes reading other people's Python code easier.

Interestingly, Python doesn't have the equivalent of a `case`/`switch`, instead, you need to use `if` with multiple `elif` statements, with an optional `else` at the end. The reason for this is that there have been many proposals for one in Python (e.g. PEP 3103), but nobody has been able to suggest one that fits well with Python's syntax and established coding style.

{% include links.md %}
