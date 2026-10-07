# ⛓️ Ethereum → Settlement

> **Settlement is the final external boundary where the PrismChain relationship is reconciled with what actually happened on Ethereum.**

This document defines the Ethereum-specific settlement model.

The central principle is:

> **PrismChain computes. PrismOutput represents. Rainbow Ring connects. Ethereum executes and settles. Evidence proves what happened.**

Settlement must therefore remain an external-system property.

---

# 1. Purpose

Settlement answers a fundamentally different question from computation.

PrismChain asks:

> **What result did the seven-layer blockchain compute?**

PrismOutput asks:

> **What result is being presented to the external relationship?**

Rainbow Ring asks:

> **What is the state of the relationship between that result and the external system?**

Ethereum asks:

> **What actually happened on Ethereum?**

Settlement answers:

> **Has the external relationship reached the defined settled state according to Ethereum's applicable rules and the evidence available to us?**

---

# 2. Complete Ethereum Path

The complete integration is:

```text id="7s8v4k"
ETHEREUM
    ↓
NATIVE STATE
    ↓
ETHEREUM NATIVE CONDUIT
    ↓
PrismInput
    ↓
PRISMCHAIN
    ↓
WHITE LIGHT BLOCK
    ↓
PrismOutput
    ↓
RAINBOW RING
    ↓
ETHEREUM EXECUTION
    ↓
ETHEREUM EVIDENCE
    ↓
SETTLEMENT
```

Settlement is therefore the end of the relationship path, not the beginning.

---

# 3. Settlement Is Not Computation

The White Light Block represents PrismChain computation.

It does not represent Ethereum settlement.

```text id="x7f2c1p"
WHITE LIGHT BLOCK
        ≠
ETHEREUM SETTLEMENT
```

A valid WLB can exist even if:

* no Ethereum action has been attempted,
* execution failed,
* the transaction remains pending,
* the transaction was reorganized,
* or settlement requirements have not been satisfied.

---

# 4. Settlement Is Not PrismOutput

PrismOutput represents the result at the external boundary.

```text id="k9d4vm"
PrismOutput
      ≠
Settlement
```

A valid PrismOutput establishes what PrismChain is presenting.

It does not establish that Ethereum accepted, executed, or finalized the corresponding external action.

---

# 5. Settlement Is Not Rainbow Ring

Rainbow Ring manages the relationship.

```text id="m3x8qz"
PrismOutput
      ↓
Rainbow Ring
      ↓
Ethereum
```

The Ring observes and manages the relationship.

It does not manufacture Ethereum settlement.

Its settlement state must be derived from appropriate external evidence.

---

# 6. Settlement Is an External Property

Ethereum remains sovereign over Ethereum.

Therefore:

```text id="p5n2yr"
PRISMCHAIN
    ↓
computes

RAINBOW RING
    ↓
connects / observes

ETHEREUM
    ↓
executes / settles
```

PrismChain cannot create Ethereum finality.

Rainbow Ring cannot override Ethereum's rules.

A commitment cannot declare Ethereum settled.

The external system remains the source of truth for its own execution and settlement.

---

# 7. Settlement State Progression

A useful conceptual progression is:

```text id="8c4v6m"
COMPUTED
    ↓
OUTPUT
    ↓
READY
    ↓
SUBMITTED
    ↓
INCLUDED
    ↓
EXECUTED
    ↓
CONFIRMED
    ↓
SETTLED
```

These states must not be collapsed into one state.

Each represents a different stage of the external relationship.

---

# 8. COMPUTED

`COMPUTED` means PrismChain has produced its result.

```text id="q4n7xz"
Seven Layers
      ↓
White Light Block
      ↓
COMPUTED
```

This establishes a PrismChain result.

It says nothing about Ethereum execution.

---

# 9. OUTPUT

`OUTPUT` means the PrismChain result has been represented through PrismOutput.

```text id="w8p3kc"
WLB
 ↓
PrismOutput
 ↓
OUTPUT
```

This establishes the external output boundary.

It still does not mean that Ethereum has executed anything.

---

# 10. READY

`READY` means the relationship has satisfied the conditions necessary to proceed toward external execution.

