---
title: Probability - Sample Space and Probability
tags:
  - 数学笔记
  - 概率论
categories:
  - 数学
  - 概率论
copyright: true
comments: true
mathjax: true
abbrlink: 457064921
date: 2021-09-14 23:00:09
---

# 采样空间 - Sample Space
* "List" (set) of possible outcomes. List must be mutually exclusive (互斥的) and collectively exhaustive (穷尽的)
* 采样空间可以分为离散空间和连续空间。

# 概率论中的公理 - Probability Axioms
两个定义
* 事件：是采样空间的一个子集
* 每个事件都会有对应的概率

三个公理:
* Nonnegativity 非负性：$\rm P(A)\ge0$
* Normalization 归一化：$\rm P(\Omega)=1$ 指的是整个采样空间的概率为1
* Additivity 互斥事件的加法法则：如果A和B两个事件互斥，即$A\cap B=\varnothing$，那么$\rm P(A\cup B)=P(A)+P(B)$

公理3可以推广到多个互斥事件上。

# 条件概率 - Conditional Probability
定义：$\rm P(A|B)=$当B发生，A发生的概率
当$\rm P(B)\neq 0$，有：

\begin{equation}
\rm 
P(A|B)=\frac{\rm P(A\cap B)}{\rm P(B)}
\end{equation}

根据条件概率可以推导出：
\begin{equation}
\rm 
P(A\cap B)=P(B)P(A|B)
\end{equation}
再结合公理3可以推出：
\begin{equation}
\rm 
P(A\cup B|C)=P(A|C)+P(B|C)
\end{equation}
乘法法则：
\begin{equation}\begin{split}\rm P(A\cap B \cap C)&=\rm P(A\cap B)P(C|A\cap B)\\\\
&=\rm P(A)P(B|A)P(C|A\cap B)
\end{split}\end{equation}

# 全概率公式 - Total Probability Theorem
假设采样空间可以分成${A_1,A_2,...,A_n}$

\begin{equation}
\begin{split}
\rm 
P(B)&=\sum_{i=1}^{n}P(B\cap A_i)\\\\
&=\sum_{i=1}^{n}P(A_i)P(B|A_i)
\end{split}
\end{equation}

# 贝叶斯公式 - Bayes' Rule
已知先验概率$P(A_i)$和$P(B|A_i)$，求$P(A_i|B)$。

\begin{equation}
\begin{split}
\rm 
P(A_i|B)&=\frac{\rm P(A_i\cap B)}{\rm P(B)}\\\\
&=\frac{\rm P(A_i)P(B|A_i)}{\rm \sum_{j=1}^{n}P(A_j)P(B|A_j)}
\end{split}
\end{equation}

# 独立事件 - Independent events
定义：两个事件是独立的，指一次实验中一事件的发生不会影响到另一事件发生的概率。如果$P(B|A)=P(B)$或者$P(A\cap B)=P(A)P(B)$，就可以称A与B是互相独立的事件。

“条件”可能会影响两个事件的独立性：Independency in original model does not imply independency in the conditional model. 反之也成立。

# 组合 - Combinations
这里组合表示为
\begin{equation}
\rm 
(^n_k)=\frac{\rm n!}{\rm k!(n-k)!}
\end{equation}
打出来有些难看，又不想打大括号复杂的公式，后面还是用$C_n^k$来表示吧。

# Assignment
## Problem Set 1

{% asset_img ProblemSet1-1.png %}

1:
(a) $\rm A\cup B\cup C$
(b) $\rm (A\cap B^c\cap C^c)\cup (A^c\cap B\cap C^c)\cup (A^c\cap B^c\cap C)\cup (A^c\cap B^c\cap C^c)$
(c) $\rm (A\cup B\cup C)^c$
(d) $\rm A\cap B\cap C$
(e) $\rm (A\cap B^c\cap C^c)\cup (A^c\cap B\cap C^c)\cup (A^c\cap B^c\cap C)$
(f) $\rm A\cap B\cap C^c$
(g) $\rm A\cup B^c$
这里(g)做错了，应该是$A\cup (A^c\cap B^c)$。因为题目是A发生，或者当A不发生时，B也不发生。

2:
(a) 1/8
(b) 1/8
(c) 3/8
(d) 1/2

3:
这题目是真的没看懂😅，看了下答案才知道大概意思。就是两个骰子摇出来的结果的和是和所有结果的总和成比例的。需要把全部可能结果列出来然后算出概率。

