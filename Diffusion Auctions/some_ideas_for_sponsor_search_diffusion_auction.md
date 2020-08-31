一些基本的规则问题

1. IC diffusion auction中的单调分配规则是满足分配规则关于报价是非递减的，关于传播情况是非递增的，构成一个偏序关系下的单调规则。
2. 关于payment，payment规则与自身报价无关，关于传播情况是非递增的。
3. 计算收益：$u_i(v_i,r_i)=v_i\cdot f(v_i,r_i) - p(r_i)$. $f$是一个diffusion auction下的单调分配函数。
4. critical bid算是一个关于传播情况的函数，critical bid是关于传播情况非递减的。（这是解决分配问题的一个关键）
5. 对于一个IC diffusion auction的机制来说，efficient和(weakly)budget-balanced之间是不能同时满足的。
6. $\tilde{x}(r_i)_i-\bar{x}_i(r_i)=v^\ast_i(r_i)$如何使用起来？
7. <font color=red>IC diffusion auction的efficiency与weakly budget-balanced之间的trade-off有没有一种系统研究？</font>

一些解决方案：

1. 分析每个人的传播能够对机制的走向以及自身的收益的影响
2. 构建critical diffusion tree是一个关键点，对于一个节点来说他的传播效益的体现一定是在critical diffusion tree上，其他的传播都是无价值传播
3. 定义一个有效的分析序列，这个序列决定着哪些人有优先进行判断是否能够获得一个slot的权利？
4. 分析一个bidder能否获得item的关键因素是$v^k(\tilde{T}_{-i})$.
5. 面对$v_i^1 \geq v_i^2$但是$r_i^2\subseteq r_i^1$的情况下的分配规则，在不满足这种偏序情况下的分配结果。
6.  深刻理解$\tilde{x}_i(r_i)-\bar{x}_i(r_i)=v^\ast_i(r_i)$. 思考在没有diffusion的情况下，这时候单物品情境下获胜者的支付结果是关键报价，但是考虑了传播之后的情况就需要考虑当出现buyer因为传播而导致的从winner变成loser时候的一个补偿。这个补偿就是$\bar{x}_i(r_i)$. 
7. 将IC diffusion auction扩展到sponsor search的情境下的时候会存在一个很大的问题是payment的分解不再是分解为$\tilde{x}_i$和$\bar{x}_i$而是变成一个多阶段的分解payment. 
8. 从价高者得的单调分配规则改变为非传递条件下的价高者得。
9. <font color=red>放宽要求，先考虑使用VCG下的单调的分配规则。价格前k高的人获得前k个slot.</font>
10. 在构造出一颗关键传播Tree的情况下可以考虑分析所有路径上的情况。（存在需要传播补偿的情况）
11. 抽象的写出一个关于关键字赞助传播拍卖的情景就是考虑将最大化社会福利（或者其他指标）作为优化目标写成优化问题的一个分配规则。
12. 从最高价开始分析，判断他是否有资格获得第一名的位次。依次类推这个过程。
13. 能否先放宽WBB的限制，寻找满足efficiency的分配规则是容易的。
14. 分配存在efficiency同时传播也是存在efficiency的

15. 一个问题，如果我不传我只去考虑我自己的变化情况但是实际上在我不传的情况下也对整个系统带来了一定的影响。（这个问题也很重要）
16. 整理目前的思路，思考存在的问题以及找一个case

---

<font color=red>梳理问题的关键点</font>

在多物品的diffusion auction中一共会存在这样几类人群：

1. 无法获得一件物品同时进行的都是无效传播，收益为0.
2. 无法获得一件物品但是进行了一部分有效传播，存在有效传播的收益。
3. 获得一件商品但是没有进行有效的传播，存在获得商品的收益但是不存在传播收益。
4. 获得一件商品同时进行了有效的传播，存在获得商品的收益以及传播的收益。

另一种思路的解决方案：

假设存在一种分配规则$f(v_i,r_i)$是在IC-DA下单调的，我们下面寻找对于$f(v_i,r_i)=1$的bidders的payment的想法。假设$f(v_i,r_i)=\alpha_j$. 也就是$i$玩家被分配到了$j$位置上。

固定其他所有人的types， 只分析$i$的type的变化对于他slot的变化的影响。

$t_i=(v_i,r_i)$. 假设固定传播，分析$v_i$的变化对于他slot变化的影响？$v_i$从0到$v^\ast_j$过程下他需要支付多少钱？

固定$v_i$，他的$r_i$关于payment的变化。（<font color=red>这个是解决问题的关键点</font>）

VCG在多物品的diffusion auction上是否IC？（证明完成VCG在多物品上的diffusion auction是IC的下面考虑思考IDM的演化）

GIDM的不IC的问题在于回溯的过程存在不传播比传播的收益更高。

