### Incentive Diffusion with Fair Rewards

---

#### Abstract

IDM的solution是给网络中的一些割点一些reward从而达到让seller的所有邻居节点都去如实地向周围节点传递auction的信息，但是在实际的网络中往往这类的割点存在的比较少，也就是说实际中的很多网络比较稠密，从而导致大部分的节点不愿意分享信息。因此本文提出一种新的机制来解决这个问题，这个机制奖励了更多的相关节点同时还保证了seller的收益。

#### Introduction

根据小世界网络的理论，在网络中一个点能够成为割点的几率是非常低的，因此IDM的激励方式可能会导致无法激励所有节点去传播auction的信息。这篇文章提出一个新的机制，这个机制不仅奖励cut-points，而且奖励那些不是割点但能够与其他非割点一起让winner无法到达seller. 这些节点相对于割点的重要性降低了但是对于winner和seller之间也是很重要的。为了处理这个问题，我们借用了一些来自redistribution mechanism design方面的知识，人们提出了很多的redistribution mechanism来将剩余money从seller手中重新分配给buyers. redistribution mechanism的目标是为了满足预算收支平衡的问题。这里仅仅借鉴redistribution mechanism的思想来对更多的buyers进行奖励。第二章陈述基本的问题；第三章介绍新的机制同时对比之前的机制；第四章陈述新机制的关键性质；最后一章给出总结。

#### Preliminaries

图$G=(V,E)$，其中$V=N\cup\{s\}=\{1,2,\cdots,n\}\cup\{s\}$. 每一个$i\in V$有一个$d_i>0$表示$i$到$s$的最小距离。对于每一个$i\in N$, 定义$\theta_i=(v_i,r_i)$表示$i$的type. 定义$i$的report type为$a_i=(v_i',r_i')$.  一个diffusion auction$\mathcal{M}$定义为一个分配规则$\pi=(\pi_1,\pi_2\cdots,\pi_n)$和一个支付规则$p=(p_1,p_2,\cdots,p_n)$. 其中$\pi_i:\Theta\rightarrow\{0,1\}$, $p_i: \Theta\rightarrow \mathbb{R}$. 对于$i$号buyer来说其收益等于$u_i(\theta_i,a)=\pi_i(a)v_i-p_i(a)$. 其他基本的定义与之前的大多数文章中的定义都是一样的，包括feasible，efficient，IR, IC等不多赘述。

#### Fair Diffusion Mechanism

这一章主要介绍FDM机制，在介绍机制之前首先引入多个概念：

**Definition 6.** 给定一个可行的profile $a\in \mathcal{F}(\theta)$，对于每一个buyer $i\in N$来说如果在没有集合$D_i\subseteq N$参与到这个auction的情况下不存在一条从$i$到$s$的路径，则我们称$D_i$是一个关于节点$i$的割集。如果不存在任何一个$D_i'\subset D_i$是的$D_i'$也是$i$的一个割集，那么我们就称$D_i$是关于$i$号buyer的一个**最小割集**。 

**Definition 7.** 给定一个可行的profile $a\in \mathcal{F}(\theta)$，对于任意一个buyer $i,j\in N$，如果$j$是$i$的某一个最小子集中的节点，那么我们定义$j$是$i$的**critical ancestor**.

**Definition 8.** 给定一个可行的profile $a\in \mathcal{F}(\theta)$，对于任意一个buyer $i,j\in N$, 如果$j$单独构成了$i$的一个最小割集，那么就称$j$是$i$的一个**strong critical ancestor**，对于那些是关于$i$的critical ancestor但是不是strong critical ancestor的节点都定义为**weak critical ancestor**. 

![FDM critical ancestors](FDM_1.png)

如上图所示所有的着色点都是节点$m$的critical ancestors, 浅黄色的节点都是weak critical ancestors同时深橘色的点表示的$m$的strong critical ancestors. 直觉上来说strong critical ancestors都是割点而其他点都是连接割点的节点. 

**Definition 9.** 给定一个可行的profile $a\in \mathcal{F}(\theta)$，对于任意一个buyer $i,j\in N$, 如果$i$是关于$j$的一个strong critical ancestor，那么我们认为$j$是$i$的一个**critical descendant**，定义$V_i=\{j|j\text{ is }i'\text{s }\text{critical descendant},j\in N\}$表示buyer $i$的**critical descendant set**. 类似地对于任意一个集合$K\subseteq N$，如果$K$是$j$的一个割集，那么我们定义$j$是$K$的critical descendant，定义$V_K=\{j|j\text{ is }K'\text{s }\text{critical descendant},j\in N\}$表示集合$K$的critical descendant set.

根据上面的定义我们很容易得到$N_{-i}=N\backslash V_i$以及$N_{-K}=N\backslash \cup_{i\in K}V_i$. 下图给出一个示例：

![FDM critical descendants](FDM_2.png)

如上图所示，$V_b=\{e,f,g,h,j,k,i,m,n\}$, $N_{-b}=\{a,d,c,i\}$.

**Definition 10.** 给定一个可行的profile $a\in \mathcal{F}(\theta)$，对于任意一个buyer $i\in N$, 定义$C_i$表示节点$i$的strong critical ancestor sequence. 写为$C_i=\{c_1^i,c_2^i,\cdots,c^i_k\}$，其中$c^i_k=i$. 对于任意一个$c_j^i\in C_i$, 定义顺序规则由depth决定$d_{c_1^i}\leq d_{c_2^i}\leq \cdots,\leq d_{c_k^i}$. 

**Definition 11.** 给定一个可行的profile $a\in \mathcal{F}(\theta)$，对于任意的$c_i,c_{i+1}\in C$, 定义$M_{c_ic_{i+1}}$表示节点$c_i$和$c_{i+1}$之间的weak critical ancestor set.  记作$M_{c_ic_{i+1}}=\{m^1_{c_ic_{i+1}},m^2_{c_ic_{i+1}}\},\cdots,m^k_{c_ic_{i+1}}$, 其中$v_{m^1_{c_ic_{i+1}}}\geq v_{m^2_{c_ic_{i+1}}}\cdots\geq v_{m^k_{c_ic_{i+1}}}$. 其中每一个节点$m^j_{c_ic_{i+1}}\in M_{c_ic_{i+1}}$都是$i$的一个weak critical ancestor，同时这个节点还在节点$c_i$和$c_{i+1}$的一条simple路径上。

以图2(a)为例，其中$m$是最高报价者，关于节点$m$的strong critical ancestor sequence表示为$C=\{b,l,m\}$. $M_{bl}=\{f,g,h,j,k\}$, $M_{lm}=\empty$.

##### Fair Diffusion Mechanism

给定一个可行的action profile $a\in \mathcal{F}(\theta)$, 找到最高报价者$h\in \arg\max_{i\in N}v_i'$. 