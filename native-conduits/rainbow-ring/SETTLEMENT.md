# 🌈 Settlement

> **PrismChain computes. Rainbow Ring connects. The external blockchain executes and settles. Evidence determines what actually happened.**

Settlement is the final external boundary of the PrismChain integration architecture.

PrismChain can compute a result.

PrismOutput can represent that result.

Rainbow Ring can establish and manage the relationship between that result and an external system.

None of those facts, by themselves, constitute settlement on the external blockchain.

Settlement occurs according to the rules of the sovereign external system.

The purpose of this document is to define how PrismChain, Native Conduits, PrismOutput, and Rainbow Ring relate to external execution and settlement without confusing their respective responsibilities.

---

# 1. Settlement Is External

The fundamental principle is:

> **PrismChain does not create external settlement.**

The external blockchain remains the authority over its own state transitions.

The high-level architecture is:

```text id="1f0m7s"
NATIVE BLOCKCHAIN
       ↓
NATIVE STATE
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
EXTERNAL EXECUTION
       ↓
EXTERNAL OBSERVATION
       ↓
SETTLEMENT
```

PrismChain determines its own computational result.

The external blockchain determines whether an external action actually occurred and became established according to its own rules.

---

# 2. What Settlement Means

Settlement should be reserved for an externally established state transition.

A useful distinction is:

```text id="yy4s7d"
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

These states are not interchangeable.

A system should not skip directly from:

```text
PrismOutput
```

to:

```text
SETTLED
```

without evidence of the external state transition.

---

# 3. Computed Is Not Settled

A PrismChain computation can be completely valid while no external transaction has occurred.

For example:

```text id="kq7b4h"
PrismChain
    ↓
WLB
    ↓
PrismOutput
```

At this point PrismChain has produced a result.

That does not mean:

```text
Ethereum
    ↓
state changed
```

The two systems have different responsibilities.

### PrismChain answers:

> What does the PrismChain computation produce?

### Rainbow Ring answers:

> What relationship exists between that result and the external system?

### External blockchain answers:

> What state transition actually occurred?

Settlement requires the third answer.

---

# 4. PrismOutput and Settlement

The current `PrismOutput` structure is:

```text id="z7iyg8"
inputCommitment
rulesCommitment
resultCommitment
executionConditions
```

These fields prepare the result for the relationship layer.

They do not themselves establish settlement.

The relationship is:

```text id="w5qgdz"
PrismOutput
     │
     ├── inputCommitment
     ├── rulesCommitment
     ├── resultCommitment
     └── executionConditions
              │
              ▼
        Rainbow Ring
              │
              ▼
     External execution
              │
              ▼
       Settlement evidence
```

`executionConditions` define what must be true for an external action to proceed.

They do not prove that the action occurred.

`resultCommitment` binds the output to the PrismChain result.

It does not prove external execution.

`rulesCommitment` binds the output to its intended rules and context.

It does not create external consensus.

---

# 5. Rainbow Ring's Role

Rainbow Ring is the relationship layer.

Its settlement responsibility is therefore not to become the external blockchain.

Instead, it maintains the relationship between:

```text id="5p5gqg"
PrismChain result
      ↕
External action
      ↕
External evidence
```

The Ring should be able to establish:

* what PrismOutput initiated or authorized a relationship,
* what external action was associated with it,
* what external system was involved,
* what execution conditions applied,
* what happened externally,
* what evidence was observed,
* and whether the resulting state satisfies the settlement criteria.

The Ring does not invent the external result.

It observes and records the relationship to it.

---

# 6. Native Sovereignty

Each external blockchain remains sovereign over its own state.

For Ethereum:

```text id="j9q2p5"
Ethereum
   │
   ├── consensus
   ├── block production
   ├── transaction execution
   ├── state transition
   └── finality / settlement rules
