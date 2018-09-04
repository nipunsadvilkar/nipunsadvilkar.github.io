---
layout: post
title:  "Neural Networks And Deep Learning Book Chapter 1 Exercise 1 Solution"
date:   2017-09-04 21:00:00
comments: true
categories: blog
description: Solutions of "Neural Networks and Deep Learning by Michael Nielsen" Exercises
---


I must say [Neural Networks and Deep Learning by Michael Nielsen](http://neuralnetworksanddeeplearning.com/) is best deep learning book I have came across. It has perfect combination of theory plus code. It delves into deep mathematics as much as code. Methodology of "from-scratch" implementation of neural networks and exercises in between really encourages you to think carefully about what's actually happening underhood of neural networks.

Following is my attempt to those exercises:


<h1 style="font-size: 40px;">Exercise 1</h1>
<hr>

<h1 style="font-size: 30px;">Sigmoid neurons simulating perceptrons, part I</h1>

Suppose we take all the weights and biases in a network of perceptrons, and multiply them by a positive constant, $$c>0$$. Show that the behaviour of the network doesn't change.
<hr>
**Solution 1:**

we know perceptron rule can be written as:

$$
\begin{eqnarray}
  \mbox{z} = \left\{
    \begin{array}{ll}
      0 & \mbox{if } w\cdot x + b \leq 0 \\
      1 & \mbox{if } w\cdot x + b > 0
    \end{array}
  \right.
\tag{1}\end{eqnarray}
$$

<br>
where $$z, w, b$$ represents *output*, *weights* and *bias* repectively.

We are asked to see perceptron's behaviour after multiplying weights and biases in a network of perceptrons by $c>0$ which happens to positive constant.

Let's multiply the above equation by $$c$$,

$$
\begin{eqnarray}
  \mbox{z} = \left\{
    \begin{array}{ll}
      0 & \mbox{if } cw\cdot x + cb \leq 0 \\
      1 & \mbox{if } cw\cdot x + cb > 0
    \end{array}
  \right.
\end{eqnarray}
$$

Focusing on condition part:

In both conditions,
<br>

$$
cw \cdot x + cb = 0
$$

And

$$
cw \cdot x + cb > 0
$$

<br>
Using basic algebra $$a(b + c) = ab + ac$$, we can take out common factor constant $$c$$.


$$
c [w \cdot x + b] = 0
$$

$$
c [w \cdot x + b] > 0
$$


Multipling both sides by positive constant $$c$$, doesn't change sign of the equation, it only changes magnitudes and the equation is unchanged.


If you find dot product confusing you can put equation $$1$$ in basic algebraic form.
<hr>
**Solution 1 in basic precise algebraic form:**

$$
\begin{eqnarray}
  \mbox{output} & = & \left\{ \begin{array}{ll}
      0 & \mbox{if } \sum_j w_j x_j + b\leq \mbox{0} \\
      1 & \mbox{if } \sum_j w_j x_j +b > \mbox{0}
      \end{array} \right.
\tag{2}\end{eqnarray}
$$

<br>

Note that above dot product representation is same as current algebraic form:

$$
w \cdot x + b \equiv \sum_j w_j x_j + b
$$


Multiplying by $$c$$,

$$
\begin{eqnarray}
  \mbox{output} & = & \left\{ \begin{array}{ll}
      0 & \mbox{if } \sum_j cw_j x_j + cb\leq \mbox{0} \\
      1 & \mbox{if } \sum_j cw_j x_j + cb > \mbox{0}
      \end{array} \right.
\end{eqnarray}
$$

Factoring out common term $$c$$,

$$
\begin{eqnarray}
  \mbox{output} & = & \left\{ \begin{array}{ll}
      0 & \mbox{if } c[\sum_j w_j x_j + b]\leq \mbox{0} \\
      1 & \mbox{if } c[\sum_j w_j x_j + b] > \mbox{0}
      \end{array} \right.
\end{eqnarray}
$$

<br>
As you can see, dividing each side by the constant $$c$$, we will have the same behavior of the perceptron as represented in equation $$2$$. That means perceptrons is unaffected by multiplying its weights and bias by a postive constant $$c$$ and ultimately the behavior of the entire network of perceptrons doesn't change.

Will post rest solutions soon.

Hope you found it helpful. If you have any doubts or found any mistakes please comment below.
