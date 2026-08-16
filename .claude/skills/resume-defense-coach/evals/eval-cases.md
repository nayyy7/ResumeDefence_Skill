# Evaluation Cases

This file contains evaluation cases for testing the resume-defense-coach Skill. Each case specifies the input, expected trigger behavior, expected actions, prohibited actions, and acceptance criteria.

---

## Positive Trigger Cases (Should Activate Full Workflow)

### Case 1: Standard Graduate Re-examination Request

**Input:**
> 这是我简历上的项目经历：[粘贴 CampusRAG 项目描述]。请帮我进行一轮考研复试模拟面试，难度中级。

**Should trigger Skill?** Yes

**Expected behavior:**
- Activate resume-defense-coach workflow.
- Extract project facts from the provided material.
- Default settings: intermediate difficulty, Chinese, 8 main questions.
- Start with the first interview question.
- Do NOT ask for interview type or difficulty again (user already provided).

**Prohibited:**
- ❌ Output a static list of questions.
- ❌ Ask "what difficulty do you want?" again.
- ❌ Give answers or scores during interview.

**Acceptance points:**
- [ ] First response is an interview question, not a feature list.
- [ ] Question is grounded in the provided project material.
- [ ] Only one question is asked.

---

### Case 2: "Ask me questions like an interviewer"

**Input:**
> 我有一段实习经历想练习面试：在一家AI公司做推荐系统优化。你像面试官一样连续追问我就行，不要一口气给我一堆问题。

**Should trigger Skill?** Yes

**Expected behavior:**
- Activate the workflow.
- Extract facts from the brief internship description.
- Ask clarifying questions if material is too thin, then begin.
- One question at a time.
- Dynamic follow-up based on answers, not a fixed list.

**Prohibited:**
- ❌ Ask "please provide your resume first" if the user already described the project.
- ❌ List multiple questions at once.

**Acceptance points:**
- [ ] Questions adapt based on user's answers.
- [ ] Never outputs more than one question per turn.

---

### Case 3: AI Product Internship Interview

**Input:**
> 我在一个 AI 产品团队实习，负责了一个智能客服项目的产品设计。请模拟一轮 AI 产品实习面试，侧重产品思维。

**Should trigger Skill?** Yes

**Expected behavior:**
- Activate workflow with interview type = AI产品实习.
- Adjust question weighting per the taxonomy (Category L: AI PM specific → High).
- Focus on product decisions, user needs, model capability boundaries, evaluation strategy.

**Prohibited:**
- ❌ Only ask algorithm implementation questions.
- ❌ Ignore the "product" emphasis.

**Acceptance points:**
- [ ] At least some questions address product thinking (why LLM, evaluation, user needs).
- [ ] Questions are appropriate for product rather than engineering role.

---

### Case 4: "Simulate first, review everything at the end"

**Input:**
> 我给你我的项目经历[粘贴内容]。你先面试我，过程里不要点评，最后再一起复盘，就像真实面试一样。

**Should trigger Skill?** Yes

**Expected behavior:**
- Strict phase separation.
- No scoring, no corrections, no hints during the interview.
- Clear transition announcement when moving to review.
- Complete review with per-question analysis, scores, and study plan.

**Prohibited:**
- ❌ "This answer would score about 3 out of 5" during interview.
- ❌ "You should have mentioned..." during interview.
- ❌ Skipping the review phase.

**Acceptance points:**
- [ ] Zero feedback during interview phase.
- [ ] Review phase is structured and comprehensive.
- [ ] Transition from interviewer to coach is explicit.

---

### Case 5: High-Difficulty Pressure Interview, Single Project

**Input:**
> 我只想练这一个项目[粘贴项目]，高难度压力面，追问可以狠一点。8 道题。

**Should trigger Skill?** Yes

**Expected behavior:**
- Difficulty = advanced/pressure.
- Depth levels mainly L3–L4.
- Higher follow-up density.
- All questions focused on the single specified project.
- Professional tone maintained despite pressure.

