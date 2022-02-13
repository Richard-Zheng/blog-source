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
