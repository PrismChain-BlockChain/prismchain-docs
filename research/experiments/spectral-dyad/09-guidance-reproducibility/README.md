# Spectral Dyad — Experiment 09: Guidance Reproducibility

**Status:** 🔵 Research
**Implementation Status:** Not yet demonstrated
**Experiment Directory:** `research/experiments/spectral-dyad/09-guidance-reproducibility`

---

# 1. Purpose

This experiment investigates whether **Spectral Dyad guidance can be reproduced, traced, compared, and explained under equivalent conditions**.

Experiments 01–08 established progressively stronger boundaries around:

* observation,
* state representation,
* mathematical constraints,
* reasoning,
* proposal,
* PrismChain interaction,
* memory,
* and the separation between memory and current observation.

The next question is whether those inputs produce guidance that is itself sufficiently stable and reproducible to be treated as an auditable system output.

The purpose is not to require every form of guidance to be identical under every circumstance.

Some reasoning systems may intentionally incorporate uncertainty, alternative hypotheses, probabilistic ranking, or non-deterministic search.

Instead, the experiment asks:

> **When the information available to Dyad is equivalent, is the resulting guidance reproducible to the degree the system claims it should be?**

And when guidance changes:

> **Can the system identify what changed and why?**

---

# 2. Central Question

> **Can Spectral Dyad produce guidance that is reproducible and traceable under equivalent epistemic conditions, while producing explainable changes when observations, memory, constraints, or assumptions change?**

A successful result must establish both:

```text
EQUIVALENT INPUTS
        ↓
REPRODUCIBLE GUIDANCE
```

and:

```text
CONTROLLED INPUT CHANGE
        ↓
TRACEABLE GUIDANCE CHANGE
```

---

# 3. Scientific Position

Guidance is downstream of multiple information classes.

Conceptually:

```text
OBSERVATION
+
STATE REPRESENTATION
+
MEMORY
+
MATHEMATICAL CONSTRAINTS
+
REASONING
+
ASSUMPTIONS
        ↓
GUIDANCE
```

Therefore, guidance reproducibility cannot be evaluated merely by comparing final text.

The experiment must establish what information produced the guidance.

A guidance result that happens to be identical across two runs is not necessarily reproducible if the underlying reasoning paths differ unpredictably.

Likewise, different guidance does not automatically indicate failure if the inputs actually differed in a meaningful way.

The key question is:

> **Can the system account for the relationship between its epistemic inputs and its guidance output?**

---

# 4. System Under Test

The system under test includes:

### Spectral Dyad

* observation processing,
* state representation,
* memory/context integration,
* mathematical constraints,
* reasoning,
* guidance generation.

### Optional FractaChain memory

Where applicable:

* historical context,
* recursive relationships,
* provenance,
* temporal context.

### Optional PrismChain interaction

Where applicable:

* PrismInput proposals,
* PrismOutput interpretation,
* computational state.

The experiment does not require every subsystem to be implemented simultaneously.

Each test must identify exactly which components participate.

---

# 5. Boundary Under Test

The conceptual pipeline is:

```text id="5r7dqm"
OBSERVATION
      ↓
STATE REPRESENTATION
      ↓
MEMORY
      ↓
MATHEMATICAL CONSTRAINTS
      ↓
REASONING
      ↓
GUIDANCE
```

Where applicable:

```text id="4e8ykm"
GUIDANCE
      ↓
PROPOSAL
      ↓
PRISMINPUT
      ↓
PRISMCHAIN
```

The reproducibility experiment focuses primarily on the first pipeline.

The downstream execution boundary remains separate.

---

# 6. Core Definitions and Distinctions

## 6.1 Reproducibility ≠ Identical Wording

Two guidance outputs may use different language while expressing the same recommendation.

Semantic equivalence may therefore matter more than textual identity.

---

## 6.2 Determinism ≠ Reproducibility

A system may be nondeterministic internally but still reproducible within defined statistical bounds.

---

## 6.3 Same Input ≠ Same Environment

Identical explicit inputs may still produce different outputs if hidden state, model version, memory state, timestamps, randomness, or external data differ.

---

## 6.4 Guidance ≠ Truth

A reproducible recommendation can still be wrong.

Reproducibility establishes consistency, not correctness.

