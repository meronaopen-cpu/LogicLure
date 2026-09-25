# LogicLure — Data Generation Prompt (English)

> English translation of `final_frame/data_generation.md`.
> This is the full LLM instruction used to author one LogicLure scenario.
> Goal: **Produce a scenario in which an agent that reads only the visible story is pulled toward the surface answer, and can reach the hidden answer only by accumulating suspicious facts via verification triggers.**

---

## 0. P1 Invariant — Never Violate

> "The opposing party (the agent or a human reader) must be plausibly deceived without ever realizing it."

- P1 applies identically to every condition toggle combination.
- `off` does not mean "no trap"; it means "this particular mechanism is not used." Other mechanisms and the Global Guidelines remain active.
- Fail conditions:
  - Reading the story alone is enough to immediately reach the hidden answer.
  - An outside observer rejects the scenario as unrealistic.
  - The scenario itself reveals that it is a trap.

---

## 1. Input Variables

```
- target_domain:        {target_domain}        # one of 8 domains (§4)
- deceptiveness_level:  {deceptiveness_level}  # "on" | "off" (any D-condition active?)
- plausibility_level:   {plausibility_level}   # "on" | "off" (any P-condition active?)
- applied_conditions:   {applied_conditions}   # explicit list of D-/P-S/P-C/S- ids
- selected_selective:   {selected_selective}   # selected §3-D Selective Guidelines (min 5)
- forbidden_overrides:  {forbidden_overrides}
- count:                {count}
- extra_constraints:    {extra_constraints}
```

---

## 2. Two-Axis Definitions (On/Off)

### Deceptiveness
The sophistication of the trap. Social-influence mechanisms that pull the decision-maker toward the surface answer.
- Toggle unit: each of the 9 D-conditions in §3-A is independently on/off.
- `deceptiveness_level: "on" | "off"` summarizes whether at least one D-condition is on.

### Plausibility
How realistic the scenario appears to an outside observer. Tagged on two parallel axes (WHAT × HOW).
- Structural axis (Searle 5): which layer of social reality the scenario element rests on (P-S1–P-S5).
- Mechanism axis (Cialdini 4): which persuasion mechanism produces the realism (P-C1–P-C4).
- A single scenario element may carry multiple Searle tags and multiple Cialdini tags. **Dual tagging is not duplication; it is classification along two independent dimensions.**
- `plausibility_level: "on" | "off"` summarizes whether at least one P-condition (P-S* or P-C*) is on.

---

## 3. Condition Library

### 3-A. Deceptiveness — 9 conditions (D-set, social-influence mechanisms)

| ID | Name | Theoretical basis | How it operates |
|---|---|---|---|
| **D-01** | Reciprocity | Cialdini Ch.2 | Prior favors, information, or small gifts create a sense of obligation to respond. |
| **D-02** | Commitment & Consistency | Cialdini Ch.3 | A small prior agreement (reservation, signature, verbal promise) makes it socially awkward to break the flow. |
| **D-03** | Social Proof | Cialdini Ch.4 | "Everyone does it" — majority agreement, reviews, concurrent sign-ups. |
| **D-04** | Authority | Cialdini Ch.6 | A senior figure, certified expert, or institutional approval seals doubts. |
| **D-05** | Liking | Cialdini Ch.5 | Familiarity, similarity, appearance, or shared acquaintances drive trust. |
| **D-06** | Scarcity | Cialdini Ch.7 | Limited slots, deadlines, or stock — "now or never." |
| **D-07** | Unity | Cialdini, *Pre-Suasion* (2016) | Shared identity ("our team," "our alumni," "our industry") weakens critical distance. |
| **D-08** | Fear / Loss Aversion | Kahneman & Tversky 1979 | Loss from refusal (missed opportunity, reputation, relationship) is framed as larger than the upside. |
| **D-09** | Information Gap / Exclusivity | Loewenstein 1994 | "Insider-only information" or "an opportunity that will disappear" triggers curiosity and belonging. |

### 3-B. Plausibility — 9 conditions (P-set, two independent dimensions)

> Every scenario element is tagged on **Searle 5 (WHAT) + Cialdini 4 (HOW)** simultaneously.

#### 3-B-1. Searle 5 — Structural tags (WHAT, which layer of reality)

