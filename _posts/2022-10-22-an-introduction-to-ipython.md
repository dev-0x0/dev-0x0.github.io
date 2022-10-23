---
layout: post
title: An Introduction to IPython
date: '2022-10-22 18:31:19 +0100'
categories: [Python, Linux]
tags: [python, linux, windows, productivity]
---

![intro to ipython](/assets/img/introduction-ipython.jpg)

_This is a repost of an old article I originally wrote at [null-byte.wonderhowto.com](https://null-byte.wonderhowto.com/how-to/introduction-ipython-0161135/_)_

```ipython``` is a tool that I used heavily throughout my time in the PEN-200 labs, and also in the OSCP exam. It allows me to rapidly debug Python exploits and other scripts, as well as perform operations like service enumeration(with modules such as ```ldap3```), task involving sockets, complex data transformations and sorting procedures that would be a little more inconvenient in the Linux terminal. It is basically the default Python interpreter on steroids.
Now on to the original article.

## What Is ipython?

<p>IPython is a richly featured replacement for the standard python interpreter. It offers a wider range of functionality, that the standard
interpreter, which generally ships with python, sorely lacks. It's a great tool for learning Python faster than you would without it, kind of like a handy cheat-sheet that's at your fingertips. It excels as a quick Python object reference(examples below), and for testing snippets of code on-the-fly. But these are just a few of the many features useful to the Python scripter. In this introduction, I will show off some it's most useful features. IPython is available for Linux, Mac and Windows.</p>

## Installing ipython
<p> I will assume here that you are using Kali linux/debian. If not, just replace the commands with the relevant ones for your distro. To install on Kali, type:</p>

```apt-get install ipython```

OR for the python 3.x version

```apt-get install ipython3```

<p>If you're trying this on Windows, already have Python installed(I will assume you do), and have some experience installing packages, you can get it with the command:</p>

```pip install ipython``` _replace with ipython3 if you use python 3.x_

Some links that can help with installation issues are here:<br>
[https://pypi.python.org/pypi/pip](https://pypi.python.org/pypi/pip)<br>
and here:<br>
[http://ipython.org/install.html](http://ipython.org/install.html)<br>

And [here](https://null-byte.wonderhowto.com/how-to/hack-like-pro-getting-started-with-kali-your-new-hacking-system-0151631/) :)<br>


## Using ipython

To start ipython, open a command prompt, and type ```ipython```
You should see this new prompt in the terminal:

![ipython terminal](/assets/img/ipython-termnal.jpg)

<p>In the examples below, I will be using Kali and the IPython for Python 2.x</p>

## Why Use ipython?

### Object exploration, a handy on-the-fly reference

IPython makes exploring and learning more about python objects(modules, data-types, data-structures etc.) a breeze. See for yourself. Let's say you wanted to find out more about the ```itertools``` module(a very useful module). IPython makes this simple:

![explore objects](/assets/img/ipython-terminal2.jpg)

The command takes the form ```object_name?```
Now hit ```<return>```

![explore objects 2](/assets/img/ipython-terminal3.jpg)


We get the modules docstring, and we find out that ```itertools``` contains "Functional tools for creating and using iterators"... Great!

Pressing ```<Enter>``` or the up/down directional keys will navigate through the rest of the docstring. We can escape back to IPython by pressing '**q**'.

However, it's not just modules you can do this with, you can also do this for python types(```str```, ```list```, ```tuple```, ```dict``` ... etc), variables you have created and ... well pretty much any object in python... and that's pretty useful, because in python, everything is an object!

![explore objects 3](/assets/img/ipython-terminal4.jpg)
![explore objects 4](/assets/img/ipython-terminal5.jpg)


### Tab Completion

Another great feature of ipython is it's Tab-completion. We can find out what methods itertools has by typing ```object_name.<TAB>``` (```<TAB>``` = press the TAB key):<br>

![tabbing](/assets/img/ipython-terminal6.jpg)


Now I want to know more about ```itertools.permutations```, again I can use ```object_name?```<br>

![tabbing2](/assets/img/ipython-terminal7.jpg)


This is also useful if you can't quite remember the name of the method you want, but you do remember for instance, the letter it started with. In this instance we could type, ```object_name.first_letter<TAB>``` which gives you all the methods starting with that letter.

![tabbing3](/assets/img/ipython-terminal8.jpg)


In short, typing ```object_name.<TAB>``` will work for almost any object, displaying it's attributes and methods, if it has any. This also works on file and directory names and any objects you may have created yourself!

## Magic Functions

These are 'magic' predefined functions whose syntax is much like that of a command line call. There are two types, **line magics** and **cell magics**.

**Line magic** syntax takes the form<br>
```%func_name <args>```
where ```<args>``` is the rest of the line, without quotes or parentheses.

Cell magics syntax is <br>
```bash
%%func_name <args>
<args>
<args>
...
```

where ```<args>``` are both the rest of the line, and in a seperate argument, the lines that follow it. Note that we use '**%**' twice for cell magics, once for line magics.

A brief example:<br>

![magic functions](/assets/img/ipython-terminal9.jpg)


A full list of magic functions can be seen by typing<br>
`%lsmagic`
<br>

Finally, to exit ipython, simply type exit and hit `<Enter>`

## In Conclusion

IPython is a very useful tool for scripting with python as a quick, easy, suitably in-depth reference, scratchpad(for testing snippets of code on the the fly) and last, but not least, for expanding your knowledge of python. 

# Summary

Explore Object:

`object_name?`

TAB-completion:

`object_name.<TAB>`

Magic Functions:

`%line_function <args>`


```bash

%%cell_function <args>
<args>
...

```