---

## 6.5 Guidance ≠ Execution

A reproducible recommendation does not establish that an action occurred.

---

## 6.6 Stable Output ≠ Valid Reasoning

A system can repeatedly produce the same incorrect answer.

The reasoning path must therefore also be evaluated.

---

## 6.7 Different Output ≠ Failure

If a controlled input change should change the guidance, different guidance may be evidence of correct sensitivity.

---

# 7. Primary Hypothesis

### H1 — Guidance Reproducibility

Given equivalent observations, memory, constraints, assumptions, configuration, and relevant system state, Spectral Dyad produces equivalent guidance within its declared reproducibility model.

---

# 8. Secondary Hypotheses

### H2 — Traceability

Guidance can be traced to the observations, memory, constraints, and assumptions that materially contributed to it.

### H3 — Controlled Sensitivity

Meaningful changes to material inputs produce explainable changes in guidance.

### H4 — Irrelevance Robustness

Changes to irrelevant information do not systematically alter guidance.

### H5 — Provenance Sensitivity

Changes to provenance or epistemic status can appropriately alter guidance where those changes materially affect confidence.

### H6 — Uncertainty Preservation

Uncertainty in upstream information remains represented in downstream guidance.

### H7 — Historical Reproducibility

Equivalent historical memory produces equivalent guidance under equivalent current conditions.

---

# 9. Reproducibility Classes

The experiment should distinguish several possible reproducibility models.

## 9.1 Exact Reproducibility

Same complete inputs produce the same output.

```text
X → Y
X → Y
X → Y
```

---

## 9.2 Semantic Reproducibility

Different wording expresses materially equivalent guidance.

```text
X → "Investigate A first."
X → "A should be investigated before proceeding."
```

These may be semantically equivalent.

---

## 9.3 Procedural Reproducibility

The same reasoning procedure produces the same decision structure even if final presentation differs.

---

## 9.4 Statistical Reproducibility

A nondeterministic system produces outputs within a defined distribution or acceptable range.

---

## 9.5 Conditional Reproducibility

Equivalent inputs under a specified environment reproduce equivalent guidance.

This may be the most realistic model for systems that depend on external state.

---

# 10. Test Design

The experiment should begin with a canonical reasoning scenario.

Record:

```text id="knq0l8"
Observation Set
Memory Set
Constraint Set
Assumption Set
Configuration
System Version
Environment
Randomness State
External Dependencies
```

Generate guidance.

Then repeat the experiment while changing one factor at a time.

This creates a controlled perturbation framework.

---

# 11. Test Class 1 — Exact Repetition

Run identical conditions multiple times.

Measure:

* textual equality,
* semantic equality,
* reasoning-path equality,
* confidence equality,
* recommendation equality.

If exact determinism is claimed, the expected result is identical output.

If exact determinism is not claimed, the system must specify the expected variability.

---

# 12. Test Class 2 — Semantic Reproducibility

Allow presentation differences while comparing the actual guidance.

For example:

```text id="r8m3yw"
"Investigate the state transition before acting."

"Determine the cause of the transition before proceeding."
```

These may represent the same guidance.

The experiment should therefore evaluate:

* action equivalence,
* priority equivalence,
* constraint equivalence,
* risk interpretation,
* confidence,
* and conditions.

Textual similarity alone is insufficient.

---

# 13. Test Class 3 — Reasoning Trace Reproducibility

Repeat the same scenario.

Compare:

```text id="0h5ylx"
observations used
memory used
constraints applied
assumptions invoked
intermediate conclusions
final conclusion
guidance
```

A reproducible final answer with materially different unsupported reasoning paths should be investigated.

---

# 14. Test Class 4 — Controlled Observation Change

Change exactly one material observation.

Example:

```text id="v8o5sp"
Run A:
X = 50

Run B:
X = 51
```

Determine:

* whether guidance changes,
* whether the change is directionally explainable,
* whether the magnitude of change is reasonable,
* whether the changed observation is actually relevant.

The objective is not to require a change every time.

The objective is to establish **sensitivity to meaningful information**.

---

# 15. Test Class 5 — Irrelevant Observation Change

Add or modify information that should not affect the reasoning.

Example:

```text id="l2ed2t"
Relevant:
X = 50

Irrelevant:
Y = 999
```

Determine whether guidance changes.

A system that changes dramatically because irrelevant information was added may have poor robustness.

---

# 16. Test Class 6 — Memory Perturbation

Run:

```text id="q9iyr7"
Current observation
+
Memory A
```

then:

```text id="e9xj7v"
Current observation
+
Memory B
```

where A and B differ by one historical fact.

Determine whether guidance changes only when that historical difference is relevant.

This connects directly to Experiments 07 and 08.

---

# 17. Test Class 7 — Memory Removal

Compare:

```text id="b3qzq1"
Current observation
+
Memory
```

with:

```text id="d4zyf6"
Current observation only
```

If guidance changes, identify exactly which historical fact caused the change.

If guidance does not change, determine whether that is expected because current evidence was sufficient.

---

# 18. Test Class 8 — Constraint Perturbation

Run identical observations with:

```text id="2dxk6c"
Constraint Set A
```

and:

```text id="t7f9pg"
Constraint Set B
```

where B changes one material constraint.

Measure whether guidance reflects the changed constraint.

This tests whether constraints are actually used rather than merely recorded.

---

# 19. Test Class 9 — Assumption Perturbation

Change one explicit assumption.

Example:

```text id="s5g0zz"
Assumption A:
Sensor is reliable.
```

versus:

```text id="k9e0f2"
Assumption B:
Sensor reliability is uncertain.
```

Determine whether guidance appropriately reflects the difference.

An assumption that materially changes guidance should be visible in the reasoning trace.

---

# 20. Test Class 10 — Uncertainty Perturbation

Change confidence or uncertainty in an upstream observation without changing its central value.

Example:

```text id="9c8c3q"
X = 50 ± 0.1
```

versus:

```text id="q7xvbn"
X = 50 ± 10
```

Determine whether guidance changes appropriately.

The objective is to test whether uncertainty survives into guidance rather than disappearing during reasoning.

---

# 21. Test Class 11 — Provenance Perturbation

Keep the observed value identical while changing its provenance.

Example:

```text id="l1p9fm"
Run A:
X = 50
Source = independently verified source
```

versus:

```text id="d8j1y7"
Run B:
X = 50
Source = unknown
```

Determine whether guidance appropriately reflects the difference in evidentiary quality.

This directly extends Experiment 08.

---

# 22. Test Class 12 — Temporal Perturbation

Keep the value unchanged but change its timestamp.

Example:

```text id="u7br2p"
X = 50 at T1
```

versus:

```text id="9s5g0d"
X = 50 at T2
```

Determine whether the temporal difference changes guidance when timing is relevant.

This tests whether Dyad treats time as meaningful context rather than decorative metadata.

---

# 23. Test Class 13 — Contradiction Perturbation

Run with:

```text id="a5y0tm"
Evidence A
```

then:

```text id="d8sk7e"
Evidence A
+
Contradictory Evidence B
```

Determine whether guidance:

* identifies the contradiction,
* reduces confidence,
* requests clarification,
* changes recommendation,
* or otherwise responds appropriately.

A contradiction that produces no change without justification should be investigated.

---

# 24. Test Class 14 — Missing Information

Remove one material piece of information.

Compare:

```text id="x9n7g0"
Complete information
```

with:

```text id="n6y1sp"
Same information minus one material field
```

Determine whether guidance appropriately reflects the increased uncertainty.

The system must not simply fill the missing information from memory or assumptions without disclosure.

---

# 25. Test Class 15 — Hidden State Detection

Repeat a supposedly identical experiment while changing one hidden variable:

* system time,
* memory version,
* configuration,
* model version,
* random seed,
* external state,
* retrieval ordering.

Determine whether output changes.

If it does, the hidden dependency must be identified.

This is a critical reproducibility test.

---

# 26. Test Class 16 — Randomness Control

If Dyad contains nondeterministic components, compare:

### Fixed seed

```text id="ld0j5e"
Seed = S
```

### Different seed

```text id="4k4qjs"
Seed = T
```

Determine whether:

* identical seeds reproduce,
* different seeds produce expected variability,
* semantic guidance remains stable where it should,
* and randomness is recorded.

---

# 27. Test Class 17 — Retrieval Variability

