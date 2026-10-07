# 🧪 Experiment 07 — Reproducibility

**Status:** 🟡 Planned
**Class:** Core PrismChain
**Evidence Level:** Implementation / Experimental

---

## 1. Objective

Demonstrate whether the documented PrismChain experiment behavior can be repeated under defined conditions and produce the same expected computational relationships.

The purpose is not necessarily to require identical hashes across every execution.

Dynamic inputs such as timestamps, generated state, configuration, or other runtime-dependent values may legitimately produce different outputs.

The primary objective is to determine whether the **expected behavior and relationships** can be reproduced.

```text id="h7n4px"
RUN 1
   ↓
OBSERVE

RUN 2
   ↓
OBSERVE

COMPARE
   ↓
REPRODUCIBLE BEHAVIOR?
```

---

# 2. Research Question

> **Can the documented PrismChain computational behavior be reproduced under equivalent execution conditions?**

A secondary question is:

> **When outputs differ between executions, can those differences be explained by documented variable inputs?**

---

# 3. Architectural Claim

A technical system should produce behavior that can be independently repeated under sufficiently defined conditions.

For PrismChain, reproducibility may exist at several levels:

```text id="m8c2vs"
STRUCTURAL
    ↓
BEHAVIORAL
    ↓
RELATIONAL
    ↓
DETERMINISTIC
```

These are not equivalent.

A system may reproduce its behavior while producing different hashes because timestamps or other inputs changed.

The experiment therefore distinguishes between:

* exact output reproducibility;
* structural reproducibility;
* behavioral reproducibility;
* relationship reproducibility.

---

# 4. Scope

### Included

* Repeated execution of a documented PrismChain experiment
* Same implementation version
* Same documented configuration
* Same defined inputs where possible
* Comparison of outputs
* Comparison of relationships
* Identification of variable inputs
* Reproduction of validation behavior

### Not included

This experiment does not attempt to demonstrate:

* Production reliability
* Long-term operational stability
* Network-wide reproducibility
* Consensus
* Decentralization
* Scalability
* Security against all attacks
* Ethereum interoperability
* Native Conduit behavior
* Rainbow Ring settlement

Those require separate evidence.

---

# 5. Reproducibility Levels

The experiment should identify what type of reproducibility is actually possible.

## Level 1 — Structural Reproducibility

The same expected system structure appears again.

For example:

```text id="u5f3ca"
7 LAYERS
   ↓
WLB
```

The same architectural relationships are observed.

---

## Level 2 — Behavioral Reproducibility

The system performs the same class of operation again.

For example:

```text id="8d0x4j"
RUN 1
Seven layers execute
WLB produced

RUN 2
Seven layers execute
WLB produced
```

The exact values may differ.

---

## Level 3 — Relational Reproducibility

The same relationships are reproduced.

For example:

```text id="y9j4wt"
WLB N
HASH A
   ↓
WLB N+1
PREVIOUS HASH = A
```

The actual hashes may differ between runs, but the expected relationship remains intact.

---

## Level 4 — Exact Deterministic Reproduction

The same inputs produce exactly the same outputs.

This level should only be claimed if the implementation actually supports deterministic execution under the defined conditions.

Do not assume deterministic reproduction merely because hashing is deterministic.

---

# 6. Preconditions

Before execution, record:

```text id="3x5r8v"
IMPLEMENTATION:
VERSION / COMMIT:
ENVIRONMENT:
OPERATING SYSTEM:
RUNTIME:
DEPENDENCIES:
CONFIGURATION:
DATE:
```

Also record the experiment being reproduced.

Example:

```text
SOURCE EXPERIMENT:
01 — Seven-Layer Computation
```

or:

```text
SOURCE EXPERIMENT:
04 — White Light Block Formation
```

---

# 7. Control Run

First execute the selected experiment normally.

Record:

```text id="2p8k4w"
Inputs
Configuration
Layer outputs
Hashes
WLB
Validation results
Execution time
Environment
```

This becomes the reference run.

Do not modify the reference results.

---

# 8. Reproduction Run

Repeat the same experiment using:

* the same implementation version;
* the same documented configuration;
* the same defined inputs where possible;
* the same execution procedure;
* the same validation process.

Record all observable outputs again.

The reproduction run should be performed independently of the first run's results.

