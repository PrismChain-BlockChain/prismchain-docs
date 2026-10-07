# 🌈 PrismChain — Settlement

> **Settlement is where a PrismChain result becomes an externally observable state change.**

PrismChain is the seven-layer blockchain.

PrismChain performs the computation.

The White Light Block records the unified result of that computation.

PrismOutput represents that result at the external boundary.

Rainbow Ring establishes the relationship between the PrismChain result and the external system.

**Settlement is the point at which the external system actually accepts and records the resulting action or state change.**

The distinction is critical:

```text id="j6p4w8"
COMPUTE
   ↓
WHITE LIGHT BLOCK
   ↓
PrismOutput
   ↓
RAINBOW RING
   ↓
EXECUTION
   ↓
SETTLEMENT
```

A result is not settled merely because PrismChain computed it.

---

# 1. Purpose

The purpose of this document is to define the settlement boundary surrounding PrismChain.

Settlement answers the question:

> **What happened externally after PrismChain produced its result?**

This creates the final relationship in the integration lifecycle:

```text id="r8m3k5"
NATIVE STATE
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
EXTERNAL EXECUTION
     ↓
SETTLEMENT
```

Settlement therefore provides evidence about what actually occurred outside PrismChain.

---

# 2. What Settlement Means

For this architecture, settlement means that an external system has accepted and recorded an action or state transition associated with a PrismChain result.

Conceptually:

```text id="v5q7n2"
PRISMCHAIN RESULT
       │
       ▼
EXTERNAL ACTION
       │
       ▼
EXTERNAL SYSTEM ACCEPTS
       │
       ▼
EXTERNAL STATE CHANGES
       │
       ▼
SETTLED
```

The exact definition of settlement depends on the external blockchain.

Ethereum settlement may have different requirements from Bitcoin, Solana, or another sovereign system.

---

# 3. What Settlement Is Not

Settlement is not:

* PrismChain computation,
* a White Light Block,
* PrismOutput,
* a Native Conduit,
* Rainbow Ring itself,
* consensus inside PrismChain,
* authentication,
* or merely submitting a transaction.

In particular:

```text id="b9x4k7"
PrismChain
    ≠
Settlement
```

and:

```text id="n6w3p1"
Rainbow Ring
    ≠
Settlement
```

Rainbow Ring establishes the relationship through which settlement may occur.

The external blockchain performs its own native execution and settlement.

---

# 4. The Settlement Boundary

The complete boundary is:

```text id="q2h8m5"
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
EXTERNAL STATE
    │
    ▼
SETTLEMENT
```

The first three stages occur within the PrismChain computational architecture.

The final stages involve the external system.

---

# 5. PrismChain Computes

The foundational relationship remains:

```text id="f7k3r9"
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
```

This is PrismChain computation.

The resulting WLB is the PrismChain result.

Settlement happens later.

---

# 6. PrismOutput Represents the Result

The WLB is passed to the output boundary through the PrismOutput architecture.

Conceptually:

```text id="m4x8v2"
WHITE LIGHT BLOCK
       │
       ▼
   PrismOutput
       │
       ▼
RAINBOW RING
```

PrismOutput provides the structured representation of the result.

It does not itself settle the result externally.

---

# 7. Rainbow Ring Establishes the Relationship

Rainbow Ring occupies the relationship layer:

```text id="w5n2q6"
PRISMCHAIN
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

Rainbow Ring is therefore the architecture surrounding the relationship between PrismChain and external systems.

It should not be described as merely:

* a bridge,
* a transaction relay,
* a second blockchain,
* or a settlement engine.

Its purpose is broader than simple message transfer.

---

# 8. External Execution

Before settlement can occur, an external action may need to execute.

Conceptually:

```text id="k7p3m9"
PrismOutput
     ↓
Execution Conditions
     ↓
External Action
     ↓
External Execution
```

The external blockchain then applies its own native rules.

PrismChain does not replace those rules.

---

# 9. Sovereign External Systems

Each integrated blockchain remains sovereign.

For example:

```text id="c4v8x1"
Ethereum
     │
     ▼
