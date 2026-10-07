# 🔐 Commitments

> **Commit the state. Bind the input. Bind the result. Bind the rules. Define the conditions. Verify every relationship.**

This document defines the commitment architecture connecting external native state to PrismChain computation and ultimately to the Rainbow Ring relationship layer.

The commitment layer is what allows the system to preserve traceability across boundaries without confusing one type of evidence with another.

The intended relationship is:

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
     │
 ┌───┴────────────────┐
 ▼                    ▼
rulesCommitment   executionConditions
 │                    │
 └────────┬───────────┘
          ▼
     RAINBOW RING
```

The purpose is not to create another blockchain.

The purpose is to make relationships between systems explicit, deterministic, inspectable, and testable.

---

# 1. Commitment Architecture

A commitment is a cryptographic binding to a defined representation of information.

In PrismChain's integration architecture, commitments provide continuity across system boundaries.

The current commitment fields are:

```text
nativeStateCommitment
inputCommitment
rulesCommitment
resultCommitment
```

Each answers a different question.

| Commitment              | Primary purpose                                      |
| ----------------------- | ---------------------------------------------------- |
| `nativeStateCommitment` | What external native state is this input bound to?   |
| `inputCommitment`       | What PrismInput is this computation/output bound to? |
| `rulesCommitment`       | What rules and execution context govern this output? |
| `resultCommitment`      | What PrismChain result is this output bound to?      |

These commitments form a chain of relationships rather than a single universal hash.

---

# 2. Commitment Is Not Consensus

One of the most important architectural distinctions is:

```text
COMMITMENT
    ≠
AUTHENTICATION
    ≠
CONSENSUS
    ≠
FINALITY
    ≠
EXECUTION
    ≠
SETTLEMENT
```

These concepts can interact, but they are not interchangeable.

### Commitment

A commitment answers:

> **What is this object or relationship cryptographically bound to?**

### Authentication

Authentication answers:

> **Who or what can establish the claimed source or authority?**

### Consensus

Consensus answers:

> **Which state does the external network accept?**

### Finality

Finality answers:

> **When can an accepted state be treated as sufficiently irreversible for the relevant application?**

### Execution

Execution answers:

> **What actually happened when an action was performed?**

### Settlement

Settlement answers:

> **What became established on the external system according to that system's own rules?**

A commitment can prove that a particular output was bound to a particular input.

It does not, by itself, prove that the underlying input was consensually accepted.

It does not create finality.

It does not execute a transaction.

It does not establish settlement.

This distinction is fundamental to the Rainbow Ring architecture.

---

# 3. Native State Commitment

The first commitment exists at the boundary between the sovereign blockchain and the Native Conduit.

```text
NATIVE BLOCKCHAIN
       │
       ▼
 NATIVE STATE
       │
       ▼
nativeStateCommitment
```

`nativeStateCommitment` binds the PrismInput to a defined representation of external native state.

For Ethereum, the current native-state model includes:

```text
blockHash
parentHash
stateRoot
transactionsRoot
receiptsRoot
blockNumber
```

The exact authentication and proof mechanism remains chain-specific.

The commitment should therefore preserve native identity rather than abstracting away the information needed to understand where the state came from.

### The commitment establishes

> **This PrismInput refers to this defined native state representation.**

### The commitment does not establish

> “This state is automatically final.”

or:

> “Ethereum consensus has been completely proven.”

or:

> “This state has been settled by PrismChain.”

Those are separate questions.

---

# 4. PrismInput Commitment

After native state has been identified, validated, authenticated to the extent currently supported, committed, and normalized, the Native Conduit constructs `PrismInput`.

The current structure is:

```text
PrismInput.Data

chainId
nativeStateCommitment
stateReference
authenticationCommitment
normalizedState
```

The next relationship is:

```text
nativeStateCommitment
        │
        ▼
    PrismInput
        │
        ▼
 inputCommitment
```

`inputCommitment` binds the downstream PrismChain computation to the specific PrismInput that entered the system.

This provides an explicit connection between:

```text
External State
      ↓
PrismInput
      ↓
PrismChain
```

Without this relationship, a later output could be difficult to associate with the exact input state from which it originated.

---

# 5. Input Commitment and Traceability

The input commitment creates a traceable boundary.

Conceptually:

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
PrismChain computation
```

The important property is not simply that hashes exist.

The important property is that each commitment has a defined semantic role.

A valid implementation should allow an investigator to ask:

```text
Which native state?
        ↓
Which PrismInput?
        ↓
Which computation?
        ↓
Which White Light Block?
        ↓
Which PrismOutput?
        ↓
Which Ring relationship?
```

