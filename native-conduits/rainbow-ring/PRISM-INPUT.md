# 🌈 Rainbow Ring — PrismInput

> **PrismInput is the formal input boundary through which a Native Conduit presents external blockchain state to PrismChain and establishes the input side of a Rainbow Ring relationship.**

PrismChain is the seven-layer blockchain.

PrismChain computes.

The Native Conduit preserves the identity and native context of the external blockchain.

PrismInput turns that native context into a defined input boundary.

Rainbow Ring ultimately relates the resulting PrismChain computation back to the external system.

The relationship begins here.

---

# 1. Purpose

This document defines the role of **PrismInput** within the Rainbow Ring architecture.

It explains:

* how native blockchain state becomes PrismInput,
* how PrismInput establishes the input boundary,
* how the input becomes traceable through PrismChain,
* how PrismInput relates to the eventual PrismOutput,
* how commitments connect the input to the Rainbow Ring relationship,
* and what remains external to PrismInput.

PrismInput is intentionally narrow.

It is a boundary.

It is not the computation engine.

It is not the White Light Block.

It is not Rainbow Ring.

It is not external settlement.

---

# 2. Position in the Architecture

The complete relationship is:

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

PrismInput is therefore the formal boundary between:

```text
External Native State
        ↓
     PrismChain
```

---

# 3. PrismInput Is a Boundary

PrismInput should be understood as a controlled representation of external state entering PrismChain.

Conceptually:

```text
NATIVE STATE
     ↓
NORMALIZATION
     ↓
PrismInput
     ↓
PRISMCHAIN
```

The Native Conduit performs the chain-specific boundary work.

PrismInput provides the standardized representation presented to PrismChain.

---

# 4. PrismInput Is Not Native State

Native blockchain state and PrismInput are different things.

```text
NATIVE STATE
    ≠
PrismInput
```

Native state belongs to the external blockchain.

PrismInput belongs to the PrismChain integration boundary.

For example, Ethereum may expose native state such as:

```text
blockHash
parentHash
stateRoot
transactionsRoot
receiptsRoot
blockNumber
```

That information can become part of the process that constructs PrismInput.

It does not become PrismChain native state merely because it crosses the boundary.

---

# 5. PrismInput Is Not the Native Conduit

The Native Conduit and PrismInput are also distinct.

```text
NATIVE CONDUIT
    ↓
constructs / validates boundary representation
    ↓
PrismInput
```

The conduit understands the external blockchain.

PrismInput defines what crosses into PrismChain.

This separation allows different external chains to retain their native semantics while presenting a controlled common input boundary.

---

# 6. Current PrismInput Structure

The current public PrismInput structure is:

```text
PrismInput.Data
├── chainId
├── nativeStateCommitment
├── stateReference
├── authenticationCommitment
└── normalizedState
```

Each field has a distinct architectural purpose.

---

# 7. chainId

`chainId` identifies the external blockchain associated with the input.

Conceptually:

```text
PrismInput
     │
     └── chainId
            ↓
      WHICH SYSTEM?
```

This prevents the input from becoming an anonymous collection of state.

Chain identity is particularly important once multiple Native Conduits exist.

---

# 8. nativeStateCommitment

`nativeStateCommitment` binds PrismInput to the native state from which it was constructed.

Conceptually:

```text
NATIVE STATE
      │
      ▼
nativeStateCommitment
      │
      ▼
PrismInput
```

The commitment does not automatically prove:

* consensus,
* finality,
* authenticity,
* or settlement.

It establishes a cryptographic relationship to the represented state.

---

# 9. State Reference

`stateReference` identifies the external state represented by the input.

A state reference can conceptually answer:

> **Which external state are we talking about?**

It may eventually include chain-specific references required by the Native Conduit.

The exact final representation remains an implementation question.

---

# 10. Authentication Commitment

`authenticationCommitment` represents the authentication relationship associated with the input.

It should remain distinct from the state commitment.

```text
nativeStateCommitment
        ≠
authenticationCommitment
```

One binds the input to state.

The other concerns authentication of the source or boundary.