The operator should not manually copy expected output values into the second run.

---

# 9. Variable Identification

Before comparing results, identify values that may legitimately change.

Potential variables include:

```text id="q6w1se"
Timestamp
Runtime-generated data
Block number
Previous state
Randomness
Environment-dependent values
Configuration
External state
Execution order
```

Every known variable should be documented.

If a value differs and the cause is unknown, record it as an investigation item rather than assuming the difference is harmless.

---

# 10. Comparison

Compare the two executions at multiple levels.

### Structural

Did both executions produce the expected seven-layer structure?

### Behavioral

Did both executions perform the expected computational process?

### Relational

Did the same integrity and chaining relationships occur?

### Output

Were exact outputs identical?

If not:

> **Why were they different?**

---

# 11. Evidence Table

A public evidence record may use:

| Observation           | Run 1      | Run 2      | Match      | Explanation       |
| --------------------- | ---------- | ---------- | ---------- | ----------------- |
| Seven layers executed | Yes        | Yes        | ✅          | Same procedure    |
| WLB produced          | Yes        | Yes        | ✅          | Same operation    |
| Layer structure       | `<actual>` | `<actual>` | ✅          | Same structure    |
| WLB relationship      | `<actual>` | `<actual>` | ✅          | Same relationship |
| Exact hash            | `<actual>` | `<actual>` | `<yes/no>` | `<reason>`        |
| Validation            | `<actual>` | `<actual>` | `<yes/no>` | `<reason>`        |

Only actual execution results should be inserted.

---

# 12. Primary Success Criteria

The experiment succeeds at the claimed reproducibility level when:

1. The experiment can be executed more than once.
2. The documented conditions can be reproduced.
3. The expected computational process occurs again.
4. Expected structural relationships are reproduced.
5. Validation behavior is consistent.
6. Differences between outputs are either explained or explicitly identified as unresolved.
7. The final claim does not exceed the demonstrated level of reproducibility.

---

# 13. Failure Criteria

Record failure or investigation if:

* The experiment cannot be repeated.
* The same documented conditions produce incompatible behavior.
* Expected layers fail to execute consistently.
* WLB formation is inconsistent without an identified cause.
* Validation results differ unexpectedly.
* Output differences cannot be explained.
* The implementation depends on undocumented conditions necessary for successful execution.

A reproducibility failure is valuable evidence.

It may identify a hidden dependency in the system.

---

# 14. Exact Hash Reproduction

Exact hash matching requires special care.

A cryptographic hash is deterministic for a given input.

But if the input changes, the hash will also change.

For example:

```text id="g2m6ka"
INPUT A
   ↓
HASH A

INPUT B
   ↓
HASH B
```

Therefore:

```text id="w3s9fp"
HASH A ≠ HASH B
```

does not automatically mean that the experiment failed.

The experiment must first determine whether the inputs were actually identical.

---

# 15. Deterministic Test

If the implementation supports controlled deterministic inputs, a separate deterministic reproduction may be performed.

For example:

```text id="6x1q8m"
DEFINED INPUTS
DEFINED TIMESTAMP
DEFINED INITIAL STATE
DEFINED CONFIGURATION
        ↓
       RUN
        ↓
EXPECTED OUTPUT
```

The exact same conditions can then be executed again.

If the output matches exactly, record:

> **Exact deterministic reproduction demonstrated under the tested conditions.**

Do not generalize that result to every runtime configuration.

---

# 16. Independent Reproduction

A stronger future experiment may involve a second operator or environment.

Conceptually:

```text id="k9v2bd"
ENVIRONMENT A
     ↓
   RESULT A

ENVIRONMENT B
     ↓
   RESULT B

      ↓
   COMPARE
```

The purpose is to determine whether the behavior depends on a specific machine or environment.

This should only be attempted when the implementation and public documentation provide enough information to reproduce the experiment without exposing proprietary source code.

---

# 17. Public Evidence Package

Potential evidence directory:

```text id="p5r8cz"
evidence/
└── 07-reproducibility/
    ├── run-01-summary.json
    ├── run-02-summary.json
    ├── comparison-results.json
    └── execution-summary.md
```

Public evidence should contain only safe, reproducible information.

Do not publish private implementation details merely to make reproduction possible.

