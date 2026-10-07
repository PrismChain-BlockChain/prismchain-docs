# 🌈 Rainbow Ring — PrismOutput

> **PrismOutput is the formal output boundary through which the unified result of PrismChain computation becomes available to Rainbow Ring and the external system.**

PrismChain is the seven-layer blockchain.

PrismChain computes.

The seven spectral layers converge into the White Light Block.

PrismOutput represents that result at the external boundary.

Rainbow Ring establishes the relationship between that result and the sovereign external system.

The external blockchain executes and settles according to its own rules.

The complete path is:

```text
NATIVE BLOCKCHAIN
       │
       ▼
  NATIVE STATE
       │
       ▼
NATIVE CONDUIT
       │
       ▼
   PrismInput
       │
       ▼
   PRISMCHAIN
       │
       ▼
WHITE LIGHT BLOCK
       │
       ▼
  PrismOutput
       │
       ▼
 RAINBOW RING
       │
       ▼
EXTERNAL EXECUTION
       │
       ▼
   SETTLEMENT
```

---

# 1. Purpose

This document defines the role of **PrismOutput** within the Rainbow Ring architecture.

It explains:

* how the White Light Block becomes an external-facing result,
* what PrismOutput represents,
* how the output remains bound to its originating input,
* how Rainbow Ring uses the output,
* how execution conditions participate in the relationship,
* and where PrismChain responsibility ends and external execution begins.

PrismOutput is a boundary.

It is not:

* a second White Light Block,
* a second computation engine,
* Rainbow Ring itself,
* external execution,
* or settlement.

---

# 2. Position in the Architecture

PrismOutput sits directly between PrismChain computation and the Rainbow Ring relationship layer.

```text
PRISMCHAIN
    │
    ▼
WHITE LIGHT BLOCK
    │
    ▼
PrismOutput
    │
    ▼
RAINBOW RING
    │
    ▼
EXTERNAL SYSTEM
```

This is the fundamental output boundary.

---

# 3. The White Light Block Comes First

PrismOutput does not replace the White Light Block.

The computational sequence remains:

```text
RED
ORANGE
YELLOW
GREEN
BLUE
INDIGO
VIOLET
   │
   ▼
WHITE LIGHT BLOCK
   │
   ▼
PrismOutput
```

The WLB is the unified result of the seven-layer PrismChain computation.

PrismOutput exposes that result at the external boundary.

---

# 4. PrismOutput Is Not the White Light Block

These are separate concepts:

```text
WHITE LIGHT BLOCK
      ≠
PrismOutput
```

The White Light Block belongs to PrismChain.

PrismOutput belongs to the boundary between PrismChain and the surrounding relationship architecture.

The output should reference or commit to the actual WLB rather than creating another computational result.

---

# 5. PrismOutput Is Not Rainbow Ring

Likewise:

```text
PrismOutput
      ≠
Rainbow Ring
```

PrismOutput represents the result.

Rainbow Ring establishes and manages the relationship around that result.

Conceptually:

```text
WLB
 ↓
PrismOutput
 ↓
Rainbow Ring
 ↓
External System
```

---

# 6. Current PrismOutput Structure

The current public PrismOutput structure is:

```text
PrismOutput.Data
├── inputCommitment
├── rulesCommitment
├── resultCommitment
└── executionConditions
```

Each field represents a different part of the output relationship.

---

# 7. inputCommitment

`inputCommitment` binds the output to the PrismInput that initiated the computation.

Conceptually:

```text
PrismInput
     │
     ▼
inputCommitment
     │
     ▼
PRISMCHAIN
     │
     ▼
PrismOutput
```

This allows the output to remain connected to its originating input.

The relationship should not become an anonymous result detached from its source.

---

# 8. Input-to-Output Continuity

The intended relationship is:

```text
NATIVE STATE
     ↓
nativeStateCommitment
     ↓
PrismInput
     ↓
inputCommitment
     ↓
PRISMCHAIN
     ↓
WHITE LIGHT BLOCK
     ↓
PrismOutput
```

This creates a traceable computational path.

The output can therefore be understood in the context of the input that produced it.

---

# 9. rulesCommitment

`rulesCommitment` binds the output to the rules or execution context associated with the result.

Conceptually:

```text
RULES / CONTEXT
      ↓
rulesCommitment
      ↓
PrismOutput
```

This prevents the output from being interpreted without regard to the conditions under which it was produced.

The precise rules represented by the commitment remain an implementation question.

---

# 10. resultCommitment

`resultCommitment` binds the output to the actual PrismChain result.

The intended relationship is:

```text
WHITE LIGHT BLOCK
       │
       ▼
resultCommitment
       │
       ▼
PrismOutput
```

This is critical.

The result commitment should ultimately correspond to the **actual White Light Block produced by PrismChain**.

PrismOutput must not introduce a separate computation engine merely to create an output result.

---

# 11. Execution Conditions

`executionConditions` describes the conditions under which the external relationship may proceed.

Conceptually:

```text
PrismOutput
     │
     ├── inputCommitment
     ├── rulesCommitment
     ├── resultCommitment
     │
     └── executionConditions
```

These conditions become relevant to Rainbow Ring.

They do not mean that PrismChain has already executed the external action.

---

# 12. The Output Boundary

The complete output boundary is:

```text
PRISMCHAIN
    │
    ▼
WHITE LIGHT BLOCK
    │
    ▼
RESULT COMMITMENT
    │
    ▼
PrismOutput
    │
    ▼
RAINBOW RING
    │
    ▼
EXECUTION CONDITIONS
    │
    ▼
EXTERNAL EXECUTION
```

PrismOutput is therefore the controlled transition from computation to relationship.

---

# 13. PrismOutput Does Not Execute

A PrismOutput does not itself execute a transaction on another blockchain.

Therefore:

```text
PrismOutput
      ≠
External Execution
```

The output represents what PrismChain produced.

The external system determines what actually executes.

---

# 14. PrismOutput Does Not Settle

Likewise:

```text
PrismOutput
      ≠
Settlement
```

A valid output does not prove that anything happened externally.

The external action must actually occur.

The resulting state must then be observed.

---

# 15. PrismOutput and Rainbow Ring

Rainbow Ring consumes the output boundary as the basis for a relationship.

Conceptually:

```text
WHITE LIGHT BLOCK
       ↓
PrismOutput
       ↓
RAINBOW RING
       ↓
External Relationship
```

Rainbow Ring can then associate the output with:

* an external system,
* a relationship identity,
* execution conditions,
* external state,
* execution status,
* and eventual settlement evidence.

The final implementation must determine the exact mechanism.

---

# 16. The Complete Round Trip

The complete architecture becomes:

```text
NATIVE BLOCKCHAIN
       │
       ▼
  NATIVE STATE
       │
       ▼
NATIVE CONDUIT
       │
       ▼
   PrismInput
       │
       ▼
   PRISMCHAIN
       │
       ▼
WHITE LIGHT BLOCK
       │
       ▼
  PrismOutput
       │
       ▼
 RAINBOW RING
       │
       ▼
EXTERNAL EXECUTION
       │
       ▼
   SETTLEMENT
```

This is the intended end-to-end relationship.

---

# 17. Relationship Identity

A PrismOutput should not exist in isolation from the external relationship it is intended to support.

Conceptually:

```text
PrismOutput
     +
External System Identity
     +
Conduit Identity
     +
Relationship Identity
```

These elements allow Rainbow Ring to determine what external system the output belongs to.

---

# 18. Native Identity

The output must preserve the identity of the external system.

For example:

```text
Ethereum PrismOutput
       ↓
Ethereum Rainbow Ring relationship
       ↓
Ethereum execution
```

An Ethereum output must not silently become a relationship with another chain.

---

# 19. Chain Identity

The broader relationship therefore includes:

```text
External Chain
      +
Native Conduit
      +
PrismInput
      +
PrismOutput
      +
Rainbow Ring
```

Chain identity should remain explicit throughout the lifecycle.

This becomes increasingly important as multiple Native Conduits are introduced.

---

# 20. Ethereum First

Ethereum is the first external system being integrated.

The intended path is:

```text
Ethereum
   ↓
Ethereum Native Conduit
   ↓
PrismInput
   ↓
PrismChain
   ↓
White Light Block
   ↓
PrismOutput
   ↓
Rainbow Ring
   ↓
Ethereum Execution
   ↓
Ethereum Settlement
```

The conduit identity currently planned for this relationship is:

```text
PRISM-ETH-01
```

This is an integration target, not a production settlement claim.

---

# 21. PrismOutput and Ethereum

The Ethereum relationship should eventually be able to establish:

```text
Ethereum Native State
        ↓
PrismInput
        ↓
PrismChain computation
        ↓
White Light Block
        ↓
PrismOutput
        ↓
Rainbow Ring
        ↓
Ethereum execution
```

The output should remain traceable to the Ethereum input state from which the relationship originated.

---

# 22. No Invented Ethereum Execution Model

This document does not define an execution mechanism that has not been implemented.

The exact Ethereum execution path must be discovered through:

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

The architecture describes the boundary.

Implementation determines the final mechanics.

---

# 23. Execution Conditions

Execution conditions are an important separation between:

```text
RESULT
```

and:

```text
ACTION
```

The PrismChain result can establish what computation produced.

The execution conditions establish what must be true before an external action should occur.

Therefore:

```text
COMPUTED RESULT
      +
EXECUTION CONDITIONS
      ↓
RELATIONSHIP
```

---

# 24. Conditions Are Not Execution

Satisfied conditions do not mean execution has already happened.

The progression remains:

```text
PrismOutput
     ↓
Conditions Evaluated
     ↓
READY
     ↓
External Execution
     ↓
Observed Result
     ↓
Settlement
```

This distinction is necessary for accurate evidence.

---

# 25. External State at Execution Time

The state represented by PrismInput may differ from the state present when execution is attempted.

Therefore the relationship may eventually need:

```text
INPUT-TIME STATE
       ↓
PrismInput
       ↓
COMPUTATION
       ↓
PrismOutput
       ↓
EXECUTION-TIME STATE
       ↓
EXECUTION
```

The final architecture must determine which execution conditions require fresh external state.

---

# 26. Stale Outputs

A PrismOutput may become stale.

For example:

```text
PrismOutput
     ↓
TIME PASSES
     ↓
External State Changes
     ↓
Original Conditions No Longer Hold
```

Rainbow Ring must eventually determine whether the relationship should:

* continue,
* pause,
* revalidate,
* expire,
* reject,
* or require a new output.

The correct behavior must be established through testing.

---

# 27. Reorganization

External blockchain reorganizations may affect output validity.

Conceptually:

```text
PrismOutput
     ↓
External Chain State
     ↓
REORGANIZATION
     ↓
State / Context Changes
     ↓
Relationship Re-evaluation
```

A relationship must not assume that an external state remains canonical merely because it was previously observed.

---

# 28. Replay Protection

A PrismOutput should not automatically be executable multiple times.

The relationship must eventually distinguish:

```text
NEW OUTPUT
      ≠
ALREADY EXECUTED OUTPUT
```

Relevant identity can include:

* input commitment,
* result commitment,
* relationship identity,
* external system identity,
* execution context,
* and settlement state.

The exact replay mechanism remains an implementation and security question.

---

# 29. Output Expiration

Some relationships may require expiration.

Conceptually:

```text
CREATED
   ↓
READY
   ↓
TIME LIMIT
   ↓
EXPIRED
```

An expired output should not silently become executable again.

Whether expiration belongs directly in the output structure or is represented by the Ring relationship remains an implementation question.

---

# 30. Commitment Chain

The commitment architecture can be represented as:

```text
NATIVE STATE
      │
      ▼
nativeStateCommitment
      │
      ▼
PrismInput
      │
      ▼
inputCommitment
      │
      ▼
PRISMCHAIN
      │
      ▼
WHITE LIGHT BLOCK
      │
      ▼
resultCommitment
      │
      ▼
PrismOutput
```

Additional output context includes:

```text
rulesCommitment
executionConditions
```

Rainbow Ring then uses these relationships to establish the external relationship.

---

# 31. Commitment Is Not Authentication

A result commitment establishes a binding.

It does not automatically establish authenticity.

Therefore:

```text
COMMITMENT
      ≠
AUTHENTICATION
```

The system must keep those concepts separate.

---

# 32. Commitment Is Not Consensus

Likewise:

```text
COMMITMENT
      ≠
CONSENSUS
```

A valid PrismOutput commitment does not mean that the external blockchain has accepted the corresponding transaction or state.

---