Neither should automatically be described as consensus or finality.

---

# 11. Normalized State

`normalizedState` represents the state after the Native Conduit has transformed native blockchain information into the representation required by PrismChain.

Conceptually:

```text
NATIVE FORMAT
     ↓
NATIVE CONDUIT
     ↓
NORMALIZATION
     ↓
normalizedState
```

Normalization allows PrismChain to work with a defined input representation without requiring PrismChain itself to understand every external blockchain's internal format.

---

# 12. The Input Boundary

The complete input boundary is:

```text
EXTERNAL BLOCKCHAIN
        │
        ▼
    NATIVE STATE
        │
        ▼
 NATIVE CONDUIT
        │
        ├── identify
        ├── validate
        ├── authenticate
        ├── commit
        └── normalize
        │
        ▼
    PrismInput
        │
        ▼
    PRISMCHAIN
```

This is the point where external state becomes an explicit PrismChain input.

---

# 13. PrismInput Lifecycle

The broader Native Conduit lifecycle is:

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

PrismInput is the product of the boundary process.

The exact implementation may evolve as testing reveals what the system actually requires.

---

# 14. PrismInput and PrismChain

PrismInput does not perform PrismChain computation.

Instead:

```text
PrismInput
    ↓
PrismChain
    ↓
Seven-layer computation
    ↓
White Light Block
```

The distinction is fundamental.

> **PrismInput provides the input. PrismChain performs the computation.**

---

# 15. PrismInput and the Seven Layers

The current public implementation demonstrates seven independent spectral layer processes and their convergence into a White Light Block.

PrismInput does not replace those layers.

It provides an external input boundary that can eventually feed the appropriate PrismChain processing path.

The exact mapping between an external input and any particular spectral layer must be established by implementation and evidence.

---

# 16. No Invented Ethereum Color Assignment

Ethereum is the first integration target.

However, PrismInput documentation does not establish an Ethereum-to-color assignment unless the implementation or architecture explicitly establishes one.

Therefore:

> **Do not invent an Ethereum color assignment.**

The integration must determine that relationship through the actual build.

---

# 17. PrismInput and the White Light Block

The relationship is:

```text
PrismInput
     ↓
PRISMCHAIN
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

The White Light Block remains the unified computational result.

PrismInput is not one of the seven layers.

It is not an eighth layer.

It is not the WLB.

---

# 18. Input Commitment

The input commitment establishes a cryptographic relationship between the input boundary and the data used by PrismChain.

Conceptually:

```text
PrismInput
     │
     ▼
inputCommitment
     │
     ▼
PRISMCHAIN
```

This allows downstream output to maintain traceability to the input.

---

# 19. Input Commitment and Native State Commitment

Two different relationships exist:

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
```

The first relationship answers:

> **What native state produced this input?**

The second answers:

> **What PrismChain input does the downstream computation refer to?**

These commitments should not be collapsed into one concept merely for convenience.

---

# 20. PrismInput to PrismOutput

A complete relationship should eventually be traceable:

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
resultCommitment
     ↓
PrismOutput
```

This provides the foundation for the Rainbow Ring relationship.

---

# 21. PrismInput and Rainbow Ring

Rainbow Ring does not replace PrismInput.

Instead, Rainbow Ring uses the input/output relationship established around PrismChain.

Conceptually:

```text
                 RAINBOW RING
                      │
                      │ relationship
                      │
NATIVE STATE → PrismInput → PRISMCHAIN → PrismOutput
```

The input establishes where the computation began.

The output establishes what computation resulted.

The Ring relates that result back to the external system.

---

# 22. Relationship Identity

A future complete relationship may therefore contain references to:

```text
External System
       +
Conduit Identity
       +
PrismInput
       +
Input Commitment
       +
White Light Block
       +
PrismOutput
```

This creates a relationship that can be traced in both directions.

---

# 23. Forward Traceability

Starting from the external state:

```text
EXTERNAL STATE
      ↓
NATIVE CONDUIT
      ↓
PrismInput
      ↓