Ethereum Native Execution


PrismChain
     │
     ▼
PrismChain Computation
```

The two systems have different responsibilities.

The integration connects them without confusing them.

---

# 10. Settlement as a State Transition

The most useful definition is:

> **Settlement is the externally observable state transition resulting from an accepted PrismChain-related action.**

Conceptually:

```text id="q6m4r8"
EXTERNAL STATE A
       │
       ▼
EXTERNAL EXECUTION
       │
       ▼
EXTERNAL STATE B
```

The transition from A to B is what ultimately provides external evidence.

---

# 11. Settlement Evidence

A settlement claim should be supported by evidence from the external system.

For a blockchain, this may include:

* transaction identifier,
* block reference,
* execution result,
* resulting state,
* receipt,
* event,
* or other native evidence.

The exact evidence depends on the external blockchain.

---

# 12. Settlement Is Not a Claim

The architecture should never treat:

```text id="p8x3v5"
TRANSACTION SUBMITTED
```

as equivalent to:

```text id="z2k7m4"
TRANSACTION SETTLED
```

Likewise:

```text id="h5q9w1"
PrismOutput CREATED
```

does not mean:

```text id="r4m8n6"
EXTERNAL STATE CHANGED
```

The external result must be observed.

---

# 13. The Complete Evidence Chain

A complete integration should eventually establish:

```text id="x8f2k5"
NATIVE STATE
      ↓
PrismInput
      ↓
INPUT COMMITMENT
      ↓
PRISMCHAIN
      ↓
WHITE LIGHT BLOCK
      ↓
RESULT COMMITMENT
      ↓
PrismOutput
      ↓
RAINBOW RING
      ↓
EXTERNAL EXECUTION
      ↓
EXTERNAL STATE CHANGE
      ↓
SETTLEMENT EVIDENCE
```

This is the strongest end-to-end evidence path.

---

# 14. Settlement and Commitments

Commitments establish relationships before external settlement.

The relevant relationship is:

```text id="m7v3q9"
PrismInput
     ↓
inputCommitment
     ↓
PrismChain
     ↓
WLB
     ↓
resultCommitment
     ↓
PrismOutput
     ↓
Rainbow Ring
     ↓
External Settlement
```

The commitment architecture makes it possible to determine what result was intended.

Settlement establishes what actually happened externally.

---

# 15. Intended Result vs Actual Result

This distinction is essential.

```text id="d6p4x8"
INTENDED
   │
   ▼
PrismOutput
   │
   ▼
EXTERNAL EXECUTION
   │
   ▼
ACTUAL
```

A valid PrismOutput can exist even when external execution fails.

Therefore:

```text id="q9n5w3"
VALID OUTPUT
      ≠
SUCCESSFUL SETTLEMENT
```

---

# 16. Execution Failure

External execution can fail.

For example:

```text id="r7k2m4"
PrismOutput
     │
     ▼
Rainbow Ring
     │
     ▼
Execution Attempt
     │
     ▼
FAILURE
```

The system should preserve enough evidence to determine:

* what was attempted,
* which PrismOutput was involved,
* why execution failed,
* what external state existed,
* and whether recovery is possible.

---

# 17. Settlement Failure

Settlement failure should not be hidden.

The architecture should distinguish:

```text id="f5m8q2"
COMPUTED
    ↓
OUTPUT CREATED
    ↓
EXECUTION ATTEMPTED
    ↓
EXECUTION FAILED
```

from:

```text id="j3v7n9"
COMPUTED
    ↓
OUTPUT CREATED
    ↓
EXECUTION
    ↓
SETTLED
```

Both are meaningful results.

Only one represents successful settlement.

---

# 18. Ethereum Settlement

Ethereum is the first target for a complete settlement path.

The intended architecture is:

```text id="a6q9w4"
ETHEREUM
   │
   ▼
Ethereum Native Conduit
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
ETHEREUM EXECUTION
   │
   ▼
