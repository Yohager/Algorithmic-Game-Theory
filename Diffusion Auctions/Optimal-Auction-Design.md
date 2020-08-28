### Optimal Auction Design

---

一个seller出售单物品的情况，seller对于auctioners是一个不完美信息的观测情况。他不清楚buyers愿意付出多少钱来购买这个item. 现在seller的问题是设计一种auction，在这种auction下存在一个纳什均衡使得他自己能够获得尽可能大的收益。本文的最优拍卖的结果可以扩展到一系列的auction design问题中。

#### Introduction

这篇论文中构建了对于一类很广泛的auction design problems的最优拍卖。尽管这些拍卖的item都是打折出售且其价格都是低于最高估值，甚至有时候item不是分配给最高报价者，但是我们将证明这类的最优拍卖下，没有更好的机制能够带给seller更高的期望收益。

将auctions看作一个不完美信息观测下的非合作博弈。在这类的博弈上已经存在了很多的成功，这里就不赘述了，后续有空再去看这些经典的论文。本文的思路大致为：第二章介绍基本的假设和符号表示，第三章分析可行拍卖机制集合的性质以及介绍如何将auction design problem转化为一个数学优化问题。第四章中则是分析了两个关于auction机制设计的引理，第五章对于满足一定规则情况下的auction design问题，给出了一类最优拍卖，第六章将第五章的结论进一步扩展到了更加泛化的情况下，第七章给出一个example来展示反直觉的auctions在bidders' value预测不是随机独立的情况下有可能是一个最优的拍卖，第八章则是对于全文的总结以及未来需要解决的问题。

#### Basic definitions and assumptions

$N$表示bidders的集合：$N=\{1,\cdots,n\}$.

定义$t_i$表示bidder $i$对于seller所售出的item的估值.

假设seller对于bidders的估值可以认为一个在有限区间内的连续的概率分布，假设$a_i$表示这个估值分布下的$i$ bidder可能最低的估值，$b_i$表示在这个估值分布下的$i$ bidder可能最高的估值。那么我们定义$f_i:[a_i,b_i]\rightarrow \mathbb{R}_{+}$为对于bidder $i$的估值$t_i$的一个概率密度函数。 
$$
F_i(t_i)=\int_{a_i}^{t_i}f_i(s_i)\mathrm{d}s_i
$$
假设$T$定义为所有bidders的可能的估值预测的组合的集合：
$$
T=[a_1,b_1]\times \cdots \times [a_n,b_n]
$$
对于任意一个bidder $i$，定义$T_{-i}$表示除了$i$以外的其他人的估值预测：
$$
T_{-i}=\underset{j \in N \atop j \neq i}{\times}\left[a_{j}, b_{j}\right]
$$
在第七章之前我们都是假设独立的随机变量，因此对于$t=(t_1,\cdots,t_n)$向量来说联合密度函数可以写为：
$$
f(t)=\prod_{j\in N}f_j(t_j)
$$
类似地对于$T_{-i}$上的向量$t_{-i}$可以得到：
$$
f(t)=\underset{j\in N \atop j\neq i}{\prod}f_j(t_j)
$$
一个bidder的估值的预测分布对于seller和其他bidders来说是不可知的。首先一个bidder的个人偏好可能对于其他的agents是未知的，第二点在于一个bidder可能比其他人拥有对于一个item的更多的信息，比如是否是完好的item，是否是一个赝品等等信息。我们定义这两种不确定性分别为：偏好不确定和质量不确定。这个区别非常重要。因为前者往往是影响不到别人的，但是后者如果让其他的bidders知道会导致其他人的估值变化。这个非常符合直觉。

大多数的auction问题都只考虑前者，但是在本文中两种不确定性全部都会被考虑在内。现在需要假设存在n个revision effect functions：$e_j:[a_i,b_i]\rightarrow \mathbb{R}$. 如果另一个bidder $i$获得了$t_j$，那么$i$会改变他的估值为$e_j(t_j)$. 如果bidder $i$得到了所有人的估值预测向量，那么它将会调整自己的估值为：
$$
v_i(t)=t_i+\underset{j\in N\atop j\neq i}{\sum}e_j(t_j)
$$
如果在考虑纯偏好不确定性的情况下，我们可以将问题简化为：$e_j(t_j)\equiv 0$. 

为了证明我们对于$t_i$的解释是$i$对于item价值的最初估值，我们应该假设这些修正效应的期望值为零，因此：
$$
\int_{a_j}^{b_j} e_j(t_j)f_j(t_j)\mathrm{d}t_j=0
$$
然而这个假设事实上对于文章中的结果并不是必要条件。

#### Feasible auction mechanism

给定密度函数$f_i$和修正效应函数$e_i$，同时给出$v_i$. seller的问题在于选择一个机制来最大化他的期望收益。首先我们将注意力集中于一类特殊的auction机制，直接显示性机制。

在一个直接显示性机制中，bidders直接告知他们的估值预测给seller，然后seller决定谁可以获得这个物品同时每一个bidder应该支付多少钱，这两个值都应是关于$t=(t_1,\cdots,t_n)$的函数，因此一个显示性机制是输出函数对$(p,x)$（$p:T\rightarrow \mathbb{R}^n$以及$x:T\rightarrow \mathbb{R}^n$）$p_i(t)$表示的是$i$获得一个物品的概率同时$x_i(t)$表示$i$期望的支付的值。

对于每一个bidder来说它的收益可以写为：
$$
U_i(p,x,t_i)=\int_{T_{-i}}(v_i(t)p_i(t)-x_i(t))f_{-i}(t_{-i})\mathrm{d}t_{-i}
$$
其中$\mathrm{d}t_{-i}=\mathrm{d}t_i\cdots \mathrm{d}t_{i-1}\mathrm{d}t_{i+1}\cdots \mathrm{d}t_n$.

