---
title: "Brief Introduction to the Bash Shell"
teaching: 10
exercises: 0
questions:
- "What is the Bash shell?"
- "How do I use the shell to run programs?"
- "How do I navigate the file system using the shell?"
objectives:
- "FIXME"
keypoints:
- "FIXME"
---

Before we venture into Python, we need to take a look at the *Bash shell*, which is one way of running programs on a computer. Throughout this course we'll be using the Bash shell a great deal, and it's arguably an invaluable tool for anyone looking to write software: it gives you greater control over your computer's functions, many operations are more efficient using a shell-type interface, and performing a sequence of instructions many time over is often far more efficient than using a graphical interface.

## What is the Bash Shell?

The most common way users interact with their computers today is via graphical user interfaces, such as those present in Microsoft Windows or Mac OS. However, before these came along it was typical to feed instructions to computers purely via the keyboard, into a *command line* interface, or CLI for short: commands are typed in, executed by the computer, and output from those commands displayed to the user, with this cycle constantly repeating.

This description makes it sound as though the user sends commands directly to the computer, and the computer sends output directly to the user. In fact, there is usually a program in between called a command shell. What the user types goes into the shell, which then figures out what commands to run and orders the computer to execute them. Note, the shell is called the shell because it encloses the operating system in order to hide some of its complexity and make it simpler to interact with.

One of the most prevalent ones, the Bash shell, has been around longer than most of its users have been alive. It has survived so long because it’s a power tool that allows people to do complex things with just a few keystrokes. It also helps them combine existing programs in new ways and automate repetitive tasks so that they don’t have to type the same things over and over again. Use of the shell is fundamental to using a wide range of other powerful tools and computing resources (including “high-performance computing” supercomputers).

## Running the Shell

Let's start by running the shell. Programs that give you access to a shell are often called a *terminal*. So let's open a new terminal by right-clicking on the desktop and selecting `Open in Terminal`. You'll be presented with a new window and something like the following:

~~~
sabsr3@sabsr3-VirtualBox:~/Desktop$
~~~
{: .language-bash}

This is the *command prompt*, which awaits your commands:

- `sabsr3` represents your username you logged in as
- `sabsr3-VirtualBox` represents the name of this virtual machine
- `~/Desktop` is the folder - or directory in Linux speak - you are currently in, showing where you currently are on the filesystem. We'll look into this a bit later

From here, you can type in and execute commands and see their output. For example, if you type the following and press `Enter`, it should show you your username:

~~~
whoami
~~~
{: .language-bash}

And you should see:

~~~
sabsr3
~~~
{: .language-bash}

So here, we are seeing the fundamentals of the command line in action: type a command, have it executed, and show us some output from that command.

## Navigating the File System

One aspect of using the shell that is often confusing is where and how you access files, and how this is represented within the shell. One key thing to remember is that the shell is always *somewhere* in your filesystem. This location is known as the *working directory*, and commands you run in the shell take this into account - it is the directory that the computer assumes we want to run commands in unless we explicitly specify something else.

One thing that tells us where we are is the prompt, which tells us we are at `~/Desktop` - the `~` is a shell shorthand that refers to our account's home directory, and `Desktop` is a directory within our home directory. Now within the SABS Ubuntu VM or provisioned laptops, our home directory is located at `/home/sabsr3`. So, in fact, we are currently located at `/home/sabsr3/Desktop` (if we replace the `~` shorthand).

Another way to find out where we are is the following - which stands for "print working directory" - and will output the current working directory in your shell:

~~~
pwd
~~~
{: .language-bash}

~~~
/home/sabsr3/Desktop
~~~
{: .language-bash}

So similarly, this tells us we are in the `Desktop` directory, which is within our home directory at `/home/sabsr3`. We can also see what's in this directory by using `ls`, which is short for "list":

~~~
ls
~~~
{: .language-bash}

And we should see that nothing is printed, and the shell unceremoniously returns us to the prompt! This is because there is nothing in the `Desktop` directory, so nothing is printed. This is fairly typical of shell commands: when nothing needs to be reported, nothing is printed.

