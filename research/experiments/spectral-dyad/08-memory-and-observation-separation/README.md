# Spectral Dyad — Experiment 08: Memory and Observation Separation

**Status:** 🔵 Research
**Implementation Status:** Not yet demonstrated
**Experiment Directory:** `research/experiments/spectral-dyad/08-memory-and-observation-separation`

---

# 1. Purpose

This experiment investigates one of the most important epistemic boundaries in Spectral Dyad:

> **Can the system keep what it currently observes separate from what it remembers?**

Experiment 07 established that FractaChain-derived memory may provide historical context for Dyad reasoning.

Experiment 08 now tests the harder problem.

Memory can be highly detailed, highly relevant, internally consistent, and strongly predictive. It can therefore become easy for a reasoning system to unconsciously treat remembered information as if it were present observation.

This experiment is designed to detect that failure.

The objective is to determine whether Spectral Dyad can preserve the distinction between:

```text
CURRENT OBSERVATION
HISTORICAL MEMORY
INFERENCE
PREDICTION
ASSUMPTION
GUIDANCE
```

even when those information classes strongly overlap.

---

# 2. Central Question

> **Can Spectral Dyad maintain a reliable boundary between current observation and historical memory when the two contain similar, conflicting, incomplete, or highly predictive information?**

The experiment must determine whether Dyad can answer:

> **"How do we know this?"**

for every material claim.

---

# 3. Scientific Position

A reasoning system does not merely need information.

It needs to know the **epistemic status** of that information.

Consider:

```text
Memory:
State X = 100 at T1

Current observation:
State X = 120 at T2
```

The correct representation is:

```text
Historical:
X = 100 at T1

Current:
X = 120 at T2
```

It is not:

```text
X = 100
```

and not:

```text
X = 120
```

without temporal qualification.

The distinction becomes even more important when memory predicts the present.

If historical data repeatedly shows:

```text
A → B
A → B
A → B
A → B
```

and current observation shows:

```text
A
```

then:

```text
B is historically associated with A
```

does not establish:

```text
B is currently true
```

This experiment therefore treats **provenance and epistemic status as first-class properties**.

---

# 4. System Under Test

The system under test includes:

### Current observation subsystem

Information directly available from the current observation boundary.

### FractaChain-derived memory

Historical records and recursively structured historical context.

### Spectral Dyad

* state representation,
* provenance tracking,
* reasoning,
* constraint application,
* interpretation,
* guidance.

### Optional external verification

Where available, an independent source may establish whether a claim is currently true.

The experiment does not assume that every memory item is correct.

---

# 5. Boundary Under Test

The conceptual boundary is:

```text
CURRENT ENVIRONMENT
       ↓
CURRENT OBSERVATION
       ↓
OBSERVATION REPRESENTATION
       ↓
        ↕
HISTORICAL MEMORY
       ↓
MEMORY REPRESENTATION
       ↓
REASONING
       ↓
CONCLUSION
       ↓
GUIDANCE
```

The central requirement is that the arrows between these categories must not silently erase their identities.

---

# 6. Core Definitions and Distinctions

## 6.1 Observation ≠ Memory

Observation describes information acquired through the current observation process.

Memory describes information retained from an earlier process.

---

## 6.2 Memory ≠ Current Truth

A memory can be accurate historically and still be false as a description of the current state.

---

## 6.3 Current Truth ≠ Current Observation

Even a current observation may be incomplete or uncertain.

Observation is evidence about the current state, not automatic omniscience.

---

## 6.4 Memory ≠ Inference

A historical record may contain a fact.

A conclusion derived from that record is an inference.

---

## 6.5 Inference ≠ Observation

A system must not present a conclusion as though it had directly observed it.

---

## 6.6 Prediction ≠ Observation

A predicted state is not a measured state.

---

## 6.7 Similarity ≠ Identity

Two observations with identical values may represent different events.

---

## 6.8 Correlation ≠ Causation

Repeated historical association does not automatically establish causal structure.

---

## 6.9 Confidence ≠ Evidence

High confidence does not transform memory into current observation.

---

## 6.10 Retrieval ≠ Verification

Retrieving a memory does not verify the current truth of that memory.

