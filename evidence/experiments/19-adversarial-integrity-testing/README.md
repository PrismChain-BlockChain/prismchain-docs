# 🛡️ Experiment 19 — Adversarial Integrity Testing

**Status:** 🟣 Experimental

**Category:** PrismChain Engineering Evidence

**Build Phase:** Integration / Boundary Verification

---

## 1. Purpose

Experiment 19 tests PrismChain under deliberate adversarial conditions.

The purpose is not to prove that PrismChain is “secure.”

The purpose is to determine whether the system can preserve the distinction between:

* valid and invalid input
* authentic and substituted artifacts
* current and stale state
* one computation and another computation
* one history and another history
* valid and mutated commitments
* valid and malformed serialization
* successful and failed computation
* computation and execution
* execution and evidence
* evidence and settlement

Experiments 14–18 test specific classes of failure and integrity.

Experiment 19 combines those lessons into a broader adversarial examination.

The system begins with a known valid control run.

An attacker is then assumed to have the ability to manipulate selected artifacts, references, ordering, serialization, commitments, or downstream representations.

The experiment measures whether those manipulations are:

1. detected,
2. contained,
3. propagated correctly,
4. prevented from becoming false computation,
5. prevented from becoming false output,
6. prevented from becoming false execution,
7. prevented from becoming false settlement representation.

---

# 2. Central Question

> **Can PrismChain preserve computational integrity when an adversary deliberately attempts to corrupt, substitute, replay, reorder, bypass, or misrepresent information across its computational and integration boundaries?**

The experiment does not assume that every attack will be detectable.

Instead, it attempts to discover which attacks are detectable, which are not, where detection occurs, and what happens after detection or failure.

---

# 3. Core Adversarial Flow

```text
VALID SYSTEM
     ↓
DEFINE ATTACK SURFACE
     ↓
SELECT CONTROL ARTIFACT
     ↓
ADVERSARIAL MUTATION / SUBSTITUTION / REPLAY / REORDERING / BYPASS
     ↓
SUBMIT TO ACTUAL SYSTEM
     ↓
OBSERVE DETECTION
     ↓
TRACE PROPAGATION
     ↓
VERIFY DOWNSTREAM STATE
     ↓
CHECK FOR FALSE SUCCESS
     ↓
RECORD RESULT
```

The experiment must test the actual implementation wherever implementation exists.

The specification may define intended behavior.

The experiment records what the software actually does.

---

# 4. Scientific Position

This experiment must not begin with the assumption that PrismChain is secure.

It must begin with the assumption that the implementation needs to be tested.

The experiment therefore follows:

```text
HYPOTHESIS
    ↓
CONTROL
    ↓
ATTACK
    ↓
OBSERVATION
    ↓
MEASUREMENT
    ↓
ANALYSIS
    ↓
CONCLUSION
```

A successful attack is not a failure of the experiment.

It is evidence.

A rejected attack is evidence.

An unexpected acceptance is evidence.

An unexpected rejection is evidence.

---

# 5. Important Distinctions

The experiment must preserve the following distinctions:

```text
ADVERSARIAL TEST
        ≠
SECURITY PROOF
```

```text
DETECTED ATTACK
        ≠
IMMUNE SYSTEM
```

```text
COMMITMENT
        ≠
AUTHENTICATION
        ≠
CONSENSUS
        ≠
FINALITY
        ≠
SETTLEMENT
```

Additional distinctions:

```text
VALID ARTIFACT
        ≠
CORRECT ARTIFACT
```

```text
VALID COMMITMENT
        ≠
VALID COMPUTATION
```

```text
DETECTED CORRUPTION
        ≠
PREVENTED CORRUPTION
```

```text
NO EXECUTION
        ≠
FAILED EXECUTION
        ≠
SUCCESSFUL EXECUTION
```

```text
NO EVIDENCE
        ≠
EVIDENCE OF FAILURE
        ≠
EVIDENCE OF SUCCESS
```

```text
NO SETTLEMENT
        ≠
SETTLED
```

---

# 6. Threat Model

Experiment 19 uses a bounded adversarial model.

The attacker is assumed to be capable of manipulating artifacts that are exposed to the tested boundary.

The attacker is **not automatically assumed** to have access to private implementation internals, private keys, operating-system privileges, or consensus authority unless a specific test explicitly models that capability.