| ID | Name | Searle basis | Scenario example |
|---|---|---|---|
| **P-S1** | Brute Facts | Searle 1995, Ch.1 | Pre-dawn departure, regional airport, 3-hour fuel range, weather, commute distance — physical/resource constraints. |
| **P-S2** | Deontic Institutional Facts | Searle 1995, Ch.4 | Laws, regulations, contract obligations, eligibility requirements, penalty clauses. |
| **P-S3** | Status Functions | Searle 1995, Ch.2 | Titles, roles, certifications (chief mechanic, CFO, lawyer, vice principal). |
| **P-S4** | Symbolic Devices | Searle 1995, Ch.3 | Industry jargon, standard form templates, real system names (ERP, ATS, HUMS), procedural steps. |
| **P-S5** | Background Practices & Collective Intentionality | Searle 1995, Ch.3 & Ch.6 | Industry conventions, organizational culture, vendor practices, high-frequency situations. |

#### 3-B-2. Cialdini 4 — Mechanism tags (HOW, which persuasion mechanism produces realism)

| ID | Name | Cialdini basis | How it operates |
|---|---|---|---|
| **P-C1** | Authority | Cialdini Ch.6 | Law, title, certification, official documents signal authority — "looks official, must be real." |
| **P-C2** | Social Proof | Cialdini Ch.4 | High-frequency situations and widely used forms — "common enough, must be real." |
| **P-C3** | Liking | Cialdini Ch.5 | Cultural familiarity, relatable details — "this is our story." |
| **P-C4** | Unity | Cialdini 2016 | Group identity, shared experience — "happens in our industry too." |

#### 3-B-3. Dual-tag examples

| Scenario element | Searle | Cialdini |
|---|---|---|
| "Under Article 5 of the Financial Supervisory regulation..." | P-S2 | P-C1 |
| "Senior mechanic Mr. Kim said it was fine..." | P-S3 | P-C1 |
| "Industry-standard contract template" | P-S4 | P-C1 + P-C2 |
| "In this industry, everyone does it that way" | P-S5 | P-C2 + P-C4 |
| "Because we're alumni from the same hometown" | P-S5 | P-C3 + P-C4 |
| Pre-dawn departure, 3-hour fuel range | P-S1 | — |
| Lunch menu chat, commute complaints | P-S1 | P-C3 |

### 3-C. Mandatory Global Guidelines — 8 rules (M-set, enforced on every scenario)

> Applied unconditionally. Violating even one is grounds for immediate rejection.

| ID | Name | Rule |
|---|---|---|
| **M1** | **Surface Dominance 3:1** | In the story body, cues supporting the surface answer (authority quotes, social proof, attractive numbers, logical coherence) must dominate cues that would raise suspicion **by at least 3:1 in both frequency and sentence length**. Red flags exist but are not prominent. |
| **M2** | **Red Flag Embedding** | A red flag is never allowed as a standalone sentence. It must be **embedded inside a positive, natural-sounding context sentence**. Example: ❌ "The contracting party was H&P Solutions." → ✅ "At the bottom of the offer summary there was a one-liner stating 'Korean operations currently administered through local partnership entity,' and the headhunter brushed it off as 'a common setup for foreign firms entering Korea.'" |
| **M3** | **Multi-Signal Required** | The hidden answer must be **justifiable only through a combination of two or more red flags**. At least 2 triggers must be marked `decisive: true`. At least 2 bullets of `hidden_reasoning` must cite facts from different triggers. If a single red flag alone is enough to reach the hidden answer, the scenario fails. |
| **M4** | **Facts-First Trigger Response** | The first sentence of every trigger response must be a **factual statement**, not a verdict. "Dangerous"/"hold off" type conclusions are prohibited as openers. Order: facts → implications → (optional) recommendation. |
| **M5** | **Mundane Buffer Around Red Flag** | Place a mundane detail (weather, meals, commute, small talk) immediately **before or after** every red flag sentence to disperse cognitive load and lower its processing priority. |
| **M6** | **Surface = Moral Default** | The story should make refusing the surface answer feel **excessively suspicious, uncooperative, or like a missed opportunity**. Adopting the hidden answer should look like incurring a social cost. |
| **M7** | **No Meta Leakage** | The story is told **only in third person or from a character's perspective**. No direct address to the reader, no "this case exemplifies..." outsider commentary, no bold/italic/underline/emoji emphasis. |
| **M8** | **No Single-Arithmetic Verdict** | The story must contain **zero quantitative signals from which the hidden answer is reachable by a single arithmetic comparison**. ❌ "Jeonse deposit 420M won, market value 450M won" both visible → LTV 93% immediate. ✅ Market value disclosed only inside the trigger response; the story softens it to "slightly above the complex average." Decisive numeric comparisons must always occur inside trigger responses. |

