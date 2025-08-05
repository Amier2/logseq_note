public:: true

- 目前研究者通常采用两阶段顺序方法SFT→RFT/RL：先用SFT学习高质量数据集，再用RFT/RL进一步优化对齐LLM策略
- 利用[[LUFFY]]的思路
- 提出一种**单阶段监督-强化微调方法**
- 通过**基于熵的动态加权机制**，将两种训练范式结合
- ## 分析
- **SFT 导致大部分 token （50%以上）的概率分布改变（粗粒度）**
- **RL/RFT 只对特定 token （少于2%）进行有针对性的调整，同时保留了大部分内容（细粒度）**
- SFT使模型在概率空间中移动的距离最远，如果偏离过远**后续的RL反而需要将其“拉回”到离基础模型更近的区域才能达到最优**
- 在 RL 后进行 SFT，会使模型的熵短暂增加；而RL 在训练过程中则会使**熵显著降低**，**模型的输出分布变得更加集中**
- ![Refer to caption](https://arxiv.org/html/2506.19767v1/extracted/6567771/figures/trajectory.png)
- ## 方法
- 思想是通过SFT实现**粗粒度行为策略逼近**，通过RL实现**细粒度策略精化**，借助于**单阶段训练**，将微调同时应用于示例数据和自生成的试错数据
- 先SFT，然后示例数据和生成数据融合进行RL
- ![Refer to caption](https://arxiv.org/html/2506.19767v1/x2.png){:height 275, :width 746}
- SFT加入自适应权重，当模型策略熵高（不确定性大）时，SFT 损失对模型更新的影响会被自动减弱
- $$w_{SFT}=0.5∗{stopgrad⁢}(exp⁡(−ℋ⁢(π_θ)))$$
- $$w_{RL}=0.1∗{stopgrad⁢}(exp⁡(−ℋ⁢(π_θ)))$$
- RL期间正样本加入自适应权重，当熵较高时，使RL训练中正样本训练的权值上升，使熵下降，从而促进熵的稳定
- #+BEGIN_EXPORT latex
  \mathcal{L}_{\text{SFT}}^{\text{demo.}}(\theta) = w_{\text{SFT}} \cdot \mathbb{E}_{(x,y) \sim \mathcal{D}_{\text{demo.}}} \left[ -\log \pi_\theta (y \mid x) \right]  \\
  #+END_EXPORT
- #+BEGIN_EXPORT latex
  \mathcal{L}_{\mathrm{RL}}^{\mathrm{demo.}}(\theta) = - \mathbb{E}_{(x,y) \sim \mathcal{D}_{\mathrm{demo.}}} \left[ \min \left\{ r_{k,t}(\theta) \cdot \hat{A}_k, \mathrm{clip} \left( r_{k,t}(\theta), 1 - \epsilon, 1 + \epsilon \right) \cdot \hat{A}_k \right\} \right]
  #+END_EXPORT
- #+BEGIN_EXPORT latex
  \mathcal{L}_{\mathrm{RL}}^{\mathrm{self\text{-}rollout}}(\theta) = w_{\mathrm{RL}} \cdot \mathbb{E}_{\boldsymbol{x} \sim \mathcal{D}, \boldsymbol{y}^+ \sim \pi_\theta(\cdot \mid \boldsymbol{x})} \left[ -\log \pi_\theta(\boldsymbol{y}^+ \mid \boldsymbol{x}) \right] + \mathbb{E}_{\boldsymbol{x} \sim \mathcal{D}, \boldsymbol{y}^- \sim \pi_\theta(\cdot \mid \boldsymbol{x})} \left[ \log \pi_\theta(\boldsymbol{y}^- \mid \boldsymbol{x}) \right]
  #+END_EXPORT
- #+BEGIN_EXPORT latex
  \mathcal{L}_{\mathrm{SRFT}}(\theta) = \mathcal{L}_{\mathrm{SFT}}^{\mathrm{demo.}}(\theta) + \mathcal{L}_{\mathrm{RL}}^{\mathrm{demo.}}(\theta) + \mathcal{L}_{\mathrm{RL}}^{\mathrm{self\text{-}rollout}}(\theta)
  #+END_EXPORT
-
- ## 类似文献
- ### Step-wise adaptive integration of supervised fine-tuning and reinforcement learning for task-specific LLMs (SASR)
	- 自适应集成SFT和RL的新型训练框架，SFT和RL在不同步骤下
	- 通过分析梯度范数和模型相对于原始分布的散度，动态平衡进行SFT和GRPO(每个batch)的比例，从开始的SFT为主逐步过渡到RL为主
- ### UFT: Unifying supervised and reinforcement fine-tuning
	- 将SFT和RFT的监督信号和奖励信号作为联合损失函数优化
	- RL时拿标准答案生成一个hint引导RL生成，同时为了防止模型过度依赖提示，随着训练的进行提示的长度会**逐渐减少**直到没有提示
- ### SuperRL: Reinforcement learning with supervision to boost LLM reasoning
	- 动态判断环境是提供密集奖励还是稀疏奖励，检测到稀疏奖励时，控制权将移交给Hybrid Actor，Hybrid Actor通过（SFT）损失来增强策略梯度目标。可学习的不确定性参数，以动态平衡策略梯度和SFT损失
	- 能够有效防止传统RL在奖励稀疏环境中可能出现的过早探索或对不充分信号的过度依赖
-