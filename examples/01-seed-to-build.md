# Example 1: Seed idea → interview → deployed prompt

A complete, unedited session. One vague sentence in; a zero-placeholder, paste-and-run deliverable out. Annotations in blockquotes are added for this document — everything else is the raw session.

---

**User:**

> I want a prompt that plans my weekly meals and builds the grocery list.

**Framework:**

I understand you want a prompt that plans weekly meals and generates a consolidated grocery list. To build this well, I need to fill in a few gaps.

**Round 1:**

1. **Household & dietary context** — How many people are you planning for, and are there any dietary constraints or preferences (vegetarian, allergies, macro targets, etc.)?

2. **Scope & cooking reality** — How many meals per day should the plan cover (all three + snacks, or just dinners?), and what's your typical cooking-time budget on weekdays vs. weekends?

3. **Planning priority** — What matters most: variety/not repeating meals, staying under a grocery budget, minimizing food waste / using overlapping ingredients, or something else?

🔴 **Discovery** — Core objective clear (meal plan + grocery list), but household shape, dietary constraints, and planning priorities are all open.

> *Every interview message carries a readiness indicator. The framework cannot generate until the gates to 🟢 are met — or the user says "Go", which skips ahead with assumptions flagged.*

**User:**

> 1. One person. No allergies, I dont like broccoli. I want to have a protein and fibre rich diet thats healthy and still tasty.
> 2. lunch and dinner plus snacks in between. breakfast is covered already.
> 3. Cheap but getting to my calorie targets reliably

**Framework:**

Good, that narrows it well. A couple more things that would materially change the plan:

**Round 2:**

1. **Calorie target** — What's your daily calorie goal? (And do you know roughly how many calories breakfast already covers, so the plan can budget the remainder across lunch, dinner, and snacks?)

2. **Cooking style** — Do you batch-prep (e.g., cook Sunday, eat all week) or cook fresh most days? And how often do you shop — once a week, or more?

🟡 **Refining** — Foundation set: solo, protein/fiber focus, no broccoli, budget-conscious, lunch+dinner+snacks. Need calorie target and prep style to build a plan that actually hits the numbers and fits your routine.

**User:**

> 1. 3000 breakfast covers around 700
> 2. shopping once a week. batch prep on sunday

**Framework:**

That covers it. Let me lock the ledger and build.

**Ledger** — 0 Objective: weekly meal plan (lunch/dinner/snacks) hitting 2,300 daily kcal + batch-prep plan + consolidated budget grocery list · 1 Context: solo, batch-prep Sundays, one weekly shop, breakfast handled separately (~700 kcal) · 2 Audience: the user · 3 Requirements: ≥150 g protein/day, ≥30 g fiber/day, no broccoli, budget-minimized, variety rotation · 4 Tone/Style: structured output — day-by-day table with macros, prep checklist, sectioned grocery list (functional default for a planning artifact) · 5 Other: N/A after scanning for equipment constraints, cuisine restrictions, and dietary-tracking integration — user volunteered none beyond broccoli; standard kitchen and open cuisine assumed.

🟢 **Ready**

> *The coverage ledger is the gate: the framework must state the objective and summarize every category before it may declare readiness. Note category 5 — it names the dimensions it scanned and the assumptions it took, rather than a reflex "nothing else needed." The user said "protein and fibre rich" without numbers; the framework quantified that into concrete targets (≥150 g / ≥30 g) as a defensible default — and flags both assumptions in the Delivery Block below, where the user can correct them.*

---

🎯 **Mode Selected:** Standalone Trigger Prompt (Mode 1)

**Reasoning:** All user-specific variables resolved through the interview — zero unresolved remain. Well-defined single-shot task with clear output structure. No consultative scaffold needed: the parameters are fixed, and the prompt executes identically each week (with optional per-week variation via an appended note).

🌍 **Deploy in:** Claude chat (standard) — or any LLM chat session
**Install/Invoke:** Paste as the opening message of a new chat. Optionally append a line or two for the week (e.g., "I have leftover rice and ground turkey" or "leaning Mediterranean this week").
**Model tier:** Any current mid-tier model handles this comfortably.
**Why:** Structured text-in/text-out with no persistence, tool, or file requirements.