ETHEREUM SETTLEMENT
```

This remains an integration objective until the complete path has been implemented and tested.

---

# 19. Ethereum Settlement Evidence

A future Ethereum settlement test should be able to associate the complete path with native Ethereum evidence.

Conceptually:

```text id="p4m8x6"
PrismOutput
     │
     ▼
External Ethereum Action
     │
     ▼
Transaction
     │
     ▼
Ethereum Block
     │
     ▼
Execution Result
     │
     ▼
Settlement Evidence
```

The exact evidence set will depend on the implementation.

No production settlement claim should be made before this path is demonstrated.

---

# 20. Ethereum Finality

Ethereum settlement should not be described simply as:

> "The transaction was included."

Inclusion and finality are different properties.

Conceptually:

```text id="w2k7n5"
INCLUDED
   ≠
SUFFICIENTLY CONFIRMED
   ≠
FINAL
```

The integration must define what level of Ethereum finality is required for a PrismChain result to be considered settled.

That policy remains an implementation and security question.

---

# 21. Reorganization Handling

External blockchains can experience reorganizations or changes in canonical state.

Therefore settlement evidence must account for the possibility that an observed execution is not yet sufficiently final.

Conceptually:

```text id="g8v4q1"
EXECUTION OBSERVED
       │
       ▼
CANONICALITY CHECK
       │
       ▼
FINALITY POLICY
       │
       ▼
SETTLED / NOT YET SETTLED
```

The final policy must be specific to the external blockchain.

---

# 22. Settlement and Native Conduits

Native Conduits provide the external-state boundary.

Settlement operates on the other side of the complete relationship.

The broad architecture is:

```text id="n5x8r3"
NATIVE BLOCKCHAIN
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
PrismOutput
       │
       ▼
RAINBOW RING
       │
       ▼
NATIVE EXECUTION / SETTLEMENT
```

The same external system therefore participates at both ends of the relationship:

```text id="v6m3p8"
NATIVE STATE
    ↓
     PrismChain
    ↓
NATIVE EXECUTION
```

The system remains sovereign throughout.

---

# 23. The Round-Trip Relationship

A complete integration can eventually be viewed as a round trip:

```text id="j8q4w7"
EXTERNAL STATE
      │
      ▼
   PrismInput
      │
      ▼
   PRISMCHAIN
      │
      ▼
   PrismOutput
      │
      ▼
EXTERNAL EXECUTION
      │
      ▼
NEW EXTERNAL STATE
```

This is the full integration loop.

---

# 24. Round-Trip Evidence

The most valuable integration demonstration would show:

```text id="m9f2k6"
STATE A
  ↓
PrismInput A
  ↓
PrismChain
  ↓
WLB A
  ↓
PrismOutput A
  ↓
Rainbow Ring
  ↓
External Execution
  ↓
STATE B
```

Then the new external state can potentially become the source for another integration cycle.

This creates an observable feedback relationship between the external system and PrismChain.

---

# 25. Settlement Does Not Feed Computation Automatically

A settled result should not automatically become a PrismChain input without explicit rules.

The architecture should distinguish:

```text id="c7p5n2"
SETTLED EXTERNAL STATE
        │
        ▼
NATIVE STATE OBSERVATION
        │
        ▼
NATIVE CONDUIT
        │
        ▼
NEW PrismInput
```

If a subsequent state is to enter PrismChain, it must pass through the input boundary again.

This keeps the architecture explicit.

---

# 26. Settlement and State References

Settlement evidence should eventually be tied to an identifiable external state.

Conceptually:

```text id="r3x8v5"
SETTLEMENT
    │
    ▼
External State Reference
    │
    ▼
Block / State Identifier
```

This creates a traceable endpoint.

The precise reference depends on the external blockchain.

---

# 27. Settlement and Execution Conditions

PrismOutput includes:

```text id="w4m7q9"
executionConditions
```

These conditions may determine whether external execution is currently permitted.

Conceptually:

```text id="p6v2n8"
PrismOutput
     │
     ▼
Execution Conditions
     │
     ├──► Satisfied
     │      ↓
     │   Execute
     │
     └──► Unsatisfied
            ↓
         Do Not Execute