So let's take a look at a slightly more interesting directory. We can *move* our working directory by using the `cd` (change directory) command, and then take a look. Let's say we wanted to see what is in our home directory, i.e. `/home/sabsr3`, which is the directory *above* this one. We could type the following, which brings us up one directory:

~~~
cd ..
~~~
{: .language-bash}

Here, we're passing an *argument* to the `cd` command. The `..` argument here means "the directory above".

We can check our working directory using `pwd` as before:

~~~
pwd
~~~
{: .language-bash}

~~~
/home/sabsr3
~~~
{: .language-bash}

And typing `ls` now, we should see:

~~~
Desktop  Documents  Downloads  Music  Pictures  Public  snap  Templates  Videos
~~~
{: .language-bash}

Another way to think about this is that it's very similar to how a file explorer or viewer application shows you files. If you click on the folder-type icon in the sidebar for example, you should see:

![gui-directory](../fig/02-gui-directory-view.png)

Which in this case, indicates the files present in the `/home/sabsr3` directory. Now, we can use the interface in a graphical way to move around and view the file system, which in a nutshell, is equivalent to using the `cd` and `ls` commands.

We can also pass special arguments to commands which change its behaviour. These typically are prefixes with a `-`. For example, if we use `-F` with `ls`, it will show us the type of each entry shown (e.g. which are files and which are directories):

~~~
ls -F
~~~
{: .language-bash}

~~~
Desktop/    Downloads/  Pictures/  snap/       Videos/
Documents/  Music/      Public/    Templates/
~~~
{: .language-bash}

A following `/` indicates a directory - so, in this case, all directories!

Now if we want to go back into the `Desktop` directory (a subdirectory of our home directory), we can pass it as an argument:

~~~
cd Desktop
~~~
{: .language-bash}

So far, we've been moving around using *relative* directory designations, either moving from our current directory to a directory above, or moving down into a subdirectory. But we can also move to other directories with an *absolute* directory reference. To get to our home directory, for example:

~~~
cd /home/sabsr3
~~~
{: .language-bash}

Other commands that reference directories - and files - operate the same way, as we'll see later. `ls /home/sabsr3` for example would show us the contents in that specified directory.

## Manipulating Files

We can also change things on the filesystem using various commands. To illustrate, let's create a file to play with first in your home directory. We can use the `touch` command to create an empty file for us:

~~~
cd
touch test.txt
ls -F
~~~
{: .language-bash}

Note here we didn't pass any argument to `cd` at all, in which case `cd` will put us in our home directory. We should see something like:

~~~
Desktop/    Downloads/  Pictures/  snap/       test.txt
Documents/  Music/      Public/    Templates/  Videos/
~~~
{: .language-bash}

We can copy files using `cp`:

~~~
cp test.txt test2.txt
ls
~~~
{: .language-bash}

~~~
Desktop/    Downloads/  Pictures/  snap/       test2.txt  Videos/
Documents/  Music/      Public/    Templates/  test.txt
~~~
{: .language-bash}

And we can move files using `mv` (e.g. into the `Documents` directory):

~~~
mv test2.txt Documents
ls -F Documents
~~~
{: .language-bash}

~~~
test2.txt
~~~
{: .language-bash}

Another feature of `mv` is that we can use it to rename files:

~~~
mv Documents/test2.txt Documents/file.txt
~~~
{: .language-bash}

So here, we reference the `test2.txt` file we want to rename in the `Documents` directory by specifying the directory first.

We can also delete files using `rm`. **Warning:** many versions of Linux, including this one, will not prompt for confirmation of the deletion first: the file will be immediately deleted. Plus, once you delete a file using this method, note the file will not be retrievable. This is unlike other graphical methods of deleting files with a file explorer, where they often end up in a "trash" folder where they can be "undeleted".

~~~
rm test.txt
rm Documents/file.txt
~~~

Which puts our file system back into the state we first found it!


{% include links.md %}

