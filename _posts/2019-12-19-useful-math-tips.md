---
layout: post
title:  "Useful mathematic tips"
author: mohamed-ali
image: assets/images/geometry-1023846_1280.jpg
categories: [ methematics, tips ]
featured: false
hidden: false
published: true

---

Given a dataset $$ \mathcal{D} = \{ x_i \in \mathbb{R} \mid i \in 1..n \} $$
, the mean $$ \bar{x} $$ of $$ \mathcal{D} $$ is defined as:
 
 $$ \bar{x}_{n} = \frac{1}{n} \sum_{i=1}^{n}{x_i} $$
 
Imagine you need to compute the mean of a continuous stream of data, the mean formule defined above can be re-aranged to find a relationship between the average at $$ i = n $$ and  $$ i = n - 1 $$, a.k.a the previous average.

To find the relationship, let's rewrite the mean forumle for $$ n-1 $$

 $$ \bar{x}_{n-1} = \frac{1}{n-1} \sum_{i=1}^{n-1}{x_i} $$ (1)
 
We can also re-write the mean formule where $$ i \in 1..n $$ as follows: 

 $$ \bar{x}_{n} = \frac{1}{n} \sum_{i=1}^{n-1}{x_i} + \frac{x_n}{n}$$ (2)
 
So, given the two equations (1) and (2), we get the following relationship:

$$ \bar{x}_{n} = \frac{n-1}{n} \bar{x}_{n-1} + \frac{x_n}{n}  $$

From this formule, we can get the current mean in a continuous stream by a keeping a counter of the number of elements received so far (until the previous step) and the sum of all element until the previous step. Then we plug in these counters and sums with the current element value to get the current mean. 

<hr />

When $$ a \ne 0 $$, there are two solutions to $$ ax^2 + bx + c = 0 $$ and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

<hr />

Stirling’s approximation for the factorial function:  $$ x! \simeq x^x \, e^{−x} $$
