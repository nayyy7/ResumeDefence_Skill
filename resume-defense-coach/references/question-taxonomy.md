# Question Taxonomy

This file defines the question categories used to build the hidden interview plan. It does **not** contain a static bank of fixed questions. Specific questions must be generated dynamically based on the user's project materials and previous answers.

---

## Category A: Project Motivation & Problem Definition

### What it assesses
Whether the user understands why the project exists, whether the need is real, and whether the problem boundary is clear.

### Basic directions
- 为什么开始这个项目？要解决什么问题？
- 原有方案或现状有什么不足？
- 目标用户或应用场景是什么？
- 如何判断这是一个值得解决的问题？

### Deep follow-up directions
- 你是如何确认这个需求真实存在的？
- 如果让你重新定义问题，你会怎么调整？
- 这个问题在你的领域中被解决到了什么程度？

### Common weaknesses
- Cannot articulate the core problem clearly.
- Confuses "what the project does" with "what problem it solves."
- No evidence that the problem actually exists.
- Problem scope is either too vague or too narrow without justification.

### Can transition to
- Category B (personal role in defining the problem)
- Category C (why this approach fits the problem)
- Category H (limitations of the problem framing)

---

## Category B: Personal Ownership & Contribution

### What it assesses
What the user personally did, not what the team collectively did.

### Basic directions
- 你负责的模块或部分是什么？
- 项目中哪个关键决策是你推动的？
- 哪部分工作是你独立完成的？
- 团队如何分工？你的角色是什么？

### Deep follow-up directions
- 你说的这部分，具体代码/实验/设计是你自己做的吗？
- 如果团队中有人离开，你的这部分能不能由别人接手？
- 你在项目中遇到的最大技术困难是什么，你怎么解决的？

### Common weaknesses
- Uses "we" for everything, cannot isolate personal contribution.
- Claims ownership but cannot explain implementation details.
- Describes team achievements as personal achievements.
- Cannot explain what they learned from their specific work.

### Can transition to
- Category C (was the method choice theirs?)
- Category E (implementation details they should know)
- Category H (personal challenges they faced)

---

## Category C: Method Selection & Alternatives

### What it assesses
Whether the method was chosen thoughtfully, and whether the user understands trade-offs.

### Basic directions
- 为什么选择这个方法/模型/框架？
- 在决定方案之前，你考虑过哪些替代方案？
- 这个方法和替代方案相比，优缺点分别是什么？

### Deep follow-up directions
- 如果你现在重新做这个项目，会换一个方法吗？
- 这个方法在什么场景下不适用？
- 替代方案中哪个最接近你的最终选择？为什么没选它？

### Common weaknesses
- Cannot name any alternative approach.
- Chose method "because it's popular" or "because the advisor said so."
- Cannot compare trade-offs concretely.
- Overclaims the chosen method without acknowledging its weaknesses.

### Can transition to
- Category D (technical principles of the chosen method)
- Category H (limitations encountered due to method choice)
- Category K (what they would do differently now)

---

## Category D: Technical Concepts & Fundamentals

### What it assesses
Whether the user truly understands the technical concepts they mention, not just the names.

### Key concept areas (examples, not exhaustive)

**LLM & Transformers**
- decoder-only architecture
- autoregressive generation
- token and tokenization
- embedding and semantic representation
- attention mechanism (self-attention, cross-attention, multi-head)
- positional encoding

**Training & Fine-tuning**
- pre-training vs SFT vs RLHF
- cross-entropy loss
- learning rate scheduling
- overfitting and regularization
- gradient accumulation

**RAG & Retrieval**
- chunking strategies and trade-offs
- embedding models and their properties
- vector database and similarity search
- top-k and relevance threshold
- hybrid search (sparse + dense)
- re-ranking

**Prompting & Agent**
- prompt engineering principles
- few-shot, chain-of-thought, tree-of-thought
- tool use and function calling
- agent workflow design
- multi-agent collaboration

**Evaluation**
- BLEU, ROUGE, BERTScore, and their limitations
- human evaluation design
- LLM-as-judge
- offline vs online evaluation
- A/B testing for LLM products

**Multimodal**
- vision-language models
- cross-modal alignment
- modality fusion strategies

### Basic directions
- 你提到了 [概念 X]，能解释一下它的基本原理吗？
- 在你的项目中，[概念 X] 具体是怎么用的？
- 为什么 [概念 X] 适合你的场景？

### Deep follow-up directions
- [概念 X] 在你的场景下有什么局限性？
- 如果不用 [概念 X]，有没有其他方式可以达到类似效果？
- 你了解 [概念 X] 的最新发展吗？和你的用法有什么不同？

