# Experiment 14 — Invalid Input Rejection

**Status:** 🟣 Experimental

**Program:** PrismChain Evidence Program

**Category:** Input Integrity / Failure Handling

---

# 1. Purpose

This experiment tests whether PrismChain correctly rejects inputs that are malformed, inconsistent, corrupted, incompatible, or otherwise invalid.

Experiments 11–13 established the intended path for valid data:

```text
NATIVE STATE
     ↓
PrismInput
     ↓
PRISMCHAIN
     ↓
7-LAYER COMPUTATION
     ↓
WHITE LIGHT BLOCK
     ↓
PrismOutput
```

Experiment 14 asks the opposite question:

> **What happens when the input is wrong?**

A functioning boundary must not only demonstrate successful acceptance.

It must also demonstrate that invalid data does not silently enter the computational system as valid data.

---

# 2. Central Question

> **Can PrismChain reliably distinguish valid PrismInput from malformed, corrupted, inconsistent, incompatible, or improperly committed input, and prevent invalid input from being treated as a valid computation?**

The experiment is therefore a **negative test**.

The goal is to deliberately create conditions that should fail and document exactly how the implementation responds.

---

# 3. Hypothesis

### Primary hypothesis

PrismChain's input boundary will reject inputs that violate required structural, serialization, commitment, identity, or validation conditions.

### Secondary hypothesis

Different classes of invalid input will fail at identifiable stages rather than silently producing a valid-looking computational result.

### Failure-handling hypothesis

When an input is rejected, the system will not falsely represent the resulting state as a successful PrismChain computation.

---

# 4. Architectural Context

The intended boundary is:

```text id="0y8krs"
EXTERNAL NATIVE STATE
        ↓
NATIVE CONDUIT
        ↓
NORMALIZATION
        ↓
PrismInput
        ↓
INPUT VALIDATION
        ↓
PRISMCHAIN
```

Invalid data should be stopped at the earliest appropriate boundary.

Conceptually:

```text id="2k4m4k"
VALID INPUT
     ↓
ACCEPT
     ↓
PRISMCHAIN

INVALID INPUT
     ↓
REJECT
     ↓
NO VALID PRISMCHAIN COMPUTATION
```

The actual implementation may have multiple validation stages.

The experiment must identify those stages rather than assuming where rejection occurs.

---

# 5. Critical Distinction

Input rejection is not the same thing as proving the external blockchain is invalid.

For example:

```text id="d9xjqs"
INVALID PrismInput
≠
INVALID ETHEREUM BLOCK
```

Similarly:

```text id="o1s3t2"
VALID PrismInput
≠
PROVEN ETHEREUM FINALITY
```

The experiment concerns the integrity of the **PrismInput boundary**.

---

# 6. What This Experiment Does Not Prove

This experiment does not prove:

* Ethereum consensus
* Ethereum finality
* external validator correctness
* external blockchain security
* settlement
* execution
* Rainbow Ring correctness
* universal interoperability
* production security
* that every possible invalid input can be detected
* that the external native state itself is truthful

It tests the defined validation and rejection behavior of the PrismChain input boundary.

---

# 7. Experimental Objectives

### Objective 1 — Structural Rejection

Determine whether malformed `PrismInput` structures are rejected.

### Objective 2 — Commitment Rejection

Determine whether incorrect commitments are detected.

### Objective 3 — State Consistency

Determine whether inconsistent native-state information is detected.

### Objective 4 — Identity Validation

Determine how incorrect chain identity and state references are handled.

### Objective 5 — Serialization Validation

Determine whether malformed serialized input is rejected.

### Objective 6 — Version Handling

Determine how unsupported or invalid versions are handled.

### Objective 7 — Authentication Handling

Determine how invalid authentication-related data is handled without confusing authentication with consensus or finality.

### Objective 8 — No False Computation

Determine whether rejected inputs can accidentally produce a valid-looking PrismChain result.

