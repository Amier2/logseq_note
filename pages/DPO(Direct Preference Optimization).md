- **RLHF是一个复杂且常常不稳定的过程，需要先拟合一个反映人类偏好的奖励模型，然后使用强化学习来优化大型无监督LM，要在最大化估计的奖励的同时，避免偏离原始模型太远**。
- **DPO的核心思想是绕过显式的奖励建模和强化学习步骤，直接使用人类偏好数据来优化语言模型**。
- #+BEGIN_EXPORT latex
  \mathcal{L}_{\text{DPO}}(\pi_\theta; \pi_{\text{ref}}) = - \mathbb{E}_{(x, y_w, y_l) \sim \mathcal{D}} \left[ 
  \log \sigma \left( 
  \beta \log \frac{\pi_\theta(y_w \mid x)}{\pi_{\text{ref}}(y_w \mid x)} 
  - \beta \log \frac{\pi_\theta(y_l \mid x)}{\pi_{\text{ref}}(y_l \mid x)} 
  \right) 
  \right]
  #+END_EXPORT
- $y_w$是人类偏好输出“winner”，$y_l$是人类不偏好输出“loser”
- $D$ 是包含输入 $x$ 和成对输出$(y_w，y_l)$的数据集，这些数据集是根据人类偏好标注的。
- 损失函数类似于二分类的交叉熵损失函数，衡量的是当前模型相对于参考模型，在多组人类偏好对中是否更倾向于生成更优回答的能力，通过最大化 log-sigmoid 分数差值来实现训练目标
- 这个过程不需要从模型生成的响应中采样，也不需要复杂的强化学习算法。
- DPO在更新模型时使用**动态重要性权重**，这有助于防止模型退化，并且能够更有效地调整模型以偏好更高质量的响应
- ![Refer to caption](https://arxiv.org/html/2503.06072v2/x11.png)
-
- ## 变体
- ### [TDPO](https://arxiv.org/abs/2404.11999)
- 在token级别优化策略，核心思想是每个token引入前向KL散度约束，而不是传统的逆向KL散度，前向KL计算从目标分布 $P$ 到模型分布 $Q$ 的散度，会倾向于倾向于使$Q$覆盖$P$ 的所有模式，从而在文本生成中同时提高对齐性和多样性。
- ![img](https://i-blog.csdnimg.cn/img_convert/ffa3e952dc3fe3c7cf498721062aceac.png)
-
- 剩下的先放一放