```

PrismChain does not replace those mechanisms.

Rainbow Ring does not replace those mechanisms.

The Native Conduit does not replace those mechanisms.

The integration connects to them while preserving their native identity.

This is essential for a multi-chain architecture.

---

# 7. Execution vs Settlement

Execution and settlement are related but distinct.

### Execution

Execution asks:

> **Did the external system perform the requested action?**

### Settlement

Settlement asks:

> **Did the resulting state become established according to the external system's rules and the application's required settlement criteria?**

An external transaction can be submitted without executing.

It can execute without yet meeting an application's confirmation requirement.

It can be included in a block while remaining subject to chain-specific finality considerations.

Therefore:

```text id="zj6jkl"
SUBMITTED
   ≠
EXECUTED
   ≠
SETTLED
```

This distinction must remain explicit throughout the Ring lifecycle.

---

# 8. The Settlement Lifecycle

The Rainbow Ring relationship may progress through states such as:

```text id="k1x9am"
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

Failure or exceptional states may include:

```text id="f0f4v9"
REJECTED
EXPIRED
FAILED
CANCELLED
REORGED
DISPUTED
```

The exact implementation of these states remains subject to integration testing.

The important architectural requirement is that the system must distinguish them rather than collapsing every successful-looking step into `SETTLED`.

---

# 9. CREATED

A relationship begins when the system has created a candidate external relationship.

At this stage, there may be:

* a PrismOutput,
* a relationship identifier,
* execution conditions,
* and an intended external target.

Nothing has necessarily been executed.

Therefore:

```text
CREATED ≠ EXECUTED
CREATED ≠ SETTLED
```

---

# 10. IDENTIFIED

The relationship identifies the external system involved.

For example:

```text id="h2a3nq"
Ethereum
PRISM-ETH-01
```

Chain identity must be explicit.

This prevents an output intended for one sovereign system from being silently interpreted as belonging to another.

The external target should also be represented according to the native system's own addressing and execution model.

---

# 11. BOUND

The relationship becomes bound to the relevant commitments.

Conceptually:

```text id="6n1vqb"
nativeStateCommitment
        ↓
inputCommitment
        ↓
resultCommitment
        ↓
PrismOutput
        ↓
Rainbow Ring relationship
```

The Ring should be able to establish which PrismChain result and which input relationship the external action belongs to.

This is the connection between the commitment architecture and settlement architecture.

---

# 12. VALIDATED

Before external execution, the relationship must be checked against the conditions and evidence available at that point.

Validation may include:

* correct chain identity,
* valid commitment relationships,
* valid output structure,
* valid rules commitment,
* valid execution conditions,
* non-expired relationship,
* replay protection,
* current external state,
* and other chain-specific requirements.

The exact validation set will evolve through implementation.

---

# 13. CONDITIONED

An output may specify conditions that must be satisfied before execution.

These conditions can concern:

* external state,
* timing,
* relationship lifecycle,
* required evidence,
* execution parameters,
* or application-specific rules.

The critical distinction is:

```text id="l8af5b"
CONDITION DEFINED
      ≠
CONDITION SATISFIED
```

The Ring must not treat an unfulfilled condition as fulfilled merely because PrismChain produced a valid output.

---

# 14. READY

A relationship reaches `READY` when the required pre-execution conditions have been satisfied according to the implemented rules.

This means the system has determined that the external action is eligible to proceed.

It does not mean that the external action has occurred.

```text id="v4bq2c"
READY
  ≠
EXECUTED
```

---

# 15. EXECUTING

At `EXECUTING`, an external action is being submitted or performed.

This is where the architecture crosses from:

```text
PrismChain / Rainbow Ring
```

into:

```text
external blockchain execution
```

The exact mechanism is chain-specific.

For Ethereum, the implementation will determine the final execution path.

The public architecture should not invent execution mechanics that have not yet been demonstrated.

---

# 16. OBSERVED

After external submission or execution, the Ring must obtain evidence from the external system.

Observation may include information such as:

* transaction identity,
* block inclusion,
* resulting state,
* receipts,
* relevant logs/events,
* confirmations,
* and chain-specific finality information.

The exact evidence depends on the external blockchain.