### Objective 9 — Failure Traceability

Record exactly where and why each invalid input fails.

---

# 8. Invalid Input Taxonomy

The experiment should classify invalid inputs rather than treating all failures as one category.

```text id="6b5gkp"
STRUCTURAL
    ↓
SERIALIZATION
    ↓
IDENTITY
    ↓
STATE
    ↓
COMMITMENT
    ↓
AUTHENTICATION
    ↓
VERSION
    ↓
SEMANTIC CONSISTENCY
```

Each category should be tested independently.

---

# 9. Test Class A — Missing Fields

Starting from a known-valid input, remove one required field at a time.

Test:

```text id="9m7v6s"
Missing chainId
Missing nativeStateCommitment
Missing stateReference
Missing authenticationCommitment
Missing normalizedState
```

Expected behavior:

```text id="l4q9is"
MISSING REQUIRED DATA
        ↓
REJECT
```

The exact error mechanism must be recorded.

---

# 10. Test Class B — Empty Fields

Replace valid values with empty values where the representation permits it.

Examples:

```text id="7h3d1k"
""
null
zero value
empty bytes
empty object
```

The experiment must determine which empty values are:

* invalid
* valid by design
* interpreted specially

Do not assume that zero or empty values are automatically invalid.

---

# 11. Test Class C — Incorrect Chain Identity

Construct a valid input and change `chainId`.

For example:

```text id="h8gq5f"
EXPECTED CHAIN
      ↓
MUTATE chainId
      ↓
SUBMIT
```

Record whether the implementation:

* rejects the input
* treats it as another chain
* accepts it under a broader rule
* or produces another defined result

The actual behavior is the evidence.

---

# 12. Test Class D — Incorrect State Reference

Change the `stateReference` while leaving the rest of the input unchanged.

Examples may include:

* different block reference
* different state identifier
* stale reference
* nonexistent reference
* reference from another run

Expected behavior should be established before execution.

The experiment must determine whether the implementation correctly prevents an input from claiming to represent one state while referencing another.

---

# 13. Test Class E — Incorrect Native State Commitment

Take a valid input and replace:

```text id="7p5lne"
nativeStateCommitment
```

with an unrelated value.

Expected:

```text id="p6f2hl"
NATIVE STATE
     ≠
COMMITMENT
     ↓
REJECTION
```

If the system accepts the input, that result must be investigated rather than automatically labeled a test failure.

The commitment domain and validation path must first be inspected.

---

# 14. Test Class F — Mutated Normalized State

Start with a valid input.

After its commitment has been established, alter the normalized state.

For example:

```text id="0h7h4v"
VALID STATE
     ↓
COMMITMENT A
     ↓
MUTATE STATE
     ↓
SUBMIT
```

The experiment determines whether the mismatch is detected.

This is one of the most important integrity tests because it checks whether the commitment actually binds the data it is intended to represent.

---

# 15. Test Class G — Incorrect Authentication Commitment

Replace the authentication commitment with an unrelated value.

This test must explicitly distinguish:

```text id="p8cl3u"
AUTHENTICATION COMMITMENT
          ≠
NATIVE STATE COMMITMENT
```

The expected result depends on the actual implementation.

If the current Ethereum builder only provides deterministic authentication plumbing rather than consensus proof, the result must be described accordingly.

Do not describe rejection as "consensus validation" unless consensus verification was actually performed.

---

# 16. Test Class H — Malformed Serialization

Take valid serialized input and mutate its encoded representation.

Test:

* truncated bytes
* extra bytes
* altered field order
* altered field length
* malformed dynamic data
* invalid encoding
* corrupted bytes

Expected:

```text id="9c1rrv"
MALFORMED SERIALIZATION
          ↓
REJECT / DECODE FAILURE
```

The exact observed behavior must be recorded.

---

# 17. Test Class I — Version Mutation

