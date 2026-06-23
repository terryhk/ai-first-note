# 附录B：AWS AIF-C01 Core Knowledge Quick Reference

> 本附录基于我备考 AWS Certified AI Practitioner (AIF-C01) 的学习笔记整理。AIF-C01 是 AWS 于2024年推出的AI从业者认证，覆盖 Generative AI 基础、Prompt Engineering、AWS AI/ML 服务、Responsible AI 与安全治理四大领域。我在2025年3月以 890/1000 通过考试——这个分数不算特别高，但足以验证：如果理解了本书前8章的核心概念，AIF-C01 的大量知识点其实是你已经掌握的知识在 AWS 产品上的映射。

### B.1 Fundamentals — 生成式AI基础

**Generative AI (GenAI)** — 深度学习的子集，能生成与训练数据相似的新数据（文本、图像、音频、代码、视频等）。→ 核心思想回扣第1章：AI不是检索答案，是基于概率生成

**Foundation Models (FM)** — 用大量无标签数据通过自监督学习预训练的大模型，可执行多种任务（生成文本、摘要、提取信息、聊天等）。例：GPT-4o、BERT。→ 自监督学习即"模型自己造标签"，见开篇

**Large Language Models (LLM)** — 基于Foundation Models的一类，专门用于生成连贯的类人文本。→ 见第2章 Token

**Tokenization** — 将原始文本拆分为token序列的过程。例："Stephane" 可能被拆为 "Steph" + "ane"。→ 见第2章，Token是AI世界的"货币"

**Context Window** — LLM生成文本时能考虑的token数量上限。例：GPT-4 Turbo 128K、Claude 2 1.2M、Gemini 1.5 Pro 1M。越大越好，但更费内存和算力。→ 见第2章"预算约束"

**Embeddings** — 将token转换为数值向量（如100维），编码语义信息（含义、语法角色、情感等）。向量越接近，语义越相似。→ 见第2章"语义坐标"

**Vectors & Vector Database** — Embeddings存储在向量数据库中，通过最近邻算法实现语义相似度搜索，是RAG的基础。→ 见第2章 Embedding + 第4章方案选型

**Training vs Inference** — Training：用数据训练模型参数；Inference：用训练好的模型对新数据做预测。Inference分实时（聊天机器人）、批处理（大规模数据分析）、边缘推理（手机/树莓派，常用SLM）。→ 见第5章 迭代与评估

**Parameters** — 模型在训练过程中学到的内部变量（权重和偏置），决定了模型的行为。参数越多，模型能力越强，但训练和推理成本也越高。

**Non-deterministic Outputs** — LLM通过概率分布预测下一个词，因此相同prompt可能产生不同输出。→ 这就是第1章"幽灵vs狗"的技术根源：AI是概率采样系统，不是确定性搜索引擎

**Diffusion Models** — 图像生成模型的原理：前向过程逐步加噪直到不可识别，生成时从纯噪声反向去噪。例：Stable Diffusion。→ 与LLM的概率采样异曲同工，都是"从概率分布采样"

**RLHF (Reinforcement Learning from Human Feedback)** — 将人类反馈整合到奖励函数中，使模型输出与人类偏好对齐。流程：收集人类数据→SFT监督微调→构建奖励模型→优化策略。→ 见第5章"行为×概率=结果"的工程实现

### B.2 Prompt Engineering & Optimization — 提示词工程与优化

**Prompt Engineering** — 开发、设计和优化prompt，引导FM产生符合需求的输出。四个组件：Instruction（指令）、Context（上下文）、Input Data（输入数据）、Output Indicator（输出格式）。→ 见第3章"契约精神"

**Zero-Shot Prompting** — 不提供任何示例，直接给模型任务。适合简单任务。→ 见第3章 4S原则

**Few-Shot Prompting** — 提供1-3个示例引导模型输出风格和格式。一个示例叫One-Shot。→ 见第3章 Few-shot

**Chain-of-Thought (CoT) Prompting** — 将复杂任务分解为推理步骤，加"think step by step"等提示。可与Zero-shot或Few-shot组合。→ 直接回扣第3章"思维链"——"一步步想"的分期付款机制

**Negative Prompting** — 明确告诉模型不要包含什么。"不要做X"有时比"要做Y"更有效。→ 见第3章 契约中的排除条款

**System Prompts** — 设置模型的行为基调，如"你是一位AWS教师"。→ 见第3章"角色设定"

**Temperature** — 控制输出创造性。低温(0.2)→保守确定；高温(1.0)→多样创意。→ 见第1章 概率采样的"旋钮"

**Top P** — 只考虑累计概率达到Top P值的词。低Top P(0.25)→更连贯；高(0.99)→更多样。→ 与Temperature协同控制概率采样

**Top K** — 只考虑概率最高的K个词。低K(10)→连贯；高K(500)→多样。→ 同上

