# ACL-main
- **[[SHARE: An SLM-based Hierarchical Action CorREction Assistant for Text-to-SQL]]**
- **[[DCG-SQL: Enhancing In-Context Learning for Text-to-SQL with Deep Contextual Schema Link Graph]]**
- **[[STaR-SQL: Self-Taught Reasoner for Text-to-SQL]]**
- **[[Uncovering the Impact of Chain-of-Thought Reasoning for Direct Preference Optimization: Lessons from Text-to-SQL]]**
- # ACL-Findings Papers
- **[[SQLForge: Synthesizing Reliable and Diverse Data to Enhance Text-to-SQL Reasoning in LLMs]]**
- **[[PARSQL: Enhancing Text-to-SQL through SQL Parsing and Reasoning]]**
- **[[UCS-SQL: Uniting Content and Structure for Enhanced Semantic Bridging In Text-to-SQL]]**
- # ACL-Accepted System Demonstrations Papers
- **[[Abacus-SQL: A Text-to-SQL System Empowering Cross-Domain and Open-Domain Database Retrieval]]**
- **[[ADEPT-SQL: A High-performance Text-to-SQL Application for Real-World Enterprise-Level Databases]]** (尚未公开)
- **[[VeriMinder: Mitigating Analytical Vulnerabilities in NL2SQL]]** (尚未公开)
- # ACL Industry Track Papers
- **[[SQLGenie: A Practical LLM based System for Reliable and Efficient SQL Generation]]**
- # ICML
- **[[Structure-Guided Large Language Models for Text-to-SQL Generation]]**
- **[[Alpha-SQL: Zero-Shot Text-to-SQL using Monte Carlo Tree Search]]**
- # AAAI
- **[[CogSQL: A Cognitive Framework for Enhancing Large Language Models in Text-to-SQL Translation]]**
- **[[SQLFixAgent: Towards Semantic-Accurate Text-to-SQL Parsing via Consistency-Enhanced Multi-Agent Collaboration]]**
- **[[Enhancing SQL Query Generation with Neurosymbolic Reasoning]]**
- **[[Filling Memory Gaps: Enhancing Continual Semantic Parsing via SQL Syntax Variance-Guided LLMs Without Real Data Replay]]**
- **[[Confidence Estimation for Error Detection in Text-to-SQL Systems]]**
- **[[MAGIC: Generating Self-Correction Guideline for In-Context Text-to-SQL]]**
- # NAACL
- **[[PRACTIQ: A Practical Conversational Text-to-SQL dataset with Ambiguous and Unanswerable Queries]]**
- **[[You Only Read Once (YORO): Learning to Internalize Database Knowledge for Text-to-SQL]]**
- **[[MSc-SQL: Multi-Sample Critiquing Small Language Models For Text-To-SQL Translation]]**
- **[[FLEX: Expert-level False-Less EXecution Metric for Text-to-SQL Benchmark]]**
- **[[H-STAR: LLM-driven Hybrid SQL-Text Adaptive Reasoning on Tables]]**
- **[[Track-SQL: Enhancing Generative Language Models with Dual-Extractive Modules for Schema and Context Tracking in Multi-turn Text-to-SQL]]**
-
-
- | 论文标题 | 核心方法/途径 | 主要贡献 | 主要技术关注领域 |
  | [[SHARE: An SLM-based Hierarchical Action CorREction Assistant for Text-to-SQL]] | 基于SLM的分层动作纠正：将SQL转换为动作轨迹，使用3个专门的SLM进行精细化修正，分层自演化训练。 | 精确错误定位，高效纠正，对LLM鲁棒，数据高效。 | 错误检测、自纠正、可靠性 |
  | [[DCG-SQL: Enhancing In-Context Learning for Text-to-SQL with Deep Contextual Schema Link Graph]] | 深度上下文模式链接图：利用图结构联合表示问题和数据库模式，改进示例检索。包括模式剪枝、基于图的编码器、自动化CoT提示。 | 卓越的示例检索，提升性能（尤其对小型LLM），高效。 | 推理、上下文学习、结构/模式理解 |
  | [[STaR-SQL: Self-Taught Reasoner for Text-to-SQL]] | 自学推理器：将SQL生成重构为推理驱动过程。LLM自生成CoT推理，根据正确结果微调，使用结果监督奖励模型（ORM）进行验证。 | 通过推理增强训练显著提升Text-to-SQL性能（Spider上86.6%执行准确率）。 | 推理、上下文学习 |
  | [[Uncovering the Impact of Chain-of-Thought Reasoning for Direct Preference Optimization: Lessons from Text-to-SQL]] | CoT增强DPO：通过合成CoT解决方案增强Text-to-SQL数据集，以激活DPO的有效性。包括执行引导的CoT DPO（ExCoT）。 | CoT对DPO至关重要，减轻奖励欺骗，增强判别能力，实现稳定性能提升。 | 推理、上下文学习 |
  | [[SQLForge: Synthesizing Reliable and Diverse Data to Enhance Text-to-SQL Reasoning in LLMs]] | 逆向数据合成：多阶段过程（SQL解析器、SQL工厂、模式架构师、问题逆向翻译器）合成可靠且多样的Text-to-SQL数据。 | 开源模型在Spider/BIRD上达到SOTA，显著缩小与闭源模型的差距，鲁棒性强。 | 数据增强/合成 |
  | [[PARSQL: Enhancing Text-to-SQL through SQL Parsing and Reasoning]] | DART-SQL：利用数据库内容进行问题重写，利用SQL执行结果进行执行引导修正。 | 通过利用数据库内容和执行反馈提高执行准确率。 | 结构/模式理解、错误检测/纠正 |
  | [[UCS-SQL: Uniting Content and Structure for Enhanced Semantic Bridging In Text-to-SQL]] |  |  | 错误检测、自纠正、实际系统设计 |
  | [[Abacus-SQL: A Text-to-SQL System Empowering Cross-Domain and Open-Domain Database Retrieval]] | 多组件系统：开放域数据库检索（Murre方法）、跨域可迁移性（融合数据增强）、SQL生成优化（Pre-SQL、自调试）。 | 高效的多数据库检索，增强的跨域适应性，改进的SQL准确性和效率。 | 数据增强/合成、实际系统设计 |
  |[[SQLGenie: A Practical LLM based System for Reliable and Efficient SQL Generation]]  | 混合代理系统：表导入器、混合SQL生成器（匹配与生成、思考与生成的多代理模式）、反馈增强、自动纠正器、模式剪枝。 | SOTA性能，生成速度提高64%，适用于工业应用，高可靠性、高效率。 | 实际系统设计、错误检测/纠正 |
  | [[Structure-Guided Large Language Models for Text-to-SQL Generation]] | SGU-SQL框架：结构感知链接（查询/模式的图表示、双图编码）、结构分解提示（语法树分解、增量生成）。 | 通过利用结构信息确保语义准确性和语法正确性，性能超越SOTA。 | 结构/模式理解 |
  | [[Alpha-SQL: Zero-Shot Text-to-SQL using Monte Carlo Tree Search]] | MCTS框架：将SQL渐进式构建建模为搜索问题。LLM作为动作模型生成CoT动作，自监督奖励函数确保一致性。 | 显著的零样本性能提升，无需微调，即插即用。 | 推理、上下文学习 |
  | [[CogSQL: A Cognitive Framework for Enhancing Large Language Models in Text-to-SQL Translation]] | 认知框架：模仿人类认知过程（SQL准备、CoT SQL生成、一致性检查SQL纠正）。 | 全面增强LLM的Text-to-SQL能力，有效缓解各种错误，泛化能力强。 | 推理、上下文学习、错误检测/纠正 |
  | [[SQLFixAgent: Towards Semantic-Accurate Text-to-SQL Parsing via Consistency-Enhanced Multi-Agent Collaboration]] | 多代理协作：SQLRefiner（核心）、SQLReviewer（橡皮鸭调试）、QueryCrafter（生成变体）。专注于语义错误检测和修复。 | 解决LLM生成SQL中的语义不准确问题，执行准确率提升3%+（Bird基准），令牌效率更高。 | 错误检测、自纠正、可靠性 |
  | [[Enhancing SQL Query Generation with Neurosymbolic Reasoning]] | 神经符号架构（Xander）：最佳优先搜索与回溯，对不完整查询进行符号检查（PQC），查询测试与修复（QTR），标准化SQL。 | 提升LM性能，减少运行时间，提高准确率，是模型规模扩展的替代方案，早期错误检测。 | 推理、上下文学习 |
  | [[Filling Memory Gaps: Enhancing Continual Semantic Parsing via SQL Syntax Variance-Guided LLMs Without Real Data Replay]] | LECSP（LLM增强持续语义解析）：记忆重构（领域无关问题/SQL骨架、组件偏差、伪样本生成）、记忆校准、任务感知双教师蒸馏。 | 在不进行数据回放/理想设置下实现CSP的SOTA，缓解遗忘，增强泛化，超越上限。 | 数据增强/合成 |
  | [[Confidence Estimation for Error Detection in Text-to-SQL Systems]] | 选择性分类器与基于熵的置信度：集成选择性分类器，使用熵进行置信度估计，分析模型校准。 | 改进错误检测，特别是针对不相关问题。强调模型校准对可靠性的重要性。 | 错误检测、自纠正、可靠性 |
  | [[MAGIC: Generating Self-Correction Guideline for In-Context Text-to-SQL]] | 多智能体指南生成：管理器、反馈、纠正代理迭代协作，自动化自纠正指南创建。自适应提示修订。 | 自动化指南生成，优于人工编写指南，增强可解释性，高效。 | 错误检测、自纠正、可靠性 |
  | [[PRACTIQ: A Practical Conversational Text-to-SQL dataset with Ambiguous and Unanswerable Queries]] | 新型数据集构建：创建PRACTIQ数据集，包含模糊和无法回答的问题，四轮对话结构，基于LLM的基线。 | 提供应对真实世界复杂性的关键基准，揭示SOTA在处理歧义/无法回答问题上的不足。 | 评估指标/基准进展、实际系统设计 |
-