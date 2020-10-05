---
title: "VSCode as an Integrated Development Environment"
teaching: 30
exercises: 0
questions:
- "What is VSCode and what are the advantages of using it?"
- "How can my scripts do different things based on data values?"
- "How can I do the same operations on many different values?"
objectives:
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


## Running VSCode for the First Time

Microsoft's VSCode is a lightweight IDE which is great when starting out developing programs. It not only supports Python, but also C++, C#, JavaScript, CSS, and Java, amongst others. It's also available for Mac OS, Linux, and Windows. Whilst lightweight, it's features can be readily extended via installation of plugins to suit your needs, and you can even develop your own plugins for VSCode.

If you haven't run VSCode yet, do this now. Select `Show Applications` from the grid-type icon in the lower left hand corner of the desktop, and type `vscode` into the text box at the top, and select the VSCode application that appears. You'll be presented with the VSCode interface.

The first thing we need to do is open our `2020-se-day1/code` folder in VSCode. Select `Open Folder` from the bar on the left, and a dialogue window will appear. Select `Home` from the navigation bar on the left and then double click on `2020-se-day1`, then double click on `code`. Finally, select `OK` in the top right of the window. This directory is now the current working directory for VSCode, so when we run scripts from VSCode, this will be the working directory they'll run from.

If you'd like to explore VSCode in more depth than this course offers, see the [VSCode documentation](https://code.visualstudio.com/docs).


## Our First Python Standalone Script

In the navigator window on the left, right-click on `Code` and Select `New` > `Python File`.  Enter `hello_world.py` into the dialog box, and press enter. This new empty file will be brought up in the editor.

Let's start with a classic 'Hello world' script:

~~~
print('Hello world!')
~~~
{: .language-python}

Then select `File` > `Save All`.

### Configure PyCharm with Anaconda

However, before we can run it, we need to configure PyCharm so that it knows where the Python interpreter is located which we want to use to run it. In our case, this is the Python interpreter that is supplied within the Anaconda Distribution. To do this:

- Select either `PyCharm` > `Preferences` (MacOS) or `File` > `Settings` (Linux)
- Then, in the preferences window that appears, select `Project: code` > `Project Interpreter` from the left. You'll see a number of Python packages displayed as a list, and importantly above that, the current Python interpreter that is being used. This is likely the default version of Python installed on your system, e.g. `Python 2.7 /usr/bin/python2.7` or `Python 3.6 /usr/bin/python3.6`, which we don't want to use.
- Select the cog-like button in the top right, then `Add ...`. An `Add Python Interpreter` window will appear.
- Select `Conda Environment` from the list on the left so it will use Anaconda, and ensure that `New environment` is selected. Enter `/home/sabs-r3/anaconda/envs/code` in the `Location` field, then select `Make available to all projects` so we can use it with other projects later.
- Select `OK` in the `Add Python Interpreter` window. Back in the `Preferences` window, you should see `Python 3.7 (code)` or similar in the `Project Interpreter` window.
- Select `OK` in the `Preferences` window.

It may take a few minutes for PyCharm to read and familiarise itself with the Anaconda installation you've configured (you may see `n processes running` in the bar at the bottom of the PyCharm IDE while it does this).

Now we've told PyCharm about the new interpreter, we can configure it for our project:

- Select `Add Configuration...` from the top right of the IDE window.
- Select `+` from the top left to add a configuration, selecting `Python` from the drop down list. You should see `Python 3.7 (code)` or similar in the `Python interpreter` field in the window. For `Script path`, select the folder button and find and select `Hello_world.py`. This tells PyCharm which script to run. You can even give this configuration a name if you like.
- Select `OK` to confirm these settings.

> ## Virtual Environments
>
> So we've created a new Python configuration within which our script can run. These are commonly known as *virtual environments*. What is a virtual environment, and why use them?
>
> Consider developing a number of different Python scripts that each have their own package dependencies (and versions of those dependencies) on the same machine. It could quickly become confusing as to which packages and package versions are required by each script, making it difficult for others to run your script themselves (or yourself on another machine!). Additionally, different scripts may need to use different versions of a given package.
>
> A virtual environment is a self-contained directory tree that houses a specific Python interpreter and specific versions of a number of Python packages, so as package dependencies are added to a script (or set of scripts), you can add them to this specific virtual environment. So, you can avoid a great deal of confusion by having separate virtual environments for each script.
{: .callout}

