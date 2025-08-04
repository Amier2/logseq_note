### 策略熵（Policy Entropy）
	- **熵**量化了一个代理在选择动作时的可预测性或随机性，给定策略模型$$π_θ​$$  和训练集 $$D$$，我们定义其在训练数据上的平均 token 级别熵为：
- #+BEGIN_EXPORT latex
  H(\pi_\theta, D) = -\mathbb{E}_{D, \pi_\theta}[\log \pi_\theta(y_t | y_{<t})] = -\frac{1}{|D|} \sum_{x \in D} \frac{1}{|y|} \sum_{t=1}^{|y|} \mathbb{E}_{y_t \sim \pi_\theta}[\log \pi_\theta(y_t | y_{<t}, x)]
  #+END_EXPORT
- #### 策略熵会被用来“换取”奖励
	- 在各种模型的RL实验中发现：
		- **策略熵在训练一开始就急剧下降**，并在之后持续单调减少，直至接近零。
		- 训练一开始性能迅速上升，随后趋于饱和。
		- 训练过程后2/3的步骤带来的性能提升非常有限，呈现边际效益递减
		- 因此利用早期的熵就可以预测后期的性能
- #+BEGIN_EXPORT latex
  R = -a \exp(\mathcal{H}) + b,
  #+END_EXPORT
- ![Refer to caption](https://arxiv.org/html/2505.22617v1/x2.png)
- #### 如果动作的概率与其优势值呈强正相关，策略熵将减少；若呈负相关，策略熵将上升。
	- 每一步策略熵的变化大致等于对数概率与logit变化之间协方差的**负值**
- #+BEGIN_EXPORT latex
  \mathcal{H}(\pi_\theta^{k+1}) - \mathcal{H}(\pi_\theta^k) \approx \mathbb{E}_{s \sim d_{\pi_\theta}} \left[ \mathcal{H}(\pi_\theta^{k+1} | s) - \mathcal{H}(\pi_\theta^k | s) \right] \approx \mathbb{E}_{s \sim d_{\pi_\theta}} \left[ - \text{Cov}_{a \sim \pi_\theta^k(\cdot|s)} \left( \log \pi_\theta^k(a|s),  z_{s,a}^{k+1} - z_{s,a}^k \right) \right]
  #+END_EXPORT
- ### 如何控制熵变化
- 加入熵损失项，对超参系数非常敏感；调整策略模型与参考模型之间的 KL 惩罚来控制熵，策略性能下降
- 通过**限制具有高协方差的 token** 的策略更新来控制策略熵，促进策略的探索能力
	- 因为只有少部分 token 的协方差极高，主导了熵坍塌现象，计算出每个token的协方差后，提出两种方法
	- #### Clip-Cov
		- 从策略梯度更新中选择一小部分高协方差的 token，不参与更新
		- #+BEGIN_EXPORT latex
		  L_{\text{Clip-Cov}}(\theta) = 
		  \begin{cases} 
		  \mathbb{E}_t \left[ \frac{\pi_\theta(y_t \mid \mathbf{y}_{<t})}{\pi_{\theta_{\text{old}}}(y_t \mid \mathbf{y}_{<t})} A_t \right], & t \notin I_{\text{clip}} \\
		  0, & t \in I_{\text{clip}}
		  \end{cases}
		  #+END_EXPORT
	- #### KL-Cov
		- 选出协方差排名前 *k* 比例的 token，*k* ≪ 1
		- 对这些被选中的 token 施加 KL 惩罚
		- #+BEGIN_EXPORT latex
		  L_{\text{KL-Cov}}(\theta) = 
		  \begin{cases} 
		  \mathbb{E}_t \left[ \frac{\pi_\theta(y_t \mid \mathbf{y}_{<t})}{\pi_{\theta_{\text{old}}}(y_t \mid \mathbf{y}_{<t})} A_t \right], & t \notin I_{\text{KL}} \\
		  \mathbb{E}_t \left[ \frac{\pi_\theta(y_t \mid \mathbf{y}_{<t})}{\pi_{\theta_{\text{old}}}(y_t \mid \mathbf{y}_{<t})} A_t - \beta \mathbb{D}_{\text{KL}}(\pi_{\theta_{\text{old}}}(y_t \mid \mathbf{y}_{<t}) \mid \mid \pi_\theta(y_t \mid \mathbf{y}_{<t})) \right], & t \in I_{\text{KL}}
		  \end{cases}
		  #+END_EXPORT
- ### 实验结论
- [[DAPO]] 的clip-higher 实际上是在将更多协方差较低的 token（即低概率、高优势，平均协方差约为 -0.03）纳入梯度计算中
- 只对极少量的 token 进行干预（比例为 10⁻⁴ 到 10⁻³），却能完全改变熵的变化曲线；此外实验并未观察到所干预的熵与模型性能之间存在明确的关系
- 结果表明，Clip-Cov 方法在熵保持方面往往更积极，但有时可能导致不稳定，而 KL-Cov 提供更稳定的训练并带来一致的改进。
-