If the current serializer uses a version identifier, alter it.

Test:

```text id="w0y2v1"
SUPPORTED VERSION
       ↓
EXPECTED ACCEPTANCE

UNSUPPORTED VERSION
       ↓
EXPECTED REJECTION
```

If version handling is not currently implemented, document that as an implementation gap rather than inventing behavior.

---

# 18. Test Class J — Cross-Run Substitution

Create two valid runs:

```text id="y3w8ri"
RUN A
RUN B
```

Then construct hybrid inputs.

Examples:

```text id="u9g5xy"
Input A
+
State B
```

or:

```text id="k4g5bd"
Input A
+
Commitment B
```

or:

```text id="2a1q3c"
Input A
+
Authentication B
```

The experiment determines whether cross-run substitution is detected.

This is important because individually valid components can still form an invalid combined state.

---

# 19. Test Class K — Corrupted Block Reference

Where the input references an external block/state object, replace the reference with:

* an older reference
* a future reference
* a nonexistent reference
* a reference from another chain
* a reference from another test run

The system's actual response must be recorded.

---

# 20. Test Class L — Duplicate or Conflicting State

Where the implementation permits multiple representations of related state, create intentionally conflicting values.

For example:

```text id="7i1q8j"
STATE REFERENCE
      ↓
Block A

NORMALIZED STATE
      ↓
Block B
```

The purpose is to determine whether the system detects internal inconsistency.

---

# 21. Test Class M — Invalid Data Types

Where applicable, replace expected types with incompatible representations.

Examples:

```text id="i6v6vp"
number → string
bytes → object
object → array
string → null
```

The system should reject values that cannot be correctly interpreted.

The test should not assume a particular programming-language error.

Record the actual boundary response.

---

# 22. Test Class N — Boundary Bypass Attempt

Attempt to pass data directly into a later stage without satisfying the intended input boundary.

Conceptually:

```text id="b4j2zy"
INVALID / BYPASSED INPUT
          ↓
       PRISMCHAIN
```

The purpose is to determine whether the architecture actually enforces its intended boundary or whether later components can be called independently in ways that bypass required validation.

This is an especially important engineering test.

---

# 23. No-False-Computation Test

For every rejected input, inspect whether any downstream computational artifact was produced.

The expected relationship is:

```text id="v2u6fl"
REJECTED INPUT
      ↓
NO VALID COMPUTATION
      ↓
NO VALID WLB
      ↓
NO VALID PrismOutput
```

However, internal diagnostic artifacts may legitimately exist.

Therefore distinguish:

```text id="7u0p3e"
DIAGNOSTIC ARTIFACT
≠
VALID COMPUTATIONAL RESULT
```

The evidence must show whether the system clearly distinguishes the two.

---

# 24. Error Classification

Every rejection should be classified.

Suggested categories:

```text id="p9v3fz"
STRUCTURAL
SERIALIZATION
IDENTITY
REFERENCE
COMMITMENT
AUTHENTICATION
VERSION
SEMANTIC
BOUNDARY
UNKNOWN
```

For each test:

```text id="r8v1ba"
TEST ID:
INPUT:
EXPECTED:
ACTUAL:
FAILURE CLASS:
REJECTED?:
DOWNSTREAM ARTIFACT CREATED?:
NOTES:
```

---

# 25. Negative Control Matrix

Create a matrix covering the major failure classes.

