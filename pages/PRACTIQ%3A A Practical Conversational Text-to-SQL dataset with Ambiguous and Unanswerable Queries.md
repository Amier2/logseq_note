## 背景
- • 真实场景中，用户问题往往：
	- – 有歧义：一句话对应多种 SQL 写法；
	- – 无法回答：所需列/值/表在库里根本不存在。
- • 缺乏公开数据 → 模型/系统从未被系统评测或训练过此类能力。
- ## 贡献
- 一个数据集
- 以 Spider dev 为基础，利用规则 + LLM 修改 schema 或问题本身
- – 4 类模糊问题：SELECT 列歧义、WHERE 列歧义、列内取值歧义、过滤条件歧义。
  – 4 类无法回答：缺失 SELECT 列、缺失 WHERE 列、缺失过滤值、不支持的连接。
- • 对话流程
  ① 初始问题（可能模糊/无法回答）
  ② 系统澄清询问（或直接给出带说明的 SQL）
  ③ 用户澄清回复
  ④ 系统给出最终 SQL + 自然语言解释 + 执行结果