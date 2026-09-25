# LogicLure

Accepted to the **Main Conference of AACL-IJCNLP 2026**. [Paper (placeholder)](https://example.com/logiclure-paper)

A benchmark for evidence-grounded decision-making under hidden risks.

- [dataset.json](dataset.json): 208 English scenarios across 8 domains, stored as a JSON array.
- [generation_prompt.md](generation_prompt.md): English authoring prompt based on the scenario-generation rules.

Use `core.story` and `core.question` as model input; the remaining fields are reference annotations.

## Dataset structure

`dataset.json` is an array of scenario objects. Each scenario contains four fields:

| Field | Type | Contents |
|---|---|---|
| `management` | Object | Scenario ID, domain, difficulty, minimum trigger requirement, and deceptiveness/plausibility conditions. |
| `core` | Object | Visible `story` and `question`; reference answers, reasoning, surface/legitimacy anchors, and red flags. |
| `trigger_bank` | Array | Verification triggers, their annotations, and links to red flags. |
| `evaluation` | Object | `critical_keywords` for reference-based evaluation. |

Each trigger includes `trigger.intent` (what to verify), `trigger.keywords` (matching terms), and `trigger.response` (the canonical oracle response). Its `decisive` flag marks decisive evidence, and `linked_red_flags` references IDs in `core.red_flags` within the same scenario.
