---
title: 解读高等数学中那些难懂的符号
date: 2021-11-13 10:53:00
tags: 数学
mathjax: true
---

## 微分符号和积分符号

准备工作：

- 了解极限的定义以及相关的无穷小等概念。
- 了解导数是什么。
- 了解极限运算法则和求导法则。
- 理解“微分是函数的线性近似”

很多人都说《高等数学》难学，一部分缘于求极限、求导和积分是全新的、之前没有接触过的运算，要掌握和熟练运用需要不少苦功夫；另一部分就要归结于编书者用“惯例”来搪塞各种解释的高傲态度。

第二章中，先介绍导数，再介绍微分。这导致前面突然就冒出个$\dfrac{\mathrm{d}}{\mathrm{d}x}$求导符号。然而介绍微分的时候又草草带过。基本上，书中是这样定义微分运算的：对函数$y=f(x)$，如果$x_0$和$x_0+\Delta x$在定义域内且
$$
\Delta y=f'\left( x\right) \Delta x+o\left( \Delta x\right)
$$
那么记作
$$
\mathrm{d}y=A\Delta x.
$$
并且通常把自变量$x$的增量$\Delta x$称为自变量的微分，记作$\mathrm{d}x$，即$\mathrm{d}x=\Delta x$. 所以函数$y=f(x)$的微分记作
$$
\mathrm{d}y=f'(x)\mathrm{d}x.
$$
嗯？这就结束了？

所以微分是什么呢？难道跟我们学的加减乘除一样，就是一个运算符号？

是，也不完全是。

回想书中前面的内容，我们一直把求导符号$\dfrac{\mathrm{d}}{\mathrm{d}x}$称为“算子”。其实这个概念在第一章第一节早有介绍，只不过大部分人都会忽略：

> 映射又称为**算子**。根据集合$X$、$Y$的不同情形，在不同的数学分支中，映射又有不同的惯用名称。例如，从非空集$X$到数集$Y$的映射又称为$X$上的**泛函**，从非空集$X$到它自身的映射又称为$X$上的**变换**，从实数集（或其子集）$X$到实数集$Y$的映射通常定义为$X$上的**函数**。

那么求导是怎样的一种映射？显然是一个原函数映射成一个导函数。那微分呢？
$$
\begin{align}
y&=x^2\\
\mathrm{d}y&=2x\mathrm{d}x
\end{align}
$$
是函数映射成函数吗？看着不像啊！这怎么又有$x$又有$\mathrm{d}x$，难道是二元函数？

你可以这么理解，但是我认为一个（在数学上是等价的）更好的理解是：对于每一个$x$，都有一个对应的函数$g(\mathrm{d}x)=2x\mathrm{d}x$. 这个函数是$y$在$x$附近的**线性近似**。微分就是把一个函数映射到这样一个实数到函数的映射（若嫌麻烦也可以理解成二元函数）上面。