The important principle is:

> **External state must be observed from the external system.**

PrismChain cannot declare an external transaction successful merely because PrismChain expected it to succeed.

---

# 17. CONFIRMED

`CONFIRMED` represents an external result that has met the required confirmation criteria.

The meaning of confirmation is chain-specific.

For one blockchain or application, inclusion may be enough.

For another, multiple confirmations may be required.

For another, a stronger finality condition may be necessary.

Therefore:

```text id="y8n5v3"
CONFIRMED
```

must be defined relative to the external system and the application.

The architecture should not impose a universal definition of finality across sovereign chains.

---

# 18. SETTLED

`SETTLED` is reached only when the required external evidence establishes that the intended result has become sufficiently established according to the applicable settlement policy.

Conceptually:

```text id="j5r0i1"
PrismOutput
     ↓
Execution
     ↓
External state transition
     ↓
External evidence
     ↓
Settlement criteria satisfied
     ↓
SETTLED
```

Settlement therefore requires evidence.

A PrismOutput alone is insufficient.

A submitted transaction alone is insufficient.

A transaction hash alone is insufficient.

Even block inclusion may be insufficient if the application's settlement policy requires stronger confirmation or finality.

---

# 19. Settlement Evidence

Settlement evidence should establish, as applicable:

```text id="y3f0qk"
Which chain?
Which external action?
Which state transition?
Which block?
Which resulting state?
Which confirmation/finality condition?
Which PrismOutput?
Which relationship?
```

This produces the evidence relationship:

```text id="b7p8zc"
PrismOutput
     ↓
Rainbow Ring relationship
     ↓
External transaction/action
     ↓
External state
     ↓
Evidence
     ↓
Settlement determination
```

The evidence should be sufficient for an independent observer to understand why the system considers the relationship settled.

---

# 20. Settlement Is Not a PrismChain Block

The external settlement record must not be confused with a White Light Block.

```text id="8j5j4q"
WHITE LIGHT BLOCK
       ≠
EXTERNAL SETTLEMENT
```

The WLB represents the unified result of PrismChain's seven-layer computation.

External settlement represents a state established on the sovereign external system.

These are different domains.

The integration connects them.

It does not merge them.

---

# 21. Settlement Is Not a Ring Block

Likewise:

```text id="h3p7s0"
RAINBOW RING
       ≠
SECOND BLOCKCHAIN
```

The Ring does not need to become a competing ledger simply to manage relationships.

Its purpose is to establish:

```text
WHO
WHAT
FROM WHERE
UNDER WHICH RULES
UNDER WHICH CONDITIONS
TO WHICH EXTERNAL SYSTEM
WITH WHAT RESULT
WITH WHAT EVIDENCE
```

The relationship is the important object.

---

# 22. Reorganization

External blockchains can reorganize or otherwise change which state should be treated as authoritative.

The settlement architecture must therefore account for reorganization.

A relationship that was previously observed may need to transition:

```text id="k9t3b1"
SETTLED
   ↓
REORGED
```

or:

```text id="7s4zqk"
OBSERVED
   ↓
REORGED
   ↓
RE-EVALUATED
```

The correct behavior depends on the external blockchain and the application's settlement policy.

The critical principle is:

> **A previous observation does not automatically remain a valid settlement claim after the external state changes.**

---

# 23. Finality

Finality must remain chain-specific.

A system should distinguish:

```text id="n4k0f1"
INCLUDED
CONFIRMED
FINAL
SETTLED
```

These terms may overlap in some environments, but they should not be treated as universally synonymous.

For Ethereum, the integration must determine which native evidence and finality conditions are required for the intended settlement guarantees.

The current architecture does not claim that a PrismChain commitment creates Ethereum finality.

It does not.

---

# 24. Failed Execution

External execution can fail.

A failed external transaction should not be represented as successful merely because the corresponding PrismOutput was valid.

The relationship should preserve the distinction:

```text id="s6n8c2"
VALID PRISM OUTPUT
        ↓
EXTERNAL EXECUTION
        ↓
FAILED
```