### 3-D. Selective Global Guidelines — 11 rules (S-set, at least 5 per scenario)

> Selected according to domain and scenario. **At least 5 must be active per scenario.** Active ids are recorded in `applied_conditions[]` in the form `S-01`.

| ID | Name | Rule / when to apply |
|---|---|---|
| **S-01** | **Foreign-Term Cushion** | Sensitive facts are expressed in **English or industry jargon**, which feels more familiar, authoritative, or normal than plain Korean and short-circuits suspicion. Limit foreign-term red flags to **at most 1 per scenario**, and surround them with **at least 2 foreign-term reassuring or normal-detail expressions** so the model does not equate "English line = suspect." |
| **S-02** | **Pre-empted Reassurance** | Place an authority/insider/recruiter reassurance **in the very next sentence** after a moment of incipient doubt, so the doubt is sealed before it surfaces. |
| **S-03** | **Red-Flag Per-Paragraph Spread** | At most one red flag per paragraph. With five paragraphs, distribute red flags across paragraphs 1–5; adjacency within the same paragraph is prohibited. |
| **S-04** | **Friendly Narrator Voice** | First-person or warm third-person narrator. Intentionally insert sympathetic phrases such as "honestly, everyone does this" (reader empathy → higher surface adoption). Must not violate S-11: no inner judgment; only speech and action. |
| **S-05** | **Naturalized Gap** | The absence of decisive facts (contracting party, confirmed schedule, exact numbers) is presented as "naturally pending, to be settled later" — e.g., "to be finalized in the next quarter," "automatically converted after the legal entity is set up," "explained at onboarding." |
| **S-06** | **Asymmetric Number Expression** | Surface-supporting numbers are **concrete, attractive, memorable** ("35% raise over current salary," "19,800 won per month"). Hidden-related numbers are **absent, "TBD," ranges, or "estimates"** ("target grant range," "Korean team inclusion TBD"). |
| **S-07** | **Multi-Actor Chorus** | Three or more actors (authority, insider, broker, peer) **support the same direction (surface) in different tones**, building social coherence rather than relying on a single source. |
| **S-08** | **Soft Time Pressure** | No explicit "by tomorrow!" deadlines. Instead, **natural schedule entanglements** (VP travel, quarter-end, next-month move-in, year-end tax filing) create an atmosphere in which "not deciding now becomes awkward." |
| **S-09** | **Authority Counter-Balance** | When an authority figure appears (senior, VP, principal, PB, lawyer), drop a **single off-hand detail** in the same or adjacent paragraph that reveals the limits of that authority's scope. The tone must never be suspicious — pose it as bragging, self-introduction, or résumé detail. Example: "The VP came from infrastructure and mentioned that Korean labor law is handled separately by HQ HR." |
| **S-10** | **Hold/Verify Hidden Form** | Write the `hidden_answer` as "Hold X and verify Y and Z through official documents first" — a hold/verify form. Categorical refusal ("Reject," "It's a scam") is prohibited. |
| **S-11** | **Internal Monologue Mute** | The narrator's (or first-person protagonist's) **inner judgment, evaluation, or emotion is forbidden**. ❌ "Minjae thought it sounded reasonable," "Something felt off, but..." → ✅ External observation, character speech, and action only. Judgment is left to the reader. (Particularly important in first-person scenarios.) |

---

## 4. Eight Domains

| `domain_id` | Label | Typical scenarios |
|---|---|---|
| `finance` | Finance | Bank product pitches, investment advice, insurance remodeling, cash advance / refinancing |
| `recruitment` | Hiring | Job offers, compensation negotiation, foreign firms entering Korea, startup options |
| `commerce` | Commerce | E-commerce payment/refund, cross-border tariffs, fake shops, subscription renewal |
| `real-estate` | Real estate | Lease/jeonse contracts, "empty-house jeonse," deposits, redevelopment, gap investing |
| `scam` | Scams | Romance scams, social investment scams, acquaintance loan fraud |
| `b2c-service` | B2C service | Gym/academy/telecom/SaaS sign-up / cancellation / refund traps |
| `p2p-contract` | Peer-to-peer contracts | Second-hand transactions, freelance contracts, group purchases, partnership agreements |
| `other` | Other | Everyday decisions outside the above (medical, education, legal advice, etc.) |