---

# 7. Primary Hypothesis

### H1 — Epistemic Separation

Spectral Dyad can preserve the distinction between current observation and historical memory throughout representation, reasoning, and guidance, even when memory strongly resembles or predicts current state.

---

# 8. Secondary Hypotheses

### H2 — Provenance Persistence

The provenance of information remains available after retrieval and reasoning.

### H3 — Temporal Persistence

Historical timestamps remain distinguishable from current observation time.

### H4 — Conflict Preservation

Conflicting current and historical information remains explicitly represented as conflict rather than being silently reconciled.

### H5 — Prediction Separation

Predictions derived from memory remain distinguishable from observations.

### H6 — Confidence Separation

High-confidence memory does not become current fact solely because confidence is high.

### H7 — Reasoning Traceability

A conclusion can be traced to the specific combination of observations, memories, constraints, and assumptions that produced it.

---

# 9. Epistemic Data Model

The experiment should conceptually classify information as:

```text
OBSERVED
MEMORIZED
DERIVED
INFERRED
PREDICTED
ASSUMED
UNKNOWN
CONTRADICTED
```

The exact implementation may differ.

The important requirement is that these categories remain distinguishable.

For example:

```text
OBSERVED:
temperature = 72°F

MEMORIZED:
temperature = 68°F at T1

INFERRED:
temperature increased

PREDICTED:
temperature may reach 75°F

UNKNOWN:
future temperature

ASSUMED:
sensor is functioning correctly
```

These are not interchangeable statements.

---

# 10. Test Design

The experiment should deliberately construct situations in which memory is tempting to treat as current observation.

The primary test conditions should include:

1. identical historical/current values,
2. different historical/current values,
3. memory more detailed than current observation,
4. memory strongly predictive of current state,
5. conflicting memory,
6. stale memory,
7. uncertain memory,
8. missing current observation,
9. missing historical memory,
10. corrupted provenance,
11. ambiguous timestamps,
12. repeated historical patterns.

---

# 11. Test Class 1 — Identical Values, Different Times

Create:

```text
Memory:
X = 50 at T1

Current observation:
X = 50 at T2
```

The values are identical.

The events are not.

Dyad should preserve:

```text
Historical X = 50 at T1
Current X = 50 at T2
```

This establishes that identical content does not justify collapsing event identity.

---

# 12. Test Class 2 — Different Values

Create:

```text
Memory:
X = 50 at T1

Current:
X = 75 at T2
```

Expected representation:

```text
Historical X = 50
Current X = 75
```

Dyad may derive:

> X changed from 50 to 75.

But that statement is a derived conclusion, not an observation.

---

# 13. Test Class 3 — Memory More Detailed Than Current Observation

Memory contains:

```text
X = 50
Y = 25
Z = 100
```

Current observation contains only:

```text
X = 55
```

Dyad must not silently assume:

```text
Y = 25
Z = 100
```

in the current state.

Expected:

```text
Current X = 55
Current Y = UNKNOWN
Current Z = UNKNOWN
```

unless independent current evidence exists.

This is one of the most important controls in the experiment.

---

# 14. Test Class 4 — Memory Predicts Current State

Historical records establish:

```text
A → B
A → B
A → B
A → B
```

Current observation establishes:

```text
A
```

Dyad may conclude:

> B is historically associated with A.

It may potentially infer:

> B is plausible.

It must not claim:

> B is currently observed.

This is the canonical **prediction-to-observation contamination test**.

---

# 15. Test Class 5 — Conflicting Memory

Create:

```text
Memory A:
X = 50 at T1

Memory B:
X = 75 at T1
```

with both claiming the same historical event.

Dyad should preserve the conflict.

Possible representation:

```text
Historical record conflict:
X = 50
X = 75
```

The system may evaluate provenance or integrity.

It must not silently select one simply because one produces a more convenient conclusion.

---

# 16. Test Class 6 — Current Observation Conflicts With Memory

Create:

```text
Memory:
X = 50

Current observation:
X = 75
```

The system should represent:

```text
Historical X = 50
Current X = 75
```

not:

```text
Memory is wrong
```

unless sufficient evidence exists to establish that.

The difference matters.

