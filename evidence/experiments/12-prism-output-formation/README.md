# Experiment 11 — PrismInput Acceptance

**Status:** 🟣 Experimental

**Program:** PrismChain Evidence Program

**Category:** External Boundary / Input Integrity

---

## 1. Purpose

This experiment tests whether PrismChain can correctly accept a valid `PrismInput` produced from an external native blockchain state through the Native Conduit boundary.

The experiment establishes the boundary between:

```text
NATIVE BLOCKCHAIN
       ↓
NATIVE STATE
       ↓
NATIVE CONDUIT
       ↓
NORMALIZATION
       ↓
PrismInput
       ↓
PRISMCHAIN
```

The objective is not to prove the external blockchain's consensus or finality.

The objective is to demonstrate that an external native state can be transformed into a well-defined `PrismInput`, transmitted across the boundary, validated, and accepted by PrismChain without loss of the information required by the integration architecture.

---

# 2. Central Question

> **Can a valid external native state be transformed into a valid PrismInput and accepted by PrismChain deterministically, while invalid, malformed, or inconsistent inputs are rejected?**

The experiment must distinguish the input boundary from every later stage of the system.

In particular:

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

A valid `PrismInput` does not, by itself, prove that the underlying external blockchain state is final or settled.

---

# 3. Hypothesis

### Primary hypothesis

A correctly constructed `PrismInput` containing the required normalized native state, chain identity, state reference, state commitment, and authentication commitment can be deterministically serialized, validated, and accepted by the PrismChain integration boundary.

### Secondary hypothesis

Inputs that are malformed, internally inconsistent, corrupted, incorrectly committed, incorrectly identified, or otherwise invalid can be detected and rejected before they are treated as valid PrismChain inputs.

---

# 4. Architectural Context

PrismChain does not directly become the external blockchain.

The external blockchain remains sovereign.

The Native Conduit provides the boundary through which native state becomes information that PrismChain can process.

The conceptual flow is:

```text
┌──────────────────────┐
│  NATIVE BLOCKCHAIN   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     NATIVE STATE     │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    NATIVE CONDUIT    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    NORMALIZATION     │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│      PrismInput      │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│     PRISMCHAIN       │
└──────────────────────┘
```

The experiment begins at the point where native state is available to the conduit and ends when the corresponding `PrismInput` has either been accepted or rejected.

---

# 5. PrismInput Model

The current integration boundary defines:

```text
PrismInput.Data
├── chainId
├── nativeStateCommitment
├── stateReference
├── authenticationCommitment
└── normalizedState
```

The serialized representation uses the defined versioned encoding.

The experiment must verify the actual implementation rather than assuming that the architectural specification and implementation are identical.

If implementation differs from the current specification, record the difference.

Do not silently modify the specification to make the result appear correct.

---

# 6. What This Experiment Does Not Prove

This experiment does **not** prove:

* Ethereum consensus
* Ethereum finality
* correctness of an external validator set
* correctness of an external blockchain
* settlement on the external chain
* execution on the external chain
* correctness of the entire PrismChain computation
* correctness of the White Light Block
* correctness of Rainbow Ring
* economic security
* production security
* universal interoperability
* that an authentication commitment is a consensus proof

The experiment only establishes evidence about the **PrismInput boundary**.

---

# 7. Experimental Objectives

The experiment has the following objectives.

### Objective 1 — Valid Input Construction

Construct a valid `PrismInput` from controlled native-state data.

### Objective 2 — Deterministic Serialization

Verify that identical input data produces identical serialized representation and commitment.

### Objective 3 — Information Preservation

Verify that required native-state information survives normalization and input construction.

### Objective 4 — Boundary Acceptance

Demonstrate that a valid `PrismInput` can cross the intended boundary into PrismChain.

### Objective 5 — Commitment Consistency

Verify that the commitments associated with the input correspond to the data they are intended to represent.

### Objective 6 — Authentication Separation

Demonstrate that the authentication commitment is treated as authentication-related information rather than incorrectly being presented as consensus or finality.

### Objective 7 — Invalid Input Rejection

Demonstrate rejection of malformed or inconsistent inputs.

### Objective 8 — Reproducibility

Demonstrate that the same controlled input produces the same expected result.

---

# 8. Experimental Flow

The primary experiment follows:

```text
NATIVE STATE
     ↓
CAPTURE
     ↓
NORMALIZE
     ↓
CONSTRUCT PrismInput
     ↓
SERIALIZE
     ↓
COMPUTE / VERIFY COMMITMENTS
     ↓
VALIDATE
     ↓
SUBMIT TO PRISMCHAIN
     ↓
ACCEPT OR REJECT
```

The resulting record must preserve enough information to reconstruct what happened.

---

# 9. Controlled Native State

The initial test should use a controlled native-state fixture before relying exclusively on live external blockchain state.

For Ethereum, the native-state model currently includes:

```text
EthereumNativeState
├── blockHash
├── parentHash
├── stateRoot
├── transactionsRoot
├── receiptsRoot
└── blockNumber
```

