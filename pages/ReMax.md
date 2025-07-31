public:: true

- ## 方法
	- 使用REINFORCE算法，不像PPO，不需要中间过程的value估计，直接用reward优化策略
	- REINFORCE算法的高方差问题，使用优势函数来平衡
	- #+BEGIN_EXPORT latex
	  A_{q,o_t} = r(o_{1:T}, q) - r(\hat{o}_{1:T}, q)\\
	  \hat{o}_{1:T} = \operatorname{argmax}_{\substack{o'_1,\ldots,o'_T}} \prod_{i=1}^T \pi_\theta(o'_i \mid q, o'_{<i})
	  #+END_EXPORT
	- 优势函数计算的baseline项是由Greedy Decoding生成的response得到的奖励得到