The failure itself is useful evidence.

The system should preserve enough information to determine:

* what was attempted,
* under which output,
* under which conditions,
* why it failed if observable,
* and whether the relationship can be retried, expired, cancelled, or disputed.

---

# 25. Expiration

A PrismOutput or Ring relationship may become invalid after a defined period or condition.

For example:

```text id="1g7b0p"
VALID
  ↓
TIME PASSES
  ↓
EXPIRED
```

An expired relationship must not automatically become executable simply because its original commitment remains cryptographically valid.

This demonstrates an important principle:

> **Cryptographic validity does not automatically imply current execution eligibility.**

---

# 26. Replay Protection

A previously settled relationship must not be executable again merely because its commitments remain valid.

Settlement therefore requires lifecycle awareness.

Conceptually:

```text id="0r8w3a"
RELATIONSHIP A
      ↓
SETTLED
      ↓
REPLAY ATTEMPT
      ↓
REJECTED
```

The exact replay protection mechanism must be determined by implementation.

Potential mechanisms may include:

* unique relationship identifiers,
* nonces,
* state references,
* consumed-output tracking,
* expiration,
* execution conditions,
* or external state checks.

No single mechanism should be assumed before testing establishes the appropriate implementation.

---

# 27. Settlement and Reversibility

Settlement policy must account for whether the external state transition can be reversed, reorganized, challenged, or otherwise superseded.

This is especially important for cross-chain relationships.

A relationship should not be treated as permanently settled merely because the external system temporarily reflected a state.

The required level of permanence depends on:

* the external chain,
* its finality model,
* the application,
* the value at risk,
* and the relationship's security requirements.

The architecture therefore separates:

```text
OBSERVATION
      ↓
CONFIRMATION
      ↓
FINALITY
      ↓
SETTLEMENT
```

rather than assuming they are identical.

---

# 28. Settlement and Native Conduits

Native Conduits preserve native blockchain identity.

Their primary role is the controlled boundary through which native state enters PrismChain.

However, native information may also be required when interpreting external execution and settlement evidence.

The broader relationship is:

```text id="2r4p9x"
NATIVE BLOCKCHAIN
       ↓
NATIVE CONDUIT
       ↓
PrismInput
       ↓
PRISMCHAIN
       ↓
PrismOutput
       ↓
RAINBOW RING
       ↓
NATIVE / EXTERNAL EXECUTION
       ↓
NATIVE EVIDENCE
```

The exact implementation of the return/evidence path is still subject to integration discovery.

The architectural invariant is:

> **The conduit preserves native identity; the Ring manages the relationship.**

---

# 29. Ethereum Settlement

Ethereum is the first external system being integrated.

The intended high-level path is:

```text id="e4f5c1"
Ethereum
    ↓
PRISM-ETH-01
    ↓
Ethereum Native State
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
Ethereum execution
    ↓
Ethereum observation
    ↓
Ethereum settlement
```

The exact Ethereum execution and settlement mechanism must be discovered through the actual implementation.

The public architecture therefore establishes the boundaries without claiming that every downstream mechanism is already production complete.

---

# 30. Settlement Evidence Must Be External

One of the strongest architectural rules is:

> **Do not use PrismChain's own assertion of success as proof of external settlement.**

Instead:

```text id="2m7n4b"
PRISMCHAIN RESULT
       ↓
INTENDED ACTION
       ↓
EXTERNAL ACTION
       ↓
EXTERNAL OBSERVATION
       ↓
EXTERNAL EVIDENCE
       ↓
SETTLEMENT
```

This prevents circular proof.

PrismChain should not be both:

1. the system asserting that settlement occurred, and
2. the only source of evidence that settlement occurred.

External state must provide the evidence of external state.

---

# 31. Evidence Chain

A complete cross-system evidence chain should eventually resemble:

```text id="4r0c8m"
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
    │
    ▼
RAINBOW RING
    │
    ▼
EXECUTION
    │
    ▼
EXTERNAL STATE TRANSITION
    │
    ▼
EXTERNAL EVIDENCE
    │
    ▼
SETTLEMENT
```