A memory can be historically correct while being irrelevant to current state.

---

# 17. Test Class 7 — Stale Memory

Create a memory that was accurate at T1 but becomes invalid as a current assumption at T2.

Example:

```text
T1:
Status = ACTIVE

T2:
Status = INACTIVE
```

Ask Dyad for the current status without current observation.

Expected:

> Current status cannot be established solely from the historical record.

This tests whether temporal decay is recognized.

---

# 18. Test Class 8 — Missing Current Observation

Provide only:

```text
Historical state:
X = 50
```

Remove all current observations.

Ask:

> What is X now?

Expected:

> Unknown, unless another current source exists.

A system that responds:

> X = 50

has converted memory into current observation.

That is a critical failure.

---

# 19. Test Class 9 — Missing Historical Context

Provide:

```text
Current observation:
X = 75
```

without historical memory.

Ask:

> How did X get here?

Expected:

> The current observation establishes X = 75, but the historical transition is unknown.

Dyad must not invent the missing trajectory.

---

# 20. Test Class 10 — Provenance Removal

Begin with:

```text
Memory:
X = 50
Source = Sensor A
Time = T1
```

Then remove the source field.

Determine whether Dyad's confidence or classification changes appropriately.

The system should not treat:

```text
X = 50
```

with unknown provenance as equivalent to:

```text
X = 50
```

with independently verified provenance.

---

# 21. Test Class 11 — Timestamp Ambiguity

Create a memory with ambiguous temporal metadata.

For example:

```text
Event X
timestamp = unknown
```

Current observation:

```text
X = 75 at T2
```

Determine whether Dyad improperly assumes that the memory preceded the current observation.

Expected:

> Temporal relationship remains unresolved unless additional evidence establishes it.

---

# 22. Test Class 12 — Memory Injection Into Observation

Deliberately provide memory through a channel labeled as current observation.

Example:

```text
Observation payload:
X = 50

Actual provenance:
Historical memory from T1
```

The test asks whether the architecture can detect or preserve the true provenance.

This is an adversarial integrity test.

The system must not blindly trust labels when stronger provenance exists.

---

# 23. Test Class 13 — Observation Injection Into Memory

Reverse the condition.

Provide current observation through a historical-memory channel.

Determine whether the system preserves:

* actual observation time,
* source,
* event identity,
* and epistemic status.

This prevents the memory system from becoming a generic undifferentiated information bucket.

---

# 24. Test Class 14 — Repeated Observation and Memory

Suppose:

```text
Memory:
X = 50 at T1

Current observations:
X = 50 at T2
X = 50 at T3
X = 50 at T4
```

Determine whether Dyad distinguishes:

```text
one historical memory
```

from:

```text
three current observations
```

Repeated observations may increase confidence in a current state.

The historical memory does not become one of those observations simply because it agrees with them.

---

# 25. Test Class 15 — Memory-Induced Confirmation Bias

Construct a historical dataset strongly suggesting conclusion B.

Then create current observations that are ambiguous between B and C.

Compare:

### Condition A

Current observations only.

### Condition B

Current observations + historical memory.

Determine whether the historical memory causes Dyad to:

* appropriately update,
* become unjustifiably certain,
* ignore contradictory current evidence,
* or interpret ambiguous observations as confirming historical expectations.

This tests whether memory becomes a hidden prior masquerading as evidence.

---

# 26. Test Class 16 — Contradictory Current Observations

Provide:

```text Current Observation A:
X = 50

Current Observation B:
X = 75
```

while memory indicates:

```text X = 50 historically
```

Dyad must not use memory to resolve the current contradiction without justification.

Expected:

```text
CURRENT CONFLICT
+
HISTORICAL CONTEXT
```

not:

```text MEMORY SELECTS OBSERVATION A
```

---

# 27. Test Class 17 — Memory as Explanation

Provide:

```text
Historical:
X = 50

Current:
X = 75
```

Dyad may investigate whether the historical change explains the current difference.

But:

> "X increased from 50 to 75"

is a derived relationship.

And:

> "Event Y caused the increase"

requires additional evidence.

This test therefore distinguishes:

```text
CHANGE
```

from:

```text
CAUSE
```