Where FractaChain memory retrieval is nondeterministic or ranked, repeat retrieval.

Measure:

* retrieved records,
* ranking,
* missing records,
* downstream guidance,
* confidence changes.

The experiment should determine whether retrieval variability creates unjustified guidance variability.

---

# 28. Test Class 18 — Guidance Stability Near Boundaries

Construct a case close to a decision boundary.

Example:

```text id="19d5bd"
Condition A:
risk = 0.49

Condition B:
risk = 0.51
```

Determine whether a small meaningful change causes:

* an appropriate decision change,
* an inappropriate large discontinuity,
* or no change when a change is expected.

This tests sensitivity near critical thresholds.

---

# 29. Test Class 19 — Guidance Under Equivalent Representations

Represent the same underlying observation in different valid forms.

For example:

```text id="cvk1x8"
Representation A:
50 units
```

and:

```text id="8p6w3j"
Representation B:
5 × 10 units
```

or other mathematically equivalent representations appropriate to the domain.

Determine whether guidance remains equivalent.

This tests whether representation details improperly dominate reasoning.

---

# 30. Test Class 20 — End-to-End Guidance Reproduction

Construct a complete scenario:

```text id="8e1yqf"
CURRENT OBSERVATION
      ↓
STATE REPRESENTATION
      ↓
FRACTACHAIN MEMORY
      ↓
MATHEMATICAL CONSTRAINTS
      ↓
REASONING
      ↓
GUIDANCE
```

Run the complete process independently multiple times.

Compare:

* inputs,
* provenance,
* reasoning,
* conclusion,
* guidance,
* uncertainty,
* and final recommendation.

This is the primary demonstration of the experiment.

---

# 31. Controls

### Control A — Exact duplicate run

All variables identical.

### Control B — One material observation changed

Tests expected sensitivity.

### Control C — One irrelevant observation changed

Tests robustness.

### Control D — One memory record removed

Tests memory dependence.

### Control E — One irrelevant memory record added

Tests memory contamination.

### Control F — One constraint changed

Tests constraint sensitivity.

### Control G — One assumption changed

Tests assumption sensitivity.

### Control H — Provenance degraded

Tests evidence-quality sensitivity.

### Control I — Uncertainty increased

Tests uncertainty propagation.

### Control J — Hidden variable changed

Tests hidden dependencies.

---

# 32. Measurements

The experiment should measure:

### Exact reproducibility

Percentage of identical outputs under exact repeated conditions.

### Semantic reproducibility

Percentage of outputs expressing equivalent guidance.

### Reasoning reproducibility

Consistency of material reasoning steps.

### Traceability

Percentage of guidance claims traceable to input evidence.

### Sensitivity

Response to controlled material changes.

### Robustness

Stability under irrelevant changes.

### Uncertainty propagation

Whether increased upstream uncertainty produces appropriate downstream uncertainty.

### Provenance sensitivity

Whether evidentiary quality affects guidance appropriately.

### Hidden dependency rate

Frequency of unexplained output changes under nominally identical conditions.

### Retrieval sensitivity

Effect of memory retrieval variation on guidance.

### Contradiction response

Whether conflicting evidence changes or qualifies guidance appropriately.

---

# 33. Guidance Equivalence

The experiment should define equivalence before evaluating results.

At minimum, compare:

### Action

What does Dyad recommend doing?

### Priority

What should happen first?

### Conditions

Under what conditions does the guidance apply?

### Constraints

What must not be violated?

### Confidence

How strongly is the guidance supported?

### Uncertainty

What remains unresolved?

Two outputs with different prose but identical answers to these questions may be semantically equivalent.

---

# 34. Critical Integrity Tests

## 34.1 Same Inputs, Different Guidance

Run exact duplicates.

If guidance differs materially, determine why.

Potential explanations include:

* randomness,
* hidden state,
* retrieval variability,
* external state,
* model version,
* undocumented assumptions.

If none can explain the difference, the result is a reproducibility failure.

---

## 34.2 Different Inputs, Same Guidance

Change a material input.

If guidance does not change, determine whether the input genuinely should have mattered.

This prevents the system from appearing stable simply because it ignores meaningful information.

---

## 34.3 Irrelevant Input Changes Guidance

