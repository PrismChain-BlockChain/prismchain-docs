# Experiment 16 — Failure Propagation

**Status:** 🟣 Experimental

**Evidence Program:** PrismChain Engineering Evidence Suite

**Position:** Experiment 16 of 20

---

## 1. Purpose

Experiment 16 tests how failures propagate through the PrismChain computational and integration boundaries.

Previous experiments have tested individual integrity properties:

* Experiment 11 — PrismInput Acceptance
* Experiment 12 — PrismOutput Formation
* Experiment 13 — Seven-Layer → WLB → Output Continuity
* Experiment 14 — Invalid Input Rejection
* Experiment 15 — Invalid Output / Commitment Detection

Those experiments primarily examine whether individual artifacts and boundaries behave correctly.

Experiment 16 asks a larger systems question:

> **When something fails inside the PrismChain pipeline, does the failure propagate correctly without being silently converted into a valid downstream result?**

The experiment therefore examines the behavior of failure as it moves through the system.

---

# 2. Central Question

> **Does PrismChain preserve the distinction between valid computation, invalid computation, failed computation, rejected input, failed output, and downstream non-completion?**

The target flow is:

```text
NATIVE STATE
     ↓
PrismInput
     ↓
SEVEN-LAYER COMPUTATION
     ↓
WHITE LIGHT BLOCK
     ↓
PrismOutput
     ↓
OUTPUT BOUNDARY
     ↓
RAINBOW RING / DOWNSTREAM RELATIONSHIP
     ↓
EXTERNAL EXECUTION
     ↓
EXTERNAL EVIDENCE
     ↓
SETTLEMENT
```

A failure may occur at any stage.

The experiment determines what happens next.

---

# 3. Architectural Principle

A failure is not automatically a system-wide failure.

Likewise, a downstream artifact is not automatically evidence that all upstream stages succeeded.

The experiment therefore distinguishes:

```text
REJECTION
FAILURE
INVALIDITY
ABORTION
CANCELLATION
EXPIRATION
DISPUTE
REORG
NON-EXECUTION
NON-SETTLEMENT
```

The exact state names used by the implementation must be inspected rather than assumed.

---

# 4. Critical Principle

The system must not silently transform:

```text
FAILURE
```

into:

```text
SUCCESS
```

or:

```text
NO EXECUTION
```

into:

```text
EXECUTED
```

or:

```text
NO SETTLEMENT
```

into:

```text
SETTLED
```

This is especially important at integration boundaries.

The fundamental rule is:

> **A failure must remain distinguishable from a successful result.**

---

# 5. Failure Model

The experiment models the system as a sequence of dependent stages:

```text
 id="r7j0ec"
STAGE N
   ↓
STAGE N+1
   ↓
STAGE N+2
   ↓
...
```

Each stage consumes evidence produced by the previous stage.

Therefore, when an upstream artifact becomes invalid, the downstream behavior must be tested.

Possible outcomes include:

```text
STOP
REJECT
FLAG
PROPAGATE FAILURE
CREATE FAILURE RECORD
WAIT
RETRY
CONTINUE
```

The correct behavior depends on the architecture and implementation.

The experiment does not assume that every failure must immediately stop the entire system.

Instead, it asks whether the resulting behavior is **explicit, traceable, and safe**.

---

# 6. Failure Categories

Failures should initially be classified into the following categories.

### A. Input failure

PrismInput is malformed, inconsistent, or invalid.

### B. Native-state failure

The external native state cannot be accepted or normalized correctly.

### C. Layer failure

One of the seven PrismChain layers fails to produce valid output.

### D. WLB failure

The White Light Block cannot be formed or verified correctly.

### E. Output failure

PrismOutput cannot be formed or validated.

### F. Commitment failure

A required commitment is missing, incorrect, or inconsistent.

### G. Serialization failure

An artifact cannot be serialized or deserialized correctly.

### H. Relationship failure

A downstream relationship cannot be established.

### I. Execution failure

An external execution attempt does not complete successfully.

### J. Evidence failure

Expected execution or settlement evidence is absent, invalid, or contradictory.

### K. Settlement failure