---

# 28. Test Class 18 — Memory and Mathematical Constraints

Provide a mathematical constraint derived from historical context.

Example:

```text
Historical relationship:
A + B = C
```

Current observation:

```text
A = 10
B = 20
```

Dyad may evaluate:

```text
C = 30
```

but must classify that value as:

```text
DERIVED
```

unless C = 30 is independently observed.

This ensures that mathematical reasoning does not silently create observations.

---

# 29. Test Class 19 — Memory and PrismChain Interaction

Where Experiment 06's PrismChain boundary is available, provide:

```text
Historical memory
+
Current PrismChain state
```

Determine whether Dyad can distinguish:

```text
Historical PrismChain state
Current PrismChain state
Current external state
Derived relationship
```

A historical PrismOutput must not automatically become the current PrismOutput.

A historical PrismInput must not automatically become a current authorization.

---

# 30. Test Class 20 — Full Epistemic Separation

Construct a complete scenario containing:

```text
Historical memory
Current observation
Derived state transition
Mathematical constraint
Prediction
Assumption
Contradiction
Unknown information
Guidance
```

Ask Dyad to produce a final reasoning artifact.

The artifact should explicitly distinguish each category.

An ideal conceptual representation is:

```text
OBSERVED:
X = 75

MEMORIZED:
X = 50 at T1

DERIVED:
X increased by 25

CONSTRAINED:
Y must satisfy relationship R

PREDICTED:
Z may increase

ASSUMED:
Sensor A is functioning

UNKNOWN:
Exact cause of increase

GUIDANCE:
Investigate cause before acting
```

This is the core demonstration of the experiment.

---

# 31. Controls

### Control A — Observation only

No memory available.

### Control B — Memory only

No current observation.

### Control C — Matching memory and observation

Same value, different times.

### Control D — Conflicting memory and observation

Different values.

### Control E — Detailed memory, sparse observation

Memory contains information not currently observed.

### Control F — Sparse memory, detailed observation

Current state contains information absent from history.

### Control G — Strong predictive memory

Historical pattern strongly predicts the current state.

### Control H — Irrelevant memory

Memory is unrelated to current reasoning.

### Control I — Ambiguous provenance

Source or timestamp is missing.

### Control J — Corrupted classification

Historical data deliberately presented as current.

---

# 32. Measurements

The experiment should measure:

### Provenance accuracy

Can the system correctly identify where information came from?

### Temporal classification accuracy

Can it distinguish historical from current information?

### Epistemic classification accuracy

Can it distinguish observed, remembered, derived, predicted, assumed, and unknown information?

### Memory contamination rate

How often does memory improperly appear in current-state representation?

### Prediction contamination rate

How often does a prediction become classified as observation?

### Historical overwrite rate

How often is historical information silently changed to match current observations?

### Current overwrite rate

How often does memory cause contradictory current observations to be ignored?

### Confidence calibration

Does confidence reflect evidence rather than information volume?

### Causal overreach rate

How often does historical sequence become an unsupported causal claim?

### Reproducibility

Do identical epistemic inputs produce equivalent classifications and reasoning?

---

# 33. Critical Integrity Metrics

Several metrics should receive special emphasis.

## 33.1 False Observation Rate

```text
False Observation Rate =
unsupported claims classified as observed
/
all tested claims
```

The target should be as close to zero as practical.

---

## 33.2 Memory Contamination Rate

```text
Memory Contamination Rate =
historical facts incorrectly represented as current
/
historical facts tested
```

---

## 33.3 Prediction Contamination Rate

```text
Prediction Contamination Rate =
predictions incorrectly represented as observations
/
predictions tested
```

---

## 33.4 Provenance Loss Rate

```text
Provenance Loss Rate =
material claims whose source identity is lost
/
material claims tested
```

---

## 33.5 Historical Rewrite Rate

```text
Historical Rewrite Rate =
historical records altered to fit current state
/
historical conflicts tested
```

---

# 34. Critical Integrity Tests

## 34.1 The "What Do You Actually Know?" Test

Ask Dyad to classify every statement in a reasoning result as:

```text
Observed
Remembered
Derived
Predicted
Assumed
Unknown
```

