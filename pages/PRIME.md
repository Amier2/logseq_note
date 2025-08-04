public:: true

- ## Process Reinforcement through Implicit Rewards
- ## 问题
- 如何高效且可扩展地获取精确的奖励信号，尤其是密集奖励信号
- 如何设计有效的 RL 算法，充分利用这些奖励信号
- ## 方法
- ### 隐式过程奖励建模（Implicit PRM）
- 通过训练一个outcome reward model (ORM)，隐式地学习到了每一步行为的价值
-
- 密集奖励：隐式PRM直接学习为每个token生成奖励的Q函数，无需额外价值模型即可缓解奖励稀疏性问题
- 可扩展性：仅需结果标签即可在线更新隐式PRM，通过带结果验证的在线策略轨迹直接更新PRM，有效缓解分布偏移与可扩展性限制
- 简洁性：隐式PRM本质即为语言模型，实践表明监督微调（SFT）模型本身即可作为优质初始PRM
-
- ![](https://pic3.zhimg.com/v2-1a0300b3471382a8effb7a6de05861b6_1440w.jpg)
-
- ### 个人看法
- 借助kl散度和特殊的ref模型造出一个过程奖励函数，能比过蒸馏好用吗
- 在Math上涨点了，但是code上没涨点，没看出来PRM的优越性