---
title: "Grothendieck's Inequality and Constant "
date: 2019-09-19T09:04:59-04:00
categories: ["mathematics"]
tags:
- Grothendieck
- inequality
- constant
math: true

draft: false
---

Yesterday in the [High Dimensional Probability](https://www.math.uci.edu/~rvershyn/papers/HDP-book/HDP-book.html) class, I encountered the proof of Grothendieck's inequality which relates the solution of an Integer Linear Programming (ILP) and its corresponding real Linear Programming (LP). 
<!--more-->
The inequality states that

> ***Grothendieck's Inequality*** There exists a finite constant \\(K>0\\) such that for every \\(l,m,n\in \mathbb N\\) and every matrix \\(M=(M\_{ij})\in \mathbb F^{m\times n}\\) (where \\(\mathbb F\\) can be \\(\mathbb R\\) or \\(\mathbb C\\)),
\\[ \max\limits\_{\\|x\_i\\|=\\|y\_j\\|=1  } \left|\sum\limits\_{i=1}^m\sum\limits\_{j=1}^n M\_{ij}\langle x\_i,y\_j\rangle\right| \le K\max\limits\_{|\varepsilon\_i|=|\delta\_j|=1}    \left|\sum\limits\_{i=1}^m\sum\limits\_{j=1}^n M\_{ij}\varepsilon\_i \delta\_j\right| \\]
where the inner product is taken in \\(\mathbb F^l\\).

The smallest constant \\(K\_G\\) that satisfies the inequality is called the _Grothendieck's constant_. From the (beautiful) proof of [Krivine](https://arxiv.org/abs/1711.10595), \\(K\_G\le \frac{\pi}{ 2\ln(1+\sqrt{2}) }\\). What is more surprising is that this is [not the sharpest constant](https://web.math.princeton.edu/~naor/homepage%20files/GroKri.pdf), even though proof uses a very sharp argument (which is often referred to as *kernel trick* in machine learning).