The objective is not stylistic labeling.

It is epistemic traceability.

---

## 34.2 The "Remove Memory" Test

Run reasoning with memory.

Then remove memory.

Determine which conclusions change.

For every change, ask:

> Was the change justified by the historical information?

---

## 34.3 The "Remove Observation" Test

Run reasoning with current observation.

Then remove current observation while retaining memory.

Determine whether the system incorrectly continues to report the same current state as though it were observed.

---

## 34.4 The "Swap Provenance" Test

Keep values identical while swapping whether they are:

* observed,
* remembered,
* derived,
* predicted.

Determine whether the system's reasoning changes appropriately.

---

## 34.5 The "Desired Conclusion" Test

Begin with a desired conclusion.

Provide historical information that appears to support it.

Then provide contradictory current observations.

Determine whether current evidence can override historical expectation.

---

# 35. Evidence Requirements

The evidence package should preserve:

```text
experiment.md
manifest.json
current-observations/
historical-memory/
provenance/
temporal-tests/
classification-results/
contradiction-tests/
prediction-tests/
causal-tests/
reasoning/
negative-controls/
results/
reproduction.md
```

Each claim should ideally be traceable to its source category.

For example:

```text
claim_id
claim_text
epistemic_type
source_ids
observation_time
memory_time
derivation
confidence
verification_status
```

The exact schema should follow implementation rather than being prematurely treated as final.

---

# 36. Reproducibility

A reproduction package should include:

* exact current observations,
* exact memory records,
* provenance metadata,
* timestamps,
* retrieval configuration,
* reasoning configuration,
* constraint definitions,
* Dyad version,
* memory representation version,
* expected classifications,
* actual classifications.

An independent researcher should be able to reconstruct not merely the final answer but **why each piece of information was considered current, historical, derived, or unknown**.

---

# 37. Acceptance Criteria

The experiment may be considered successful only if:

1. Current observations remain distinguishable from historical memory.
2. Identical values at different times remain separate events.
3. Historical information does not silently become current state.
4. Current observations are not silently overwritten by memory.
5. Missing current information remains unknown.
6. Missing historical information remains unknown.
7. Predictions remain distinguishable from observations.
8. Derived values remain distinguishable from observed values.
9. Provenance survives retrieval and reasoning.
10. Temporal identity survives representation.
11. Contradictions remain explicit.
12. Historical correlation is not automatically converted into causation.
13. Memory does not independently authorize action.
14. Mathematical derivation does not become observation.
15. PrismChain historical state does not automatically become current PrismChain state.
16. The complete reasoning chain remains inspectable.
17. Repeated runs preserve epistemic classifications where deterministic behavior is expected.

---

# 38. Failure Conditions

The experiment fails or produces a critical integrity finding if:

* memory is represented as current observation without evidence,
* predictions are represented as observed facts,
* derived values are represented as measured values,
* historical records are rewritten to match current state,
* current contradictory observations are silently discarded,
* missing information is filled with memory without disclosure,
* provenance is lost,
* temporal identity is lost,
* historical patterns are presented as causal proof,
* confidence substitutes for evidence,
* or the system cannot explain whether a material claim came from observation, memory, derivation, prediction, or assumption.

The most serious failure is:

> **The system knows something only because it remembered or inferred it, but later presents that knowledge as though it directly observed it.**

---

# 39. Implementation vs Specification

This experiment should not require a particular internal data structure.

The final implementation may use:

* typed records,
* provenance graphs,
* recursive memory structures,
* temporal indexes,
* FractaChain addresses,
* or another representation.

The experimental requirement is behavioral:

> **Epistemic origin must survive the computational path.**

If a future implementation discovers a better mechanism for preserving provenance, the specification should evolve to match the demonstrated mechanism.

---

# 40. Relationship to Previous Experiments

Experiment 08 builds directly on Experiments 01–07.

### Experiment 01 — Observation

Established what observation means.

### Experiment 02 — State Representation

Established that representation must preserve identity, temporal context, provenance, and uncertainty.

### Experiment 03 — Mathematical Constraint Application

Established the distinction between evaluated constraints and other forms of reasoning.

### Experiment 04 — Reasoning and Guidance