**Prohibited:**
- ❌ Drifting to other projects.
- ❌ Using L1–L2 questions primarily.
- ❌ Being rude or personally attacking.

**Acceptance points:**
- [ ] Questions reach L3–L4 depth.
- [ ] Stays focused on the specified project.
- [ ] Tone is challenging but professional.

---

## Negative Cases (Should NOT Trigger Full Workflow)

### Case 6: Standalone Concept Question

**Input:**
> 什么是 cross-entropy loss？能给我讲讲吗？

**Should trigger Skill?** No

**Expected behavior:**
- Answer the question directly without activating the interview workflow.
- Do not start a simulation or ask for a resume.

**Prohibited:**
- ❌ "Let me simulate an interview about loss functions."
- ❌ "Please provide your resume first."
- ❌ Entering any interview phase.

**Acceptance points:**
- [ ] Skill is not activated.
- [ ] Direct answer is provided.

---

### Case 7: Resume Bullet Rewriting Request

**Input:**
> 帮我润色一下这条简历描述："负责深度学习模型训练和调优，提升了模型效果"

**Should trigger Skill?** No

**Expected behavior:**
- Help rewrite the bullet without activating the interview workflow.
- May ask clarifying questions about the actual work, but not as an interview.

**Prohibited:**
- ❌ Starting a mock interview.
- ❌ "Let me interview you about this bullet point first."

**Acceptance points:**
- [ ] Skill is not activated.
- [ ] Rewriting assistance is provided.

---

### Case 8: Static Question List Request

**Input:**
> 给我 20 道考研复试算法面试常见题。

**Should trigger Skill?** No

**Expected behavior:**
- Recognize this is a request for a static list, not an adaptive interview.
- Either provide a general list or explain that the Skill does adaptive interviews and offer to do one instead.

**Prohibited:**
- ❌ Pretending to do an adaptive interview while outputting a fixed list.
- ❌ Silently providing the list without clarifying the Skill's actual capability.

**Acceptance points:**
- [ ] Acknowledges the Skill is not a static question bank.
- [ ] Offers the adaptive interview alternative or provides a reasonable list.

---

### Case 9: Non-Interview Career Question

**Input:**
> 考研复试穿什么衣服比较合适？

**Should trigger Skill?** No

**Expected behavior:**
- Answer the question directly or state it's outside the Skill's scope.
- Do not activate the interview workflow.

**Prohibited:**
- ❌ "Let's do a mock interview to prepare you for the real thing."
- ❌ Treating this as a trigger for the Skill.

**Acceptance points:**
- [ ] Skill is not activated.
- [ ] Question is answered or politely declined.

---

## Boundary Cases (Edge Condition Testing)

### Case 10: No Project Material Provided

**Input:**
> 我想练习考研复试面试。

**Should trigger Skill?** Yes (attempted), but cannot proceed

**Expected behavior:**
- Recognize that resume/project material is missing.
- Ask the user to provide project information before starting.
- Do NOT fabricate a project or use sample data as if it's the user's.

**Prohibited:**
- ❌ Starting the interview without any project material.
- ❌ Using the sample resume in place of the user's material.
- ❌ Making up a fake project.

**Acceptance points:**
- [ ] Politely asks for project material.
- [ ] Explains what kind of information is needed.
- [ ] Does not proceed without material.

---

### Case 11: User's Metric Contradicts Resume

**Input (setup):** Resume says "准确率 85%". During interview, user says "准确率大概 92% 左右".

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- Detect the contradiction.
- Ask for clarification: "你的简历上写的是 85%，刚才你说是 92%。这两个数字的差异是怎么来的？"
- Record the discrepancy for the review.

**Prohibited:**
- ❌ Ignoring the contradiction.
- ❌ Accusing the user of lying.
- ❌ Choosing one number arbitrarily.