Conceptually:

```text id="t6v1qa"
PrismOutput
    ↓
conditions evaluated
    ↓
READY
```

The exact conditions are implementation-dependent.

They may include:

* valid commitments,
* valid relationship identity,
* current external state,
* valid execution conditions,
* non-expired output,
* replay protection,
* and other requirements.

---

# 11. SUBMITTED

`SUBMITTED` means an external action has actually been submitted to Ethereum.

This is not execution.

```text id="a9k5fz"
SUBMITTED
    ≠
EXECUTED
```

A submitted transaction can fail.

It can remain pending.

It can become stale.

It can be replaced or otherwise become irrelevant to the intended relationship.

Submission is therefore evidence of an attempt, not proof of success.

---

# 12. INCLUDED

`INCLUDED` means the relevant Ethereum transaction has been observed as included in an Ethereum block.

This is stronger than submission.

It still does not automatically mean:

* successful execution,
* finality,
* or settlement.

The relationship must continue to inspect the applicable Ethereum evidence.

---

# 13. EXECUTED

`EXECUTED` means the relevant Ethereum action actually executed according to the applicable external evidence.

Execution should not be inferred merely from transaction submission or inclusion.

Where appropriate, execution evidence may include:

* transaction receipt,
* execution status,
* relevant logs,
* resulting state,
* or other Ethereum-native evidence.

The exact evidence model is implementation-dependent.

---

# 14. CONFIRMED

`CONFIRMED` represents an additional confidence or confirmation state established by the integration's defined Ethereum policy.

The exact meaning must be explicitly defined by implementation.

It must not be used as a vague synonym for:

* submitted,
* included,
* executed,
* or settled.

A confirmation policy should state what evidence is required.

---

# 15. SETTLED

`SETTLED` is the final relationship state.

It means that the applicable Ethereum-side settlement conditions have been satisfied and sufficient external evidence exists to establish that outcome.

Conceptually:

```text id="r7x2mh"
PrismOutput
      ↓
Rainbow Ring
      ↓
Ethereum Action
      ↓
Ethereum Evidence
      ↓
Settlement Conditions
      ↓
SETTLED
```

Settlement is therefore evidence-driven.

---

# 16. The No-Silent-Settlement Rule

The fundamental rule is:

> **Do not call something settled because PrismChain says it is settled.**

PrismChain computes.

It does not determine Ethereum settlement.

Likewise:

> **Do not call something executed because it was submitted.**

And:

> **Do not call something final because it was included.**

Each claim requires the appropriate evidence.

---

# 17. Ethereum Evidence

The settlement process should eventually consume Ethereum-native evidence.

Depending on the final implementation, this may include:

```text id="b2q8yx"
Transaction Identity
        ↓
Block Inclusion
        ↓
Transaction Receipt
        ↓
Execution Status
        ↓
Logs / Events
        ↓
Resulting State
        ↓
Confirmation / Finality Evidence
```

Not every relationship will necessarily require every evidence type.

The implementation must determine the minimum sufficient evidence for each settlement condition.

---

# 18. Transaction Identity

The relationship must be able to identify the external Ethereum action associated with the PrismOutput.

Conceptually:

```text id="c6m4vk"
PrismOutput
    ↓
Rainbow Ring
    ↓
Ethereum Transaction
```

The transaction identity must remain associated with the relationship being tracked.

This prevents external evidence from being accidentally attributed to the wrong output.

---

# 19. Block Inclusion

The Ring should distinguish:

```text id="y5t9ws"
Transaction Submitted
        ↓
Transaction Included
```

Submission proves that an attempt was made.

Inclusion establishes that Ethereum observed the transaction in a block.

Neither statement alone necessarily proves successful execution or final settlement.

---

# 20. Execution Status

Where Ethereum provides explicit execution status, the relationship should use that evidence.

Conceptually:

```text id="f1k8cq"
Transaction
    ↓
Receipt
    ↓
Execution Status
```

A transaction that was included but failed execution must not be represented as successful settlement.

---

# 21. Resulting State

Some relationships may require verification of the resulting Ethereum state.