**RAG (Retrieval-Augmented Generation)** — 让模型引用外部数据源（无需微调），动态获取最新和特定信息。数据源如S3、Confluence、SharePoint等；向量数据库可选OpenSearch、Aurora、Neptune、Pinecone等。→ 回扣第2章Embedding理解 + 第4章方案选型：RAG是"查资料再回答"，不是"凭记忆回答"

**Fine-tuning vs RAG vs Prompt Engineering** — 三条改进路径的成本递增：
1. Prompt Engineering：最便宜，不改模型
2. RAG：中等成本，需维护向量数据库，不改模型
3. Fine-tuning：最贵，需额外算力
→ 回扣第4章六方案对比——从轻到重，从便宜到昂贵

**Instruction-based Fine-Tuning** — 用标注的prompt-response对微调，让模型以特定方式回应。

**Continued Pre-Training (Domain-Adaptation)** — 用无标签领域数据继续预训练，让模型成为领域专家。成本更高。→ 类比：Prompt Engineering是"面试辅导"，Fine-tuning是"上岗培训"，Continued Pre-Training是"读个学位"

**LoRA / PEFT** — Parameter-Efficient Fine-Tuning，只微调少量参数而非全量，大幅降低成本。→ 见第4章 Fine-tuning的轻量替代方案

**Agents** — 能自主思考和多步执行任务的智能体，配置Action Group定义可执行操作，可接入API/Lambda/知识库。背后使用Chain of Thought规划步骤。→ 回扣第8章 Agent自动化——AWS Bedrock Agent 就是第8章 ReAct 模式的云服务实现

### B.3 AWS AI/ML Core Services — AWS AI/ML核心服务

**Amazon Bedrock** — 核心平台。统一API访问多家FM（Anthropic Claude、Meta Llama、Cohere、Amazon Titan等），按使用量付费（On-Demand / Batch / Provisioned Throughput）。→ 本书的"云上AI工具箱"

**Amazon Titan** — AWS自研Foundation Model系列，使用自监督学习。→ Bedrock里的"自家模型"

**Amazon SageMaker** — ML全流程平台：数据准备（Data Wrangler）→训练→调参（AMT）→部署（实时/无服务器/批处理/异步）→监控（Model Monitor）。含Canvas无代码界面、JumpStart模型商店、Clarify偏差检测等。→ ML工程师的"全功能厨房"

**Amazon Q Business** — 面向企业员工的GenAI助手，基于公司内部数据，支持40+数据源连接器。内置Guardrails和IAM权限控制。→ 企业版"半人马协作"

**Amazon Q Developer** — AI编程助手，支持代码建议、安全扫描、AWS文档问答。分Free/Pro($20/月)两层。→ 程序员的AI pair programmer

**Amazon Comprehend** — NLP服务，从文本中提取洞察、实体、情感。可自定义术语。→ "AI读心术"

**Amazon Transcribe** — 语音转文字，自动移除PII（redaction），支持多语言。Medical版本符合HIPAA。→ "AI耳朵"

**Amazon Rekognition** — 图像/视频分析：人脸检测与搜索、内容审核、目标标签、名人识别、自定义标签。→ "AI眼睛"

**Amazon Textract** — 从文档（PDF/图片）自动提取文本、表格和结构化数据，支持查询。→ "AI文档扫描仪"

**Amazon Translate** — 神经机器翻译，支持标准和自定义翻译。→ "AI翻译官"

**Amazon Polly** — 文本转语音，支持SSML标记、自定义发音词典（Lexicons）、多种语音引擎（neural/standard/generative/long-form）。→ "AI嘴巴"

**Amazon Lex** — 构建聊天机器人的服务，集成ASR+NLU，可连接Lambda/Connect等。→ "AI客服引擎"

**Amazon Personalize** — 实时个性化推荐，使用与Amazon.com同样的技术。→ "AI导购"

**Amazon Kendra** — 智能搜索服务，支持自然语言查询、文档索引、增量学习。→ "企业版Google"

**Amazon OpenSearch Service** — 支持向量搜索（KNN），是RAG的常用向量数据库选择。→ 见第2章向量数据库 + 第4章RAG

**Amazon A2I (Augmented AI)** — 将人工审核整合进ML工作流。与SageMaker Ground Truth配合，用于数据标注和RLHF。→ "人在环"——回扣第5章贝叶斯裁判 + 第8章检查点

**Amazon HealthScribe** — 分析医患对话自动生成临床笔记。→ 医疗行业AI应用

### B.4 Responsible AI & Security — 负责的AI与安全

**Hallucination（幻觉）** — LLM因概率采样而产生看似合理但实际错误的内容。→ 第1章"幽灵vs狗"，第3章"契约精神"就是防幻觉的第一道防线