类似地对于seller从这个auction中获得的期望收益可以写为：
$$
U_0(p,x)=\int_T\left(v_0(t)\left(1-\sum_{j\in N}p_j(t)\right)+\sum_{j\in N}x_j(t)\right)f(t)\mathrm{d}t
$$
注意不是每一个函数对$(p,x)$都表示一个可行的auction mechanism. 存在三种对于$(p,x)$的约束条件。首先单物品的拍卖，$p$分配规则应该满足：
$$
\sum_{j\in N}p_j(t)\leq 1 \text{ and } p_i(t)\geq 0, \forall i \in N, \forall t\in T
$$
满足individual-rationality：
$$
U_{i}\left(p, x, t_{i}\right) \geqslant 0, \quad \forall i \in N, \quad \forall{t_{i}} \in\left[a_{i}, b_{i}\right]
$$
同时这个机制还需要满足IC性，假设一个bidder $i$的虚报value estimate为$s_i$，那么他在这种情况下的收益可以表示为：
$$
\int_{T_{-i}}(v_i(t)p_i(t_{-i},s_i)-x_i(t_{-i},s_i))f_{-i}(t_{-i})\mathrm{d}t_{-i}
$$
其中$(t_{-i},s_i)=(t_1,\cdots,t_{i-1},s_i,t_{i+1},\cdots,t_n)$. 为了保证IC性，我们应有：
$$
\begin{split}
U_{i}\left(p, x, t_{i}\right) & \geqslant \int_{T_{-i}}\left(v_{i}(t) p_{i}\left(t_{-i}, s_{i}\right)-x_{i}\left(t_{-i}, s_{i}\right)\right) f_{-i}\left(t_{-i}\right) d t_{-i} \\
&\forall i \in N, \quad \forall t_{i} \in\left[a_{i}, b_{i}\right], \quad \forall s_{i} \in\left[a_{i}, b_{i}\right]
\end{split}
$$
满足上面的三条规则，这个机制可以保证所有的bidders都乐意参加同时机制执行下的auction可以预测到最终的走向和结果。到这里我们都是讨论的直接显示机制。然而seller是可以设计其他不同的auction game的，在一个广义的auction game下，每一个bidder都存在一个策略的选择集合$\Theta_i$同时存在一个输出函数：
$$
\hat{p}: \Theta_{1} \times \cdots \times \Theta_{n} \rightarrow \mathbb{R}^{n} \quad \text { and } \quad \hat{x}: \Theta_{1} \times \cdots \times \Theta_{n} \rightarrow \mathbb{R}^{n}
$$
一个auction mechanism是这样的一个auction game和一个关于strategic plans的并集，一般来说这个strategic plan可以写为：$\hat{\theta}_i:[a_i,b_i]\rightarrow \Theta_i$，其中$\hat{\theta}_i(t_i)$表示的是如果他的value estimate表示为$t_i$的情况下他期望在这个auction game中使用的策略。在这样的描述下，我们可以将直接显示性机制表示为：$\Theta_i=[a_i,b_i],\hat{\theta}_i(t_i)\equiv t_i$.

**Lemma 1.** 显示性原理：给定任意一个可行的auction mechanism，存在一个等价的可行的直接显示性机制可以达到跟那个任意的auction mechanism相同的seller的以及bidders的期望收益。

#### Analysis of the problem

给定一个auction mechanism $(p,x)$，我们定义：
$$
Q_i(p,t_i)=\int_{T_{-i}}p_i(t)f_{-i}(t_{-i})\mathrm{d}t_{-i}
$$
对于任意一个bidder $i$以及其value estimate $t_i$, $Q_i(p,t_i)$表示的是bidder $i$在给定其$t_i$的情况下能够从这个机制$(p,x)$中获得item的条件概率分布。

**Lemma 2.** $(p,x)$是可行的，当且仅当下面的条件得到满足：
$$
\begin{aligned}
&\text{if}\quad s_i\leq t_i \quad \text{then} \quad Q_i(p,s_i)\leq Q_i(p,t_i),\quad \forall i\in N,\quad \forall s_i,t_i\in [a_i,b_i]; \\
&U_i(p,x,t_i)=U_i(p,x,a_i) + \int_{a_i}^{t_i}Q_i(p,s_i)\mathrm{d}s_i,\quad \forall i\in N,\quad \forall t_i\in [a_i,b_i];\\
&U_i(p,x,a_i)\geq 0,\quad \forall i\in N\\
&\sum_{j\in N}p_j(t)\leq 1\quad \text{and}\quad p_i(t)\geq 0, \quad i\in N, \quad \forall t\in T.
\end{aligned}
$$
*Proof.* 基于前面我们对于$v_i(t)$的假设：$v_i(t)=t_i+\underset{j\in N\atop j\neq i}{\sum}e_j(t_j)$, 我们可以导出：
$$
\begin{align}
&\int_{T_{-i}}(v_i(t)p_i(t_{-i},s_i)-x_i(t_{-i},s_i))f_{-i}(t_{-i})\mathrm{d}t_{-i}\\
=&\int_{T_{-i}}((v_i(t_{-i},s_i)+(t_i-s_i))p_i(t_{-i},s_i)-x_i(t_{-i},s_i))f_{-i}(t_{-i})\mathrm{d}t_{-i} \\
=&U_i(p,x,s_i) + (t_i-s_i)Q_i(p,s_i)
\end{align}
$$
