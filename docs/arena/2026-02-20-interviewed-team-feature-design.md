# Expert Arena: How to Design /interviewed-team-feature Skill

> **Status:** Consensus reached
> **Date:** 2026-02-20
> **Experts:** Steve Portigal, Marty Cagan, Teresa Torres, Steve Krug, Rich Hickey

---

## Verdict

**2-4 adaptive questions, zero technical questions, dynamic branching based on input clarity.**

The 15-question scripted interview is accidental complexity. Half the questions gather information the autonomous agents already determine themselves (tech stack, risks, affected areas, tests, deadlines). The skill should ask ONLY what the AI genuinely cannot infer from the codebase.

---

## Key Debate Moments

**Opening positions:**
- Portigal: "15 questions is a survey, not an interview. 3-5 adaptive questions following a stage map."
- Cagan: "3 mandatory questions + 1-2 adaptive. Focus on value risk, not tech specs."
- Torres: "Branching paths: clear requests go fast, vague ones get hypothesis proposals."
- Krug: "3-4 max. 15 questions is a UX crime. Buttons everywhere."
- Hickey (Devil's Advocate): "15 questions for 1 string argument is a ceremony, not an interview. Maybe the skill shouldn't exist at all."

**Critical challenge — Hickey vs everyone:**
Hickey argued team-feature should ask questions when stuck, not pre-interview. Torres countered: "team-feature's philosophy is Full Autonomy — it NEVER asks the user. Wrong intent at launch = expensive full-team failure." Hickey conceded this point — the asymmetric cost justifies pre-run questions.

**Convergence moment — Hickey shifts:**
Hickey moved from "zero questions" to "3 essential questions" after accepting that autonomous agents can't pause mid-execution. His argument compressed the group's 4 questions to 3 by showing Q1 (situational framing) makes Q3 (success criteria) often redundant.

**Torres's key contribution — Branch B:**
When the user's request is vague, instead of asking more questions, the AI proposes 2-3 hypotheses as questions: "Do you mean A or B?" This reduces cognitive load and speeds up the interview.

**Krug's lasting influence:**
"Every question is friction." This principle pushed the group from 4-5 questions down to 2-4 adaptive. His insistence on buttons everywhere was unanimously adopted.

---

## Final Consensus: Interview Structure

### Q1 (mandatory, skip if already answered in user's initial message):
**"What will change when this works — and for whom?"**

- Situational framing forces concrete over abstract
- "Reporting system" becomes "clients can export last month's invoices as PDF"
- Contains audience implicitly ("for whom")
- If answer is vague: AI proposes 2-3 hypotheses as button options (Torres's Branch B)
- Adapts to input type: story-frame for pain-driven requests, outcome-frame for improvements (Cagan)

### Q2 (adaptive, only if Q1 didn't reveal):
**Deepening question based on Q1 answer**

- If audience unclear: "Who will use this most?" (buttons: end users / admins / team / other)
- If scope unclear: "Is this a new feature or changing something existing?" (buttons)
- If both clear from Q1: SKIP entirely

### Q3 (conditional, only if Q1 wasn't specific enough):
**"How will you know it's working?"**

- Success criteria — the one thing agents cannot derive from codebase
- If Q1 was specific ("clients can export invoices as PDF") — success criteria are implicit, SKIP
- If Q1 was abstract ("improve the dashboard") — this question is essential

### Q4 (optional):
**"Anything that must NOT be included?"**

- Scope boundary — prevents agents from building maximum possible
- User can skip with "Nothing specific" button
- Critical when the feature touches sensitive areas

### Design principles (unanimous):
- Each question answerable in 1-2 sentences
- Nothing the AI can infer from codebase belongs in the interview
- Buttons + "Other" everywhere to reduce cognitive load
- Skip questions already answered in user's initial message
- No question can be removed without losing genuinely non-inferable information

---

## Arguments FOR the chosen design

| # | Argument | Who | Why convincing |
|---|---------|-----|----------------|
| 1 | Autonomous agents can't pause to ask — wrong intent = full rebuild | Torres, Portigal | Asymmetric cost: 2 min interview saves 10+ min rework |
| 2 | Technical questions are agents' job, not user's | All 5 | team-feature already runs codebase-researcher, reference-researcher, risk-testers |
| 3 | Situational framing extracts more signal than direct questions | Hickey, Portigal | "What will change?" > "Describe the feature" — forces concrete thinking |
| 4 | Hypotheses-as-questions for vague input | Torres | Reduces cognitive load, faster than asking more open questions |
| 5 | Buttons reduce friction for non-technical users | Krug | "Don't Make Me Think" — predefined options > typing |

## Arguments AGAINST (accepted as tolerable risks)

| # | Argument | Who | Why tolerable |
|---|---------|-----|--------------|
| 1 | Any pre-interview is overhead — just iterate | Hickey | True for simple requests, but agents can't iterate with user mid-execution |
| 2 | 2-3 questions may miss edge cases | Portigal | Agents do risk analysis themselves; interview catches intent, not edge cases |
| 3 | Success criteria sometimes implicit | Hickey | That's why Q3 is conditional — skip when obvious |

## Remaining disagreements

- **Hickey** still believes one well-framed question could suffice in most cases. The group accepted this as valid for simple requests (skill should skip when enough info is given) but not as the default.
- **Krug** wanted Q3 (success criteria) to be optional always. Cagan and Torres insisted it's mandatory when Q1 is abstract — accepted as conditional compromise.

---

## Recommendation

Build the skill with **2-4 adaptive questions** that:
1. Start with a situational Q1 that combines "what" and "for whom"
2. Use AI to analyze the answer and decide which follow-ups are needed
3. Propose hypotheses (not more questions) when input is vague
4. Skip anything the codebase-researcher can determine
5. Compile answers into a brief and pass to /team-feature

The skill should feel like a 2-minute conversation, not a 15-minute form.

## Action Plan

1. Rewrite SKILL.md with 2-4 adaptive questions (replace current 15-question structure)
2. Move expert principles to references/interview-principles.md
3. Add branching logic: clear input → fast path (2 questions), vague input → hypothesis path (3-4 questions)
4. Remove all technical questions — agents handle those
5. Add brief compilation and handoff to /team-feature