```

The exact condition model remains subject to implementation.

---

# 28. Conditional Settlement

Some future integrations may require conditions to remain true until execution.

Therefore:

```text id="k5q8r4"
OUTPUT CREATED
      ↓
CONDITIONS CHECKED
      ↓
EXECUTION
      ↓
SETTLEMENT
```

The conditions may need to be checked more than once.

This is an area for future Rainbow Ring and security research.

---

# 29. Settlement and Replay Protection

A successfully settled output should not normally be executable repeatedly unless the architecture explicitly allows it.

Therefore the settlement layer must eventually establish:

```text id="v8m4p7"
OUTPUT
  ↓
EXECUTION STATE
  ↓
SETTLED
  ↓
REPLAY PROTECTION
```

The exact mechanism remains an implementation question.

---

# 30. Settlement State Machine

A useful conceptual state model is:

```text id="g4x7q2"
CREATED
   ↓
VALIDATED
   ↓
READY
   ↓
SUBMITTED
   ↓
EXECUTING
   ↓
OBSERVED
   ↓
CONFIRMED
   ↓
SETTLED
```

Possible failure paths include:

```text id="r9n5w3"
VALIDATION FAILED
EXECUTION FAILED
REJECTED
EXPIRED
REORGED
CANCELLED
```

The final state machine should be determined by actual implementation.

---

# 31. Settlement Is Evidence

The strongest settlement claim is not:

> "The system sent a transaction."

It is:

> "The PrismChain result was associated with an external execution that was observed and accepted by the external system under the defined settlement policy."

That claim can then be supported by native evidence.

---

# 32. Settlement Evidence Record

A future evidence record may conceptually contain:

```text id="x5k8m2"
PrismOutput
     │
     ├── inputCommitment
     ├── rulesCommitment
     ├── resultCommitment
     └── executionConditions
            │
            ▼
     External Execution
            │
            ├── transaction reference
            ├── external state reference
            ├── execution result
            └── finality / confirmation evidence
```

The exact schema is not yet fixed.

---

# 33. Failure Evidence

Failures should be preserved just as carefully as successes.

A failure record should eventually allow investigators to answer:

```text id="n7q3v6"
WHAT WAS REQUESTED?
WHAT WAS COMPUTED?
WHAT OUTPUT WAS CREATED?
WHAT WAS ATTEMPTED?
WHAT FAILED?
WHAT EXTERNAL STATE EXISTED?
WHAT HAPPENED AFTERWARD?
```

This follows the PrismChain evidence philosophy:

> **A failed test is useful information.**

---

# 34. Settlement Security Boundary

Settlement is one of the highest-risk portions of the integration because it connects internal computation to external state changes.

Potential threats include:

* unauthorized execution,
* output substitution,
* replay,
* stale output,
* execution-condition bypass,
* transaction substitution,
* external state mismatch,
* reorganization,
* finality errors,
* and incorrect settlement reporting.

These must be treated as explicit security questions.

---

# 35. Trust Boundaries

The architecture contains multiple trust boundaries:

```text id="h6m2r8"
EXTERNAL BLOCKCHAIN
        │
        │
        ▼
 NATIVE CONDUIT
        │
        │
        ▼
    PrismInput
        │
        │
        ▼
   PRISMCHAIN
        │
        │
        ▼
   PrismOutput
        │
        │
        ▼
   RAINBOW RING
        │
        │
        ▼