### Common weaknesses
- Knows the name but cannot explain the mechanism.
- Explains by analogy only, no technical depth.
- Cannot connect the concept to its use in their project.
- Confuses related but distinct concepts.

### Can transition to
- Category E (implementation details involving the concept)
- Category F (how the concept affects experiment design)
- Category J (trends related to this concept)

---

## Category E: Implementation & Engineering Details

### What it assesses
Whether the user can explain how the project was actually built.

### Basic directions
- 你的技术栈是什么？为什么这样选？
- 项目代码结构是怎样的？
- 数据处理流程是怎样的？
- 遇到了哪些工程上的困难？

### Deep follow-up directions
- 你的训练/推理 pipeline 怎么设计的？
- 怎么处理数据不平衡/噪声/缺失问题？
- 项目的可扩展性如何？如果数据量增加 10 倍呢？
- 你是怎么调试和验证实现正确性的？

### Common weaknesses
- Cannot describe the code structure or pipeline.
- Never wrote core implementation code.
- Cannot explain data preprocessing decisions.
- No awareness of engineering best practices.

### Can transition to
- Category D (technical principles of key components)
- Category H (engineering difficulties that became limitations)
- Category F (how implementation choices affect experiments)

---

## Category F: Data & Experiment Design

### What it assesses
Whether the user understands proper experiment design and data handling.

### Basic directions
- 你的数据从哪里来？规模多大？
- 数据怎么划分训练/验证/测试集？
- 你怎么确保测试集没有泄漏？
- 实验设置是怎样的？

### Deep follow-up directions
- 数据有什么 bias？你怎么处理的？
- 你的数据标注质量如何控制？
- 如果换一个数据集，你的结论还成立吗？
- 消融实验做了哪些？每个模块的贡献是多少？

### Common weaknesses
- Cannot describe the dataset in detail.
- No awareness of data leakage risks.
- Test set is not truly held out.
- Never did ablation studies.
- Confuses correlation with causation.

### Can transition to
- Category G (metrics and what they actually measure)
- Category H (data limitations)
- Category K (better experiment design)

---

## Category G: Metrics & Results

### What it assesses
Whether the user's claimed results are meaningful and well-measured.

### Basic directions
- 你用什么指标评测？为什么选这些指标？
- Baseline 是什么？你的方法比 baseline 提升了多少？
- 你的结果在统计上显著吗？

### Deep follow-up directions
- 这个指标在你的场景下有什么局限性？
- 提升 30% 意味着什么？对用户体验有什么实际影响？
- 你的结果可复现吗？其他人能跑出同样的数字吗？
- 有没有做过错误分析？主要失败在什么 case 上？

### Common weaknesses
- Claims "accuracy improved by X%" without defining accuracy.
- No baseline comparison.
- Cannot explain what the metric actually measures.
- No statistical significance testing.
- Results are cherry-picked.