# 33. Commitment Is Not Finality

Likewise:

```text
COMMITMENT
      ≠
FINALITY
```

An output can be validly constructed while the external action remains:

* pending,
* replaceable,
* reversible,
* reorganizable,
* or otherwise not final.

External finality must be established according to the external chain.

---

# 34. Commitment Is Not Settlement

Likewise:

```text
COMMITMENT
      ≠
SETTLEMENT
```

The output commits to a PrismChain result.

Settlement occurs only when the external system actually records the resulting state or action according to its own rules.

---

# 35. External Execution

The output relationship eventually reaches:

```text
PrismOutput
      ↓
Rainbow Ring
      ↓
External Execution
```

The exact execution mechanism is external-chain-specific.

Rainbow Ring should establish the relationship without pretending to be the external execution environment.

---

# 36. External Settlement

After execution:

```text
External Execution
      ↓
External State
      ↓
Observation
      ↓
Settlement Evidence
```

The external blockchain remains the authority over what happened on that system.

---

# 37. No Silent Success

The architecture requires a strict distinction between:

```text
SUBMITTED
```

and:

```text
EXECUTED
```

and:

```text
SETTLED
```

They are not interchangeable.

A submission is not proof of execution.

Execution is not automatically proof of finality.

A PrismOutput is not proof of settlement.

---

# 38. Settlement Evidence

A complete relationship should eventually produce evidence such as:

```text
PrismOutput
      ↓
Relationship Identity
      ↓
External Transaction / Action
      ↓
External Block / State Reference
      ↓
Observed Result
      ↓
Settlement Status
```

The exact evidence structure remains subject to implementation.

---

# 39. Result Verification

A key future test is:

> **Does `resultCommitment` actually bind to the White Light Block that PrismChain produced?**

The intended test relationship is:

```text
WLB
  ↓
resultCommitment
  ↓
PrismOutput
```

If the WLB changes, the corresponding result relationship should change.

This must be demonstrated experimentally.

---

# 40. Mutation Testing

The output boundary should be tested through controlled mutations.

For example:

```text
CHANGE inputCommitment
      ↓
EXPECTED: OUTPUT RELATIONSHIP INVALID
```

```text
CHANGE rulesCommitment
      ↓
EXPECTED: RULE CONTEXT INVALID
```

```text
CHANGE resultCommitment
      ↓
EXPECTED: RESULT BINDING INVALID
```

```text
CHANGE executionConditions
      ↓
EXPECTED: EXECUTION CONDITIONS RE-EVALUATED
```

These tests determine whether the fields actually provide the bindings they are intended to provide.

---

# 41. White Light Block Mutation

A particularly important experiment is:

```text
ORIGINAL
   ↓
White Light Block
   ↓
PrismOutput
```

Then change one component of the underlying WLB:

```text
CHANGE ONE LAYER INPUT
        ↓
LAYER HASH CHANGES
        ↓
WLB CHANGES
        ↓
RESULT COMMITMENT SHOULD CHANGE
        ↓
PrismOutput RELATIONSHIP SHOULD CHANGE
```

This would provide evidence that the output remains bound to the actual PrismChain result.

---

# 42. Input Mutation

Likewise:

```text
CHANGE PrismInput
       ↓
COMPUTATION CHANGES
       ↓
WLB SHOULD CHANGE
       ↓
PrismOutput SHOULD CHANGE
```

This provides a second direction of traceability.

---

# 43. Output Serialization

The current PrismOutput serializer uses a versioned representation.

Conceptually:

```text
VERSION
   +
inputCommitment
   +
rulesCommitment
   +
resultCommitment
   +
executionConditions
```

Canonical serialization matters because commitment values depend on deterministic representation.

---

# 44. Output Domain Separation

The output commitment architecture uses the distinct domain:

```text
PRISM_OUTPUT
```

This separates output commitments from input commitments.

Conceptually:

```text
PRISM_INPUT
     ≠
PRISM_OUTPUT
```

Domain separation helps prevent unrelated commitment types from becoming cryptographically ambiguous.

---

# 45. Relationship Lifecycle

PrismOutput enters the Rainbow Ring relationship lifecycle.

Conceptually:

```text
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

Possible failure states include:

```text
REJECTED
FAILED
EXPIRED
CANCELLED
REORGED
DISPUTED
```

These are relationship states.

They are not additional PrismOutput fields.

---

# 46. PrismOutput State vs Ring State

The architecture should preserve the distinction:

```text
PrismOutput
      ≠
Rainbow Ring relationship state
```

PrismOutput represents the result and execution context.

Rainbow Ring tracks the relationship around that output.

This prevents the output object from becoming an entire settlement engine.

---

# 47. One Output, One Relationship Context

An output should remain associated with a clearly identifiable relationship context.

Conceptually:

```text
PrismOutput
    │
    ├── External System
    ├── Conduit
    ├── Input
    ├── Result
    └── Conditions
```

This allows the Ring to determine what the output is intended to interact with.

---

# 48. Multi-Chain Output Isolation

As additional conduits are introduced:

```text
Ethereum PrismOutput
       ↓
Ethereum relationship

Bitcoin PrismOutput
       ↓
Bitcoin relationship

Solana PrismOutput
       ↓
Solana relationship
```

Outputs must not cross relationship boundaries accidentally.

---

# 49. PrismOutput Does Not Replace Native Conduits

The output boundary does not eliminate the need for a chain-specific Native Conduit.

The external system may require chain-specific:

* transaction construction,
* execution interfaces,
* state observation,
* authentication,
* finality handling,
* and settlement evidence.

Those requirements remain external-system-specific.

---

# 50. PrismOutput and Native Conduit Cooperation

The relationship may therefore involve the conduit on both sides of the complete integration:

```text
NATIVE INPUT SIDE
        │
        ▼
Native Conduit
        │
        ▼
PrismInput
        │
        ▼
PrismChain
        │
        ▼
PrismOutput
        │
        ▼
Rainbow Ring
        │
        ▼
Native / External Execution Interface
        │
        ▼
External State
```

The exact division between Ring and conduit on the output side must be determined through implementation.

The architectural rule is that native blockchain semantics remain native.

---

# 51. External Observation

After execution, the external system must be observed.

Conceptually:

```text
External Execution
       ↓
External State
       ↓
Observation
       ↓
Rainbow Ring
       ↓
Settlement Evidence
```

This prevents PrismChain from declaring an external event successful without external evidence.

---

# 52. The Source of Truth

Different components have different sources of truth.

```text
PRISMCHAIN
    ↓
PrismChain computation / WLB

EXTERNAL BLOCKCHAIN
    ↓
External execution / native state

RAINBOW RING
    ↓
Relationship state / evidence
```

No layer should claim authority over facts that belong to another layer.

---

# 53. Security Questions

Important output-side questions include:

* Does the output bind to the correct input?
* Does the result commitment bind to the actual WLB?
* Can an output be modified?
* Can an output be replayed?
* Can an output be routed to the wrong chain?
* Can stale execution conditions be accepted?
* Can a reorganized external state invalidate the relationship?
* Can submission be mistaken for execution?
* Can execution be mistaken for settlement?
* Can settlement be reported without external evidence?

Each question should eventually become a test.

---

# 54. Testing the Output Boundary

A useful testing progression is:

```text
TEST 1
Generate valid WLB
      ↓
TEST 2
Construct PrismOutput
      ↓
TEST 3
Verify result commitment
      ↓
TEST 4
Verify input commitment
      ↓
TEST 5
Validate execution conditions
      ↓
TEST 6
Bind output to Rainbow Ring
      ↓
TEST 7
Execute externally
      ↓
TEST 8
Observe external result
      ↓
TEST 9
Record settlement evidence
```

This isolates the output boundary before the complete end-to-end loop is trusted.

---

# 55. End-to-End Evidence

The strongest future demonstration will establish:

```text
NATIVE INPUT
      ↓
PrismInput
      ↓
SEVEN-LAYER COMPUTATION
      ↓
WHITE LIGHT BLOCK
      ↓
PrismOutput
      ↓
RAINBOW RING
      ↓
EXTERNAL EXECUTION
      ↓
EXTERNAL OBSERVATION
      ↓