**Acceptance points:**
- [ ] Contradiction is detected.
- [ ] Clarification is requested professionally.
- [ ] Discrepancy is noted in the final review.

---

### Case 12: User Answers "I don't know" Consecutively

**Input (setup):** Three consecutive answers are variations of "不知道" / "不太清楚" / "没想过".

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- First "不知道": note the weakness, briefly confirm, switch topic.
- Second consecutive "不知道" on a new topic: note again, consider if difficulty is too high.
- Third: acknowledge the pattern and ask if the user wants to adjust difficulty or end early.

**Prohibited:**
- ❌ Repeatedly pressing on the same topic after user says "不知道".
- ❌ Mocking or expressing frustration.
- ❌ Continuing as if nothing happened.

**Acceptance points:**
- [ ] Does not press the same topic after "不知道".
- [ ] Records weaknesses for review.
- [ ] Offers to adjust difficulty after pattern emerges.

---

### Case 13: User Requests Difficulty Increase Mid-Interview

**Input (setup):** Interview at intermediate difficulty. User says "提高难度".

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- Acknowledge the request.
- Immediately adjust subsequent questions to higher depth levels (L3–L4).
- Note the change in the final report.

**Prohibited:**
- ❌ Ignoring the request.
- ❌ "We'll increase difficulty after this topic."
- ❌ Restarting the interview.

**Acceptance points:**
- [ ] Next question is demonstrably harder.
- [ ] Change is noted in the report.

---

### Case 14: User Asks for a Hint Mid-Interview

**Input (setup):** In the middle of an interview, user says "给我一点提示吧，我不知道从哪里回答".

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- Ask: "你想退出真实模拟模式吗？如果给我提示，我会在报告中标注这一题是在提示后完成的。"
- If user insists: provide a limited hint, flag in report.
- If user decides to continue without hint: continue normally.

**Prohibited:**
- ❌ Silently providing the answer.
- ❌ Refusing to give any hint under any circumstance.
- ❌ Not flagging the hint in the final report.

**Acceptance points:**
- [ ] User is asked whether to exit simulation mode.
- [ ] If hint is given, it's limited and flagged in report.
- [ ] User's choice is respected.

---

### Case 15: User Requests Immediate End and Review

**Input (setup):** 3 questions into an 8-question interview. User says "结束模拟，直接复盘吧，不想继续了。"

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- Stop asking questions immediately.
- Do not ask "are you sure?" more than once (a brief confirmation is acceptable).
- Transition to review with whatever answers have been collected.
- Mark uncovered competencies as "未充分评估".

**Prohibited:**
- ❌ "Let's do one more question first."
- ❌ Continuing the interview.
- ❌ Scoring uncovered dimensions.

**Acceptance points:**
- [ ] Interview stops immediately.
- [ ] Review covers only the questions that were asked.
- [ ] Uncovered dimensions are marked "未充分评估" not given forced scores.

---

### Case 16: User Has Three Projects, Wants to Focus on the Second

**Input:**
> 我有三个项目经历：[项目A]、[项目B]、[项目C]。重点面试第二个项目就行，其他的可以简单问问。

**Should trigger Skill?** Yes

**Expected behavior:**
- Prioritize project B for deep coverage.
- Spend the majority of questions on project B.
- Possibly ask 1–2 questions from projects A and C for breadth.
- Note the focus preference in the report.

**Prohibited:**
- ❌ Asking all questions about project A.
- ❌ Ignoring the user's preference.
- ❌ Equal distribution across all three projects.

**Acceptance points:**
- [ ] Majority of questions are on project B.
- [ ] User's preference is respected.
- [ ] Other projects get minimal but present coverage.

---

### Case 17: English Resume, Chinese Interview

**Input:**
> [English resume content]. Please interview me in Chinese.

**Should trigger Skill?** Yes

**Expected behavior:**
- Understand English technical terms from the resume.
- Conduct the interview in Chinese.
- Use English terms for technical concepts when appropriate (e.g., "你的 RAG pipeline 中...").

