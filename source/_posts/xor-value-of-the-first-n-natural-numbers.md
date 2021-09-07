---
title: 求前 n 个自然数的异或值
date: 2021-09-07 21:01:00
tags: ['算法','数学']
mathjax: true
---

时间复杂度 $O(1)$ ，分为感性认识和理性认识。

如无特别注明，下文所指均为二进制下的数位。按位逻辑运算符号表在[此处](https://imzlp.com/posts/23224/#%E9%80%BB%E8%BE%91%E8%BF%90%E7%AE%97)。

## 感性认识

由于 $0\oplus 1=1$，问题也可以转化成求 $[1, n]$ 的异或值。

```
Number Binary-Repr  XOR-from-1-to-n
1         1           [0001] 1
2        10           [0011] 3
3        11           [0000] 0  <----- We get a 0
4       100           [0100] 4  <----- Equals to n
5       101           [0001] 1
6       110           [0111] 7
7       111           [0000] 0  <----- We get 0
8      1000           [1000] 8  <----- Equals to n
9      1001           [0001] 1
10     1010           [1011] 11
11     1011           [0000] 0  <------ We get 0
12     1100           [1100] 12 <------ Equals to n
```

所以我们可以这么写：

```c++
// C++ program to find XOR of numbers
// from 1 to n.
#include<bits/stdc++.h>
using namespace std;
 
// Method to calculate xor
int computeXOR(int n)
{
   
  // If n is a multiple of 4
  if (n % 4 == 0)
    return n;
 
  // If n%4 gives remainder 1
  if (n % 4 == 1)
    return 1;
 
  // If n%4 gives remainder 2
  if (n % 4 == 2)
    return n + 1;
 
  // If n%4 gives remainder 3
  return 0;
}
 
// Driver method
int main()
{
  int n = 5;
  cout<<computeXOR(n);
}
 
 
// This code is contributed by rutvik_56.

```

## 理性认识

记 $f(x,\ y)$ 为 $x$ 到 $y$ 的所有整数的异或值。

现在考虑 $f(2^k,\ 2^{k+1}-1)$. 令 $k\geq 1$，则 $2^k$ 为偶数。且这里面的 $2^k$ 个数从左往右第 $k+1$ 位（最高位）都为 $1$. 再结合异或运算法则我们就知道，将这 $2^k$ 个数的最高位去掉，异或值不变。也就是说，
$$
f(2^k,\ 2^{k+1} -1) = f(2^k - 2^k,\ 2^{k+1} -1 -2^k) = f(0,\ 2^k -1).
$$
所以，
$$
\begin{aligned}
f(0,\ 2^{k+1} -1)&=f(0,\ 2^k -1)\oplus f(2^k,\ 2^{k+1} -1)\\
&=f(0,\ 2^k -1)\oplus f(0,\ 2^k -1)\\
&=0.
\end{aligned}
$$
也就是，
$$
f(0,\ 2^k - 1) = 0\ (k >= 2).
$$

对于 $f(0,\ n)\ (n\geq 4)$ ，设 $n$ 的最高位在第 $k$ 位 $(k \geq 2)$. 则
$$
f(0,\ n) = f(0,\ 2^k - 1)\oplus f(2^k,\ n) = f(2^k,\ n).
$$
$[2^k,\ n]$ 共有 $n+1-2^k$ 个数，设为 $m$. 这些数的第 $k$ 位（最高位）共有 $m$ 个 $1$.

**(a)** 当 $n$ 为奇数时，$m$ 为偶数，则最高位有偶数个 $1$ ，所以
$$
f(0,\ n) = f(2^k,\ n) = f(0,\ n - 2^k).
$$
且 $n-2^k$ 与 $n$ 同奇偶，我们可以递推：
$$
f(0,\ n) = f(0,\ n - 2^k) = f(0,\ n - 2^k - 2^{k-1}) = \cdots = f(0,\ n \bmod 4).
$$
注：$n\geq4$. 每一步递推都将最高位去掉。

当 $n \bmod 4= 1$ 时， $f(0,\ n) = f(0,\ 1) = 1$.

当 $n \bmod 4 = 3$ 时， $f(0,\ n) = f(0,\ 3) = 0$.

**(b)** 当 $n$ 为偶数时，$m$ 为奇数，则最高位有奇数个 $1$ ，所以
$$
f(0,\ n) = f(2^k,\ n) = f(0,\ n - 2^k) \vee 2^k.
$$
注：最高位的 $1$ 我们先提出来，最后用取或（$\vee$）加回去。

像**(a)**那样递推时，我们会发现每一步都保留了当前最高位，所以除了 $n$ 的最后两位其余都会被保留下来，我们记这个数为 $n'$.
$$
f(0,\ n) = f(2^k,\ n) = f(0,\ n \bmod 4) \vee n'.
$$

当 $n \bmod 4=0$ 时 $n$ 的后两位是 $00$，所以 $n=n'$.
$$
f(0,\ n) = f(0,\ n \bmod 4) \vee n' = f(0,\ 0) \vee n = n.
$$
当 $n \bmod 4 = 2$ 时 $n=n'+2$，所以
$$
\begin{aligned}
f(0,\ n) &= f(0,\ n \bmod 4) \vee n'\\
&=f(0,\ 2) \vee n'\\
&=3 \vee n'\\
&=3 \vee 2 \vee n\\
&=n+1.
\end{aligned}
$$
综上所述，
$$
f\left( 0,\ n\right) =\left\{
\begin{array}{l}
n&, n \bmod 4=0\\
1&, n \bmod 4=1\\
n+1&, n \bmod 4=2\\
0&, n \bmod 4=3.
\end{array}
\right.
$$
Q.E.D.

## 参考文献

1. [求1到n这n个整数间的异或值 （O(1)算法)](https://www.cnblogs.com/flyinghearts/archive/2011/03/22/1992001.html)
2. [Calculate XOR from 1 to n - GeeksforGeeks](https://www.geeksforgeeks.org/calculate-xor-1-n/) （异或值表格及代码）
3. [问题：求1到n这n个整数间的异或值，即 1 xor 2 xor 3 … xor n](https://siukwan.sinaapp.com/?p=883)