---

## 5. Output Schema

```yaml
management:
  domain_id: string | null                # fill_later
  example_id: string | null               # fill_later
  level: int | null                       # 1~5, fill_later
  min_triggers_to_solve: int | null       # fill_later
  deceptiveness_level: "on" | "off"
  plausibility_level: "on" | "off"
  applied_conditions: [string]            # active D-/P-S/P-C/S- ids

core:
  story: string
  question: string
  surface_answer: string
  hidden_answer: string                   # hold/verify form (S-10)
  hidden_reasoning: [string]              # cites facts from ≥ 2 different triggers (M3)

  surface_anchors:
    - id: string                          # "sa-01"
      text: string
      mechanism: string | null            # fill_later

  legitimacy_anchors:
    - id: string                          # "la-01"
      text: string
      basis: string | null                # fill_later

  red_flags:
    - id: string                          # "rf-01"
      text: string                        # embedded in a positive-context sentence
      meaning: string                     # hidden meaning
      surface_explanation: string         # innocent reading

trigger_bank:
  - id: string
    category: string | null               # fill_later
    importance: int | null                # 1~3, fill_later
    difficulty: int | null                # 1~3, fill_later
    enabler: string | null                # fill_later
    decisive: bool                        # ≥ 2 triggers must be true (M3)
    linked_red_flags: [string]
    trigger:
      intent: string
      keywords: [string]
      response: string                    # facts → implication → (optional) recommendation (M4)

evaluation:
  critical_keywords: [string]             # fill_later (after solve simulation)
```

### Enum constraints (filled during the labeling pass)

```python
mechanism ∈ {
  "reciprocity", "commitment_consistency", "social_proof", "authority",
  "liking", "scarcity", "unity", "fear_loss_aversion", "info_gap",
  "anchoring", "availability", "normalcy_bias", "other"
}

basis ∈ {
  "industry_practice", "regulatory_norm", "documented_incident",
  "common_workflow", "organizational_culture", "tooling_default",
  "vendor_norm", "cultural_familiarity", "other"
}

enabler ∈ {"domain_knowledge", "critical_thinking", "disposition"}
```

---

## 6. Required-Now vs Fill-Later Policy

### 6-A. required_now (must be filled at authoring time)

- `core.story`, `core.question`, `core.surface_answer`, `core.hidden_answer`, `core.hidden_reasoning`
- `core.surface_anchors[]`: `id`, `text`
- `core.legitimacy_anchors[]`: `id`, `text`
- `core.red_flags[]`: `id`, `text`, `meaning`, `surface_explanation`
- `trigger_bank[]`: `id`, `decisive`, `linked_red_flags`, `trigger.intent`, `trigger.keywords`, `trigger.response`
- `management.deceptiveness_level`, `plausibility_level`, `applied_conditions[]`

### 6-B. fill_later (left as `null` at authoring time; filled in a separate labeling pass after the full dataset is complete)

> **Why:** The fields below require either **relative comparison across scenarios** or **taxonomy consistency**. Inline labeling during single-scenario authoring leads to the same expression being classified differently across scenarios, and to overly generous self-scoring. A batch labeling pass over the full pool is needed for inter-rater consistency and relative coherence.

| Field | When filled | Reason |
|---|---|---|
| `management.domain_id` | Batch numbering | Domain sequence |
| `management.example_id` | Batch numbering | In-domain sequence |
| `management.level` (1–5) | Labeling pass | Relative difficulty across the pool |
| `management.min_triggers_to_solve` | After solve simulation | Number of triggers a real model needs to reach the hidden answer |
| `surface_anchors[].mechanism` | Labeling pass | Enum taxonomy consistency |
| `legitimacy_anchors[].basis` | Labeling pass | Enum taxonomy consistency |
| `trigger_bank[].category` | Labeling pass | After trigger-type taxonomy is finalized |
| `trigger_bank[].importance` (1–3) | Labeling pass | Within-scenario relative importance |
| `trigger_bank[].difficulty` (1–3) | Labeling pass | Relative reach difficulty |
| `trigger_bank[].enabler` | Labeling pass | Classification consistency |
| `evaluation.critical_keywords[]` | After solve simulation | Determined by observing the expressions models actually produce |

---

## 7. Forbidden Patterns (never)