Once done, you're ready to run your script!


### Running the Script from within PyCharm

Right-click the `hello_world.py` file in the PyCharm navigator on the left, and select `Run hello_world`. The program will run in a terminal window at the bottom of the IDE window and display something like:

~~~
/Users/user/.conda/envs/code/bin/python /Users/user/module01_se_day1-gh-pages/code/hello_world.py
Hello World!

Process finished with exit code 0
~~~
{: .output}

Here, we can see that a new shell has been created that uses the Anaconda interpreter at `/Users/user/.conda/envs/code/bin/python` to run our script located at `/Users/user/module01_se_day1-gh-pages/code/hello_world.py`.

### Running the Script from the Command Line

You'll remember that we were originally running the Python interpreter directly from the command line earlier. Let's run our new script using Python from the command line.

First, we can make use of the Python Anaconda environment we created for our script. Open up a new terminal and type the following to list all the environments Anaconda is aware of:

~~~
conda env list
~~~
{: .language-bash}

We can see our environment we created (`code`) in this list, so let's use that:

~~~
conda activate code
~~~
{: .language-bash}

Now we can run our script in that environment, ensuring first we are in the directory where it resides:

~~~
cd module01_se_day1-gh-pages/code
python hello_world.py
~~~
{: .language-bash}

~~~
Hello World!
~~~
{: .output}

So here, we're doing a very similar thing to what PyCharm was doing when running our script: we give the command line the Python interpreter to run (which will use the one in the environment we created) and our script, which resides in the local directory.

## Python Control Flow

Let's look at how we can influence control flow within a Python script using loops and conditionals. We'll use PyCharm to write a new script.

Create a new script, as we did before, by right-clicking the `code` directory in the PyCharm navigator on the left, and selecting `New` > `Python File`. Let's call this script `vowels.py`.

### Loops

~~~
vowels = "aeiou"

for letter in vowels:
    print(letter)
~~~
{: .language-python}

Unlike many other languages where a `for` loop is just an incremental counter over a defined range of numbers, Python's loop is based around the higher level concept of `for value in collection`. So here, `value` is our usual loop variable and `collection` can be any collection of things, like a string is a collection of letters, or a list is a collection of objects, etc. The loop will iterate over each of them.

You'll notice the body of the loop doesn't have any traditional syntax to show its end, e.g. `}` like in C or Java. The indentation is sufficient to designate the loop body. Python's syntax has taken into account many lessons learned from decades of programming language development, and research has shown that people tend to just look at indentation to identify inner code blocks, so Python just uses that. Notice the `:` however, which indicates the start of the loop body.

Now, save our file and run it within PyCharm, and within the terminal you should see:

~~~
a
e
i
o
u
~~~
{: .output}

Going back to traditional `for` loops, Python has a built-in function called `range()` which can generate a sequence of numbers. Create a new Python file called `range.py` e.g.:

~~~
for x in range(1, 10, 2):
    print(x)
~~~
{: .language-python}

So here, the syntax is `range(start, stop, step)`, but note that `stop` is non-inclusive, so the sequence printed will not include this number. Right-click on this new Python file and select `Run range` this and you get:

~~~
1
3
5
7
9
~~~
{: .output}

### Conditionals

Let's go back to extending our vowels script to do something involving Python's conditional `if` statement. Select the `vowels.py` tab from the code editor.

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

Save and re-run it, and you'll notice the `for` loop and `letter.lower() in vowels` works exactly as it did before. The design of Python's syntax aims to be minimal: there should only be one (ideally obvious) way to do something. This keeps the language simple, and is in contrast to many other languages. A notable counter-example being Perl where there are many, many ways to anything in the language, which can make learning Perl and sharing it with others a challenge - the way you might do something in Perl might be very different to how someone else does it. In Python, at least from point of view of syntax, generally people's code tends to look the same which generally makes reading other people's Python code easier.

Interestingly, Python doesn't have the equivalent of a `case`/`switch`, instead, you need to use `if` with multiple `elif` statements, with an optional `else` at the end. The reason for this is that there have been many proposals for one in Python (e.g. PEP 3103), but nobody has been able to suggest one that fits well with Python's syntax and established coding style.

{% include links.md %}