**Key Optimization Strategy:** All parameters baked in with specific numbers — no placeholders to fill. Batch-prep plan added as a dedicated output section since Sunday prep is the operational backbone. Budget strategy embedded as ingredient-selection heuristics rather than a vague "keep it cheap" instruction.

---

🚀 **Your Optimized Prompt**

```
You are a practical meal-planning nutritionist. Generate a complete weekly meal plan and consolidated grocery list based on the fixed parameters below.

If the user appends a weekly note (leftover ingredients to use up, a cuisine craving, a meal to skip), incorporate it. Otherwise, plan fresh from the parameters alone.

## Parameters (fixed)

- Covers: lunch, dinner, and 2 snacks per day (Mon–Sun). Breakfast is handled separately.
- Daily calorie target across these meals: 2,300 kcal
- Macro priority: high protein (≥150 g/day across planned meals), high fiber (≥30 g/day)
- Household: 1 person
- Excluded ingredients: broccoli
- Budget: minimize grocery cost — prefer bulk staples, seasonal produce, versatile proteins (thighs over breasts, dried legumes over canned, frozen veg where quality holds)
- Prep model: batch-prep on Sunday, quick assembly or reheating on weekdays. Weekend dinners may be cooked fresh.
- Shopping: one trip per week

## Output (three sections, in order)

### 1. Weekly Meal Plan

Day-by-day table (Mon–Sun). Columns: Meal (Lunch / Snack 1 / Snack 2 / Dinner), Dish, Calories, Protein (g), Fiber (g). Show daily totals. Flag any day that drifts more than 150 kcal from the 2,300 target.

Variety rule: no identical main dish more than twice per week. Rotate protein sources across the week (poultry, legumes, eggs, fish, pork, tofu).

### 2. Sunday Batch-Prep Plan

Checklist in cooking order (longest-cook items first). Per item: yield in servings, which meals it feeds, and storage instruction (fridge or freezer, expected shelf life).

### 3. Grocery List

Organized by store section: Produce · Protein/Meat · Dairy & Eggs · Grains & Legumes · Frozen · Pantry Staples · Other. Each item with quantity needed for the full week. Omit common pantry basics (salt, pepper, oil) unless a recipe needs an unusual amount.

## Rules

- Every dish is a real, named meal — no generic "protein + veg + grain" placeholders.
- Plan ingredient overlap across meals to reduce waste and cost.
- Hit macro targets through snack composition when main meals fall short — don't inflate portions.
- Include a one-line prep note per dish only when the method isn't obvious (e.g., "marinate overnight").
```

---

📋 **Delivery Block**

**Top Strengths:**
- Zero placeholders — all parameters baked in from the interview, so the prompt executes on paste with no setup friction.
- The batch-prep section is structurally tied to the meal plan (it names which meals each prep feeds), so the two outputs stay internally consistent.
- Budget strategy is operationalized as ingredient-selection heuristics rather than a vague directive — the model knows *how* to be cheap, not just that it should be.

**Known Limitations:**
- Calorie and macro estimates from any LLM are approximate, not lab-measured. If precise tracking matters, cross-check a few key dishes against a nutrition database (e.g., Cronometer) during the first week and recalibrate expectations.
- The prompt assumes a standard kitchen (oven, stovetop, basic cookware). If you're working without an oven or have specific appliances (Instant Pot, air fryer) that should shape recipe selection, append that to the weekly note or I can bake it into the parameters.

**Verify Before Use:**
- Confirm the 150 g protein / 30 g fiber daily targets feel right for your goals — these are solid defaults for a high-protein diet but worth checking against your actual tracking if you use Hevy or a nutrition app alongside this.

> *One transparency note: the mention of a specific fitness app in the last line comes from the maintainer's account memory — Claude Projects feed known user context into sessions. Your runs won't reference tools you never mentioned. This personalization behavior is documented in the README's limitations.*
