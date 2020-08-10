一些基本的规则问题

1. diffusion auction中的单调分配规则是满足分配规则关于报价是非递减的，关于传播情况是非递增的，构成一个偏序关系下的单调规则。
2. 关于payment，payment规则与自身报价无关，关于传播情况是非递增的。
3. 计算收益：$u_i(v_i,r_i)=v_i\cdot f(v_i,r_i) - p(r_i)$. $f$是一个diffusion auction下的单调分配函数。
4. critical bid算是一个关于传播情况的函数，critical bid是关于传播情况非递减的。（这是解决分配问题的一个关键）
5. 对于一个diffusion auction的机制来说，efficient和(weakly)budget-balanced之间是不能同时满足的。
6. $\tilde{x}(r_i)_i-\bar{x}_i(r_i)=v^\ast_i(r_i)$如何使用起来？

一些解决方案：

1. 分析每个人的传播能够对机制的走向以及自身的收益的影响
2. 构建critical diffusion tree是一个关键点，对于一个节点来说他的传播效益的体现一定是在critical diffusion tree上，其他的传播都是无价值传播
3. 定义一个有效的分析序列，这个序列决定着哪些人有优先进行判断是否能够获得一个slot的权利？
4. 分析一个bidder能否获得item的关键因素是$v^k(\tilde{T}_{-i})$.
5. 