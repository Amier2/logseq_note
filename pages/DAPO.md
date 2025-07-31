public:: true

- ## Decoupled Clip and Dynamic sampling Policy Optimization
- [[DrGRPO]]思路类似，都从GRPO发现问题
- #+BEGIN_EXPORT latex
  \begin{aligned}
  \mathcal{J}_{\text{DAPO}}(\theta) =& \ \mathbb{E}_{(q,a) \sim \mathcal{D}, \{o_i\}_{i=1}^G \sim \pi_{\theta_{\text{old}}}(\cdot|q)} \\
  & \left[ \frac{1}{\sum_{i=1}^G |o_i|} \sum_{i=1}^G \sum_{t=1}^{|o_i|} \min \left( r_{i,t}(\theta) \hat{A}_{i,t}, \ \text{clip} \left( r_{i,t}(\theta), 1 - \varepsilon_{\text{low}}, 1 + \varepsilon_{\text{high}} \right) \hat{A}_{i,t} \right) \right], \\
  & \text{s.t.} \ 0 < \left| \left\{ o_i \mid \text{is\_equivalent}(a, o_i) \right\} \right| < G.
  \end{aligned}
  #+END_EXPORT
- ### Clip-Higher
- **问题**：
	- PPO 或 GRPO 存在着**熵坍塌**现象：
	- 随着训练推进，策略的熵迅速下降。某些批次采样的响应几乎完全相同，表明**探索受限**、策略过早趋向确定，从而阻碍了进一步扩展。
	- 发现这是由于PPO的**upper clip**限制了策略的探索
	- 因为根据Clip方法，优势值大于0时，新策略提升该动作概率不能超过旧策略概率的$(1+ϵ)$ 倍
	- 对于低概率词元 0.01，其新概率上限为 0.01×(1+0.2)=0.012
	- 对于高概率词元 0.9，其新概率上限为 0.9×(1+0.2)=1.08
	- 意味着本来高概率的词很容易提升概率，低概率的词很难提升概率，实验也证明被Clip限制的通常是低概率词
	- 如果模型无法有效提高那些不常见但有潜力的动作的概率，它就难以发现更优的策略，这可能导致**熵坍塌**
- **方法**：
	- 提高了Clip的上界范围，鼓励模型探索更多罕见但可能信息丰富的 token
- ### Dynamic Sampling
- **问题**：
	- 参考 [[DrGRPO]] 里的Question-level difficulty bias，DAPO也发现了这个问题
	- **随着训练进行，准确率为1的样本数量不断增加 ，这意味着每个批次中有效提示的数量不断减少**，导致梯度方差增大并削弱了模型训练的梯度信号 。同样地，准确率为0的样本也会导致零梯度问题 。
- **方法**：
	- 准确率全1或全0的批次不可用，在训练前，**持续采样直到批次中充满准确率既非0也非1的样本 。**
- ### Token-Level Policy Gradient Loss
- **问题**：
	- GRPO对于一个训练批次中的每个**完整响应样本**（即一个 `prompt + response` 对），它首先会计算这个response中所有 token 的损失的平均值。然后将**每个样本的平均损失聚合起来**，得到一个最终的批次总损失
	- 那么**每个样本**无论长短，在最终的总损失计算中被赋予了**相等的权重**，也就是如果有两个样本，10个token的和100个token的样本权重各占50%
	- 这种方法在Long CoT场景时，单个 token 对整个批次总损失的贡献被**稀释**了
	- 如果有一个高质量的长response，模型在反向传播时**很难有效地学习到其中包含的、与推理相关的关键模式和步骤**。
	- 对于胡言乱语、复读的低质量长response，由于被稀释导致损失计算无法有效惩罚长样本中这些不期望的输出，导致模型性能可能不好，但生成长度却在增加
- **方法**：
	- DAPO 实现了**token 级别的损失函数**，目标函数的分母从样本数 G 替换为所有生成序列的**总 token 数**
- ### Overlong Reward Shaping
- **问题**：
	- 如果一个response过长，会在最大长度处截断，并被给一个惩罚奖励，论文认为如果一个合理的推理过程可能仅仅因为长度过长而被惩罚，这会是一种奖励噪声，这种噪声会混淆模型对其推理过程有效性的判断，严重扰乱训练过程 。
- **方法**：
	- **Soft Overlong Punishment**，在超出预设的最大长度（减去缓存长度）时，进入一个惩罚区间，在此区间内，响应越长，惩罚越大 ，此惩罚叠加到原始基于规则的正确性奖励上 。
-