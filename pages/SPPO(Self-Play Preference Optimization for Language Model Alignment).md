public:: true

- 将RLHF问题严格定义为一个两玩家常和博弈(two-player constant-sum game)，目标是达到纳什均衡策略
- 同一个策略对于一个问题输出多个响应，用已有的偏好奖励模型打分，响应之间两两比较，统计每个响应的胜率，作为偏好得分，构建数据集$$\mathcal{D}_t$$ ，进行训练
- #+BEGIN_EXPORT latex
  \mathcal{D}_t = \left\{ \left( \mathbf{x}_i, \mathbf{y}_i, \widehat{P}(\mathbf{y}_i \succ \pi_t \mid \mathbf{x}_i) \right) \right\}_{i \in [N]}
  #+END_EXPORT
-
- 意义：
	- 不依赖外部参考响应或人工偏好标注，而是通过策略自博弈产生偏好数据
	- 不需要一个固定的参考答案或 reference 策略