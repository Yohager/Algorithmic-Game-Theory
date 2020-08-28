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

**定义七**：（值单调分配）如果对于任何一个$t'$和任何一个$i$，有$\pi_i((v'_i,r_i'),t'_{-i})=1$, 那么当$v_i'' > v_i'$时则会有$\pi_i((v_i'',r_i'),t_{-i}')=1$成立. 对于一个在这样的diffusion auction有这样分配规则存在，那么就称这个分配策略是值单调的。

 在给定了$t_{-i}'$以及$r_i'$的情况下，当且仅当$v_i'\geq v^\ast_i(r_i')$的情况下才会有$\pi_i((v_i',r_i'),t_{-i}')=1$. 

下面给出关于IC的diffusion auction需要满足值单调性的说明。

**Lemma 1**：如果一个diffusion auction $(\pi,x)$是IC的，那么它一定是值单调的。

*Proof*：反证法，假设存在$v_i^2>v_i^1$的情况下，有$\pi_i((v_i^1,r_i),t_{-i})=1$而$\pi_i((v_i^2,r_i),t_{-i})=0$. 对于两个types $t_i^1=(v_i^1,r_i)$和$t_i^2=(v_i^2,r_i)$，他们对应的支付分别为：$\tilde{x}_i(t_i^1)$与$\bar{x}_i(t^2_i)$. 如果有$v_i^1 - \tilde{x}_i(t_i^1) \geq 0 - \bar{x}_i(t_i^2)$, 那么agent $i$存在误报为$v_i^1$的倾向，因为这样的收益更高一些: $v_i^2-\tilde{x}_i(t_i^1) \geq v_i^1-\tilde{x}_i(t_i^1)>-\bar{x}_i(t^2_i)$. 类似地，如果存在$v_i^1 - \tilde{x}_i(t^1_i)<-\bar{x}_i(t^2_i)$时，那么agent $i$又有误报为$v_i^2$的倾向去失去这个商品。因为收益: $v_i^1\cdot 0 - \bar{x}_i(t^2_i) > v_i^1 \cdot 1 - \tilde{x}_i(t_i^1)$。由于在这两种情况下，agent $i$都存在更高收益的偏离当前的策略，那么这样一个diffusion auction就不是IC的，因此一个满足IC的diffusion auction一定是值单调的。

**定义八**：(Bid-Independent Decoupled-Payments). 如果对于所有的$t_{-i}'$以及任意的$i$的两种不同的报价的情况下$(v_i',r_i')$和$(v_i'',r_i')$，都有$\tilde{x}_i(v_i',r_i')=\tilde{x}_i(v_i'',r_i)$，$\bar{x}_i(v_i',r_i')=\bar{x}_i(v_i'',r_i')$.

**Lemma 2**：如果一个diffusion auction是IC的，那么对于支付$x$的分解的结果一定是bid-independent的。

*Proof*：这个结论很容易证明，对于两种不同的汇报types，$t_i^1=(v_i^1,r_i)$,$t_i^2=(v_i^2,r_i)$, 如果这两个汇报types都是满足能够获得一件item的，即$\min\{v_i^1,v_i^2\}\geq v^\ast(r_i)$，假设两种type下的支付结果不等，即要么假设存在$\tilde{x}_i(v_i^1,r_i) > \tilde{x}_i(v_i^2,r_i)$, 在这种情况下，在type $t_i^1=(v_i^1,r_i)$下的agent $i$有误报为$t_i^2(v_i^2,r_i)$的倾向，因为这样可以通过虚报降低他的payment. 同样的当变为loser时也就是$\max\{v_i^1,v_i^2\}$时，我们会有类似的结论，可以通过误报得到更高的收益。因此IC的diffusion auction一定需要满足bid-independent.

**Lemma 3**：如果一个diffusion auction是IC的，那么我们一定有对于所有的$t$和$i$，都会存在$\tilde{x}_i(r_i)-\bar{x}_i(r_i)=v^\ast(r_i)$.

*Proof*. 依旧使用反证法，假设我们有$\tilde{x}_i(r_i)-\bar{x}_i(r_i)\neq v^\ast(r_i)$, 则存在两种可能，要么$\tilde{x}_i(r_i)-\bar{x}_i(r_i) > v^\ast(r_i)$, 要么$\tilde{x}_i(r_i)-\bar{x}_i(r_i) < v^\ast(r_i)$. 对于前面一种情况下，那些汇报type为$t_i=(v^\ast(r_i),r_i)$的agents会想办法降低自己的报价使得自己输掉这场auction，因为输掉的收益更高即：$-\bar{x}_i(r_i) > v^\ast(r_i)-\tilde{x}_i(r_i)$. 而对于后一种情况：那些本身是输家的玩家会提高自己的报价使得自己的收益提升。

**定义九**：(Diffusion-Monotonic Decoupled-Payments). 如果对于所有的$i$以及所有的$t_{-i}'$，$r_i''\subseteq r_i'$, 我们都有$\tilde{x}_i(v_i',r_i'')\geq \tilde{x}_i(v_i,r_i')$同时$\bar{x}_i(v_i',r_i'') \geq \bar{x}_i(v_i',r_i')$. 那么我们就称支付$x$的两部分分解都是传播单调的。

**Lemma 4**：如果一个diffusion auction是IC的，那么支付规则$x$的分解部分都是传播单调的。

*Proof*. 假设存在一个IC的diffusion auction以及两个diffusion sets $r_i^2\subseteq r_i^1$, 如果 $\tilde{x}_i(r_i^2) < \tilde{x}_i(r_i^1)$，假设存在一个winner$(v_i,r_i^1)$，其中$v_i\geq \max\{ v^\ast_i(r_i^1),v^\ast_i(r_i^2) \}$，那么这个winner会希望误报为$(v_i,r_i^2)$，考虑这个winner原本的收益为：$u_i^1 = v_i - \tilde{x}_i(r_i^1)$，而假设误报的情况下收益变为：$u_i^2 = v_i - \tilde{x}_i(r_i^2)$. 而我们发现$u_i^2 >u_i^1$的，因此这是违背IC的，因此前面的假设$\tilde{x}_i(r_i^2)<\tilde{x}_i(r_i^1)$是错误的；类似的结论在对于$\bar{x}_i(r_i^2) < \bar{x}_i(r_i^1)$的假设下也是错误的。因此在一个IC的diffusion auction下支付规则$x$的分解部分都是传播单调的。

**Theorem 2**：假设一个diffusion auction$(\pi ,x)$是IC的，当且仅当对于所有的type profile $t$和所有的$i$，P1-P4都是满足的：

P1：$\pi$是值单调的

P2：$\tilde{x}_i$和$\bar{x}_i$是bid-independent.

P3：$\tilde{x}_i(r_i) - \bar{x}_i(r_i)=v^\ast_i(r_i)$

P4：$\tilde{x}_i$和$\bar{x}_i$都是传播单调的

*Proof*. 证明分为两步：（1）证明无动机偏离；（2）证明truthful导致的是最大化的收益。首先证明第一步无动机偏离，假设存在一个winner，他是实报的，当他想要误报使得自己从一个winner变成一个loser时，他的收益从：$v_i-\tilde{x}_i(r_i)$变为了$-\bar{x}_i(r_i')$. 而：$v_i-\tilde{x}_i(r_i) \geq v^\ast_i(r_i)-\tilde{x}_i(r_i)=-\bar{x}_i(r_i)\geq -\bar{x}_i(r_i')$. 所以作为一个赢家他是没有理由或者动机去偏离当前的策略；当存在一个实报的loser，他想误报使得自己从一个loser变为一个winner，他的收益变化为：$-\bar{x}_i(r_i)$变为$v_i-\tilde{x}_i(r_i')$. 而：$v_i - \tilde{x}_i(r_i')\leq v_i^\ast(r_i)-\tilde{x}_i(r_i')\leq v_i^\ast(r_i)-\tilde{x}_i(r_i)=-\bar{x}_i(r_i)$. 同样的实报的loser也没有动机去变成一个winner. 第二步证明truthful能够导出的收益是最大的收益：假设一个实报的winner，他的收益为：$v_i-\tilde{x}_i(r_i)$，假设他误报自己的type为$t_i'$，那么他的收益变化为$v_i-\tilde{x}_i(r_i')$，根据传播单调性我们可以知道这样做降低了他的收益，因此对于这个winner来说实报使得他的收益最大化，无论他如何改变自己的type都不会有超过实报的收益；对于一个实报的loser来说，他的收益是$-\bar{x}_i(r_i)$，他改变自己的type，如果依然是一个loser那么他的收益变为$-\bar{x}_i(r_i')$，根据传播单调性可知收益会出现下降，如果变成了一个winner，第一步中已经证明了这种情况下收益的下降，因此对于loser来说实报也是使得他的收益最大化的。

**Theorem 3**：一个diffusion auction是IR的当且仅当所有的$i$和$t$都满足性质五：$\bar{x}(\empty)\leq 0$.

*Proof*. 固定$t_{-i}$，那么$i$的收益为：$u_i(v_i,r_i)=\pi_i(v_i,r_i)(v_i-\tilde{x}_i(r_i))+(1-\pi_i(v_i,r_i))(-\bar{x}_i(r_i)) = \pi_i(v_i,r_i)(v_i - v_i^\ast(r_i))-\bar{x}_i(r_i)$. 最小化这个收益的结果是$-\bar{x}_i(r_i)$. 这个经过简单推理就可以得到，这里不多赘述。所以我们希望$-\bar{x}_i(r_i)\geq 0$恒成立，而根据传播的单调性又可以知道当$r_i'=\empty$时$-\bar{x}_i(r_i')$会取到最小的结果，即$-\bar{x}_i(\empty)\geq 0$，从而导出结论，当且仅当满足$\bar{x}_i(\empty)\leq 0$时diffusion auction才是IR的。

### Monotonic Allocation and Optimal Payment

在设计单调的分配策略和最优的payment策略时，遵循一个真实情境下的直觉，报价高且传播地少的人更加有可能获得auction的胜利。

对于一个参与者$i$，定义一个types的偏序关系，这个偏序关系满足：$(v_i^1,r_i^1)\succ (v_i^2,r_i^2)$当且仅当$v_i^1\geq v_i^2 \and r_i^1\subseteq r^2_i$. 

**定义十**：如果对于一个diffusion auction下的分配策略$\pi$存在当每一个$t_i$以及$\pi_i(t_i,t_{-i})=1$的情况下，对于任意的$t_i'\succ t_i$都有$\pi_i(t_i',t_{-i}')=1$. 那么就称这个分配策略是单调的。

**Lemma 5**：如果一个分配策略$\pi$是单调的，那么对于所有的$i$和$r_i'\subseteq r_i$来说，$v^\ast_i(r_i')\leq v^\ast_i(r_i)$.

*Proof*. 利用反证法，假设对于两种报价：$t_i=(v_i^\ast(r_i),r_i)$和$t_i'=(v^\ast_i(r_i),r_i')$，其中$r_i'\subseteq r_i$, 存在一个单调的分配策略$\pi$，使得$v^\ast_i(r_i')>v^\ast_i(r_i)$. 那么最终的分配结果就变为：$\pi_i(t_i)=1$同时$\pi_i(t_i')=0$，但是根据定义的偏序关系和定义十我们又知道$t_i'\succ t_i$，因此推出矛盾，证毕。

基于Lemma 5的结论，对于agent $i$来说他的关键报价函数是关于他的传播$r_i'$非递减的，而同时我们又知道payment分解的两个部分又是关于$r_i'$非递增的，有了这些，下面我们要引入非常重要的结论，任意一个单调的分配策略都是implementable的。

**性质二**：在diffusion auction中，任何的一个单调的分配规则都是implementable的。

*Proof*. 当且仅当对于任意的$t_{-i}$和任意的buyer $i$以及他的type $(v_i,r_i)$满足前面的P1-P5的属性, 一个diffusion auction能够满足IC和IR。给定一个单调的分配策略，则P1直接满足了，下面我们构建payment分解的两个部分：$\tilde{x}_i(r_i)=\tilde{f}_i(v^\ast_i(r_i)) + h_i(t_{-i})$, $\bar{x}_i(r_i)=\bar{f}_i(v^\ast_i(r_i)) + h_i(t_{-i})$, 其中$h_i(t_{-i})$独立于$i$上报的type，$\tilde{f}_i(v^\ast_i(r_i))$和$\bar{f}_i(v^\ast_i(r_i))$都是关于$v^\ast_i(r_i)$非递增的，同时还有$\tilde{f}_i(v^\ast_i(r_i))-\bar{f}_i(v^\ast_i(r_i))=v^\ast_i(r_i)$. 这样对于$\tilde{x}$和$\bar{x}$的构建满足P2-P4，一个可行的选择就是定义$\tilde{f}_i(v^\ast_i(r_i))=-\alpha v^\ast_i(r_i)$同时$\bar{f}_i(v^\ast_i(r_i))=-(1+\alpha)v^\ast_i(r_i)$. 其中的$\alpha$可以是任何的非负的值。设置$h_i(t_{-i})=(1+\alpha)v^\ast(\empty)$. 那么P5就能够得到满足。因此对于任意一个单调的分配策略来说，都会存在一个payment使得这个机制是IC且IR的，证毕。

上面的证明不难发现在给定一个单调的分配策略的前提下，支付规则的可选择空间是巨大的，因此下面就从卖家收益的角度来考虑这个支付规则的选择。

**定义十一**：给定一个单调的分配规则$\pi$和两个支付规则$x^1,x^2$. 两者均满足IR和IC，如果对于任意的type profile $t$来说都有$Rev^{(\pi,x^1)}(t)\geq Rev^{(\pi,x^2)}(t)$，则称$x^1$ dominate $x^2$.

**Theorem 4**：给定任意的单调的分配策略$\pi$，最优的支付规则是$x^\ast = \{x_i^\ast=v_i^\ast(\empty) - v^\ast_i(r_i)(1-\pi_i(t))\}_{i\in N_{-s}}$.

*Proof*. 对于任意的$t$与单调的分配策略$\pi$，卖家的收益可以写为：
$$
Rev(t)=\tilde{x}_w(r_w) + \sum_{i(\neq w)\in N_{-s}}\bar{x}_i(r_i)
$$
其中$w$表示赢得商品的人，其他人都是losers. 最优付款规则$x^\ast$需要满足最大化$Rev(t)$以及$(\pi,x^\ast)$是IC+IR的。而IC和IR是由P1-P5导出的。我们将$\tilde{x}_w(r_w)=\bar{x}_w(r_w)+v^\ast_w(r_w)$带入到$Rev(t)$中可以得到$Rev(t)=v^\ast_w(r_w)+\sum_{i\in N_{-s}}\bar{x}_i(r_i)$. 显然$v^\ast_w(r_w)$是一个常量，因此优化的目标变为：$x^\ast=\arg\max_{x}\sum_{i\in N_{-s}}\bar{x}_i(r_i)$. 而对于每一个agent，其payment是独立于其他agents的，因此我们将这个问题转换为了$|N|-1$个独立的优化子问题：
$$
\begin{split}
&\max_{(\tilde{x}_i,\bar{x}_i)} \bar{x}_i(r_i) \\
s.t.\quad &\forall v_i'\neq v_i'',r_i'\subseteq r_i\\
    &\bar{x}_i(v_i',r_i)=\bar{x}_i(v_i'',r_i)\\
    &\tilde{x}_i(r_i)=\bar{x}_i(r_i) + v^\ast_i(r_i)\\
    &\bar{x}_i(r_i) + v^\ast_i(r_i)\leq \bar{x}_i(r_i')+v^\ast_i(r_i')\\
   & \bar{x}_i(\emptyset)\leq 0

\end{split}
$$
根据约束三我们不难发现必须保证$\bar{x}_i(r_i) + v^\ast_i(r_i)\leq \bar{x}_i(\empty)+v^\ast_i(\empty)$, 改写一下：
$$
\bar{x}_i(r_i)\leq \bar{x}_i(\empty) + v^\ast_i(\empty) - v_i^\ast(r_i)
$$
而约束四会告诉我们$\bar{x}_i(r_i)$的上界为$v^\ast_i(\empty)-v^\ast_i(r_i)$.

因此最终$\bar{x}_i(r_i)=v^\ast_i(\empty) - v^\ast_i(r_i)$以及$\tilde{x}_i(r_i)=\bar{x}_i(r_i)+v^\ast_i(r_i)=v^\ast_i(\empty)$. 是一个可行的payment规则同时也是最优的结果。也就是说，要求winner支付$v^\ast_i(\empty)$同时要求loser支付$v^\ast_i(\empty)-v^\ast_i(r_i)$将会最大化卖家的收益。

最终得到$x_i^\ast = v^\ast_i(\empty)-v^\ast_i(r_i)(1-\pi_i(t))$. 证毕。

下面给出最后一个性质：

**性质三**：不存在一个IC且IR的diffusion auction是既满足efficient同时满足(weak)budget-balanced.

在给出这个性质的证明之前我们首先证明VCG机制的支付规则满足theorem4. 

**Lemma 6**：在VCG机制中，每一个agent的付款规则符合Theorem 4.

*Proof*. VCG机制中最高价者获得商品，每一个buyer支付的结果为：
$$
x_i^{vcg}(t)=W(\pi^\ast,t\backslash\{t_i\}) - (W(\pi^\ast,t)-\pi_i^\ast(t)v_i)
$$
其中不难发现：$W(\pi^\ast,t\backslash\{t_i\})=v^\ast(\empty)$，如果$i$没有赢得商品，第二项等于$W(\pi^\ast,t)-\pi_i^\ast(t)v_i=W(\pi^\ast,t)=v^\ast _i(r_i)$. 否则第二项应该就为0.

因此对于任意一个buyer $i$来说：
$$
\tilde{x}_i^{vcg}=W(\pi^\ast,t\backslash\{t_i\})=v^\ast_i(\empty)​
$$


同时：
$$
\bar{x}_i^{vcg}=W(\pi^\ast,t\backslash\{t_i\})-W(\pi^\ast,t)=v^\ast_i(\empty) - v^\ast_i(r_i)
$$
下面证明性质三：

首先Lemma 6证明了VCG机制是满足于Theorem 4的支付规则的，也就是说VCG机制实际上是满足了最大化卖家收益的，而之前的工作我们又说明了VCG是一个efficient但是不是weakly budget-balanced，因此性质三成立，证毕。

#### 结论和一些可扩展的方向

从一个很高的角度将IC的diffusion auction做了一个总结，类似迈尔森引理一样地给出了一套完整的关于IC diffusion auction的可行分配以及对应的最优支付规则的框架。未来探究的方向出现在其他的多参数环境下的拍卖机制，多物品下的diffusion auction的框架，online mechanism design的结合等等。







