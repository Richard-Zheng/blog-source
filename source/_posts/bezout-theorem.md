---
title: Bezout 定理
date: 2022-03-26 23:00:00 +08:00
tags: 算法
mathjax: true
---

简单起见，我们把两个整数 $a$，$b$ 的最大公因数记为 $(a,b)$.

## Euclidean algorithm

**Theorem 1** 若存在整数 $k$ 使得 $a=r+bk$，则 $(a,b)=(b,r)$.

*Proof.* 由 $r=a-bk$ 得：$a$ 和 $b$ 的公因数都是 $r$ 的因数，也就是 $b$ 和 $r$ 的公因数。所以 $(a,b) \leq (b,r)$. 由 $a=r+bk$ 同理可得 $(b,r) \leq (a,b)$. 因此，$(a,b)=(b,r)$. 证毕。

据此我们可以构造一个数列 $r$，令 $r_{1}=a, r_{2}=b$，并且

$$
r_{i}=r_{i-2} \bmod r_{i-1},\;\;\; 0\leq r_{i} < |r_{i-1}|.
$$

不失一般性，我们假设 $a \geq b \geq 0$，那么 $r$ 是单调递减的。所以数列最后一定会出现 $0$，但是 $0$ 不能作为除数，所以我们规定数列在 $0$ 截止，且 $r_{n+1}=0$（也即 $0$ 的前一个数是数列末尾）。

现在要证明

$$
(r_{1}, r_{2})=(r_{2}, r_{3})=\cdots=(r_{n},r_{n+1})=r_{n}.
$$

由数列的定义得

$$
r_{i-2}=r_{i}+r_{i-1}q_{i-1}.
$$

其中 $q_{i-1}$ 为带余除法 $r_{i-2}/r_{i-1}$ 得到的商。应用上面提到的定理得 $(r_{i-1}, r_{i})=(r_{i-2}, r_{i-1})$. 若 $i=n+1$，则我们可以一路递推至 $i=2$ 的情况，也即 $(a,b)$. 由于 $r_{n+1}=0$，任何数都是零的因数，所以 $(r_{n},r_{n+1})=r_{n}$. 证毕。

这也为我们提供了一种计算最大公因数的高效算法。

## Bézout's Identity

**Theorem 2** 对于任意非零整数 $a$,$b$，存在整数 $x$ 和 $y$ 使得

$$
(a,b)=ax+by.
$$

特别地，当 $a$ 与 $b$ 互质时，存在整数 $x$ 和 $y$ 使得 $ax+by=1$

*Proof.* 使用数学归纳法证明。

下面证明

$$
\forall i \leq n,\,\exists x,y \in \mathbb{Z},\,(r_{i}, r_{i+1})=r_{i}x+r_{i+1}y.
$$

初始条件：由 $r_{n+1}=0$ 有

$$
(r_{n}, r_{n+1})=r_{n} \cdot 1 + r_{n+1} \cdot 0.
$$

即 $x=1,\ y=0$（$y$ 是不是只能为 $0$？）

递推：假设已存在 $x,y \in \mathbb{Z}$ 使得 $(r_{i}, r_{i+1})=r_{i}x+r_{i+1}y$，现在来证存在 $x',y' \in \mathbb{Z}$ 使得 $(r_{i-1}, r_{i})=r_{i-1}x'+r_{i}y'$.

由数列的定义得

$$
r_{i-1}=r_{i+1}+r_{i}q_{i}.
$$

也即

$$
r_{i+1}=r_{i-1}-r_{i}q_{i}.
$$

代入递推假设得

$$
\begin{align*}
(r_{i}, r_{i+1})&=r_{i}x+r_{i+1}y\\
&=r_{i}x+(r_{i-1}-r_{i}q_{i})y\\
&=r_{i-1}y+r_{i}(x-q_{i}y).
\end{align*}
$$

又由定理 1 得 $(r_{i}, r_{i+1})=(r_{i-1}, r_{i})$（上面已经证明），所以

$$
(r_{i-1}, r_{i})=r_{i-1}y+r_{i}(x-q_{i}y).
$$

且 $y$ 和 $x-q_{i}y$ 都为整数，所以 $x'=y, y'=x-q_{i}y$. 递推证明完成。

结论：当 $i=1$ 时我们得到存在整数 $x,y$ 使得 $(r_{1}, r_{2})=r_{1}x+r_{2}y$ 即 $(a,b)=ax+by$. 证毕。

利用上面的递推过程我们得到了 extended Euclidean algorithm. 它可以计算出 $(a,b)=ax+by$ 的一组整数解。

下面是一个可能注释比上面的证明好理解得多的 Python 代码实现（？）。

```python
def exgcd(a, b):
    if b == 0:
        return (1, 0)
    m, n = exgcd(b, a%b)
    # recursion invariant: b * m + (a%b) * n == gcd(b, a%b) == gcd(a, b)
    # let a = b * q + a%b
    # then b * m + (a - b * q) * n == gcd(a, b)
    # thus a * n + b * (m - n * q) == gcd(a, b)
    q = a // b
    return (n, m - n * q)


x, y = exgcd(10319, 2312)
print('x =', x, ', y =', y, ', gcd =', a*x+b*y)
```
