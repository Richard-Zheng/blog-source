---
title: 解读高等数学中那些难懂的符号
date: 2021-11-13 10:53:00
tags: 数学
mathjax: true
---

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

有了链式法则，我们就有了**微分形式不变性**：对于上面的自变量的微分$\mathrm{d}u$，我们原先把它看作自变量的增量$\Delta u$，但是现在我们发现如果$u$又作为另外一个函数$g$的因变量，$\mathrm{d}u$可以直接被替换成它求微分的结果$g'(x)\mathrm{d}x$.

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
两边同时除$\mathrm{d}x^2$得到
$$
\dfrac{\mathrm{d}^2y}{\mathrm{d}x^2}=f''(x)+f'(x)\dfrac{\mathrm{d}^2x}{\mathrm{d}x^2}
$$

好像多了一项？这是基于$x$的变化的影响，我们现在是要让$\mathrm{d}x\to 0$，所以我们实际上求的是对$\mathrm{d}x$的偏微分
$$
\dfrac{(\partial ^ 2 y) _ {\mathrm dx}}{{\mathrm{d}x^2}}=f''(x)
$$

现在来说积分。这里直接跳过书上的“记作”论调，重新定义：积分就是微分的**逆运算**。回想起我们对微分的理解：微分就是把一个函数映射到一个“实数到函数的映射”（若嫌麻烦也可以理解成二元函数）上面。那么积分就是微分的**逆映射**。给一个实数到函数的映射（二元函数），就能对应回一个函数上。嗯？等等，微分这个映射并不是单射，不同的函数也可能有相同的微分。那怎么办呢？我们给它打个补丁：由于有相同微分的原函数互相都只相差某个常数，我们就把积分定义成一个实数到函数的映射对应一个函数集合。这个函数集合中的函数互相都只相差某个常数，我们就用$F(x)+C$来表示这个函数集合。

从定义立即可以得到，如果在区间$I$上可导函数$F(x)$的导函数为$f(x)$，即对任一$x\in I$，都有
$$
\int \mathrm{d}F(x)=\int f(x)\mathrm{d}x=F(x)+C.
$$
回到上面的复合函数，如果$f(u)$具有原函数$F(u)$，由微分形式不变性，有
$$
\int f(g(x))g'(x)\mathrm{d}x=\int f'(u)\mathrm{d}u=F(u)+C
$$
这就是换元积分法中的**第一类换元法**。其实，这就是对被积表达式部分积分。
