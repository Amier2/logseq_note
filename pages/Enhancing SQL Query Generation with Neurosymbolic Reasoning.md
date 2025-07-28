public:: true

- ## 背景
- 传统语言模型在推理过程中主要依赖线性搜索策略，这限制了它们探索多条解决路径的能力。
- 当面临多个有效推理选项时，模型往往只选择一条路径，这妨碍了它们在复杂查询生成中的表现。
- SQL语法的变化可能导致训练数据集的不一致，使得模型在生成逻辑上正确但风格上不同的查询时受到惩罚。
- ## 方法
- ![first image](https://chatdoc-arxiv.oss-us-west-1.aliyuncs.com/images/aaai/34198/36353/first_image.jpeg?AWSAccessKeyId=LTAI5t6b2G8eTtEBczAMwjhc&Signature=3pJeLbipuhvxvHXsODc1jbzmGyk%3D&Expires=9223372038607951872)
-
- 纠错、剪枝、回溯     **token-by-token**
-
- ### Partial-Query Checker
- 输入用户请求(NL+输出示例)、数据库模式以及一个部分 SQL 查询
- 判断该查询是否有效
- 对查询进行语法错误、运行时错误和查询输出错误的常见检查
- PQC不能访问整个数据库
	- #### PQC-Symbolic Query Checker
		- 词汇检查
		  逐个子句进行检查，每个子句都要包含正确的词汇。
		- 作用域检查
		  检查所有在 `SELECT`、`WHERE`、`GROUP BY` 和 `HAVING` 子句中提到的表是否也出现在 `FROM` 子句中。作用域检查只能发现**运行时错误**。
		- 类型检查
		  将 `SELECT` 子句返回的元组类型与示例输出中的元组类型进行比较，以确保选择了正确数量和类型的列。类型检查只能检测**查询输出错误**。
	- #### PQC-Neural Query Checker(准确率反而更低)
		- NQC逐词处理查询，生成**隐藏状态**，这些状态编码了关于部分查询中潜在错误的信息。然后通过 **max pooling** 将这些隐藏状态聚合成一个表示，用于判断整个查询是否包含错误。
		- 为了训练神经查询检查器，使用训练集、一个微调后的语言模型和 Beam Search生成一批查询，并根据它们的执行结果进行标注。
- ### Query Test-and-Repair
- 执行生成的完整查询，尝试对该查询进行修复
- 需要注意修复后的查询与原始生成的查询之间的汉明距离（Hamming Distance）应尽可能小
- **也不会尝试修复常量值的近似错误**（例如将 “France” 更改为 “Grance”），因为这样的搜索空间过大，且成功的可能性极低。
-