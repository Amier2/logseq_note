public:: true

- ## NAACL2025
-
- ## 方法
- 把一次工具链的规划过程表示成一棵**深度有限**的搜索树
- 节点 = 当前状态 + 已用工具；边 = 下一步工具调用。
  – 采用**深度优先搜索 + 剪枝**：
  • 剪枝规则：重复工具、冗余参数、价值函数 < 阈值。
- ### Planning Agent
	- 分解子任务
- ### Executor Agent
	- 思考
	- 选工具
	- 生成参数
	- 执行
- ### Answer Agent
	- 用于为减轻因上下文过长而导致的性能下降，在每个步骤和子问题中提取关键内容
- ### Verifier Agent
	- 验证智能体充当早停与反思机制，在效果与效率之间取得平衡
-
-
- ![Refer to caption](https://arxiv.org/html/2405.05955v4/x1.png){:height 353, :width 778}
- ![Refer to caption](https://arxiv.org/html/2405.05955v4/x2.png)
-