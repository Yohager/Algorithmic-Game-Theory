## Incentive-Compatible Diffusion Auction

### 摘要

Diffusion Auction是一种非典型性的多维度机制设计问题。当将agents之间的社交关系纳入这个auction问题的考虑中时，我们会发现这种情境下的IC机制需要保证其满足实报同时还必须向所有的邻居节点报告这场拍卖的信息。

这篇文章给出了一个diffusion auction设计DSIC机制的充分必要条件的归纳说明。主要关键点有：在多维度机制设计情境下考虑分配规则的单调性；任何一个单调的分配规则都是能够导向DSIC的diffusion auction的；更进一步，当给出一个确定的分配规则时，我们可以找到最优的付款机制来使得卖家的收益最大化。

### Preliminary

**定义一**：一个在图$G$上的传播拍卖机制$\mathcal{M}=(\pi,x)$包含两个部分，分配规则$\pi=\{\pi_i\}_{i\in N_{-s}}$, 支付规则$x=\{x_i\}_{i\in N_{-s}}$. 其中$\pi_i:T\rightarrow \{0,1\}$, $x_i:T\rightarrow \mathcal{R}$是关于agent $i$的分配函数和支付函数。

社会福利定义为：$W(\pi,t') = \sum_{i\in N_{-s}}\pi_i(t')v_i'$

定义一个efficient分配规则$\pi^\ast$：最大化$W(\pi^\ast,t')$

**定义二**：如果对于所有的$t'\in T$, 都有$\pi^\ast\in \arg\max_{\pi'\in\Pi}W(\pi',t')$. 则称这个分配规则是efficient的。

拟线性收益：$u_i(t_i,t',(\pi,x)) = \pi_i(t')v_i - x_i(t')$

**定义三**：对于一个传播拍卖机制$(\pi,x)$，如果对于所有的$i\in N_{-s}$,$r'_i\in \mathcal{P}(r_i)$, 以及$t'_{-i}\in T_{-i}$, 都有$u_i(t_i,((v_i,r'_i),t'_{-i}),(\pi,x))\geq 0$，那么则称这个传播拍卖机制是IR的。

**定义四**：对于一个传播拍卖机制$(\pi,x)$, 如果对于所有的$i\in N_{-s}, t'_i\in T_i,t'_{-i}\in T_{-i}$，都有$u_i(t_i,(t_i,t'_{-i}),(\pi,x))\geq u_i(t_i,(t'_i,t''_{-i}),(\pi,x))$，那么则称这个传播拍卖机制是IC的。

卖家的收益等于：$Rev^{\mathcal{M}}(t')=\sum_{i\in N_{-s}}x_i(t')$

**定义五**：对于一个传播拍卖机制$(\pi,x)$，如果对于所有的$t'\in T$都有$Rev^{\mathcal{M}}\geq 0$, 则称这个传播拍卖机制是弱收支平衡的。

### Incentive-Compatible Diffusion Auctions

一般来说，如果对于一个分配规则$\pi$，存在一个支付规则$x$使得这个机制$(\pi,x)$是一个IR且IC的，那么就定义这个allocation rule是implementable的 。

引出critical bid的概念，超过这个价格或者低于这个价格，$i$会得到或者失去这个item. 

**Theorem 1**: Myerson's Lemma: 单物品拍卖的环境下，没有信息传播的过程。

(a). 当且仅当一个分配规则是值单调时我们称这个分配规则$\pi$是implementable的。

(b). 如果一个分配规则$\pi$是值单调的，那么就会存在一个唯一的付款机制$x$, 使得机制$(\pi,x)$是IR且IC的，同时赢家支付其critical bid，输家支付为0.

在diffusion auction的情境下，给定任意一个$r'_i\subseteq r_i$，都存在一个最小的bid使得$i$获胜。因此对于每一个agent来说，他的critical bid是一个关于自己传播情况的函数。

**定义六**：给定一个分配规则以及其他所有buyers的汇报type $t'_{-i}$，我们定义$i$的critical bid为：$v_i^\ast(r_i') = \arg\min_{b_i'\in \mathcal{R}_{\geq 0}}\{\pi_i((b_i',r_i'),t_{-i}') = 1\}$

考虑单物品的拍卖时，一个买家要么赢得item，要么拿不到item。因此我们认为这个payment可以分解为两个部分，赢得商品($x_i(t'|\pi_i(t')=1$)的payment和输掉商品($x_i(t'|\pi_i(t')=0)$)的payment。我们定义$\tilde{x}(t_i',t'_{-i})=x_i(t'|\pi_i(t')=1)$，$\bar{x}(t_i',t_{-i}')=x_i(t'|\pi_i(t')=0)$.

**性质一**：payment分解：给出一个机制$(\pi,x)$，对于所有的$i$以及$t'_{-i}$，$i$的payment可以分解为$x_i(t')=\pi_i(t')\tilde{x}_i(t'_i,t'_{-i})+(1-\pi_i(t'))\bar{x}_i(t_i',t'_{-i})$.



