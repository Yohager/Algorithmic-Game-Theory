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