INPUT COMMITMENT
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
```

This is the forward path.

---

# 24. Backward Traceability

Starting from an external execution:

```text
EXTERNAL EXECUTION
      ↓
RAINBOW RING
      ↓
PrismOutput
      ↓
WHITE LIGHT BLOCK
      ↓
PRISMCHAIN
      ↓
PrismInput
      ↓
NATIVE CONDUIT
      ↓
EXTERNAL STATE
```

A mature system should eventually make this trace possible through inspectable evidence.

---

# 25. Input-to-Output Binding

The input should not disappear after computation begins.

The output should retain a relationship to its originating input.

That relationship is represented through the commitment architecture.

Conceptually:

```text
PrismInput
    │
    ▼
inputCommitment
    │
    ▼
COMPUTATION
    │
    ▼
resultCommitment
    │
    ▼
PrismOutput
```

This provides continuity without requiring PrismOutput to reproduce the entire input.

---

# 26. Rules Commitment

PrismOutput also contains:

```text
rulesCommitment
```

This allows the eventual output relationship to identify the rules or execution context associated with the result.

The relationship therefore becomes:

```text
INPUT
  ↓
COMPUTATION
  ↓
RESULT
  +
RULES
  ↓
OUTPUT
```

The exact rules represented by this commitment remain implementation-dependent.

---

# 27. Execution Conditions

PrismOutput also contains:

```text
executionConditions
```

These conditions belong to the output relationship rather than PrismInput.

Therefore:

```text
PrismInput
    =
INPUT CONTEXT

PrismOutput
    =
RESULT + EXECUTION CONTEXT
```

The distinction prevents input state and output execution requirements from being confused.

---

# 28. Native State Does Not Guarantee Finality

A valid PrismInput does not automatically mean that the referenced external state is final.

This distinction is critical.

```text
NATIVE STATE
    ≠
FINAL STATE
```

The external chain's consensus and finality rules remain external concerns.

The Native Conduit must preserve whatever assumptions are required.

Rainbow Ring must not treat a PrismInput as final merely because it was accepted.

---

# 29. Reorganizations

External blockchains can change their canonical history.

Therefore an input may eventually need to be evaluated against the external chain's reorganization behavior.

Conceptually:

```text
External State A
      ↓
PrismInput
      ↓
COMPUTATION
      ↓
External Chain Reorganizes
      ↓
State A no longer canonical
```

The relationship may then require:

* invalidation,
* re-evaluation,
* waiting,
* re-binding,
* or another response.

The correct behavior must be established by implementation and testing.

---

# 30. Replay Protection

PrismInput must also participate in replay protection.

The system should be able to distinguish:

```text
NEW INPUT
    ≠
REPLAYED INPUT
```

Relevant identity may include:

* chain identity,
* state reference,
* commitments,
* relationship identity,
* and external execution context.

The final mechanism remains a security and implementation question.

---

# 31. Wrong-Chain Protection

A PrismInput associated with Ethereum must not silently become a Bitcoin relationship.

Conceptually:

```text
Ethereum PrismInput
       ↓
Ethereum relationship
```

not:

```text
Ethereum PrismInput
       ↓
arbitrary external chain
```

Chain identity must remain explicit throughout the relationship.

---

# 32. Stale Inputs

An input can become stale.

For example:

```text
External State
      ↓
PrismInput
      ↓
TIME PASSES
      ↓
External State Changes
```

The system must determine whether the original input remains valid.

This is especially important for relationships that take time to reach execution.

---

# 33. Authentication Is Not Consensus

The input boundary must preserve the distinction:

```text
AUTHENTICATION
      ≠
CONSENSUS
```

A prototype that deterministically authenticates an input is not therefore a complete proof that Ethereum's network consensus accepts that state.

This distinction applies to the current Ethereum integration work.

---

# 34. Authentication Is Not Finality

Likewise:

```text
AUTHENTICATION
      ≠
FINALITY
```

Authentication establishes a source or relationship property.

Finality concerns whether the external system considers a state sufficiently irreversible.

These are separate questions.

---

# 35. Commitment Is Not Settlement

Likewise:

```text
COMMITMENT
      ≠
