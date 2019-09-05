---
title: "Programming Paradigms"
teaching: 10
exercises: 0
questions:
- "What are programming paradigms?"
- "Why do they exist?"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## Programming Paradigms

> In science and philosophy, a **paradigm** (/ˈpærədaɪm/) is a distinct set of **concepts or thought patterns**, including theories, research methods, postulates, and standards for what constitutes legitimate contributions to a field.
>
> -- Wikipedia - Paradigm

### Imperative Programming
Code describes how data should be processed.

#### Structured Programming
Code should be grouped into logical blocks.

Early examples: Algol (1958)

#### Procedural Programming
Code should be grouped into procedures performing a single task.

Early examples: FORTRAN (1957), COBOL (1959)

#### Object Oriented Programming
Data should be structured.  Code should be stored with the data it processes.

Early examples: Smalltalk (1972)

### Declarative Programming
Code describes what the result of data processing should be

#### Functional Programming
Functions are mathematical operations and should perform exactly one task.  Code is data.

Early examples: Lisp (1958)

## FizzBuzz

FizzBuzz is a simple game often used as an example to compare programming languages.
In FizzBuzz, you count up from the number one, but replace every number divisible by three with 'Fizz' and every number divisible by five with 'Buzz'.
Numbers which are divisible by both three and five become 'FizzBuzz'.

~~~
1, 2, Fizz, 4, Buzz, Fizz, 7, 8, Fizz, Buzz, 11, Fizz, 13, 14, FizzBuzz, ...
~~~
{: .output}

We see below, three implementations of FizzBuzz, taken from Rosetta Code with minor modification.

First we see an implementation in C.
As a language, C is typical of the procedural paradigm.

~~~
#include<stdio.h>
 
int main (void)
{
    int i;
    for (i = 1; i <= 100; i++)
    {
        if (!(i % 15))
            printf("FizzBuzz");
        else if (!(i % 3))
            printf("Fizz");
        else if (!(i % 5))
            printf("Buzz");
        else
            printf("%d", i);
 
        printf("\n");
    }
    return 0;
}
~~~
{: .language-c}

Next we see an implementation of FizzBuzz in Java, a strongly Object Oriented language.
One of the most obvious things about this version is that although the core is very similar to the C version, we have added an extra layer of wrapping around the whole program, in the form of `class FizzBuzz`.
Note also the difference in how the text is printed to the terminal as compared to the C version.

~~~
class FizzBuzz {
 
    public static void main(String[] args) {
 
        for (int i = 1; i < 101; i++) {
            if ((i % 3 == 0) && (i % 5 == 0)) {
                System.out.println("FizzBuzz");
            } else if (i % 3 == 0) {
                System.out.println("Fizz");
            } else if (i % 5 == 0) {
                System.out.println("Buzz");
            } else {
                System.out.println(i);
            }
        }
    }
}
~~~
{: .language-java}

Finally, we see the same program in Haskell, a typical functional language.
Here the program looks completely different from both of the previous versions.
The program no longer describes the flow of control, but a sequence of operations which are to be performed

~~~
fizzbuzz :: Int -> String
fizzbuzz x
  | f 15 = "FizzBuzz"
  | f 3 = "Fizz"
  | f 5 = "Buzz"
  | otherwise = show x
  where
    f = (0 ==) . rem x
 
main :: IO ()
main = mapM_ (putStrLn . fizzbuzz) [1 .. 100]
~~~
{: .language-haskell}

{% include links.md %}