| Test | Mutation                | Expected                | Actual | Rejected | Downstream Result |
| ---- | ----------------------- | ----------------------- | ------ | -------- | ----------------- |
| A    | Missing field           | Reject                  |        |          |                   |
| B    | Empty field             | Reject/defined behavior |        |          |                   |
| C    | Wrong chain ID          | Defined behavior        |        |          |                   |
| D    | Wrong state reference   | Reject/defined behavior |        |          |                   |
| E    | Wrong commitment        | Reject                  |        |          |                   |
| F    | Mutated state           | Reject                  |        |          |                   |
| G    | Wrong authentication    | Reject/defined behavior |        |          |                   |
| H    | Corrupt serialization   | Reject                  |        |          |                   |
| I    | Wrong version           | Reject/defined behavior |        |          |                   |
| J    | Cross-run substitution  | Reject                  |        |          |                   |
| K    | Invalid block reference | Reject/defined behavior |        |          |                   |
| L    | Conflicting state       | Reject                  |        |          |                   |
| M    | Wrong data type         | Reject                  |        |          |                   |
| N    | Boundary bypass         | Reject/blocked          |        |          |                   |

The table should be populated from actual results.

---

# 26. Rejection Consistency

Repeat selected invalid cases multiple times.

For example:

```text id="b5n2sj"
Invalid Input A
    ↓
Run 1 → Reject

Invalid Input A
    ↓
Run 2 → Reject

Invalid Input A
    ↓
Run 3 → Reject
```

Determine whether the same invalid condition consistently produces the same validation result.

If the result changes, investigate why.

---

# 27. Near-Valid Boundary Test

Create inputs that differ from a valid input by exactly one controlled property.

For example:

```text id="j0h7q9"
VALID INPUT
     ↓
CHANGE ONE FIELD
     ↓
INVALID INPUT
```

This is useful for determining the actual validation boundary.

The test should identify the smallest mutation that changes acceptance behavior.

---

# 28. False Positive Test

A particularly important metric is:

> How often does intentionally invalid input appear valid?

For the controlled negative dataset:

```text id="n0k4sq"
False Positive Rate =
Invalid Inputs Accepted
───────────────────────
Total Invalid Inputs
```

The calculation should only be applied to the defined test population.

It must not be generalized into a claim about all possible invalid inputs.

---

# 29. False Negative Test

Likewise:

> How often does valid input get incorrectly rejected?

Use the valid control set from Experiment 11.

```text id="6x5e2n"
False Negative Rate =
Valid Inputs Rejected
────────────────────
Total Valid Inputs
```

This prevents the system from achieving apparent security simply by rejecting everything.

---

# 30. Reproducibility

Freeze the complete invalid-input test suite.

A second run should produce equivalent classifications.

```text id="6u9h5f"
TEST SUITE A
      ↓
RESULT SET A

TEST SUITE A
      ↓
RESULT SET B

COMPARE
```

Any difference must be explained.

---

# 31. Evidence Package

The experiment should ultimately contain:

```text id="1h3y3v"
14-invalid-input-rejection/
├── experiment-definition.md
├── README.md
├── inputs/
│   ├── valid-controls.json
│   ├── malformed-inputs.json
│   ├── commitment-mutations.json
│   ├── state-mutations.json
│   ├── identity-mutations.json
│   ├── serialization-mutations.json
│   ├── version-tests.json
│   ├── cross-run-tests.json
│   └── boundary-bypass-tests.json
├── outputs/
│   ├── validation-results.json
│   ├── rejection-results.json
│   ├── error-classifications.json
│   ├── downstream-artifact-results.json
│   └── reproducibility-results.json
├── analysis/
│   ├── structural-validation.md
│   ├── commitment-validation.md
│   ├── state-validation.md
│   ├── identity-validation.md
│   ├── serialization-validation.md
│   ├── authentication.md
│   ├── version-handling.md
│   ├── cross-run-substitution.md
│   ├── boundary-bypass.md
│   ├── false-positives.md
│   ├── false-negatives.md
│   ├── controls.md
│   └── final-analysis.md
└── final-report.md
```

The actual evidence structure may expand as the implementation reveals additional validation boundaries.

---

# 32. Acceptance Criteria

The experiment succeeds at the engineering level if it demonstrates:

### A. Valid Inputs Still Work

Known-valid controls are accepted.

### B. Malformed Inputs Are Identified

Structurally invalid inputs are rejected or handled according to defined rules.