到这里，有必要解释一下为啥书里面不先介绍微分了。这其实是个历史遗留问题。微分的符号$\mathrm{d}$最早是莱布尼茨发明的（顺便一提，积分符号也是他发明的），他把$\Delta x$和$\Delta y$当成是有限的增量，对应的$\mathrm{d}x$和$\mathrm{d}y$就是无穷小增量。然而麻烦的是，莱布尼茨对于无穷小和微分的定义是很不精确的（莱布尼茨发明微积分的时候还没有极限的严格定义，具体可以参考[这里的回答](https://math.stackexchange.com/questions/21199/is-frac-textrmdy-textrmdx-not-a-ratio)），所以我们现在学习的**并不是他的理论**。然而我们要学他的符号，因为这已经是“惯例”了。我们学习的是
$$
\dfrac{\mathrm{d}}{\mathrm{d}x}y=\lim _{\Delta x\to 0}{\frac {\Delta y}{\Delta x}}
$$
其中$\dfrac{\mathrm{d}}{\mathrm{d}x}$就是一个写得比较奇怪的记号。那么你可能会问：先讲微分，不就没这么多破事了吗？不好意思，不行。因为我们现在采用的是柯西给出的微积分定义（极限的严格定义也是柯西给出的）。他是用导数定义微分的：
$$
\mathrm{d}y=f'(x)\mathrm{d}x.
$$
这下死循环了。所以编书者没办法，就这么将就学吧。

有人会问：不是说牛顿和莱布尼茨同时发明了微积分吗？牛顿的符号为啥没流传下来呢？其实现在也在用，就是$\dot {y}$，表示$y$的一阶导数，二阶就是加两个点，三阶就是加三个点，以此类推。但是这样写并没有显式地指明自变量是什么，容易造成误解。

莱布尼茨符号流行的另外一个原因是它能辅助记忆用于微分和积分的公式。比如链式法则：假设函数$g$在$x$处可微，$y = f(u)$在$u = g(x)$处可微。那么复合函数$y = f(g(x))$在$x$处是可微的，其导数用莱布尼茨符号表示为：
$$
\dfrac{\mathrm{d}y}{\mathrm{d}x}=\dfrac{\mathrm{d}y}{\mathrm{d}u}\cdot \dfrac{\mathrm{d}u}{\mathrm{d}x}
$$
把$\mathrm{d}u$消……等等！谁告诉你能这么消的？
$$
\dfrac{\mathrm{d}y}{\mathrm{d}x}=\lim _{\Delta u\to 0}{\frac {\Delta y}{\Delta u}} \cdot \lim _{\Delta x\to 0}{\frac {\Delta u}{\Delta x}}
$$
用极限形式写出来。显然，这两个极限的变量都不一样，不可以消去。

如果要证明链式法则，我们可以利用微分的概念。
$$
\begin{align}
\Delta y&=f'(u)\Delta u+o(\Delta u)\\
&=f'(u)\left[g'(x)\Delta x+o(\Delta x)\right]+o(\Delta u)\\
&=f'(u)g'(x)\Delta x+f'(u)\cdot o(\Delta x)+o(\Delta u)
\end{align}
$$
所以
$$
\mathrm{d}y=f'(u)\mathrm{d}u=f'(u)g'(x)\mathrm{d}x
$$
书中用导数定义微分，因此复合函数的微分法则就是由链式法则推出。但是我个人感觉这样的写法更自然好懂：既然我要的是线性近似，那么自变量$u$当然也可以被它自己的线性近似替代。

有了链式法则，我们就有了**一阶微分形式不变性**：对于上面的自变量的微分$\mathrm{d}u$，我们原先把它看作自变量的增量$\Delta u$，但是现在我们发现如果$u$又作为另外一个函数$g$的因变量，$\mathrm{d}u$可以直接被替换成它求微分的结果$g'(x)\mathrm{d}x$.

那既然对谁微分都是一样的形式，岂不是自变量就不重要了？所以$\mathrm{d}$无论出现在哪里都是一个意思，无论$y$对应的自变量是$x$还是$v$？

错。我们上面说的微分形式不变性是对于**一阶微分**而言的，对于二阶微分会是什么样的情况呢？

对于二阶导数，书中是这么写的
$$
f''(x)=\dfrac{\mathrm{d}}{\mathrm{d}x}\left(\dfrac{\mathrm{d}y}{\mathrm{d}x}\right)=\dfrac{\mathrm{d}^2y}{\mathrm{d}x^2}
$$

