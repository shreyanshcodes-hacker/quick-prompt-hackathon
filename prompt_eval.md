# Prompt Evaluation Report

## Overall Score

| Criterion | Score | Max | Notes |
|---|---:|---:|---|
| Prompt Clarity | 74 | 100 | Clear scenario and deliverables, but lacks a hard output schema and explicit failure rules. |
| Output Quality & Schema Guidance | 76 | 100 | Strong task framing and deliverables, but missing strict formatting and edge-case instructions. |
| Efficiency & Token Economy | 38 | 50 | Mostly concise and readable, though some wording is longer than needed and could be more operational. |
| Total | 188 | 250 | Solid business-planning prompt with room for more deterministic structure. |

## Executive Summary

This prompt is strong as a challenge brief: it defines a realistic scenario, gives a clear budget constraint, and asks for practical business reasoning. The structure is easy to follow and the deliverables are meaningful. It is likely to produce a useful business plan when used as a human or AI task.

The main weaknesses are not in the core idea, but in execution detail. The prompt does not give a strict output schema, does not tell the model how to resolve missing or contradictory assumptions, and leaves some ambiguity around daily demand modeling and numeric assumptions. It also repeats a bit of guidance without giving strong negative constraints or an explicit decision policy.

## Evaluated Prompt Analysis

### Prompt source
The prompt evaluated is the challenge brief in [pr.md](pr.md).

### Estimated token count
Approximately 500–700 tokens depending on tokenizer and formatting.

### Structural overview
The prompt has a clear narrative flow:
- Scenario framing
- Task objective
- Required deliverables
- Constraints
- Evaluation criteria
- Optional bonus challenge

This is good for readability, but it could be made more deterministic by adding:
- strict output fields
- explicit assumption rules
- refusal/fallback instructions
- a required calculation template

## Detailed Parameter Breakdown

### 1) Prompt Clarity (74 / 100)

#### Strengths
- The scenario is concrete and motivating: “You've been given ₹10,000 to improve your college canteen for one week.”
- The task is well-scoped into five practical decision areas: menu, pricing, quantities, demand management, and budget.
- Constraints are clearly listed, including the spending cap and daily serving assumption.
- The deliverables are broken into numbered sections, which helps the responder structure their output.

#### Weaknesses
- The prompt does not define a clear role for the responder. It does not say whether the actor is a “canteen manager,” “student consultant,” or “operations planner.”
- Some phrases are vague: “you may adjust and justify a different number” and “rough calculation.” These allow wide variation without a fixed standard.
- The prompt tells the respondent what to include, but not exactly how to prioritize the outputs when assumptions conflict.
- There are few explicit negative constraints such as “do not ignore food cost,” “do not assume unlimited inventory,” or “do not propose unrealistic prices.”

#### Score rationale
This criterion is strong on scenario clarity and structure, but weaker on precision and operational guardrails. It is not ambiguous enough to fail, but it leaves open too many model choices for consistent high-quality outputs.

### 2) Output Quality & Schema Guidance (76 / 100)

#### Strengths
- The deliverables list is well-aligned with a realistic business plan: budget breakdown, menu pricing, demand strategy, profit estimate, assumptions.
- The evaluation criteria provide a useful benchmark for judging quality: “Budget Discipline,” “Menu Sense,” “Demand Handling,” and “Math & Reasoning.”
- The prompt encourages a practical, realistic plan rather than a generic brainstorm.

#### Weaknesses
- There is no mandated output format beyond “Present your plan with” and a few headings. This means the responder may produce inconsistent tables, missing data, or unstructured narratives.
- The prompt does not specify whether numbers should be rounded to nearest rupee, whether weekly profit is estimated gross or net, or whether supply inventory should be explicit per day.
- There is no section on how to handle ambiguity, such as missing data or contradictory conditions like low demand with high waste risk.
- It does not define an example response or schema, so the model may under-specify the calculations or overstate assumptions.

#### Score rationale
This prompt does a good job describing what the plan should cover, but it does not strongly enforce a standardized output structure or operational edge-case handling.

### 3) Efficiency & Token Economy (38 / 50)

#### Strengths
- The prompt is concise overall and avoids unnecessary story-building.
- Each major section has a purpose and is relevant to the problem.
- The structure is efficient enough for a straightforward planning task.