**Prohibited:**
- ❌ Conducting the interview in English.
- ❌ Confusing English resume with English interview preference.

**Acceptance points:**
- [ ] Interview is in Chinese.
- [ ] English technical terms are properly mixed in.
- [ ] All project facts are correctly understood from the English resume.

---

### Case 18: Material Has No Quantitative Results

**Input:**
> 我做过一个课程项目：用协同过滤做图书推荐。就是一个 Demo，没有上线，也没有评测数据。

**Should trigger Skill?** Yes

**Expected behavior:**
- Recognize the project has no quantitative results.
- Do NOT press for metrics that don't exist.
- Focus on: design decisions, implementation, concepts, what they learned, what they'd do differently.
- In the review, note the lack of evaluation as a project limitation, not a personal failure.

**Prohibited:**
- ❌ Repeatedly asking "so what was your accuracy?"
- ❌ Fabricating a baseline to compare against.
- ❌ Penalizing the user for not having data from a demo project.

**Acceptance points:**
- [ ] Does not fabricate or demand non-existent metrics.
- [ ] Focuses on appropriate dimensions (design, concepts, learning).
- [ ] Review notes the demo nature of the project.
- [ ] Review suggests how to add evaluation if relevant.

---

## V1.1 Feature Cases (Four Optimizations)

### Case 19: Single Turn Never Contains More Than 2 Sub-Questions

**Input (setup):** A resume with a technically rich project (RAG system, multiple modules). Interview is in progress.

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- Every turn contains exactly **1 core question**.
- A core question may include at most **2 highly-related sub-questions** (e.g. "为什么选择 RAG 而不是全量放入上下文？相比微调的主要代价是什么？").
- Anything else worth asking is held back until after the user answers.
- Questions are phrased for oral answers, not questionnaire-style lists.

**Prohibited:**
- ❌ "我有几个问题：第一…第二…第三…" (3+ questions in one turn).
- ❌ Listing unrelated questions even if each is short.

**Acceptance points:**
- [ ] No turn contains 3 or more questions.
- [ ] Sub-questions, when present, are tightly related to the same core question.
- [ ] After a weak answer, probing is delivered as follow-up questions one at a time, not as a batch.

---

### Case 20: Interview Progresses from High-Level to Technical Detail

**Input:** A resume with a technically deep project (e.g. fine-tuning + RAG + evaluation).

**Should trigger Skill?** Yes

**Expected behavior:**
- Opening questions target `PROJECT_OVERVIEW` / `PERSONAL_CONTRIBUTION`: background, goal, high-level approach, personal role.
- Later questions move through `METHOD_REASONING` / `IMPLEMENTATION` into `TECHNICAL_DEPTH` / `CHALLENGE` (principles, parameters, failure cases, counterfactuals).
- Transitions are not mechanical: a natural follow-up may jump depth, and a weak answer may keep the interview shallow for a while.
- Switching projects resets the arc for the new project.

**Prohibited:**
- ❌ Opening with fine technical parameters or low-level principles ("你的 chunk size 是多少？attention 的公式是什么？").
- ❌ Rigid stage-by-stage progression that ignores the user's answers.

**Acceptance points:**
- [ ] First 1–2 core questions are high-level (overview / contribution).
- [ ] Later core questions demonstrably deepen (methods → implementation → principles/challenges).
- [ ] Follow-up probes can deepen the current topic regardless of the planned stage.

---

### Case 21: Three-Project Resume Is Not Reduced to One Project

**Input:**
> 我有三个项目：[项目A：简历重点、技术深度高]、[项目B：中等篇幅]、[项目C：较小但与你目标方向相关]。请模拟一轮 8 道核心问题的面试。

**Should trigger Skill?** Yes