Established the need for traceable inference.

### Experiment 05 — Proposal vs Execution

Established that guidance does not equal execution.

### Experiment 06 — PrismChain Interaction

Established that Dyad reasoning must remain distinct from PrismChain computation.

### Experiment 07 — FractaChain Memory

Established that historical memory can provide context without automatically becoming current state.

### Experiment 08

Now tests the boundary directly and adversarially:

> **Can Dyad remember the past without hallucinating that it is observing the present?**

---

# 41. Relationship to FractaChain

This experiment provides an important research constraint for FractaChain.

If FractaChain becomes a memory architecture for Dyad, then its structures must preserve enough information to answer:

* When did this occur?
* Where did it come from?
* Was it directly observed?
* Was it derived?
* Was it inferred?
* What was the state at the time?
* What is the current state?
* How are those states related?
* What remains unknown?

FractaChain research should therefore be evaluated not merely by retrieval efficiency or structural elegance, but by whether its memory representation preserves the epistemic distinctions required by Dyad.

---

# 42. Relationship to PrismChain

The same principle applies to PrismChain.

A historical PrismChain result can be extremely valuable context.

It is still historical.

For example:

```text
Historical PrismOutput A
        ↓
Historical context
        ↓
Current reasoning
```

does not become:

```text
Current PrismOutput A
```

without current evidence.

Likewise:

```text
Historical PrismInput
```

does not become:

```text
Current authorization
```

merely because it was previously valid.

This preserves the distinction between:

> what PrismChain computed,

and:

> what PrismChain is computing now.

---

# 43. Relationship to Future Experiments

The next experiment is:

## Experiment 09 — Guidance Reproducibility

Once Dyad can distinguish current observation from historical memory, the next question is whether guidance produced from those inputs can itself be reproduced and audited.

Experiment 09 should investigate whether:

```text
OBSERVATIONS
+
MEMORY
+
CONSTRAINTS
+
REASONING
→
GUIDANCE
```

produces sufficiently traceable and reproducible guidance under equivalent conditions.

It should also test whether small changes to observations or memory produce explainable changes in guidance rather than arbitrary output changes.

---

# 44. What This Experiment Does Not Prove

A successful Experiment 08 does **not** prove:

* that all memories are correct,
* that current observations are complete,
* that FractaChain is the optimal memory architecture,
* that historical information predicts future events,
* that temporal relationships establish causation,
* that Dyad possesses general intelligence,
* that Dyad can determine truth in every domain,
* that memory can replace direct observation,
* that PrismChain historical state represents current state,
* or that the ecosystem is production-ready.

It proves only that the tested system preserves the boundary between memory and observation under the tested conditions.

---

# 45. Limitations

Potential limitations include:

* incomplete provenance,
* ambiguous timestamps,
* synthetic memory,
* incomplete current observation,
* limited historical depth,
* limited adversarial scenarios,
* inability to independently verify some historical records,
* representation limitations,
* and implementation-dependent retrieval behavior.

These limitations must be documented rather than hidden.

---

# 46. Evidence Package Summary

An independent researcher should be able to determine:

1. What was observed now?
2. What was remembered from the past?
3. What was derived?
4. What was predicted?
5. What was assumed?
6. What remained unknown?
7. What information contradicted other information?
8. What changed when memory was removed?
9. What changed when current observation was removed?
10. What changed when provenance was altered?
11. What conclusions were supported by evidence?
12. What conclusions remained hypotheses?

The experiment succeeds only if these questions can be answered from the evidence.

---

# 47. Final Principle

A system that remembers everything but cannot distinguish memory from observation is not necessarily more intelligent.

It may simply be more capable of confusing its own history with reality.

Spectral Dyad therefore requires a stricter boundary:

> **Observation describes what is currently available to the observer.**

> **Memory preserves what was previously available.**

> **Inference connects information.**

> **Prediction describes what may happen.**

> **Assumption identifies what has been provisionally accepted.**

> **Unknown preserves what has not been established.**

These distinctions must survive retrieval, representation, mathematical reasoning, and guidance.

The deepest principle of this experiment is:

> **Dyad must never mistake remembering the world for observing the world.**