External settlement does not occur or cannot be demonstrated.

---

# 7. Failure Propagation Model

The experiment begins with a successful control path:

```text
 id="9c5v8n"
VALID INPUT
   ↓
VALID COMPUTATION
   ↓
VALID WLB
   ↓
VALID OUTPUT
   ↓
VALID RELATIONSHIP
   ↓
VALID EXECUTION
   ↓
VALID EVIDENCE
   ↓
SETTLEMENT
```

Then individual failures are introduced.

For each failure:

```text
INJECT FAILURE
      ↓
OBSERVE IMMEDIATE RESPONSE
      ↓
OBSERVE DOWNSTREAM RESPONSE
      ↓
RECORD FINAL STATE
      ↓
VERIFY NO FALSE SUCCESS
```

---

# 8. Test A — PrismInput Failure

Start with Experiment 14-style invalid inputs.

Examples:

* incorrect chain identity,
* incorrect state reference,
* incorrect commitment,
* malformed serialization,
* mutated normalized state,
* invalid authentication commitment.

Attempt to continue the pipeline.

The experiment asks:

> Does invalid PrismInput prevent the system from representing a valid downstream computation?

Expected safe behavior is generally:

```text
INVALID INPUT
      ↓
REJECT / INVALID
      ↓
NO VALID COMPUTATION
```

The actual implementation determines the exact state transition.

---

# 9. Test B — Native-State Failure

Introduce a failure before PrismInput construction.

Examples:

```text
missing native state
incomplete native state
inconsistent native state
invalid state reference
unsupported chain identity
unavailable state source
```

Test whether the system:

1. rejects the state,
2. creates a failure record,
3. retries,
4. waits,
5. produces partial artifacts,
6. or incorrectly continues.

A failure to obtain external state must not silently become a valid PrismInput.

---

# 10. Test C — Single-Layer Failure

The PrismChain architecture consists of seven computational layers.

Test what happens if one layer fails.

```text
RED
ORANGE
YELLOW
GREEN
BLUE
INDIGO
VIOLET
```

For each layer, where practical, introduce an isolated failure.

Examples:

* missing layer artifact,
* malformed layer artifact,
* invalid layer hash,
* invalid previous hash,
* invalid block structure,
* unexpected block number,
* invalid data,
* failed layer computation.

Then observe whether the WLB stage:

```text
ACCEPTS
REJECTS
WAITS
FLAGS
```

the failure.

---

# 11. Layer Failure Matrix

The experiment should cover each layer independently.

| Layer  | Failure Introduced | WLB Attempted | Downstream Result | Classification |
| ------ | ------------------ | ------------: | ----------------- | -------------- |
| RED    | Invalid artifact   |           Yes | Record            | Record         |
| ORANGE | Invalid artifact   |           Yes | Record            | Record         |
| YELLOW | Invalid artifact   |           Yes | Record            | Record         |
| GREEN  | Invalid artifact   |           Yes | Record            | Record         |
| BLUE   | Invalid artifact   |           Yes | Record            | Record         |
| INDIGO | Invalid artifact   |           Yes | Record            | Record         |
| VIOLET | Invalid artifact   |           Yes | Record            | Record         |

The purpose is to determine whether layer failure is visible at the WLB boundary.

---

# 12. Test D — Missing Layer

Remove one layer entirely.

The experiment should determine whether the system can accidentally form a White Light Block from:

```text
6 / 7 layers
```

or another incomplete set.

This is a particularly important negative control.

The system must not represent an incomplete computational weave as a complete seven-layer result unless the architecture explicitly defines such behavior.

---

# 13. Test E — WLB Formation Failure

Introduce a failure after all seven layers have been produced but before WLB completion.

Examples:

* malformed layer collection,
* incorrect layer ordering,
* invalid previous WLB hash,
* invalid spectral hash,
* corrupted WLB serialization,
* missing required layer,
* inconsistent layer identities.

Determine whether:

```text
FAILED WLB
```

can accidentally become:

```text
VALID WLB
```

or:

```text
VALID PrismOutput
```

---

# 14. Test F — WLB Mutation After Formation