Every arrow represents a relationship that should be testable or observable.

---

# 32. Settlement Testing

Settlement cannot be proven by unit tests alone.

Unit tests can establish that the software behaves correctly under defined inputs.

Integration tests can establish that components connect correctly.

External experiments can establish that the relationship behaves correctly against the sovereign blockchain.

Therefore the evidence model should include:

```text id="p2m7h4"
UNIT TEST
    ↓
INTEGRATION TEST
    ↓
EXTERNAL TESTNET EXPERIMENT
    ↓
EXTERNAL OBSERVATION
    ↓
SETTLEMENT EVIDENCE
```

The final level is particularly important.

A local test that says:

```text settlement = true
```

does not prove external settlement.

A testnet transaction with externally observable evidence is substantially stronger.

---

# 33. Settlement Test Cases

The Ethereum integration should eventually test at least:

### Successful execution

```text
Valid PrismOutput
        ↓
Valid conditions
        ↓
External execution
        ↓
Expected external state
        ↓
SETTLED
```

### Failed execution

```text
Valid PrismOutput
        ↓
External execution
        ↓
Failure
        ↓
FAILED
```

### Expired output

```text
Valid output
        ↓
Expiration
        ↓
Execution attempt
        ↓
REJECTED / EXPIRED
```

### Replay

```text
SETTLED relationship
        ↓
Replay attempt
        ↓
REJECTED
```

### Wrong chain

```text
Ethereum output
        ↓
Non-Ethereum execution context
        ↓
REJECTED
```

### Modified output

```text
Original PrismOutput
        ↓
Mutation
        ↓
Commitment mismatch
        ↓
REJECTED
```

### Reorganization

```text
Observed external state
        ↓
External reorganization
        ↓
Prior evidence reevaluated
        ↓
Relationship state updated
```

The exact expected lifecycle transitions should be established through implementation.

---

# 34. Settlement Invariants

The settlement layer should preserve the following invariants.

### Invariant 1 — External sovereignty

The external blockchain remains authoritative over its own state.

### Invariant 2 — No silent settlement

No relationship becomes `SETTLED` without the required external evidence.

### Invariant 3 — Output binding

Settlement evidence remains traceable to the relevant PrismOutput.

### Invariant 4 — Input traceability

The PrismOutput remains traceable to the PrismInput from which it originated.

### Invariant 5 — Result integrity

The output remains bound to the actual White Light Block.

### Invariant 6 — Chain isolation

Settlement evidence belongs to the intended sovereign blockchain.

### Invariant 7 — Lifecycle integrity

A relationship cannot silently skip required states.

### Invariant 8 — Replay resistance

A settled relationship cannot be reused as a new execution without satisfying the applicable rules.

### Invariant 9 — Reorganization awareness

External state changes can invalidate or require reevaluation of previous observations.

### Invariant 10 — Evidence discipline

Claims about execution, confirmation, finality, and settlement require evidence appropriate to the claim.

---

# 35. What Settlement Does Not Mean

Settlement does not mean:

* PrismChain approved something, therefore it happened.
* Rainbow Ring recorded something, therefore it happened.
* A transaction was submitted, therefore it happened.
* A transaction was included, therefore it is permanently final.
* A commitment exists, therefore external settlement exists.
* A local test returned success, therefore mainnet settlement occurred.
* An external action was expected, therefore the external state changed.

Instead:

> **Settlement is an externally evidenced state established according to the rules of the sovereign system and the applicable settlement policy.**

---

# 36. Public Evidence

Public settlement claims should be accompanied by evidence appropriate to the claim.

Depending on the stage of development, this may include:

* test results,
* transaction identifiers,
* block identifiers,
* observed receipts,
* relevant state references,
* confirmation information,
* finality information,
* reproducible test procedures,
* and documented limitations.

The goal is not to overwhelm the reader with raw data.

