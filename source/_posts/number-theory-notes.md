---
title: Number theory notes
date: 2022-03-10 11:34:00
tags: Math
mathjax: true
---

## Euclidean

[Modular arithmetic](https://en.wikipedia.org/wiki/Modular_arithmetic) is congruence, meaning that it is an [equivalence relation](https://en.wikipedia.org/wiki/Equivalence_relation "Equivalence relation") that is compatible with the operations of addition, subtraction, and multiplication.

$$
\left.
\begin{array}{ll}
a\equiv b \pmod {n}\\
c\equiv d \pmod {n}
\end{array}
\right\} \implies a-c \equiv b-d \pmod {n}
$$

The Euclidean algorithm just flows out:

$$
\left.
\begin{array}{ll}
a \equiv 0 \pmod {d}\\
b \equiv 0 \pmod {d}
\end{array}
\right\} \implies a-kb \equiv 0 \pmod {d}
$$

For all $d \in \mathbb{N}^+$, $k \in \mathbb{Z}$, if $d \mid a$ ($d$ is a divisor of $a$), $d \mid b$ ($d$ is a divisor of $b$) and $a \geq b$ then $d \mid a-kb$. Thus we see that $gcd(a,b)=gcd(b, a \bmod b)$.

To describe and proof the algorithm, we can define an array $r$ such that $r_0=a$ and $r_1=b$, while

$$
r_{j}=r_{j-2} \bmod r_{j-1}
$$

It basically means

$$
r_{j-2} = r_{j-1}q_{j-1} + r_{j}
$$

where $q_{j-1}= [r_{j-2} / r_{j-1}]$ stands for quotient. When hit $r_{n-1} \bmod r_n = 0$, we stop. Thus $r_{n+1}=0$.

Therefore

$$
\begin{gather*}
gcd(r_j, r_{j+1})=gcd(r_{j+1}, r_{j+2})\\
r_n= gcd(r_n, 0) = \cdots = gcd(r_0, r_1)
\end{gather*}
$$

Let $g=gcd(a,b)$, notice that

$$
\begin{align*}
g=gcd(r_n,0) &= 1\times r_n + 0\times r_{n+1}=r_n\\
&=r_{n-2}-q_{n-1}r_{n-1}\\
&=r_{n-2}-q_{n-1}(r_{n-3}-r_{n-2}q_{n-2})\\
&=q_{n-1}r_{n-3}+(1+q_{n-2}q_{n-1})r_{n-2}\\
&=\cdots
\end{align*}
$$

We may wonder if there exists a linear combination such that $g=ax+by$. In fact, this is what Bezout's theorem says.

**Proof** by induction.

*Base case:*

$$
g= 1\times r_n + 0\times r_{n+1}
$$

*Induction step:*

Given that $r_{j+1}=r_{j-1}-r_{j}q_{j}$

$$
\begin{align*}
g&=r_{j}x_{j}+r_{j+1}y_{j}\\
&=r_{j}x_{j}+(r_{j-1}-r_{j}q_{j})y_{j}\\
&=r_{j-1}y_{j}+r_{j}(x_{j}-q_{j}y_{j})
\end{align*}
$$

So $x_{j-1}=y_{j}, y_{j-1}=x_j-q_jy_j$.

Finally,

$$
g=r_0x_0+r_1y_0=ax_0+by_0
$$

This also provides us an algorithm to produce a linear combination.

```python
def exgcd(a, b):
    if b == 0:
        return (1, 0)
    else:
        x, y = exgcd(b, a % b)
        return (y, x-(a//b)*y)


x, y = exgcd(10319, 2312)
print('x =', x, ', y =', y, ', gcd =', a*x+b*y)
```

References:

- [The Euclidean Algorithm](http://gauss.math.luc.edu/greicius/Math201/Fall2012/Lectures/euclidean-algorithm.article.pdf)

## Linear Congruences

Suppose you want to solve

$$
ax \equiv c \pmod b
$$

and you need to find the minimum integer $x$.

First we can translate it to a normal equation.

$$
ax \equiv c \pmod b \iff ax - c = by
$$