Change information known to be irrelevant.

If guidance changes materially, investigate contamination.

---

## 34.4 Uncertainty Disappears

Increase uncertainty in a critical observation.

If guidance becomes equally confident without justification, uncertainty propagation has failed.

---

## 34.5 Provenance Disappears

Replace verified evidence with unknown-source evidence.

If guidance remains identical where provenance materially matters, investigate.

---

## 34.6 Reasoning Path Changes Without Input Change

If the final guidance is unchanged but the reasoning path changes substantially under identical conditions, determine whether the system is genuinely reproducible or merely producing the same endpoint through unstable reasoning.

---

# 35. Evidence Requirements

A reproducible evidence package should contain:

```text id="s0i0hb"
experiment.md
manifest.json
inputs/
observations/
memory/
constraints/
assumptions/
reasoning/
guidance/
perturbations/
controls/
reproducibility-runs/
comparisons/
results/
reproduction.md
```

The manifest should identify, where applicable:

```text id="h0u3ec"
dyad_version
memory_version
constraint_version
configuration
environment
timestamp
random_seed
external_dependencies
input_hashes
output_hashes
```

---

# 36. Reproducibility Manifest

A particularly important artifact should be the **reproducibility manifest**.

Conceptually:

```text id="d3k0mz"
RUN ID
SYSTEM VERSION
MEMORY VERSION
CONFIGURATION
INPUT SET
CONSTRAINT SET
ASSUMPTION SET
RANDOMNESS
ENVIRONMENT
EXTERNAL DEPENDENCIES
EXPECTED REPRODUCIBILITY CLASS
ACTUAL RESULT
```

This allows an independent researcher to determine whether two runs were genuinely equivalent.

---

# 37. Acceptance Criteria

The experiment may be considered successful only if:

1. Equivalent conditions produce equivalent guidance under the declared reproducibility model.
2. Material input changes can produce explainable guidance changes.
3. Irrelevant changes do not systematically distort guidance.
4. Memory perturbations have measurable and explainable effects where relevant.
5. Constraint changes produce appropriate guidance changes.
6. Assumption changes are visible in reasoning.
7. Uncertainty propagates into guidance.
8. Provenance differences can affect guidance when materially relevant.
9. Contradictions are preserved and appropriately reflected.
10. Hidden dependencies can be identified or explicitly declared.
11. Randomness is controlled or measured where present.
12. Reasoning and guidance remain traceable to their inputs.
13. Reproducibility claims are explicitly bounded.
14. Guidance remains distinguishable from execution.
15. The evidence package permits independent reproduction.

---

# 38. Failure Conditions

The experiment fails or produces a critical integrity finding if:

* identical conditions produce materially different guidance without explanation,
* materially different inputs produce identical guidance because relevant information was ignored,
* irrelevant information systematically changes guidance,
* uncertainty disappears during reasoning,
* provenance is discarded when materially relevant,
* contradictions are silently resolved,
* hidden state materially affects guidance without disclosure,
* random behavior is presented as deterministic,
* reasoning cannot be traced to available evidence,
* or reproducibility is claimed more strongly than the evidence supports.

A particularly serious failure is:

> **The system produces stable guidance that cannot be reproduced or explained from the information that was supposedly available to it.**

That would create the appearance of reliability without demonstrable reliability.

---

# 39. Implementation vs Specification

This experiment must not prematurely assume that Dyad is deterministic.

The implementation may ultimately use:

* deterministic rules,
* probabilistic reasoning,
* search,
* learned models,
* stochastic sampling,
* recursive memory retrieval,
* or combinations of these.

The experimental requirement is instead:

> **The system must accurately state what kind of reproducibility it actually provides.**

If exact determinism is unavailable, the system should not claim exact determinism.

If statistical reproducibility is the appropriate property, the experiment should measure statistical reproducibility.

The evidence determines the claim.

---

# 40. Relationship to Previous Experiments

Experiment 09 builds directly on Experiments 01–08.

### Experiment 01 — Observation

Established what information Dyad receives.

### Experiment 02 — State Representation

Established how observations are preserved.

### Experiment 03 — Mathematical Constraint Application

Established explicit constraint evaluation.

### Experiment 04 — Reasoning and Guidance

Established the reasoning path from information to guidance.

