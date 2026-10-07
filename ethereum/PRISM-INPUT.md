# ⛓️ Ethereum → PrismInput

> **PrismInput is the formal input boundary through which Ethereum state enters PrismChain.**

This document defines the Ethereum-specific construction and role of `PrismInput`.

The purpose is to establish a controlled transformation:

```text
ETHEREUM
    ↓
Ethereum Native State
    ↓
Ethereum Native Conduit
    ↓
PrismInput
    ↓
PRISMCHAIN
```

The Native Conduit preserves Ethereum's identity.

PrismInput defines how the resulting state representation is presented to PrismChain.

PrismChain then performs its own seven-layer computation.

---

# 1. Purpose

The Ethereum integration needs a precise boundary between Ethereum's native state model and PrismChain's computation model.

That boundary is `PrismInput`.

The architecture is:

```text
Ethereum Native State
        ↓
Ethereum Native Conduit
        ↓
PrismInput
        ↓
PrismChain
```

PrismInput is therefore neither:

* Ethereum state itself,
* the Native Conduit,
* the White Light Block,
* PrismOutput,
* nor Rainbow Ring.

It is the formal input object connecting the Ethereum boundary to PrismChain.

---

# 2. Ethereum Integration Identifier

The planned Ethereum Native Conduit identifier is:

```text
PRISM-ETH-01
```

The relationship should remain explicitly associated with Ethereum throughout the input lifecycle.

Conceptually:

```text
Ethereum
    ↓
PRISM-ETH-01
    ↓
PrismInput
```

This identity must not be silently transferable to another sovereign blockchain.

---

# 3. Current PrismInput Structure

The current `PrismInput.Data` structure is:

```text
chainId
nativeStateCommitment
stateReference
authenticationCommitment
normalizedState
```

Conceptually:

```text
PrismInput.Data
{
    chainId,
    nativeStateCommitment,
    stateReference,
    authenticationCommitment,
    normalizedState
}
```

Each field has a distinct purpose.

---

# 4. `chainId`

`chainId` identifies the sovereign blockchain associated with the input.

For the Ethereum integration, the input must remain explicitly associated with Ethereum.

The purpose is to prevent a valid representation of one chain from being silently interpreted as another chain's input.

Conceptually:

```text
chainId
   ↓
Ethereum
   ↓
PRISM-ETH-01
```

Chain identity must remain intact from the originating state through PrismInput and into the downstream relationship.

---

# 5. `nativeStateCommitment`

`nativeStateCommitment` binds the PrismInput to the Ethereum native state from which it was constructed.

The relationship is:

```text
Ethereum Native State
        ↓
Canonical Representation
        ↓
nativeStateCommitment
        ↓
PrismInput
```

This allows downstream systems to establish which defined Ethereum state representation the input corresponds to.

The commitment does not automatically establish:

* Ethereum consensus,
* canonicality,
* finality,
* execution,
* or settlement.

Those are separate properties.

---

# 6. `stateReference`

`stateReference` preserves an explicit reference to the originating Ethereum state.

The purpose is traceability.

A downstream investigator should be able to determine:

> **Which Ethereum state produced this PrismInput?**

The reference may correlate with information such as:

```text
Ethereum chain identity
+
block identity
+
state context
```

The exact final representation is an implementation concern.

The important requirement is that the relationship remain recoverable.

---

# 7. `authenticationCommitment`

`authenticationCommitment` represents authentication information associated with the Ethereum state presented through the Native Conduit.

The current implementation includes deterministic authentication prototype plumbing.

This must be described accurately.

It is not currently equivalent to a complete Ethereum consensus proof.

The architecture therefore maintains the distinction:

```text
AUTHENTICATION
      ≠
CONSENSUS
      ≠
FINALITY
```

A future implementation may strengthen this boundary as actual Ethereum verification requirements are established.

---

# 8. `normalizedState`

`normalizedState` is the representation of Ethereum information prepared for consumption by PrismChain.

The transformation is:

```text
Ethereum Native State
        ↓
Preserve Native Identity
        ↓
Validate / Authenticate
        ↓
Normalize
        ↓
PrismInput
```

Normalization exists to provide PrismChain with a consistent input representation without pretending that Ethereum's native state model is identical to PrismChain's internal model.

