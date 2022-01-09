本文目标读者：已有 C/C++ 开发基础，备考学校考试。

> In the syntax notation used in this clause, syntactic categories (nonterminals) are indicated by *italic* type, and literal words and character set members (terminals) by **bold** type. A colon (:) following a nonterminal introduces its definition. Alternative definitions are listed on separate lines, except when prefaced by the words ‘‘one of’’. An optional symbol is indicated by the subscript ‘‘opt’’, so that
>
> **{** *expression*<sub>opt</sub> **}**
>
> indicates an optional expression enclosed in braces.
>
> When  syntactic  categories  are  referred  to  in  the  main  text,  they are  not  italicized  and words are separated by spaces instead of hyphens.
>

## 程序与函数

- 一个程序由一个或多个源程序文件组成。
- 函数是C程序的主要组成部分。

**一个C程序是由一个或多个函数组成**，其中必须包含一个main函数（且只能有一个main函数）。

程序一般对应 工程 概念，指编译成一个可执行文件。

## 标识符

*`identifier`*:

 *`identifier-nondigit`*

 *`identifier`* *`identifier-nondigit`*

 *`identifier`* *`digit`*

*`identifier-nondigit`*:

 *`nondigit`* 下划线及英文字母

 *`universal-character-name`* Unicode 字符

标识符由字母、数字、下划线组成，并且首字母不能是数字。（与 `0x01` 等记法冲突）

## 逗号运算符

```c
while (a = b, c < d)
  ...
```

逗号运算符是将两个或多个表达式放在只允许一个值的位置，while 循环运行与否的实际判断仅受最后一个表达式的控制。

## 赋值表达式

```c
while (current = get_user_input()) != "quit"
    ...
```

```c
int a;
float b;
a = b = 4.5; // 4.5 is a double, it gets converted to float and stored into b 
// this returns a float which is converted to an int and stored in a
// the whole expression returns an int
```

[What does an assignment return?](https://stackoverflow.com/questions/9514569/what-does-an-assignment-return) An assignment expression has the value of the **left operand** after the assignment.

## 求值顺序

[求值顺序](https://zh.cppreference.com/w/c/language/eval_order)

## 声明

> **declarator**
>
> The "second half" of a C declaration, consisting of an identifier name along with optional `*`, `[]`, or `()` syntax indicating (if present) that the identifier is a pointer, array, function, or some combination. See question [1.21](http://c-faq.com/decl/cdecl1.html).

[声明 - cppreference](https://zh.cppreference.com/w/c/language/declarations)

[声明与自然语言转换](https://cdecl.org/)

http://c-faq.com/decl/cdecl1.html

> If a *type-specifier* is not provided in a declaration, it is taken to be **`int`**.

> **declaration mimics use**
>
> The reasoning behind [this syntax](https://en.cppreference.com/w/c/language/declarations#Declarators) is that when the identifier declared by the declarator appears in an expression of the same form as the declarator, it would have the type specified by the type specifier sequence.

## 常量

不带 **`f`**、**`F`**、**`l`** 或 **`L`** 后缀的浮点常量类型为 **`double`**。 如果后缀是字母 **`f`** 或 **`F`**，则常量的类型为 **`float`**。 如果后缀是字母 **`l`** 或 **`L`**，则常量的类型为 **`long double`**。 

*`unsigned-suffix`*: one of

 **`u`** **`U`**

*`long-suffix`*: one of

 **`l`** **`L`**

*`long-long-suffix`*: one of

 **`ll`** **`LL`**

*`floating-suffix`*: one of

 **`f`** **`l`** **`F`** **`L`**