EXTERNAL EXECUTION
```

Each boundary requires its own assumptions and verification.

No single commitment should be assumed to secure the entire path.

---

# 36. Settlement Security Questions

Important questions include:

* Who is authorized to execute?
* What exactly is being executed?
* How is the output authenticated?
* How is replay prevented?
* What external state must be present?
* What constitutes sufficient finality?
* How are reorganizations handled?
* What happens when execution partially succeeds?
* How are failures recorded?
* How is settlement independently verified?
* Can an external result be incorrectly attributed to a PrismOutput?
* What prevents an output from being executed under altered conditions?

These questions should become implementation and testing requirements.

---

# 37. Ethereum Security Questions

The Ethereum integration introduces additional questions:

* What Ethereum state is considered canonical?
* What proof or authentication mechanism is required?
* How is Ethereum finality represented?
* How are reorganizations detected?
* What Ethereum transaction represents the output?
* How is execution verified?
* What evidence establishes settlement?
* What happens if the Ethereum transaction fails?
* What happens if it succeeds but later loses canonical status?
* How is replay prevented?

These remain active integration questions.

---

# 38. Settlement Testing

A useful testing progression is:

```text id="q4n7x5"
TEST 1
Construct valid PrismInput

        ↓

TEST 2
Produce known PrismChain result

        ↓

TEST 3
Construct PrismOutput

        ↓

TEST 4
Verify result commitment

        ↓

TEST 5
Pass through Rainbow Ring

        ↓

TEST 6
Execute externally

        ↓

TEST 7
Observe external result

        ↓

TEST 8
Verify settlement evidence
```

This should be performed incrementally.

---

# 39. Negative Settlement Tests

The system should also deliberately test failure.

Examples:

```text id="m8v3p6"
INVALID OUTPUT
     ↓
REJECT


EXPIRED OUTPUT
     ↓
REJECT


REPLAYED OUTPUT
     ↓
REJECT


INVALID CONDITIONS
     ↓
REJECT


FAILED EXTERNAL EXECUTION
     ↓
REPORT FAILURE
```

These tests are as important as successful settlement.

---

# 40. End-to-End Mutation Test

One of the strongest future experiments is to alter the initial input and trace the effect all the way through settlement.

```text id="f6q2w9"
INPUT A
  ↓
WLB A
  ↓
OUTPUT A
  ↓
SETTLEMENT A


INPUT B
  ↓
WLB B
  ↓
OUTPUT B
  ↓
SETTLEMENT B
```

The experiment should establish whether a controlled input change creates the expected downstream differences.

---

# 41. Settlement and the White Light Block

The WLB remains the central computational artifact.

The settlement relationship is:

```text id="v9k4p2"
SEVEN-LAYER COMPUTATION
        ↓
WHITE LIGHT BLOCK
        ↓
PrismOutput
        ↓
Rainbow Ring
        ↓
External Settlement
```

Settlement therefore demonstrates the ability of the surrounding architecture to carry a PrismChain result into an external system.

It does not redefine what the WLB is.

---

# 42. Settlement and PrismChain Identity

Settlement does not make the external blockchain part of PrismChain.

Instead:

```text id="j7m5x3"
PrismChain
    computes

Rainbow Ring
    connects

External Blockchain
    executes / settles
```

Each system retains its own identity.

---

# 43. Settlement and Multi-Chain Architecture

The same conceptual model can eventually support multiple Native Conduits:

```text id="p4x8n6"
Ethereum ──► PrismChain ──► Ethereum Settlement
Bitcoin  ──► PrismChain ──► Bitcoin Settlement
Solana   ──► PrismChain ──► Solana Settlement
Base     ──► PrismChain ──► Base Settlement
Avalanche──► PrismChain ──► Avalanche Settlement
Sui      ──► PrismChain ──► Sui Settlement
IBC      ──► PrismChain ──► IBC Relationship
```

These are architectural targets, not claims that all integrations currently exist.

---

# 44. Planned Conduit Identity

The current planned conduit identifiers are:

```text id="y8r4m2"
PRISM-ETH-01
PRISM-BTC-02
PRISM-SOL-03
PRISM-BASE-04
PRISM-AVAX-05
PRISM-SUI-06
PRISM-IBC-07
```

Ethereum is the first integration being developed.

The other identifiers represent planned architectural expansion and should not be interpreted as completed integrations.

---

# 45. Settlement and Sovereignty

The Native Conduit principle continues through settlement:

> **Connect systems without confusing them.**

The external blockchain remains responsible for its own:

* execution,
* consensus,
* native state,
* transaction rules,
* and settlement.

PrismChain remains responsible for its own computation.

Rainbow Ring establishes the relationship between them.

---

# 46. Current Status

The settlement architecture is currently a combination of:

**🟢 Architectural Definition**

The boundary and responsibilities are defined.

**🟣 Experimental Integration**

Ethereum-related infrastructure is being developed and tested.

**🔵 Research**

Complete trust, finality, reorganization, and security semantics remain under investigation.

**🟡 Future**

Complete multi-chain settlement and production settlement infrastructure remain future work.

---

# 47. What Is Currently Demonstrated

The broader project currently establishes the architectural components needed to investigate:

* PrismInput,
* PrismChain computation,
* White Light Block production,
* PrismOutput,
* commitment relationships,
* Native Conduits,
* Ethereum-specific integration plumbing,
* and Rainbow Ring boundaries.

These components create the path toward settlement.

They should not be represented as proof of a completed production settlement network.

---

# 48. What Remains Unproven

The following remain unproven until implemented and tested:

* complete Ethereum end-to-end settlement,
* production-grade external execution,
* Ethereum finality handling,
* complete reorganization handling,
* production replay protection,
* complete settlement verification,
* multi-chain settlement,
* production security,
* and decentralized production operation.

Evidence must determine when these statements can change.

---

# 49. Public Evidence Standard

Settlement claims should follow:

```text id="c8m5r1"
CLAIM
  ↓
