# 🧪 Experiment 03 — Chain Integrity

**Status:** 🟡 Planned
**Class:** Core PrismChain
**Evidence Level:** Implementation / Experimental

---

## 1. Objective

Demonstrate that successive PrismChain blocks maintain the expected cryptographic relationship between one block and the next.

The experiment focuses specifically on the chain relationship:

```text
BLOCK N
   │
   ├── HASH N
   │
   ▼
BLOCK N+1
   │
   ├── PREVIOUS HASH = HASH N
   │
   ▼
BLOCK N+2
   │
   └── PREVIOUS HASH = HASH N+1
```

The objective is to demonstrate that PrismChain does not merely produce isolated blocks, but maintains a sequential relationship between successive blocks.

---

## 2. Research Question

> **When PrismChain produces successive blocks, does each block correctly reference the hash of the immediately preceding block?**

---

## 3. Architectural Claim

PrismChain maintains sequential state through cryptographic hash relationships.

For a valid sequence:

```text
Hash(Block N)
        ↓
PreviousHash(Block N+1)

Hash(Block N+1)
        ↓
PreviousHash(Block N+2)
```

The experiment tests this relationship directly.

The experiment does not assume that a chain is secure merely because hashes exist.

It tests whether the expected relationship is actually present in the running implementation.

---

## 4. Scope

### Included

* Successive PrismChain blocks
* Block numbering
* Block timestamps
* Previous-hash references
* Current block hashes
* Sequential validation
* Detection of unexpected chain breaks

### Not included

This experiment does not attempt to demonstrate:

* Consensus
* Decentralization
* Network security
* Economic security
* Byzantine fault tolerance
* Scalability
* External blockchain finality
* Ethereum integration
* Native Conduits
* Rainbow Ring
* White Light Block formation
* Production readiness

Those questions require separate experiments.

---

# 5. Preconditions

Before execution, record:

```text
IMPLEMENTATION:
VERSION / COMMIT:
ENVIRONMENT:
OPERATING SYSTEM:
RUNTIME:
DEPENDENCIES:
CONFIGURATION:
DATE:
```

The experiment must be executed against the actual PrismChain implementation.

No evidence should be fabricated or manually constructed.

---

# 6. Control Sequence

Generate a sequence containing at least three valid successive blocks.

Three or more blocks are preferred because they demonstrate that the relationship continues beyond a single predecessor/successor pair.

Example:

```text
BLOCK 100
    HASH → A

BLOCK 101
    PREVIOUS HASH → A
    HASH → B

BLOCK 102
    PREVIOUS HASH → B
    HASH → C
```

The actual values must come from the running implementation.

---

# 7. Execution

The experiment should:

1. Start from a known valid PrismChain state.
2. Generate the first test block.
3. Capture its block number and hash.
4. Generate the next block.
5. Capture its block number, previous hash, and hash.
6. Generate another successive block.
7. Capture its block number, previous hash, and hash.
8. Validate each block.
9. Compare every successor's `previous_hash` against the preceding block's `hash`.
10. Record the complete result.

The experiment runner should capture the actual values rather than manually constructing the expected relationship.

---

# 8. Evidence Record

The public evidence should contain enough information to demonstrate the chain relationship without exposing private implementation.

Example structure:

| Block | Previous Hash | Current Hash    | Link Valid |
| ----- | ------------- | --------------- | ---------- |
| N     | —             | `<actual hash>` | ✅          |
| N+1   | `<hash N>`    | `<actual hash>` | ✅          |
| N+2   | `<hash N+1>`  | `<actual hash>` | ✅          |

The actual hashes must be populated only after execution.

---

# 9. Primary Success Criteria

The experiment succeeds if:

1. Multiple successive blocks are generated.
2. Each block validates according to the implementation's validation rules.
3. Block numbering progresses as expected.
4. Each successor contains the expected predecessor hash.
5. The recorded relationship matches the actual generated blocks.
6. No unexpected chain break occurs within the tested sequence.

The central condition is:

```text
previous_hash(Block N+1)
        =
hash(Block N)
```

and:

```text
previous_hash(Block N+2)
        =
hash(Block N+1)
```

for every tested successor.

---

# 10. Failure Criteria

The experiment should be recorded as failed or requiring investigation if:

* A generated block does not validate.
* A successor references the wrong previous hash.
* A previous hash is missing when the implementation requires one.
* Block sequencing is inconsistent.
* A chain relationship cannot be verified.
* The runtime produces contradictory evidence.
* The experiment cannot reproduce the expected relationship.

A failure is not something to hide.

A failure identifies something that needs to be understood.

---

# 11. Optional Chain-Break Observation

