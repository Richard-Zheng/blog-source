---
title: 如何看待「动态规划问题既独立又重叠」
date: 2021-09-01 21:23:00
tags: 算法
---

这篇文章的起因是《算法导论》中的一段话：

> "It may seem strange that dynamic programming relies on subproblems being both independent and overlapping. Although these requirements may sound contradictory, they describe two different notions, rather than two points on the same axis. Two subproblems of the same problem are independent if they do not share resources. Two subproblems are overlapping if they are really the same subproblem that occurs as a subproblem of different problems" (CLRS 3rd edition, 386).

这里的independent和overlap都是啥意思呢？下面是我查了StackOverflow以后得到的结果：

「独立」的意思是说：如果我们说一个解是最优的，那么这个最优的性质并不依赖任何我们要解决的母问题。也就是说不管我们是为了哪个更大的问题来解这个子问题，都会得到这个解。举个简单的例子：从A到B的最短路径经过C，那么我直接求从A到C的最短路径，后者答案应该是前者答案的一部分。这就是最优子结构(optimal substructure)的定义。

「重叠」的意思就很自然：不同的子问题会解多个子子问题，而其中很多子子问题是重复的。有意思的是由于我们刚才的「独立」性质，这些重复的子子问题就算有不同的母问题，他们的解也应该是相同的。因此我们就可以开个数组把这些解存下来。