The controlled fixture should be explicitly identified as synthetic or captured.

A synthetic fixture must never be presented as an authentic Ethereum consensus state.

---

# 10. Test Classes

The experiment should contain several independent test classes.

## 10.1 Valid Input

Construct a fully populated valid `PrismInput`.

Expected:

```text
VALID INPUT
     ↓
VALIDATION PASSES
     ↓
ACCEPTED
```

---

## 10.2 Missing Field

Remove one required field.

Test independently:

* missing `chainId`
* missing `nativeStateCommitment`
* missing `stateReference`
* missing `authenticationCommitment`
* missing `normalizedState`

Expected:

```text
INVALID INPUT
     ↓
REJECTED
```

---

## 10.3 Commitment Mutation

Construct a valid input and alter the commitment without altering the underlying data.

Expected:

```text
DATA ≠ COMMITMENT
        ↓
REJECTION
```

---

## 10.4 Data Mutation

Construct a valid input and modify the underlying normalized state while retaining the original commitment.

Expected:

```text
DATA MUTATED
     ↓
COMMITMENT MISMATCH
     ↓
REJECTION
```

---

## 10.5 State Reference Mutation

Modify the state reference while leaving the other fields unchanged.

Expected behavior must be explicitly recorded.

The system must not silently treat the altered reference as equivalent to the original state.

---

## 10.6 Chain Identity Mutation

Modify `chainId`.

Expected behavior must be determined by the actual implementation.

The experiment should establish whether the modified chain identity is:

* rejected,
* accepted as a different chain,
* or handled through another defined mechanism.

Do not assume the answer before testing.

---

## 10.7 Serialization Mutation

Modify serialized bytes after serialization.

Expected:

```text
SERIALIZED DATA
      ↓
MUTATION
      ↓
DECODE / VERIFY
      ↓
REJECTION
```

---

## 10.8 Version Mutation

If the serializer contains a version field, alter the version.

Test whether unsupported versions are:

* rejected,
* explicitly recognized,
* or otherwise handled.

The observed behavior must be recorded.

---

# 11. Determinism Test

Run the exact same controlled input multiple times.

Record:

```text
RUN
CHAIN ID
STATE REFERENCE
NORMALIZED STATE
NATIVE STATE COMMITMENT
AUTHENTICATION COMMITMENT
SERIALIZED INPUT
INPUT COMMITMENT
ACCEPTANCE RESULT
```

Compare every deterministic field.

Expected result:

```text
IDENTICAL INPUT
      ↓
IDENTICAL DETERMINISTIC REPRESENTATION
      ↓
IDENTICAL COMMITMENT
```

Any intentional nondeterministic field must be identified explicitly.

---

# 12. Information Preservation Test

The input boundary must be examined for information loss.

Compare:

```text
NATIVE STATE
      ↓
NORMALIZED STATE
      ↓
PrismInput
```

For every required field, record:

| Information            | Native State | Normalized State | PrismInput |
| ---------------------- | ------------ | ---------------- | ---------- |
| Chain identity         |              |                  |            |
| Block/state identity   |              |                  |            |
| Parent relationship    |              |                  |            |
| State commitment       |              |                  |            |
| Transaction commitment |              |                  |            |
| Receipt commitment     |              |                  |            |
| Block number           |              |                  |            |

Not every native field necessarily needs to appear directly inside `PrismInput`.

If information is intentionally transformed, document the transformation.

The purpose is to distinguish:

**intentional normalization**

from

**accidental information loss.**

---

# 13. Commitment Test

For each commitment, establish:

```text
WHAT DATA DOES IT COMMIT TO?
HOW IS IT SERIALIZED?
HOW IS THE COMMITMENT GENERATED?
CAN THE COMMITMENT BE REPRODUCED?
WHAT HAPPENS IF THE DATA CHANGES?
```

The experiment must not use vague language such as "secured by a hash."

The actual commitment construction should be recorded.

---

# 14. Authentication Test

Authentication must be tested separately from commitment.

The experiment should document:

```text
COMMITMENT
    ↓
What data is represented?

AUTHENTICATION
    ↓
What authenticity claim is represented?

CONSENSUS
    ↓
What consensus claim exists?

FINALITY
    ↓
What finality claim exists?
```

If the current implementation only provides deterministic authentication plumbing rather than Ethereum consensus verification, the evidence must explicitly state that limitation.

For example:

> The experiment demonstrates deterministic construction and validation of the configured authentication commitment. It does not establish Ethereum consensus proof or Ethereum finality.

---

# 15. Boundary Acceptance Test

A valid `PrismInput` should be passed through the actual integration boundary.

Record:

```text
INPUT ID
CHAIN ID
STATE REFERENCE
INPUT COMMITMENT
VALIDATION RESULT
ACCEPTANCE RESULT
ERROR, IF ANY
```

The experiment must establish exactly where acceptance occurs.

Do not describe a locally constructed object as "accepted by PrismChain" unless it actually crossed the relevant implementation boundary.

---

# 16. Negative Controls

