## REINFORCE Leave-One-Out
- 算法认为PPO 的许多组件在 RLHF 环境中是不必要的，直接采用更简单的policy gradient类强化学习算法也可以取得很好的效果，PPO中的value模型，clip操作等模块可能并不有效。
- ### 特点
	- RLOO使用RL中policy-based最基础的**Vanilla Policy Gradient REINFORCE**算法，直接计算梯度更新策略网络
	- RLOO 将语言模型根据提示生成的**整个文本序列**视为一个单一的“动作”。它不关心序列中每个 token 的即时奖励或中间状态的价值。
	- 在经典 REINFORCE 算法的基础上，引入了“Leave-One-Out”(留一法)技巧来**降低梯度估计的方差**。
- #+BEGIN_EXPORT latex
  \frac{1}{k} \sum_{i=1}^{k} \left[ R(y_{(i)}, x) - \frac{1}{k-1} \sum_{j \neq k} R(y_{(j)}, x) \right] \nabla \log \pi_\theta (y_{(i)} \mid x) \text{ for } y_{(1)}, \ldots, y_{(k)} \overset{i.i.d}{\sim} \pi_\theta(. \mid x)
  #+END_EXPORT
- 从当前策略 $π_θ$​中，独立同分布地（i.i.d）采样了$k$个**完整**的回答序列
- 括号里面是RLOO 的**核心创新点**，$$\frac{1}{k-1} \sum_{j \neq i} R(y_{(j)}, x)$$
- 直接使用奖励可能会导致梯度波动较大。通过减去一个基线，只关注当前序列$y_{(i)}$相对于同批次其他序列的“好坏程度”，降低方差
-
- RLOO算法对样本的独立性假设较为依赖，如果样本之间存在较强的相关性，可能会影响基线的有效性，进而影响算法性能。