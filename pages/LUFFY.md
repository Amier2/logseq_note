public:: true

- ## Learning to reason Under oFF-policY guidance
- ![图片](https://mmbiz.qpic.cn/mmbiz_png/Psho9dm7oDF1Ovy3nTAxcGK3za8QVxYHicygwpHYs47umMfujzCC9krsYmslhHwVRBLia42VAAXdoV9PxvdRsNTA/640?wx_fmt=png&from=appmsg&randomid=u46yn96v&tp=webp&wxfrom=5&wx_lazy=1)
-
-
- **zero-RL**一方面受制于模型本身能力，很难在推理行为上产生质的飞跃，RL可能更多地是放大模型在预训练阶段学习到的行为，并没有获取额外的推理能力
- **SFT**又存在泛化能力的不足
-
- 为了**既能借鉴专家经验，又能保持自身探索**
- 就引入来自强大外部策略的高质量**推理示范**，同时让模型不断进行**自主的推理尝试**
- 这种做法的难点在于：
	- 如果简单地把外部示范硬塞给模型，会出现“熵坍塌”，模型可能会因为过度依赖示范而变得贪婪保守
	- 需要在训练达到**“即模仿又探索”的自适应平衡**
- ### 混合策略训练
	- 使用来自更强模型或专家的推理轨迹+模型自己推理出来的轨迹数据进行混合计算优势函数更新策略，引导模型向高奖励动作靠拢，同时保留自身有效尝试
- ### Policy Shaping
	- 目的是让模型更加关注那些它原本很少尝试、但专家解题中出现的关键步骤，既引导模型汲取高手解题的精华，又防止模型把不重要的表面模式一股脑模仿过去
	- 改变了原始[[PPO]]中的重要性采样比值计算，在比值外面加了个函数变换$$\frac{x}{x+γ} ，γ=0.1$$，对专家数据分布的梯度进行重新加权，对于高概率token采样权重不会有太大变化，显著提高梯度的低概率token相对权重
	- #+BEGIN_EXPORT latex
	  \nabla_\theta \mathcal{J}_{\mathrm{SHAPING\text{-}OFF}}(\theta) = \mathbb{E}_{\tau \sim \pi_\phi} \left[ f'(\pi_\theta) \frac{\pi_\theta}{\pi_\phi} \nabla_\theta \log \pi_\theta \cdot \hat{A}_j \right]
	  #+END_EXPORT
- 这种**边学边练**的范式，无需在“模仿”还是“探索”之间二选一，而是可以设计智能体**一边向历史经验学习，一边在实践中创新**
-