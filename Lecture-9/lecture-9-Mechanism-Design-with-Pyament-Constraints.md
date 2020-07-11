### Lecture 9

----

### Mechanism Design with Payment Constraints

之前在机制设计问题的研究上我们对于payment的限制只停留在最简单的情境，非负且保证实报bidders不会有负收益。在这一讲中我们第一次考虑带支付限制的机制设计问题而不是仅仅incentive和可行的限制。

9.1节中将预算约束考虑进近似线性收益模型；9.2节探究多单位物品的拍卖，在这种拍卖中bidders存在预算，同时提出了如果没有DSIC的一种解决方案：uniform-price auction；9.3节我们描述了一种clinching auction，这是一种更加复杂的拍卖情境；9.4节提出了不考虑钱的机制设计问题，涉及经典的房屋分配问题同时学习TTC算法的一些性质。

#### 9.1 Budget Constraints

在许多的实际应用中，对于payment往往是有一些约束的。首先就是budget constraints，这个限制了一个智能体所能付出的钱的数量。预算问题在一些一个agent可能购买很多的物品的情境下会变得十分重要。例如在关键词搜索拍卖中，每一个bidder都被要求知道他对于每一次点击的bid以及他每天的预算。

最简单的将budgets加入我们的收益模型的方式是重新定义带budget为$B_i$的智能体$i$对于结果$\omega$和payment为$p_i$的情况：
$$
\begin{split}
v_i(\omega)-p_i & \text{  if }p_i\leq B_i \\
-\infty & \text{  if }p_i>B_i
\end{split}
$$
我们需要新的拍卖形式来将budget约束纳入进来。例如考虑最简单的单物品拍卖情境，其中每一个bidder拥有一个已知的budget为1，同时有一个私人估值。二价拍卖下，获胜者需要支付第二高的价格，其中有可能出现这个价格超过了它的预算。更加广泛的结论是：没有带有非负payments的DSIC的单物品拍卖能够最大化社会福利同时还能够遵守bidders'的预算。

#### 9.2 The Uniform-Price Multi-Unit Auction

多单位物品拍卖问题的情境如下：存在$m$个相同的items，每一个bidder都对每一个他得到的物品有一个估值$v_i$，不同于k-unit物品拍卖的形式，我们假设每一个bidder都希望得到尽可能多的单位的物品。因此$i$号bidder从$k$个items中获得的价值为$k\cdot v_i$. 可以认为这样的多单位物品拍卖问题是单参数的环境。另外的话每一个bidder都有一个公共皆知的预算$B_i$，也就是说卖家是提前知道所有人的这个预算值的。

The Uniform-Price Auction

首先定义$i$号bidder在价格为$p$时的需求量：
$$
D_i(p)=\begin{cases} \min\{|\frac{B_i}{p}|,m\} &\text{ if } p < v_i;\\
0 & \text{ if } p>v_i;
\end{cases}
$$
