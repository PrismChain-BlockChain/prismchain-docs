# Experiment 17 — Deterministic Computation

**Status:** 🟣 Experimental

**Evidence Program:** PrismChain Engineering Evidence Suite

**Position:** Experiment 17 of 20

---

# 1. Purpose

Experiment 17 tests whether PrismChain produces deterministic computational results when the same valid inputs, state, rules, and execution conditions are processed repeatedly.

Determinism is a foundational property for a system whose computation is represented through cryptographic artifacts.

If the same defined computational state can produce materially different results without an explicitly defined source of nondeterminism, then:

* commitments may differ,
* White Light Blocks may differ,
* PrismOutputs may differ,
* reproducibility may become difficult,
* verification becomes weaker,
* and downstream relationships may become ambiguous.

The purpose of this experiment is therefore not simply to run PrismChain twice.

It is to identify **exactly which inputs determine the result**, execute controlled repetitions, and determine whether equivalent computational conditions produce equivalent results.

---

# 2. Central Question

> **Given the same defined PrismInput, rules, computational state, and relevant execution conditions, does PrismChain produce the same seven-layer computation, White Light Block, and PrismOutput?**

The fundamental test is:

```text
SAME DEFINED INPUT
        ↓
SAME DEFINED STATE
        ↓
SAME DEFINED RULES
        ↓
SAME COMPUTATION
        ↓
SAME RESULT
```

Where a result is expected to be deterministic, repeated execution should produce the same relevant artifacts.

If differences occur, the experiment must identify why.

---

# 3. Architectural Principle

Determinism does not necessarily mean:

> Every byte produced by every component must always be identical.

Different timestamps, runtime metadata, logging information, process identifiers, or intentionally nondeterministic components may legitimately differ.

The experiment must therefore distinguish:

```text
COMPUTATIONAL DETERMINISM
```

from:

```text
RUNTIME IDENTITY
```

and:

```text
ARTIFACT BYTE-FOR-BYTE IDENTITY
```

The exact definition must be established for each tested artifact.

---

# 4. Determinism Model

The experiment begins by defining a computational input state.

Conceptually:

```text id="r0e9lf"
D = {
    PrismInput,
    native state,
    layer state,
    rules,
    configuration,
    relevant prior WLB state,
    execution conditions
}
```

The computation is:

```text id="4u4m9q"
RESULT = F(D)
```

A deterministic implementation should satisfy:

```text id="u7x5fb"
F(D) = F(D)
```

across independent executions, provided all inputs and relevant state are genuinely equivalent.

The experiment must determine what belongs inside `D`.

That question is part of the experiment.

---

# 5. Why Determinism Matters

Determinism supports:

* reproducibility,
* verification,
* debugging,
* independent testing,
* commitment stability,
* cross-node comparison,
* historical reconstruction,
* evidence generation,
* and scientific experimentation.

If a result cannot be reproduced from the same defined conditions, then the system must explain the source of variation.

A difference is not automatically a bug.

An unexplained difference is an important result.

---

# 6. Scope

Experiment 17 focuses on the PrismChain computational path:

```text id="4b8j8j"
PrismInput
   ↓
RED
   ↓
ORANGE
   ↓
YELLOW
   ↓
GREEN
   ↓
BLUE
   ↓
INDIGO
   ↓
VIOLET
   ↓
WHITE LIGHT BLOCK
   ↓
PrismOutput
```

Where supported by the current implementation, the experiment may extend into:

```text id="l4z4u9"
PrismOutput
   ↓
Rainbow Ring
```

However, the primary determinism claim concerns PrismChain computation and its direct output representation.

External blockchain behavior is not assumed to be deterministic merely because PrismChain's internal computation is.

---

# 7. Critical Distinctions

The experiment must preserve several distinctions.

### Determinism ≠ Immutability

A deterministic computation can produce different results when its input changes.

### Determinism ≠ Consensus

Deterministic execution does not establish external blockchain consensus.

### Determinism ≠ Finality

A deterministic result does not prove an external state is final.