SETTLEMENT
```

A valid input commitment does not mean that an external action has happened.

Settlement only becomes an external fact after the external system executes and the result is observed.

---

# 36. The Complete Evidence Chain

The desired evidence chain is:

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
resultCommitment
      ↓
PrismOutput
      ↓
RAINBOW RING
      ↓
EXTERNAL EXECUTION
      ↓
SETTLEMENT EVIDENCE
```

Each stage answers a different question.

---

# 37. Testing PrismInput

PrismInput should be tested independently before relying on it in a complete Ring relationship.

Important tests include:

### Identity

Does the input identify the correct external chain?

### Commitment

Does changing native state change the native-state commitment?

### Serialization

Does the same input serialize deterministically?

### Validation

Are malformed inputs rejected?

### Authentication

Are invalid authentication relationships rejected?

### Normalization

Does the same valid native state produce the expected normalized representation?

### Traceability

Can the input be connected to the originating native state?

---

# 38. Mutation Testing

Controlled mutations should demonstrate that the boundary actually protects itself.

For example:

```text
CHANGE chainId
      ↓
REJECT
```

```text
CHANGE nativeStateCommitment
      ↓
REJECT
```

```text
CHANGE stateReference
      ↓
REJECT
```

```text
CHANGE authenticationCommitment
      ↓
REJECT
```

```text
CHANGE normalizedState
      ↓
REVALIDATE / REJECT
```

The exact expected behavior should be established by the implementation.

---

# 39. Serialization

The current PrismInput serializer uses a versioned representation.

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
```

Canonical serialization matters because commitments depend on deterministic representation.

Two logically identical inputs should not produce different commitment values merely because they were serialized differently.

---

# 40. Domain Separation

The commitment architecture uses a distinct input domain:

```text
PRISM_INPUT
```

This helps distinguish input commitments from other commitment types.

Conceptually:

```text
PRISM_INPUT
    ≠
PRISM_OUTPUT
```

The domain is part of the cryptographic boundary architecture.

---

# 41. Ethereum PrismInput

The first implementation target uses Ethereum-specific native state.

Conceptually:

```text
Ethereum
   ↓
EthereumNativeState
   ↓
EthereumNativeConduit
   ↓
EthereumPrismInputBuilder
   ↓
PrismInput
```

The current builder is a prototype.

It should not be represented as a complete Ethereum consensus-proof system.

---

# 42. Ethereum State Representation

The current public Ethereum boundary identifies:

```text
EthereumNativeState
├── blockHash
├── parentHash
├── stateRoot
├── transactionsRoot
├── receiptsRoot
└── blockNumber
```

These fields provide a native-state representation for the integration boundary.

They do not themselves define the complete Ethereum proof model.

---

# 43. No Ethereum Color Assignment

PrismInput does not establish which spectral layer should receive Ethereum input.

That remains an implementation question.

The correct rule is:

> **Do not invent the Ethereum color assignment.**

The actual PrismChain integration must determine the correct path through testing.

---

# 44. Input Boundary and Spectral Computation

Once PrismInput is accepted, the external integration boundary ends and PrismChain computation begins.

Conceptually:

```text
PrismInput
     │
     ▼
PRISMCHAIN
     │
     ├── RED
     ├── ORANGE
     ├── YELLOW
     ├── GREEN
     ├── BLUE
     ├── INDIGO
     └── VIOLET
     │
     ▼
WHITE LIGHT BLOCK
```

PrismInput does not dictate the internal implementation of that computation.

---

# 45. PrismInput and the Ring Relationship

PrismInput is therefore the **origin point** of a potential Ring relationship.

The relationship can be represented as:

```text
EXTERNAL STATE
      ↓
PrismInput
      ↓
PRISMCHAIN
      ↓
PrismOutput
      ↓
RAINBOW RING
      ↓
EXTERNAL SYSTEM
```

The Ring is not complete merely because PrismInput exists.

The complete relationship requires a corresponding output and external observation.

---

# 46. No Automatic Settlement

A valid PrismInput does not imply:

* valid output,
* successful execution,
* or settlement.

The stages remain separate:

```text
INPUT
  ↓