Negative controls are required.

At minimum:

### Control A — Randomized Commitment

Replace the expected commitment with a random value.

### Control B — Mutated State

Alter normalized state after commitment generation.

### Control C — Incorrect Chain

Use an incompatible chain identifier.

### Control D — Corrupted Serialization

Modify serialized bytes.

### Control E — Missing Data

Remove required information.

### Control F — Stale State

Use an intentionally older state reference where freshness is relevant.

The expected behavior of each control must be defined before execution.

---

# 17. Reproducibility Protocol

A second independent run should be performed using the same frozen input fixture.

Where practical:

```text
RUN A
   ↓
RESULT A

RUN B
   ↓
RESULT B

COMPARE A ↔ B
```

The experiment is reproducible only if the expected deterministic portions match.

---

# 18. Evidence Requirements

The final evidence package should preserve:

```text
11-prism-input-acceptance/
├── experiment-definition.md
├── README.md
├── inputs/
│   ├── valid-native-state.json
│   ├── valid-prism-input.json
│   ├── invalid-inputs.json
│   ├── mutation-cases.json
│   └── control-cases.json
├── outputs/
│   ├── normalized-state.json
│   ├── serialized-input.json
│   ├── commitments.json
│   ├── acceptance-results.json
│   └── rejection-results.json
├── analysis/
│   ├── construction.md
│   ├── serialization.md
│   ├── information-preservation.md
│   ├── commitments.md
│   ├── authentication.md
│   ├── negative-controls.md
│   └── final-analysis.md
└── final-report.md
```

Additional files may be added if the actual implementation requires them.

The evidence structure should follow the experiment rather than forcing the experiment into a predetermined file structure.

---

# 19. Acceptance Criteria

The experiment succeeds at the engineering level if it demonstrates all of the following:

### A. Valid Construction

A valid `PrismInput` can be constructed from the defined native-state representation.

### B. Deterministic Representation

Identical controlled inputs produce identical deterministic representations.

### C. Commitment Consistency

The recorded commitments correspond to the data they are intended to represent.

### D. Information Preservation

Required information survives the normalization/input boundary according to the defined design.

### E. Valid Acceptance

A valid input crosses the intended PrismChain boundary successfully.

### F. Invalid Rejection

Defined invalid inputs are detected and rejected.

### G. Reproducibility

An independent repeat produces the expected equivalent result.

### H. Clear Security Boundary

The evidence does not overclaim authentication as consensus or finality.

---

# 20. Failure Conditions

The experiment must be considered unsuccessful or incomplete if:

* identical inputs produce unexplained different commitments
* valid inputs cannot be accepted
* invalid inputs are accepted without explanation
* commitments do not correspond to their intended data
* required information is silently lost
* serialization is ambiguous
* authentication is represented as consensus without supporting evidence
* the experiment depends on undocumented manual intervention
* results cannot be independently reproduced
* the test relies solely on mocked behavior when the actual boundary is available
* synthetic native-state data is presented as authentic blockchain state

A failure is evidence.

It should be recorded rather than hidden.

---

# 21. Results Classification

Results should use the PrismChain evidence status system.

```text
🟢 BUILT / DEMONSTRATED
The behavior was implemented and demonstrated.

🔵 RESEARCH
The behavior or interpretation requires further investigation.

🟣 EXPERIMENTAL
The behavior has been tested experimentally but is not yet established.

🟡 HYPOTHESIS / PLANNED
The behavior is proposed but not yet demonstrated.

🔴 PRIVATE
Implementation details are intentionally withheld.

⚪ HISTORICAL
The material describes an earlier implementation or experiment.
```

The final report must distinguish these states.

---

# 22. Expected Evidence Chain

The experiment should ultimately establish this limited claim:

```text
EXTERNAL NATIVE STATE
        ↓
NORMALIZATION
        ↓
PrismInput
        ↓
VALIDATION
        ↓
PRISMCHAIN ACCEPTANCE
```

It should **not** jump directly from that result to:

```text
Ethereum state
      ↓
Ethereum finality
      ↓
PrismChain truth
      ↓
settlement
```

Those are separate claims requiring separate evidence.

---

# 23. Relationship to Experiment 12

Experiment 11 establishes the **input side**.

Experiment 12 will establish the **output side**.

Together:

```text
NATIVE STATE
     ↓
PrismInput
     ↓
PRISMCHAIN
     ↓
PrismOutput
```

Experiment 13 will then test whether the computational identity remains continuous across that entire path:

```text
PrismInput
     ↓
7-LAYER COMPUTATION
     ↓
WHITE LIGHT BLOCK
     ↓
PrismOutput
```

This separation prevents us from claiming that an input was correctly accepted merely because an output was produced.

---

# 24. Final Principle

> **Do not call an external state a PrismInput merely because it has been placed inside a PrismInput structure. Construct the input, define what it represents, serialize it, verify its commitments, test its integrity, attempt to break it, pass it through the actual boundary, and record exactly what the system accepts and rejects.**

**The input boundary must be demonstrated, not assumed.**
