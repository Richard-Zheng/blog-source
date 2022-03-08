# Elegant Pieces of Algorithm

## Number Theory

### Euclidean

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
\right\} \implies a-b \equiv 0 \pmod {d}
$$

For all $d \in \mathbb{N}^+$, if $d \mid a$, $d \mid b$ and $a \geq b$ then $d \mid a-b$. Thus we see that $gcd(a,b)=gcd(b, a-b)$.

### ExGCD

Suppose you want to solve

$$
ax \equiv c \pmod b
$$

and you need to find the minimum integer $x$.

First we can translate it to a normal equation.

$$
ax \equiv c \pmod b \iff ax - c = by
$$

Then we will compute this by induction.

Base case:

$$
a \times 1 + 0 \times 0 = a = gcd(a,0)
$$