The attacker model must therefore be documented rather than assumed.

---

## 6.1 Attacker Capabilities

Where technically supported by the implementation, the attacker may attempt to:

* modify serialized input
* modify normalized state
* modify state references
* modify commitments
* substitute one artifact for another
* replay an old artifact
* replay an artifact from another run
* replay an artifact from another state
* reorder artifacts
* duplicate artifacts
* delete artifacts
* insert artifacts
* mutate layer data
* substitute layer artifacts
* substitute WLB artifacts
* mutate WLB history
* modify previous-hash relationships
* substitute PrismOutput artifacts
* mutate execution conditions
* alter serialization
* alter version information
* create valid-looking but unrelated artifacts
* attempt boundary bypass
* create cross-run contamination
* create stale-state conditions
* create forked histories
* create mismatched input/output relationships
* create mismatched computation/evidence relationships
* represent an execution that did not occur
* represent settlement that did not occur

---

## 6.2 Attacker Non-Capabilities

The experiment does not automatically grant the attacker:

* control over Ethereum consensus
* control over external blockchain finality
* private signing keys
* administrator privileges
* unrestricted access to private PrismChain implementation
* authority to redefine protocol rules
* authority to rewrite immutable external-chain history
* control of every external system
* cryptographic breakthroughs

If any such capability becomes relevant to a specific test, it must be explicitly documented.

---

# 7. Attack Surface

The adversarial surface is divided into computational, historical, boundary, and downstream domains.

```text
NATIVE STATE
     ↓
PrismInput
     ↓
SEVEN LAYERS
     ↓
WHITE LIGHT BLOCK
     ↓
PrismOutput
     ↓
COMMITMENTS / SERIALIZATION
     ↓
RAINBOW RING / RELATIONSHIP
     ↓
EXECUTION
     ↓
EVIDENCE
     ↓
SETTLEMENT
```

Each boundary becomes a potential test surface.

---

# 8. Attack Surface Inventory

## 8.1 PrismInput Boundary

Test:

* malformed input
* valid-but-wrong input
* wrong chain identity
* wrong state reference
* wrong commitment
* mutated normalized state
* stale input
* replayed input
* cross-run input
* serialization mutation
* version mutation
* duplicate input
* conflicting input

Primary question:

> Can an attacker cause an incorrect external state to be treated as the intended PrismInput?

---

## 8.2 Seven-Layer Artifacts

Test:

* mutated layer data
* incorrect layer identity
* incorrect layer ordering
* stale layer
* layer substitution
* missing layer
* duplicated layer
* cross-run layer
* incorrect previous hash
* unrelated valid layer

Primary question:

> Can an attacker substitute or manipulate one layer without the computational relationship recognizing the inconsistency?

---

## 8.3 White Light Block Formation

Test:

* mutated WLB
* incorrect layer references
* missing layer
* substituted WLB
* stale WLB
* previous-WLB mutation
* cross-run WLB
* unrelated valid WLB
* incorrect reconstruction
* WLB/output mismatch

Primary question:

> Can a false White Light Block be made to appear to be the result of the intended seven-layer computation?

---

## 8.4 Historical Linkage

Test:

* previous-hash mutation
* insertion
* deletion
* duplication
* reordering
* rollback
* fork
* historical substitution
* stale state
* replay

Primary question:

> Can an attacker manipulate computational history without the resulting history becoming distinguishably invalid?

---

## 8.5 PrismOutput

Test:

* wrong input commitment
* wrong rules commitment
* wrong result commitment
* wrong WLB
* mutated execution conditions
* stale output
* cross-run output
* unrelated valid output
* malformed serialization

Primary question:

> Can an output belonging to one computation be represented as the output of another?

---

## 8.6 Serialization

Test:

* field mutation
* field omission
* field reordering where relevant
* type mutation
* version mutation
* malformed encoding
* alternate representations
* ambiguous decoding
* serialization/deserialization mismatch

Primary question:

> Can two different logical states become indistinguishable through serialization, or can one logical state acquire multiple unintended meanings?

---

## 8.7 Cross-Run Substitution

Test:

```text
RUN A INPUT
RUN B LAYERS
RUN A WLB
RUN B OUTPUT
```

and other combinations.

Primary question:

> Can valid artifacts from separate computations be recombined into an apparently valid computation?

---

## 8.8 Replay and Stale Artifacts

Test:

```text
CURRENT INPUT
      +
OLD WLB
```

```text
CURRENT STATE
      +
OLD OUTPUT
```

```text
CURRENT RUN
      +
PREVIOUS RUN ARTIFACT
```

Primary question:

> Can an old valid artifact be reused where a current artifact is required?

---

## 8.9 Boundary Bypass

Where supported, attempt to:

* skip validation
* skip expected construction stages
* submit downstream artifacts directly
* bypass commitment checks
* bypass serialization checks
* bypass state linkage
* bypass relationship states
* bypass expected execution/evidence transitions

Primary question:

> Can the intended trust boundary be bypassed without producing a detectable invalid state?

---

# 9. Attack Classes

The following attack classes form the primary adversarial matrix.

---

## A — Malformed Artifact

Create structurally invalid artifacts.

Examples:

* missing fields
* invalid types
* truncated data
* malformed serialization
* invalid version

Expected result:

The system should reject or explicitly classify the artifact according to actual implementation behavior.

---

## B — Valid-but-Wrong Artifact

Use an artifact that is internally valid but belongs to the wrong computation.

Example:

```text
VALID RUN A WLB
        ↓
SUBMITTED AS RUN B WLB
```

This is more important than simple malformed-data testing.

The attacker is not supplying garbage.

The attacker is supplying something valid in the wrong context.

---

## C — Mutation

Change one meaningful field.

Examples:

* block number
* state root
* layer data
* previous hash
* WLB field
* input commitment
* result commitment
* execution condition

Measure exactly where the mutation becomes detectable.

---

## D — Substitution

Replace one artifact with another valid artifact.

Examples:

```text
RED(A)
ORANGE(A)
YELLOW(B)
GREEN(A)
...
```

or:

```text
INPUT(A)
LAYERS(A)
WLB(B)
OUTPUT(A)
```

---

## E — Replay

Reuse an artifact from a previous valid computation.

Test:

* same input replay
* old WLB replay
* old output replay
* old execution evidence replay
* old settlement representation replay

---

## F — Stale State

Provide an artifact that was once valid but is no longer current.

This tests temporal integrity rather than simple validity.

---

## G — Ordering Manipulation

Attempt:

* layer reordering
* output reordering
* state reordering
* historical reordering

Where ordering is meaningful, determine whether order is actually enforced.

Do not assume it is.

---

## H — Insertion / Deletion / Duplication

Attempt:

```text
A → B → C
```

to become:

```text
A → X → B → C
```

or:

```text
A → C
```

or:

```text
A → B → B → C
```

Determine whether the resulting history remains accepted, rejected, or ambiguously interpreted.

---

## I — Cross-Run Contamination

Combine valid artifacts from separate runs.

This is one of the most important tests because every individual artifact may remain internally valid.

---

## J — Commitment Confusion

Attempt to exploit confusion between:

* input commitment
* authentication commitment
* rules commitment
* result commitment
* WLB hash
* native-state commitment
* relationship binding

Test whether each commitment is interpreted only within its intended domain.

---

## K — Serialization Ambiguity

Attempt to produce:

```text
different logical state
        ↓
same serialized representation
```

or:

```text
same logical state
        ↓
unexpectedly different representation
```

Test versioning and decoding behavior where supported.

---

## L — Boundary Bypass

Attempt to move directly from an upstream artifact to a downstream stage without satisfying the expected intermediate relationship.

Example:

```text
PrismInput
    ↓
[BYPASS]
    ↓
PrismOutput
```

The implementation determines whether such a path is actually possible.

---

## M — Failure Masking

Create a failure and attempt to make it appear successful.

Examples:

* failed input represented as valid
* failed WLB represented as completed
* failed output represented as valid
* missing execution represented as executed
* missing evidence represented as successful evidence
* unsettled state represented as settled

---

## N — Output Impersonation

Construct a valid-looking PrismOutput that does not correspond to the actual WLB.

The purpose is to determine whether output identity is actually bound to computation.

---

## O — Execution / Evidence Mismatch

Test:

```text
PrismOutput says X
        ↓
execution evidence says Y
```

and:

```text
PrismOutput says execution occurred
        ↓
no execution evidence
```

The experiment must determine what the actual implementation records and validates.

---

## P — Settlement Misrepresentation

Attempt to represent settlement without sufficient external evidence.

The core rule is:

> **Do not call something settled because PrismChain says it is settled.**

External settlement must remain an external fact.

---

## Q — Concurrency / Race Conditions

Only where the implementation supports concurrent or asynchronous processing, test:

* simultaneous submissions
* duplicate submissions
* conflicting submissions
* state updates arriving out of order
* stale state racing current state
* repeated execution requests

If concurrency is not currently supported, record this test as **not applicable**, rather than inventing behavior.

---

## R — Fork / History Manipulation

Attempt to create:

```text
A → B → C
```

and:

```text
A → B → D
```

Then test whether the system:

* distinguishes the histories,
* accepts both as separate branches,
* incorrectly merges them,
* or lacks the mechanism to make the distinction.

---

## S — Configuration / Rules Mismatch

Use:

```text
INPUT A
+
RULES B
+
COMPUTATION A
```

or:

```text
INPUT A
+
RULES A
+
OUTPUT B
```

Determine whether rules identity is sufficiently represented and bound.

---

## T — Degradation

Where relevant, introduce conditions that reduce system integrity without necessarily destroying execution.

Examples:

* stale dependencies
* missing expected artifact
* delayed artifact
* partial state
* repeated submissions

This experiment focuses on integrity rather than generic denial-of-service testing.

---

# 10. Control Runs

Every adversarial test requires a control where practical.

The control establishes:

```text
VALID INPUT
      ↓
VALID COMPUTATION
      ↓
VALID WLB
      ↓
VALID OUTPUT
```

The control must be preserved before attack mutation.

Recommended identifiers:

```text
CONTROL-001
CONTROL-002
CONTROL-003
```

Each attack should identify the control from which it originated.

---

# 11. One-Variable Attacks

The first adversarial pass should change exactly one meaningful variable.

Example:

```text
CONTROL
  ↓
CHANGE resultCommitment ONLY
  ↓
TEST
```

Then:

```text
CONTROL
  ↓
CHANGE previousHash ONLY
  ↓
TEST
```

This establishes causal clarity.

---

# 12. Compound Attacks

After one-variable attacks are understood, combine attacks.

Examples:

```text
STALE INPUT
    +
VALID OLD WLB
    +
CURRENT OUTPUT
```

or:

```text
CROSS-RUN INPUT
    +
SUBSTITUTED LAYER
    +
VALID SERIALIZATION
```

Compound attacks test whether multiple individually understandable manipulations interact unexpectedly.

---

# 13. Chained Attacks

The final adversarial layer attempts escalation.

Example:

```text
SUBSTITUTE INPUT
      ↓
SUBSTITUTE LAYER
      ↓
REUSE WLB
      ↓
MUTATE OUTPUT
      ↓
ATTEMPT DOWNSTREAM EXECUTION
      ↓
ATTEMPT REPRESENTATION AS SETTLED
```

The goal is not merely to determine whether individual attacks fail.

The goal is to determine whether a failure at one boundary can be concealed by a later valid-looking artifact.

---

# 14. Detection

For every attack, record:

```text
ATTACK ID:
CONTROL RUN:
ATTACK CLASS:
TARGET:
MODIFICATION:
EXPECTED DETECTION POINT:
ACTUAL DETECTION POINT:
DETECTED:
REJECTED:
PROPAGATED:
CONTAINED:
DOWNSTREAM ARTIFACT CREATED:
EXECUTION REPRESENTED:
SETTLEMENT REPRESENTED:
FINAL STATE:
```

Detection must be based on observed behavior.

---

# 15. Containment

Detection alone is insufficient.

For each attack determine whether the invalid condition:

```text
STOPPED AT BOUNDARY
```

or:

```text
ENTERED COMPUTATION
```

or:

```text
REACHED WLB
```

or:

```text
REACHED OUTPUT
```

or:

```text
REACHED RELATIONSHIP
```

or:

```text
REACHED EXECUTION REPRESENTATION
```

or:

```text
REACHED SETTLEMENT REPRESENTATION
```

This establishes the propagation boundary.

---

# 16. Propagation Analysis

For each successful attack or accepted mutation, trace:

```text
INPUT
 ↓
LAYER
 ↓
WLB
 ↓
OUTPUT
 ↓
RELATIONSHIP
 ↓
EXECUTION
 ↓
EVIDENCE
 ↓
SETTLEMENT
```

The purpose is to determine whether the system:

1. detects the attack,
2. contains the attack,
3. transforms the attack into another failure,
4. incorrectly accepts the attack,
5. or loses track of the attack.

---

# 17. False Positives

A false positive occurs when a valid control is incorrectly rejected.

Measure:

```text
valid controls rejected
-----------------------
valid controls tested
```

Investigate:

* environment dependence
* ordering assumptions
* serialization differences
* state assumptions
* configuration differences
* implementation defects

---

# 18. False Negatives

A false negative occurs when an invalid or adversarial condition is accepted as valid when the test defines that condition as invalid.

Measure:

```text
invalid/adversarial cases incorrectly accepted
-----------------------------------------------
invalid/adversarial cases tested
```

False negatives are particularly important when the accepted artifact can propagate downstream.

---

# 19. Attack Severity

Do not classify an attack only as “passed” or “failed.”

Record its maximum propagation depth.

Example:

```text
LEVEL 0 — rejected at input
LEVEL 1 — entered computation
LEVEL 2 — affected layer
LEVEL 3 — affected WLB
LEVEL 4 — affected output
LEVEL 5 — affected relationship
LEVEL 6 — represented execution
LEVEL 7 — represented evidence
LEVEL 8 — represented settlement
```

The levels are an experimental reporting framework.

They are not assumed to exist as protocol states.

---

# 20. Adversarial Attack Matrix

| Class | Target        | Manipulation            | Primary Question                                     |
| ----- | ------------- | ----------------------- | ---------------------------------------------------- |
| A     | Artifact      | Malformed data          | Is structural corruption detected?                   |
| B     | Artifact      | Valid-but-wrong data    | Is contextual correctness enforced?                  |
| C     | Artifact      | Mutation                | Does a meaningful change remain detectable?          |
| D     | Artifact      | Substitution            | Can valid artifacts be exchanged?                    |
| E     | History       | Replay                  | Can old artifacts be reused?                         |
| F     | State         | Stale state             | Is temporal identity preserved?                      |
| G     | Ordering      | Reordering              | Is meaningful ordering enforced?                     |
| H     | History       | Insert/delete/duplicate | Can history be altered?                              |
| I     | Runs          | Cross-run substitution  | Are runs isolated?                                   |
| J     | Commitments   | Domain confusion        | Are commitments bound correctly?                     |
| K     | Serialization | Encoding mutation       | Is representation unambiguous?                       |
| L     | Boundary      | Bypass                  | Can validation be skipped?                           |
| M     | Failure       | Masking                 | Can failure appear successful?                       |
| N     | Output        | Impersonation           | Can false output represent real computation?         |
| O     | Execution     | Evidence mismatch       | Can execution be misrepresented?                     |
| P     | Settlement    | Misrepresentation       | Can settlement be falsely represented?               |
| Q     | Runtime       | Race                    | Where supported, can ordering produce inconsistency? |
| R     | History       | Fork manipulation       | Are divergent histories distinguishable?             |
| S     | Rules         | Configuration mismatch  | Are rules bound to computation?                      |
| T     | Runtime       | Degradation             | Does integrity survive degraded conditions?          |

---

# 21. Evidence Requirements

Every attack must preserve enough information to reproduce the result.

At minimum:

```text
experiment_id
attack_id
control_run_id
input_identity
source_artifact_identity
mutated_artifact
mutation_description
expected_result
actual_result
detection_point
propagation_path
final_state
environment
timestamp
software/version information
```

Where cryptographic or serialized artifacts are involved, preserve the actual bytes or canonical representation used by the implementation.

---

# 22. Reproducibility

A meaningful adversarial result must be reproducible.

At minimum:

1. execute the valid control,
2. preserve the control artifacts,
3. apply the same attack,
4. execute the same test,
5. compare the result,
6. repeat from a fresh environment where practical.

The experiment should determine whether:

```text
SAME CONTROL
+
SAME ATTACK
=
SAME RESULT
```

If not, investigate the source of nondeterminism.

---

# 23. Acceptance Criteria