For example:

```text id="m8p3vz"
Expected External Result
        ↓
Ethereum State
        ↓
Observed External Result
```

The exact state evidence required depends on the action being performed.

The architecture intentionally does not invent a universal Ethereum execution model before implementation establishes what the integration actually needs.

---

# 22. Confirmation and Finality

Confirmation and finality must remain distinct concepts.

A transaction may have:

* been submitted,
* been included,
* received confirmations,
* or reached the applicable Ethereum finality condition.

These states are not interchangeable.

The integration should explicitly define which condition is required before declaring settlement.

---

# 23. Finality Is External

Ethereum finality belongs to Ethereum's own consensus system.

Therefore:

```text id="s4j7np"
PrismChain Commitment
       ≠
Ethereum Finality
```

A PrismOutput can be completely valid while the corresponding Ethereum action has not reached the required finality condition.

The Ring must observe the external finality state rather than inventing one.

---

# 24. Reorganization

Ethereum state can change through chain reorganization.

The settlement model must therefore account for the possibility that an observed inclusion is later no longer part of the canonical chain.

Conceptually:

```text id="u7q2hf"
INCLUDED
   ↓
OBSERVED
   ↓
REORGANIZATION
   ↓
RE-EVALUATE
```

A relationship may therefore move into a state such as:

```text id="q9d3xm"
REORGED
```

when previously observed evidence is invalidated by the relevant external chain behavior.

The exact reorg policy must be determined through implementation.

---

# 25. Replay Protection

A settled relationship must not unintentionally become executable again.

Conceptually:

```text id="x6m1pz"
SETTLED
   ↓
Replay Attempt
   ↓
REJECTED
```

The final implementation may use:

* relationship identity,
* input commitment,
* result commitment,
* execution state,
* consumed-output tracking,
* expiration,
* or other controls.

The important requirement is behavioral:

> **A completed relationship must not silently authorize unintended repeated execution.**

---

# 26. Stale Results

A PrismOutput may be valid when created but become stale before execution.

For example:

```text id="h2w8cn"
PrismOutput
     ↓
time passes
     ↓
Ethereum state changes
     ↓
execution conditions change
     ↓
output must be re-evaluated
```

The Ring should not blindly execute stale results.

The implementation may establish:

* expiration,
* state references,
* freshness requirements,
* current-state checks,
* or other controls.

---

# 27. Expiration

An output may eventually have a defined validity window.

Conceptually:

```text id="v5r9kd"
VALID
  ↓
time
  ↓
EXPIRING
  ↓
EXPIRED
```

An expired output should not automatically remain executable.

The final expiration mechanism is implementation-dependent.

---

# 28. Failure

External execution may fail.

The relationship must represent failure explicitly.

```text id="n7c4yx"
READY
  ↓
SUBMITTED
  ↓
EXECUTION FAILURE
  ↓
FAILED
```

A failed external action must not be converted into:

```text id="x1m6qb"
SETTLED
```

simply because the original PrismOutput was valid.

---

# 29. Cancellation

A relationship may also be cancelled before execution or settlement.

Conceptually:

```text id="j4p8tz"
READY
   ↓
CANCELLED
```

Cancellation must remain distinguishable from:

* failure,
* expiration,
* rejection,
* and settlement.

---

# 30. Dispute

A relationship may eventually require a dispute state where available evidence does not establish the expected outcome.

Conceptually:

```text id="a8k2qf"
EXPECTED RESULT
      ↓
CONFLICTING / INSUFFICIENT EVIDENCE
      ↓
DISPUTED
```

The exact dispute mechanism is outside the current architecture definition.

The important principle is that uncertainty should remain visible.

---

# 31. Settlement State Machine

The broader Rainbow Ring relationship can therefore be represented as:

```text id="c7m5zn"
CREATED
   ↓
IDENTIFIED
   ↓
BOUND
   ↓
VALIDATED
   ↓
CONDITIONED
   ↓
READY
   ↓
EXECUTING
   ↓
OBSERVED
   ↓
CONFIRMED
   ↓
SETTLED
```

Exceptional states include:

```text id="w2q9pk"
REJECTED
EXPIRED
FAILED
CANCELLED
REORGED
DISPUTED
```

The actual implementation may refine this state machine.

---

# 32. Settlement Evidence Chain

The settlement relationship should ultimately be traceable:

```text id="m9x4qv"
Ethereum Native State
        ↓
nativeStateCommitment
        ↓
PrismInput
        ↓
inputCommitment
        ↓
PrismChain
        ↓
White Light Block
        ↓
resultCommitment
        ↓
PrismOutput
        ↓
Rainbow Ring
        ↓
Ethereum Transaction
        ↓
Ethereum Evidence
        ↓
Settlement
```

This creates a complete provenance path.

---

# 33. Bidirectional Traceability

The relationship should work in both directions.

Forward:

```text id="p4z8ks"
Ethereum State
    ↓
PrismInput
    ↓
PrismChain
    ↓
WLB
    ↓
PrismOutput
    ↓
Ethereum Action
```

Backward:

```text id="t6c2ny"
Ethereum Settlement Evidence
    ↓
Ethereum Action
    ↓
Rainbow Ring
    ↓
PrismOutput
    ↓
WLB
    ↓
PrismInput
    ↓
Ethereum State
```

The objective is not merely to create a transaction.

It is to preserve the relationship surrounding that transaction.

---

# 34. Settlement Does Not Rewrite PrismChain

Ethereum settlement does not change what PrismChain computed.

The WLB remains the PrismChain result.

Ethereum evidence establishes what happened externally.

Therefore:

```text id="q5v8mb"
PRISMCHAIN RESULT
        +
ETHEREUM OUTCOME
```

are related but distinct facts.

One does not overwrite the other.

---

# 35. Settlement Does Not Rewrite Ethereum

Likewise, PrismChain cannot reinterpret Ethereum's external state merely to make the relationship appear successful.

If Ethereum rejects an action:

```text id="b8k3wr"
Ethereum
   ↓
REJECTED
```

the Ring must represent that outcome.

If execution fails:

```text id="f6x1qy"
Ethereum
   ↓
FAILED
```

the Ring must represent that outcome.

If finality requirements are not satisfied:

```text id="z2m7pc"
Ethereum
   ↓
NOT FINAL
```

the relationship remains unresolved.

---

# 36. Settlement Conditions

The final settlement condition should be explicit.

Conceptually:

```text id="u8x5mv"
VALID PRISMOUTPUT
        +
VALID RELATIONSHIP
        +
VALID EXTERNAL ACTION
        +
VALID EXECUTION EVIDENCE
        +
REQUIRED CONFIRMATION / FINALITY
        ↓
SETTLED
```

The exact required evidence is an implementation decision.

The principle is that settlement must have an objectively defined basis.

---

# 37. Ethereum Sovereignty

The external blockchain remains sovereign.

Ethereum determines:

* whether transactions are accepted,
* whether transactions execute,
* what state results,
* how blocks are produced,
* and what finality means under Ethereum's own rules.

Rainbow Ring observes these facts.

PrismChain does not replace them.

---

# 38. Security Requirements

The Ethereum settlement implementation should eventually demonstrate protection against:

### Wrong-chain execution

An output for Ethereum cannot silently execute against another chain.

### Replay

A completed relationship cannot unintentionally execute again.

### Stale output

Old results cannot bypass current validity requirements.

### Reorganization

Previously observed external state can be re-evaluated when necessary.

### False settlement

Internal state cannot declare settlement without required external evidence.

### Failed execution

Failed Ethereum execution cannot be recorded as successful settlement.

### Incorrect attribution

Evidence from one Ethereum transaction cannot be attached to another PrismOutput.

### Missing evidence

Incomplete evidence cannot silently become settlement.

---

# 39. Testing Strategy

Settlement testing should occur at multiple levels.

```text id="c2q7xm"
UNIT TESTS
    ↓
RELATIONSHIP TESTS
    ↓
COMMITMENT TESTS
    ↓
EXECUTION TESTS
    ↓
REORG TESTS
    ↓
REPLAY TESTS
    ↓
EXTERNAL ETHEREUM TESTS
    ↓
END-TO-END SETTLEMENT
```