看着也挺怪的，我们用微分写
$$
\begin{align}
\mathrm{d}^2y&=\mathrm{d}(\mathrm{d}y)\\
&=\mathrm{d}(f'(x)\mathrm{d}x)\\
&=\mathrm{d}(f'(x))\mathrm{d}x+f'(x)\mathrm{d}(\mathrm{d}x)\\
&=(f''(x)\mathrm{d}x)\mathrm{d}x+f'(x)\mathrm{d}^2x\\
&=f''(x)\mathrm{d}x^2+f'(x)\mathrm{d}^2x
\end{align}
$$

好像多了一项$f'(x)\mathrm{d}^2x$？

这就是为什么微分形式不变性对于二阶微分不成立！二阶微分不但会受$\mathrm{d}x^{2}$影响，也会受$\mathrm{d^2}x$影响。

我们若是想得到二阶导数的形式，就必须把$x$**看成自变量而不是一个可微的函数**，我们实际上求的是对$\mathrm{d}x$的偏微分

$$
\left(\partial ^ 2 y\right) _ {\mathrm{d}x}=f''(x)\mathrm{d}x^2
$$

所以，二阶微分不具有形式不变性。

现在来说积分。这里直接跳过书上的“记作”论调，重新定义：积分就是微分的**逆运算**。回想起我们对微分的理解：微分就是把一个函数映射到一个“实数到函数的映射”（若嫌麻烦也可以理解成二元函数）上面。那么积分就是微分的**逆映射**。给一个实数到函数的映射（二元函数），就能对应回一个函数上。嗯？等等，微分这个映射并不是单射，不同的函数也可能有相同的微分。那怎么办呢？我们给它打个补丁：由于有相同微分的原函数互相都只相差某个常数，我们就把积分定义成一个实数到函数的映射对应一个函数集合。这个函数集合中的函数互相都只相差某个常数，我们就用$F(x)+C$来表示这个函数集合。

从定义立即可以得到，如果在区间$I$上可导函数$F(x)$的导函数为$f(x)$，对任一$x\in I$，都有
$$
\int \mathrm{d}F(x)=\int f(x)\mathrm{d}x=F(x)+C.
$$
回到上面的复合函数，如果$f(u)$具有原函数$F(u)$，由微分形式不变性，有
$$
\int f(g(x))g'(x)\mathrm{d}x=\int f'(u)\mathrm{d}u=F(u)+C
$$
这就是换元积分法中的**第一类换元法**。其实，这就是对被积表达式部分积分。

我们也可以反向操作：

令$t=\phi ^{-1}(x)$，则$x=\phi (t)$，有
$$
\int f(x)\mathrm{d}x=\int f(\phi (t))\mathrm{d}\phi (t)=\int f(\phi (t))\phi '(t)\mathrm{d}t
$$
这就是换元积分法中的**第二类换元法**。

微分法则能启发我们计算积分，比如：对于在区间$I$上的可微函数$f(x)$和$g(x)$有
$$
\begin{aligned}
\mathrm{d}\left[f(x)g(x)\right]&=f(x)\cdot \mathrm{d}g(x)+\mathrm{d}f(x)\cdot g(x)\\
&=f(x)g'(x)\mathrm{d}x+f'(x)g(x)\mathrm{d}x
\end{aligned}
$$
两边积分得
$$
\int \mathrm{d}\left[f(x)g(x)\right]=\int f(x)g'(x)\mathrm{d}x+\int f'(x)g(x)\mathrm{d}x
$$
即
$$
\int f(x)g'(x)\mathrm{d}x=f(x)g(x)-\int f'(x)g(x)\mathrm{d}x
$$
这就是**分部积分法**。

**References:**

1. [迷之记号 dx 到底是什么鬼](https://www.cnblogs.com/li-hua/p/6617366.html)
2. [什么是微分形式不变性？一阶微分形式不变性与链式法则是等价的吗（两者可互推？）？两者有什么区别？ - 马同学的回答](https://www.zhihu.com/question/30296338/answer/120574352)
3. [微分符号 dx、dy 表示什么含义？](https://www.zhihu.com/question/26490937)
4. [Is d/dx not a ratio?](https://math.stackexchange.com/questions/21199/is-frac-textrmdy-textrmdx-not-a-ratio)
5. [The second differential versus the differential of a differential form](https://math.stackexchange.com/a/3561534/858590)

## 微分中值定理和洛必达法则

在第 1.7 节 无穷小的比较中就介绍了等价无穷小：

> 如果 $\lim \dfrac{\beta}{\alpha}=1$，那么就说 $\beta$ 和 $\alpha$ 是等价无穷小，记作 $\alpha \sim \beta$.

比如
$$
\sin x \sim x \ (x\to 0)
$$
等价无穷小有什么特别的，以至于要专门给他分配个符号呢？

由极限运算法则，如果 $\lim f(x)=A$，$\lim g(x)=B$，那么
$$
\lim[f(x)\cdot g(x)]=\lim f(x)\cdot \lim g(x)=A\cdot B
$$
所以
$$
\lim_{x\to 0} f(x) = \lim_{x\to 0} f(x) \cdot \lim_{x\to 0}\dfrac{\sin x}{x} = \lim_{x\to 0} \left[ f(x) \cdot \dfrac{\sin x}{x} \right]
$$
来看个实际用例：
$$
\lim _{x\rightarrow 0}\dfrac{\sin x}{x^{3}+3x}=\lim _{x\rightarrow 0}\left( \dfrac{\sin x}{x^{3}+3x}\cdot \dfrac{x}{\sin x}\right) = \lim _{x\rightarrow 0}\dfrac{x}{x(x^{2}+3)} = \dfrac{1}{3}
$$
常用的等价无穷小还有
$$
e^x-1\sim x\ (x\to 0)\\
\ln (1+x)\sim x\ (x\to 0)
$$
过了一段时间，你学到了拉格朗日中值公式。如果（省略）则
$$
f(b)-f(a)=f'( \xi )(b-a)
$$
回到上面那个实际用例。我们可以说，由 $\sin x$ 在 $x=0$ 的某一邻域内可导，所以存在 $\xi \in \mathring{U}(0,x)$ 使得
$$
\sin x-\sin 0=\cos \xi(x-0)
$$
当 $x\to 0$ 时有
$$
\lim_{x\to 0}\dfrac{\sin x}{x}=\lim_{x\to 0}\dfrac{\sin x-\sin 0}{x-0}=\lim_{x\to 0}\cos \xi=1
$$
看起来有点意思？还有更有意思的。

如果 $f(x)$ 和 $F(x)$ 在 $a$ 的某去心邻域内可导，对于下面这个极限
$$
\lim_{x\to a}\frac{f(x)}{F(x)}
$$
我们可以把上面的方法同时应用到分子分母上。也就是说存在 $\xi_1 \in \mathring{U}(a,x), \xi_2 \in \mathring{U}(a,x)$​ 使得
$$
f(x)-f(a)=f'(\xi_1)(x-a)\\
F(x)-F(a)=F'(\xi_2)(x-a)
$$
那么就有
$$
\frac{f(x)-f(a)}{F(x)-F(a)}=\frac{f'(\xi_1)(x-a)}{F'(\xi_2)(x-a)}=\frac{f'(\xi_1)}{F'(\xi_2)}
$$
柯西中值定理！

如果当 $x\to a$ 时函数 $f(x)$ 和 $F(x)$ 都趋于零，且 $F'(x)\neq 0$，有
$$
\lim_{x\to a}\dfrac{f(x)}{F(x)}=\lim_{x\to 0}\dfrac{f(x)-f(a)}{F(x)-F(a)}=\lim_{x\to 0}\frac{f'(\xi_1)(x-a)}{F'(\xi_2)(x-a)}=\lim_{x\to 0}\frac{f'(\xi_1)}{F'(\xi_2)}
$$
洛必达法则！

又过了一段时间，你学到了泰勒公式，它是拉格朗日中值公式的推广（令 $n=2m$）
$$
\begin{align}
\sin \left(x\right)&= x-{\frac {x^{3}}{3!}}+{\frac {x^{5}}{5!}}-{\frac {x^{7}}{7!}}+\cdots +(-1)^{m-1}\dfrac{x^{2m-1}}{(2m-1)!}+R_{2m}(x)\\
e^{x}&=1+x+{\frac {x^{2}}{2!}}+{\frac {x^{3}}{3!}}+\cdots +\frac{x^{n-1}}{(n-1)!} +R_{n}(x)\\
\ln(1+x)&=x-{\frac {x^{2}}{2}}+{\frac {x^{3}}{3}}-\cdots+(-1)^{n-1}\dfrac{1}{n}x^n+R_{n}(x)
\end{align}
$$
