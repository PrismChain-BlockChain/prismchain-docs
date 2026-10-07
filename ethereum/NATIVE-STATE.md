# ⛓️ Ethereum Native State

> **Native state is Ethereum's state. The Native Conduit preserves that state before presenting a defined representation to PrismChain.**

This document defines the Ethereum native-state boundary used by the PrismChain Ethereum integration.

It does not redefine Ethereum.

It does not replace Ethereum consensus.

It does not claim that a commitment to Ethereum state is equivalent to proof of Ethereum consensus or finality.

The purpose is to establish a precise starting point for the first PrismChain Native Conduit.

---

# 1. Purpose

The Ethereum Native Conduit needs a defined representation of the Ethereum state that it is connecting to PrismChain.

The current architectural path is:

```text
ETHEREUM
    ↓
ETHEREUM NATIVE STATE
    ↓
ETHEREUM NATIVE CONDUIT
    ↓
PrismInput
```

The native-state layer exists so that the integration does not immediately collapse Ethereum's native concepts into generic PrismChain concepts.

The principle is:

> **Preserve native identity before normalization.**

---

# 2. Ethereum Remains the Source of Truth

Ethereum remains authoritative for its own state.

PrismChain does not become the source of truth for Ethereum.

The Native Conduit does not become the source of truth for Ethereum.

Rainbow Ring does not become the source of truth for Ethereum.

The relationship is:

```text
Ethereum
    │
    │ defines its own state
    ▼
Native State
    │
    │ represented to PrismChain
    ▼
Native Conduit
    │
    ▼
PrismInput
```

PrismChain can compute using information originating from Ethereum.

It cannot redefine what Ethereum considers valid Ethereum state.

---

# 3. Current Native-State Representation

The current Ethereum-specific native-state structure contains:

```text
blockHash
parentHash
stateRoot
transactionsRoot
receiptsRoot
blockNumber
```

Conceptually:

```text
EthereumNativeState
{
    blockHash,
    parentHash,
    stateRoot,
    transactionsRoot,
    receiptsRoot,
    blockNumber
}
```

This is the current integration representation.

It is a defined boundary structure, not a claim that these six fields constitute every piece of Ethereum state relevant to every future use case.

---

# 4. `blockHash`

`blockHash` identifies the Ethereum block associated with the native-state representation.

Conceptually:

```text
Ethereum Block
      ↓
blockHash
```

This provides a direct reference to the block from which the represented state originates.

It is important for:

* state identity,
* traceability,
* replay analysis,
* relationship binding,
* and external evidence.

A block hash should not be treated as a synonym for finality.

A block can be identified without automatically establishing that the block satisfies whatever finality requirement a particular application requires.

---

# 5. `parentHash`

`parentHash` identifies the parent block referenced by the represented Ethereum block.

Conceptually:

```text
PARENT BLOCK
     ↓
parentHash
     ↓
CURRENT BLOCK
     ↓
blockHash
```

This preserves part of Ethereum's native chain relationship.

It can help establish:

* ancestry,
* continuity,
* state-transition context,
* reorganization analysis,
* and consistency checks.

The parent relationship is especially important when evaluating whether an observed Ethereum state remains part of the chain being relied upon.

---

# 6. `stateRoot`

`stateRoot` identifies the Ethereum state commitment associated with the represented block.

Conceptually:

```text
Ethereum Block
      ↓
stateRoot
      ↓
Ethereum State
```

This field is important because the integration may need to distinguish between:

* the identity of a block,
* the committed Ethereum state associated with that block,
* and evidence concerning that state.

The presence of `stateRoot` in the native-state representation does not by itself constitute proof that PrismChain has independently verified the underlying Ethereum state.

The verification model must be established by the actual conduit implementation.

---

# 7. `transactionsRoot`

`transactionsRoot` identifies the transaction commitment associated with the represented Ethereum block.

Conceptually:

```text
Ethereum Block
      ↓
transactionsRoot
      ↓
Transactions
```

This preserves native Ethereum information concerning the transactions associated with the block.

It may become relevant to:

* transaction inclusion,
* input identification,
* relationship traceability,
* execution analysis,
* and external evidence.

The integration should preserve the distinction between identifying a transaction commitment and proving that a particular transaction satisfies a required execution or settlement condition.

---

# 8. `receiptsRoot`

`receiptsRoot` identifies the receipt commitment associated with the represented Ethereum block.

Conceptually:

```text
Ethereum Block
      ↓
receiptsRoot
      ↓
Transaction Receipts
```

Receipts can become important when determining what happened after an Ethereum transaction was submitted.