The exact normalized representation must remain synchronized with the actual implementation.

---

# 9. Native State Is Preserved Before Normalization

The integration must not normalize away Ethereum identity before establishing the native-state relationship.

The intended sequence is:

```text
NATIVE STATE
     ↓
IDENTIFY
     ↓
VALIDATE
     ↓
AUTHENTICATE
     ↓
COMMIT
     ↓
NORMALIZE
     ↓
CONSTRUCT PrismInput
```

This ordering preserves the distinction between:

* what Ethereum actually supplied,
* what the conduit verified or authenticated,
* what was committed,
* and what PrismChain ultimately consumes.

---

# 10. Ethereum Native State

The current Ethereum native-state representation contains:

```text
blockHash
parentHash
stateRoot
transactionsRoot
receiptsRoot
blockNumber
```

The PrismInput construction therefore begins with:

```text
EthereumNativeState
        ↓
Ethereum Native Conduit
```

The Native Conduit is responsible for transforming that native representation into the PrismInput boundary.

---

# 11. PrismInput Construction

Conceptually, the construction process is:

```text
Ethereum Native State
        ↓
Read
        ↓
Identify
        ↓
Validate
        ↓
Authenticate
        ↓
Commit
        ↓
Normalize
        ↓
Construct PrismInput
```

The resulting object contains the defined input fields:

```text
chainId
nativeStateCommitment
stateReference
authenticationCommitment
normalizedState
```

The exact mechanics of construction are implementation-defined.

---

# 12. Input Lifecycle

The Ethereum PrismInput lifecycle is:

```text
DISCOVER
   ↓
READ
   ↓
IDENTIFY
   ↓
VALIDATE
   ↓
AUTHENTICATE
   ↓
COMMIT
   ↓
NORMALIZE
   ↓
CONSTRUCT
   ↓
SUBMIT
```

Each stage has a distinct responsibility.

---

# 13. Discover

The integration first determines which Ethereum state is being considered.

This may involve identifying:

* the relevant Ethereum chain,
* the relevant block,
* the relevant state context,
* and the information required for the intended operation.

The integration should not construct a PrismInput from an ambiguous or unidentified state.

---

# 14. Read

The Native Conduit obtains the required Ethereum native-state information.

Current representation:

```text
blockHash
parentHash
stateRoot
transactionsRoot
receiptsRoot
blockNumber
```

The conduit should preserve the values as obtained before normalization.

---

# 15. Identify

The integration establishes the identity of the originating system and state.

Conceptually:

```text
Ethereum
    ↓
PRISM-ETH-01
    ↓
specific Ethereum state
```

This prevents a generic state object from losing its chain context.

---

# 16. Validate

The Native Conduit checks that the native-state representation satisfies the requirements of the input boundary.

Validation may include:

* required fields,
* valid encoding,
* expected chain identity,
* internal consistency,
* supported representation version,
* and other requirements established by implementation.

Validation should reject malformed or ambiguous input rather than silently repairing it.

---

# 17. Authenticate

Authentication establishes whatever source or integrity evidence the current conduit implementation provides.

The current Ethereum builder includes deterministic authentication prototype behavior.

That behavior should be treated as an experimental implementation component until stronger Ethereum-specific guarantees have been established.

The documentation must therefore avoid saying:

> “PrismInput proves Ethereum consensus.”

That would be a stronger claim than the current implementation supports.

---

# 18. Commit

The Native Conduit establishes:

```text
nativeStateCommitment
```

This binds the PrismInput to the defined Ethereum native-state representation.

The input relationship becomes:

```text
Ethereum Native State
        ↓
nativeStateCommitment
        ↓
PrismInput
```

This is a binding relationship, not a replacement for Ethereum consensus.

---

# 19. Normalize

After the originating state has been identified and committed, the relevant information is normalized into the representation required by PrismChain.

Conceptually:

```text
Ethereum Native Representation
        ↓
Normalization
        ↓
PrismInput.normalizedState
```

Normalization should not silently change the meaning of the underlying Ethereum state.

If a transformation changes semantics, that transformation must be explicitly defined and tested.

---

# 20. Construct

The final PrismInput is assembled from the validated components.

Conceptually:

```text
chainId
nativeStateCommitment
stateReference
authenticationCommitment
normalizedState
        ↓
PrismInput
```

The object then becomes eligible for submission to PrismChain.

---

# 21. Submit

Submission is the boundary at which PrismInput enters PrismChain.

```text
Ethereum
   ↓
Native Conduit
   ↓
PrismInput
   ↓
PRISMCHAIN
```

Once submitted, PrismChain operates on the input according to its own architecture.

The Native Conduit does not become a PrismChain computation layer.

---

# 22. PrismChain Computation

The PrismInput enters the existing seven-layer PrismChain architecture:

```text
PrismInput
    ↓
RED
ORANGE
YELLOW
GREEN
BLUE
INDIGO
VIOLET
    ↓
WHITE LIGHT BLOCK
```

The seven spectral layers remain the blockchain.

The WLB remains the unified computational result.

Ethereum does not receive a special PrismChain layer.

---

# 23. No Invented Ethereum Color Assignment

The Ethereum integration must not invent a spectral layer assignment for Ethereum.

Ethereum is external to the seven-layer PrismChain architecture.

The correct path is:

```text
Ethereum
    ↓
Native Conduit
    ↓
PrismInput
    ↓
Seven PrismChain Layers
```

There is no:

```text
Ethereum Layer
```

and there is no eighth layer created for Ethereum.

If a future architecture requires a specific spectral relationship, that decision must come from the actual architecture and implementation rather than assumption.

---

# 24. Input Commitment

The PrismInput participates in a second commitment relationship downstream of native state:

```text
nativeStateCommitment
        ↓
PrismInput
        ↓
inputCommitment
        ↓
PrismChain
```

The `inputCommitment` binds the downstream PrismChain relationship to the actual PrismInput.

This creates two distinct bindings:

```text
Ethereum State
      ↓
nativeStateCommitment
      ↓
PrismInput
      ↓
inputCommitment
      ↓
PrismChain
```

These commitments should not be conflated.

---

# 25. Commitment Domains

The input commitment uses the defined Prism input commitment domain:

```text
PRISM_INPUT
```

Domain separation prevents a commitment created for one purpose from being silently interpreted as a commitment for another purpose.

Conceptually:

```text
PRISM_INPUT
     +
canonical PrismInput representation
     ↓
inputCommitment
```

The exact serialization and hashing behavior must remain synchronized with the implementation.

---

# 26. Serialization

PrismInput serialization is part of the commitment boundary.

The current architecture uses a versioned serialization model based on:

```text
VERSION = 1
```

with the defined PrismInput fields.

Conceptually:

```text
VERSION
+
chainId
+
nativeStateCommitment
+
stateReference
+
authenticationCommitment
+
normalizedState
        ↓
canonical serialized representation
        ↓
commitment
```

Serialization must be deterministic.

Field order must be explicit.

Encoding must be unambiguous.

Version changes must be deliberate.

---

# 27. Determinism

The same PrismInput must produce the same serialized representation and commitment when all relevant inputs are identical.

Conceptually:

```text
PrismInput A
      ↓
Serialization A
      ↓
Commitment A

PrismInput A
      ↓
Serialization A
      ↓
Commitment A
```

Expected:

```text
Commitment A == Commitment A
```

Meaningful mutation should produce a different commitment.

---

# 28. Mutation Testing

Each meaningful PrismInput field should be tested for commitment sensitivity.

For example:

```text
Original PrismInput
        ↓
inputCommitment A
```

Change:

```text
chainId
```

Then:

```text
Mutated PrismInput
        ↓
inputCommitment B
```

Expected:

```text
A ≠ B
```

The same principle should be tested for:

* `nativeStateCommitment`,
* `stateReference`,
* `authenticationCommitment`,
* `normalizedState`.

The purpose is to verify that the commitment actually binds the fields the architecture says it binds.

---

# 29. Input-to-Output Traceability

PrismInput exists partly to establish traceability from Ethereum into PrismChain.

The intended relationship is:

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

This allows the final result to remain connected to its originating external state.

---

# 30. Reorganization Handling

Ethereum state can become unsuitable for continued use because the chain context changes.

The PrismInput architecture must therefore support identifying when an input is affected by a reorganization.

