## Diffusion and Auction on Graphs

### 摘要

卖家收益（seller's revenue）和分配有效性（allocation efficiency）的冲突。

拍卖情景扩展到网络上同时提出IDM机制满足激励相容（IC），进一步提出在社交社会网络中的拍卖机制设计。

### Introduction

在拍卖机制设计中的两个重要的目标：最大化社会福利（最大化所有参与者的收益）；拍卖者的收益。

拍卖情景的扩展：除了花费金钱做宣传外如何让更多的人参与到这个拍卖中？

一个自然的解决方式：如何让原本参与在这个拍卖中的买家自愿将这个信息分享给更多的人？

这篇文章的主要内容包括：第一部分：在无权图上提出了一种新的类别的拍卖机制：**critical diffusion mechanism** （CDM）（其中IDM机制是这类机制的一种特例，且其是收益最低的一种情况）；第二部分：在带权图上提出了**weighted diffusion mechanism**（WDM）

在这两种情境下，每一个参与买家的最优策略均为实报+将拍卖信息传递给他的所有邻居。

### Preliminaries

拍卖情景：digraph：$G=(V,E)$, $|V|=n$, seller: $s$, 图中的其他节点：$i$: $t_i(v_i,r_i)$，其中$v_i$表示节点$i$对于item的估值，$r_i$表示为节点$i$的邻居集合。节点$i$只能通过存在的链接$(i,j)\in E$进行交流。初识情况下，只有$s$的邻居节点拥有拍卖的信息。

$w(i,j)$表示节点$i,j$之间连边的权重

问题情境：$t_i=(v_i,r_i)$表示节点$i$的私人type，$t=(t_1,\cdots,t_n)$表示所有节点的types集合，假定$t_{-i}=\{ t_1,t_2,\cdots,t_{i-1},t_{i+_1},\cdots,t_n \}$表示除去节点$i$的所有节点的types，即$t=(t_{-i},t_i)$，假定$T_i=\mathbb{R}_{\geq0}\times \mathbb{P}(V)$表示节点$i$的type空间。其中$\mathbb{P}(V)$是节点集$V$的幂集，$T$表示所有节点的profile的types的空间。$t'_i=(v'_i,r'_i)\in T_i$为节点$i$自己报告出去的type.

**定义一**：给定一个汇报给seller的type profile为$t'$，定义从seller到节点$i$的trading path为$(a_1,a_2,\cdots,a_{l},a_{l+1}=i)$,其中$a_1\in r_s$同时对于$1< j<l+1$,均有$a_j\in r'_{a_{j-1}}$. 

在所有的从seller到i的trading path中定义最短的那一条为$L^*_i(t')$，即$L^*_i(t')=\arg \min_{L\in\mathbb{L}_i(t')}\sum_{(i,j)}\in L w(i,j)$，其中$\mathbb{L}_i(t')$是关于节点$i$所有的可能的trading path.

**定义二**：传播拍卖可以定义为$\mathcal{M}=(\pi,x)$，其中$\pi$表示为分配规则：$T\rightarrow \mathbb{L}$,其决定了一个唯一的trading path，其尾节点为分配得到物品的买家；$x$表示为付款规则，$x=\{x_i\}_{i\in V\backslash \{s\}}$，每一个节点都会有一个付款规则。

在传播拍卖中的社会福利定义为$v(\pi(t))-\sum_{(i,j)\in \pi(t)}w(i,j)$

关于社会福利的问题，一般情况下单物品的社会福利表示为$\sum_{i\in B}v_i x_i$，这里的传播拍卖中需要考虑物品传播过程的外部效应的影响。不变的一点在于对于所有的分配规则，$\pi*$必须满足对每一个$t\in T$都是社会福利最大化的，即$\pi^*\in \arg \max_{\pi'\in \Pi}v(\pi'(t))-\sum_{(i,j)\in \pi'(t)}w(i,j)$

其中$\Pi$表示可实行的分配规则，使用$W^*(t)$表示有效分配规则下的社会福利。

关于所有的节点来说，我们认为其收益函数满足一个近似线性的函数，在给定一个节点$i$的真实type为$t_i$，同时给予整体的$t'$的分配方式，那么对于$i$来说其收益被定义为：$u_i(t_i,t',(\pi,x))=v_iz_i(t')-x_i(t')$

diffusion auction中关于IR的定义：实报价格，任意传播方式下，对于每一个节点都能保证其收益非负。($u_i(t_i,((v_i,r_i'),t_{-i}')(\pi,x))\geq	0$)

diffusion auction中关于IC的定义：实报type对于每一个节点来说都是他们的dominant strategy即：$u_i(t_i,(t_i,t_{-i}'),(\pi,x))\geq u_i(t_i,(t_i',t_{-i}'')，(\pi,x))$ for all $i \in V\backslash \{s\}$

给定一个diffusion auction情境下的上报的type profiles为$t'$和机制$\mathcal{M}=(\pi,x)$,卖家的收入定义为$Rev^{\mathcal{M}}(t')=\sum_{i\in V\backslash \{s\}}x_i(t')-\sum_{(i,j)\in \pi(t')}w(i,j)$

###  Auction Mechanism on Unweighted Graph

关键传播节点(critical diffusion nodes)：对于节点$i$来说，其关键传播节点表示如果缺少该节点则$i$无法参与这场auction中。

定义：$C_i(t)'=\{ \cap L \}_{L\in\mathbb{L}_i(t')}$为节点$i$的关键传播节点集合。