The native-state representation therefore preserves this field even though the exact role of receipt evidence in the final Ring lifecycle remains an implementation question.

The important distinction is:

> **A receipt is evidence about Ethereum execution. It is not automatically equivalent to final settlement for every application.**

---

# 9. `blockNumber`

`blockNumber` identifies the numerical position of the represented Ethereum block.

Conceptually:

```text
Ethereum Chain

Block N-1
    ↓
Block N
    ↓
Block N+1
```

The block number provides an additional native reference alongside the block hash.

It can be useful for:

* ordering,
* state references,
* synchronization,
* observation,
* reorganization analysis,
* and testing.

Block number alone does not uniquely establish a canonical or final Ethereum state.

The integration must use the appropriate combination of native identifiers and evidence.

---

# 10. Why Multiple Fields Are Preserved

The native-state representation intentionally preserves multiple Ethereum identifiers rather than reducing everything to one generic value.

The fields provide different relationships:

```text
blockHash
    │
    ├── identifies the block
    │
parentHash
    │
    ├── identifies ancestry
    │
stateRoot
    │
    ├── identifies committed state
    │
transactionsRoot
    │
    ├── identifies transaction commitment
    │
receiptsRoot
    │
    ├── identifies receipt commitment
    │
blockNumber
    │
    └── identifies block position
```

These relationships may become important at different stages of the integration.

The boundary should preserve them before deciding which information is necessary downstream.

---

# 11. Native State vs. Native Conduit

These are not the same thing.

```text
ETHEREUM
   ↓
NATIVE STATE
   ↓
NATIVE CONDUIT
```

**Native state** is information originating from Ethereum.

**Native Conduit** is the mechanism that reads, validates, authenticates, commits, normalizes, and presents that information to PrismChain.

The conduit operates on native state.

It does not create Ethereum state.

---

# 12. Native State vs. PrismInput

Native state is also not the same thing as PrismInput.

The relationship is:

```text
Ethereum Native State
        ↓
Ethereum Native Conduit
        ↓
PrismInput
```

The current PrismInput structure is:

```text
chainId
nativeStateCommitment
stateReference
authenticationCommitment
normalizedState
```

The Native Conduit therefore performs a boundary transformation.

It takes native Ethereum information and produces a representation that PrismChain can consume without losing the identity of the originating system.

---

# 13. Native State Commitment

The Ethereum native-state representation participates in:

```text
nativeStateCommitment
```

Conceptually:

```text
Ethereum Native State
        ↓
Canonical Representation
        ↓
nativeStateCommitment
        ↓
PrismInput
```

The purpose is to bind the PrismInput to a defined representation of Ethereum state.

The commitment should be deterministic.

Equivalent input should produce the same commitment.

A meaningful mutation should produce a different commitment.

These properties must be tested.

---

# 14. Commitment Is Not Proof of Consensus

This distinction is fundamental.

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

A commitment can establish that a particular representation was used.

It does not automatically establish:

* that Ethereum accepted the state,
* that Ethereum consensus finalized the state,
* that the state is canonical,
* that a transaction executed successfully,
* or that a relationship is settled.

Those properties require their own evidence.

---

# 15. Authentication

The current Ethereum integration includes deterministic authentication plumbing/prototype behavior.

This provides a starting point for the boundary.

It should not be described as a complete Ethereum consensus proof.

The correct progression is:

```text
NATIVE STATE
     ↓
AUTHENTICATION
     ↓
COMMITMENT
     ↓
PrismInput
```

The actual security guarantee provided by the authentication mechanism must be demonstrated through implementation and testing.

---

# 16. Canonical Representation

A commitment is only meaningful if the underlying representation is deterministic.

The integration therefore needs a canonical serialization of the native-state structure.

Conceptually:

```text
EthereumNativeState
        ↓
Canonical Serialization
        ↓
Hash / Commitment
```

The serialization must avoid ambiguity caused by:

* field ordering,
* encoding differences,
* representation changes,
* missing values,
* numeric encoding,
* or inconsistent serialization rules.

The exact canonical encoding is an implementation concern and must remain synchronized with the actual code.

---

# 17. Versioning

Native-state representations may evolve.

A future implementation may require:

* additional fields,
* stronger authentication,
* different evidence,
* or different serialization rules.

The integration should therefore treat the native-state representation as versionable rather than assuming that today's structure is permanently sufficient.

Conceptually:

```text
Ethereum Native State
        ↓
Representation Version
        ↓
Canonical Serialization
        ↓
Commitment
```