The answer should be deterministically traceable.

---

# 6. The White Light Block

PrismChain performs its computation through its seven spectral layers.

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
```

The White Light Block is the unified result of the seven-layer PrismChain computation.

It is not an eighth layer.

It is not the Rainbow Ring.

It is not an external settlement record.

It is the convergence point of the PrismChain computation.

The commitment architecture must therefore bind the output boundary to the actual White Light Block produced by PrismChain.

It must not create a second computation merely to generate a convenient output hash.

---

# 7. Result Commitment

The `resultCommitment` binds `PrismOutput` to the actual PrismChain result.

The intended relationship is:

```text
PrismChain
     │
     ▼
White Light Block
     │
     ▼
resultCommitment
     │
     ▼
PrismOutput
```

This is one of the most important boundaries in the system.

The result commitment should ultimately represent the actual WLB produced by PrismChain.

It must not silently represent:

* a reconstructed result,
* an independently recomputed result,
* a Solidity replacement for PrismChain,
* a second WLB implementation,
* or an unrelated summary of the computation.

The principle is:

> **The output commitment must bind to the result that PrismChain actually produced.**

This preserves the distinction between PrismChain's computational core and the integration layer surrounding it.

---

# 8. Rules Commitment

The output also contains:

```text
rulesCommitment
```

This commitment binds the output to the rules and execution context under which the output is intended to be interpreted or acted upon.

Conceptually:

```text
RULES / EXECUTION CONTEXT
          │
          ▼
   rulesCommitment
          │
          ▼
      PrismOutput
```

This prevents an output from being interpreted independently of the conditions under which it was created.

The exact contents of the rules commitment should be determined by implementation and testing.

The public architecture therefore defines its purpose without inventing an implementation that has not yet been demonstrated.

---

# 9. Execution Conditions

`PrismOutput` also contains:

```text
executionConditions
```

These conditions define what must be true before an external action is considered eligible to proceed.

They are distinct from the result itself.

```text
RESULT
  ≠
EXECUTION CONDITIONS
```

A valid PrismChain result does not automatically mean that an external blockchain should execute an action.

The Ring must be able to reason about the relationship between:

```text
What PrismChain produced
        +
What conditions must be satisfied
        +
What actually happened externally
```

That distinction becomes particularly important when external systems can experience:

* reorganization,
* stale state,
* expiration,
* replay,
* transaction failure,
* conflicting execution,
* or other state transitions.

---

# 10. Commitment Chain

The complete commitment architecture can be represented as:

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
                      │
              ┌───────┴────────┐
              │                │
              ▼                ▼
      rulesCommitment   executionConditions
              │                │
              └───────┬────────┘
                      ▼
                 RAINBOW RING
```

This creates a chain of traceability.

It does not mean every element is generated by the same hash function or using the same serialization.

Each commitment must be defined according to the object and domain it represents.

---

# 11. Domain Separation

Commitments must not become ambiguous simply because two different objects happen to contain similar information.

The current commitment domains include:

```text
PRISM_INPUT
PRISM_OUTPUT
```

Domain separation establishes that a commitment belongs to a particular semantic namespace.

Conceptually:

```text
PRISM_INPUT
    +
canonical input representation
    ↓
input commitment
```

and:

```text
PRISM_OUTPUT
    +
canonical output representation
    ↓
output commitment
```

A commitment generated for one domain should not be silently reusable as though it were a commitment from another domain.

This protects against cross-context interpretation.

---

# 12. Canonical Serialization

Commitments are only meaningful if the data being committed is represented consistently.

Therefore the commitment system must define:

* field order,
* field types,
* encoding,
* versioning,
* domain separation,
* treatment of empty values,
* treatment of optional values,
* and any relevant normalization rules.

Two implementations representing the same logical object must not produce different commitments merely because they serialized the object differently.

Likewise, two semantically different objects must not accidentally produce the same commitment because their representations were ambiguously constructed.

The current PrismInput and PrismOutput serializers establish versioned representations for their respective commitment domains.

The implementation remains the source of truth for exact serialization behavior.

---

# 13. Versioning

Commitment formats must be versioned.

A commitment is not only a hash.

It is a hash over a defined representation.

Changing the representation can change the commitment even if the underlying conceptual object appears unchanged.

Therefore:

```text
VERSION
   +
DOMAIN
   +
CANONICAL REPRESENTATION
   ↓
COMMITMENT
```

When serialization changes, the commitment specification and compatibility behavior must be tested explicitly.

