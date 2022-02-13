第一次看 3Blue1Brown 的线代本质还是高中，那时候几乎没有 pause and ponder 的时候，一通刷下来也不做题自以为自己学懂了，现在回头一想啥都不记得。

在 [03 - 矩阵与线性变换](https://www.bilibili.com/video/BV1ys411472E?p=4) 这节，我个人感觉 Grant 讲的不够清楚。首先是 04:25 讲的
$$
\begin{split}
\vec{v}&=-1\hat{i}+2\hat{j} \\
\text{Transformed }\vec{v}&=-1(\text{Transformed }\hat{i})+2(\text{Transformed }\hat{j})
\end{split}
$$
这是线性变换给我们的一个重要性质，也是矩阵乘法和线性变换之间的联系的直接原因。但是实际上这并不局限于单位向量：
$$
\vec{v}=a\vec{i}+b\vec{j} \iff \text{Transformed }\vec{v}=a(\text{Transformed }\vec{i})+b(\text{Transformed }\vec{j})
$$
其中 $\vec{i}$ 和 $\vec{j}$ 就是普通的向量。这个性质其实就是在说，如果我知道一个向量 $\vec{v}$ 是由两个向量的数乘加起来而得的，而且我又知道这两个向量在线性变换后的值，那么我就可以直接跟原来一样数乘和累加得到线性变换后对应的 $\vec{v}$.

然后就是结尾 10:51 放的线性变换的严谨定义，Grant 完全可以在向量的基础上讲明白这个。在 01 - 向量究竟是什么 的 04:35 讲过，向量是一个列表，和向量是一个在空间中的箭头，被两种向量的运算联系起来。一个是数乘，一个是加法。二维平面中，我们先定义出单位向量 $\hat{i}=\begin{bmatrix}1 \\0 \end{bmatrix}$ 和 $\hat{j}=\begin{bmatrix}0 \\1 \end{bmatrix}$，然后就有了
$$
\vec{v}=\begin{bmatrix}x \\y \end{bmatrix} \iff \vec{v}=x\hat{i}+y\hat{j}=x\begin{bmatrix}1 \\0 \end{bmatrix}+y\begin{bmatrix}0 \\1 \end{bmatrix}=\begin{bmatrix}1 & 0 \\0 & 1 \end{bmatrix}\begin{bmatrix}x \\y \end{bmatrix}
$$
现在再来看线性变换的定义
$$
\begin{split}
L(\vec{v}+\vec{w})&=L(\vec{v})+L(\vec{w}) \\
L(c\vec{v})&=cL(\vec{v})
\end{split}
$$
显而易见，第一个对应的是线性变换对向量加法透明（保持网格线平行且等距），第二个对应的是线性变换对向量数乘透明（保持原点不动）。那么
$$
\vec{v}=a\vec{i}+b\vec{j} \iff L(\vec{v})=aL(\vec{i})+bL(\vec{j})
$$
就是很明显的了。

想当年自己极度迷信所谓“几何直观”，认为只要领会到一个概念的所谓直觉就能平步青云。随着对数学的认识的不断深入，越发感觉到严谨的、抽象的定义和证明对于思维之重要。诚然，直观的讲解不但有利于记忆，还能启发我们所谓 play around with it. 在玩的过程中感受到性质。理解和感受数学中的结构和性质，才是“直观”的内核。良好的定义所形成的性质和常识的碰撞，才是“直观”的形成条件。但遗憾的是，数学归根结底是由逻辑推理构建的，与其把自己对数学的全部理解建立在直观之上，不如用直观来辅助认识更基本的逻辑推导。