**Expected behavior:**
- Detect all three major projects (`projects_detected`).
- Allocate the 8 core questions across projects by importance, resume space, target direction, and follow-up value — e.g. A: 3, B: 3, C: 2. Not necessarily equal.
- Track `projects_covered` and core questions used per project.
- Before ending, check the plan: if an important project has zero core questions, switch to it instead of digging the current project further.
- Follow-up questions between core questions do not consume the quota.

**Prohibited:**
- ❌ All 8 core questions on project A without a stated reason (e.g. the user explicitly said "只问项目A").
- ❌ Silently skipping project C while continuing to deep-dive project A near the end.

**Acceptance points:**
- [ ] All three projects receive at least one core question.
- [ ] Distribution reflects importance (deepest coverage on the most important project).
- [ ] The report states which projects were covered and at what depth.

---

### Case 22: Follow-Up OFF — No Probing Based on the Answer

**Input (setup):** User chose 关闭追问 before the interview. During the interview the user says "效果提升了 30%，用户都说好" (unsupported metric) and later contradicts the resume.

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- After each answer: internal analysis only — no probing question based on the current answer.
- Move directly to the next planned core question (coverage plan + stage progression).
- Errors, vague statements, unsupported metrics, and contradictions are recorded.
- The final review surfaces all recorded issues, including the probe questions that were withheld (e.g. "这个 30% 是和什么 baseline 比的？").

**Prohibited:**
- ❌ "你刚才说的 30% 是怎么算出来的？" during the interview.
- ❌ Any question that references the current answer's content as a probe (the next core question may be on a new topic).
- ❌ Dropping the recorded issues from the final review.

**Acceptance points:**
- [ ] No answer-based probing questions during the interview.
- [ ] Next core questions follow the plan, not the answer's weaknesses.
- [ ] Final review explicitly lists recorded-but-unasked issues (see review template section 九).

---

### Case 23: Follow-Up ON — Dynamic Probing Still Works

**Input (setup):** User chose 开启追问 (or mode defaulted to ON). Interview in progress.

**Should trigger Skill?** Yes (already in workflow)

**Expected behavior:**
- Vague answer ("主要负责核心模块") → probe for a concrete example or specific work.
- Strong answer → escalate depth (reasoning → principles → counterfactual) or switch to an uncovered dimension.
- Same knowledge point: default at most 2–3 consecutive follow-up layers before switching.
- Contradiction with the resume → clarification probe (exception to the 2–3 layer limit).
- "不知道" → record and move on.

**Prohibited:**
- ❌ Moving to a new core question immediately after a weak/vague answer without probing.
- ❌ Endless same-point grilling beyond the 2–3 layer default without a contradiction.
- ❌ Revealing the answer while probing.

**Acceptance points:**
- [ ] Weak answers trigger probes (example, baseline, personal contribution).
- [ ] Strong answers trigger depth escalation.
- [ ] Same-point probing stops within 2–3 layers by default; contradiction is the exception.

---

## Evaluation Methodology

### How to Use These Cases

1. **Automated testing**: These cases can serve as prompts for evaluating the Skill with a language model. Compare the model's output against the expected behavior.
2. **Manual testing**: A human tester can play the role of the user and verify the Skill's behavior against the acceptance points.
3. **Regression testing**: After any change to SKILL.md or supporting files, run through the positive and boundary cases to ensure no behavioral regression.

### Scoring an Evaluation Run

For each case, rate as:

- **PASS**: All acceptance points are met. No prohibited actions occurred.
- **PARTIAL**: Most acceptance points are met, but behavior was not fully correct or one minor prohibited action occurred.
- **FAIL**: Key acceptance points not met, or a major prohibited action occurred.

### Minimum Bar for MVP Release

- 5/5 positive trigger cases must PASS.
- 4/4 negative cases must PASS (skill not incorrectly triggered).
- At least 7/9 boundary cases must PASS.

### Minimum Bar for V1.1

- 5/5 V1.1 feature cases (Cases 19–23) must PASS.
- No regression in the MVP cases above.
