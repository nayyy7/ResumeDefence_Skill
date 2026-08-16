# Follow-Up Strategies

This file defines the answer analysis logic and next-question decision rules. After each user answer, the agent must analyze the response and decide the next action using these detectors.

---

## Follow-Up Mode Gate

The analysis pipeline runs after every answer in **both** modes:

- **Follow-up OFF**: run the pipeline for **recording only**. The detectors identify errors, contradictions, vague statements, unsupported metrics, and missed opportunities — record each finding together with the probe question you would have asked — then move directly to the next core question. No probing question may be based on the current answer.
- **Follow-up ON**: run the pipeline and act on it — the highest-priority detected signal becomes the next question, subject to the limits in this file.

---

## Answer Analysis Pipeline

After every user answer, run through these checks in order:

```text
1. Did the user actually answer the question?
2. Does the answer contradict the resume or previous answers?
3. Did the user use "we" without clarifying personal contribution?
4. Did the user cite data or metrics without evidence?
5. Did the user mention technical terms without explaining them?
6. Did the user describe what was done but not why?
7. Did the user ignore alternatives, limitations, or failure cases?
8. Is the current topic worth further deepening?
9. Should we switch to an uncovered competency dimension?
```

---

## Detectors

### D1: `non_answer` — Did not answer the question

**Recognition signals:**
- Response is completely off-topic.
- User responds with a question instead of an answer.
- User gives a one-word or evasive response.

**Objective:**
- Re-ask the original question more directly.

**Follow-up approaches:**
- "我可能没有表达清楚。让我换一种方式：..."
- "你刚才的回答没有直接回应我的问题。我想了解的是..."

**What NOT to do:**
- Do not accept the non-answer and move on.
- Do not fill in the answer yourself.
- Do not immediately switch topics.

**When to stop:**
- After 2 re-asks, if still no answer, note it and move on.
- Follow-up OFF mode: do not re-ask at all — record the non-answer and move to the next core question.

---

### D2: `vague_answer` — Abstract, hollow, no examples

**Recognition signals:**
- "主要负责整体推进" / "参与了一些优化工作" / "效果还不错"
- General statements with no concrete actions, numbers, or examples.
- Cannot name a single specific task they did.

**Objective:**
- Force a concrete example, process, or data point.

**Follow-up approaches:**
- "能给我一个具体的例子吗？"
- "你说'效果不错'，具体是指什么指标？提升了多少？"
- "你刚才提到你负责优化——能具体说说你改了哪些地方吗？"

**What NOT to do:**
- Do not accept the vague statement and ask about something else.
- Do not prompt with "did you do X or Y?" (leading).

**When to stop:**
- After 2 follow-ups, if still vague, note this as a major weakness and move on.

---

### D3: `ownership_gap` — "We" without personal responsibility

**Recognition signals:**
- Every sentence uses "we" / "我们".
- Cannot distinguish team work from personal work.
- "我们团队做了..." / "我们决定..." / "我们的方案..."

**Objective:**
- Isolate what the user personally did.

**Follow-up approaches:**
- "你本人具体完成了哪一部分？"
- "刚才你说的这些，哪些是你独立做的，哪些是和团队一起做的？"
- "如果只说你自己的贡献，不包括团队其他人的工作，你会怎么描述？"

