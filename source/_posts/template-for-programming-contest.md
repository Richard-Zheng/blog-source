---
title: 算法竞赛常用模板
date: 2021-11-26 19:44:00 +08:00
tags: 算法
mathjax: true
---

## 对拍脚本

Win32 Command Prompt

```bat
@echo off
:loop
python a.py < stdin.txt > myout.txt
fc stdout.txt myout.txt
if not errorlevel 1 echo ok
::choice /t 1 /d y /n >nul
pause
cls
goto :loop
```

## 基础算法

### 快速幂

```c++
typedef long long ll;
ll quick_pow(ll base, ll exp) {
    int result = 1;
    while (exp) {
        if (exp & 1) {
            result *= base;
        }
        exp >>= 1;
        base *= base;
    }
    return result;
}
```

### 二分查找

给定长度为n的数组（$n\geq 1$）

问题1：找到值为value的元素的下标

```c++
int BinarySearch(int array[], int n, int value) {
    int left = 0;
    int right = n - 1;
    while (left <= right) {
        // 注意防止溢出
        int middle = left + ((right - left) >> 1);
        if (array[middle] > value) {
            right = middle - 1;
        } else if (array[middle] < value) {
            left = middle + 1;
        } else {
            return middle;
        }
    }
    return -1;
}
```

问题2：找到**第一个**值为value的元素的下标

这时候遇到相等也不能直接返回，只能排除掉右侧的所有数。

数组的长度为 1 或 2 时，`middle`为 0. 若`array[0]`为要找的数，则`right`将被赋值为 -1，循环结束，`left`为答案。数组长度为 2 且`array[1]`为要找的数时，`left`将被赋值为 1，回到数组长度为 1 的情况。

因此最后再判断一下`left`是否为要找的数，如果是则返回，否则答案不存在。

```c++
int BinarySearch(int array[], int n, int value) {
    int left = 0;
    int right = n - 1;

    while (left <= right) {
        int middle = left + ((right - left) >> 1);

        if (array[middle] >= value) {
            right = middle - 1;
        } else {
            left = middle + 1;
        }
    }

    if (left < n && array[left] == value) {
        return left;
    }
    return -1;
}
```

问题3：找到**最后一个**值为value的元素的下标

这就是问题2的倒序版本。改动两个地方即可

1. `if (array[middle] >= value)` 中的等号去掉；

2. `if (right >= 0 && array[right] == value) {return right;}`

问题4：找到**第一个大于等于**value的下标

在问题2中，我们的策略是让`left`刚好为第一个大于等于value的数的下标，而让`right`刚好为第一个小于value的数的下标。因此只需要去掉最后判断答案存在的`array[left] == value`条件即可。

问题5：找到**最后一个小于等于**value的下标

与问题4同理，去掉问题3中最后判断答案存在的`array[right] == value`条件。

## 数论

### 欧拉筛

```c++
bool is_prime[MAXN];
int prime[MAXN];
int sieve(int n) {
    memset(is_prime, 1, sizeof(is_prime));
    is_prime[1] = 0;
    int cnt = 0;
    for (int i = 2; i <= n; i++) {
        if (is_prime[i]) {
            prime[++cnt] = i;
        }
        for (int j = 1; j <= cnt && i * prime[j] <= n; j++) {
            is_prime[i * prime[j]] = 0;
            if (i % prime[j] == 0) {
                break;
            }
        }
    }
    return cnt;
}
```

### 辗转相除法求最大公因数（Greatest Common Divisor）

最大公因数的算法是辗转相除法，基于一个原理：如果$a>b$则$gcd(a,b)=gcd(b,a-b)$. 

如果$a-b>b$，那么就继续相减到$a-b<b$为止，所以直接$gcd(a,b)=gcd(b,a\bmod b)$.

代码：

```c++
int gcd(int a, int b) {
    int tmp;
    while (b != 0) {
        tmp = a;
        a = b;
        b = tmp % b;
    }
    return a;
}
```

### 最小公倍数（Least Common Multiple）

两个数的最大公因数（Greatest Common Divisor）就是它们质因数的**交集**的乘积

考虑最小公倍数的性质。最小公倍数必须被$a$或$b$整除，也就是说最小公倍数必须同时包含这两数的所有质因数，所以是它们质因数的**并集**的乘积。怎样得到这个乘积？$a\times b$，然后容斥除掉共同的质因数$gcd(a,b)$就好了。
$$
lcm(a,b)=\dfrac{a\times b}{gcd(a,b)}
$$
实际编程中一般先除后乘，防止溢出。

代码：

```c++
int lcm(int a, int b) {
    return a / gcd(a, b) * b;
}
```

### 裴蜀定理

裴蜀定理，又称贝祖定理（Bézout's lemma）。是一个关于最大公约数的定理。

其内容是：

设 $a,b$ 是不全为零的整数，则存在整数 $x,y$, 使得 $ax+by=\gcd(a,b)$.

#### 证明：

```c++
int gcd(int a, int b) {
    return b ? gcd(b, a%b) : a;
}
```

在函数返回之前，存在 $b=0$ . 这时显然有 $x=1,y=0$ 使得

$$
a\cdot 1+0\cdot 0=gcd(a,0)
$$

0 和任何数的最大公约数都等于原数。

当$b>0$时，有$gcd(a,b)=gcd(b,a\bmod b)$. 假设存在$x,y$使得

$$
bx+(a\bmod b)y=gcd(b,a\bmod b)
$$

