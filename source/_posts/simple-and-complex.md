---
title: 简单与复杂
date: 2020-05-31 12:02:06
tags:
- 数学
- 信息学
---

之前有一篇文章是我在学习排列组合时做的笔记，自从这篇文章发出来之后，我也向不少人询问过意见。很多人觉得我的思路很好，但是从结果看来太过冗长了，尤其是与课本上的解释比起来。这中说法引起了我的思考：我做的事情，是不是把简单的问题复杂化了呢？究竟什么对于我来说是简单，又有什么是复杂的？由此，还可以继续追问：数学和物理学的发展究竟是越来越简单，还是越来越复杂？我们现在实际追求的，又是什么？

要解决这个问题，首先我们需要寻找「简单」和「复杂」的定义。回想一下，我们一般认为什么是简单的，又有什么是复杂的呢？最简单的方法是从认知规律的角度定义：小学生学的肯定比高中生学的要简单。不过，我上一篇文章不也是小学奥数的内容吗？我们也可以感受到，有些习以为常的现象背后有着深刻的物理学规律。所以，这样定义似乎不够准确。

我们还可以从问题的角度定义：有些问题解决起来需要花费更多成本，它们是相对更「难」的问题。不过我们也可以发现，同一个问题有着不同的解法，而从解法上来说又有着准确性之分。寻找某个解法的成本和解法的准确性有时是矛盾的。就像是日心说和地心说。如果从整个物理学的发展历程来看的话，物理学是正在变得越来越准确了。然而物理学上的成果越靠近现代，越难为人理解和掌握了。这一点有些让人感到奇怪。难道古代人就不会自创出一些复杂而冗长的解释吗？我想这应该很有可能，只不过那些解释随着无法解释（或者解释起来很困难）的新的现象被发现被淘汰掉了。看起来，我们一直在追求着简单化的学说。不过这有点像是背包问题：你不知道现在看起来简单易懂的学说在解释新现象时是否会变得更加冗长。也许，我们在这一点上只能一直采取贪心策略。不过从运动来看的话，「本质」就是相对于「现象」的运动，更加静止的东西。如果说简洁的学说就是更加静止的、「本质」的，那么它能够被我们自然而然地追求和发现也就不足为奇了。

与此相对的，就是「科学有时是反直觉的」。有些物理和数学现象会让我们感到很疑惑，与我们常规的认知相悖。不过在我看来，这种情况完全说不上是一件坏事。因为违反直觉的部分往往就是最关键的部分，它往往与这个学说的最根本的前提有关。

我们可以从上面提到的两种「复杂」概括出科学发展的方向：其一是给出新定义，以使理论更加贴近现实，更加完美地解释现实。其二是从逻辑上完善严谨性，让那些违反直觉的部分得到精确的论证。当然，这两个部分本来就是相互依存的。

我们还可以从信息量的角度定义复杂程度。例如，为什么「数形结合」使得问题简化了？如果我们不能在平面直角坐标系里思考二维坐标，那么他们对于我们而言就是两个数字的组合而已。显然，我们人类擅长从视觉中提取信息。当「两个数字的组合」放到坐标系里表达时，虽然并没有本质上的变化，但是我们得到的信息变多了：两个点之间的距离有多大、直线穿过几个点、曲线是什么形状的等等。

我在看数学压轴题的题解时，常常有这种感觉：看完之后能够从逻辑上认同给出的答案，但是自己做的时候，就又不会了。这是因为没有仔细理解每个步骤的意图，也即「为什么这么做？」。要从题解中很好地理解每个步骤的意图是很复杂的。这也暗示了从「解题思路」到「题解」的转换之间存在着信息的损失。更好的例子是从高级语言到汇编码的转换。对于机器来讲，汇编码是简单的，因为它其中的每一条指令都很具体和底层。可是对于人来说，我们想要理解代码的意思，这时高级语言就更加简洁和清晰了。用高级语言编写的源代码包含一种信息，就是我们构造代码的「理念」：我们想要这段代码在宏观上作出什么事情。而汇编码只会指导机器一步一步地执行具体的操作，而不关心究竟得到了什么。

汇编码到高级语言的转换常常被人称作「抽象」。在这里我们可以瞥见抽象的一个重要意义：它通过归纳和概括，隐去一些不重要的信息，从而使得「理念」性的信息凸显出来，使人易于理解。事实上，并非完全没有办法把汇编码反编为高级语言。但是得到的结果也往往和原先的代码差别很大，而且和转换前一样难以理解。这与抽象时的「一对多」情况有关。也就是多个版本的源代码可能会编译出同样的汇编码。具体可以看看我写的另一篇文章「排列组合为什么这么难」。与之相同的是，我之前幻想能够把一道数学题的难以理解的代数解法一条一条转换为几何解法。现在看来，这是行不通的。不过这么做也许是思考几何解法的一个好的开始，因为几何图形对我们来说信息量更大，也更丰富。

在数学和物理中，有很多精妙的抽象大大简化了我们对「理念」的认识过程。而大多数都与「数形结合」有关。平面直角坐标系、向量场、微分方程中的相图......数学之所以让人感到难学，有很大一部分原因是我们对它的认识「不精确」：这个定理描述的是什么？这种解法什么时候起作用？极限是什么意思？图像和其他的直观的理解，正是它们在我们脑海「精确化」的过程。