Construct a valid WLB.

Then mutate it.

Possible mutations:

* layer hash,
* previous WLB hash,
* timestamp,
* data,
* spectral hash,
* block number,
* serialized representation.

Attempt to continue downstream.

This test connects directly to Experiments 6, 12, 13, and 15.

---

# 15. Test G — PrismOutput Formation Failure

Cause output formation to fail.

Examples:

```text
missing WLB
missing input commitment
missing rules commitment
missing result commitment
invalid execution conditions
serialization failure
```

Then observe whether downstream components can accidentally proceed.

Desired architectural behavior:

```text
OUTPUT FAILURE
      ↓
NO VALID OUTPUT
      ↓
NO VALID DOWNSTREAM COMPLETION
```

The exact implementation may use a different mechanism, but the distinction must remain observable.

---

# 16. Test H — Commitment Failure

Introduce an invalid commitment after a valid output has been constructed.

Examples:

```text
wrong inputCommitment
wrong rulesCommitment
wrong resultCommitment
unrelated valid commitment
cross-run commitment
```

Then trace the failure downstream.

The experiment should determine whether the invalid commitment:

* is rejected immediately,
* is flagged,
* causes relationship failure,
* reaches execution,
* reaches settlement,
* or is silently accepted.

---

# 17. Test I — Serialization Failure

Corrupt a serialized artifact between stages.

For example:

```text
PrismOutput
   ↓
serialize
   ↓
CORRUPT
   ↓
deserialize
```

Repeat this across different boundaries where serialization is actually used.

The key question is:

> Does serialization corruption remain visible, or does the system reconstruct a seemingly valid artifact?

---

# 18. Test J — Cross-Run Failure Propagation

Create two valid runs:

```text
RUN A
RUN B
```

Then mix artifacts:

```text
Input-A
WLB-B
Output-A
```

or:

```text
Input-B
WLB-A
Output-B
```

Observe where the mismatch is detected.

This test is especially important because all individual artifacts may be valid.

The failure exists in their **relationship**.

---

# 19. Test K — Relationship Failure

If Rainbow Ring or another relationship layer is present in the tested implementation, deliberately prevent the expected relationship from being established.

Examples may include:

* missing binding,
* invalid lifecycle transition,
* invalid commitment,
* missing prerequisite,
* incompatible output,
* expired relationship,
* cancelled relationship.

The experiment should determine whether PrismOutput remains incorrectly represented as downstream completion.

---

# 20. Test L — Execution Failure

Where an actual execution adapter exists, introduce a controlled execution failure.

The purpose is not to attack the external blockchain.

The purpose is to test PrismChain's representation of what happened.

Possible outcomes:

```text
EXECUTION FAILED
EXECUTION NOT ATTEMPTED
EXECUTION REJECTED
EXECUTION UNKNOWN
EXECUTION SUCCESSFUL
```

The system must not convert:

```text
EXECUTION FAILED
```

into:

```text
EXECUTION SUCCESSFUL
```

---

# 21. Test M — Missing Execution Evidence

Construct a scenario where an execution is expected but evidence is absent.

Test whether the system distinguishes:

```text
EXECUTED
```

from:

```text
EXECUTION CLAIMED
```

and:

```text
EXECUTION UNVERIFIED
```

Evidence must determine the final classification.

---

# 22. Test N — Settlement Failure

Where settlement is part of the tested integration path, simulate or observe a case where settlement does not occur.

The result should not be represented as:

```text
SETTLED
```

without external settlement evidence.

This reinforces the principle:

> **Do not call something settled because PrismChain says it is settled.**

---

# 23. Failure Containment

Not every failure should necessarily propagate infinitely.

The experiment should determine the **containment boundary**.

For each failure:

```text
FAILURE LOCATION
        ↓
FIRST DETECTION
        ↓
FIRST REJECTION
        ↓
DOWNSTREAM VISIBILITY
        ↓
FINAL SYSTEM STATE
```

Record whether the failure:

* stops computation,
* stops output formation,
* prevents relationship formation,
* prevents execution,
* prevents settlement,
* becomes a diagnostic record,
* or remains incorrectly invisible.