COMPUTATION
  ↓
OUTPUT
  ↓
RELATIONSHIP
  ↓
EXECUTION
  ↓
SETTLEMENT
```

This separation is essential to honest evidence.

---

# 47. Failure Handling

Potential input failures include:

```text
UNKNOWN CHAIN
INVALID STATE
INVALID COMMITMENT
INVALID AUTHENTICATION
MALFORMED INPUT
STALE STATE
REORGED STATE
DUPLICATE INPUT
UNSUPPORTED FORMAT
```

Each should remain distinguishable where practical.

A failure at the input boundary should not be disguised as a PrismChain computation failure.

---

# 48. Security Boundary

PrismInput is security-critical because it determines what external information PrismChain is being asked to process.

The central questions are:

> **What entered PrismChain?**

> **Where did it come from?**

> **Which external state does it represent?**

> **Was that state authenticated appropriately?**

> **Has the state changed?**

> **Can the input be replayed?**

The implementation must eventually provide evidence for these answers.

---

# 49. Public and Private Boundary

Public documentation should expose:

* PrismInput structure,
* boundary responsibilities,
* commitment relationships,
* lifecycle,
* security questions,
* testing methodology,
* and demonstrated behavior.

It should not expose:

* proprietary authentication techniques,
* undisclosed mathematical mechanisms,
* private optimizations,
* protected protocol mechanics,
* or unreleased implementation details.

The principle remains:

> **Reveal the architecture. Protect the advantage.**

---

# 50. Current Status

PrismInput is:

**🟢 Architecturally Defined**

The public structure and boundary role are defined.

**🟣 Experimentally Implemented**

The Ethereum integration contains prototype components.

**🔵 Under Testing**

Authentication, state handling, reorganization behavior, replay protection, and complete external evidence remain areas for continued testing.

**🟡 Not Yet Proven**

Production-grade cross-chain input security and finality handling remain unproven.

---

# 51. What Is Established

The architecture establishes:

```text
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
```

It also establishes that:

* PrismInput is an explicit boundary,
* native state remains externally owned,
* Native Conduits preserve native identity,
* commitments provide traceability,
* PrismChain remains responsible for computation,
* and Rainbow Ring remains responsible for the external relationship.

---

# 52. What Is Not Yet Proven

This document does not claim:

* complete Ethereum consensus verification,
* complete Ethereum finality verification,
* production-grade authentication,
* production replay protection,
* production reorganization handling,
* complete multi-chain input support,
* or production Rainbow Ring settlement.

Those claims require implementation and evidence.

---

# 53. The Input Principle

PrismInput exists to make the beginning of the relationship explicit.

```text
NATIVE STATE
      ↓
NATIVE CONDUIT
      ↓
PrismInput
      ↓
PRISMCHAIN
```

The input boundary should answer:

> **What entered PrismChain?**

> **Where did it come from?**

> **Which external state does it represent?**

> **What commitments bind it to that state?**

> **Can the relationship be traced forward to the eventual result?**

---

# 54. Final Architecture

The complete relationship is:

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

PrismInput is the formal doorway into PrismChain.

The Native Conduit preserves native identity.

PrismChain performs the computation.

The White Light Block represents the unified result.

PrismOutput represents that result at the external boundary.

Rainbow Ring establishes the relationship.

The external blockchain remains the authority over its own execution and settlement.

---

# 55. Final Principles

> **Make the input boundary explicit.**

> **Preserve native identity.**

> **Bind PrismInput to its originating state.**

> **Do not confuse authentication with consensus or finality.**

> **Do not confuse commitments with settlement.**

> **Make the computation traceable from input to White Light Block.**

> **Make the output traceable back to its originating input.**

> **Let Rainbow Ring establish the relationship.**

> **Let the external blockchain determine external truth.**

And above all:

> **Connect systems without confusing them.**

> **PrismChain is the seven-layer blockchain.**

> **Prism computes.**
