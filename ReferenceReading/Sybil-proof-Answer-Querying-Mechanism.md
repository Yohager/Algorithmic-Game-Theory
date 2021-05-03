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

