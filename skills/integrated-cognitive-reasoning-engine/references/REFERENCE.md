# ICRE — Mathematical & Theoretical Reference
**Integrated Cognitive Reasoning Engine v1.0.0**
*Author: DOWNWIND LEE — License: MIT*

---

## Module 1 — Neurosymbolic Ingestion

### Theory
Neurosymbolic AI combines the pattern-recognition strength of neural networks
with the precision of symbolic logic. Pure LLMs are prone to hallucination
because they operate on statistical associations without hard logical
constraints. Neurosymbolic grounding adds a deterministic validation gate:
any extracted fact must satisfy strict logical predicates before advancing.

### Process
```
Raw Input → Neural Parsing → Semantic Token Extraction → Symbolic Predicate Mapping → Validation Gate
                                                                                            ↓
                                                                               PASS → Module 2
                                                                               FAIL → Request clarification
```

### Constraint Rule
For every extracted fact F with associated predicate P:
```
valid(F) ↔ P(F) = TRUE ∧ ¬contradiction(F, KB)
```
Where KB = current knowledge base. Any F where valid(F) = FALSE is flagged
and either discarded or escalated as an anomaly for Module 2.

---

## Module 2 — Abductive Anomaly Resolution

### Theory
Abductive reasoning selects the *most likely explanation* for an observation,
not the logically certain one. Formalized by C.S. Peirce: given an observation
O and a rule R ("if H then O"), abduce H as the best explanation.

The selection principle is **Inference to the Best Explanation (IBE)**,
constrained by Occam's Razor: prefer the hypothesis that is both sufficient
and minimal.

### Process
```
Anomaly Detected → Generate {H1, H2, ... Hn} → Score each Hi → Select H*
```

### Scoring Function
For each hypothesis Hi, compute:

```
Score(Hi) = ExplanatoryPower(Hi) / Complexity(Hi)
```

Select:
```
H* = argmax_i [ Score(Hi) ]
```

Where:
- **ExplanatoryPower**: fraction of observed anomalies explained by Hi
- **Complexity**: number of independent assumptions required by Hi

### Example (CHADD Grow context)
```
Observation: EC sensor drops to 0 every night at 23:00
H1: Sensor hardware failure         → Score = 0.4 / 1   = 0.40
H2: Power cycling on timer circuit  → Score = 0.9 / 1   = 0.90  ← H*
H3: Algae growth on probe           → Score = 0.5 / 2   = 0.25
→ Selected: H2 (power cycling). Intervention: check timer relay.
```

---

## Module 3 — Causal Modeling & Counterfactuals

### Theory
Correlation ≠ causation. Causal inference uses **Structural Causal Models
(SCMs)** — directed acyclic graphs (DAGs) where edges represent
cause → effect relationships, not statistical co-occurrence.

Developed by Judea Pearl, the **do-calculus** allows computing the effect
of an intervention (forcing a variable to a value) independent of
observational confounders.

### Core Formula
**Interventional probability:**
```
P(Y | do(X = x))
```
Read: "the probability of Y, given that we *force* X to value x"
— distinct from P(Y | X = x) which is purely observational.

### Counterfactual Query Structure
For any proposed action A:
```
1. Build causal DAG from known variables
2. Identify backdoor paths (confounders)
3. Block confounders via adjustment formula:
   P(Y | do(X)) = Σ_z P(Y | X, Z=z) · P(Z=z)
4. Compute counterfactual: "What would Y be if X had been different?"
```

### Example (IoT Sensor context)
```
DAG: [Temperature] → [CO2 Level] → [Plant Growth]
               ↘                  ↗
               [Humidity]

Query: do(reduce_humidity) → P(growth_increase | do(humidity=40%)) = 0.78
Confounders blocked: temperature controlled in adjustment.
```

---

## Module 4 — Virtual Bayesian Updating

### Theory
Standard Bayesian updating requires a hard observed event E to update
belief in hypothesis H:
```
P(H | E) = P(E | H) · P(H) / P(E)
```

However, sensor data is often **uncertain or noisy** — E is not cleanly
observed. **Jeffrey's Conditioning** (Richard Jeffrey, 1965) handles
this by allowing updates based on *probability distributions over evidence*
rather than hard facts.

### Jeffrey's Updating Rule
```
P_new(H) = Σ_i P(H | E_i) · P_virtual(E_i)
```

Where:
- **P(H | E_i)**: likelihood of H given each possible evidence state Ei
- **P_virtual(E_i)**: virtual (uncertain) probability assigned to each Ei
- The sum normalizes across all mutually exclusive evidence states

### Virtual Likelihood Ratio
For noisy sensor evidence, assign a **virtual likelihood ratio** λ:
```
λ = P(E | H_true) / P(E | H_false)
```
High λ → strong evidence. λ ≈ 1 → evidence is uninformative.

### Confidence Score Output
Always express posterior as a range, never a single point:
```
P_new(H) = 0.82  [95% CI: 0.74 – 0.89]
Updated from prior: 0.51 → posterior: 0.82
Evidence weight: λ = 6.4 (strong)
```

### Example (mmWave sensor context)
```
Prior: P(person_present) = 0.50
Sensor reading: noisy positive signal
P_virtual(signal_true) = 0.80, P_virtual(signal_false) = 0.20
P(present | signal_true)  = 0.92
P(present | signal_false) = 0.15

P_new(present) = (0.92 × 0.80) + (0.15 × 0.20)
              = 0.736 + 0.030 = 0.766

Posterior: 0.77 — moderate-high confidence, not binary assertion.
```

---

## Module 5 — Meta-Cognitive Oversight

### Theory
Meta-cognition is "thinking about thinking." In an LLM context, it means
the system monitors its own reasoning process for failure modes:
- **Hallucination**: generating plausible but unvalidated facts
- **Logic loops**: circular reasoning with no convergence
- **Overconfidence**: binary assertions without uncertainty accounting
- **Complexity explosion**: reasoning chain growing without bound

### Trigger Thresholds
```
PAUSE triggered if ANY of:
  - Reasoning depth > 8 nested steps without convergence
  - Contradiction detected between Module 1 output and Module 3 graph
  - Confidence score oscillates (Δ > 0.3 between consecutive updates)
  - Same hypothesis appears in >2 abductive cycles without resolution
```

### Recovery Protocol
```
1. HALT current reasoning thread
2. Snapshot current state (which module, which variable, what error)
3. Re-evaluate heuristic: is the framing of the problem correct?
4. Select alternative strategy (simplify DAG / request more data / escalate)
5. Document error signal: type, trigger, resolution chosen
6. RESUME from Module 1 with revised framing
```

### Error Signal Log Format
```xml
<Error_Signal>
  Type: logic_loop
  Triggered_at: Module 3 — causal graph cycle detected
  Variables_involved: [humidity, temperature, CO2]
  Resolution: simplified DAG, removed humidity↔temperature bidirectional edge
  Strategy_updated: true
</Error_Signal>
```

---

## Full Reasoning Trace Format

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

## References

- Pearl, J. (2009). *Causality: Models, Reasoning, and Inference*. Cambridge UP.
- Jeffrey, R. (1965). *The Logic of Decision*. McGraw-Hill.
- Peirce, C.S. (1883). *A Theory of Probable Inference*.
- Marcus, G. & Davis, E. (2019). *Rebooting AI*. Pantheon.
- IJCAI 2025: *Neuro-Symbolic AI: Towards Improving LLM Reasoning*.
