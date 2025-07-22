- ![Refer to caption](https://arxiv.org/html/2406.13408v4/x2.png)
- ## 方法
- ### SQLReviewer
	- **语法错误**：把 SQL 丢到真实数据库跑一遍，看能否编译/执行。
	- **语义错误**：用“小黄鸭调试法”（Rubber Duck Debugging）——让模型像跟小黄鸭解释代码一样，逐句说明 SQL 与问题描述是否匹配；若发现不一致就触发修复流程。
- ### SQLCrafter
	- • 对原问题做多种改写（paraphrase）→ 让 SQLTool 重新生成 SQL → 得到一批候选。
	  • 同时利用 SQLTool 的历史错误记忆，避免重复踩坑。
- ### SQLRefiner
	- • 基于“相似修复检索”——在以往的成功修复中找最接近的案例做示范。
	  • Reflexion 机制：若选出的 SQL 仍报错或无结果，记录错误信息，迭代再选；直至通过或达到最大轮次。