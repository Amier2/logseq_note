## ICLR 2025
-
- ## 背景
	- 现有工作流评估框架存在以下局限：
	- 仅关注整体性能，忽视结构化工作流的准确性；
	- 场景覆盖范围有限；
	- 工作流结构过于简单（如线性序列）；
	- 评估标准宽松，缺乏系统性量化指标
- ## 方法
- ### 提出基准测试框架
	- 系统评估LLM代理生成**复杂图结构工作流**的能力
	- 涵盖**问题解决、函数调用、具身规划、开放式规划**四大类，共**21439**个样本
	- 采用**有向无环图（DAG）**建模工作流，节点为可执行子任务，边为依赖关系；
	- 通过**拓扑排序**确保工作流的正确性，避免循环依赖
- ### 评估
	- **序列维度**：模型生成的工作流步骤顺序是否正确？
	- **图结构维度**：模型是否准确捕捉到步骤之间的复杂依赖（并行、分支）？
	- #### Sequence-level匹配
		- 拿gold工作流做一次拓扑排序，得到唯一确定的**步骤顺序**。模型生成的工作流同样做拓扑排序，然后计算两者的**最长公共子序列（LCS）**长度，归一化后得到 0-1 之间的“顺序准确率”。
	- #### Graph-level匹配
		- 拿gold图和预测图使用匈牙利算法求出最大权重匹配，匹配得分除以gold图节点总数即得到 **“图准确率”**