---

# 24. Failure State vs Artifact State

An important distinction must be preserved.

A failed process may still generate artifacts.

For example:

```text
failed validation
       ↓
error log
```

does not mean:

```text
failed validation
       ↓
valid computation
```

Therefore the experiment must classify artifacts separately from state.

Useful categories include:

```text
DIAGNOSTIC ARTIFACT
VALID COMPUTATIONAL ARTIFACT
INVALID ARTIFACT
PARTIAL ARTIFACT
FAILURE ARTIFACT
EVIDENCE ARTIFACT
```

---

# 25. No-False-Success Test

For every injected failure, test:

```text
Did the system create a valid WLB?
Did the system create a valid PrismOutput?
Did the system establish a valid relationship?
Did the system report execution?
Did the system report settlement?
```

A failure should not accidentally produce a complete success chain.

The critical test is:

```text
FAILURE
  ↓
NO FALSE SUCCESS
```

---

# 26. Failure Propagation Matrix

Maintain a matrix similar to:

| Failure                    | Detection Stage     | Propagates? | Stops Valid Completion? | Final State |
| -------------------------- | ------------------- | ----------- | ----------------------- | ----------- |
| Invalid PrismInput         | Input boundary      | Record      | Yes                     | Record      |
| Missing layer              | WLB stage           | Record      | Yes                     | Record      |
| Invalid layer hash         | Layer/WLB           | Record      | Yes                     | Record      |
| WLB mutation               | WLB/output          | Record      | Yes                     | Record      |
| Invalid result commitment  | Output boundary     | Record      | Yes                     | Record      |
| Cross-run output           | Output/relationship | Record      | Yes                     | Record      |
| Relationship failure       | Ring boundary       | Record      | Yes                     | Record      |
| Execution failure          | External execution  | Record      | Yes                     | Record      |
| Missing execution evidence | Evidence stage      | Record      | Yes                     | Record      |
| Settlement failure         | Settlement stage    | Record      | Yes                     | Record      |

The final table must use actual observed behavior.

---

# 27. Failure Propagation Depth

Measure how far a failure travels.

For example:

```text
LEVEL 0 — failure detected locally
LEVEL 1 — downstream boundary notified
LEVEL 2 — computation prevented
LEVEL 3 — output prevented
LEVEL 4 — relationship prevented
LEVEL 5 — execution prevented
LEVEL 6 — settlement prevented
```

This is not a universal scoring system.

It is a way to describe where the failure becomes contained.

A failure that is correctly contained at Level 1 may be safer than a failure that travels to Level 5 before detection.

---

# 28. Recovery Behavior

Where the implementation supports recovery, test it separately.

Possible behaviors:

```text
RETRY
RESTART
RECOMPUTE
REJECT
ROLL BACK
WAIT
RESUME
```

Do not treat recovery as success merely because the system eventually produces an artifact.

The recovery must preserve lineage.

For example:

```text
FAILED RUN A
      ↓
RECOVERY
      ↓
RUN B
```

must not silently represent Run B as though it were the original successful Run A.

---

# 29. Reorg and External-State Changes

If the integration implementation supports external state changes or reorganization handling, test how those changes propagate.

The external chain remains sovereign.

Therefore:

```text
EXTERNAL STATE CHANGE
        ↓
NATIVE STATE
        ↓
PrismInput
        ↓
PRISMCHAIN
        ↓
OUTPUT
```

must be re-evaluated according to the actual integration rules.

Do not assume that an earlier output remains valid merely because it was previously valid.

---

# 30. Failure Classification

Each injected failure should receive a final classification.

Suggested categories:

```text
CORRECTLY REJECTED
CORRECTLY CONTAINED
CORRECTLY PROPAGATED
CORRECTLY RECOVERED
CORRECTLY FLAGGED
UNEXPECTED ACCEPTANCE
UNEXPECTED PROPAGATION
FALSE SUCCESS
FALSE SETTLEMENT
UNDETERMINED
UNSUPPORTED
```

This allows the experiment to distinguish successful failure handling from merely observing that something went wrong.

