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
- # 主要发现总结（Gemini总结的）
  
  近期Text-to-SQL领域取得了显著进展，主要由大型语言模型（LLM）驱动。这些进展体现在多个关键方面：
- A. 增强推理和搜索策略
- B. 改进错误纠正和鲁棒性。增强Text-to-SQL系统检测和纠正错误的能力，从而提高其整体鲁棒性，是研究的关键领域。这涉及复杂的多代理框架和执行引导的细化技术。
- C. 优化数据效率和泛化能力。解决数据稀缺性挑战和增强Text-to-SQL模型的泛化能力对于其广泛采用至关重要。这涉及创新的数据合成、持续学习和知识内化策略。
- D. 推进上下文理解和多轮交互。Text-to-SQL系统的演进超越了单轮查询翻译，涵盖了对话交互的复杂性，包括多轮对话、歧义解决和处理无法回答的问题。
- E. Text-to-SQL的评估指标和基准测试。准确的评估对于推进Text-to-SQL系统至关重要。然而，传统指标已显示出显著局限性，导致了更复杂、更对其人类的评估方法的发展。
- | 论文标题 | 核心方法/途径 | 主要贡献 | 主要技术关注领域 |
  :LOGBOOK:
  CLOCK: [2025-07-23 Wed 16:17:00]
  :END:
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
  | [[You Only Read Once (YORO): Learning to Internalize Database Knowledge for Text-to-SQL]] | **内部化数据库知识**：提出了一种方法让模型将数据库的知识（如模式和内容）内部化到其参数中，而不是在每次推理时都显式地读取这些知识。通过**预训练任务**和**结构化提示学习**实现。这减少了对大量上下文窗口的需求，并降低了推理成本。| 大幅降低了Text-to-SQL模型的**推理成本和延迟**，特别是在面对大型数据库时。提高了在低资源环境下的效率和性能，且能更好地处理复杂查询。 | LLM增强方法；模式链接与理解技术；效率与实际部署考量 |
  | [[MSc-SQL: Multi-Sample Critiquing Small Language Models For Text-To-SQL Translation]] | **多样本批评（Multi-Sample Critiquing）**：针对小型、开源LLM，通过生成多个SQL候选，然后使用一个**批评模型**（critique model）来评估这些候选，选出最佳的SQL，或提供反馈进行优化。该批评模型可以是一个更强大的LLM或经过微调的SLM。 | 显著提升了小型、开源LLM在Text-to-SQL任务上的性能，使其能够达到甚至超越大型LLM的水平，同时**降低了部署成本**和计算资源需求。 | LLM增强方法；错误检测、纠正与鲁棒性提升；效率与实际部署考量 |
  | [[FLEX: Expert-level False-Less EXecution Metric for Text-to-SQL Benchmark]] | 提出了一种新的Text-to-SQL评估指标，旨在**纠正传统执行准确性度量中的缺陷**，特别是那些因数据库状态、SQL方言差异或评估环境限制导致的误判（假阳性/假阴性）。通过更精细的SQL解析和执行结果验证来提高评估的可靠性。 | 提供了一个**更准确、更可靠**的Text-to-SQL模型评估方法，能够更真实地反映模型性能，避免了现有度量标准造成的误导，有助于更公平地比较不同模型。 | 评估指标与基准数据集构建 |
  | [[H-STAR: LLM-driven Hybrid SQL-Text Adaptive Reasoning on Tables]] | 提出一个由LLM驱动的混合推理框架，结合了**符号（SQL）和文本推理**。它能根据表格数据和用户查询的复杂性，**自适应地选择**是使用SQL查询、文本推理还是两者的结合来回答问题，尤其适用于表格问答（Table QA）任务。 | 实现了在表格问答任务中**更灵活、更准确的推理**，弥补了单一模式（纯SQL或纯文本）的不足，在各种表格推理数据集上表现出SOTA性能。 | LLM增强方法；神经符号方法；推理与上下文学习 |
  | [[Track-SQL: Enhancing Generative Language Models with Dual-Extractive Modules for Schema and Context Tracking in Multi-turn Text-to-SQL]] | **双抽取模块**：在多轮对话式Text-to-SQL中，通过引入专门的**模式抽取模块**（Schema Extraction Module）和**上下文跟踪模块**（Context Tracking Module）来增强LLM。这些模块分别负责从对话历史中识别和跟踪相关的数据库模式信息以及上下文依赖。 | 显著提高了生成式语言模型在**多轮Text-to-SQL**任务中的性能，特别是对**模式和上下文变化的适应性**，使得模型能够更准确地处理复杂的、跨回合的查询。 | 多轮对话式Text-to-SQL；模式链接与理解技术；LLM增强方法 |
-
- # 未来研究方向与开放挑战
  
  尽管取得了显著进展，Text-to-SQL领域仍面临多项开放挑战和未来研究方向：
- **对多样化和噪声输入的鲁棒性：** 需要进一步研究如何处理高度模糊、格式不佳或不完整的自然语言查询，从结构化对话转向更灵活的人机交互。
- **可扩展到极其庞大和复杂的模式：** 尽管已取得进展，但为包含数千个表和列的数据库高效准确地生成SQL仍然是一项重大挑战。
- **增强可解释性：** 除了生成正确的SQL，未来的系统应提供清晰的推理解释，尤其是在出现错误或需要澄清时，以建立用户信任。
- **动态环境中的持续学习：** 开发鲁棒的持续学习策略，能够在不发生灾难性遗忘或损害数据隐私的情况下适应不断演变的数据库模式和用户查询模式，对于长期部署至关重要。
- **现实世界场景的基准测试：** 创建更全面、更具挑战性的基准，真正反映工业应用的复杂性（例如，效率指标、歧义处理、无法回答性、多轮上下文、领域泛化），对于推动有意义的进展至关重要。
- **高效且经济的部署：** 模型压缩、高效推理技术和优化系统架构方面的持续创新将是使高性能Text-to-SQL系统广泛可用且经济可行的必要条件。
  **与更广泛AI系统的集成：** 探索如何将Text-to-SQL无缝集成到更大的AI系统中（例如，知识图谱、分析平台），以实现更复杂的数据驱动应用。
-