A representation change must not silently produce an indistinguishable commitment from an incompatible representation.

---

# 18. State Reference

PrismInput includes:

```text
stateReference
```

The state reference provides a way to retain an explicit relationship to the originating Ethereum state.

It should allow the integration to answer:

> **Which Ethereum state was this PrismInput created from?**

The exact contents of `stateReference` are an implementation concern.

The principle is that the relationship must remain traceable.

---

# 19. State Identity

A complete Ethereum state reference should not depend on a single ambiguous identifier when the implementation requires additional context.

The integration may need to correlate:

```text
chain identity
+
block identity
+
state commitment
+
relevant execution context
```

The exact combination should be determined by the actual security and execution requirements.

The goal is to prevent:

* wrong-chain interpretation,
* stale-state reuse,
* accidental cross-context reuse,
* and replay.

---

# 20. Reorganization

Ethereum chain reorganizations are a fundamental consideration for any integration that relies on block-specific state.

The native-state layer therefore needs to preserve enough information to detect or evaluate changes in the chain relationship.

Conceptually:

```text
STATE A
  ↓
BLOCK A
  ↓
OBSERVED

       Ethereum reorganizes

STATE B
  ↓
BLOCK B
  ↓
NEW CANONICAL CONTEXT
```

A previously observed state must not automatically remain authoritative simply because PrismChain already processed it.

The final reorganization policy must be established through implementation and testing.

---

# 21. Stale State

A native state can become stale.

For example:

```text
Ethereum State
      ↓
PrismInput created
      ↓
time passes
      ↓
Ethereum advances
```

The fact that the PrismInput was valid when created does not automatically mean it remains appropriate for every later action.

The integration must distinguish:

* historical state,
* current state,
* stale state,
* canonical state,
* and finalized state

where those distinctions matter to the application.

---

# 22. Replay Protection

Native-state identity also contributes to replay protection.

A relationship created from one Ethereum state should not automatically be reusable in an unrelated context.

The integration must eventually establish protections against:

```text
same input
    ↓
same relationship
    ↓
unintended second execution
```

Possible mechanisms include relationship identity, state references, consumed commitments, nonces, expiration, or execution conditions.

The final mechanism should be discovered through implementation rather than assumed here.

---

# 23. Wrong-Chain Protection

Ethereum native state must remain explicitly associated with Ethereum.

The Native Conduit identifier is:

```text
PRISM-ETH-01
```

The broader integration must preserve chain identity throughout the path:

```text
Ethereum
    ↓
PRISM-ETH-01
    ↓
PrismInput
    ↓
PrismChain
    ↓
PrismOutput
    ↓
Rainbow Ring
    ↓
Ethereum
```

An Ethereum result must not be silently interpreted as belonging to another sovereign blockchain.

---

# 24. Native State and PrismChain Computation

Native state is an input boundary.

It is not itself the PrismChain computation.

The correct relationship is:

```text
Ethereum Native State
        ↓
Native Conduit
        ↓
PrismInput
        ↓
PrismChain
        ↓
Seven Spectral Layers
        ↓
White Light Block
```

The Ethereum integration should therefore adapt Ethereum to PrismChain rather than create a second Ethereum-specific computation system inside PrismChain.

---

# 25. Native State and White Light Block

The WLB is downstream of the Ethereum native-state boundary.

```text
Ethereum Native State
        ↓
PrismInput
        ↓
PrismChain
        ↓
White Light Block
```

The WLB does not replace the native Ethereum state.

It represents the result of PrismChain's own computation after receiving its input.

This distinction must remain intact.

---

# 26. Native State and PrismOutput

The eventual output relationship is:

```text
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
```

This creates a traceable relationship between the external state that entered PrismChain and the PrismChain result that eventually reaches Rainbow Ring.

---

# 27. Native State and Rainbow Ring

Rainbow Ring does not replace the Ethereum Native Conduit.

The separation is:

```text
ETHEREUM
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
ETHEREUM
```

The Native Conduit preserves and presents Ethereum state.

Rainbow Ring manages the relationship around the resulting PrismOutput and external action.

They are complementary components.

They are not interchangeable.

---

# 28. Evidence

The native-state representation provides identifiers and commitments that can participate in an evidence chain.

A future evidence trail may look like:

```text
Ethereum Block
      ↓
blockHash
      ↓
Native State
      ↓
nativeStateCommitment
      ↓
PrismInput
      ↓
inputCommitment
      ↓
White Light Block
      ↓
resultCommitment
      ↓
PrismOutput
      ↓
Rainbow Ring
      ↓
Ethereum Execution Evidence
```

