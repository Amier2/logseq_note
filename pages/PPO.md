## Proximal Policy Optimization
- PPO是Actor-Critic算法的经典算法，简单、稳定，基于TRPO而来
- #+BEGIN_EXPORT latex
  J_{\text{PPO}}(\theta) = \mathbb{E}_{(s,a) \sim \pi_{\theta'}(a|s)} \left[ \text{clip} \left( \frac{\pi_{\theta}(a|s)}{\pi_{\theta'}(a|s)}, 1 - \varepsilon, 1 + \varepsilon \right) A(s,a) \right]
  #+END_EXPORT
- PPO对于朴素的Actor-Critic而言引入了优势函数、Clip和重要性采样等概念：
	- **优势函数**：在计算损失时，早期直接用回报进行计算的算法由于受动作等影响在每次训练时变动大，也就是方差大，造成训练不稳定，使用优势函数可以减少梯度估计的方差，一般用**Generalized Advantage Estimation**
	- **Clip**：通过限制策略更新的范围，大于范围的直接取范围边界值，防止策略参数的剧烈变化，避免因更新过大而导致学习过程不稳定或发散(还有penalty方法作为替代，但大部分用clip)
	- **重要性采样**：如果说PPO更新一次网络就需要与环境交互一次，时间成本大，现在希望交互的数据可以拿来训练多次，那么为了让**在旧策略下交互生成的数据在更新后的策略下仍然有正确的指导能力**，需要计算策略比率$r_t(θ)$来调整旧策略下生成的数据的权重
- 一般来讲，PPO算法对超参没有其他的RL算法那么敏感，训练比较稳定，然而数据利用效率比较低等([[RLOO]]论文中表示PPO计算成本高，超参调整敏感)
- 在RLHF中有四个模型：
	- **Actor Model(Policy Model)**：这就是我们想要训练的目标语言模型，执行生成NL的动作
		- 可以进行SFT来初始化
		- 目的是生成符合人类偏好的响应(response)，给出一个prompt，补全后面的回答，然后将这个prompt+response(一般叫completion)作为收集的数据参与训练
	- **Critic Model**：它的作用是**估计在给定状态下，遵循当前策略所能获得的未来累积奖励**，需要对他进行训练
	- **Reward Model**：它的作用是计算即时收益，通常使用学习到的人类偏好模型  （或任何其他分类模型）代替环境的奖励函数，一般来讲是response-level的奖励，而不是token-level的奖励，使用奖励模型的缘故是可以根据不同任务给出不同的奖励信号，复杂的响应也不好用定义的奖励函数计算出奖励值，类似于逆强化学习的思路
	- **Reference Model**：它的作用是在RLHF阶段给语言模型增加一些“约束”，防止语言模型训歪（朝不受控制的方向更新，效果可能越来越差），和actor是一个模型，只是这个参数不变
- ![](https://newfacade.github.io/notes-on-reinforcement-learning/_images/trl2.png)
-
- 训练流程如下：
- ![](https://newfacade.github.io/notes-on-reinforcement-learning/_images/trl1.png){:height 446, :width 778}
-