**Bias（偏差）** — 模型输出中的系统性偏好，可能来自训练数据的偏差。SageMaker Clarify用于检测偏差。→ 第5章"结果正确≠行为正确"

**Toxicity（毒性）** — 模型生成的有害内容。策略包括策展训练数据（Curating Training Data）和设置Guardrails。→ 输出端的可控性问题

**Guardrails for Amazon Bedrock** — 控制用户与FM的交互：屏蔽特定话题、过滤有害内容、移除PII、减少幻觉（Contextual Grounding）。可叠加多层。→ 第3章"契约"的AWS实现——给AI加围栏

**Data Privacy & PII Handling** — 保护个人可识别信息。Amazon Macie扫描S3中的敏感数据；Transcribe自动redact PII；Guardrails自动mask PII。→ 数据输入端的合规性

**Model Evaluation** — 两种方式：自动评估（程序化指标 + Model-as-Judge）和人工评估（AWS Managed Team或自带团队）。关键指标：ROUGE（摘要/翻译召回率）、BLEU（翻译精度）、BERTScore（语义相似度）、Perplexity（预测置信度）。→ 回扣第5章评估方法论

**Human Review** — 通过A2I实现"人在环"，对模型输出进行人工审核。→ 第8章"检查点"的AWS标准化

**Prompt Injection / Jailbreaking** — 恶意输入操纵模型行为。防范：在System Prompt中添加忽略无关内容的指令，使用Guardrails。→ 第3章契约中的"防篡改条款"

**Overfitting & Underfitting** — 过拟合：训练集好但新数据差；欠拟合：训练集和测试集都差。防止方法：增大数据、早停、数据增强。→ 第5章"行为×概率=结果"的统计学基础

**Confusion Matrix** — 分类模型评估工具，衍生的关键指标：Precision（精确率）、Recall（召回率）、F1 Score（调和平均）、Accuracy（准确率）。→ 评估AI输出质量的量化工具

**AWS Shared Responsibility Model** — AWS负责基础设施安全，客户负责数据安全、IAM配置、Guardrails设置、合规审计。→ 安全是"半人马"的——AWS守基础设施，你守应用层

**Compliance** — AWS符合NIST、ISO、SOC、HIPAA、GDPR、PCI DSS等标准。可用AWS Artifact获取合规报告，AWS Config追踪配置变更。→ 企业AI必须过的合规关

**MLOps** — DevOps在ML领域的延伸：版本控制、自动化、CI/CD、持续再训练、持续监控。SageMaker Pipeline实现ML工作流自动化。→ 第5章DMAIC循环的工程化

### B.5 Exam Tips — 备考策略与考试经验

**考试结构** — 65道题（多选+多答），120分钟，满分1000，及格线700。四大领域权重：
1. Fundamentals of AI and ML (~20%)
2. Fundamentals of Generative AI (~24%)
3. Applications of Foundation Models (~28%)
4. Guidelines for Responsible AI (~28%)

**重点领域** — 考试最密集的知识点：
- RAG是什么、怎么配置、用什么向量数据库 → 第2+4章
- Prompt Engineering技术对比（Zero/Few/CoT）→ 第3章
- Fine-tuning vs RAG vs Prompt Engineering的适用场景和成本对比 → 第4章
- Bedrock Guardrails的功能和配置 → 第3章契约精神
- Responsible AI的挑战（Hallucination/Bias/Toxicity）和缓解措施 → 第1+5章
- 选择正确的AWS服务匹配业务场景 → 理解"工具选型"思维

**备考策略** — 我的方法：
1. 先过一遍Stephane Maarek的Udemy课程（本笔记的来源），建立知识框架
2. 重点做Section Quiz和Practice Exam，错的回去重看
3. 自己画AWS服务脑图——理解服务之间的关系比记忆单个服务更重要
4. 考试前一天复习本题笔记的B.1-B.4

**我的890/1000** — 不算高分，但足以总结几个教训：
- "选择最合适的AWS服务"类题目占比很大。关键不是记住每个服务的参数，而是理解"这个场景需要什么能力，哪个服务提供这个能力"。这和第4章"方案选型"的逻辑一模一样
- Responsible AI占分很重（28%），不要忽视。很多题考的不是"什么是bias"，而是"用什么AWS服务检测bias"——答案是SageMaker Clarify
- 考试中遇到不确定的题，先排除明显错误选项，在剩余选项中选"最安全、最通用"的那个——这就是第1章"五维思考"中的概率判断

**与本书的联系** — 如果你已经读懂了这本书的前8章，AIF-C01约有60-70%的知识点你已经掌握了底层逻辑。剩下的30-40%是AWS产品的特定配置和认证考试的套路。把本书的理解作为"思维框架"，把AWS文档和Practice Exam作为"细节填充"，备考效率会远高于从零开始。
