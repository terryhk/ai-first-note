# 目录

* [AI大模型学习实践笔记](README.md)

## 开篇

* [基础公理与Aha时刻](00_axioms/README.md)
  * [Steven的两周](00_axioms/0.1_steven_aha.md)
  * [十五年的笔记](00_axioms/0.2_my_aha.md)
  * [从Aha时刻到基础公理](00_axioms/0.3_axioms.md)
  * [本节小结](00_axioms/summary.md)

## 第一部分：AI大模型的思维方式

* [第一部分概述](part1_thinking/README.md)

* [第1章 谜题：为什么世界上没有完美的AI？](01_puzzle/README.md)
  * [1.1 两个怪现象](01_puzzle/1.1_two_weird_phenomena.md)
  * [1.2 第一性原理：AI在算概率](01_puzzle/1.2_first_principle.md)
  * [1.3 人类活在五维，AI死在四维](01_puzzle/1.3_five_dimensions.md)
  * [1.4 非确定性的实践含义](01_puzzle/1.4_nondeterminism.md)
  * [1.5 结果正确≠行为正确](01_puzzle/1.5_result_vs_behavior.md)
  * [1.6 概率工具箱](01_puzzle/1.6_probability_toolkit.md)
  * [本章小结](01_puzzle/summary.md)

* [第2章 稀缺的硬通货：Token与语义坐标](02_token/README.md)
  * [2.1 Token的双重面孔](02_token/2.1_token_two_faces.md)
  * [2.2 值不值？AI任务的经济考量](02_token/2.2_economic_consideration.md)
  * [2.3 Embedding：AI世界的"地理坐标"](02_token/2.3_embedding_coordinates.md)
  * [本章小结](02_token/summary.md)

* [第3章 契约精神：如何写一份无法违约的"交付规格书"](03_contract/README.md)
  * [3.1 Prompt的第一性](03_contract/3.1_contract_first_principle.md)
  * [3.2 4S原则](03_contract/3.2_4s_principles.md)
  * [3.3 思维链：合同的"分期付款"机制](03_contract/3.3_chain_of_thought.md)
  * [3.4 Few-shot示例驱动](03_contract/3.4_few_shot_examples.md)
  * [3.5 三层架构：Spec → Verifier → Environment](03_contract/3.5_three_layer_architecture.md)
  * [本章小结](03_contract/summary.md)

* [第4章 市场的进化：从赤手空拳到工具外挂](04_market/README.md)
  * [4.1 六个方案能力对比](04_market/4.1-six-solutions-comparison.md)
  * [4.2 Function Calling：签发授权委托书](04_market/4.2-function-calling.md)
  * [4.3 MCP：AI世界的统一接口](04_market/4.3-mcp.md)
  * [4.3.1 延伸阅读：MCP vs CLI](04_market/4.3.1-mcp-vs-cli.md)
  * [4.4 ReAct与PAL：Agent两大核心技术](04_market/4.4-react-pal.md)
  * [4.5 概率选型决策](04_market/4.5-probabilistic-selection.md)

* [第5章 技术世界的宏观调控：如何成为合格的贝叶斯裁判](05_governance/README.md)
  * [5.1 概率思维的核心方程](05_governance/5.1-core-equations.md)
  * [5.2 评估的本质：贝叶斯更新](05_governance/5.2-bayesian-update.md)
  * [5.3 迭代改进的循环](05_governance/5.3-iteration-loop.md)
  * [5.4 自动指标与人评的正确用法](05_governance/5.4-metrics-vs-human.md)
  * [延伸阅读：什么是贝叶斯推断](05_governance/5.5-bayesian-inference.md)

## 第二部分：AI大模型的实践笔记

* [第二部分概述](part2_practice/README.md)


* [第6章 实践1：告别"记得看过但找不到"——零代码搭一个AI知识库](06_personal_knowledge_base/README.md)
  * [6.1 为什么散落的知识没有复利？](06_personal_knowledge_base/6.1-scaling-inefficiency.md)
  * [6.2 RAG的零代码搭建思路](06_personal_knowledge_base/6.2-rag-zero-code.md)
  * [6.3 知识连接×AI：跨学科的顿悟时刻](06_personal_knowledge_base/6.3-knowledge-connection.md)
  * [6.4 每周知识整理工作流](06_personal_knowledge_base/6.4-weekly-workflow.md)
  * [6.5 概率工具箱与经济账](06_personal_knowledge_base/6.5-probability-toolbox.md)
  * [6.6 可复用模板](06_personal_knowledge_base/6.6-templates.md)

* [第7章 实践3：用AI赋能产品工作——周报、规范、分析与日常提效](07_product_work/README.md)
  * [7.1 产品经理的AI武器库概览](07_product_work/7.1_ai_weapon_overview.md)
  * [7.2 周报自动化的四步法](07_product_work/7.2_weekly_report_automation.md)
  * [7.3 规范对比的结构化方法](07_product_work/7.3_spec_comparison.md)
  * [7.4 产品运营分析](07_product_work/7.4_operations_analysis.md)
  * [7.5 沟通提效](07_product_work/7.5_communication_efficiency.md)
  * [本章小结](07_product_work/summary.md)

* [第8章 实践6：用Agent自动化重复任务——从ReAct到放手](08_agent_automation/README.md)
  * [8.1 Skill：Agent的"技能包"](08_agent_automation/8.1_skill.md)
  * [8.2 Harness：Agent的"运行时容器"](08_agent_automation/8.2_harness.md)
  * [8.3 ReAct：Agent的"大脑"](08_agent_automation/8.3_react.md)
  * [8.4 你的第一个Agent任务](08_agent_automation/8.4_first_agent_task.md)
  * [8.5 人在环](08_agent_automation/8.5_human_in_the_loop.md)
  * [本章小结](08_agent_automation/summary.md)

* [后记：焦虑消失之后，你的新起点](09_epilogue/README.md)

---

* [附录A：核心词汇表](appendix_glossary/README.md)
* [附录B：AWS AIF-C01 Core Knowledge Quick Reference](appendix_aws_aif/README.md)
