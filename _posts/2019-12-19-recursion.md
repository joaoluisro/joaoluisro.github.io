---
layout: post
title: Recursion and induction
subtitle: How recursive functions and proof by induction are connected.
#gh-repo: daattali/beautiful-jekyll
#gh-badge: [star, fork, follow]
tags: [induction, recursion, algorithms]
comments: true
---

As a computer science student, you'll often hear the words recursion or recurrence when talking about functions that "call themselves", most likely in a algorithms course. When i first got in contact with recursion, it was for implementing the factorial function in a non-iterative way.

So changing this :

```python
  def factorial(n):
    res = 1
    for i in range(1,n+1,1):
      res *= i
    return res
```
to this :
```python
  def factorial(n):
    if n == 0:
      return 1
    return n * factorial(n - 1)
```
My first thoughts were that it looked much simpler and elegant, and also resembled much more the formal factorial definition.
When our professor showed us other examples i was quite intriged by how it worked. To this day, i still feel like recursion is kinda "magical" in the sense that, at first, the code looks confusing and doesn't really do anything, until you actually understand it, and appreaciate its beauty.

Another powerful idea you are going to encounter as a CS student, is the concept of proof by induction, most likely in a algebra course or a discrete mathematics one.

Basically, when wanting to prove a certain statement for integers, for example say that you suspect that for every integer $n$ $>$ $0$ the following is true:
$$\begin{equation}
  \nonumber
  \sum_{n}^{i=1} i = \frac{n(n + 1)}{2}
\end{equation}$$

If you hate induction (i certainly did the first time i got in touch with it), i'll show why you shouldn't, and also, explain what is the connection that recursion and induction have.