### Determinism ≠ Correctness

A system can deterministically produce an incorrect result.

### Determinism ≠ Security

Deterministic behavior does not guarantee resistance to attack.

### Reproducibility ≠ Determinism

A process may be reproducible under a fixed environment without proving that every valid environment produces the same result.

---

# 8. Defining the Deterministic Input

Before testing, identify every input that can influence the result.

Candidate inputs include:

```text id="txrjti"
PrismInput
native state
normalized state
chain identity
state reference
authentication commitment
rules configuration
layer ordering
previous layer state
previous WLB hash
block number
computation parameters
execution conditions
software version
configuration version
serialization version
```

The actual implementation must determine which of these are computationally significant.

Do not assume that a field is irrelevant simply because it appears to be metadata.

---

# 9. Hidden Inputs

The experiment must specifically search for hidden sources of nondeterminism.

Examples include:

* system time,
* random number generators,
* operating-system randomness,
* process IDs,
* filesystem ordering,
* network responses,
* unordered dictionary iteration,
* concurrency,
* thread scheduling,
* floating-point behavior,
* environment variables,
* external API responses,
* machine-specific paths,
* locale,
* timezone,
* dependency versions,
* unpinned libraries.

A deterministic computation requires knowing which of these are actually capable of influencing the result.

---

# 10. Test A — Exact Repeat

Run the same computation twice using the same frozen input.

```text id="r5n4f0"
RUN A
   ↓
RESULT A

RUN B
   ↓
RESULT B
```

Compare:

* layer data,
* layer hashes,
* previous hashes,
* WLB contents,
* WLB hash,
* PrismOutput fields,
* commitments,
* serialized representations.

Record both exact equality and semantic equality.

---

# 11. Test B — Repeated Execution

Repeat the same frozen computation multiple times.

For example:

```text id="w8nq5d"
RUN 1
RUN 2
RUN 3
RUN 4
RUN 5
...
```

The number of repetitions must be defined before the final experiment report.

The purpose is to detect intermittent nondeterminism that two executions might miss.

---

# 12. Test C — Fresh Process Determinism

Do not merely execute the computation repeatedly inside the same process.

Start independent processes.

```text id="2cn7b1"
PROCESS A
   ↓
RESULT A

PROCESS B
   ↓
RESULT B
```

This helps identify hidden in-memory state.

---

# 13. Test D — Fresh Environment

Where practical, execute the same experiment from a clean environment.

Compare:

```text id="j0j2v0"
ENVIRONMENT A
ENVIRONMENT B
```

while keeping all intended computational inputs fixed.

Record:

* operating system,
* interpreter/compiler version,
* dependency versions,
* repository revision,
* configuration,
* runtime parameters.

The goal is not necessarily to prove universal cross-platform determinism.

The goal is to identify the environment boundary within which deterministic behavior is currently demonstrated.

---

# 14. Test E — Input Identity

Run the same input through the system multiple times.

Verify that the input commitment remains stable.

Conceptually:

```text id="r9s6x1"
PrismInput-A
    ↓
Commitment-A

PrismInput-A
    ↓
Commitment-A
```

If identical serialized inputs produce different commitments, investigate immediately.

---

# 15. Test F — Layer Determinism

Test each of the seven layers independently.

For each layer:

```text id="b1s5pd"
same layer input
      ↓
run 1
run 2
run 3
```

Compare:

* block number,
* data,
* previous hash,
* hash,
* serialization,
* metadata.

The experiment should distinguish intentional differences such as timestamps from actual computational differences.

---

# 16. Layer Determinism Matrix

| Layer  | Same Input | Same Computation | Same Result | Differences Explained |
| ------ | ---------: | ---------------: | ----------: | --------------------: |
| RED    |        Yes |           Record |      Record |                Record |
| ORANGE |        Yes |           Record |      Record |                Record |
| YELLOW |        Yes |           Record |      Record |                Record |
| GREEN  |        Yes |           Record |      Record |                Record |
| BLUE   |        Yes |           Record |      Record |                Record |
| INDIGO |        Yes |           Record |      Record |                Record |
| VIOLET |        Yes |           Record |      Record |                Record |

