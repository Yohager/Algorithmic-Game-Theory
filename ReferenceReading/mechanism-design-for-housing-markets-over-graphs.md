### Mechanism Design for Housing Market over Social Network

---

#### Model

Consider a networked housing market problem

a set of agents $N=\{1,\cdots,i,\cdots,n\}$.

a set of indivisible objects: $H=\{h_1,h_2,\cdots,h_n\}$.

初始状态下每个agent是拥有一个自己的house $h_i$.

在这个情境下一个机制的allocation可以认为是：$\bold{x}=\{x_i\}_{i\in N}$. 对于所有的房屋进行重新分配。

对于每一个agent，其type表示为$t_i=(\succ_i,r_i)$. $\succ_i$表示的是agent $i$对于所有的houses的一个偏好的order，我们记$h\succ_i h^\prime$表示对于agent $i$来说，对比$h^\prime$他严格更加偏好于房子$h$. $h\succeq_ih^\prime$表示要么$h=h'$要么$h\succ h'$. 

denote $\bold{t'}=\{t_1',t_2',\cdots,t_n'\}$ 表示所有的agents的report types.

我们将我们的机制定义为一个函数$f$，这个函数将这样的一个profile $\bold{t}'$映射到一个新的分配结果上。$f_i(\bold{t}')$表示为对于agent $i$ 来说重新分配给他的房屋。

在这类匹配领域中需要引入的一些性质包括：

***Strategy-proofness*** (SP) 表示为对于每一个agent来说，$t_i'=t_i=(\succ_i,r_i)$是占优策略。

