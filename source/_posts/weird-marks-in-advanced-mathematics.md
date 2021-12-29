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
这就是**分部积分法**。也可以写成简洁形式
$$
\int u\mathrm{d}v=uv-\int v\mathrm{d}u
$$
如果你想要理解这些积分法则，这里有一个线索：第一、第二类换元法对应的是复合函数，分部积分法对应的是两个函数的乘积运算。[这个视频](https://www.bilibili.com/video/BV1qW411N7FU?p=4) 也许也能帮助你更直观地理解。

学积分的时候应该注意思考积分法则的逆运算（逆操作）是什么。如果能明白简单的积分形式是怎么变复杂的，看到复杂的积分也就不难化简了。上面这三种积分法则的逆运算是什么呢？

很容易发现第一类、第二类换元法是互为逆运算的。而分部积分法的逆运算是它自己
$$
\int u\mathrm{d}v=uv-\int v\mathrm{d}u=uv-\left(uv- \int u\mathrm{d}v \right)=\int u\mathrm{d}v
$$

**References:**

1. [迷之记号 dx 到底是什么鬼](https://www.cnblogs.com/li-hua/p/6617366.html)
2. [什么是微分形式不变性？一阶微分形式不变性与链式法则是等价的吗（两者可互推？）？两者有什么区别？ - 马同学的回答](https://www.zhihu.com/question/30296338/answer/120574352)
3. [微分符号 dx、dy 表示什么含义？](https://www.zhihu.com/question/26490937)
4. [Is d/dx not a ratio?](https://math.stackexchange.com/questions/21199/is-frac-textrmdy-textrmdx-not-a-ratio)
5. [The second differential versus the differential of a differential form](https://math.stackexchange.com/a/3561534/858590)

## 从等价无穷小到泰勒公式

### 启程

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
\begin{aligned}
e^x-1&\sim x\ (x\to 0)\\
\ln (1+x)&\sim x\ (x\to 0)
\end{aligned}
$$

### 岔路

过了一段时间，你学到了拉格朗日中值公式。如果（省略）则
$$
f(b)-f(a)=f'( \xi )(b-a)
$$
回到上面那个实际用例。我们可以说，由 $\sin x$ 在 $x=0$ 的某一去心邻域内可导，所以存在 $\xi \in \mathring{U}(0,x)$ 使得
$$
\sin x-\sin 0=\cos \xi(x-0)
$$
当 $x\to 0$ 时有
$$
\lim_{x\to 0}\dfrac{\sin x}{x}=\lim_{x\to 0}\dfrac{\sin x-\sin 0}{x-0}=\lim_{x\to 0}\cos \xi=1
$$
看起来有点意思？还有更有意思的。

如果 $f(x)$ 和 $g(x)$ 在 $a$ 的某去心邻域内可导，当 $x\to a$ 时函数 $f(x)$ 和 $g(x)$ 都趋于零，对于下面这个极限
$$
\lim_{x\to a}\frac{f(x)}{g(x)}
$$
我们可以把上面的方法同时应用到分子分母上。我们为了连续性假定 $f(a)=g(a)=0$ 则此时两函数在 $a$ 的某邻域内连续。

存在 $\xi_1 \in \mathring{U}(a,x), \xi_2 \in \mathring{U}(a,x)$​ 使得
$$
\begin{aligned}
f(x)-f(a)&=f'(\xi_1)(x-a)\\
g(x)-g(a)&=g'(\xi_2)(x-a)
\end{aligned}
$$

若 $g'(x)\neq 0$，有
$$
\lim_{x\to a}\dfrac{f(x)}{g(x)}=\lim_{x\to a}\dfrac{f(x)-f(a)}{g(x)-g(a)}=\lim_{x\to a}\frac{f'(\xi_1)(x-a)}{g'(\xi_2)(x-a)}=\lim_{x\to a}\frac{f'(x)}{g'(x)}
$$
洛必达法则！实际上证明洛必达法则并不依赖柯西中值定理。

上面的推导启示我们，洛必达法则和等价无穷小有某种意义上的联系。若函数 $f(x)$ 和 $g(x)$ 在 $x=x_0$ 的某邻域内 $n$ 阶可导，且当 $x\to x_0$ 时 $f(x)\sim g(x)$ 则
$$
\lim_{x\to x_0}\dfrac{f(x)}{g(x)}=\lim_{x\to x_0}\frac{f^{(n)}(x)}{g^{(n)}(x)}=1
$$
另外，在这个过程中你可能会发现
$$
\frac{f(b)-f(a)}{g(b)-g(a)}=\frac{f'(\xi_1)(b-a)}{g'(\xi_2)(b-a)}=\frac{f'(\xi_1)}{g'(\xi_2)}
$$
柯西中值定理？其实并不是，柯西中值定理还需要 $\xi_1=\xi_2$​，构造
$$
h(x) = [f(x) - f(a)][g(b) - g(a)] - [g(x) - g(a)][f(b) - f(a)].
$$
显然 $h(a)=h(b)=0$​，由罗尔中值定理得
$$
0 = h'(\xi) = f'(\xi)(g(b) - g(a)) - g'(\xi)(f(b) - f(a))
$$

为什么同济高数书上要写成这么别扭的样子呢？
$$
h(x)=f(x)-\frac{f(b)-f(a)}{g(b)-g(a)}g(x)
$$
我猜大概是为了强调 $g(b)-g(a)\neq 0$ 吧（由 $g'(x)\neq 0$ 推出）

再来看一个洛必达法则的证明：

若 $f, g : (a, b) \to R$ 在 $x_0 \in (a,b)$ 上可导，且 $f(x_0)=g(x_0)=0$，$g'(x_0)\neq 0$. 则
$$
\frac{f'(x_0)}{g'(x_0)}=\frac{\lim_{x\to x_0}{\frac{f(x)-f(x_0)}{x-x_0}}}{\lim_{x\to x_0}{\frac{g(x)-g(x_0)}{x-x_0}}}=\lim_{x\to x_0}{\frac{f(x)-f(x_0)}{g(x)-g(x_0)}}=\lim_{x\to x_0}{\frac{f(x)}{g(x)}}
$$
这就证完了？能用一行证明，为什么上面要绕一大圈？

请注意洛必达法则的条件

> 1. 当 $x\to x_0$ 时，函数 $f(x)$ 及 $g(x)$ 都趋于零.
> 2. 在点 $x_0$ 的**某去心邻域内**，$f'(x)$ 及 $g'(x)$ 都存在且 $g'(x)\neq 0$.
> 3. $\lim_{x\to x_0}{\frac{f'(x)}{g'(x)}}$ 存在（或为无穷大）.

其中第 1、2 点都不一样，但是证明时假定了 $f(x_0)=g(x_0)=0$ 所以实际上第 1 点没有区别。最关键的是第 2 点：$f(x)$ 和 $g(x)$ 只需要在 $x_0$ 的某去心邻域可导，不需要在 $x_0$ 可导。与之相对应，公式中也是取两函数导数的比值的极限。

### 迷途

我们来看一道 经 典 例 题：
$$
\lim_{x\to0}\left(\frac{e^x +xe^x}{e^x-1}-\frac{1}{x}\right)
$$
你可能会这么写：
$$
\begin{aligned}
\lim_{x\to 0}\left(\frac{e^x +xe^x}{e^x-1}-\frac{1}{x}\right)&=\lim_{x\to 0}\frac{e^x +xe^x}{e^x-1} - \lim_{x\to 0}\frac{1}{x} \\
&=\lim_{x\to 0}\frac{e^x +xe^x}{e^x-1}\times \lim_{x\to 0}\frac{e^x-1}{x}-\lim_{x\to 0}\frac{1}{x} \\
&=\lim_{x\to 0}\left(\frac{e^x +xe^x}{e^x-1} \times \frac{e^x-1}{x}\right)-\lim_{x\to 0}\frac{1}{x} \\
&=\lim_{x\to 0}\left(\frac{e^x +xe^x}{x}-\frac{1}{x}\right) \\
&=\lim_{x\to 0}\frac{e^x +xe^x-1}{x} \\
&=\lim_{x\to 0}\left(2e^x-xe^x\right) \\
&=2
\end{aligned}
$$

然而！答案是 $\frac{2}{3}$.

错在哪呢？其实第一步就错了，拆出来成了 $\infty -\infty$，而极限运算法则**只在两极限存在时才成立**，不能拆。如果你不是这么做的但是得到了错误的结果，请自行根据 [这篇文章](https://zhuanlan.zhihu.com/p/62029838) 对号入座。

辅导书和老师可能会告诉你，等价无穷小的用法仅限于极限值整体乘以 1 再代换！这种说法确实没错，但是事情是不是就这么简单地结束了呢？为什么有的情况下替换不会出现问题呢？

请看同济高数第 1-7 节定理 1: $\beta$ 和 $\alpha$ 是等价无穷小的充分必要条件为
$$
\beta=\alpha + o(\alpha)
$$
可以看出，两个等价无穷小之间差了一个高阶无穷小。那么什么时候不能用等价无穷小呢？

就是除了无穷小以外的量全部都被消去的情况，这时候高阶无穷小才会左右极限的结果，而它会受到等价无穷小替换的影响而不准确。

也就是说

> 已知 $\lim_{x\to x_0}{\frac{\alpha_1}{\alpha_2}}$  存在， $\alpha_1,\alpha_{2},\beta_{1},\beta_{2}$ 都是 $x\rightarrow x_0$ 的无穷小量，且 $\alpha_1\sim\beta_1$，$\alpha_{2}\sim\beta_{2}$.
>
> 若 $\lim_{x\rightarrow x_0}{\frac{\alpha_1}{\alpha_2}} \neq 1$ （两者的泰勒展开的第一项不相同），则 $\alpha_1-\alpha_2\sim \beta_1-\beta_2$;
>
> 若 $\lim_{x\rightarrow x_0}{\frac{\alpha_1}{\alpha_2}} \neq -1$（两者的泰勒展开的第一项不互为相反数），则 $\alpha_1+\alpha_2\sim\beta_1+\beta_2$.

### 终点

上面看似已经把等价无穷小的用法说清楚了，但是还有很多隐藏的问题。比如说，极限运算法则必须要两个极限存在才成立，那么如果我要求的极限本来就不存在呢？难道我每次用之前还要证明这个极限存在？

所以我们不如用回等价无穷小的充要条件
$$
\alpha \sim \beta \Leftrightarrow \beta=\alpha + o(\alpha)
$$
等价替换永远是最直接、最少出错的。

而实际上我们用等价无穷小的时候几乎从来都是换成多项式函数，因为它好化简、好求极限。

又过了一段时间，你学到了泰勒公式，它是拉格朗日中值公式的推广（令 $n=2m$）
$$
\begin{align}
\sin \left(x\right)&= x-{\frac {x^{3}}{3!}}+{\frac {x^{5}}{5!}}-{\frac {x^{7}}{7!}}+\cdots +(-1)^{m-1}\dfrac{x^{2m-1}}{(2m-1)!}+o(x^{2m})\\
e^{x}&=1+x+{\frac {x^{2}}{2!}}+{\frac {x^{3}}{3!}}+\cdots +\frac{x^{n-1}}{(n-1)!} +o(x^n)\\
\ln(1+x)&=x-{\frac {x^{2}}{2}}+{\frac {x^{3}}{3}}-\cdots+(-1)^{n-1}\dfrac{1}{n}x^n+o(x^n)
\end{align}
$$

接下来不用多说了吧。**用泰勒公式，别用等价无穷小。**

后记：这篇文章写的很混乱，中途删了又写，写了又删。最后终于在高数期末考前仓促结尾，行文思路混乱，更别说严谨性。现在回头反思，总感觉自己太过于相信自己的所谓直觉，推导一番后又发现和目标不搭边。总结：想的太多，读的太少，算的更少。

**References:**

1. [Cauchy's Mean Value Theorem and L'Hopital's rule](http://www.math.pitt.edu/~sparling/23012/23012lhopital1/node1.html)
2. [(PDF)Lecture 7 : Cauchy Mean Value Theorem, L'Hospital Rule](https://home.iitk.ac.in/~psraj/mth101/lecture_notes/lecture7.pdf)
3. [高数常见坑点：等价无穷小](https://zhuanlan.zhihu.com/p/62029838)
3. [“等价无穷小量的替换”的详析 - 李亦督的文章 - 知乎](https://zhuanlan.zhihu.com/p/99373470)
