### Incentive Mechanisms for Crowdsensing: Crowsouring with Smartphones

---

引入了两个激励模型：crowdsourcer-centric model和user-centric model

##### Crowdsourcer-Centric Model

total reward is $R$ and motivate $n$ 个用户参与

在这个模型中，数据搜集者只有一个task和一个固定的reward，每个user的profile是$t_i$，表示可以上传数据的时间，同时每个用户有一个自己的成本$k_it_i$. 对于用户$i$来说收益表示为：
$$
\bar{u}_i=\frac{t_i}{\sum_{j\in \mathcal{U}}t_j}R-k_it_i
$$
对于数据搜集者来说，其收益表示为：
$$
\bar{u}_0=g(\tilde{t}_1,\tilde{t}_2,\cdots,\tilde{t}_l;n_1,n_2,\cdots,n_l)
$$
其中$\bar{u}_0$是关于每一个$t_i$单调递增的。

**Incentive Mechanism 1**: 使用一个stackelberg game  (IMCC game), 分为两个阶段：数据搜集者首先公布reward $R$，然后选择自己的关于可搜集数据时间的策略来使得自己的收益最大化。

对于users来说，STD game (IMCC game)的第二阶段一定存在一个唯一的纳什均衡，同时文章给出了计算这个纳什均衡的算法；对于数据搜集者来说，IMCC game整个过程一定存在一个stackelberg均衡同时也给出了算法来计算这个均衡。

求解均衡的方式和一般的解博弈是类似的：

找到best response strategy: 对于每一个$u_i$，对$t_i$求偏导数找极值点：
$$
\frac{\part \bar{u}_i}{\part{t_i}}=\frac{R}{\sum_{j\in \mathcal{U}}t_j}-\frac{Rt_i}{(\sum_{j\in \mathcal{U}}t_j)^2} -k_i
$$
同时可以计算二阶偏导数是负值，从而如果存在一个best response那么其一定是唯一的。

令一阶偏导数为0计算得到：
$$
t_i=\sqrt{\frac{R\sum_{j\in \mathcal{U_{-i}}}t_j}{k_i}}-\sum_{j\in \mathcal{U}_{-i}}t_j
$$

Algorithm for computation of NE:

首先根据cost和该cost下满足条件的人的数量在满足某些条件的前提下我们将其加入到winner的集合中。

 计算对应的均衡下的每个winner被用于采集数据的时间：
$$
t_i^{ne}=\frac{(|S|-1)R}{\sum_{j\in S}k_j}\left(1-\frac{(|S|-1)k_i}{\sum_{j\in S}k_j}\right)
$$
Crowdsensing Utility:

对于crowdsenser来说，他的收益可以表示为：
$$
\bar{u}_0=g(X_1R,X_2R,\cdots,X_lR;n_1,n_2,\cdots,n_l)-R
$$
其中所有的$X_j$我们可以写为：
$$
X_j=\begin{cases}
\frac{(n_0-1)}{\sum_{\theta_k\in \Theta_w}n_k\theta_k}\left(1-\frac{(n_0-1)\theta_j}{\sum_{\theta_k\in \Theta_w}n_k\theta_k}\right) & \theta_j\in \Theta_w\\
0&\theta_j\notin\Theta_w
\end{cases}
$$

##### User-Centric Model

 以用户为中心的模型中，crowdsourcer公布一个任务的集合$\Gamma=\{\tau_1,\tau_2,\cdots,\tau_m\}$, 这些任务供给用户进行选择，每一个任务$\tau_j\in \Gamma$对于机制设计者来说都会有一个value $v_j>0$. 用户$i$根据自己的偏好选择一个任务子集$\Gamma_i\subseteq \Gamma$. 对于user $i$ 有一个相关的花费$c_i$, 用户$i$提交的内容是一个task-bid $(\Gamma_i,b_i)$. 注意这个$b_i$表示的是用户$i$的保留价。

用户$i$的收益表示为：$\tilde{u}_i=p_i-c_i$ when $i\in \mathcal{S}$. 对于crowdsourcer来说其收益为：$\tilde{u}_0=v(\mathcal{S})-\sum_{i\in \mathcal{S}}p_i$. 其中$v(\mathcal{S})=\sum_{\tau_j\in \cup_{i\in \mathcal{S}}\Gamma_i}v_j$. 