Experiment 19 is successful as an experiment when:

* a valid control can be established,
* attack surfaces can be identified,
* adversarial mutations can be applied reproducibly,
* results can be observed,
* detection points can be identified where detection occurs,
* propagation can be traced,
* false positives can be measured,
* false negatives can be measured,
* successful attacks can be documented rather than hidden,
* containment behavior can be characterized,
* downstream representations can be distinguished from actual external events,
* limitations are explicitly recorded.

A successful experiment does **not** require every attack to fail.

Unexpected acceptance is a valid experimental result.

---

# 24. Failure Conditions

The experiment itself is considered incomplete if:

* no valid control exists,
* attacks cannot be reproduced,
* artifacts cannot be identified,
* expected and actual results cannot be distinguished,
* mutation provenance is lost,
* downstream effects cannot be traced,
* false positives cannot be measured where applicable,
* false negatives cannot be measured where applicable,
* results are interpreted from specification alone,
* successful attacks are silently discarded,
* implementation behavior is replaced with assumed behavior.

---

# 25. Implementation vs Specification

This experiment must preserve the project's implementation discipline.

Specifications describe intended architecture.

Implementation reveals actual behavior.

Therefore:

```text
SPECIFICATION
      ↓
HYPOTHESIS
      ↓
IMPLEMENTATION
      ↓
ATTACK
      ↓
OBSERVATION
      ↓
SPECIFICATION UPDATE
```

If the implementation behaves differently from the current specification:

**record the difference.**

Do not silently modify the experiment to make the implementation appear compliant.

Do not silently modify the implementation to make the experiment appear successful.

The experiment exists to discover reality.

---

# 26. Relationship to Previous Experiments

Experiment 19 builds directly on Experiments 14–18.

### Experiment 14 — Invalid Input Rejection

Established deliberate attacks against the PrismInput boundary.

Experiment 19 expands this into broader cross-boundary attacks.

### Experiment 15 — Invalid Output / Commitment Detection

Established output and commitment mutation testing.

Experiment 19 extends this into substitution, replay, cross-run, and impersonation attacks.

### Experiment 16 — Failure Propagation

Established how failures move through the system.

Experiment 19 asks whether an adversary can manipulate that propagation or disguise a failure as success.

### Experiment 17 — Deterministic Computation

Established the importance of repeatable computation.

Experiment 19 uses repeatability to reproduce attacks and distinguish genuine attack effects from nondeterministic behavior.

### Experiment 18 — State Continuity / Sequential WLB Evolution

Established sequential history and state relationships.

Experiment 19 attacks those relationships through replay, insertion, deletion, duplication, reordering, rollback, substitution, and forks.

---

# 27. Relationship to Experiment 20

Experiment 20 is the final end-to-end reproducible PrismChain demonstration.

Experiment 19 should therefore serve as an adversarial stress test immediately before that demonstration.

The relationship is:

```text
11  PrismInput
        ↓
12  PrismOutput
        ↓
13  Input → Layers → WLB → Output
        ↓
14  Invalid Input Rejection
        ↓
15  Invalid Output Detection
        ↓
16  Failure Propagation
        ↓
17  Deterministic Computation
        ↓
18  State Continuity
        ↓
19  Adversarial Integrity Testing
        ↓
20  End-to-End Reproducible Demonstration
```

Experiment 20 should not conceal weaknesses discovered in Experiment 19.

If Experiment 19 discovers an integrity limitation, Experiment 20 should either:

* incorporate the limitation into its declared scope,
* demonstrate the corrected implementation,
* or explicitly report the unresolved limitation.

---

# 28. What This Experiment Does Not Prove

Experiment 19 does **not** prove:

* complete protocol security,
* absence of undiscovered vulnerabilities,
* cryptographic security,
* Ethereum consensus security,
* Ethereum finality,
* external-chain security,
* economic security,
* Sybil resistance,
* network-level security,
* denial-of-service resistance,
* private-key security,
* production readiness,
* formal verification,
* complete adversarial coverage,
* resistance to attacks outside the defined threat model.

It also does not prove that PrismChain can never be compromised.

It only establishes evidence about the attacks actually tested.

---

# 29. Coverage Limitations

The attack matrix must be treated as a test population, not an exhaustive universe.

Document:

* attack classes tested,
* attack classes not tested,
* implementation features unavailable,
* concurrency features unavailable,
* external systems not simulated,
* cryptographic assumptions,
* environment limitations,
* untested private components,
* tests that remain theoretical,
* tests deferred until implementation exists.

A test marked “not applicable” is preferable to an invented result.

---

# 30. Evidence Package

The proposed evidence package is:

```text
19-adversarial-integrity-testing/
├── experiment-definition.md
├── README.md
│
├── controls/
│   ├── control-run-001.json
│   ├── control-run-002.json
│   └── control-summary.json
│
├── attacks/
│   ├── malformed-artifacts.json
│   ├── valid-but-wrong-artifacts.json
│   ├── mutation-cases.json
│   ├── substitution-cases.json
│   ├── replay-cases.json
│   ├── stale-state-cases.json
│   ├── ordering-cases.json
│   ├── insertion-deletion-duplication.json
│   ├── cross-run-cases.json
│   ├── commitment-confusion.json
│   ├── serialization-attacks.json
│   ├── boundary-bypass.json
│   ├── failure-masking.json
│   ├── output-impersonation.json
│   ├── execution-evidence-mismatch.json
│   ├── settlement-misrepresentation.json
│   ├── concurrency-cases.json
│   ├── fork-history-cases.json
│   └── rules-mismatch.json
│
├── outputs/
│   ├── detection-results.json
│   ├── containment-results.json
│   ├── propagation-results.json
│   ├── downstream-results.json
│   ├── false-positive-results.json
│   ├── false-negative-results.json
│   ├── severity-results.json
│   └── reproducibility-results.json
│
├── analysis/
│   ├── threat-model.md
│   ├── attack-surface.md
│   ├── control-analysis.md
│   ├── input-attacks.md
│   ├── layer-attacks.md
│   ├── wlb-attacks.md
│   ├── history-attacks.md
│   ├── output-attacks.md
│   ├── commitment-attacks.md
│   ├── serialization-attacks.md
│   ├── cross-run-attacks.md
│   ├── replay-attacks.md
│   ├── boundary-bypass.md
│   ├── failure-masking.md
│   ├── execution-evidence.md
│   ├── settlement-representation.md
│   ├── compound-attacks.md
│   ├── chained-attacks.md
│   ├── false-positives.md
│   ├── false-negatives.md
│   ├── coverage-limitations.md
│   └── final-analysis.md
│
└── final-report.md
```

---

# 31. Recommended Final Report Structure

The final report should contain:

```text
1. Experiment Objective
2. System Under Test
3. Threat Model
4. Attacker Capabilities
5. Attack Surface
6. Control Runs
7. Attack Matrix
8. One-Variable Results
9. Compound Attack Results
10. Chained Attack Results
11. Detection Analysis
12. Containment Analysis
13. Propagation Analysis
14. False Positives
15. False Negatives
16. Downstream Integrity
17. Execution Representation
18. Settlement Representation
19. Reproducibility
20. Coverage Limitations
21. Discovered Weaknesses
22. Discovered Strengths
23. Implementation/Specification Differences
24. Relationship to Experiment 20
25. Final Conclusion
```

---

# 32. Interpretation Rules

When interpreting results, use precise language.

Prefer:

> “The implementation rejected this mutation at the PrismInput boundary.”

over:

> “PrismChain is secure.”

Prefer:

> “The substituted WLB was detected during validation.”

over:

> “WLB substitution is impossible.”

Prefer:

> “The tested attack did not produce a downstream execution artifact.”

over:

> “Execution cannot be forged.”

The experiment must never generalize beyond the evidence.

---

# 33. Final Principle

> **Do not test an adversary by asking whether the system looks secure. Give the adversary something real to attack.**

Take valid artifacts.

Mutate them.

Substitute them.

Replay them.

Reorder them.

Combine them.

Try to bypass boundaries.

Try to disguise failures.

Try to make one computation look like another.

Then trace exactly what happens.

The objective is not to prove that PrismChain is invulnerable.

The objective is to discover where its integrity holds, where it fails, how failures propagate, and whether the system can tell the difference between what actually happened and what merely looks valid.

**Attack the relationships.**

**Measure the boundaries.**

**Record the failures.**

**Prove only what the evidence supports.**