Do not silently change a commitment format while treating the resulting values as interchangeable with earlier versions.

---

# 14. Commitment vs Authentication

The Native Conduit currently distinguishes:

```text
nativeStateCommitment
authenticationCommitment
```

These are intentionally separate.

The commitment establishes what representation is being bound.

Authentication establishes evidence concerning the source or authority of that representation.

For example:

```text
native state
    │
    ├──────────────► commitment
    │
    └──────────────► authentication evidence
```

One does not replace the other.

For Ethereum, the current `EthereumPrismInputBuilder` contains deterministic authentication plumbing/prototype behavior.

That must not be described as a complete Ethereum consensus proof unless and until the implementation actually establishes that property.

---

# 15. Rainbow Ring Relationship

Rainbow Ring consumes the commitment relationships.

It does not create a substitute PrismChain result.

The relationship is:

```text
PrismInput
    │
    ▼
PrismChain
    │
    ▼
WLB
    │
    ▼
PrismOutput
    │
    ├── inputCommitment
    ├── rulesCommitment
    ├── resultCommitment
    └── executionConditions
             │
             ▼
        Rainbow Ring
```

The Ring uses these relationships to establish and manage the connection between PrismChain and the external system.

The Ring therefore operates on evidence and relationships rather than replacing the computation that produced the result.

---

# 16. Input-to-Output Traceability

A central security property is the ability to trace an output backward.

Given a `PrismOutput`, an investigator should ultimately be able to determine:

```text
PrismOutput
     ↓
resultCommitment
     ↓
White Light Block
     ↓
PrismChain computation
     ↓
inputCommitment
     ↓
PrismInput
     ↓
nativeStateCommitment
     ↓
native state
```

The reverse relationship should also be possible:

```text
native state
     ↓
PrismInput
     ↓
PrismChain
     ↓
WLB
     ↓
PrismOutput
     ↓
Rainbow Ring relationship
```

This bidirectional traceability is more important than simply producing hashes.

The hashes are useful because they make the relationships cryptographically testable.

---

# 17. Replay Protection

Commitments must be evaluated in the context of replay.

A valid commitment does not automatically mean that the associated action is valid to execute again.

The system must distinguish between:

```text
same data
same commitment
same relationship
same execution
```

These are not necessarily the same thing.

Replay protection may require additional context such as:

* chain identity,
* state reference,
* execution conditions,
* relationship identity,
* lifecycle state,
* expiration,
* nonce or equivalent sequencing,
* or external execution evidence.

The exact mechanism must be determined through implementation and testing.

---

# 18. Cross-Chain Isolation

Commitments must preserve chain identity.

A commitment associated with Ethereum must not accidentally become interpretable as though it originated from another sovereign chain.

This is one reason `chainId` exists within `PrismInput`.

The broader invariant is:

> **A relationship to one sovereign blockchain must not silently become a relationship to another sovereign blockchain.**

This becomes increasingly important as additional Native Conduits are implemented.

Planned conduit identities include:

```text
PRISM-ETH-01
PRISM-BTC-02
PRISM-SOL-03
PRISM-BASE-04
PRISM-AVAX-05
PRISM-SUI-06
PRISM-IBC-07
```

These identify planned integration boundaries.

They do not mean those integrations are currently implemented.

---

# 19. Reorganization and Stale State

Commitments do not eliminate external blockchain state transitions.

A previously committed state may later become stale or invalid for the application's intended purpose.

Therefore the system must account for:

```text
REORG
STALE STATE
EXPIRED OUTPUT
REPLAY
CONFLICTING EXECUTION
```

The commitment remains a commitment to the representation that was actually committed.

What changes is the interpretation of whether that state remains eligible for a particular downstream relationship.

This distinction is critical.

A cryptographically valid commitment can remain valid as a commitment while the underlying state becomes unsuitable for execution.

---

# 20. Mutation Testing

Commitments should be tested by deliberately changing the information they are supposed to bind.

Examples include:

```text
Change chainId
Change blockHash
Change stateRoot
Change blockNumber
Change normalizedState
Change input data
Change rules
Change execution conditions
Change WLB result
```

Expected behavior:

```text
MUTATION
   ↓
COMMITMENT CHANGES
   ↓
DEPENDENT RELATIONSHIP NO LONGER MATCHES
```

A commitment system that does not detect meaningful mutations is not providing the binding property it claims to provide.

Testing should therefore include:

* positive commitment tests,
* negative commitment tests,
* serialization tests,
* domain separation tests,
* mutation tests,
* replay tests,
* cross-chain tests,
* stale-state tests,
* reorganization tests where applicable,
* and integration tests connecting actual PrismChain output.