The final experiment report must replace these placeholders with actual observations.

---

# 17. Test G — WLB Determinism

Given the same seven valid layer artifacts and the same previous WLB state, produce the WLB repeatedly.

Conceptually:

```text id="5g7z8e"
LAYERS A-G
    ↓
WLB-1

LAYERS A-G
    ↓
WLB-2
```

Compare:

```text id="a9m9t1"
spectral_hashes
previous_hash
timestamp
data
hash
```

If timestamps are part of the WLB structure, determine whether timestamp normalization or freezing is required to make a meaningful deterministic comparison.

---

# 18. Timestamp Problem

The current PrismChain implementation contains timestamp-bearing artifacts.

Therefore the experiment must explicitly answer:

> Is time part of the computation, part of the artifact, or merely metadata?

Three possible cases exist.

### Case 1 — Timestamp is computational

Changing the timestamp legitimately changes the result.

### Case 2 — Timestamp is metadata

The computational result should remain equivalent even if timestamp differs.

### Case 3 — Timestamp is unintentionally influencing computation

This is a potential nondeterminism or hidden-input problem.

The experiment must determine which case applies.

---

# 19. Test H — Previous-State Determinism

A sequential blockchain cannot be evaluated only from isolated inputs.

The previous state may be part of the computation.

Therefore test:

```text id="mkw8kw"
Previous State A
      ↓
Input A
      ↓
Result A
```

and repeat using the exact same previous state.

Then compare.

This establishes whether the computation is deterministic as a function of both current and previous state.

---

# 20. Test I — Sequential Determinism

Construct a controlled sequence:

```text id="4jj0ea"
STATE 0
  ↓
BLOCK 1
  ↓
BLOCK 2
  ↓
BLOCK 3
  ↓
BLOCK 4
```

Repeat the complete sequence.

Then compare corresponding states:

```text id="m5h0a2"
RUN A BLOCK 1 ↔ RUN B BLOCK 1
RUN A BLOCK 2 ↔ RUN B BLOCK 2
RUN A BLOCK 3 ↔ RUN B BLOCK 3
RUN A BLOCK 4 ↔ RUN B BLOCK 4
```

This is stronger than testing one isolated computation.

---

# 21. Test J — Order Determinism

Verify that the seven layers are processed in the intended order.

Compare the canonical ordering against deliberate permutations.

For example:

```text id="u4k7x2"
RED → ORANGE → YELLOW → GREEN → BLUE → INDIGO → VIOLET
```

versus an invalid permutation.

The purpose is not to make permutations produce the same result.

The purpose is to determine whether ordering is an explicit deterministic input.

---

# 22. Test K — Equivalent Input Representation

Where the architecture permits equivalent representations, test whether they produce:

1. identical results,
2. equivalent results,
3. different results,
4. or rejection.

Examples may include:

* equivalent serialized representations,
* normalized representations,
* reordered non-semantic metadata,
* equivalent input forms.

Do not assume equivalence.

The implementation must define canonicalization rules.

---

# 23. Test L — Variable / Metadata Perturbation

Change a field known to be non-semantic.

Examples may include:

* diagnostic metadata,
* logging fields,
* external display labels.

Then determine whether the computational result changes.

If a supposedly irrelevant field changes the result, that field is computationally significant whether intended or not.

---

# 24. Test M — Controlled Computational Perturbation

Change one legitimate computational input.

For example:

```text id="a8d4v1"
INPUT A
```

versus:

```text id="j1q4fb"
INPUT A'
```

where only one defined computational value differs.

Expected behavior:

```text id="4gq1s8"
INPUT CHANGE
     ↓
COMPUTATIONAL CHANGE
     ↓
RESULT CHANGE
```

This establishes **sensitivity**.

Determinism is not the claim that everything always produces the same output.

It is the claim that a given input produces a predictable output.

---