ARCHITECTURAL BASIS
  ↓
IMPLEMENTATION
  ↓
TEST
  ↓
EXTERNAL EXECUTION
  ↓
OBSERVED RESULT
  ↓
SETTLEMENT EVIDENCE
  ↓
LIMITATIONS
```

No step should be skipped when making a strong public claim.

---

# 50. Settlement Demonstration

The ideal public demonstration eventually becomes:

```text id="w7q3n8"
1. Native external state identified
              ↓
2. PrismInput constructed
              ↓
3. PrismChain computes
              ↓
4. White Light Block produced
              ↓
5. PrismOutput constructed
              ↓
6. Rainbow Ring processes relationship
              ↓
7. External action executed
              ↓
8. External state changes
              ↓
9. Settlement independently observed
```

That demonstration would provide a complete evidence trail.

---

# 51. Architecture Must Follow Implementation

Settlement is one of the areas where implementation will likely teach the architecture the most.

The development process remains:

```text id="k4x8m7"
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

If the external chain requires a different execution condition:

**change the design.**

If finality requires another verification step:

**add it.**

If settlement exposes an architectural weakness:

**fix the architecture.**

If testing disproves a claim:

**change the claim.**

The specification is guidance until implementation and evidence establish the final design.

---

# 52. Settlement as the End of the Current Loop

The complete current integration objective is:

```text id="p8v2m6"
EXTERNAL BLOCKCHAIN
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

This is the full boundary relationship the Ethereum integration is intended to establish.

---

# 53. The Settlement Principle

Settlement is the final external evidence that a PrismChain result became a real state transition outside PrismChain.

The distinction is:

```text id="y5n8q3"
PrismChain
    COMPUTES

White Light Block
    RECORDS RESULT

PrismOutput
    REPRESENTS RESULT

Rainbow Ring
    CONNECTS RELATIONSHIP

External Blockchain
    EXECUTES

Settlement
    CONFIRMS EXTERNAL RESULT
```

Each role remains separate.

---

# 54. Final Principle

> **Do not confuse computation with execution.**

> **Do not confuse execution with settlement.**

> **Do not confuse a commitment with finality.**

> **Do not claim settlement until the external system provides evidence.**

The architecture is:

```text id="r3w7k5"
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
EXTERNAL EXECUTION
     ↓
SETTLEMENT
```

**PrismChain computes.**

**The White Light Block records the unified result.**

**PrismOutput represents the result.**

**Rainbow Ring connects the relationship.**

**The external blockchain executes and settles according to its own rules.**

**Evidence tells us when settlement has actually occurred.**

> **Connect systems without confusing them.**

> **Compute internally. Execute externally. Verify everything.**

**PrismChain is the seven-layer blockchain.**