**What NOT to do:**
- Do not accept the "we" framing and move on.
- Do not ask "did you personally do X?" (leading — they'll say yes).
- Do not let the entire interview pass without personal ownership being established.

**When to stop:**
- After clear personal contribution is established, or after 3 attempts if the user genuinely cannot separate their work.

---

### D4: `unsupported_metric` — Data or effect without evidence

**Recognition signals:**
- "准确率提升了 30%"
- "用户满意度显著提高"
- "效果比 baseline 好很多"
- Numbers without context: no baseline, no dataset, no metric definition, no sample size.

**Objective:**
- Probe the evidence chain: baseline → metric → dataset → methodology.

**Follow-up approaches:**
- "你说的准确率是怎么定义的？在什么测试集上测的？"
- "这个 30% 的提升是和什么 baseline 比的？"
- "你的测试集有多大？结果在统计上显著吗？"
- "你提到用户满意度提升——你是怎么衡量的？样本量是多少？"

**What NOT to do:**
- Do not accept unsupported numbers at face value.
- Do not fill in plausible baselines or metrics yourself.
- Do not immediately conclude the number is fabricated — probe first.

**When to stop:**
- After 2 rounds of probing, if the evidence chain remains broken, flag for review and move on.

---

### D5: `method_without_reason` — What, not why

**Recognition signals:**
- Lists technologies used but not why they were chosen.
- "我们用了 BERT + CRF" — but no reason given.
- Cannot explain what happens if you swap or remove a component.

**Objective:**
- Elicit reasoning about method selection.

**Follow-up approaches:**
- "你为什么选择 [方法 X]？有没有考虑过其他方案？"
- "如果不用 [方法 X]，换一种方式，你觉得会怎样？"
- "在这个场景下，[方法 X] 相比 [常见替代方案] 的优势是什么？"

**What NOT to do:**
- Do not assume the choice was wrong just because it's unexplained.
- Do not ask about 4 different methods at once.

**When to stop:**
- After the user articulates reasoning, or after 2 attempts if they clearly don't know why.

---

### D6: `concept_surface_only` — Can name, can't explain

**Recognition signals:**
- Names technical terms (RAG, embedding, attention, BERT, cross-entropy...) but cannot explain them.
- When asked "how does X work?", gives a vague analogy or a one-sentence definition.
- Cannot connect the concept to its specific use in the project.

**Objective:**
- Test whether the understanding is deep or superficial.

**Follow-up approaches:**
- "你提到了 [概念 X]，能具体说说它在你的项目里是怎么工作的吗？"
- "[概念 X] 在你的场景下有什么局限性？"
- "如果不用 [概念 X]，你觉得还有什么方式可以达到类似效果？"

**What NOT to do:**
- Do not immediately explain the concept (that's for review phase).
- Do not mock or express disbelief.
- Do not ask "have you even read the paper?" — keep it professional.

**When to stop:**
- After 2 probes, if the understanding stays at surface level, flag as a key weakness for review.

---

### D7: `contradiction` — Conflict with resume, materials, or earlier answers

**Recognition signals:**
- Answer contradicts what the resume says.
- Answer contradicts a previous answer from this interview.
- Claimed metric conflicts with what's written in the project report.

**Objective:**
- Clarify the inconsistency without accusation.

**Follow-up approaches:**
- "你刚才说 [X]，但你的简历上写的是 [Y]。能帮我澄清一下吗？"
- "之前你提到 [A]，现在你说 [B]。这两个说法好像不太一致，你怎么看？"

**What NOT to do:**
- Do not accuse the user of lying.
- Do not treat every inconsistency as intentional deception.
- Do not make the user feel like they're on trial.

**When to stop:**
- After the inconsistency is clarified or acknowledged. Record for review either way.

---

### D8: `missing_tradeoff` — No alternatives or trade-offs considered

**Recognition signals:**
- Presents the chosen approach as the only possible approach.
- Cannot name any alternative that was considered.
- "This was the best way" without comparison.

**Objective:**
- Test awareness of design space.

**Follow-up approaches:**
- "你在做这个决定的时候，有没有考虑过其他方案？"
- "如果有一个同事提出完全不同的方案，你觉得可能是什么？"
- "在你放弃的方案里，哪一个最接近最终选择？"

**What NOT to do:**
- Do not suggest alternatives yourself (that's for review phase).
- Do not conclude the choice was wrong — just probe the reasoning.

**When to stop:**
- After 2 probes, or once the user demonstrates awareness of trade-offs.

---

### D9: `missing_limitations` — Only positives, no failures

**Recognition signals:**
- Describes the project as entirely successful.
- Cannot name a single failure case, edge case, or limitation.
- "It worked great for everything."

**Objective:**
- Elicit honest acknowledgment of limitations.

**Follow-up approaches:**
- "在什么情况下你的方案会失败或不适用？"
- "你提到 [某个模块]，它在所有 case 上都表现一致吗？"
- "回顾这个项目，有什么是你想做但没做到的？"

**What NOT to do:**
- Do not frame this as "gotcha — your project has flaws."
- Do not push for limitations the project obviously wouldn't have.

**When to stop:**
- After 2 probes, or when the user acknowledges specific limitations.

---

### D10: `strong_answer` — Complete, accurate, evidence-backed, reflective

**Recognition signals:**
- Answer includes: background, specific personal actions, reasoning, alternatives considered, evidence/metrics, and limitations.
- User can handle follow-ups smoothly.
- User distinguishes their work from team work confidently.

**Objective:**
- Increase difficulty. Push to the next depth level or switch to an uncovered dimension.

**Follow-up approaches:**
- Raise the depth level (L2→L3 or L3→L4).
- Ask a counterfactual: "如果 [关键条件] 变了，你的方案还成立吗？"
- Ask about parameter sensitivity: "[某个参数] 的变化对你的结果影响大吗？"
- Switch to a completely uncovered competency category.

**What NOT to do:**
- Do not repeat similar questions at the same difficulty.
- Do not immediately switch to an easy question from another category.
- Do not end the interview just because one answer was strong.

**When to stop:**
- When the topic has reached L4 depth, or all major competencies are covered.

---

## Decision Pseudocode

```text
function decide_next_action(user_answer, interview_state):
    analysis = analyze_answer(user_answer, interview_state.resume)
    record_for_review(analysis)  # always record; in OFF mode this is the only use of the analysis

    if interview_state.follow_up_mode == OFF:
        return next_core_question_from_coverage_plan()

    if analysis.contradiction:
        return ask_for_clarification(analysis.contradiction_detail)
    elif analysis.ownership_gap and interview_state.ownership_probes < 3:
        return ask_personal_contribution()
    elif analysis.unsupported_metric:
        return ask_baseline_metric_dataset()
    elif analysis.concept_error_or_surface_only:
        return probe_mechanism_and_application()
    elif analysis.vague_answer and interview_state.vagueness_probes < 2:
        return ask_for_concrete_example()
    elif analysis.method_without_reason:
        return ask_why_and_alternatives()
    elif analysis.missing_limitations:
        return ask_failure_case()
    elif analysis.missing_tradeoff:
        return ask_alternative_comparison()
    elif analysis.strong_answer and interview_state.current_depth < max_depth:
        return ask_counterfactual_or_increase_depth()
    elif interview_state.follow_ups_on_topic >= 3:
        return move_to_highest_priority_uncovered_category()
    else:
        return deepen_current_topic_or_switch()
```

---

## Follow-Up Limits

| Rule | Limit |
|---|---|
| Same knowledge point | Default ≤ 2–3 consecutive follow-up layers (2 if answers add little substance, 3 if they keep adding substance) |
| Exception to above | Clear contradiction — may probe beyond 3 |
| Vague answer probe | ≤ 2 attempts before noting weakness and moving on |
| Ownership probe | ≤ 3 attempts |
| User says "不知道" | Stop immediately, note, switch topic |
| User wants to skip | Respect immediately |

---

## Depth Escalation Rules

| Current depth | User performance | Next action |
|---|---|---|
| L1 (fact recall) | Weak | Stay at L1, different angle |
| L1 (fact recall) | Adequate | Move to L2 (reason explanation) |
| L2 (reason explanation) | Weak | Probe L2 more or drop to L1 |
| L2 (reason explanation) | Strong | Move to L3 (principles & tradeoffs) |
| L3 (principles & tradeoffs) | Weak | Stay at L3, different angle |
| L3 (principles & tradeoffs) | Strong | Move to L4 (boundaries & counterfactuals) |
| L4 (boundaries) | Strong | Switch to uncovered category |
| L4 (boundaries) | Weak | Stay at L4 or move to new category |

In Follow-up OFF mode, depth escalation happens **between core questions** — the next planned question targets a deeper stage of the coverage plan — not within a topic.

---

## Topic Switching Rules

When switching topics, prefer:

1. The highest-priority **uncovered** competency category for the interview type.
2. Adjacent categories (e.g., method → data → metrics) over distant jumps.
3. Categories the user's materials suggest will be weak points.
4. Categories the user explicitly or implicitly wants to skip last.

Do not announce the category switch — just ask the next question naturally.