### C. Commitment Violations Are Detected

Incorrect or mismatched commitments do not silently pass validation.

### D. State Inconsistency Is Detectable

Conflicting state representations are rejected or explicitly classified.

### E. Serialization Integrity Is Tested

Corrupted encoded data does not silently become valid input.

### F. Cross-Run Substitution Is Tested

Components from unrelated runs cannot silently be combined where continuity is required.

### G. Boundary Bypass Is Tested

The intended input validation boundary cannot simply be ignored without consequence.

### H. No False Valid Computation

Rejected input does not silently become a valid PrismChain computation.

### I. Valid/Invalid Balance Is Measured

The system is evaluated using both valid controls and invalid controls.

### J. Results Are Reproducible

The rejection classifications can be repeated under the same conditions.

---

# 33. Failure Conditions

The experiment is incomplete or unsuccessful if:

* invalid inputs are routinely accepted without explanation
* incorrect commitments are accepted when commitment validation is expected
* corrupted serialization is silently interpreted as valid
* conflicting state is silently accepted
* cross-run artifacts can be substituted without detection where binding is required
* invalid inputs produce indistinguishable valid computational results
* all inputs are rejected, including known-valid controls
* rejection behavior changes unpredictably under identical conditions
* errors cannot be classified or reproduced
* validation exists only in documentation and is not present in the actual implementation
* the experiment relies on mocked validation while the actual boundary is available

A failure is not something to hide.

A failure identifies the boundary that must be corrected.

---

# 34. Results Classification

Use the PrismChain evidence status system:

```text id="6x5j3k"
🟢 BUILT / DEMONSTRATED
The behavior has been implemented and demonstrated.

🔵 RESEARCH
The behavior or interpretation requires further investigation.

🟣 EXPERIMENTAL
The behavior has been experimentally tested but is not yet established.

🟡 HYPOTHESIS / PLANNED
The behavior is proposed but not yet demonstrated.

🔴 PRIVATE
Implementation details are intentionally withheld.

⚪ HISTORICAL
The evidence describes an earlier implementation.
```

---

# 35. Relationship to Previous Experiments

Experiment 11 established that valid `PrismInput` can be constructed and accepted.

Experiment 12 established that actual PrismChain results can be represented as `PrismOutput`.

Experiment 13 established the intended continuity:

```text id="9d1czm"
PrismInput
     ↓
7-LAYER COMPUTATION
     ↓
WLB
     ↓
PrismOutput
```

Experiment 14 attacks the first boundary:

```text id="b4e6ik"
PrismInput
     ↓
VALIDATION
     ↓
ACCEPT / REJECT
```

This creates an important distinction:

```text id="f3p7qi"
VALID INPUT
    ↓
COMPUTE

INVALID INPUT
    ↓
DO NOT COMPUTE AS VALID
```

---

# 36. Relationship to Future Experiments

Experiment 15 will extend the same integrity methodology to the **output and commitment boundary**.

Experiment 16 will examine what happens when failures occur at different stages of the complete pipeline.

Experiment 17 will investigate deterministic computation.

Experiment 18 will test sequential state continuity.

Experiment 19 will perform broader adversarial integrity testing.

Experiment 20 will ultimately combine the verified PrismChain path with the completed external integration and Rainbow Ring relationship.

---

# 37. Final Principle

> **A system is not proven reliable because valid data works. It is proven more completely when deliberately invalid data is introduced and the system correctly distinguishes failure from success.**

The experiment must therefore ask:

```text id="5c5m8d"
WHAT HAPPENS
WHEN THE INPUT IS WRONG?
```

Not:

```text id="i7q3l4"
CAN WE MAKE THE INPUT WORK?
```

**Build the valid path. Attack the boundary. Record the failure. Fix what breaks. Then verify that valid computation still works.**

That is how PrismChain's input boundary becomes evidence rather than an assumption.