---

# 21. WLB Mutation Experiment

A particularly important experiment concerns the relationship between `resultCommitment` and the actual White Light Block.

The experiment should establish that changing the actual WLB changes the resulting commitment.

Conceptually:

```text
WLB A
  ↓
resultCommitment A

WLB B ≠ WLB A
  ↓
resultCommitment B

resultCommitment B ≠ resultCommitment A
```

The important question is not merely whether a hash changes.

The important question is:

> **Does the commitment remain cryptographically bound to the actual PrismChain result?**

This experiment should eventually be performed against the real Clean Version PrismChain implementation rather than a substitute computation.

---

# 22. Input Mutation Experiment

Likewise, modifying a meaningful PrismInput field should invalidate the expected downstream relationship.

For example:

```text
PrismInput A
    ↓
inputCommitment A
    ↓
computation/output relationship A
```

Changing a meaningful input:

```text
PrismInput B ≠ PrismInput A
    ↓
inputCommitment B
```

should prevent the system from treating the resulting relationship as though it were derived from the original input.

This is the practical meaning of input binding.

---

# 23. Rules Mutation Experiment

The same principle applies to `rulesCommitment`.

Changing a rule or execution context that is supposed to affect eligibility should change the rules commitment.

The system should not silently accept:

```text
OUTPUT A
+
RULES B
```

when the output was actually produced under:

```text
OUTPUT A
+
RULES A
```

The commitment relationship exists to make this distinction machine-verifiable.

---

# 24. External Execution Evidence

Commitments end at a particular boundary.

They do not prove external execution merely because an output was created.

The complete relationship must eventually incorporate external evidence:

```text
PrismOutput
     ↓
Rainbow Ring
     ↓
External execution
     ↓
External observation
     ↓
Execution evidence
     ↓
Settlement determination
```

This is why:

> **Do not call something settled because PrismChain says it is settled.**

Likewise:

> **Do not call something executed because it was submitted.**

And:

> **Do not call something final because it was included.**

The external blockchain remains sovereign over its own execution and settlement.

Evidence determines what actually happened.

---

# 25. Security Model

The commitment architecture should protect against at least the following classes of failure:

### Wrong input

An output is associated with the wrong native state.

**Defense:** native-state commitment and input binding.

### Modified input

An input is altered after commitment.

**Defense:** input commitment mismatch.

### Modified result

The output claims a different WLB than PrismChain actually produced.

**Defense:** result commitment bound to the actual WLB.

### Modified rules

An output is interpreted under different rules than those under which it was created.

**Defense:** rules commitment.

### Wrong chain

An output or input is interpreted as belonging to another sovereign blockchain.

**Defense:** chain identity, conduit identity, domain separation, and tests.

### Replay

A valid historical relationship is incorrectly reused.

**Defense:** relationship lifecycle, state references, execution conditions, and replay-specific controls.

### Stale state

A previously valid state is no longer eligible.

**Defense:** state awareness and external-state verification.

### Reorganization

The external blockchain changes the state from which an input was derived.

**Defense:** native-state tracking, reorganization handling, and finality-aware policy.

### False settlement

PrismChain claims external success without external evidence.

**Defense:** external observation and explicit settlement evidence.

---

# 26. What Commitments Prove

A properly defined commitment can establish a cryptographic binding relationship.

For example:

> This `PrismOutput` is bound to this `PrismInput`.

or:

> This `PrismOutput` is bound to this particular White Light Block representation.

or:

> This PrismInput is bound to this defined native-state representation.

Those are meaningful properties.

They should not be expanded into claims the commitment itself cannot support.

A commitment does not independently prove:

* consensus,
* finality,
* execution,
* or settlement.

Those properties require their own evidence.

---

# 27. Evidence Requirements

Every commitment-related claim should eventually have corresponding evidence.

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

For commitments specifically:

```text
CLAIM
  ↓
DEFINED REPRESENTATION
  ↓
COMMITMENT
  ↓
MUTATION TEST
  ↓
INTEGRATION TEST
  ↓
EXTERNAL EVIDENCE
```

The public documentation should distinguish between:

🟢 **Built / Demonstrated**

🔵 **Research**

🟣 **Experimental**

🟡 **Hypothesis / Planned**

🔴 **Private**

The existence of a commitment field in an architectural document does not automatically mean the complete production security property has been demonstrated.

---

# 28. Current Ethereum Boundary

Ethereum is the first Native Conduit being developed.

The intended relationship is:

```text
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
Ethereum execution / settlement
```

The Ethereum integration should establish the commitment chain experimentally before generalizing the architecture to additional sovereign chains.

No Ethereum color assignment should be invented here.

That decision must come from the actual architecture and implementation if one exists.

---

# 29. Implementation Boundary

The commitment architecture describes relationships.

The implementation determines the exact mechanics.

This distinction is intentional.

The system is being developed according to:

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

Specifications are architectural guidance.

They are not treated as immutable implementation contracts before the actual integration has been built and tested.

If implementation reveals that a commitment boundary should change, the architecture should be updated to accurately describe what was actually built.

The goal is not to make the code conform to a diagram at all costs.

The goal is to discover the correct architecture through implementation and evidence.

---

# 30. Public and Private Boundary

The public documentation should expose:

* commitment roles,
* relationships,
* domains,
* serialization principles,
* security properties,
* test methodology,
* demonstrated behavior,
* limitations,
* and evidence.

It should not expose proprietary implementation details that provide an engineering advantage.

The public goal is:

> **Reveal the architecture. Protect the advantage.**

The architecture should be understandable.

The implementation details that constitute proprietary advantage do not need to be.

---

# 31. Commitment Lifecycle

The complete relationship can be summarized as:

```text
1. IDENTIFY
      ↓
2. COMMIT NATIVE STATE
      ↓
3. CONSTRUCT PrismInput
      ↓
4. COMMIT INPUT
      ↓
5. COMPUTE THROUGH PRISMCHAIN
      ↓
6. PRODUCE WHITE LIGHT BLOCK
      ↓
7. COMMIT RESULT
      ↓
8. BIND RULES
      ↓
9. DEFINE EXECUTION CONDITIONS
      ↓
10. CONSTRUCT PrismOutput
      ↓
11. ESTABLISH RAINBOW RING RELATIONSHIP
      ↓
12. EXECUTE EXTERNALLY
      ↓
13. OBSERVE EXTERNAL RESULT
      ↓
14. DETERMINE SETTLEMENT
      ↓
15. RECORD EVIDENCE
```

Each stage answers a different question.

That separation is the architecture.

---

# 32. Core Invariants

The commitment architecture should preserve these invariants:

### Invariant 1 — Native identity

The origin blockchain remains identifiable.

### Invariant 2 — Input binding

PrismChain computation remains traceable to its PrismInput.

### Invariant 3 — Result binding

PrismOutput remains bound to the actual PrismChain result.

### Invariant 4 — Rules binding

Execution interpretation remains bound to its intended rules/context.

### Invariant 5 — Domain separation

Input and output commitments cannot be silently treated as interchangeable domains.

### Invariant 6 — Serialization determinism

Equivalent canonical representations produce equivalent commitments.

### Invariant 7 — Mutation sensitivity

Meaningful changes to committed data change the relevant commitment.

### Invariant 8 — Cross-chain isolation

One sovereign chain's relationship cannot silently become another chain's relationship.

### Invariant 9 — External sovereignty

PrismChain does not create external consensus, execution, or settlement.

### Invariant 10 — Evidence discipline

Claims about execution and settlement require external evidence.

---

# 33. The Relationship in One View

```text
                 SOVEREIGN BLOCKCHAIN
                         │
                         ▼
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
                  resultCommitment
                         │
                         ▼
                    PrismOutput
                         │
               ┌─────────┴─────────┐
               │                   │
               ▼                   ▼
       rulesCommitment      executionConditions
               │                   │
               └─────────┬─────────┘
                         ▼
                    RAINBOW RING
                         │
                         ▼
                EXTERNAL EXECUTION
                         │
                         ▼
                  EXTERNAL EVIDENCE
                         │
                         ▼
                     SETTLEMENT
```

The architecture is therefore not simply:

> blockchain → bridge → blockchain

It is a sequence of explicit relationships between independently defined systems.

---

# 34. Final Principles

The commitment layer exists to make the system's relationships explicit and verifiable.

**Commit the state.**

**Bind the input.**

**Bind the result.**

**Bind the rules.**

**Define the conditions.**

**Verify every relationship.**

Do not confuse commitment with authentication.

Do not confuse authentication with consensus.

Do not confuse consensus with finality.

Do not confuse finality with execution.

Do not confuse execution with settlement.

Do not claim external success without external evidence.

The architecture remains:

> **PrismChain is the seven-layer blockchain.**

> **Prism computes.**

> **Rainbow Ring connects.**

> **The external blockchain remains sovereign.**

> **Evidence determines what the commitments actually prove.**
