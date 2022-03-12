---
title: 常见 Wrong Answer 原因集锦
date: 2021-12-01 09:11:00 +08:00
tags: 算法
mathjax: true
---

## 变量运算过程中溢出

> Codeforces [#137522685](https://codeforces.com/contest/1609/submission/137522685)
>
> Diagnostics detected issues [cpp.clang++-diagnose]: p71.cpp:66:40: runtime error: signed integer overflow: 99999 * 100000 cannot be represented in type 'int'

尽管指定运算结果会被赋值/加到一个较大的数据类型（比如 long long），运算过程中仍然会有精度问题。

解决方案：保证所有运算中变量数据类型一致。

## `std::cout` 输出浮点数精度问题

`std::cout << std::cout.precision();` 默认输出为 6. 即最多输出小数点后 6 位。

解决方案：

- `std::cout << std::setprecision(int n)`
- `printf("pi = %.5f", 4*atan(1.0));`

## 负数取余取模问题

在数学上模运算一般是根据欧几里得除法（带余除法）定义的：

对于任意整数 $a$, $b$ $(b\neq 0)$ 存在唯一的整数 $q$ 和 $r$ 使得 $0 \leq r < |b|$ 且

$$
a = bq + r
$$

则 $r = a \bmod b$. 

注意，这里规定了 $r \geq 0$.

对于 $a \geq 0, b > 0$ 的情况，一切正常。

但是如果 $a < 0$ 问题就出现了：

$$
\begin{align*}
-5 &= 3 \cdot (-1) + (-2) \\
-5 &= 3 \cdot (-2) + 1
\end{align*}
$$

按照上面的定义 $-5 \bmod 3 = 1$，但是在 C++ 中结果是 $-2$.

为什么？这是因为 C++ 的 `%` 运算符是取余而非取模。

```cpp
int remainder(int a, int b) {
    return a - (a / b) * b;
}
```

换句话说，C99 标准要求，`a == b * (a / b) + a % b`. 也即 `q = a / b`，`r = a % b`.

$-5/3 = -1.\dot{6}$，按照 C++ 的标准去掉小数部分即为 $-1$. 这就是问题所在：C++ 中的商取整永远都是朝着 0 取。

再来看几个例子：

$$
\begin{align*}
-5 &= (-3) \cdot 1 + (-2)\\
-5 &= (-3) \cdot 2 + 1
\end{align*}
$$

而 C++ 中 `-5 / -3 = 1` 所以 `-5 % -3 = -2`. 如果商取整朝着负无穷取的话，那么结果的正负号和除数一致。

$$
\begin{align*}
5 &= (-3) \cdot (-1) + 2\\
5 &= (-3) \cdot (-2) - 1
\end{align*}
$$

此时 `%` 运算符和取模匹配。

据此我们可以归纳得出，C++ 中的 `%` 运算符结果正负号与被除数一致。当被除数大于等于 0 的情况下，`%` 运算符和取模结果一致。否则需要在结果上加上除数。

```cpp
int mod(int a, int b) {
    int r = a % b;
    return r < 0 ? r + b : r;
}
```

最后来看看 Python:

```
>>> -5 % 3
1
>>> -5 % -3
-2
>>> 5 % -3
-1
```

显然 Python 中商取整都是朝着负无穷取。

```
>>> -5 // 3
-2
>>> -5 // -3
1
>>> 5 // -3
-2
```