# 25. Test N — No Hidden Randomness

Run repeated identical computations while explicitly monitoring for random sources.

Test for:

* random seeds,
* UUID generation,
* nondeterministic ordering,
* random sampling,
* concurrency effects,
* time dependence,
* external network dependence.

If randomness is intentionally part of the architecture, document it rather than treating it as an error.

---

# 26. Test O — Deterministic Serialization

For the same valid artifact, serialize repeatedly.

```text id="n3e9je"
OBJECT
  ↓
SERIALIZE 1
SERIALIZE 2
SERIALIZE 3
```

Compare byte-for-byte outputs.

If serialization is canonical, identical objects should produce identical serialized representations.

If serialization permits multiple equivalent representations, document the allowed variation.

---

# 27. Test P — Commitment Determinism

For every deterministic commitment tested:

```text id="q1j4z5"
SAME INPUT
   ↓
COMMITMENT 1

SAME INPUT
   ↓
COMMITMENT 2
```

Compare commitments.

This test is particularly important because commitments are used by the integration boundary to bind artifacts.

A deterministic commitment function should not randomly produce different commitments for identical committed data.

---

# 28. Test Q — PrismOutput Determinism

Using the same actual WLB and input:

```text id="5c1w4v"
WLB
 ↓
PrismOutput A

WLB
 ↓
PrismOutput B
```

Compare:

* `inputCommitment`,
* `rulesCommitment`,
* `resultCommitment`,
* `executionConditions`,
* serialization.

Where execution conditions intentionally contain dynamic data, isolate that data from the deterministic computational comparison.

---

# 29. Test R — Full Pipeline Determinism

Run the complete internal PrismChain path repeatedly.

```text id="ny7c2g"
PrismInput
   ↓
RED
   ↓
ORANGE
   ↓
YELLOW
   ↓
GREEN
   ↓
BLUE
   ↓
INDIGO
   ↓
VIOLET
   ↓
WLB
   ↓
PrismOutput
```

Compare every computationally relevant artifact.

This is the primary experiment.

---

# 30. Test S — Cross-Machine or Cross-Environment Comparison

Where practical, run the same frozen test vector in another environment.

Possible comparison:

```text id="r0jz5r"
ENVIRONMENT A
        ↓
RESULT A

ENVIRONMENT B
        ↓
RESULT B
```

Do not claim universal portability from one comparison.

Instead record the tested boundary:

> Deterministic across the tested environments.

---

# 31. Test T — Blind Reproduction

Create a frozen test vector.

Have the expected result committed before the second execution.

Then perform the second computation without using the expected result as an input.

After execution:

```text id="3flw3b"
RUN RESULT
     ↓
REVEAL COMMITTED EXPECTATION
     ↓
COMPARE
```

This helps prevent accidental confirmation from the expected answer.

---

# 32. Determinism vs Correctness

The experiment must explicitly preserve this distinction:

```text id="5w6q9g"
DETERMINISTIC
≠
CORRECT
```

For example, a faulty algorithm may produce:

```text id="0y6m0v"
Wrong Result A
Wrong Result A
Wrong Result A
```

That is deterministic.

It is still wrong.

Experiment 17 therefore measures consistency.

Experiments 1–16 provide other forms of evidence about structure, integrity, and continuity.

---

# 33. Determinism vs Consensus

Likewise:

```text id="t3u7j8"
PrismChain determinism
≠
Ethereum consensus
```

A deterministic PrismChain result does not establish that Ethereum agrees with it.

External consensus must be demonstrated through the external system's own evidence.

---

# 34. Determinism Score

The experiment may report a deterministic result across several dimensions.

For example:

| Dimension                      | Result |
| ------------------------------ | ------ |
| Input construction             | Record |
| Input commitment               | Record |
| Layer computation              | Record |
| Layer serialization            | Record |
| WLB formation                  | Record |
| WLB commitment                 | Record |
| PrismOutput construction       | Record |
| Output serialization           | Record |
| Full pipeline                  | Record |
| Cross-process reproduction     | Record |
| Cross-environment reproduction | Record |