> For any $i\in N$, for any $\bold{t}_{-i}$ and $\bold{t}_{-i}'\in R(\bold{t}_{-i})$ and $t_i,t_i'\in R(t_i)$, it holds that $f_i(t_i\bold{t}_{-i}')\succeq_i f_i(t_i',\bold{t}_{-i}')$.

***Strict Core*** (SC) 表示在一个SC的分配下，没有任何agents构成的group有集体偏离当前机制的结果的动机。

> For a networked housing market, allocation $x\in X$ is said to be in the SC under $\bold{t}$, if $\nexists S\subseteq N$ such that, under some allocation $y\in X$ satisfying $\bigcup _{i\in S}y_i=\bigcup_{i\in S}h_i$, (a) $y_i\succeq_i x_i$ holds for any $i\in S$; (b) $y_j\succ_jx_j$ holds for some $j\in S$. 

在strict core之上还定义了一个weak core，表示的是将条件(a),(b)换成(c) $y_i\succ_i x_i$ for any $i\in S$. 也就是说找不到这样一个子集使得每个人都严格更优。

***Individual Rationality*** (IR) 表示在实报的情况下，每一个agent重新分配得到的房屋一定不会差于初始情况下自己的房屋。

> For a networked housing market, feasible allocation $x\in X$ is said to be IR for given $\bold{t}$, if $x_i\succeq_i h_i$ for any $i \in N$.

***Pareto Efficiency*** (PE) 表示一个allocation是PE当且仅当我们无法找到另外一个allocation使得对于所有的agents重新分配的结果是弱优于之前的分配，同时存在一个agent的结果是严格由于之前的分配的。

> For a networked housing market, feasible allocation $x$ Pareto dominates another one $y$ under $\bold{t}$ if $x_i\succeq_i y_i$ for any $i \in N$ and $x_j \succ_j y_j$ for some $j\in N$. 

我们可以发现strict core是一个在IR和PE下更加严格的要求，事实上，在选择令$S=N$的情况下strict core的定义就完全等同于PE，而如果令$S=\{i\}$ $\forall i\in N$. strict core和weak core的定义就等同于IR. 表达为公式的形式可以写为：
$$
\forall \theta, SC(\theta)\subseteq \{PE(\theta)\cap IR(\theta)\}\text{ and } SC(\theta)\subseteq WC(\theta)\subseteq IR(\theta)
$$

##### Top Trading Cycles (TTC Algorithm)

传统的TTC算法：如果在这个市场中不存在agents剩余的时候，算法就会停止。否则的话我们构建一个有向图，他们的节点对应于所有的剩下的agents，每个agent $i$指向另一个agent，那个agent手中的房屋是$i$在剩余的agents中他最偏好的那个。显然必定会存在一个cycle，每一次在一个环中我们根据边的方向将房屋在环内进行重新的分配，然后将这个cycle中的所有的agents都剔除。重新上述的步骤直至算法终止。

在传统的房屋分配市场问题中，strict core是唯一的，且TTC导出的最终结果一定是这个strict core.

在传统的房屋分配市场问题中，TTC算法导出的唯一的一个满足SP，IR，PE的机制。

#### General Results

首先考虑SP，对于networked housing market来说，IC性不仅仅要求每个人真实的反映自己的偏好，还要求所有的agents都不能够通过减少向他的周围人的传播来获得更高的收益。

>  For a networked housing market $(N,\Pi,r)$, with general $r$, TTC satisfies SP when $n\leq 2$.

Proof: 考虑参与的agents的人数小于等于2的情况下，第一种情况如果两个agents之间不是父子节点的关系，这样的networked housing market问题与传统问题一致，TTC显然是满足SP的；第二种情况两个节点$i,j$之间$i$ diffuse information to $j$那么我们考虑如果$i$ not diffuse, 最终的结果一定是$i$得到$h_i$，然后如果他diffuse使得$j$也参与进来的话，那么$i$要么会得到$h_i$要么会得到$h_j$，反正结果一定是优于他not diffuse的情况的。也就是说在agents的数量少于等于2个的情况下，TTC导出的结果一定是SP的。

> For a networked housing market $(N,\Pi,r)$, with general $r$, there exist no mechanism that satisfies SP, IR and PE when $n\geq 3$.

Proof: 给出在$n\geq 3$的情况下，TTC一定是违背SP的。给出一个实例，假设有三个agents $i,j,k$, diffusion的情况如下：$r_s=\{i\},r_i=\{j\},r_j=\{k\}$. 同时给出他们的偏好情况：
$$
\begin{split}
\succ_i: & h_k\succ h_j\succ h_i\\
\succ_j: & h_k\succ h_i \succ h_j\\
\succ_k: & h_i\succ h_k \succ h_j
\end{split}
$$
不难计算得到TTC返回的结果为：$x_i=h_k,x_k=h_i,x_j=h_j$. 

此时我们考虑agent $j$ not diffuse to $k$, then TTC返回的结果为：$x_i=h_j,x_j=h_i$. 对于$j$来说他的收益实际上通过少传播的方式得到了增加，这就违背了SP的原则。 TTC是唯一的满足SP，IR和PE的机制，这也就说明当$n\geq 3$的情况下是不存在一个机制在networked housing market下满足SP, IR和PE的机制。

由于前面我们之前TTC导出的机制是唯一的一个满足SP和SC的机制。这样的理论说明了SP和SC是不相容的。因此现在考虑的就是将已有的strict core的概念进行弱化，同时将网络结构信息考虑进去。首先考虑的是所有的变种中最简单的同时最弱的一种，我们只关心两人联盟式的合作（以父子节点出现的那种）。

***Strict Core for Neighbors*** (SC4N) 在一个networked housing market下，我们认为一个结果是SC4N的如果在$\theta$的情况下，strict core对于所有的单个agent构成的联盟成立，同时对于任意的$i,j$满足存在$s\to\cdots\to i\to j$的结构的父子节点组合的联盟都是成立的。

> For a networked housing market, an outcome is said to be in the strict core for neighbors (SC4N) under profile $\theta$ if the strict core condition holds for any singleton agent $i\in N$ and for any pair $i,j$ of agents such that there is a path $s\to \cdots \to i\to j$ under $\theta$. Let $SC4N(\theta)$ be the set of such allocations for given $\theta$. A mechanism is said to satisfy SC4N if $f(\theta)\in SC4N(\theta)$ for any $\theta$.

类似的我们可以定义weak core for neighbors (WC4N). 我们可以找到一些概念之间的关系。

<img src="./Figures/housing-1.png" style="zoom:60%;" />

我们可以看到，从strict core这里我们可以衍生出很多的概念，首先是从strict core到weak core的扩展，strict core要求是不存在一个agents集合$S$使得有一个分配$y$对于所有在$S$中的agent都有分配结果$y$弱优于$x$，同时存在至少一个强优于$x$. 而weak core的要求是全部都优于$x$. 前面介绍过$SC(\theta)\subseteq WC(\theta)$. 这个地方需要深刻理解一下，strict core的要求显然是更高的，考虑一个在SC的分配，这个分配一定是在WC中的，因为这个分配不存在联盟使得$y$弱占优于$x$的，自然不会存在联盟使得$y$强占优于$x$. 从strict core出发，进一步将集合$S$进行限制，限制在要么是单个node，要么是两个构成父子关系的节点集合得到SC4N，对于WC是类似地得到WC4N，而从WC4N进一步放松限制$S$到单点集，从而得到的结果就是IR，从另一个角度，如果令集合$S=N$得到的就是PE.

**Example**: 考虑类似前面的实例，三个agents $i,j,k$, diffusion的情况如下：$r_s=\{i\},r_i=\{j\},r_j=\{k\}$. 同时给出他们的偏好情况：
$$
\begin{split}
\succ_i: \quad& h_k\succ h_j\succ h_i\\
\succ_j: \quad& h_i\succ h_k \succ h_j\\
\succ_k: \quad& h_i\succ h_j \succ h_k
\end{split}
$$
对于分配：$x_i=h_j,x_j=h_k,x_k=h_i$来说，它是PE且IR的。显然是IR的，因为每个人都拿到了自己初始状态拥有的房屋好，考虑PE，我们无法找到一个新的分配使得对于每一个agent来说都能够拿到更好的结果（可以逐一验证）。但是我们又会发现这个分配是不满足SC4N的，因为$\{i,j\}$是会形成一个coalition的，如果$x_i=h_j,x_j=h_i$对于$\{i,j\}$是更优的。但是考虑另一个分配：$y_i=h_j,y_j=h_i,y_k=h_k$是SC4N的但是却不是PE的，因为另外一个分配：$z_i=h_k,z_j=h_i,z_k=h_j$是Pareto占优于$y$的。（这个问题还是挺复杂的……）

给出另外一个实例：

**Example**: 考虑现在有four agents $N=\{i,j,k,l\}$, 社交网络表示为：

<img src=".\Figures\housing-2.png" style="zoom:70%;" />

同时他们的偏好如下：
$$
\begin{split}
\succ_i: \quad& h_l\succ h_k\succ h_i\succ h_j\\
\succ_j: \quad& h_i\succ h_k\succ h_l\succ h_j\\
\succ_k: \quad& h_l\succ h_j\succ h_k\succ h_i\\
\succ_l: \quad& h_i\succ h_j\succ h_l\succ h_k
\end{split}
$$
Allocation $\bold{x}$: $x_i=h_k,x_j=h_i,x_k=h_l,x_l=h_j$. 这个分配是PE同时IR的，但是不是WC4N的，考虑coalition $\{i,l\}$, strongly block $x$. 

Allocation $\bold{y}$: $y_i=h_k,y_j=h_l,y_k=h_j,y_l=h_i$. 这个是WC4N的但是不是PE的，类似前面的例子。

上面给出的两个例子表明了：由于每个人的偏好都是严格偏好，所以说一定存在唯一的一个分配是SC的，这也就意味着：$SC4N\cap\{PE\cap IR\}\neq \empty$; $WC4N\cap\{PE \cap IR\}\neq \empty$.

> For a networked housing market $(N,\Pi,r)$, with general $r$, there dose not exist a mechanism that satisfies SP and WC4N when $n\geq 3$.

这个结论告诉我们在networked housing market下，当agents的数量大于等于3时，我们找不到一个机制同时满足SP和WC4N.

Proof: 考虑下面给出的例子：

<img src=".\Figures\housing-3.png" style="zoom:70%;" />
$$
\begin{split}
\succ_i: \quad &h_k\succ h_i \succ h_j\\
\succ_j: \quad &h_k\succ h_j \succ h_i\\
\succ_k: \quad &h_j\succ h_i \succ h_k
\end{split}
$$
There are 3 allocations $x,y,z$ satisfying IR: 
$$
\begin{split}
x &= (h_i,h_k,h_j)\\
y &= (h_k,h_j,h_i)\\
z &= (h_i,h_j,h_k)
\end{split}
$$

因此想要满足WC4N必须是在这3个分配规则中。但是对于分配规则$y$和$z$来说，$\{j,k\}$都会组成一个阻塞联盟。因此想要一个机制既满足WC4N同时也满足SP的话，只有可能返回的结果是$x$这一种分配，然而我们又可以发现此时$i$得到的仍然是它自己的房屋$h_i$, 此时它是有动机不diffuse the information to $j$，假设不传给$j$我们得到的结果: $i$获得$h_k$同时$k$获得$h_i$. $i$玩家通过不传播使得自己的收益增加了。从而通过这个例子我们说明了SP和WC4N是不相容的。

#### Preference Restrictions

前面一章我们说明了当参与agents的数量大于等于3时，在networked housing market中是不存在一个满足SP，IR和PE的机制的。

因此下面我们考虑对其中的一些方面进行约束，首先考虑的是对所有的agents的偏好进行约束：我们讨论无圈的偏好。下面我们给出一个结论，当且仅当偏好域是无圈的情况下，TTC在networked housing market中是满足SP的。

***Acyclic Domain*** 我们称一个domain $\Pi'\subseteq \Pi$的偏好是无圈的，如果对于任意两个偏好$\succ,\succ'\in\Pi'$和对于任意的其他三个不同的houses，$h_i,h_j,h_k\in H$, 有结论：
$$
[h_i\succ h_j\succ h_k]\Rightarrow [h_i\succ' h_k]
$$
直观上来说，无环性要求了所有的偏好都有一个类似的形式，可以通过使用如下递归的规则表达出来。（1）至少被一个偏好排名在最前面的房屋的数量为1或者2，同时如果是两个房屋的话，我们记为$h_i,h_j$, 所有的偏好都会将他们排在最前面和第二名。（这个概念还是比较绕的，需要思考一下）

> For a networked housing market $(N,\Pi',r)$ with $n\geq 3$ and general $r$, TTC satisfies SP if and only if domain $\Pi'$ of preference is acyclic.

Proof: 

首先证明充分性：假设domain $\Pi'$的偏好都是无圈的，我们证明TTC是满足SP的。根据无圈性的定义我们可以知道所有的房屋都可以分为一些不同的层次且每一个层中要么有一个房屋，要么有两个房屋。所以在交换的时候每一个agent只会考虑和自己在一个层次的agent进行房屋的交换。所以说显然传播只有可能增加他的收益不会有可能降低他的收益的，因为传播了有可能让他从不能交换变成能够交换得到更好的房屋。同时传播增加的那些不跟自己在一层的agents不会影响自己的房屋的交换情况，所以说全传是一个占优策略。从而我们可以发现TTC在这种情况下在networked housing market问题下是SP的。

下面证明必要性：考虑TTC满足SP，我们说明此时的偏好必须是满足无环的。假设两个偏好$\succ,\succ'\in \Pi'$和三个不同的房屋$h_i,h_j,h_k\in H$, 有$[h_i\succ h_j\succ h_k]\and [h_k\succ' h_i]$, 此时对于$h_j,h_k$在$\succ'$上只有两种可能性了，要么是$h_k\succ' h_j$或者是$h_j\succ' h_k$.

这里的证明简略说明一下，文中分别讨论了上述的两种情况，然后发现，在两种情况下我们都可以找到反例，存在agent可以通过少传播来使得自己的交换的结果更优，从而也就说明了当$\succ=[h_i\succ h_j\succ h_k]$的情况下，不能够出现类似$\succ'$中有这种环$h_k\succ' h_i$的情况，出现了这种情况就代表一定有agent可以通过少传使得自己的交换结果更优。因此对于任意的$\succ'$必须满足$h_i\succ'h_k$，这也就是满足了acyclic preference的定义，从而充要性证明完毕。

注意到，当对偏好域进行约束的情况下，TTC算法的唯一性是不能保证的，因为可能还存在其他的算法也满足SP，IR和PE. 举个例子：对于单峰值的偏好而言，在传统的房屋分配问题下还存在另一种机制Crawler Mechanism也满足和TTC一样的性质。因此在networked housing market下也是可能存在一些其他的机制的。

#### Network Restriction

之前我们对偏好域进行了一定的约束，现在我们不再对偏好域进行约束，而是对networked housing market中的network进行约束，使得整个network满足一些特殊的限制的条件下考虑TTC机制。

##### Pareto Efficiency

先给出第一个结论：

> For a networked housing market $(N,\Pi,r)$ with $n\geq 3$ and a fixed $r$, TTC satisfies SP iff $r_s=N$, i.e. all the agents are directly connected to all other members.

Proof:

首先证明充分性：考虑所有的agents都是连接到moderator的，也就是说任何的hidden diffusion的操作都是没有任何意义的，实际上这个场景就退化到了传统的housing market问题上，进一步TTC显然是SP的。

下面证明必要性：如果TTC是SP的，那么我们要证明这个network一定是这种星型的网络。前面我们证明了当agents的数量小于等于2的情况下，TTC是满足SP的，下面我们考虑的是去证明只要在有一个agent不是直接连接到moderator的情况下，TTC就是不满足SP的就可以complete这个证明。我们假设这个agent用$j$表示同时他的parent节点表示为$i$. 我们考虑如下图所示的这两种情况：

<img src=".\Figures\housing-4.png" style="zoom:80%;" />

第一种情况就是如果$i$不diffuse到$j$的话，此时整个网络中只有$i$这一个agent；第二种情况就是如果$i$不diffuse给$j$的情况下除了$i$以外至少还有一个agent也还在这个network中。仍然是对这两种情况进行推导，构建出一个反例使得在所有的agents中有agent存在动机少传播来使得自己的结果更好。证明也是从略。

上述的结论也可以改写为如下推论：

> For a networked housing market $(N,\Pi,r)$ with $n\geq 3$ and a fixed $r$, there exists a mechanism that satisfies SP, IR, PE iff $r_s=N$.

##### Strict core for Neighbors

下面考虑的是当约束了网络结构之后，SP和SC4N是否能够相容的情况。在之前的结论中，我们发现到一个agent的多重路径使得SP和SC4N之前是不相容的，因此下面我们只去考虑directed tree的网络结构。首先引入一个TTC的修正算法。这个修正算法对于agents的actions进行了约束。

***Modified TTC*** 算法的基本流程如下：

如果市场上没有agents了那么算法就终止。否则的话，我们对于剩余的agents构建一个有向图，和TTC算法是类似的，不过我们约束每一个agent只能指向他的parents，herself或者他的descendants其中的一个，他选择在这些nodes中拥有他最喜欢的房子的那个node. 对于出现环的情况，按照环的指示对于所有环上的agents进行房屋的重分配。反复进行这个过程直到算法终止。

这里给出一个example：

**Example of Modified TTC**: 

<img src=".\Figures\housing-5.png" style="zoom:100%;" />

给出如下的偏好：

<img src=".\Figures\housing-6.png" style="zoom:80%;" />

走一遍算法流程：根据modified TTC，step 1我们将i指向m，将j指向i，将k指向l，将l指向l，将m指向k. 找到第一个环，从l指向l，将$h_l$分配给l；进行step 2，重复这个流程。之后的流程不一一赘述。算法很清晰且容易理解。

最终的分配结果为：$x_i=h_m,x_j=h_j,x_k=h_i,x_l=h_l,x_m=h_k$. 根据这个结果我们可以发现其中是存在blocking coalition的，包括$\{j,m\}$和$\{k,l,m\}$，但是这些coalition都不满足WC4N和SC4N. 因此我们可以给出结论：

> The modified TTC satisfies both SP and SC4N for a networked housing market $(N,\Pi,r)$ when $r$ is a tree network.

证明从略，大致的思路是考虑两种diffusion的策略，要么是$r_i$要么是$r_i'\subseteq r_i$，文中证明了使用$r_i'$matching到的房屋使用$r_i$也能够matching到，这是证明SP时的大致思路，也就是说全传播的结果永远不会差于少传的结果。在证明SC4N时，证明思路是类似的，也是反证法。

#### Discussion

这一部分作者主要讨论了一个问题，大概是在network auctions中我们大部分的机制都是基于diffusion critical tree (DCT) 进行的，但是这个思想在networked housing market是不太适用的，在networked auction的问题下，我们发现DCT下的SP的机制有两个重要的性质，（1）拥有更多的孩子节点对于自己的来说收益一定是不会减少的；（2）对于$i$来说，其他分支上的结构不会影响$i$的输出结果。但是在networked housing market这个问题上就不太行，作者给出了他自己的说明，如果我们对于SC4N进行修正的话，第二个性质会被破坏。最终作者给出了一个不可能的结论，在DCT上定义的WC4N是无法找到机制同时满足SP和WC4N的，更进一步的，不仅仅是在这个DCT上定义的WC4N上定义的新TTC算法不难阻，任何一个在DCT上定义的SP的机制都是不能够满足WC4N的。

#### Conclusion Remarks

一个新的资源分配问题，关于housing market的问题，如何考虑没有money去补偿的情况下，讨论agents去隐藏信息传播的动机。分析了在对于偏好进行约束情况下的SP机制；在对于network进行约束情况下的SP的机制，同时给出了一个改进的TTC机制在tree network下有很好的性质。未来的探究方向包括：考虑额外的由moderator提供的房屋；考虑其他的一些偏好的限制和约束；允许单个人拥有多个房屋的情况；考虑除了PE之外的其他性质，比如说最大的交换次数等等。