### Can transition to
- Category H (what the results don't tell you)
- Category F (experiment design that produced these results)
- Category K (how to improve measurement)

---

## Category H: Challenges, Failures & Trade-offs

### What it assesses
Whether the user has honest self-awareness about their project's weaknesses.

### Basic directions
- 项目中遇到的最大挑战是什么？
- 有什么是你想做但没做到的？
- 这个方案在什么情况下会失败？

### Deep follow-up directions
- 你做过的最重要的 trade-off 是什么？为什么这样取舍？
- 如果让你指出项目中最薄弱的一环，是什么？
- 你有没有遇到过让你改变方向的关键失败？

### Common weaknesses
- "It worked great, no real challenges."
- Cannot name a single failure case.
- Describes only technical difficulties, not design trade-offs.
- No awareness of when the approach breaks down.

### Can transition to
- Category K (how to address the failures)
- Category I (whether the innovation survived the challenges)
- Category L (product trade-offs vs technical trade-offs)

---

## Category I: Innovation & Contribution

### What it assesses
Whether the claimed innovation is genuine and the user can position it against prior work.

### Basic directions
- 你的项目相比现有方案，最大的不同是什么？
- 你认为最重要的贡献是什么？
- 相关工作有哪些？你的位置在哪里？

### Deep follow-up directions
- 如果审稿人会说"这只是一个工程改进"，你怎么回应？
- 你的方法中哪个部分是真正新的，哪个部分是工程组合？
- 有没有想过你做的这件事别人也做过？你怎么确认 novelty？

### Common weaknesses
- Claims innovation but cannot compare to related work.
- Novelty is exaggerated — "first to do X" without verification.
- Confuses engineering effort with research contribution.
- Cannot articulate what makes the contribution significant.

### Can transition to
- Category J (how the field views this contribution)
- Category K (next steps to strengthen the contribution)

---

## Category J: Domain Understanding & Trends

### What it assesses
Whether the user follows the broader field beyond their own project.

### Basic directions
- 你怎么看这个领域最近一年的发展？
- 你觉得这个方向未来会怎么走？
- 有哪些重要的相关工作是你们项目之后出现的？

### Deep follow-up directions
- 如果现在重新做，有哪些新技术可以用？
- 你觉得当前领域的最大瓶颈是什么？
- 你的项目在领域发展趋势中的位置是什么？

### Common weaknesses
- Cannot name any recent related work beyond their own project.
- Overestimates the significance of their narrow sub-area.
- No opinion on where the field is headed.
- Cannot connect their work to broader trends.

### Can transition to
- Category K (how future trends could change their approach)
- Category D (new technical concepts from recent work)

---

## Category K: Future Work & Counterfactuals

### What it assesses
Research thinking and the ability to plan next steps grounded in current limitations.

### Basic directions
- 如果有更多时间和资源，你会做什么？
- 你的下一步研究计划是什么？
- 如果这个项目要继续，最重要的改进方向是什么？

### Deep follow-up directions
- 如果去掉 [某个模块]，重新设计，你会怎么做？
- 如果给你一个很大的变化（例如：数据变成 100 倍，或用完全不同的模型架构），你的方案还 work 吗？
- 如果你现在拿到负面结果，发现你的核心假设是错的，你怎么办？

### Common weaknesses
- No concrete next steps, only vague "improve the model."
- Cannot think counterfactually.
- Assumes the current approach is the only approach.
- No prioritization among future directions.

### Can transition to
- Category H (future work should address specific limitations)
- Category J (future work informed by trends)

---

## Category L: AI Product Manager Specific

### What it assesses
For AI product roles: whether the user understands product thinking around AI/LLM applications.

### Basic directions
- 为什么这个场景需要 LLM？规则或传统 ML 不行吗？
- 用户真正的需求是什么？你是怎么验证的？
- 模型的哪些能力边界影响了你的产品设计？

### Deep follow-up directions
- 如何设计离线评测和在线评测来验证产品效果？
- Prompt、RAG、Workflow、微调在你的产品中分别解决什么问题？
- 怎么控制幻觉、成本、时延和稳定性？
- 用户需要的是模型能力，还是一整套工作流？
- 如果模型的某个能力提升了 10 倍，你的产品设计会变吗？

### Common weaknesses
- Cannot distinguish when LLM is and isn't needed.
- No evaluation strategy for LLM product quality.
- Ignores cost, latency, and reliability trade-offs.
- Product thinking is "add AI" without understanding what AI changes.

### Can transition to
- Category C (method selection from product perspective)
- Category G (product metrics vs model metrics)

---

## Weight Adjustment by Interview Type

| Category | 考研复试 | 科研面试 | 算法实习 | AI产品实习 |
|---|---|---|---|---|
| A. Motivation & Problem | High | High | Medium | High |
| B. Personal Ownership | High | High | High | Medium |
| C. Method Selection | Medium | High | High | High |
| D. Technical Concepts | High | High | High | Medium |
| E. Implementation | Medium | Medium | High | Low |
| F. Data & Experiments | Medium | High | High | Medium |
| G. Metrics & Results | Medium | High | High | High |
| H. Challenges & Failures | Medium | High | Medium | Medium |
| I. Innovation | Low | High | Medium | Medium |
| J. Domain & Trends | Medium | High | Medium | High |
| K. Future Work | Medium | High | Medium | Medium |
| L. AI PM Specific | Low | Low | Low | High |

**Weight scale**: High = must cover, Medium = cover if time allows, Low = optional unless prompted by the user's material.

---

## Interview Depth Stage Mapping

Use this mapping when building the hidden interview plan so the interview follows a shallow-to-deep arc.

| Stage | Primary categories | Typical depth band |
|---|---|---|
| `PROJECT_OVERVIEW` | A. Motivation & Problem | L1 |
| `PERSONAL_CONTRIBUTION` | B. Personal Ownership | L1–L2 |
| `METHOD_REASONING` | C. Method Selection & Alternatives | L2–L3 |
| `IMPLEMENTATION` | E. Implementation, F. Data & Experiments, G. Metrics & Results | L2–L3 |
| `TECHNICAL_DEPTH` | D. Technical Concepts & Fundamentals | L3–L4 |
| `CHALLENGE` | H. Challenges & Failures, K. Future Work & Counterfactuals | L3–L4 |

Secondary categories are woven into the stage they serve: I. Innovation fits `METHOD_REASONING` / `CHALLENGE`, J. Domain & Trends fits `CHALLENGE`, L. AI PM Specific spans the product interview arc.

The stage sets the default depth band for a project's questions; the follow-up machinery (`references/follow-up-strategies.md`) may still escalate within or beyond the band based on answer quality.