The purpose is traceability.

The purpose is not to pretend that a single hash proves the entire relationship.

---

# 29. Testing Requirements

The native-state boundary should be tested independently before relying on it for complete integration.

At minimum, testing should address:

### Field preservation

Verify that all required native-state fields survive the boundary correctly.

### Serialization

Verify deterministic serialization.

### Commitment determinism

The same native state should produce the same commitment.

### Mutation sensitivity

Changing a meaningful native-state field should change the commitment.

### Field omission

Missing required fields should not silently produce an apparently valid state.

### Wrong-chain identity

Ethereum state must not be accepted as another conduit's native state.

### State-reference integrity

The PrismInput must remain traceable to its originating state.

### Replay behavior

Previously consumed or invalid relationship inputs must not be silently reused.

### Reorganization behavior

Changed chain context must produce the appropriate response.

### Stale-state behavior

State that no longer satisfies the required conditions must not silently remain valid for later execution.

---

# 30. Mutation Testing

Mutation testing is especially important for commitment-based state identity.

For example:

```text
Original
    ↓
EthereumNativeState
    ↓
Commitment A
```

Then mutate one meaningful field:

```text
Mutated
    ↓
EthereumNativeState
    ↓
Commitment B
```

Expected:

```text
Commitment A ≠ Commitment B
```

This should be tested across the relevant fields.

The goal is to establish that the commitment actually binds the information the architecture says it binds.

---

# 31. What Is Currently Defined

🟢 **Defined**

* Ethereum is the first Native Conduit target.
* Conduit identifier: `PRISM-ETH-01`.
* Current native-state fields:

  * `blockHash`
  * `parentHash`
  * `stateRoot`
  * `transactionsRoot`
  * `receiptsRoot`
  * `blockNumber`
* Native state feeds the Ethereum Native Conduit.
* Native state participates in `nativeStateCommitment`.
* Native state is distinct from PrismInput.
* Native state is distinct from PrismChain computation.
* Native state is distinct from Rainbow Ring.
* Ethereum remains sovereign over its own state.

---

# 32. What Is Experimental or Incomplete

🟣 **Experimental / implementation-dependent**

* Ethereum state acquisition.
* Deterministic authentication plumbing.
* Complete Ethereum consensus verification.
* Finality verification.
* Reorganization policy.
* Stale-state policy.
* Replay protection.
* Complete execution evidence model.
* Complete settlement evidence model.
* Final production serialization/versioning policy.

These should not be presented as finished capabilities until implementation and testing establish them.

---

# 33. What Is Not Being Claimed

This document does **not** claim that the current native-state representation:

* independently verifies all Ethereum consensus rules,
* proves Ethereum finality,
* proves transaction execution,
* proves settlement,
* replaces an Ethereum node,
* replaces Ethereum consensus,
* or establishes trustless interoperability by itself.

Those are separate technical properties.

They require separate evidence.

---

# 34. Implementation Discovery

The native-state specification is an architectural boundary.

It is not an excuse to freeze implementation prematurely.

The actual development process remains:

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

If implementation reveals that a field is insufficient, the architecture should be updated.

If testing reveals that an assumption is wrong, the assumption should be corrected.

If Ethereum requires a different evidence model than initially expected, the integration should evolve accordingly.

The code and tests reveal the real boundary.

The documentation should then describe what was actually built and proven.

---

# 35. Public / Private Boundary

The public documentation should expose:

* the native-state model,
* the role of each public field,
* commitment relationships,
* security questions,
* testing requirements,
* demonstrated results,
* and known limitations.

It does not need to expose proprietary implementation details merely to establish the architecture.

The governing principle remains:

> **Reveal the architecture. Protect the advantage.**

---

# 36. Final Principles

**Ethereum defines Ethereum state.**

**The Native Conduit preserves Ethereum identity.**

**Native state is not PrismInput.**

**PrismInput is not PrismChain.**

**A commitment is not consensus.**

**Authentication is not finality.**

**Finality is not execution.**

**Execution is not settlement.**

**The Ethereum Native Conduit does not replace Ethereum.**

**PrismChain computes using its own seven-layer architecture.**

**The White Light Block remains the PrismChain computational result.**

**Rainbow Ring manages the relationship after the PrismChain result reaches the external boundary.**

**Evidence determines what the integration can actually claim.**

The core relationship remains:

```text
ETHEREUM NATIVE STATE
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

> **Preserve the native state. Bind the state. Compute the result. Establish the relationship. Observe the external system. Let evidence determine what actually happened.**

**Connect systems without confusing them.**