Each layer should establish evidence for the next.

---

# 40. Unit Tests

Unit testing should establish:

* settlement-state transitions,
* valid and invalid evidence,
* expiration handling,
* replay handling,
* commitment verification,
* serialization behavior,
* and failure-state handling.

---

# 41. Integration Tests

Integration tests should establish:

```text id="v8m4zs"
PrismOutput
    ↓
Rainbow Ring
    ↓
Ethereum Action
    ↓
Observed Evidence
    ↓
Settlement State
```

The test must verify that internal relationship state changes only when the required conditions are actually satisfied.

---

# 42. Reorganization Tests

The integration should eventually simulate or observe a scenario where previously observed Ethereum state becomes non-canonical.

Expected behavior:

```text id="h5x2nr"
OBSERVED
   ↓
REORG DETECTED
   ↓
RE-EVALUATE
   ↓
REORGED / PENDING / OTHER VALID STATE
```

The exact final state depends on the implementation.

The key requirement is that the Ring does not silently preserve invalidated external evidence.

---

# 43. Replay Tests

A completed relationship should be subjected to a replay attempt.

Expected:

```text id="j9q3vc"
SETTLED
   ↓
REPLAY ATTEMPT
   ↓
REJECTED
```

This test should be performed against the actual relationship mechanism rather than merely asserting that replay protection exists.

---

# 44. Failure Tests

External failure must be represented explicitly.

Examples:

```text id="s6m1kw"
TRANSACTION REVERT
TRANSACTION FAILURE
INVALID CONDITIONS
EXPIRED OUTPUT
WRONG CHAIN
MISSING EVIDENCE
STALE STATE
REORG
```

The expected result must be a defined non-settled state.

---

# 45. End-to-End Ethereum Test

The final proof target is:

```text id="p7c4yz"
ETHEREUM STATE
      ↓
NATIVE CONDUIT
      ↓
PrismInput
      ↓
PRISMCHAIN
      ↓
WHITE LIGHT BLOCK
      ↓
PrismOutput
      ↓
RAINBOW RING
      ↓
ETHEREUM TRANSACTION
      ↓
ETHEREUM EXECUTION
      ↓
ETHEREUM EVIDENCE
      ↓
SETTLEMENT
```

This should eventually be demonstrated with real evidence.

The goal is not simply to show that the contracts compile.

The goal is to show that the entire relationship works.

---

# 46. Evidence Over Assertion

A successful settlement demonstration should preserve evidence sufficient to answer:

```text id="g1q6nv"
What Ethereum state entered PrismChain?
        ↓
What PrismInput was constructed?
        ↓
What PrismChain result was produced?
        ↓
What PrismOutput represented it?
        ↓
What relationship did Rainbow Ring establish?
        ↓
What Ethereum action occurred?
        ↓
What evidence proves the action?
        ↓
Why is the relationship considered settled?
```

This is the standard of evidence the integration should aim toward.

---

# 47. What Settlement Proves

A successfully verified settlement relationship can establish that:

1. A defined Ethereum state was associated with the input.
2. A PrismInput was constructed from that relationship.
3. PrismChain produced a result.
4. The result was represented through PrismOutput.
5. Rainbow Ring established the external relationship.
6. An Ethereum action occurred.
7. Appropriate Ethereum evidence was observed.
8. The defined settlement conditions were satisfied.

The exact claims depend on the evidence actually collected.

---

# 48. What Settlement Does Not Prove

A successful settlement does not automatically prove that:

* PrismChain is universally superior to other blockchains,
* every Ethereum state was independently consensus-verified by PrismChain,
* every possible cross-chain scenario is secure,
* the architecture is free of all vulnerabilities,
* or the system can generalize to every other blockchain without additional work.

Claims should remain proportional to evidence.

---

# 49. Current Ethereum Status

🟣 **Experimental / active integration**

The architecture currently defines:

* external settlement as an Ethereum-side property,
* Rainbow Ring settlement relationship,
* execution/evidence distinctions,
* settlement-state progression,
* reorg handling requirements,
* replay requirements,
* stale-output requirements,
* failure states,
* and end-to-end testing objectives.