If supported by the existing implementation, a controlled chain-break observation may be performed.

For example:

```text
BLOCK N
HASH → A

BLOCK N+1
PREVIOUS HASH → X
```

where:

```text
X ≠ A
```

The purpose is only to observe whether the existing validation mechanism recognizes the broken relationship.

This should **not** replace Experiment 06, which is dedicated to broader tamper-detection testing.

The experiment must not assume that a particular failure mechanism exists before it has been observed in the implementation.

---

# 12. Evidence to Preserve

Preserve the public-safe portions of:

```text
Block numbers
Timestamps
Previous hashes
Current hashes
Validation results
Execution summary
Environment information
Version / commit identifier
```

Potential evidence package:

```text
evidence/
└── 03-chain-integrity/
    ├── chain-results.json
    ├── validation-results.txt
    └── execution-summary.md
```

Only create these artifacts from actual execution.

---

# 13. Public Evidence Example

A completed public record might eventually resemble:

```text
Experiment:
03 — Chain Integrity

Blocks Tested:
3

Block Sequence:
N → N+1 → N+2

Block N:
Hash: <actual value>

Block N+1:
Previous Hash: <actual value>
Hash: <actual value>
Link: VALID

Block N+2:
Previous Hash: <actual value>
Hash: <actual value>
Link: VALID

Overall Result:
PASS
```

This is an example of the **format**, not experimental evidence.

No actual result should be inserted until the experiment has been executed.

---

# 14. What This Experiment Demonstrates

If successful, this experiment demonstrates that the tested PrismChain implementation maintains the expected sequential hash relationship across the tested blocks.

That is observable evidence of chain integrity within the tested scope.

---

# 15. What This Experiment Does Not Demonstrate

A successful chain-integrity experiment does **not** prove:

* that PrismChain is immune to attack;
* that the chain cannot be rewritten;
* that consensus is secure;
* that the network is decentralized;
* that historical state is permanently immutable;
* that the system is production-ready;
* that the chain scales under real-world load.

Those claims require additional evidence.

---

# 16. Reproducibility

A future execution should use the same documented procedure while recording its own:

```text
Implementation version
Environment
Configuration
Execution date
Block sequence
Observed hashes
Validation results
```

If repeated executions produce different hashes because of dynamic inputs such as timestamps or generated data, that difference must be documented rather than treated automatically as a failure.

The reproducibility question is whether the **expected chain relationship** remains reproducible under equivalent conditions.

---

# 17. Result Record

Complete only after execution:

```text
EXPERIMENT:
03 — Chain Integrity

DATE:

VERSION:

ENVIRONMENT:

BLOCKS TESTED:

EXPECTED RESULT:

ACTUAL RESULT:

CHAIN LINKS VERIFIED:

VALIDATION RESULT:

EVIDENCE:

LIMITATIONS:

CONCLUSION:

STATUS:
```

Possible statuses:

```text
🟢 Demonstrated
🟣 Experimental
🔴 Failed
🟡 Requires Investigation
⚪ Inconclusive
```

---

# 18. Research Interpretation

The purpose of this experiment is deliberately narrow.

It asks whether the running implementation maintains the chain relationship it is expected to maintain.

If the relationship works:

**record the evidence.**

If the relationship fails:

**investigate the implementation.**

If the implementation behaves differently than the architecture describes:

**update the understanding before updating the claim.**

The experiment exists to discover what the system actually does.

---

# 19. Public Demonstration

The conceptual public demonstration is:

```text
          PRISmCHAIN

       BLOCK N
       HASH A
          │
          │
          ▼
       BLOCK N+1
    PREVIOUS HASH A
       HASH B
          │
          │
          ▼
       BLOCK N+2
    PREVIOUS HASH B
       HASH C
```

The important evidence is not the diagram.

The important evidence is the **actual relationship observed in the running system**.

---

# 20. Core Principle

> **A blockchain is not demonstrated by saying that blocks are linked. The relationship must be observable in the blocks themselves.**

This experiment provides that observation at the chain-link level.

```text
GENERATE
   ↓
CAPTURE
   ↓
COMPARE
   ↓
VALIDATE
   ↓
DOCUMENT
```

**Let the implementation produce the evidence.**

---

## Final Statement

Experiment 03 establishes the next layer of public evidence for PrismChain:

**Individual state has integrity.**

**Successive state has relationships.**

The next experiment will examine how those successive operations converge into the **White Light Block**.

> **PrismChain is the seven-layer blockchain.**
>
> **Build the chain. Test the relationship. Publish the evidence.**
>
> **Reveal the architecture. Protect the advantage.**
