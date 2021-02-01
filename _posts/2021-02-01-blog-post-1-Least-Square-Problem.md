---
title: 'Least-Square-Problem'
date: 2021-02-01
permalink: /posts/2021/02/Least-Square-Problem/
tags:
  - Machine Learning
  - Linear Algebra
  - Numerical Analysis
---



Least-Square-Problem
======

### Below is a flow of thinking to understanding the LS problem.

**1. Why do we need to learn least square problem?**: 

Because while Ax=b is a very common problem, most of the time it doesn’t have a solution. So the motivation is to find a x which can best approximate the Ax to b.


**2. How do we measure the degree of being approximate??**:

The “distance” between Ax and b, which is calculated by Residual = |b-Ax| (didn’t know it’s just that straightforward, conceptually we can treat them like scalars). Noted that Residual != Error, where Error is how much the coefficient Ai are off by. 


**3. Then, how do we compute |b-Ax|?**:

1. Algebraically, it equals to the square root of sum of squares.
2. Geometrically, we need to have the intuition of thinking Ax as a “plane” spanned by the columns of A. In another word, Ax is in the column space Col A. 
	1. Then |b-Ax| will be the “distance” between a random vector b and another vector Ax, a point within the plane ran(A). 
	2. The distance will be minimized when it’s the projection. That is, Ax’ – b is orthogonal to plane ran(A). 
	3. Because Ax’-b is orthogonal to Col space of A, each column is a basis in the plane, so Ax’-b is orthogonal to each of the column aj. i.e. aj dot (b - Ax-hat) = 0
	4. Since aj dot (b - Ax-hat) = 0, ajT (b – Ax-hat) = 0 --- a conversion from dot product to cross product using transpose. (This part, I didn’t know before)
	5. Because ajT (b – Ax-hat) = 0 for all ajT, entire matrix AT will have AT(b-Ax-hat)=0. Which is totally fine with distributive law.
	6. So, in order to solve Ax = b, we just need to solve: __ATAx = ATb__, where that system of equations is called the __normal equations__ for Ax=b. And it will reduce the number of equations from the previous __overdetermined problem__, making it easier to solve. 

**4. What’s the flaw of this way of solution?**:

Not being very accurate, since ATA is ill-condition matrix. (why?)

**5. What’s a better solution? And how to understand it?**:

QR factorization and Reduced QR factorization are better for LS problem. The concept is to decompose A to Q and R, where Q is an orthogonal matrix, i.e. QTQ=I, and R is an upper triangular matrix.

**6. What are the steps?**:

1. b = Ax 
2. b = QRx
3. b = QRx
4. bQT = Rx
5. bQT is known, R is known --- we get x

------
