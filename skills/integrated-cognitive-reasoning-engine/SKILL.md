---
name: integrated-cognitive-reasoning-engine
description: >
  Structured 5-module cognitive reasoning pipeline for explainable, logical,
  and probabilistically accurate analysis. Use when the task involves noisy or
  uncertain data, contradictions or anomalies, root cause analysis, causal
  "why" questions, multi-variable decision-making, counterfactual "what-if"
  planning, confidence scoring, hallucination recovery, sensor data
  interpretation, or safety-critical reasoning. Also activated immediately
  by the keywords /icre or /reason anywhere in the user message. Routes input
  through neurosymbolic grounding, abductive hypothesis selection, causal
  modeling, Bayesian uncertainty quantification, and meta-cognitive
  self-correction. Appends a Reasoning_Trace block to every output.
license: MIT
metadata:
  homepage: https://github.com/ohrbit/edgeai/skills/integrated-cognitive-reasoning-engine
  author: downwind-lee x perplexity x claude sonnet 4.6 webui
  version: "1.0.0"
  project: ICRE
  tags: reasoning, causal, bayesian, neurosymbolic, explainability
  id: spark-think
  aliases: [Agent_API, Inter-Agent_Protocol]
  galaxy_links: [[SOUL], [MEMORY], [REASONING]]
  shape: box
  pinned: true
  callout: true
---

## Integrated Cognitive Reasoning Engine

### Manual Activation Keywords
If the user message contains `/icre` or `/reason`, activate this skill
**immediately**, regardless of any other context.

- `/icre` — full pipeline activation, e.g. `/icre warum fällt mein pH-Sensor immer nachts aus?`
- `/reason` — shorthand alias, e.g. `/reason is this sensor data reliable?`

---

Process ALL inputs through the following 5-module pipeline **in sequence**
before generating a final response.

---

### Module 1 — Neurosymbolic Ingestion *(Data Grounding)*
Parse unstructured or noisy input into discrete semantic tokens.
Map tokens to symbolic logic rules. **Reject any fact that fails
deterministic logical validation** before passing to Module 2.

---

### Module 2 — Abductive Anomaly Resolution *(Hypothesis Generation)*
Scan for contradictions, missing data, or anomalies.
If found: halt standard prediction → generate mutually exclusive hypotheses
→ select the hypothesis with maximum explanatory power and minimum complexity
(Occam's Razor).

---

### Module 3 — Causal Modeling & Counterfactuals *(Structural Logic)*
Build a directional causal graph from validated variables.
Never conflate correlation with causation.
Apply do-calculus: P(Y | do(X)).
Evaluate counterfactual "what-if" scenarios to isolate true intervention impact.

---

### Module 4 — Virtual Bayesian Updating *(Uncertainty Management)*
Assign virtual likelihood ratios to uncertain evidence.
Apply Jeffrey's updating rule:
P_new(H) = Σ P(H|Ei) · P_virtual(Ei)
Adjust confidence scores **gradually** — no binary assertions.

---

### Module 5 — Meta-Cognitive Oversight *(Self-Correction)*
Monitor all prior modules for logic loops, dead-ends, or hallucination signals.
If detected: trigger explicit PAUSE → re-evaluate heuristic →
reallocate focus → document error signal for pattern recognition → RESUME.

---

## Execution Routing Table

| Input State              | Primary Module           | Output State                         |
|--------------------------|--------------------------|--------------------------------------|
| Unstructured/messy data  | Neurosymbolic Ingestion  | Validated symbolic tokens            |
| Contradictions/anomalies | Abductive Reasoning      | Most plausible root-cause hypothesis |
| Strategy / "Why" / Plan  | Causal Reasoning         | Verified intervention outcome        |
| Noisy sensors/ambiguity  | Virtual Bayesian         | Posterior belief + confidence range  |
| Hallucination/logic loop | Meta-Cognitive Oversight | Process halted, strategy revised     |

---

## Output Format

Append a `<Reasoning_Trace>` block at the end of every response:

```xml
<Reasoning_Trace>
  Modules_Activated: [M1 Neurosymbolic] → [M3 Causal] → [M4 Bayesian]
  Causal_Intervention: do(X) → P(Y | do(X)) = 0.87
  Bayesian_Confidence: 0.82 posterior [CI: 0.74–0.89], updated from 0.51 prior
  Meta_Cognitive_Events: none
</Reasoning_Trace>
```

See [references/REFERENCE.md](references/REFERENCE.md) for detailed
module theory and mathematical derivations.
