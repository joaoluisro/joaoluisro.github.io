---
layout: post
title: Recursion and induction
subtitle: How recursive functions and proof by induction are connected.
#gh-repo: daattali/beautiful-jekyll
#gh-badge: [star, fork, follow]
tags: [induction, recursion, algorithms]
comments: true
---
## Recursion
As a computer science student, you'll often hear the words recursion or recurrence to label functions that "call themselves", most likely in a algorithms course. When i first got in contact with recursion, it was for implementing the factorial function in a non-iterative way.

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

## Induction
Another powerful idea you are going to encounter as a CS student, is the concept of proof by induction, most likely in a algebra course or a discrete mathematics one.
It is used to prove statements about integers in a very simple way, which makes it a very powerful tool when dealing with them. For example say that you suspect that for every integer $n$ $\geq$ $0$ the statement $P(n)$ :
$$\begin{equation}
  \nonumber
  \sum_{i=1}^{n} i = \frac{n(n + 1)}{2}
\end{equation}$$ is true.
So how does one go about proving it? Proof by induction is probably your best bet. Here's how it works:

* 1) Prove that for the base case $P(0)$, the statement holds.
* 2) Assume that for $a$ $\in$ $[0..k]$ the statement $P(a)$ is true.
* 3) Prove that $P(k+1)$ is true.

For first-year CS me that was some pretty advanced stuff, but that's because i didn't see the bigger picture back then. The idea is to "induce" all the integers to verify that the statement is in fact true. We start proving that for $n$ $=$ $0$ the statement holds, we call that our base case. Next, by assuming that given an integer $a$ $\in$ $[0..k]$ the statement $P(a)$ is true, we can then prove that $P(k+1)$ is also true. If you have followed these steps you have proven the statement $P(n)$ for all $n$ $>$ $0$. Now why does that work? Here's the catch: By proving that $P(0)$ is true, we have then proved that $P(1)$ is also true, by 2) and 3). But wait a minute, that means that $P(2)$ is also true, and that means that $P(3)$ also is, and $P(4)$... A domino effect. The idea is that each $P(k)$ guarantees that the next $P(k+1)$ is true, hence the name "induction".

## Connecting the dots

In a course about theoretical CS (namely Introduction to Theoretical Computer Science CI1059) we were talking about how the extended transition function of a Finite-Deterministic-Automata could be described by a recurison, and that we should prove it by induction. At that moment, the professor told us something quite shocking: Induction *is* Recursion.

Now why did he say that? This dude with a Phd gets to be paid to say nonsense? Let's investigate this a bit further.

The idea is to look at recursion in a different angle, from a different perspective. Ok so what is recurson afterall? Just a function that calls itself and does stuf? Well, yes, but it's something much bigger than that.
Let's think about binary search for a minute, so i can provide an example to what the main idea is. Here's the pseudo-code :

```
BinarySearch(x,v,a,b)
  1. if a > b
  2.  return a - 1
  3. m = (a+b)/2
  4. if x < v[m]
  5.  return BinarySearch(x, v, a, m-1)
  6. else
  7.  return BinarySearch(x, v, m+ 1, b)
```
What it does is to look for a value $x$ in a sorted array $v$ in the interval $[a..b]$. By using a divide-and-conquer strategy, the algorithm first checks whether $a$ and $b$ are in ascending order (1), this is our *base case*. Next, it breaks the problem in two by taking the element in the middle (m) and calling ´´BinarySearch()´´ on the half that contains numbers which are greater than $x$, creating a recursion.

How do we make sure that the algorithm works? Simple, just use induction. By taking the three induction steps, we'll finally start to see how these two concepts are actually connected. The proof is not hard, but this post is starting to get long already, so i'll just link it [here](https://www.cs.cornell.edu/courses/cs211/2006sp/Lectures/L06-Induction/binary_search.html).   

By proving the algorithm is correct, you can start to see similarities between the two concepts. Both have corresponding base-cases, but that's about it right? Well remember the domino effect that our proof had? It's easy to see that when we think about recursion, the same process takes shape, in our example, by assuming that the element is either in the lower or upper part of the array, we know what its exact position is. It's easier if you think about it in terms of induction, by assuming that an instance of size $k+1/2$ is correct we can then prove that a instance of size $k+1$ is also correct. Doing for all integers leads us to the base case, where we know for a fact that the answer is correct. This is the important part of the recursion, the relation between some arbitrary instance $k$ and the next one $k+1$, which is pretty much steps 2) and 3) of induction.

The correctness proof and the execution of a recursive algorithm are strictly connected, meaning that induction and recursion are in the end, the same thing. My final thoughts are that the next time you find yourself asking over how a certain recursive algorithm works, think about it as a black box, or as i mentioned, a statement $P(n)$. Then, apply the induction steps and see what is the relation between a certain instance $P(k)$  and the next one $P(k+1)$, and also what the base case is. After that, you'll have internalized what the recursion is trying to tell you.
