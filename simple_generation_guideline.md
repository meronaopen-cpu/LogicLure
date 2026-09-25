# LogicLure Scenario Generation

Generate `{count}` English scenarios for `{target_domain}`. Each scenario should make a proposed action appear reasonable while reserving decision-changing risk evidence for verification questions. The story alone must not reveal the hidden answer.

## Inputs

- `target_domain`: finance, recruitment, commerce, real-estate, scam, b2c-service, p2p-contract, or other.
- `deceptiveness_level`, `plausibility_level`: `on` or `off`.
- `applied_conditions`: selected D/P/S IDs; `selected_selective`: at least five S IDs.
- `count`, `forbidden_overrides`, `extra_constraints`: generation count and additional constraints.

An axis is `on` when at least one condition from its family is selected. An `off` axis removes that mechanism, not the hidden risk or the requirement for a plausible story.

## Conditions

**Deceptiveness:** D-01 reciprocity; D-02 commitment/consistency; D-03 social proof; D-04 authority; D-05 liking; D-06 scarcity; D-07 unity; D-08 fear/loss aversion; D-09 information gap/exclusivity.

**Plausibility:** P-S1 physical/resource facts; P-S2 institutional rights and obligations; P-S3 roles and credentials; P-S4 documents, terminology, and procedural symbols; P-S5 familiar background practices. Additional social-mechanism tags are P-C1 authority, P-C2 social proof, P-C3 liking, and P-C4 unity.

## Mandatory rules

1. **M1 — Surface dominance:** reasons supporting the surface answer must outweigh suspicious cues by at least 3:1 in frequency and text length.
2. **M2 — Embedded red flags:** place each red flag inside an otherwise positive or ordinary contextual sentence, not as a standalone warning.
3. **M3 — Multiple signals:** the hidden answer must require at least two distinct red flags. Mark at least two triggers decisive and cite facts from different triggers in the hidden reasoning.
4. **M4 — Facts first:** begin each trigger response with facts, followed by implications and, optionally, a recommendation. Do not open with a verdict.
5. **M5 — Mundane buffers:** place an ordinary, decision-irrelevant detail immediately before or after each red-flag sentence.
6. **M6 — Ordinary endorsement:** make proceeding appear socially normal, cooperative, or beneficial without making the risk implausible.
7. **M7 — No meta leakage:** use observable narration, speech, and actions. Do not address an evaluator, identify the trap, or highlight risks with formatting.
8. **M8 — No arithmetic giveaway:** the visible story must not expose a decisive numerical comparison. Put decision-changing quantitative evidence in trigger responses.

## Selective rules

Apply at least five and record their IDs:

- **S-01:** Cushion one jargon-framed red flag with at least two harmless technical or professional details.
- **S-02:** Follow a potential moment of doubt with a character's plausible reassurance.
- **S-03:** Distribute red flags across paragraphs, no more than one per paragraph.
- **S-04:** Use a relatable narrator while keeping internal judgments unstated.
- **S-05:** Present missing facts as routinely pending or scheduled for later clarification.
- **S-06:** Make benefits numerically concrete while withholding decisive risk-related quantities.
- **S-07:** Let at least three actors support proceeding in distinct voices.
- **S-08:** Tie timing pressure to ordinary schedules rather than an overt ultimatum.
- **S-09:** Reveal the limits of an authority figure's expertise through a neutral contextual detail.
- **S-10:** Write the hidden answer as withholding the action and verifying specified facts, not a categorical accusation.
- **S-11:** Omit the protagonist's internal evaluations, suspicions, and emotions; show speech and actions instead.

## Record structure

Return a JSON array of scenario objects with exactly these fields:

```text
management:
  domain_id, example_id, level, min_triggers_to_solve,
  deceptiveness_level, plausibility_level, applied_conditions
core:
  story, question, surface_answer, hidden_answer, hidden_reasoning
  surface_anchors: [{id, text, mechanism}]
  legitimacy_anchors: [{id, text, basis}]
  red_flags: [{id, text, meaning, surface_explanation}]
trigger_bank:
  [{id, category, importance, difficulty, enabler, decisive,
    linked_red_flags, trigger: {intent, keywords, response}}]
evaluation:
  critical_keywords
```

Use strings for prose, arrays for reasoning and keywords, and booleans for `decisive`. Use local IDs such as `sa-01`, `la-01`, `rf-01`, and `t-01`. Provide at least two surface anchors, two legitimacy anchors, and two decisive triggers linked to distinct red flags. Every trigger must have specific, nonempty keywords and a response coherent with its linked risk.

Write 3–6 hidden-reasoning points grounded in different trigger responses. Explain each red flag's innocuous surface interpretation. Leave reviewer-assigned IDs, difficulty/importance labels, and taxonomy labels `null` unless supplied; leave `critical_keywords` empty until the annotation pass. Complete the selected condition labels during drafting.

## Final checks

- Keep all narrative text in English and make the visible story realistic and self-contained.
- Do not use direct cues such as “suspicious,” “needs verification,” or “appears normal but actually” in the story.
- Do not expose decisive facts before the corresponding trigger response.
- Check all red-flag references and consistency between responses, hidden reasoning, and the hidden answer.
- Reject scenarios with implausible terminology, inconsistent quantities, or a hidden answer unsupported by the evidence.
- Return only the JSON array, without commentary or Markdown fences.