4:
P(B)=71/72
P(C)=0
$P(A\cap D)=25/72$

这里只有P(C)做对了。P(B)的面积应该是一个小正方形而不是三角形，这里想错了，所以应该是35/36。$P(A\cap D)$这里算少了上面一部分，只计算了Alice大于1/3并且大于Bob 1/3的部分，没有算上小于Bob的部分，最终结果应该是41/72。

{% asset_img ProblemSet1-2.png %}

5:
(a) 圆的面积是半径平方乘以$\pi$，要等50分就要在1in里面，所以应该是1/100。
(b)30分是在1～3in这个空心圆中(9-1)/100=2/25
(c)对John来说，结果和Mike应该是一样的，因为左右半区并不会影响成绩。

6:
这个真的想不到证明的方法。可以参考<https://math.stackexchange.com/questions/2622714/prove-that-for-any-three-events-a-b-c-pabc-ge-pa-pb-pc-%E2%88%92-2>

## Problem Set 2

上课的时候感觉学的东西很简单，但是每次课后题都这么难。

{% asset_img ProblemSet2-1.png %}

1:
(a) 
A = {Forecast is rain}
B = {It is rain}
C = {It is winter}
D = {It is summer}
\begin{equation}
\begin{split}
\rm
P(A|B\cup C)&=\frac{\rm P(A\cup B\cup C)}{\rm P(B\cup C)}=\frac{56}{59}
\end{split}
\end{equation}

\begin{equation}
\begin{split}
\rm
P(A|B\cup D)&=\frac{\rm P(A\cup B\cup D)}{\rm P(B\cup D)}=\frac{16}{24}
\end{split}
\end{equation}

(b)



2:
(a)
\begin{equation}
\rm
P(A) = \frac{1}{25} \\\\
P(B) = 1-\frac{16}{25}=\frac{9}{25} \\\\
P(C) = \frac{9}{25} \\\\
P(B|A)=1\neq P(B)
P(C|A)=0\neq P(C)
\end{equation}
所以，A与B或C都不独立。

(b)
\begin{equation}
\rm
P(D) = \frac{4}{25}\\\\
P(E) = \frac{8}{25}\\\\
P(F) = \frac{10}{25}\\\\
P(F|E) = \frac{1}{2} \neq P(F)
P(E|D) = \frac{1}{2}
P(F|D) = \frac{1}{2}
P(E\cap F |D)=\frac{1}{4}=P(E|D)P(F|D)
\end{equation}
(i) 因为$P(F|E)\neq P(F)$，所以他们是相关的
(ii) 但是在D发生的条件下，他们是无关的。

3:
(a)
\begin{equation}
\rm
P = \frac{1}{2}\*0.15^2+\frac{1}{2}\*0.05^2
\end{equation}
看了下答案，发现这里其实是一个没有放回的抽取，所以不能直接用平方。
(b)
\begin{equation}
\begin{split}
\rm
P(old|two\ defective)&=\frac{\rm P(old)P(two\ defective)*P(old)}{\rm P(old)P(two\ defective|old)+P(new)P(two\ defective|new)}
\end{split}
\end{equation}


{% asset_img ProblemSet2-2.png %}

4:
(a)
$\rm P(A)=0.4,\ P(B)=0.6,\ P(find|A)=0.25,\ P(find|B)=0.15$
$\rm P(A\cap find)=P(find|A)P(A)=0.1$
$\rm P(B\cap find)=P(find|B)P(B)=0.09$
所以第一天应该选A森林
(b)
\begin{equation}
\begin{split}
\rm
P(A|not\ find\ in\ A)
&=\rm \frac{\rm P(not\ find\ in\ A|A)P(A)}{\rm P(not\ find\ in\ A)}\\\\
&=\rm \frac{\rm P(not\ find\ in\ A|A)P(A)}{\rm P(not\ find\ in\ A|A)P(A)+P(not\ find\ in\ A|B)P(B)}\\\\
&=\rm \frac{\rm 0.75\*0.4}{0.75\*0.4+1\*0.6}=\frac{1}{3}
\end{split}
\end{equation}
(c)
\begin{equation}
\begin{split}
\rm P(looked\ in\ A|find\ dog)&=\frac{\rm P(find\ dog|looked\ in\ A)P(looked\ in\ A)}{\rm P(find dog)}\\\\
&=\rm \frac{0.25\*0.4\*0.5}{0.25\*0.4\*0.5+0.15\*0.6\*0.5}
\end{split}
\end{equation}
