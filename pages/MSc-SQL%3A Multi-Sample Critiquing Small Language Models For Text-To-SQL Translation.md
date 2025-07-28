public:: true

- ![Refer to caption](https://arxiv.org/html/2410.12916v2/x1.png)
-
- ## 方法
- ### Generator
- 每个问题产出 k=5 条候选 SQL，构成“候选池”
- ### Critiquer
- – 先用 10 k 问题的“SQL-对/错”标签做二分类预训练。
  – 再用强化学习（REINFORCE）微调，奖励函数 = 执行准确率 − 平均代价。
- 用来给每条候选 SQL 打分，选出最高分的一条作为最终输出。
- ### Executor
- 把“执行信号”喂给批判模型，供其打分
-