The goal is to make important claims independently inspectable.

---

# 37. Failure Is Evidence

A failed settlement experiment is not a useless result.

For example:

```text
EXPECTED
    ↓
EXECUTION
    ↓
FAILURE
    ↓
DIAGNOSIS
    ↓
ARCHITECTURAL DISCOVERY
    ↓
TUNE
    ↓
RETEST
```

This follows the development process:

**Inspect → Specify → Test → Connect → Tune → Verify**

Failures should therefore be documented rather than hidden.

A system that records only successful experiments provides a distorted picture of its actual development.

---

# 38. Implementation Discovery

Settlement is one of the areas where implementation may reveal requirements that are not obvious from the initial architecture.

The specification therefore intentionally does not prescribe every mechanism.

The actual integration may reveal the need for:

* additional evidence fields,
* lifecycle states,
* external state references,
* execution receipts,
* finality tracking,
* reorg handling,
* retry policies,
* expiration rules,
* or additional commitment relationships.

When implementation reveals a necessary architectural change:

> **Update the architecture to describe what actually works.**

The objective is not to force the implementation to obey an incomplete diagram.

The objective is to discover the correct system.

---

# 39. Current Status

The settlement architecture is currently best understood as:

🟢 **Architectural definition**

🟣 **Experimental integration target**

🔵 **Research / implementation discovery**

The complete production settlement guarantee is not claimed merely because the settlement architecture has been documented.

The Ethereum integration must establish the actual behavior through:

```text
Implementation
    ↓
Testing
    ↓
External execution
    ↓
Observation
    ↓
Evidence
```

Only then should a stronger public capability claim be made.

---

# 40. Public / Private Boundary

The public documentation should expose:

* settlement architecture,
* lifecycle concepts,
* responsibility boundaries,
* evidence requirements,
* security properties,
* test methodology,
* demonstrated behavior,
* and known limitations.

It does not need to expose proprietary implementation details.

The governing principle remains:

> **Reveal the architecture. Protect the advantage.**

The public should be able to understand how settlement is supposed to work without receiving every internal mechanism used to implement it.

---

# 41. Complete Relationship

The complete architecture can be summarized as:

```text id="r3h5w7"
                   EXTERNAL BLOCKCHAIN
                          │
                          │ native state
                          ▼
                    NATIVE CONDUIT
                          │
                          ▼
                      PrismInput
                          │
                          ▼
                     PRISMCHAIN
                          │
             ┌────────────┴────────────┐
             │ RED                     │
             │ ORANGE                  │
             │ YELLOW                  │
             │ GREEN                   │
             │ BLUE                    │
             │ INDIGO                  │
             │ VIOLET                  │
             └────────────┬────────────┘
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
                 EXECUTION CONDITIONS
                          │
                          ▼
                  EXTERNAL EXECUTION
                          │
                          ▼
                   OBSERVED STATE
                          │
                          ▼
                  CONFIRMATION / FINALITY
                          │
                          ▼
                      SETTLEMENT
                          │
                          ▼
                       EVIDENCE
```

The systems remain distinct.

PrismChain computes.

Rainbow Ring establishes the relationship.

The external blockchain executes.

The external blockchain establishes its own state.

Evidence tells us what actually happened.

---

# 42. Final Principles

**Do not call something settled because PrismChain says it is settled.**

**Do not call something executed because it was submitted.**

**Do not call something final because it was included.**

**Do not confuse commitment with settlement.**

**Do not confuse computation with execution.**

**Do not confuse execution with settlement.**

**Do not replace sovereign blockchain rules with assumptions made by the integration layer.**

Instead:

> **PrismChain computes.**

> **PrismOutput represents the result.**

> **Rainbow Ring connects.**

> **The external blockchain executes and settles according to its own rules.**

> **External evidence establishes what actually happened.**

The ultimate principle is simple:

**Connect systems without confusing them.**

**Let every boundary have a defined responsibility.**

**Let every settlement claim have evidence.**

> **PrismChain is the seven-layer blockchain.**
