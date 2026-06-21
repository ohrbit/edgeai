# 🧠 Integrated Cognitive Reasoning Engine (ICRE)

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/downwind-lee/integrated-cognitive-reasoning-engine)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-purple.svg)](https://agentskills.io)
[![Standard](https://img.shields.io/badge/format-SKILL.md-orange.svg)](SKILL.md)

> A structured, multi-modal cognitive reasoning pipeline that routes any input through five sequential reasoning modules before generating a response — delivering explainability, logical consistency, and probabilistic accuracy on every output.

---

## 📋 Overview

Modern LLMs generate plausible-sounding responses based on statistical patterns. **ICRE** enforces a deterministic reasoning architecture on top of any LLM, transforming it into a structured cognitive system that:

- ✅ Grounds unstructured input into logically validated tokens
- ✅ Detects anomalies and resolves them via best-explanation hypothesis selection
- ✅ Separates correlation from causation using causal graph modeling
- ✅ Quantifies uncertainty with Bayesian posterior updates instead of binary assertions
- ✅ Monitors itself for hallucinations and logic loops with automatic recovery

Every response includes a `<Reasoning_Trace>` block showing exactly which modules fired, which causal interventions were selected, and the final Bayesian confidence score.

</div>
<p align="center">
  <img src="https://github.com/ohrbit/edgeai/blob/main/skills/integrated-cognitive-reasoning-engine/assets/hero.png" alt="front" width="80%" />

---

## 🚀 Quick Start

### Manual Activation Keywords

Trigger ICRE instantly by prefixing any message with:

| Keyword | Description |
|---------|-------------|
| `/icre` | Full pipeline activation |
| `/reason` | Shorthand alias |

**Examples:**
```
/icre why does my pH sensor drop every night at 23:00?
/reason is this CO2 sensor reading reliable?
```

### Installation

**Claude Code**
```bash
cp -r integrated-cognitive-reasoning-engine ~/.claude/skills/
```

**Cursor**
```bash
cp -r integrated-cognitive-reasoning-engine .cursor/skills/
```

**Gemini CLI**
```bash
cp -r integrated-cognitive-reasoning-engine ~/.gemini/skills/
```

**Roo Code / VS Code**
```bash
cp -r integrated-cognitive-reasoning-engine .roo/skills/
```

**Validate**
```bash
npx skills-ref validate ./integrated-cognitive-reasoning-engine
```

---

## 🔬 The 5 Reasoning Modules

### Module 1 — Neurosymbolic Ingestion *(Data Grounding)*

Parses noisy or unstructured input into discrete semantic tokens, then maps them against symbolic logic predicates. Any fact that fails deterministic logical validation is rejected before advancing — preventing hallucinations at the source.

```
Raw Input → Neural Parsing → Semantic Tokens → Symbolic Validation Gate
                                                        ↓
                                           PASS → Module 2  |  FAIL → Clarification
```

---

### Module 2 — Abductive Anomaly Resolution *(Hypothesis Generation)*

When contradictions or anomalies are detected, standard prediction halts. Multiple mutually exclusive hypotheses are generated and scored using **Inference to the Best Explanation (IBE)**:

```
Score(Hi) = ExplanatoryPower(Hi) / Complexity(Hi)
H* = argmax_i [ Score(Hi) ]
```

> **Example:** EC sensor drops to 0 nightly → H1: hardware failure (0.40) vs H2: timer relay cycling (0.90) → H2 selected ✓

---

### Module 3 — Causal Modeling & Counterfactuals *(Structural Logic)*

Builds a Directed Acyclic Graph (DAG) of cause→effect relationships. Applies Pearl's **do-calculus** to compute true interventional probabilities — not observational correlations:

```
P(Y | do(X = x))  ≠  P(Y | X = x)
```

Evaluates counterfactual "what-if" scenarios by blocking confounders via the backdoor adjustment formula.

---

### Module 4 — Virtual Bayesian Updating *(Uncertainty Management)*

Handles noisy, uncertain evidence using **Jeffrey's Conditioning** (1965) — updating beliefs based on probability distributions over evidence, not hard observations:

```
P_new(H) = Σ_i P(H | E_i) · P_virtual(E_i)
```

All confidence scores are expressed as posterior ranges with 95% CI — never as binary assertions.

---

### Module 5 — Meta-Cognitive Oversight *(Self-Correction)*

Continuously monitors the reasoning pipeline for failure modes. Triggers a **PAUSE** if:

- Reasoning depth > 8 nested steps without convergence
- Contradiction detected between Module 1 output and Module 3 causal graph
- Confidence score oscillates (Δ > 0.3 between consecutive updates)
- Same hypothesis appears in >2 abductive cycles without resolution

Recovery: HALT → Snapshot state → Re-evaluate heuristic → Reallocate focus → RESUME

---

## 🗺️ Execution Routing Table

| Input State Detected | Primary Module Triggered | Desired Output State |
|---|---|---|
| Unstructured / messy data | Neurosymbolic Ingestion | Validated symbolic tokens |
| Contradictions or anomalies | Abductive Reasoning | Most plausible root-cause hypothesis |
| Strategy, planning, or "why" | Causal Reasoning | Verified intervention outcome |
| Noisy sensors or ambiguity | Virtual Bayesian Reasoning | Posterior belief + confidence interval |
| Hallucination or logic loop | Meta-Cognitive Oversight | Process halted, strategy revised |

---

## 📤 Output Format

Every ICRE response appends a structured trace block:

```xml
<Reasoning_Trace>
  Modules_Activated: [M1 Neurosymbolic] → [M2 Abductive] → [M3 Causal] → [M4 Bayesian]
  Anomaly_Detected: EC sensor dropout at 23:00 daily
  Selected_Hypothesis: H2 — power cycling on timer relay (Score: 0.90)
  Causal_Intervention: do(check_timer_relay) → P(EC_normal | do(fix)) = 0.91
  Bayesian_Confidence: 0.87 posterior [CI: 0.79–0.93], updated from 0.50 prior
  Meta_Cognitive_Events: none
</Reasoning_Trace>
```

---

## 🏗️ Repository Structure

```
integrated-cognitive-reasoning-engine/
├── SKILL.md                   # Agent Skills spec — main skill definition
├── LICENSE                    # MIT License
├── references/
│   └── REFERENCE.md           # Full mathematical derivations & theory
└── assets/
    └── hero.jpg               # Architecture infographic
```

---

## 🔌 Platform Compatibility

| Platform | Status | Notes |
|---|---|---|
| Claude Code | ✅ | Native Agent Skills support |
| Cursor | ✅ | Native Agent Skills support |
| Gemini CLI | ✅ | Native Agent Skills support |
| GitHub Copilot | ✅ | Native Agent Skills support |
| Roo Code | ✅ | Native Agent Skills support |
| VS Code (Copilot) | ✅ | Native Agent Skills support |
| OpenAI Codex | ✅ | Native Agent Skills support |
| LangChain / LangGraph | ⚙️ | Each module = one graph node |
| Home Assistant AI | ⚙️ | Use as conversation agent config |
| Open WebUI | ⚙️ | Paste into Modelfile system prompt |

---

## 🧪 Ideal Use Cases

- **IoT & Sensor Systems** — diagnosing noisy or conflicting sensor streams
- **Hydroponic / Agricultural AI** — multi-variable grow environment decisions
- **Robotics Fault Diagnosis** — root cause analysis of hardware anomalies
- **Safety-Critical Reasoning** — any domain where wrong conclusions have real consequences
- **BCI / EEG Data** — probabilistic interpretation of ambiguous neural signals
- **General Debugging** — structured analysis of any system exhibiting unexpected behavior

---

## 📚 References

- Pearl, J. (2009). *Causality: Models, Reasoning, and Inference*. Cambridge University Press.
- Jeffrey, R. (1965). *The Logic of Decision*. McGraw-Hill.
- Peirce, C.S. (1883). *A Theory of Probable Inference*.
- Marcus, G. & Davis, E. (2019). *Rebooting AI*. Pantheon.
- IJCAI 2025: *Neuro-Symbolic AI: Towards Improving LLM Reasoning*.
- NeurIPS 2024: *Unveiling Causal Reasoning in Large Language Models*.

---

## 📄 License

MIT © 2026 [ohrbit](https://github.com/ohrbit)

---

<p align="center">
  <sub>Built with ❤️ as an open-source Agent Skill — compatible with the <a href="https://agentskills.io">agentskills.io</a> open standard</sub>
</p>