A numerical score should only be introduced if the test population and scoring rules are defined beforehand.

Avoid creating an arbitrary percentage that hides important differences.

---

# 35. Difference Classification

When repeated runs differ, classify the difference.

Suggested categories:

```text id="t5p1q9"
EXPECTED METADATA DIFFERENCE
EXPECTED STATE DIFFERENCE
INTENTIONAL NONDETERMINISM
ENVIRONMENTAL DIFFERENCE
SERIALIZATION DIFFERENCE
COMPUTATIONAL DIFFERENCE
UNEXPECTED NONDETERMINISM
UNKNOWN
```

Every unexplained computational difference requires investigation.

---

# 36. Reproducibility Record

Each run should record:

```text id="f9kq12"
experiment_id
test_case_id
run_id
input_hash
rules_hash
native_state_reference
layer_artifact_hashes
WLB_hash
PrismOutput commitments
serialized artifacts
software revision
environment
dependency versions
configuration
timestamp
result
comparison result
difference classification
```

This creates a reproducibility trail rather than merely a pass/fail report.

---

# 37. Evidence Package

Proposed structure:

```text id="h0v7r5"
17-deterministic-computation/
├── experiment-definition.md
├── README.md
│
├── inputs/
│   ├── frozen-test-vectors.json
│   ├── expected-results-commitment.json
│   ├── perturbation-cases.json
│   ├── environment-configurations.json
│   └── control-cases.json
│
├── runs/
│   ├── run-001/
│   ├── run-002/
│   ├── run-003/
│   └── ...
│
├── outputs/
│   ├── layer-results.json
│   ├── wlb-results.json
│   ├── prism-output-results.json
│   ├── serialization-results.json
│   ├── commitment-results.json
│   ├── cross-environment-results.json
│   └── reproducibility-results.json
│
├── analysis/
│   ├── input-determinism.md
│   ├── layer-determinism.md
│   ├── wlb-determinism.md
│   ├── output-determinism.md
│   ├── serialization-determinism.md
│   ├── commitment-determinism.md
│   ├── hidden-inputs.md
│   ├── perturbation-analysis.md
│   ├── environment-analysis.md
│   ├── difference-classification.md
│   └── final-analysis.md
│
└── final-report.md
```

The actual evidence structure may evolve with implementation.

---

# 38. Acceptance Criteria

### AC-01 — Defined Inputs

The experiment identifies the inputs that actually determine the tested computation.

### AC-02 — Repeatability

Repeated execution of identical frozen test vectors produces equivalent computational results.

### AC-03 — Independent Processes

The result remains reproducible across independent processes where determinism is claimed.

### AC-04 — Layer Determinism

Each tested layer produces reproducible results under identical conditions.

### AC-05 — WLB Determinism

The WLB is reproducible when all computationally relevant inputs are fixed.

### AC-06 — Output Determinism

PrismOutput is reproducible when the underlying input, rules, and WLB are fixed.

### AC-07 — Commitment Determinism

Deterministic commitments remain stable for identical committed data.

### AC-08 — Serialization Determinism

Canonical serialization, where claimed, produces equivalent or identical serialized output.

### AC-09 — Perturbation Sensitivity

A legitimate computational input change produces an appropriately corresponding result change.

### AC-10 — Hidden Input Discovery

Potential sources of nondeterminism are identified and classified.

### AC-11 — Blind Reproduction

At least one frozen test vector can be reproduced without revealing the expected result beforehand.

---

# 39. Failure Conditions

The experiment must record failures such as:

* identical inputs produce unexplained different computational results,
* layer outputs vary without an identified cause,
* WLB changes under equivalent conditions without explanation,
* commitments differ for identical committed data,
* serialization varies unexpectedly,
* process restarts change computation,
* environment changes unexpectedly alter the result,
* hidden randomness affects computation,
* system time unexpectedly affects computation,
* unordered processing changes the result,
* equivalent representations produce inconsistent outcomes without defined rules.

