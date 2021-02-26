---
layout: post
author: Dougie
category: programming
---

I’ve been spending time with Python recently and am beginning to really like some of the language’s features. List comprehension (listcomp) creates a list by evaluating an expression on each item in a given list, from left to right.
<!-- more -->
It combines and expression and a loop:
```python
>>> [ord(letter) for letter in 'example']
[101, 120, 97, 109, 112, 108, 101]
```
Apply a condition:
```python
>>> [ord(letter) for letter in 'example' if ord(letter) < 112]
[101, 97, 109, 108, 101]
```
It’s useful for combining lists:
```python
>>> [(letter, number) for letter in 'ab' for number in '12']
[('a', '1'), ('a', '2'), ('b', '1'), ('b', '2')]
```
Pimoroni’s Rainbow Hat introduction has an example to cycle colours on the LED rainbow:
```python
for i in range(101):
    h = i / 100.0
    r, g, b = [int(c * 255) for c in colorsys.hsv_to_rgb(h, 1.0, 1.0)]
    rh.rainbow.set_all(r, g, b)
    rh.rainbow.show()
```
This is a little hard to follow but we’ll break it down. Hue, Saturation and Value (HSV) represents colour using three values between 0.0 and 1.0 creating a colour “wheel” that is easy to cycle on the LED. Unfortunately the LED combines red, green and blue. The Colorsys library can convert between the two.

The expression is `int(c*255)`. The loop is `for c in colorsys.hsv_to_rgb(h, 1.0, 1.0)`

The `h=i/100` is giving a range of values from 0.0 to 1.0 in 0.01 steps (we could use a list comprehension too `[i/100 for i in range(101)]`).

So let’s look at a snapshot, where h=1.3:
```python
>>> colorsys.hsv_to_rgb(0.13,1.0,1.0)
(1.0, 0.78, 0.0)
```
Which the list comprehension converts to:
```python
>>> [int(c*255) for c in colorsys.hsv_to_rgb(0.13, 1.0, 1.0)]
[255, 198, 0]
```
Giving us the RGB value needed.