#### Weaknesses
- Some repeated ideas appear in the problem definition and the evaluation criteria without adding much new instruction.
- The prompt includes multiple framing sentences that could be condensed into a more operational specification.
- A more compact design could combine the action items, constraints, and output schema into a single, high-signal instruction set.
- The optional bonus challenge is useful, but it adds length without moving the core objective forward.

#### Score rationale
The prompt is not bloated, but it could be tightened significantly while preserving clarity and richness.

## Actionable Recommendations

1. Add a clear role and objective block.
   - Example: “You are a student operations consultant tasked with designing a 7-day canteen plan under a ₹10,000 cap.”

2. Define a strict response schema.
   - Require explicit sections for budget, menu table, demand plan, profit estimate, and assumptions.
   - Specify columns and units for each table.

3. Add assumption rules.
   - State that all cost estimates must include ingredient cost, not just selling price.
   - Require a single base daily student count and a justification for any variation by weekday/weekend.

4. Add edge-case handling instructions.
   - If an item sells out, explain how the plan responds.
   - If demand is higher than expected, specify how to reorder or substitute.
   - If leftovers remain, state how they are reduced or repurposed.

5. Add a required calculation discipline.
   - Ask for a weekly total cost, total revenue, and net profit with formulas or at least a micro-calculation summary.

6. Remove unnecessary repetition.
   - Compress the scenario and evaluation criteria into a cleaner one-pass brief.

7. Include a short example of the desired table structure.
   - This will improve consistency and reduce formatting drift.

## Optimized Prompt Rewrite (Production-Ready)

```text
You are a student operations consultant helping redesign a college canteen for 7 days under a strict ₹10,000 budget.

<objective>
Create a realistic, financially disciplined canteen plan that keeps students satisfied, prevents waste, handles peak demand, and stays within budget without running out of popular items.
</objective>

<context>
- Budget: ₹10,000 total for the full week
- Operating days: 7 days
- Estimated student traffic: 150–300 students per day; you may use a different daily estimate only if you justify it clearly
- Food cost must be included in every pricing decision; selling price alone is not enough
- The plan should reflect realistic student preferences, demand spikes, and simple operational constraints
</context>

<task>
Design the following:
1. Menu: what foods and drinks will be sold
2. Pricing: selling price for each item
3. Quantities: how much of each item will be stocked or prepared each day, including changes across weekdays vs. weekends and rush periods
4. Demand management: how you will handle peak-hour queues, stockouts, leftovers, and student affordability concerns
5. Financial plan: weekly spend, projected revenue, and expected profit/loss
</task>

<constraints>
- Total weekly spend must not exceed ₹10,000
- The plan must cover all 7 days of operation
- Assume realistic ingredient costs and practical portion sizes
- Do not propose menu items that are unrealistic for a college canteen budget or operational capacity
- Do not ignore food waste or stockouts; address them explicitly
</constraints>

<required_output>
Return your answer in this exact structure:

1. Budget Breakdown
- Provide a table with columns: Category | Item/Use | Quantity | Unit Cost | Total Cost
- Total must equal ₹10,000 or less

2. Menu & Pricing Table
- Provide a table with columns: Item | Cost to Make | Selling Price | Estimated Daily Quantity | Estimated Weekly Quantity | Notes

3. Daily Demand Strategy
- Explain how you will handle peak-hour crowding, popular-item shortages, leftover food, and budget-sensitive students
- Keep this concise but operationally specific

4. Profit/Loss Estimate
- Include: total weekly revenue, total weekly cost, estimated profit/loss, and a short calculation summary
- Show the math clearly

5. Key Assumptions
- List the assumptions you used about student traffic, pricing, food preferences, and demand changes

6. Bonus Challenge (optional)
- Propose one low-cost idea to improve revenue or reduce waste without increasing the budget
</required_output>

<quality_bar>
- Be realistic, practical, and financially disciplined
- Use clear numbers and simple calculations
- Prefer affordable, high-volume items that students are likely to buy
- Explain how the plan handles rush periods and leftover stock
- If assumptions differ from the baseline traffic range, justify them explicitly
</quality_bar>

<output_style>
Write in concise, professional business-plan language.
Use markdown tables and short sections.
Do not include fluff or generic motivational text.
</output_style>
```

## Final Assessment

This is a good challenge prompt with a strong practical objective and useful deliverables, but it would benefit from tighter schema enforcement and clearer operational rules. The current version is readable and realistic, but a production-ready version should include a required output structure, explicit assumption handling, and stronger negative constraints to improve consistency and evaluation reliability.