These are evidence of nondeterminism or an incompletely defined computational boundary.

---

# 40. Implementation vs Specification

The experiment must not force the current implementation to conform to an assumed deterministic model before the implementation has been inspected.

First determine:

```text id="4t5ncs"
WHAT IS ACTUALLY DETERMINISTIC?
```

Then determine:

```text id="0y6q1f"
WHAT SHOULD BE DETERMINISTIC?
```

Then compare them.

The result may reveal:

```text id="0c9v2q"
IMPLEMENTATION = SPECIFICATION
```

or:

```text id="9d4zq1"
IMPLEMENTATION ≠ SPECIFICATION
```

or:

```text id="o7l9sw"
SPECIFICATION DOES NOT YET DEFINE THE CASE
```

All three are legitimate findings.

---

# 41. Relationship to Previous Experiments

## Experiment 1 — Seven-Layer Computation

Experiment 1 establishes that the seven-layer computational process can produce a result.

Experiment 17 asks whether that result is reproducible under equivalent conditions.

---

## Experiment 3 — Chain Integrity

Chain integrity establishes relationships between sequential artifacts.

Experiment 17 asks whether those relationships are reproduced consistently.

---

## Experiment 7 — Reproducibility

Experiment 7 establishes basic reproducibility.

Experiment 17 goes deeper into **deterministic computation**, identifying the exact inputs and hidden variables that govern repeated execution.

The two experiments are related but not redundant.

---

## Experiment 13 — Continuity

Experiment 13 traces:

```text id="g3l9j0"
PrismInput
→ Seven Layers
→ WLB
→ PrismOutput
```

Experiment 17 asks whether repeating that same trace produces the same computational lineage.

---

## Experiment 15 — Invalid Output / Commitment Detection

Experiment 15 tests whether output integrity can be preserved.

Experiment 17 tests whether valid outputs are consistently regenerated under the same conditions.

---

# 42. Relationship to Future Experiments

Experiment 18 will extend determinism into **state continuity and sequential WLB evolution**.

Experiment 19 will attack the deterministic system adversarially.

Experiment 20 will combine the evidence into a complete reproducible PrismChain demonstration.

The progression is:

```text id="x4m0a1"
17 — DETERMINISM
       ↓
18 — STATE CONTINUITY
       ↓
19 — ADVERSARIAL INTEGRITY
       ↓
20 — END-TO-END REPRODUCTION
```

---

# 43. What This Experiment Does Not Prove

A successful determinism experiment does not prove:

* the algorithm is mathematically correct,
* the architecture is optimal,
* the result is externally true,
* Ethereum agrees with the result,
* external consensus occurred,
* external settlement occurred,
* the system is secure against all attacks,
* the system is deterministic under every possible environment,
* or that every hidden source of nondeterminism has been eliminated.

It establishes only the deterministic behavior demonstrated by the tested conditions.

---

# 44. Interpretation

The desired result is not:

> “Every artifact is byte-for-byte identical no matter what.”

The desired result is:

> **For a clearly defined computational state, the system produces a clearly defined and reproducible computational result.**

If metadata changes while the computational result remains equivalent, document that.

If a computationally irrelevant field unexpectedly changes the result, investigate that.

If the result changes because the input changed, that is expected.

If the result changes while the complete computational state is unchanged, that is the important finding.

---

# 45. Final Principle

> **A deterministic system must be able to explain why the same input produces the same result—and why a different result occurs when something actually changed.**

Do not confuse determinism with correctness.

Do not confuse reproducibility with proof.

Do not hide nondeterminism behind changing timestamps or environment details.

Identify the true computational inputs.

Freeze them.

Run the computation independently.

Repeat it.

Perturb it deliberately.

Compare the results.

And when two supposedly identical computations produce different results:

> **Do not choose the result you prefer. Find the variable that changed.**

**Determinism is not the claim that PrismChain can never produce a different result.**

**It is the claim that when the defined computational state is the same, the computation is predictably the same—and when the result changes, the cause can be identified.**