---

# 31. False-Positive Analysis

A particularly dangerous outcome is:

```text
FAILURE
   ↓
VALID RESULT
```

Define a failure-propagation false positive as:

> A deliberately invalid or failed upstream condition that ultimately produces a downstream state indistinguishable from a valid successful execution.

Examples:

* failed input produces valid WLB,
* invalid WLB produces valid output,
* invalid output produces valid relationship,
* failed execution produces execution success,
* missing evidence produces settlement,
* invalid commitment produces accepted completion.

These cases require immediate investigation.

---

# 32. False-Negative Analysis

Also record cases where the system rejects valid recovery or valid operation.

Examples:

* valid input incorrectly rejected,
* valid layer incorrectly treated as failed,
* valid WLB incorrectly invalidated,
* valid output rejected,
* legitimate retry incorrectly blocked.

A system that rejects everything is not a successful integrity system.

It must preserve valid computation while preventing invalid computation.

---

# 33. Control Experiments

At least one clean control run must accompany failure tests.

The control should execute:

```text
VALID INPUT
   ↓
VALID SEVEN LAYERS
   ↓
VALID WLB
   ↓
VALID OUTPUT
```

Where integration is available:

```text
   ↓
VALID RELATIONSHIP
   ↓
VALID EXECUTION
   ↓
VALID EVIDENCE
   ↓
SETTLEMENT
```

The control establishes what successful behavior looks like before failures are injected.

---

# 34. Reproducibility

Every failure injection must be reproducible.

Record:

```text
experiment_id
run_id
failure_id
failure_location
input identifier
layer identifiers
WLB identifier
PrismOutput identifier
commitments
mutation definition
code revision
environment
expected result
actual result
final state
```

Repeat representative failures multiple times.

The same failure condition should produce the same classification unless nondeterminism is explicitly part of the tested system.

---

# 35. Evidence Package

Proposed structure:

```text
16-failure-propagation/
├── experiment-definition.md
├── README.md
│
├── inputs/
│   ├── control-run.json
│   ├── input-failures.json
│   ├── layer-failures.json
│   ├── wlb-failures.json
│   ├── output-failures.json
│   ├── commitment-failures.json
│   ├── relationship-failures.json
│   ├── execution-failures.json
│   └── settlement-failures.json
│
├── outputs/
│   ├── failure-results.json
│   ├── propagation-results.json
│   ├── containment-results.json
│   ├── downstream-results.json
│   ├── recovery-results.json
│   └── reproducibility-results.json
│
├── analysis/
│   ├── input-failures.md
│   ├── layer-failures.md
│   ├── wlb-failures.md
│   ├── output-failures.md
│   ├── commitment-failures.md
│   ├── relationship-failures.md
│   ├── execution-failures.md
│   ├── settlement-failures.md
│   ├── containment.md
│   ├── false-successes.md
│   ├── recovery.md
│   └── final-analysis.md
│
└── final-report.md
```

The actual package may change as implementation develops.

---

# 36. Acceptance Criteria

### AC-01 — Failure Detection

Known injected failures can be detected at an identifiable stage.

### AC-02 — Failure Classification

The system can distinguish failure types sufficiently to diagnose them.

### AC-03 — No False Computation

An invalid input or failed computational stage cannot silently become a valid computational result.

### AC-04 — No False WLB

A failed or incomplete layer set cannot silently become a valid White Light Block.

### AC-05 — No False Output

A failed WLB cannot silently become a valid PrismOutput.

### AC-06 — No False Relationship

An invalid output cannot silently establish a valid downstream relationship.

### AC-07 — No False Execution

A failed or absent execution cannot be represented as successful execution without evidence.

### AC-08 — No False Settlement

Settlement cannot be represented as complete without the appropriate external evidence.

### AC-09 — Failure Traceability

The original failure can be traced through its downstream consequences.

### AC-10 — Recovery Integrity

Where recovery exists, recovered results preserve their own correct lineage.

### AC-11 — Reproducibility

Representative failure cases produce repeatable classifications.

---

# 37. Failure Conditions

