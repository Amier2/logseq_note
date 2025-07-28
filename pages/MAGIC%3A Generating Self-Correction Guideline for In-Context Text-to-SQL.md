public:: true

- ![Refer to caption](https://arxiv.org/html/2406.12692v3/x2.png)
-
- ## Prompt工程
- 多智能体协作自动纠错
	- **Manager Agent**
	- **Correction Agent**
	- **Feedback Agent**
- ## 值得注意的点
- MAGIC 只用 BIRD-train 的 9 485 个失败案例（约占训练集 20%）就能收敛；作者实验表明再增加更多失败样本，收益趋于饱和。
- Feedback Agent 最初给 11 种细粒度错误标签，结果迭代次数暴增且指引碎片化；后来合并成 5 类（Schema 不匹配、JOIN 缺失、列歧义、聚合/排序错误、其它）才在收敛速度和最终精度间取得平衡，所以真正落地可能需要错误聚类，自己尝试几类错误是最优的选择