<font color=red>An analysis of approximations for maximizing submodular set function</font>这篇文章中提到了一个很重要的结论，如果对于一个收益函数$u$来说，满足次模性，单调性和非负性那么我们就可以找到一个贪心的算法来得到$(1-1/e)$的近似结果。

<font color=red>Maximizing non-monotone submodular functions</font>这篇文章给出满足次模性且非负的但是不满足单调性的收益函数的近似算法。

这篇文章就是基于这个思想给出了local search based auction.

算法的流程大致如下：

> **Alogrithm 2**: Local Search Based Auction
>
> 1. 找到能够最大化$f(\{i\})$的那个bidder $i$，将其添加到$S$集合中。
> 2. 将所有满足$i\in \mathcal{U}\backslash S$且存在$f(S\cup\{i\})>(1+\frac{\epsilon}{n^2})f(S)$的那些bidders都添加到集合$S$中
> 3. 如果存在$i\in S$同时$f(S\backslash\{i\})>(1+\frac{\epsilon}{n^2})f(S)$那么就将这个$i$从$S$中去掉，同时返回第二步。
> 4. 如果$f(\mathcal{U}\backslash S)>f(S)$, 那么就令$S=\mathcal{U}\backslash S$.
> 5. 对于每一个在集合$S$中的bidder，都令$p_i=b_i$，即令他们酬劳等于他们自己上报的保留价格
> 6. 最后返回集合$S$和所有的payments.

**[性质]**：

- 可计算性：这个算法的时间复杂度为$O(\frac{1}{\epsilon}n^3m\log m)$，多项式时间算法。
- 是否IR：考虑机制设计者支付的是每一个bidder自己报出来的保留价，显然满足IR的性质。
- 是否WBB：是WBB的，因为我们一开始假设了一定存在一个$i$使得$\tilde{u}_0(\{i\})>0$满足，那么对于机制设计者来说是不会亏钱的。
- 是否IC：不是IC的，有高报的倾向。

针对这个LSB Auction并不是truthful的问题，之后文中提出了另外一种auction的机制。

IMCU Auction

>**Algorithm 3** IMCU Auction
>
>1. 找到最大化$i\leftarrow \arg \max_{j\in \mathcal{U}}(v_j(\mathcal{S}-b_j))$
>2. 如果对于$i$来说，其满足$b_i<v_i$同时集合$\mathcal{S}\neq \mathcal{U}$, 那么我们将bidder $i$添加到集合$\mathcal{S}$中同时找到这样一个新的$i$, 反复重复这个过程直到找不到这样的一个$i$为止。
>3. 对于所有的$i$初始化他们得到来自于机制设计者的支付值为$p_i\leftarrow 0$.
>4. 对于每一个$i\in \mathcal{S}$: 首先初始化$\mathcal{U}_{-i}\leftarrow \mathcal{U}\backslash\{i\},\mathcal{T}\leftarrow \empty$，然后重复如下过程：令$i_j$表示一个bidder，这个bidder满足$\arg\max_{j\in \mathcal{U}_{-i}\backslash\mathcal{T}}(v_j(\mathcal{T})-b_j)$; 令$p_i$等于$\max\{p_i,\min\{v_i(\mathcal{T})-(v_{i_j}(\mathcal{T})-b_{i_j}),v_i(\mathcal{T})\}\}$, 同时将$i_j$添加到$\mathcal{T}$集合中。这个过程一直循环进行直到$b_{i_j}\geq v_{i_j}$或者出现$\mathcal{T}=\mathcal{U}_{-i}$. 如果出现$\mathcal{T}=\mathcal{U}_{-i}$则令$p_i\leftarrow \max\{p_i,v_i(\mathcal{T})\}$.
>5. 返回$(S,p)$

注意其中的$v_i(\mathcal{S})$表示的是$i$的边际效益，即$v_i(\mathcal{S})=v(\mathcal{S}\cup\{i\})-v(\mathcal{S})$.