Conceptually:

```text
Ethereum State A
       ↓
PrismInput A
       ↓
PrismChain
       ↓
Ethereum chain context changes
       ↓
State A requires re-evaluation
```

The final reorganization behavior is an implementation question.

Possible outcomes may include:

```text
VALID
REPLACED
STALE
REORGED
REJECTED
```

The actual state machine should be determined by testing.

---

# 31. Stale Input Handling

A valid PrismInput at time `T1` does not automatically remain suitable at `T2`.

The integration therefore needs a policy for stale inputs.

Potential considerations include:

* block age,
* relationship expiration,
* required finality,
* current Ethereum state,
* execution conditions,
* and application-specific validity windows.

The exact policy should not be invented before the implementation requires it.

---

# 32. Replay Protection

PrismInput must not become an unintended replay mechanism.

A previously processed input should not automatically authorize a second external action.

The relationship may eventually incorporate:

* unique relationship identifiers,
* input commitments,
* execution conditions,
* consumption state,
* expiration,
* or other replay controls.

The implementation must demonstrate that the chosen mechanism works.

---

# 33. Wrong-Chain Protection

A PrismInput created for Ethereum must remain associated with Ethereum.

The complete identity relationship is:

```text
Ethereum
    ↓
PRISM-ETH-01
    ↓
chainId
    ↓
nativeStateCommitment
    ↓
PrismInput
```

A valid PrismInput from another chain must not be accepted merely because its fields have the same general shape.

Cross-chain identity is a security property.

---

# 34. Failure Behavior

The input boundary should fail explicitly when required conditions are not satisfied.

Examples include:

```text
MISSING STATE
INVALID STATE
WRONG CHAIN
INVALID ENCODING
AUTHENTICATION FAILURE
COMMITMENT MISMATCH
INVALID NORMALIZATION
STALE INPUT
REPLAY
UNSUPPORTED VERSION
```

The integration should prefer explicit rejection over silent correction.

A failed boundary condition is evidence about the system.

---

# 35. What PrismInput Does Not Do

PrismInput does not:

* execute Ethereum transactions,
* settle Ethereum transactions,
* replace Ethereum consensus,
* establish Ethereum finality by itself,
* compute the White Light Block,
* establish Rainbow Ring relationships,
* or determine external settlement.

Its role is narrower:

> **Present a defined, traceable representation of external state to PrismChain.**

---

# 36. Relationship to PrismOutput

PrismInput is the beginning of the PrismChain relationship.

PrismOutput is the corresponding external result boundary.

The complete relationship is:

```text
PrismInput
    ↓
PrismChain
    ↓
White Light Block
    ↓
PrismOutput
```

The two boundaries must remain connected through commitments.

```text
inputCommitment
        ↓
PrismChain
        ↓
resultCommitment
```

This provides the basis for the later Rainbow Ring relationship.

---

# 37. Relationship to Rainbow Ring

Rainbow Ring does not consume raw Ethereum state directly as a substitute for PrismInput.

The intended path is:

```text
Ethereum
    ↓
Native Conduit
    ↓
PrismInput
    ↓
PrismChain
    ↓
PrismOutput
    ↓
Rainbow Ring
```

This keeps the input boundary, computation boundary, output boundary, and relationship boundary distinct.

---

# 38. Evidence Requirements

A complete Ethereum PrismInput demonstration should be able to show:

```text
Ethereum State
        ↓
nativeStateCommitment
        ↓
PrismInput
        ↓
inputCommitment
        ↓
PrismChain
```

The evidence should establish:

* which Ethereum state was used,
* which PrismInput was constructed,
* which commitments were generated,
* which serialization was used,
* and whether the same values can be reproduced.

The goal is inspectable traceability rather than assertion.

---

# 39. Testing Requirements

The Ethereum PrismInput boundary should eventually include tests for:

### Construction

A valid Ethereum native state produces a valid PrismInput.

### Field preservation

Required information survives construction correctly.

### Chain identity

Ethereum inputs remain associated with the Ethereum conduit.

### Authentication

Authentication behavior matches the guarantees claimed by the implementation.

### Serialization

Equivalent PrismInputs serialize identically.

### Commitment determinism