### Experiment 05 — Proposal vs Execution

Established that guidance is not execution.

### Experiment 06 — PrismChain Interaction

Established the boundary between Dyad reasoning and PrismChain computation.

### Experiment 07 — FractaChain Memory

Established historical memory as contextual information.

### Experiment 08 — Memory and Observation Separation

Established that memory must not masquerade as current observation.

### Experiment 09

Now asks:

> **Can the resulting guidance itself be reproduced and audited?**

---

# 41. Relationship to FractaChain

FractaChain memory may become a major source of contextual information for Dyad.

Experiment 09 therefore provides an important constraint:

> Memory retrieval variability must not create unexplained reasoning variability.

If two equivalent memory states produce materially different guidance, the reason must be identifiable.

This may reveal important properties of:

* recursive retrieval,
* neighborhood selection,
* temporal weighting,
* historical relevance,
* geometric addressing,
* or memory compression.

These are research questions rather than established conclusions.

---

# 42. Relationship to PrismChain

Where Dyad guidance becomes a PrismInput proposal, the reproducibility boundary remains explicit:

```text id="9shxpk"
GUIDANCE
    ↓
PROPOSAL
    ↓
PRISMINPUT
    ↓
PRISMCHAIN
```

Reproducible guidance does not guarantee reproducible external execution.

Likewise:

```text id="8w8f1u"
PRISMOUTPUT
```

does not retroactively prove that Dyad's guidance was correct.

The evidence chain remains separate.

---

# 43. Relationship to Future Experiments

The next experiment is:

## Experiment 10 — Contradiction Handling

Experiment 09 establishes whether guidance can be reproduced and whether controlled changes produce explainable changes.

Experiment 10 should investigate what happens when the information available to Dyad is internally inconsistent.

The central challenge becomes:

```text id="h0t2s9"
OBSERVATION A
        +
OBSERVATION B
        +
MEMORY C
        +
CONSTRAINT D
```

where the available information cannot all simultaneously be satisfied.

The experiment should determine whether Dyad can preserve, identify, characterize, and reason through contradiction rather than silently selecting whichever information produces the preferred answer.

---

# 44. What This Experiment Does Not Prove

A successful Experiment 09 does **not** prove:

* that guidance is correct,
* that reasoning is complete,
* that Dyad is deterministic,
* that Dyad is generally intelligent,
* that FractaChain memory is correct,
* that PrismChain computation is correct,
* that guidance should always be followed,
* that guidance constitutes authorization,
* or that external execution will reproduce the recommendation.

It proves only the reproducibility and traceability properties demonstrated by the experiment.

---

# 45. Limitations

Potential limitations include:

* nondeterministic reasoning,
* stochastic retrieval,
* external state changes,
* model version changes,
* hidden configuration,
* incomplete provenance,
* semantic-equivalence measurement difficulties,
* subjective evaluation of guidance quality,
* and insufficient test diversity.

These limitations must be explicitly recorded.

---

# 46. Evidence Package Summary

An independent researcher should be able to answer:

1. Were the two runs actually equivalent?
2. What information did Dyad receive?
3. What memory was available?
4. What constraints were active?
5. What assumptions were active?
6. What randomness or hidden state existed?
7. What reasoning occurred?
8. What guidance was produced?
9. If guidance changed, what changed upstream?
10. If guidance did not change, should it have?
11. Were irrelevant inputs truly irrelevant?
12. Was uncertainty preserved?
13. Was provenance preserved?
14. Can the result be independently reproduced?

If these questions cannot be answered, the guidance cannot yet be considered adequately reproducible.

---

# 47. Final Principle

Reliability is not created merely by producing the same answer twice.

A system becomes scientifically reproducible when another researcher can determine:

> **what it was given, what it remembered, what assumptions it used, what constraints applied, what changed, what it concluded, and why the resulting guidance followed from those conditions.**

Spectral Dyad therefore should not merely produce guidance.

It should produce **auditable guidance**.

The governing principle is:

> **Equivalent evidence should produce equivalent guidance to the degree the system claims; meaningful changes in evidence should produce explainable changes in guidance.**

And:

> **Reproducibility is not proof that guidance is correct. It is proof that the system's behavior can be examined rather than merely observed.**