The complete Ethereum settlement path remains an implementation and testing target.

---

# 50. What Is Defined

🟢 **Defined**

* Ethereum remains sovereign over settlement.
* PrismChain computes the result.
* PrismOutput represents the result.
* Rainbow Ring manages the relationship.
* External Ethereum evidence establishes execution state.
* Settlement is distinct from submission, inclusion, execution, and confirmation.
* Reorganizations must be handled explicitly.
* Replay and stale-output conditions must be considered.
* Failed execution must not become successful settlement.
* Settlement requires defined external evidence.

---

# 51. What Remains to Be Proven

🔵 **To be proven through implementation**

* Exact Ethereum execution mechanism.
* Exact Ethereum evidence model.
* Required confirmation/finality threshold.
* Complete settlement-state implementation.
* Reorganization handling.
* Replay protection.
* Stale-output handling.
* Expiration behavior.
* Failure recovery.
* End-to-end Ethereum settlement.
* Complete evidence preservation.

---

# 52. What Is Not Being Claimed

This architecture does not claim that PrismChain or Rainbow Ring:

* controls Ethereum,
* creates Ethereum consensus,
* creates Ethereum finality,
* creates Ethereum settlement,
* or independently guarantees external execution.

Ethereum remains the authority for Ethereum's own state and execution.

---

# 53. Implementation Discovery

The settlement architecture is intentionally precise about **what must be proven** while remaining open about **how the final implementation achieves it**.

The development process remains:

```text id="n5q8xm"
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

Implementation may reveal that:

* additional evidence is required,
* a state needs to be split,
* a commitment needs additional context,
* reorg handling needs another transition,
* or settlement conditions need refinement.

When that happens, the implementation and tests should determine the final architecture.

The documentation should then be updated to match what is actually built.

---

# 54. Public / Private Boundary

Public documentation should expose:

* settlement architecture,
* state distinctions,
* evidence requirements,
* security properties,
* testing methodology,
* demonstrated behavior,
* and known limitations.

It should not expose proprietary implementation details unnecessarily.

The principle remains:

> **Reveal the architecture. Protect the advantage.**

---

# 55. The Complete Ethereum Relationship

The complete relationship is:

```text id="v1s8qy"
┌───────────────────────────────┐
│          ETHEREUM             │
│                               │
│ Native State                  │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│      NATIVE CONDUIT           │
│       PRISM-ETH-01            │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│         PrismInput            │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│         PRISMCHAIN             │
│                               │
│ RED ORANGE YELLOW GREEN       │
│ BLUE INDIGO VIOLET            │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│      WHITE LIGHT BLOCK        │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│         PrismOutput           │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│        RAINBOW RING           │
│                               │
│ Relationship / Observation    │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│          ETHEREUM             │
│                               │
│ Execution / Evidence          │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│          SETTLEMENT           │
└───────────────────────────────┘
```

---

# 56. Final Principles

**PrismChain computes.**

**The seven layers produce the White Light Block.**

**PrismOutput represents the result.**

**Rainbow Ring establishes and manages the relationship.**

**Ethereum executes according to Ethereum's own rules.**

**Ethereum provides the evidence of what happened on Ethereum.**

**Settlement is determined from that external evidence.**

**Commitment is not consensus.**

**Authentication is not consensus.**

**Consensus is not finality.**

**Submission is not execution.**

**Inclusion is not automatically settlement.**

**PrismChain cannot declare Ethereum settled.**

**Rainbow Ring cannot manufacture Ethereum truth.**

**Do not call something settled because PrismChain says it is settled.**

**Do not call something executed because it was submitted.**

**Do not call something final because it was included.**

The governing model is:

```text id="w8m2jc"
PRISMCHAIN
    ↓
COMPUTES

PrismOutput
    ↓
REPRESENTS

RAINBOW RING
    ↓
CONNECTS / OBSERVES

ETHEREUM
    ↓
EXECUTES / SETTLES

EVIDENCE
    ↓
PROVES WHAT HAPPENED
```

> **Connect systems without confusing them.**
