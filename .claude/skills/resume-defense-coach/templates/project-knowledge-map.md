# Project Knowledge Map

> **Internal template** — used by the agent during MATERIAL_ANALYSIS and INTERVIEW_PLANNING phases.
> Do **NOT** display this to the user during the interview. This is for the agent's reasoning only.

---

## Candidate Context

- **Interview type:** [考研复试 / 科研面试 / 算法实习 / AI产品实习 / 其他]
- **Target program/role:** [目标学校/专业/岗位]
- **Target direction:** [研究方向/产品方向]
- **Difficulty:** [初级 / 中级 / 高级 / 压力面试]
- **Target main question count:** [默认 8]
- **Follow-up mode:** [ON 动态追问 / OFF 关闭追问，仅记录]
- **Language:** [中文 / English / 中英混合]

---

## Project [N]: [Project Name]

### Basic Information

- **Project name:**
- **Source evidence:** [简历 / 用户描述 / 论文 / 项目报告 / README / PPT / 其他]
- **Background:** [项目背景，从材料中提取]
- **Problem being solved:** [核心问题]
- **Target users / application scenario:** [用户或应用场景]
- **Goal:** [项目目标]

### Technical Details

- **Methods / models / technology stack:** [使用的方法、模型、技术]
- **Workflow / pipeline:** [项目流程]
- **Data sources:** [数据来源]
- **Data scale:** [数据规模，如果材料中提到]
- **Experiment / evaluation setup:** [实验设置]
- **Metrics:** [评测指标]
- **Results:** [项目结果]
- **Implementation details:** [实现细节]

### Responsibility & Team

- **User's stated personal responsibilities:** [用户声称的个人职责]
- **Team structure (if mentioned):** [团队分工]
- **Collaboration boundary:** [个人与团队的协作边界]

### Quality & Reflection

- **Challenges encountered:** [遇到的难点]
- **Decisions and trade-offs made:** [决策取舍]
- **Claimed innovation:** [声称的创新点]
- **Limitations acknowledged in materials:** [材料中已提到的限制]
- **Future work mentioned:** [材料中提到的未来方向]

### Knowledge Map

- **Related concepts to probe:** [与项目相关的基础概念和延伸知识]
- **Key technical terms used:** [使用的关键技术术语]

### Risk & Gap Analysis

- **Missing information:** [材料中缺失的关键信息]
- **Potential contradictions:** [材料内部的潜在矛盾]
- **High-risk resume claims:** [简历中可能被质疑的表述]
- **Vague or ambiguous statements:** [模糊或可能被误解的表述]
- **Unverified inferences:** [从材料中推测但未明确证实的内容 — 标记为"待确认"]

---

## Project Coverage Plan

> Build during INTERVIEW_PLANNING when the resume contains 2+ major projects. Update counters during INTERVIEWING.

- **projects_detected:** [Project A, Project B, Project C, ...]
- **Prioritization basis:** [项目重要程度 / 简历篇幅 / 目标面试方向 / 可追问价值]

| Project | Importance | Core-question quota | Core questions used | Covered? |
|---|---|---|---|---|
| Project A | 高 | 3 | | ⬜ |
| Project B | 中 | 3 | | ⬜ |
| Project C | 低 | 2 | | ⬜ |

- Follow-up questions do **not** consume the quota — any number of follow-ups may sit between two core questions.
- Before ending: any important project with 0 used core questions → switch to it instead of digging the current project further (unless the user explicitly scoped the interview).
- **projects_covered:** [update when a project receives its first core question]

---

## Interview Coverage Tracker

Track which competency categories have been addressed during the interview. Mark as the interview progresses.

| Category | Status | Notes |
|---|---|---|
| A. Motivation & Problem Definition | ⬜ Not covered / 🟡 Partially / 🟢 Covered | |
| B. Personal Ownership & Contribution | ⬜ / 🟡 / 🟢 | |
| C. Method Selection & Alternatives | ⬜ / 🟡 / 🟢 | |
| D. Technical Concepts & Fundamentals | ⬜ / 🟡 / 🟢 | |
| E. Implementation & Engineering | ⬜ / 🟡 / 🟢 | |
| F. Data & Experiment Design | ⬜ / 🟡 / 🟢 | |
| G. Metrics & Results | ⬜ / 🟡 / 🟢 | |
| H. Challenges, Failures & Trade-offs | ⬜ / 🟡 / 🟢 | |
| I. Innovation & Contribution | ⬜ / 🟡 / 🟢 | |
| J. Domain Understanding & Trends | ⬜ / 🟡 / 🟢 | |
| K. Future Work & Counterfactuals | ⬜ / 🟡 / 🟢 | |
| L. AI PM Specific (if applicable) | ⬜ / 🟡 / 🟢 | |

---

## Question Log

Record each question asked and key observations from the answer.

| # | Project | Stage | Question | Category | Depth | Key observations | Follow-up needed? |
|---|---|---|---|---|---|---|---|---|
| 1 | | | | | L1/L2/L3/L4 | | Yes/No |
| 2 | | | | | | | |
| ... | | | | | | | |

---

## Usage Notes

1. Fill in what you can from user materials before starting the interview.
2. Mark speculative information as **"待确认"** — never treat it as fact.
3. Update the coverage tracker and the Project Coverage Plan counters after each core question.
4. Use the risk analysis to prioritize high-value probing areas.
5. With Follow-up OFF, log the recorded-but-unasked probing points in "Key observations" so they reach the final review.
6. This template supports the agent's internal reasoning. Do not output it to the user.