Equivalent PrismInputs produce identical commitments.

### Mutation sensitivity

Meaningful changes alter the commitment.

### Missing data

Required information cannot silently disappear.

### Wrong-chain input

A foreign-chain input is rejected.

### Replay

Previously consumed inputs cannot be reused incorrectly.

### Stale state

Inputs outside their valid context are rejected or re-evaluated according to policy.

### Reorganization

Changed Ethereum chain context is handled explicitly.

### End-to-end traceability

The resulting WLB can ultimately be associated with the originating PrismInput.

---

# 40. Current Implementation Status

The Ethereum PrismInput boundary currently includes architectural and implementation work around:

🟣 **Experimental / active development**

* `PrismInput.Data`
* deterministic serialization
* `PRISM_INPUT` commitment domain
* Ethereum native-state representation
* `EthereumPrismInputBuilder`
* deterministic authentication prototype
* Ethereum Native Conduit plumbing

The current authentication mechanism should not be represented as a complete Ethereum consensus proof.

The final integration remains subject to implementation and testing.

---

# 41. What Is Defined

🟢 **Defined**

* Ethereum is the first integration.
* Native Conduit identifier is `PRISM-ETH-01`.
* PrismInput has five defined fields.
* Ethereum native state has a defined initial representation.
* Native state is committed before becoming a PrismChain input.
* PrismInput has a distinct input commitment.
* `PRISM_INPUT` is the input commitment domain.
* PrismInput is upstream of PrismChain computation.
* PrismInput is distinct from PrismOutput and Rainbow Ring.

---

# 42. What Remains to Be Proven

🔵 **To be proven through implementation and testing**

* Complete Ethereum state acquisition.
* Appropriate Ethereum authentication.
* Consensus-level verification where required.
* Finality requirements.
* Final normalization rules.
* Complete integration with the actual PrismChain runtime.
* Reorganization behavior.
* Stale-state behavior.
* Replay protection.
* Complete end-to-end traceability.
* Production-ready Ethereum integration.

---

# 43. What Is Not Being Claimed

This document does not claim that PrismInput itself:

* proves Ethereum consensus,
* proves Ethereum finality,
* proves Ethereum execution,
* proves Ethereum settlement,
* or creates trustless interoperability merely by existing.

PrismInput is an input boundary.

Stronger claims require stronger evidence.

---

# 44. Implementation Discovery

The specification describes the intended architectural boundary.

It does not override implementation evidence.

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

If the implementation reveals that PrismInput needs to change, the architecture should change with it.

If testing reveals that a commitment does not bind what it was intended to bind, the implementation and specification must be corrected.

If Ethereum requires additional native evidence, that evidence should be added because the integration demonstrates that it is necessary—not because the architecture guessed it in advance.

The final specification should describe what the system actually builds and proves.

---

# 45. Public / Private Boundary

The public documentation should expose:

* the PrismInput architecture,
* its public fields,
* commitment relationships,
* Ethereum boundary semantics,
* testing requirements,
* implementation status,
* demonstrated behavior,
* and known limitations.

It should not unnecessarily expose proprietary implementation details.

The governing principle remains:

> **Reveal the architecture. Protect the advantage.**

---

# 46. Final Principles

**Ethereum supplies native state.**

**The Native Conduit preserves Ethereum identity.**

**PrismInput defines the formal input boundary.**

**Native state is committed before entering the PrismChain relationship.**

**Authentication is not consensus.**

**Commitment is not finality.**

**PrismInput is not computation.**

**PrismInput does not execute or settle Ethereum transactions.**

**The seven PrismChain layers perform the computation.**

**The White Light Block remains the PrismChain computational result.**

**PrismOutput represents that result at the external boundary.**

**Rainbow Ring establishes the relationship with Ethereum.**

**Ethereum remains sovereign over its own execution and settlement.**

**Evidence determines what the integration can actually claim.**

The complete input-side relationship is:

```text
ETHEREUM
    ↓
NATIVE STATE
    ↓
ETHEREUM NATIVE CONDUIT
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
```

> **Preserve the native state. Authenticate what can be authenticated. Commit what must be bound. Normalize without losing meaning. Construct the input. Then let PrismChain compute.**

**Connect systems without confusing them.**