The experiment should demonstrate what can be reproduced publicly without exposing protected implementation.

---

# 18. What This Experiment Demonstrates

If successful, this experiment demonstrates that the tested PrismChain behavior can be repeated under the documented conditions at the demonstrated level.

For example:

> **Seven-layer computation and White Light Block formation were reproduced under the same implementation and documented conditions, with expected differences attributable to changing runtime inputs.**

That is a meaningful technical result.

---

# 19. What This Experiment Does Not Demonstrate

A successful reproducibility experiment does not prove:

* universal deterministic behavior;
* perfect portability;
* production reliability;
* consensus;
* decentralization;
* scalability;
* security;
* mathematical correctness;
* external blockchain interoperability.

The claim must remain tied to the actual conditions tested.

---

# 20. Reproducibility and Public Documentation

The experiment should reveal enough information for an informed technical reader to understand:

```text id="r4h7mz"
WHAT WAS RUN
WHEN IT WAS RUN
WHICH VERSION
UNDER WHAT CONDITIONS
WHAT WAS EXPECTED
WHAT ACTUALLY HAPPENED
WHAT CHANGED
WHY IT CHANGED
```

It does not require publishing the private implementation.

The goal is **reproducible evidence**, not necessarily **public source code**.

---

# 21. Relationship to Previous Experiments

Experiment 07 builds on the previous evidence suite:

```text id="9w2k4f"
01 — Seven-Layer Computation
        ↓
02 — Layer Integrity
        ↓
03 — Chain Integrity
        ↓
04 — WLB Formation
        ↓
05 — Sequential Operation
        ↓
06 — Tamper Detection
        ↓
07 — Reproducibility
```

The first six experiments establish what the system does.

Experiment 07 asks:

> **Can we do it again and obtain the same expected behavior?**

---

# 22. Result Record

Complete only after execution:

```text id="x5v9qa"
EXPERIMENT:
07 — Reproducibility

SOURCE EXPERIMENT:

DATE:

VERSION:

ENVIRONMENT:

RUN 01:

RUN 02:

INPUTS IDENTICAL:

VARIABLE INPUTS:

STRUCTURAL RESULT:

BEHAVIORAL RESULT:

RELATIONAL RESULT:

EXACT OUTPUT MATCH:

DIFFERENCES:

EXPLANATION FOR DIFFERENCES:

EXPECTED RESULT:

ACTUAL RESULT:

EVIDENCE:

LIMITATIONS:

CONCLUSION:

REPRODUCIBILITY LEVEL:

STATUS:
```

Possible statuses:

```text id="n3f6yw"
🟢 Demonstrated
🟣 Experimental
🔴 Failed
🟡 Requires Investigation
⚪ Inconclusive
```

---

# 23. Research Interpretation

Reproducibility is not the demand that every execution produce identical bytes.

It is the discipline of understanding **why outputs are the same or different**.

The experiment therefore asks:

```text id="c7m1xs"
RUN
 ↓
COMPARE
 ↓
IDENTIFY VARIABLES
 ↓
EXPLAIN DIFFERENCES
 ↓
REPEAT
 ↓
DOCUMENT
```

If the results match:

**record the match.**

If the results differ:

**identify why.**

If the reason is unknown:

**record the uncertainty.**

That is stronger scientific evidence than pretending every run should be identical.

---

# 24. Core Principle

> **A result becomes stronger when another execution can reproduce the behavior and explain the differences.**

The standard is:

**Repeat the experiment.**

**Record the conditions.**

**Compare the results.**

**Explain the differences.**

**Do not hide variability.**

---

## Final Statement

Experiment 07 completes the initial core PrismChain evidence sequence.

We have now defined experiments for:

```text id="v1h6rt"
01  Seven-Layer Computation
02  Layer Integrity
03  Chain Integrity
04  White Light Block Formation
05  Sequential Operation
06  Tamper Detection
07  Reproducibility
```

Together, these experiments move the public evidence from:

**“PrismChain is described as a seven-layer blockchain.”**

to:

**“Here is what was executed, here is what happened, and here is the evidence showing the behavior.”**

> **PrismChain is the seven-layer blockchain.**
>
> **Run it. Repeat it. Compare it. Document it.**
>
> **Reveal the architecture. Demonstrate the behavior. Publish the evidence. Protect the implementation.**
