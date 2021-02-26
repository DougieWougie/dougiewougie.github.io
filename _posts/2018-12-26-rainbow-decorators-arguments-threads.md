---
layout: post
author: Dougie
category: programming
---

Playing with Rainbow Hat I learned a few things about Python as a result I found out what a decorator is, the difference between args and kwargs and threads. I also learned that a lot of guides don’t understand either.

> If you can’t explain it simply, you don’t understand it well enough.[^1]
<!-- more -->
## Decorators

Rainbow Hat documentation says “use touch handlers either by passing in a function by name, or using the method as a decorator”.

Learning Python (Lutz, 2013) dedicates a chapter to decorators and sums it up rather well:

> In short, decorators provide a way to insert automatically run code at the end of function and class definition statements—at the end of a def for function decorators, and at the end of a class for class decorators. [^2]

With similar notation to Java’s annotations:

```python
@decorator_function def function(arguments): ...
```

Python is running one function through another and binding the result to the original function name.

```python
def function(arguments):
    ...

function = decorator_function(function)
```

For example, Python has a built in function that returns a static method **staticmethod(function)**. To make **example_func** static, we put:

```python
@staticmethod
def example_func(arg)
    ...
```

Which is rebound to:

```python
staticmethod(example_func)(arg)
```

So now I know what a decorator is in Python, I used it for the buttons. What to use them for though? I figure that they should control speed of LED, sequence or colour. That’s going to need a thread running as an event handler.

## A short digression on arguments

What on earth is a key-worded argument? Lots of documentation refers to \*args and \*\*kwargs but had no idea what it was. Arguments passed to functions are read left to right:

```python
function('Dougie', 42)
```

But we can also use a key-value pair:
```python
function(name='Dougie', age=42)
```

Apart from improving readability in the function call, default arguments can be assigned in the function definition:

```python
def function(name='Dougie', age=42)
```

By convention these are referred to as arg and kwarg. Almost there – that just leaves the \*. Python lets you define functions that take any number of arguments, assembling them into a tuple. If you use key-value arguments, it assembles a dictionary.

```python
def function(**kwargs): {...}
```

Now the clever(er) bit because if you do the same on the function call, Python unpacks the argument into individual arguments (\*arg) or key-value pairs (\*\*kwarg).

```python
function(**kwargs)
```

## Back to the main thread

The Rainbow Hat has buttons so I want to use these to control rainbow speed. This seems suited to a thread running an event handler. The syntax for the thread library (hopefully explaining the digression) is:

```python
thread.start_new_thread (function_name, (*args, **kwargs))
```

Concurrency in Python is probably a post in its own right. The CPython interpreter bytecode isn’t fully thread safe. There are different interpretations of what that means so I’ll use the Open University definition:

> A class is considered thread-safe if its instances behave under concurrent method calls as if they were called sequentially.[^3]

Python source code is compiled to bytecode which is run in a VM as machine code. In order to ensure only one thread executes bytecode at once the current thread has to hold a global lock (Global Interpreter Lock (GIL)).

This means multiple processor cores aren’t being used. In this application it doesn’t matter because the interpreter emulates concurrency by routinely switching threads.

[^1]: Albert Einstein
[^2]: Learning Python (Lutz, 2013), pp1034 "Chapter 32: Advanced Class Topics"
[^3]: M362 Developing concurrent distributed systems (THE OU, 2008)
