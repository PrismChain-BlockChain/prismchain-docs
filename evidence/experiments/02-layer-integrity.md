# 🧪 Experiment 02 — Layer Integrity

> **Demonstrate that an individual PrismChain layer can detect alteration of its recorded state.**

**Status:** 🟡 Planned

**Experiment Class:** Core PrismChain

**Evidence Level:** Implementation / Experimental

---

# 1. Objective

Demonstrate that a PrismChain layer's recorded state is cryptographically linked to its stored hash and that modifying the layer data causes the expected integrity relationship to fail.

The experiment establishes the basic integrity property on which the higher-level chain relationships depend.

---

# 2. Research Question

> **If a valid PrismChain layer block is altered after creation, does the integrity mechanism detect the alteration?**

---

# 3. Architectural Claim Being Tested

The current public PrismChain implementation represents layer blocks with information including:

```text
block_number
timestamp
data
previous_hash
hash
```

The layer's hash provides an integrity relationship between the recorded block contents and its cryptographic identity.

The experiment tests that relationship directly.

---

# 4. Scope

This experiment tests **individual layer integrity**.

It does not test:

* the complete seven-layer computation;
* White Light Block formation;
* multi-block chain integrity;
* external blockchain integration;
* Ethereum;
* Rainbow Ring;
* consensus;
* network security;
* or production security.

Those belong to other experiments.

---

# 5. Preconditions

Record before execution:

```text
Implementation:
Version / Commit:
Environment:
Operating System:
Runtime:
Configuration:
Experiment Date:
Layer Tested:
```

The experiment should use an actual generated layer block from the PrismChain implementation.

---

# 6. Control State

First generate a valid layer block without modification.

Preserve the original state.

Example structure:

```text id="j4r7qz"
BLOCK NUMBER:
TIMESTAMP:
DATA:
PREVIOUS HASH:
HASH:
```

This is the **control state**.

The control must first be shown to pass the applicable integrity validation.

---

# 7. Control Validation

Before tampering with the block, verify that the original block is valid.

Record:

```text id="3z4x8n"
Original Block:
VALIDATION:
EXPECTED:
ACTUAL:
```

### Expected

The original, untouched block passes validation.

If the control does not pass validation, the tamper experiment should not proceed until the cause is understood.

---

# 8. Tampering Method

After establishing a valid control state, create a controlled copy.

Change exactly one relevant field.

Possible fields include:

* `data`;
* `block_number`;
* `timestamp`;
* `previous_hash`;
* or another field covered by the implementation's integrity calculation.

For the first run, changing the **data field** is preferred because it provides the clearest demonstration.

The original evidence must remain untouched.

---

# 9. Example Tampering Model

```text id="u6z2qk"
ORIGINAL

DATA
  ↓
HASH
  ↓
VALID


TAMPERED

DATA'
  ↓
ORIGINAL HASH
  ↓
VALIDATION
  ↓
FAILURE
```

The experiment should preserve both states.

---

# 10. Expected Result

The modified block should no longer match the cryptographic identity represented by its original hash.

Therefore, validation should detect the alteration.

The important relationship is:

```text id="9h8r2m"
ORIGINAL DATA
      ↓
ORIGINAL HASH
      ✓


MODIFIED DATA
      ↓
ORIGINAL HASH
      ✕
```

---

# 11. Evidence To Capture

Preserve:

```text id="f8x4z1"
Original Block
Original Hash
Modified Block
Modified Field
Validation Result
Relevant Error / Rejection
Execution Timestamp
Environment
```

Where appropriate, produce a before/after comparison.

---

# 12. Evidence Table

The final public record should contain a table similar to:

| State    | Data     | Stored Hash | Validation |
| -------- | -------- | ----------- | ---------- |
| Original | Original | Original    | —          |
| Tampered | Modified | Original    | —          |

Populate the final values from the actual experiment.

Do not fabricate results.

---

# 13. Success Criteria

The experiment succeeds if:

1. A valid layer block can be generated.
2. The original block passes the applicable integrity check.
3. One controlled field is modified.
4. The original cryptographic identity is retained.
5. Validation detects the mismatch.
6. The failure is observable and recordable.

---

# 14. Failure Criteria

The experiment requires investigation if:

* the original block does not validate;
* modifying a covered field does not affect validation;
* the modified block is incorrectly accepted;
* validation produces an unexpected result;
* or the experiment cannot reliably distinguish the original and modified states.

A failure should be documented.

It should not be silently corrected before the result is recorded.

---

# 15. What This Demonstrates

A successful result demonstrates that, within the tested implementation and conditions:

> **The integrity mechanism can detect alteration of the tested layer block.**

This establishes an important observable property of the layer representation.

---

# 16. What This Does Not Demonstrate

This experiment does **not** establish:

* complete blockchain security;
* resistance to every form of attack;
* consensus security;
* cryptographic security under every threat model;
* network security;
* immutability in the absolute sense;
* or production readiness.

The experiment demonstrates one specific integrity property.

---

# 17. Why This Matters

The seven-layer architecture depends on trustworthy layer outputs.

If a layer's recorded state could be silently changed without detection, later relationships built from that state could become unreliable.

The integrity experiment therefore establishes a foundational property before testing:

```text id="w0x8fj"
LAYER
  ↓
INTEGRITY
  ↓
CHAIN
  ↓
WHITE LIGHT BLOCK
```

The experiment should be understood as one piece of the larger evidence chain.

---

# 18. Public Demonstration

The public-facing demonstration should be simple.

Show:

```text id="v3j7pk"
VALID BLOCK
     ↓
HASH = ABC123...
     ↓
VALID


CHANGE DATA
     ↓
HASH REMAINS ABC123...
     ↓
VALIDATION
     ↓
REJECTED
```

The actual hashes and validation output should come from the experiment.

No source code needs to be published.

---

# 19. Reproducibility

Where practical, document:

* the original block structure;
* the field modified;
* the experiment conditions;
* the validation procedure;
* the expected behavior;
* and the resulting evidence.

A qualified observer should be able to understand exactly what was tested.

The proprietary implementation remains private.

---

# 20. Result Record

Complete this section only after execution.

```text id="8n5v2k"
## Result

**Status:**

**Execution Date:**

**Implementation Version / Commit:**

**Environment:**

**Layer Tested:**

### Control Result

[Record the result of validating the original block.]

### Tamper Operation

[Record exactly what was changed.]

### Actual Result

[Record what the implementation actually did.]

### Evidence

[List the public evidence artifacts.]

### Conclusion

[State exactly what the experiment demonstrates.]

### Limitations

[Record what remains untested.]

### Next Step

[Identify the next experiment or investigation.]
```

---

# 21. Research Interpretation

The experiment should be interpreted narrowly.

A successful result supports the statement:

> **The tested PrismChain layer detects modification of the tested integrity-protected state.**

It should not be expanded into:

> “PrismChain is completely secure.”

The evidence must remain proportional to the experiment.

---

# 22. Final Principle

The point of the experiment is simple:

> **Create a valid state.**

> **Change the state.**

> **Test the identity.**

> **Observe the result.**

If the alteration is detected, we have demonstrated an actual integrity property of PrismChain.

If it is not detected, we have discovered something important that requires investigation.

Either result is useful.

> **Test assumptions.**

> **Show the result.**

> **Preserve the evidence.**

> **Let the implementation tell us what is actually true.**
