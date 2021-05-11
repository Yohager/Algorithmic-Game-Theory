### Sybil-proof Answer Querying Mechanism 

---

#### Abstract

社交网络中的问询问题，一个requester希望在网络中有agents能够给出问题的解。目标是设计激励机制使得参与者能够将这个问询的消息传播出去，现有一些关于这方面的机制都是不能够满足false name attack的。这篇文章首先给出了关于匿名攻击的一些不可能的结论，然后引入了一类新的机制能够满足防匿名和一些其他性质。另外文中也分析了关于cost minimization的问题。

#### Introduction

社交网络下的answer/resourse querying mechanisms via a social network存在两个难点，一个是requester只能够向周围的人寻求帮助，因此他需要一种能够让更多人知道自己的问题的方式从而获得一个答案。这个可以通过激励他的邻居传播信息给邻居的邻居。关于这个diffusion incentive的难点，有如下的一些解决方案：

"FOCS 05 Query incentive networks"

"EC 07 On threshold behavior in query incentive networks"

"CIKM 10 Threshold behavior of incentives in social networks"

"AGT 07 Cascading behavior in networks: Algorithmic and economic issues"

第二个难点是Sybil-proof的问题，也就是匿名攻击。

这篇文章给出了一种在问询网络下的占优策略的中心化的防匿名攻击的激励机制。

#### Model

首先对这个问题进行建模。我们考虑一个问询场景的设定，一个问询者$r$在一个agents的集合中寻找答案。这些agents通过社交网络联系在一起。传播过程构成了一棵树$T=(V,E)$. rooted at $r$. edge $(i,j)\in E$表示agent $i$将信息传递给了agent $j$. 对于网络中的每一个agent $i\in T$, 令$p(i)$表示为$i$的直接parents, $s(i)$表示$i$的直接children.

denote给出答案那个人为winner $w$，显然$w\neq r$，假设有多个提供答案的人我们在depth最小的人中随机选择一个。给出一个从winner $w$到requester $r$的winning path，$p_w=(i_1,i_2,\cdots,i_n)$.

***Definition 1*** 一个reward mechanism被称为path mechanism如果满足下面的两个条件：

1. 只有在winning path上的agents才有可能得到非零的收益。
2. 一个在winning path上的agent的reward只取决于depth和路径的长度。

***Definition 2*** incentive compatiable (IC) 的定义: $x_i\geq x_i'\quad\forall i\in N$

1. $x_i$表示agent在知道答案的情况下实报自己知道答案这件事情得到的收益；或者如果不知道答案的情况下将这个信息传递给他所有的邻居节点下的收益。
2. $x_i'$表示在其他情况下的收益。

***Definition 3*** individual rational (IR) 的定义： $x_i\geq 0,x(j,n) \geq 0$对于所有的agent $i$都成立。SIR表示强个体理性，将等号去掉。

***Definition 4*** budget constrained (BC) ： if there exist a constant $B<\infty$ such that: 
$$
\sum_{i\in p_w}x_i = \sum_{j=1}^n x(j,n)\leq B
$$
for all querying network $T$, for all winning path $p_w$ of length $n$ in T.

***Definition 5*** Sybil-proof (SP) ：这里的匿名攻击我们只考虑在winning path上的agents，他们匿名攻击的方式为扩充从agent $p(i)$到$s(i)$的这一段距离。如果对于任意的winning path：$p_w=(i_1,i_2,\cdots,i_n)$，如果一个agent $i_j\in p_w$扩展了$p_w$，添加了$m$个匿名账户来得到了一个新的winning path：$p_w'=(i_1,\cdots,i_{j-1},i^0_j,i^q_j,\cdots,i_j^m,i_{j+1},\cdots,i_n)$. 
$$
x_{i_j}=x(j,n)\geq \sum_{k=0}^m x'_{i_{j}^k} =\sum_{k=0}^m x(j+k,n+m)
$$

> A path mechanism is Sybil-proof if and only if:
> $$
> x(j,n)\geq x(j,n+1) + x(j+1,n+1)
> $$

*Proof* 必要性是显然的，下面主要证明充分性：
$$
\begin{split}
x(j,n) &\geq x(j,n+1) + x(j+1,n+1)\\
&\geq [x(j,n+2)+x(j+1,n+2)] + [x(j+1,n+2)+x(j+2,n+2)]\\
&\geq \cdots\\
&\geq \sum_{k=0}^m \binom{m}{k} x(j+k,n+m)\\
&\geq \sum_{k=0}^m x(j+k,n+m)
\end{split}
$$
***Definition 6*** 一个path mechanism是防合谋的 ($\lambda-$collusion--proof) ($\lambda-CP$)如果满足：
$$
x(j,n)\leq \sum_{k=0} ^{\lambda'-1}x(j+k,n+\lambda'-1)
$$
如果$\lambda$-CP对于所有的$\lambda >1$都成立，即：
$$
x(j,n) \leq \sum_{k=0}^m x(j+k,n+m)
$$
则我们将这个机制称为是collusion-proof.

（任何的agents的联盟都无法通过将多个节点看作单个节点来获得更高的收益。）

***Definition 7*** 一个path mechanism是$\rho-\text{split secure}$ ($\rho-$SS) $\rho \in (0,1)$如果对于所有的agents $i_j\in p_w\setminus \{w\}$, $x_{i_j}\geq \rho x_{i_{j+1}}$. i.e. $x(j,n)\geq \rho x(j+1,n)$. 

基于上面给出的这些个定义我们就可以得到新的结论，给出这个引理Lemma 1.

> SIR,SP and $\lambda-$CP ($\lambda \geq 3$) are compatible. 

证明可以通过SP和CP的定义出发，导出满足条件的SP和$\lambda-$CP的结果一定为$x(j+1,n+\lambda-1)=0$，也就是说存在winning path上的agent的收益为0，与SIR的定义是矛盾的。

即使我们放宽SIR的条件为IR，我们得到的结果是存在满足SP和CP的机制，但是是一种十分特殊的机制：two-headed mechanism. 

> A path mechanism called two-headed mechanism if its reward function satisfies:
> $$
> x(j,n)=\begin{cases}
> a+b & \text{if  } j=1 \text{ and } n = 1\\
> a & \text{if  } j=1 \text{ and } n > 1\\
> b & \text{if  } j=n \text{ and } n > 1\\
> 0 & \text{otherwise}
> \end{cases}
> $$

直觉上来说：一个two-headed mechanism只将reward分配给winning path上的第一个agent和最后的winner，其他人的收益均为0.

