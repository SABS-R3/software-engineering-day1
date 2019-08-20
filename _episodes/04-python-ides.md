---
title: "Python Integrated Development Environments"
teaching: 80
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## Jupyter Notebooks


### Object State within Notebooks

When I type code in the notebook, the objects live in memory between cells.

~~~
number = 0
print(number)
~~~
{: .language-python}

~~~
0
~~~
{: .output}

If I change a variable:

~~~
number = number + 1
print(number)
~~~
{: .language-python}

~~~
1
~~~
{: .output}

It keeps its new value for the next cell. But cells are not always evaluated in order.

If I now go back to Input 33, `reading number = number + 1`, and run it again, with shift-enter. Number will change from 2 to 3, then from 3 to 4. Try it!

So it's important to remember that if you move your cursor around in the notebook, it doesn't always run top to bottom.


## PyCharm


{% include links.md %}

