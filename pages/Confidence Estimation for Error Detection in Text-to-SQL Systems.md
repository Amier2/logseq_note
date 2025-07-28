public:: true

- 给定一批<自然语言问句，模型生成SQL>，系统能自动给每条SQL打一个“置信度分”，用来判断Text2SQL有没有错
- ## 方法
- ### 选择性分类器
- 接收模型生成的SQL查询以及一个不确定性估计值u
- u通常来自Text-to-SQL模型的输出概率，通过生成的SQL查询的概率分布计算
- 使用高斯混合模型通过对不确定性分布进行建模，区分正确和错误的查询
- #+BEGIN_EXPORT latex
  p_l = P(y_l | y_{<l}, x, \theta)
  #+END_EXPORT
- #+BEGIN_EXPORT latex
  H(p_l) = -\sum_{v=0}^{|V|} p_v \log(p_v)
  #+END_EXPORT
- #+BEGIN_EXPORT latex
  u = \max(H_0, \dots, H_L)
  #+END_EXPORT
- ### 模型校准
- Platt校准和**Isotonic**回归
- ## 发现
- 选择性分类器有效降低风险
- 校准对可靠性至关重要
- 数据库分布变化影响性能
- 查询复杂性与置信度无关，即使是复杂查询，模型也可能自信地生成错误结果