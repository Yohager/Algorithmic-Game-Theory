### Strategy Proof and Non-Wasteful Multi-Unit Auction via Social Network

---

#### 摘要

本文主要提出了一种满足strategy-proofness，non-deficit，non-wastefulness，IR的同质多物品单位需求量的auction的机制。同时对比了两种简单的机制，发现新机制的性质更加优异。包括社会福利，卖家收益，激励buyers说实话等等。

#### Preliminaries

$k$个相同物品的集合$K$，$n$个buyers的集合$N$. 其中每个agent都是要求一个单位的物品。定义$\bold{x}= (x_i)_{i\in N} \subset \{0,1\}^n$表示一种分配结果，$x_i=1$表示$i$得到一件item，$x_i=0$表示$i$没有获得商品。真实单位商品估值等于$v_i\in \mathcal{R}_{\geq 0}$，拟线性收益：$u_i=v_i\cdot x_i - p_i$. 

$r_i\subseteq N\backslash \{i\}$表示$i$的followers，定义拍卖网络$G=(N\cup \{s\},E)$，$i$的true type定义为：$\theta_i=(v_i,r_i)$，report type为$\theta_i'=(v_i',r_i')$. 如果基于$\bold{\theta}'$得到拍卖网络下的路径$s\rightarrow \cdots,\rightarrow i$，那么就认为$i$是connected. 定义$\hat{N}$为所有connected的buyers的集合。定义$d(i)$表示从$s$到$i$的最短路径的距离。定义$j$是$i$的关键parent，假设$j$不参与则$i$一定参加不了。定义$P_i(\bold{\theta}')\subseteq \hat{N}$表示的是在$\theta'$下的$i$的所有critical parents的集合。

定义一个机制$(f,t)$，其中$f$表示分配规则，$t$表示付款规则。

**定义一**：如果对于所有的$\theta'$都有$f(\theta')$是可行的，则认为机制$(f,t)$是可行的。

**定义二**：给定一个机制$(f,t)$和一个agent $i$，其真实type为$\theta_i=(v_i,r_i)$，假设一个report type $\theta^\ast=(v^\ast,r^\ast)\in R(\theta_i)$都有$v_i \cdot f(\theta^\ast,\theta'_{-i})-t_i(\theta^\ast,\theta'_{-i}) \geq v_i \cdot f(\theta',\theta'_{-i})-t_i(\theta',\theta'_{-i})$ 则这个$\theta^\ast$是一个占优策略. 如果实报对于$i$来说是一个占优策略，那么定义机制是IC的。

**定义三**：如果对于任意的$i,\theta_i$以及$\theta'_{-i}$，都有：$v_i\cdot f(\theta_i,\theta'_{-i})-t_i(\theta_i,\theta'_{-i})\geq v_i\cdot f(\theta_i',\theta'_{-i})-t_i(\theta_i',\theta'_{-i})$.

**定义四**：如果对于任意的$\theta'$都有$\sum_{i\in N}t_i(\theta')\geq 0$，则表示机制non-deficit.

**定义五**：如果对于任意的$\theta'$都有$\sum_{i\in N}f_i(\theta')\geq \min \{k,|\hat{N}|\}$.

两种简单的用于后续对比的机制，VCG和FCFS-F机制。

#### Distance-based Network Auction mechanism for Multi-Unit, Unit-demand buyers

我们定义一个重要的概念叫做*Diffusion Critical Tree*, 写作$T(\theta')$, $T(\theta')$中的节点由$\hat{N}$中节点以及他们的最小关键parent构成，边由传播的情况构成。给定一个$\theta'$, 一个子集$S\subseteq \hat{N}$，一个整数$k'\leq k$，定义$v^\ast(S,k')$表示在集合$S$中的第$k'$高的报价。如果$k'\leq 0$则$v^\ast(S,k')=\infty$; 如果$|S|\leq k'$则$v^\ast(S,k')=0$.

**定义六**：给定$\theta'$，将$\hat{N}$中的节点按照$d(i)$从小到大的顺序进行排序并在图中标号。给出$T(\theta')$，定义$i\notin \hat{N}$，$f_i(\theta')=0,t_i(\theta)=0$. 定义$\hat{N}_{-i}$表示所有connected节点的集合，给出算法流程：

> $k'=k,W\leftarrow \emptyset$
>
> for each $i\in \hat{N}$（按照距离的降序排列的顺序）do:
>
> ​	$p_i\leftarrow v^\ast(\hat{N}_{-i}\backslash W,k')$
>
> ​	if $v_i'\geq p_i$ then 
>
> ​		$f_i(\theta')\leftarrow 1,t_i(\theta')\leftarrow p_i$, $k'\leftarrow k,W\leftarrow W\cup\{i\}$
>
> ​	else:
>
> ​		$f_i(\theta')\leftarrow 0, t_i(\theta')=0$
>
> ​	end if
>
> end for

上面的算法流程就是DNA-MU机制的运行过程。

![Example for DNA-MU](example1.png)

左图为初始auction network，根据距离进行了编号。右图为$T(\theta)$.

假设共计有三个物品待拍卖。

下面以上图为例分析算法的实现流程：

从$i_1$开始分析，$p_1=v^\ast(i_2,i_3,i_4,i_5,i_6,i_7,3)=50$，而$v_1'=30<p_1$，因此$i_1$无法得到一件item，继续算法，$i_2$, $p_2=v^\ast(i_1,i_3,i_5,i_6,i_7,3)=40$，而$v_2'=72>p_2$，因此$i_2$得到一件item，将$i_2$加入到$W$集合中，$k'-1=2$，继续算法，重复上述的算法，最终会发现$\{i_2,i_3,i_5\}$最终获得了三件items，三个人的付款值分别为：40,30,45. 

<font color=black>存在的几点希望能够有改进的地方：</font>

<font color=red>1. 如何将CDM的思想放入这个算法中进行改进？是否这个改进点是可行的还有待考虑。</font>

<font color=red>2. 思考这个根据距离远近来进行分配的方式是否存在不DSIC的情况，能不能给出反例，或者说这个排序的地方是否可以改进</font>

<font color=red>3. 在i的报价低于p时是否存在i是一个获胜者的关键传播parent，此时应该不应该给i一些奖励？</font>

<font color=red>4. 能不能将这个算法扩展到Sponsor Search Auctions？</font>

##### DNA-MU的一些性质

定义$\hat{W}=\{w_1,w_2,\cdots\}$, 同时定义$\hat{W}_{\succ j}=\{w\in \hat{W}|w\succ j\}$.

**理论一**：DNA-MU满足可行性，IR以及non-deficit.

**理论二**：DNA-MU是non-wasteful的.

**理论三**：DNA-MU是IC的.