且

$$
a\bmod b=a-b\cdot \left\lfloor \dfrac{a}{b} \right\rfloor
$$

所以

$$
\begin{aligned}
bx+(a\bmod b)y&=bx+\left(a-b\cdot \left\lfloor \dfrac{a}{b} \right\rfloor\right)y\\
&=ay-b\left(x-\left\lfloor \dfrac{a}{b} \right\rfloor y\right )
\end{aligned}
$$

令 $x'=y,\ y'=x-\left\lfloor \dfrac{a}{b} \right\rfloor y$ ，可得

$$
ax'+by'=gcd(a,b)
$$

用归纳法即可得证。

参考：https://www.cnblogs.com/fusiwei/p/11775503.html

### 扩展欧几里得

为什么叫它扩展欧几里得呢？因为它就是在欧几里得算法（辗转相除法）求得 $gcd(a,b)$ 的基础上，像上面裴蜀定理的证明那样倒着回溯找了一组 $x,y$ 满足

$$
ax+by=gcd(a,b)
$$

具体代码请看下面的线性同余方程。

### 线性同余方程（线性丢番图方程）

形如 $ax\equiv c\pmod b$ 的方程被称为线性同余方程 (Congruence Equation)。

#### 求解方法

根据以下两个定理，我们可以求出同余方程 $ax \equiv c \pmod b$ 的解。

**定理 1**：方程 $ax+by=c$ 与方程 $ax \equiv c \pmod b$ 是等价的，有整数解的充要条件为 $\gcd(a,b) \mid c$ 。

根据定理 1，方程 $ax+by=c$，我们可以先用扩展欧几里得算法求出一组 $x_0,y_0$ ，也就是 $ax_0+by_0=\gcd(a,b)$ ，然后两边同时除以 $\gcd(a,b)$ ，再乘 $c$ 。然后就得到了方程 $a\dfrac{c}{\gcd(a,b)}x_0+b\dfrac{c}{\gcd(a,b)}y_0=c$ ，然后我们就找到了方程的一个解。

**定理 2**：若 $\gcd(a,b)=1$ ，且 $x_0$、$y_0$ 为方程 $ax+by=c$ 的一组解，则该方程的任意解可表示为：$x=x_0+bt$ ，$y=y_0-at$ , 且对任意整数 $t$ 都成立。

根据定理 2，可以求出方程的所有解。但在实际问题中，我们往往被要求求出一个最小整数解，也就是一个特解 $x=(x \bmod t+t) \bmod t$，其中 $t=\dfrac{b}{\gcd(a,b)}$。

```c++
int ex_gcd(int a, int b, int& x, int& y) {
  if (b == 0) {
    x = 1;
    y = 0;
    return a;
  }
  int d = ex_gcd(b, a % b, x, y);
  int temp = x;
  x = y;
  y = temp - a / b * y;
  return d;
}
bool liEu(int a, int b, int c, int& x, int& y) {
  int d = ex_gcd(a, b, x, y);
  if (c % d != 0) return 0;
  int k = c / d;
  x *= k;
  y *= k;
  return 1;
}
```

### Python 版

```python
def exgcd(a, b):
    if b == 0:
        return (1, 0)
    m, n = exgcd(b, a%b)
    # recursion invariant: b * m + (a%b) * n == gcd(b,a%b) == gcd(a,b)
    # let a = b * q + a%b
    # then b * m + (a - b * q) * n == gcd(a,b)
    # thus a * n + b * (m - n * q) == gcd(a,b)
    q = a // b
    return (n, m - n * q)

def CRT(a, r):
    n = reduce(lambda x, y: x*y, r)
    ans = 0
    for i in range(len(a)):
        m = n / r[i]
        mi, _ = exgcd(m, r[i]) # m's multiplicative inverse
        ans += a[i] * m * mi
        ans %= n
    return ans
```

## 常用 STL

### 比较两个 string 是否相等

[std::string::compare](https://www.cplusplus.com/reference/string/string/compare/)

|     string (1) | `int compare (const string& str) const noexcept; `           |
| -------------: | ------------------------------------------------------------ |
| substrings (2) | `int compare (size_t pos, size_t len, const string& str, size_t subpos, size_t sublen = npos) const; ` |
|   c-string (3) | `int compare (const char* s) const; int compare (size_t pos, size_t len, const char* s) const; ` |
|     buffer (4) | `int compare (size_t pos, size_t len, const char* s, size_t n) const;` |

返回值

| value | relation between *compared string* and *comparing string*    |
| ----- | ------------------------------------------------------------ |
| `0`   | They compare equal                                           |
| `<0`  | Either the value of the first character that does not match is lower in the *compared string*, or all compared characters match but the *compared string* is shorter. |
| `>0`  | Either the value of the first character that does not match is greater in the *compared string*, or all compared characters match but the *compared string* is longer. |

### 从容器中删除指定的元素

从字符串中删除某些字符

```c++
#include <algorithm>
void removeCharsFromString( string &str, char* charsToRemove ) {
   for ( unsigned int i = 0; i < strlen(charsToRemove); ++i ) {
      str.erase(remove(str.begin(), str.end(), charsToRemove[i]), str.end());
   }
}
```

[std::remove](https://www.cplusplus.com/reference/algorithm/remove/)

```c++
template <class ForwardIterator, class T>
  ForwardIterator remove (ForwardIterator first, ForwardIterator last, const T& val);
```
