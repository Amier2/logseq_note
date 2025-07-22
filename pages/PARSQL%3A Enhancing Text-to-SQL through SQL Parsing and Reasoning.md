## 背景
- 如果把 SQL 当长字符串，模型容易在 JOIN/嵌套/聚合等长依赖位置出错。
  SQL 天然有“解析树”这一结构化中间表示；如果让 LLM 先显式地生成树，再补全细节，既降低幻觉又方便约束解码。
- ## 方法
- **解析→增强→推理→校对**
- ### PARSer
- 先把 SQL 拆解成抽象语法树（AST），逐一提炼出用户在查询过程中的每个约束条件、子查询片段和关键节点。接着，「PARSQL 」会依照 SQL 的执行顺序来「讲故事」，从 FROM、WHERE 到 GROUP BY、HAVING，再到 ORDER BY，最后到SELECT，系统化地生成每一步的自然语言解释，为数据增强提供高质量训练样本。
- ### 数据增强和多任务学习策略
- 同一次训练中，并行优化Text-to-SQL和Text-to-Reason两个任务，让模型既会写SQL，也会「说理由」
- ### 高效选择策略
- 生成多组候选SQL和对应的「推理脚本」，通过N-gram相似度计算挑出最契合逻辑的那条
- ![](https://mmbiz.qpic.cn/mmbiz_png/TPrXz70LUrt11jzICAOcv3FnQXaWR4iakicAfJtImvryNzy90Gc5Sr2tIXaz6KQvP5EaP3mmLich4rBNEC4HcSnmw/640?wx_fmt=png&randomid=z53zr2pp&tp=webp&wxfrom=5&wx_lazy=1)
- https://mp.weixin.qq.com/s/ntw50QFj5R_6Z9yV1aRb4w
-
-