SETTLEMENT
```

Every transition should be inspectable.

Every important claim should have evidence.

---

# 56. Architecture Must Follow Testing

The output specification is architectural guidance.

It is not a promise that every field or lifecycle state will remain unchanged after implementation.

The development process remains:

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

If testing reveals that the output needs a different representation:

**change it.**

If a field proves unnecessary:

**remove it.**

If another boundary becomes necessary:

**add it.**

If the external chain requires a different relationship:

**adapt it.**

The implementation should determine the final architecture.

---

# 57. Public / Private Boundary

Public documentation should expose:

* PrismOutput's architectural role,
* public structure,
* commitment relationships,
* execution conditions,
* testing methodology,
* relationship boundaries,
* and demonstrated behavior.

It should protect:

* proprietary execution mechanisms,
* undisclosed protocol logic,
* novel optimization,
* private security mechanisms,
* and unreleased implementation details.

The principle remains:

> **Reveal the architecture. Protect the advantage.**

---

# 58. Current Status

PrismOutput is:

**🟢 Architecturally Defined**

The public output boundary and current data structure are defined.

**🟣 Experimentally Implemented**

Prototype boundary components exist.

**🔵 Under Integration Testing**

The relationship between the actual WLB, PrismOutput, Rainbow Ring, and external execution is still being established.

**🟡 Not Yet Proven**

Production external execution, finality handling, replay protection, and settlement evidence remain unproven.

---

# 59. What Is Established

The architecture establishes:

```text
PRISMCHAIN
    ↓
WHITE LIGHT BLOCK
    ↓
PrismOutput
    ↓
RAINBOW RING
    ↓
EXTERNAL EXECUTION
    ↓
SETTLEMENT
```

It also establishes that:

* WLB is the actual PrismChain result,
* PrismOutput represents that result at the boundary,
* `resultCommitment` should bind to the actual WLB,
* `inputCommitment` preserves input traceability,
* `rulesCommitment` preserves execution context,
* `executionConditions` define requirements for external execution,
* Rainbow Ring manages the relationship,
* and the external blockchain remains authoritative for external execution and settlement.

---

# 60. What Is Not Yet Proven

This document does not claim:

* production Rainbow Ring execution,
* production Ethereum execution,
* production settlement,
* complete Ethereum finality handling,
* complete replay protection,
* complete reorganization handling,
* decentralized observation,
* or production security.

Those require implementation and evidence.

---

# 61. The Output Principle

PrismOutput exists to make the end of PrismChain computation explicit.

It should answer:

> **What did PrismChain produce?**

> **Which input produced it?**

> **Which rules or context govern the result?**

> **What conditions apply to external execution?**

> **Which external system is this result intended to relate to?**

> **Can the external outcome eventually be observed and proven?**

---

# 62. Final Architecture

```text
                    NATIVE BLOCKCHAIN
                           │
                           ▼
                      NATIVE STATE
                           │
                           ▼
                    NATIVE CONDUIT
                           │
                           ▼
                       PrismInput
                           │
                           ▼
                      PRISMCHAIN
                           │
                           ▼
                  WHITE LIGHT BLOCK
                           │
                           ▼
                      PrismOutput
                           │
                           ▼
                    RAINBOW RING
                           │
                           ▼
                  EXTERNAL EXECUTION
                           │
                           ▼
                      SETTLEMENT
                           │
                           ▼
                   EXTERNAL STATE
```

The White Light Block is the unified PrismChain result.

PrismOutput represents that result at the external boundary.

Rainbow Ring establishes and manages the relationship.

The external blockchain executes according to its own rules.

Settlement is established by observing the external system.

---

# 63. Final Principles

> **Bind the output to the actual PrismChain result.**

> **Preserve the connection to the originating input.**

> **Keep execution conditions explicit.**

> **Do not confuse output with execution.**

> **Do not confuse execution with settlement.**

> **Do not claim external success without external evidence.**

> **Let Rainbow Ring manage the relationship.**

> **Let the external blockchain remain sovereign.**

> **Let testing determine the final implementation.**

The essential relationship is:

```text
PrismChain
    ↓
WHITE LIGHT BLOCK
    ↓
PrismOutput
    ↓
Rainbow Ring
    ↓
External Execution
    ↓
Settlement
```

> **PrismChain computes.**

> **Rainbow Ring connects.**

> **The external blockchain executes and settles according to its own rules.**

> **Evidence proves what actually happened.**

> **Connect systems without confusing them.**

> **PrismChain is the seven-layer blockchain.**
