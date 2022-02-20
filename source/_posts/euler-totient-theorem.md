---
title: Euler's Totient Theorem
date: 2022-02-20 12:21:00
tags: 数学
mathjax: true
---

> 本篇为交互式 Jupyter Notebook 文档，请在 [这里](https://note.stay-curious.win/) 查看完整版。
>

由于叫 欧拉定理 的定理太多所以就用这个名字了。

在开始讲解之前，首先要问这么一个问题：

$3^{2012} \bmod 17$是多少？

看到取模，我们当然要先找找规律：

```python
print([3**exponent%17 for exponent in range(1, 17)])
print([3**exponent%17 for exponent in range(17, 33)])
```

啊哈！3的幂对17取模，结果是循环的。

所以 $2012 = 125 \cdot 16 + 12$，$3^{2012} \equiv 3^{12} \equiv 4 \pmod {17}$.

我们应该再仔细思考一下，为什么是以16个数为一循环？

因为一个数对17取模，得到的结果只可能在 $[0, 16]$ 这个区间上。而如果一个结果是0，那么其他结果全是0，所以只能在 $[1, 16]$ 上。

那无论底数是什么，都是16个数一循环吗？一定会形成循环吗？

首先来看后面这个问题，答案是会。因为一定会有重复，有重复就会出现循环。

$$
3^{x} \equiv 3^{y} \pmod {17} \iff 3^{x+1} \equiv 3^{y+1} \pmod {17}
$$

对于前一个问题，鉴于有重复就会出现循环，一个循环里面不可能有重复。总共只有16个数，根据鸽巢原理，循环的长度一定小于等于16. 问题也等价于：$[1, 16]$ 中的每一个数都会出现吗？

```python
print([2**exponent%17 for exponent in range(1, 17)])
```

看来并不是。那么接下来怎么办呢？

我们不如换一种思路，看看有没有哪个数是一定会出现的。

```python
for base in range(0, 17):
    print(base, [base**exponent%17 for exponent in range(1, 17)])
```

令人惊奇的是，每个数的第16次方对17取余，结果都是1. 也即

$$
a^{16} \equiv 1 \pmod {17}
$$

联想到上面我们证明循环等价于重复的公式：

$$
a^{16} \equiv 1 \pmod {17} \iff a^{16+1} \equiv a \pmod {17}
$$

我们如果可以证明上式右边成立，我们就能证明无论如何第1到第16个数都会形成循环了。

作为严谨证明的大纲，先演示对于一个特殊情况：$a=3$，模数为 7 的证明。

我们先看一个引理：如果我们有正整数 $p$ 并且它不被另一个正整数 $a$ 整除，我们可以写下这样的数列

$$
a, 2a, 3a, \cdots , (p-1)a
$$

我们对这数列的每一项都对 $p$ 取余，就能得到一个从 $1$ 到 $p-1$ 的全排列。也就是说，每个数都会出现一次。

```python
a = 3
p = 7
print([a*i for i in range(1, p)])
print(perm := [a*i%p for i in range(1, p)])
print(set(perm))
```

在这之后，我们会把这两个数列分别乘起来。由于前者只是后者的 $a$ 倍，所以它们模 $p$ 同余。

$$
a \times 2a \times 3a \times \cdots \times (p-1)a \equiv 1 \times 2 \times 3 \times \cdots \times (p-1) \pmod p
$$

化简得到

$$
a^{p-1}(p-1)! \equiv (p-1)! \pmod p
$$

最后，我们会把两边的 $(p-1)!$ “消去”（我知道不能这么直接消，bear with me!）得到

$$
a^{p-1} \equiv 1 \pmod p
$$

```python
lhs = 1
for i in range(1, p):
    lhs *= a*i
rhs = 1
for i in range(1, p):
    rhs *= i
print(lhs, '===', rhs, '(mod ' + str(p) + ') is', lhs%7 == rhs%7)
print('Canceling out (p-1)! gives us:')
print(lhs//rhs, '=== 1 (mod ' + str(p) + ') is', (lhs/rhs)%7 == 1)
```

要完成这个证明，有两个地方需要我们详细说明：

- 引理：如果我们有正整数 $p$ 并且它不被另一个正整数 $a$ 整除，$i$ 为正整数且 $i \leq p-1$ 时，$\{ia\bmod p\} = \{i\}$
- 同余式两边何时能同时消去一个数

我们先看第二个：同余式除法，因为第一个依赖第二个证明。

上面我们已经用了同余式两边同时乘上同余的数，同余式仍然成立的性质。除此之外对于加减法也有效。但是对于除法，就没那么简单了。

首先把同余式写成等式。

$$
ac \equiv bc \pmod m \iff \exists k \in \mathbb{Z}, ac = bc + km
$$

右式两边同时除以 $c$ 得

$$
a = b + \frac{km}{c}
$$

如果 $c \nmid m$ 那么我们还需要换掉整数 $k$ 以使模数为一个整数。

$$
\begin{aligned}
k' &= \frac{k \cdot gcd(m, c)}{c} \\
a &= \frac{k'm}{gcd(m, c)}
\end{aligned}
$$

最后得到

$$
ac \equiv bc \pmod m \iff a \equiv b \ \left(\bmod \frac{m}{gcd(m, c)} \right)
$$

如果我们希望前后模数相等，当且仅当 $gcd(m, c) = 1$ 也即 $m$ 与 $c$ 互质才成立。

回到刚才的这个式子

$$
a^{p-1}(p-1)! \equiv (p-1)! \pmod p
$$

要让两边消掉 $(p-1)!$ 又不改变模数，有且仅有 $(p-1)!$ 与 $p$ 互质，这等价于 $p$ 为一个质数。7 和 17 都满足这个要求。

现在再来看那个引理：如果有正整数 $p$ 并且它不被另一个正整数 $a$ 整除，$i$ 为正整数且 $i \leq p-1$ 时，$\{ia\bmod p\} = \{i\}$.

首先，小于 $p$ 的数 $i$ 与 $p$ 互质，而 $a$ 也与 $p$ 互质，所以这两个数乘起来仍然与 $p$ 互质（欧几里得引理）。所以 $ia \bmod p \in [1, p-1]$. 然后要证明这些数互不相等。运用反证法，假设有两个不相等的数 $x,y < i$ 使得

$$
xa \equiv ya \pmod p
$$

那么由上面推导的同余式除法得

$$
x \equiv y \pmod p
$$

而 $x<i, y<i$ 所以 $x=y$ 与假设矛盾。证毕。

至此，证明全部完成。

由上面的推导，我们得到了费马小定理：

> 对于质数 $p$ 以及任意正整数 $a$ 满足 $p \nmid a$ 有
>
> $$
> a^{p-1} \equiv 1 \pmod p
> $$

如果你足够细心，你也许会注意到我刚才说第二点的时候并没有提到 $p$ 一定是个素数。这让我们不禁想推广刚才得到的成果。我们先来感性的认识一下，当 $p$ 不是素数时是什么样的。因为 $p$ 是 prime 的意思，所以下面换成合数的情况下我们用 $m$ 来代替。

我们先来看看 $m=10$ 的情形：

```python
def extract_repeat(arr):
    for index, value in enumerate(arr[1:]):
        if arr[0] == value:
            return arr[0:index+1]

m = 10
for a in range (1, m):
    print('a =', a, arr := [a**exponent%m for exponent in range(1, m)], extract_repeat(arr))
```

注意到，当 $a$ 与 $m$ 有公因数的时候，循环不一定会出现 1. 这是为什么呢？任意整数 $k$，$km+1$ 这时候都肯定跟 $m$ 互质，因此 $a^{x} \neq km+1$.

有没有整数 $a,x$ 使得

$$
a^x \equiv 1 \pmod m
$$

呢？要找到这个数，我们就得找到一个数列 $T$，使其满足我们上面的两点要求

- 对每个数乘以 $a$ 再 $\bmod \ m$ 得到的数列是 $T$ 的全排列
- 把 $T$ 中的数全乘起来，得到的数与 $m$ 互质（可以从同余式两边消去）

在 $m = p$ 的情况下，我们已经看到了 $T=\{1,2,3,\cdots,p-1\}$. 现在考虑的是 $m$ 不为质数的情况。

先看第一点。需要 $T$ 中的数 $t_i$ 都与 $m$ 互质，$a$ 与 $m$ 互质，以及 $t_ia \bmod m \in T \implies T$ 是比 $m$ 小且与 $m$ 互质的数的集合。

再看第二点，由 $T$ 是与 $m$ 互质的数的集合，$T$ 中的数全乘起来，得到的数与 $m$ 互质，满足条件。

下面开始外层证明。令 $r$ 为 $T$ 中所有数的乘积，即 $r = \prod t_i$. $\phi(m)$ 为 $m$ 对应的数组 $T$ 中的元素个数。

$$
\begin{aligned}
at_1 \times at_2 \times \cdots \times at_n &\equiv t_1 \times t_2 \times \cdots \times t_n \pmod m \\
a^{\phi(m)} r &\equiv r \pmod m \\
a^{\phi(m)} &\equiv 1 \pmod m
\end{aligned}
$$

```python
import math
def phi(m):
    res = []
    for k in range(1, m+1):
        if math.gcd(k, m) == 1:
            res.append(k)
    return res

def prod(arr):
    res = 1
    for t in arr:
        res *= t
    return res
    
a = 3
m = 10
T = phi(m)
r = prod(T)

print(prod([a*t for t in T]), '===', r, '(mod ' + str(m) + ') is', prod([a*t for t in T])%m == r%m)
print(a**len(T)*r, '===', r, '(mod ' + str(m) + ') is', a**len(T)*r%m == r%m)
print(a**len(T) , '=== 1', '(mod ' + str(m) + ') is', a**len(T)%m == 1%m)
```

这就证明了欧拉定理（数论）：

> $m$ 和 $a$ 是互质的正整数，$\phi(m)$ 为小于等于 $n$ 的正整数中与 $n$ 互质的数的数目（欧拉函数），有
>
> $$
> a^{\phi(m)} \equiv 1 \pmod m
> $$

参考资料：

1. [Euler’s Totient Theorem, Misha Lavrov[PDF]](https://www.math.cmu.edu/~mlavrov/arml/12-13/number-theory-11-11-12.pdf)
2. [Proofs of Fermat's little theorem, Wikipedia](https://en.wikipedia.org/wiki/Proofs_of_Fermat%27s_little_theorem#Proof_as_a_particular_case_of_Euler's_theorem)