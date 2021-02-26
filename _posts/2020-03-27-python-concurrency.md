---
layout: post
author: Dougie
title: Using Threading rather than Thread
category: programming
---

In an earlier post, I used Threads but the thread module in Python when I should be using threading. The [documentation](https://docs.python.org/3/library/threading.html) for threading says it builds upon the thread module (renamed \_thread):

> This module provides low-level primitives for working with multiple threads (also called light-weight processes or tasks) — multiple threads of control sharing their global data space. For synchronization, simple locks (also called mutexes or binary semaphores) are provided. The threading module provides an easier to use and higher-level threading API built on top of this module.

<!-- more -->
That makes sense, so I should be using the threading module. So why is there a leading underscore on thread? The [Style Guide (PEP 8)](https://www.python.org/dev/peps/pep-0008/#id36) says it’s a weak internal use indication and that for example modules with an underscore are not imported when using an asterisk.

There are two ways to use this module. Define a subclass and override the run method or to use the Thread class’s default run method. I’ll use the second method here.

The Python 2.x code I was using looked like this:

```python
import thread
thread.start_new_thread(scroll, (text,))
```

The new code:

```python
import threading

def scroll(text):
    print(text)

text = 'Example text'
thread = threading.Thread(target=scroll, args=(text,))
thread.start()
```

So this isn’t that different but it is a lot more readable. The arguments are explicit and there’s no ambiguity.

Fluent Python (Ramalho, 2015) suggests using   concurrent.futures package with Python 3.x. ThreadPoolExecutor and ProcessPoolExecutor implement interfaces to submit threads or processes respectively for execution. I’ll expand on this in a future post as it is useful to submit multiple tasks and collect results – however that’s not what is needed in this example.
