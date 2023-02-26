---
layout: post
title: Counting and multiplying
tags: pseudocode algorithms maths
---

How does one count? It interests me that something seemingly so simple as counting, which we do by rote memorary, really demands some thinking about to understand how it works just so it can run on a computer. But I have this - remembering the four properties of an algorithm i.e. 

1. _Unique initialisation_
2. _Unique succession_
3. _Finiteness_
4. _Solution_

here is how to count in pseudocode!
<br>
<br>

<embed src="/assets/images/count.svg" width="70%" height="70%" />

<br>
Now, supringsly, I find it easier and shorter to write an algorithm for multiplication. Bearing in mind, computers pretend to multiply by still adding numbers, but just in loops à la below.
<br>
<br>
<embed src="/assets/images/times.svg" width="70%" height="70%" />
<br>
<br>
Here is a trace of the TIMES alogrithm of the values _prod_ and _u_ everytime it enters the **_repeat...endrepeat_** construct:


| _prod_   | 0 | 13 | 26 | 39 | 52  | 65  |
| _u_      | 0 | 1 | 2 | 3   | 4   | 5   |

The notion here is that the algorithm multiplies x = 5 by y =13. 