Experiment 16 itself fails to demonstrate safe failure propagation if it discovers cases such as:

* invalid input produces valid computation,
* incomplete layers produce valid WLB,
* corrupted WLB produces valid output,
* invalid output produces valid downstream relationship,
* failed execution is represented as successful execution,
* absent evidence is represented as successful execution,
* absent settlement is represented as settlement,
* failure identity is lost,
* cross-run artifacts become indistinguishable,
* recovery silently changes lineage,
* validation behavior is nondeterministic without explanation.

These are not merely test failures.

They identify architectural behavior requiring investigation.

---

# 38. Implementation vs Specification

The exact failure behavior must be discovered from the actual implementation.

The specification may say:

```text
FAILURE → REJECT
```

while the implementation may actually use:

```text
FAILURE → FLAG → WAIT
```

That difference matters.

The experiment should document what exists.

If the implementation behavior is architecturally preferable but undocumented, update the specification afterward.

If the implementation behavior creates an unsafe condition, document the failure before changing it.

The process remains:

```text
INSPECT
   ↓
SPECIFY
   ↓
TEST
   ↓
CONNECT
   ↓
TUNE
   ↓
VERIFY
```

---

# 39. Relationship to Previous Experiments

## Experiment 14 — Invalid Input Rejection

Experiment 14 asks:

> Does the system reject invalid inputs?

Experiment 16 asks:

> What happens to the system after a failure occurs, and does that failure remain visible downstream?

---

## Experiment 15 — Invalid Output / Commitment Detection

Experiment 15 attacks output integrity.

Experiment 16 takes those failures and follows them through the system.

```text
INVALID OUTPUT
      ↓
WHAT HAPPENS NEXT?
```

This makes Experiment 16 a systems-level extension of Experiment 15.

---

## Experiment 13 — Continuity

Experiment 13 establishes computational continuity.

Experiment 16 tests whether that continuity is broken safely when something fails.

```text
VALID CONTINUITY
```

versus:

```text
BROKEN CONTINUITY
       ↓
CORRECT FAILURE
```

---

# 40. Relationship to Future Experiments

Experiment 17 will investigate deterministic computation.

Experiment 18 will examine state continuity and sequential WLB evolution.

Experiment 19 will broaden adversarial testing across the architecture.

Experiment 20 will combine the validated components into a complete reproducible demonstration.

The progression is intentional:

```text
11  INPUT
12  OUTPUT
13  CONTINUITY
14  INVALID INPUT
15  INVALID OUTPUT
16  FAILURE PROPAGATION
17  DETERMINISM
18  STATE CONTINUITY
19  ADVERSARIAL INTEGRITY
20  END-TO-END DEMONSTRATION
```

---

# 41. What This Experiment Does Not Prove

A successful failure-propagation experiment does not prove:

* PrismChain is mathematically correct,
* PrismChain is immune to all failures,
* all possible failure modes have been discovered,
* Ethereum consensus is correct,
* external execution is guaranteed,
* external settlement is guaranteed,
* Rainbow Ring is universally safe,
* or that every possible adversarial condition has been tested.

It demonstrates only the failure behavior actually tested.

---

# 42. Interpretation

The goal is not to make every failure disappear.

The goal is to make failure **visible, bounded, classifiable, and incapable of masquerading as success**.

A mature system does not require:

```text
NO FAILURES
```

It requires:

```text
FAILURE
   ↓
DETECTION
   ↓
CLASSIFICATION
   ↓
CONTAINMENT
   ↓
EVIDENCE
```

when appropriate.

---

# 43. Final Principle

> **A failure is only dangerous when the system loses track of it.**

PrismChain should not merely demonstrate successful computation.

It must demonstrate what happens when computation, validation, output formation, relationships, execution, or settlement fail.

**Failures must remain failures.**

**Invalid states must remain distinguishable from valid states.**

**Diagnostic artifacts must not become false success.**

**Recovery must preserve lineage.**

**Execution must not be inferred from intent.**

**Settlement must not be inferred from execution claims.**

And above all:

> **Do not ask whether the system can succeed. Ask whether the system can fail safely, visibly, and truthfully.**
