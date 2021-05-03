auction markets

seller-centric auctions

buyer-centric auctions

Target:

involve sellers to propagate auction information to her neighbors over the graph.

ensure budget feasibility on the buyer's side?

diffusion mechanisms in auctions focus on seller-centric markets

their work must guarantee the truthfulness that incentives sellers to report real costs and propagate auction information to all their neighbors simultaneously.

**Buyer-Centric Auctions** (Reverse auctions)

One buyer and multiple sellers

For the buyer: the buyer has one budget $B$.

For each seller $s_i$, she has a cost $c_i$, and her value is $v_i$. her neighbor set is $n_i$. Assume her truthful type is $t_i=(c_i,n_i)$ and reported type is $b_i=(c_i',n_i')$.

Some assumptions: cost of items is small: $c_i\ll B$  and the market size $|S|\leq N_{\max}$

Denote $\mathcal{M}=(f,p)$ by the mechanism where $f$ is the allocation rule and $p$ is the payment rule.

Utility of agents:

Seller: $U_i(b_i,\mathbb{b},\mathcal{M})=p_i-x_ic_i$

Buyer: $U_a(\mathbb{b},\mathcal{M})=\sum_{1\leq i\leq n} v_ix_i$

Object is to maximize the buyer's utility: $\max U_a(\mathbb{b},\mathcal{M})$.

IR: $u_i(t_i,(t_i,\mathbb{b}_{-i}),\mathcal{M})\geq 0,\forall i\in n$.

IC for Seller: $u_i(t_i,(t_i,\mathbb{b}_{-i}),\mathcal{M})\geq u_i(b_i,(b_i,\mathbb{b}_{-i}'),\mathcal{M}),\forall i\leq n$.

Budget feasibility: $\sum_{i=1}^n p_i\leq B$.

$v_i$ means the valuation of the seller's good for the buyer.

#### Mechanisms for homogeneous item setting: BDM-H

- Generate one seller sequence
  - calculate each seller's shortest distance to the buyer.
  - sort sellers in the non-decreasing order of the distance denoted by $\mathcal{O}$.
- Divide the winner selection process into $L=\lceil \log_2N_\max\rceil$ phases; each phase is allocated with a partial budget $\hat{B}=\frac{B}{L}$; in l-th phase, set a fixed payment $\tau_p^l$ and the target number of winners $\tau_w^l$, and $\tau_p^l\cdot \tau_w^l=\hat{B}$.
- start from the first phase and the first seller in $\mathcal{O}$.
- In l-th phase set $\tau_p^l=\frac{\hat{B}}{2^{l-1}}$ and find $\tau_w^l=2^{l-1}$ winners with costs no greater that $\tau_p^l$.