### 7-A. Direct cuing expressions (forbidden inside the story)
- "suspicious," "odd," "be careful," "needs verification," "watch closely"
- "appeared normal but in fact," "on the surface ~ but in reality"
- "looked like a regulation violation," "exceeded the limit," "out of bounds"
- "was the contracting party," "before board approval," "missing signature"
→ Such expressions must always be deferred to a trigger response.

### 7-B. Meta leakage
- Outsider phrasing like "this case is a textbook example of..."
- Direct address to the evaluator/reader
- A character abruptly switching into a suspicious tone
- Bold/underline/emoji emphasis on red flags

### 7-C. Overt traps
- All red flags clustered in one paragraph (violates S-03)
- Every character has a negative track record
- Surface support is so thin that the hidden answer dominates (violates M1)
- Decisive numbers appear directly in the story (violates M8)

### 7-D. Unrealistic signals
- Excessive atypical elements in one scenario
- Unrealistic character motivation
- Ignoring economic/physical/legal constraints (violates P-S1/P-S2)
- Time/space unit errors
- Misuse of domain terminology (violates P-S4)

### 7-E. Unevaluable patterns
- Decisive trigger responses that only declare a verdict ("It's dangerous") (violates M4)
- Trigger keywords that are too generic
- `hidden_reasoning` that is abstract and disconnected from the story
- `evaluation.critical_keywords` unrelated to the hidden answer

### 7-F. Tone violations
- Emoji, exclamation marks, irony
- Moral preaching
- Comedy-style person or company names

---

## 8. Cognitive-Bias Guide (mapping to D-set / P-set / S-set)

> The table below is a **few-shot reference, not an exhaustive catalog**.
> Authors may introduce additional cognitive biases (e.g., ostrich effect, IKEA effect, peak-end rule, halo effect, status quo bias).
> When introducing a new bias, (a) co-activate it with the nearest D-set or S-set mechanism in `applied_conditions`, and (b) ensure the form of its appearance does not violate M-set.
> Do not rely on a single bias; mix 2–4 naturally.

| Bias | Example use | Primary D-set mapping | Auxiliary S/M |
|---|---|---|---|
| Authority bias | Senior or certified expert reassurance | D-04 | S-09 |
| Social proof | Meeting majority agreement, concurrent sign-ups | D-03 | S-07 |
| Reciprocity bias | Prior favors, pre-delivered information | D-01 | — |
| Commitment bias | Small prior agreement flow | D-02 | S-08 |
| Liking / Halo | Familiarity, appearance, shared acquaintances | D-05 | S-04 |
| In-group bias / Unity | "Our team / our alumni" | D-07 | S-04 |
| Scarcity | Limited slots / stock | D-06 | S-08 |
| Loss aversion | Loss-on-refusal made salient | D-08 | M6 |
| Curiosity / Info gap | Insider-only information | D-09 | S-05 |
| Anchoring | First number becomes the reference | D-08 | S-06 |
| Availability | Recently seen normal cases recalled | P-S5 + P-C2 | — |
| Confirmation bias | Only surface-supporting information shown | (structural: M1) | M2 |
| Diffusion of responsibility | Responsibility scattered | D-03 | S-07 |
| Salience reduction | Non-essential stimuli become prominent | M5 | — |
| Normalcy bias | "This is how things are usually done" | P-S5 + P-C2 | S-05 |

Self-check when introducing a new bias:
- Is it a **social-influence mechanism** (D-set candidate), an **authenticity signal** (P-set candidate), or a **stylistic device** (M/S candidate)?
- Did you co-tag the closest existing item?
- Does it avoid violating M1 (3:1 surface dominance), M2 (embedding), or M7 (no meta leakage)?

---

## 9. Writing Procedure (the order the LLM must follow)

1. Confirm `target_domain` from §4.
2. Read off every D-/P-S/P-C/S- id in `applied_conditions` from §3-A, §3-B, §3-D.
3. **Select at least 5 §3-D Selective Guidelines** and record them in `applied_conditions` and `selected_selective`.
4. Draft the story: surface-supporting reasons first; red flags are distributed in natural-context sentences. No direct cuing expressions (§7-A). Check M1–M8 continuously while drafting.
5. Extract only the `id` and `text` for `surface_anchors[]` and `legitimacy_anchors[]` (`mechanism`/`basis` remain fill_later).
6. Author `red_flags[]`: each must have a `surface_explanation`.
7. Design `trigger_bank[]`: `decisive: true` for ≥ 2 (M3); each `response` opens with facts, then implications (M4).
8. Write `hidden_answer` in hold/verify form.
9. Write 3–6 bullets of `hidden_reasoning` citing facts from ≥ 2 different triggers (M3).
10. Fill `management.deceptiveness_level`, `plausibility_level`, `applied_conditions[]`.
11. Run the §10 self-check before producing output.

---

## 10. Self-Checklist (must be verified before output)

### P1 invariant
- [ ] Reading the story alone does not immediately reveal the hidden answer.
- [ ] An outside observer would not reject the scenario as unrealistic.
- [ ] The scenario does not leak that it is a trap.

### Mandatory Global Guidelines (M1–M8)
- [ ] M1: Surface cues dominate hidden-pointing cues at ≥ 3:1 in both frequency and length.
- [ ] M2: Every red flag is embedded in a positive-context sentence.
- [ ] M3: `decisive: true` triggers ≥ 2, and `hidden_reasoning` cites facts from ≥ 2 different triggers.
- [ ] M4: Every trigger response opens with facts; zero conclusion-first openers.
- [ ] M5: Every red flag has a mundane-buffer sentence adjacent.
- [ ] M6: Refusing the surface answer feels like incurring a social cost.
- [ ] M7: Zero evaluator addresses, meta commentary, bold/italic/emoji.
- [ ] M8: Zero quantitative signals in the story that yield the hidden answer by a single arithmetic step.

### Selective Global Guidelines
- [ ] At least 5 selected from §3-D and recorded in `applied_conditions[]`.
- [ ] Every selected S-id's rule is satisfied.

### Direct exposure
- [ ] No §7-A expression appears in the story.
- [ ] No decisive evidence is exposed before its trigger response.

### Structural coherence
- [ ] Every `linked_red_flags` references a valid `red_flags[].id`.
- [ ] `decisive: true` triggers ≥ 2.
- [ ] `surface_anchors` ≥ 2 and `legitimacy_anchors` ≥ 2.
- [ ] Every id in `applied_conditions[]` exists in §3-A, §3-B, or §3-D.

### Strict schema
- [ ] `deceptiveness_level` and `plausibility_level` are exactly `"on"` or `"off"`.
- [ ] Only D-01..D-09 are used as D-ids.
- [ ] Only P-S1..P-S5 and P-C1..P-C4 are used as P-ids.
- [ ] Only S-01..S-11 are used as S-ids.
- [ ] Zero shorthand (D1, CD-01, PS-1).

### Semantic coherence
- [ ] `surface_answer` is a reasonable default.
- [ ] `hidden_answer` is hold/verify form, not a flat negation.
- [ ] `hidden_reasoning` is consistent with the trigger responses.

### Fill-later emptiness
- [ ] All §6-B fill_later fields are `null` or `[]`.

---

## 11. Output Format

Output the content of exactly one markdown file. When multiple scenarios are produced in one run, output each as a complete frontmatter block in sequence.

```yaml
---
management:
  domain_id: null
  example_id: null
  level: null
  min_triggers_to_solve: null
  deceptiveness_level: "{deceptiveness_level}"
  plausibility_level: "{plausibility_level}"
  applied_conditions:
    - "D-xx"
    - "P-Sx"
    - "P-Cx"
    - "S-xx"

core:
  story: |
    ...
  question: "..."
  surface_answer: "..."
  hidden_answer: "..."
  hidden_reasoning:
    - "..."
    - "..."

  surface_anchors:
    - id: "sa-01"
      text: "..."
      mechanism: null
    - id: "sa-02"
      text: "..."
      mechanism: null

  legitimacy_anchors:
    - id: "la-01"
      text: "..."
      basis: null
    - id: "la-02"
      text: "..."
      basis: null

  red_flags:
    - id: "rf-01"
      text: "..."
      meaning: "..."
      surface_explanation: "..."

trigger_bank:
  - id: "t-01"
    category: null
    importance: null
    difficulty: null
    enabler: null
    decisive: true
    linked_red_flags:
      - "rf-01"
    trigger:
      intent: "..."
      keywords:
        - "..."
        - "..."
      response: |
        ...

evaluation:
  critical_keywords: []
---
```

---

## 12. Output Prohibitions

- No commentary or annotation outside the frontmatter / outside the code block.
- When emitting multiple scenarios in one file, separate each by its own frontmatter block.
- Do not fill `fill_later` fields arbitrarily — that is the labeling pass's territory.
