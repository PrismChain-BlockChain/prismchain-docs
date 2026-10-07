# 06 — Known-Solution Recovery

**Experiment ID:** `LC-06`
**Status:** 🟣 Experimental
**Type:** Independent Mathematical Evaluation
**Program:** Spectral Discovery Program
**Depends On:** LC-01, LC-02, LC-03, LC-04, LC-05

---

# 1. Purpose

This experiment evaluates whether the Spectral Inversion system can recover known mathematical solutions **without being given those solutions during the inversion process**.

LC-05 established and characterized the inversion mechanism.

LC-06 asks a different question:

> **Can the system recover mathematically valid answers when the correct answers are hidden from it?**

The distinction is critical.

A system that can generate a candidate after being shown the answer has demonstrated candidate construction.

A system that receives only a problem and independently generates a candidate that is later verified against hidden ground truth has demonstrated **blind recovery**.

This experiment therefore serves as the first independent evaluation of the proposed spectral discovery process.

---

# 2. Core Hypothesis

The hypothesis is:

> **A mathematical problem represented in spectral coordinates may contain sufficient structural information for spectral inversion to generate candidates that correspond to valid mathematical solutions, even when the known solution is withheld from the inversion process.**

This hypothesis is experimental.

The experiment does **not** assume that spectral coordinates contain complete mathematical information.

It does **not** assume that inversion must always produce a solution.

It does **not** assume that a generated candidate is correct.

Every candidate must be independently evaluated against mathematical ground truth.

---

# 3. What This Experiment Is Testing

LC-06 tests whether the system can:

1. receive a mathematical target without its answer,
2. construct the appropriate spectral representation,
3. perform inversion,
4. generate one or more candidate solutions,
5. rank or classify candidates,
6. satisfy supplied constraints,
7. survive equivalent representations of the same problem,
8. recover multiple valid solutions where they exist,
9. handle periodic or bounded solution spaces,
10. avoid falsely declaring invalid candidates correct,
11. reproduce its results,
12. generalize to problems not used during development.

The central measurement is:

> **Did the system recover a valid solution that was hidden from it?**

---

# 4. Experimental Principle

The experiment must maintain strict separation between:

```text
PROBLEM
   ↓
SPECTRAL REPRESENTATION
   ↓
INVERSION
   ↓
CANDIDATE GENERATION
   ↓
CANDIDATE VERIFICATION
   ↓
HIDDEN GROUND TRUTH
```

The inversion system must never receive:

* the known solution,
* a solution-dependent spectral coordinate,
* a ranking derived from the hidden solution,
* test-set-specific tuning,
* manually selected parameters based on test results.

The evaluator may use the hidden solution **after** candidate generation.

---

# 5. Blind-Test Architecture

The experiment is divided into two datasets.

## Development Set

The development set may be used to:

* tune parameters,
* test implementation,
* discover bugs,
* select representations,
* determine tolerances,
* compare inversion strategies.

Its solutions are known to the developers.

However, development results must never be mixed with final evaluation results.

---

## Blind Test Set

The blind test set is frozen before the final evaluation.

The inversion system receives:

```text
TARGET
DOMAIN
CONSTRAINTS
TOLERANCE
REPRESENTATION
```

It does not receive:

```text
KNOWN SOLUTION
SOLUTION RANKING
GROUND-TRUTH LABEL
```

The correct answers remain hidden until candidate generation is complete.

---

# 6. Ground-Truth Commitment

Because this is intended to become public scientific evidence, the hidden answers should not simply remain privately editable.

Before the blind run:

1. construct the complete ground-truth dataset,
2. calculate a cryptographic hash of the ground-truth file,
3. publish or record the hash,
4. freeze the test set,
5. run the inversion system,
6. preserve the outputs,
7. reveal the ground truth,
8. independently evaluate the candidates.

Conceptually:

```text
HIDDEN GROUND TRUTH
        ↓
   HASH / COMMITMENT
        ↓
   TEST SET FROZEN
        ↓
   BLIND INVERSION
        ↓
   CANDIDATES FROZEN
        ↓
GROUND TRUTH REVEALED
        ↓
   VERIFICATION
```

This prevents the evaluation answers from being silently changed after seeing the results.

The commitment proves that the ground-truth dataset existed in a particular form before evaluation.

It does not itself prove that the mathematics is correct.

---

# 7. Test Problem Families

The test suite should contain several classes of mathematical problems.

## 7.1 Simple Scalar Problems

Examples:

```text
x + 7 = 12
3x = 21
x / 4 = 6
x² = 49
```

Purpose:

* establish basic recovery,
* expose implementation failures,
* establish a minimum baseline.

These problems should not be considered impressive discoveries.

They establish whether the machinery works at all.

---

# 8. Polynomial Problems

Examples:

```text
x² - 5x + 6 = 0
```

with:

```text
x = 2
x = 3
```

Additional polynomial families should include:

* unique roots,
* multiple roots,
* repeated roots,
* higher-degree equations,
* systems with known solutions.

The evaluation must distinguish:

```text
one valid solution recovered
```

from:

```text
all valid solutions recovered
```

---

# 9. Multiple-Solution Problems

Some mathematical problems have more than one valid answer.

The system must not be evaluated as though only one answer exists.

For a problem with solution set:

```text
S = {s₁, s₂, s₃}
```

the evaluator should determine:

```text
Recovered ∩ S
```

and measure how much of the valid solution set was recovered.

This produces a more meaningful evaluation than simply asking whether the top-ranked candidate matches one predetermined answer.

---

# 10. Constrained Problems

The same mathematical target should be evaluated under different constraints.

Examples:

```text
x² = 16
```

with:

```text
x ∈ ℝ
```

and:

```text
x > 0
```

The first admits:

```text
x = -4, 4
```

while the second admits:

```text
x = 4
```

The system must demonstrate that constraints actually influence candidate generation or candidate selection.

A candidate violating an explicit constraint cannot be counted as a valid recovery.

---

# 11. Periodic Problems

Trigonometric problems introduce an important test of whether the system understands solution structure rather than merely isolated numerical answers.

Examples:

```text
sin(x) = 0
```

or:

```text
cos(x) = 1
```

The evaluation must define a domain before judging recovery.

For example:

```text
0 ≤ x < 2π
```

or another explicitly declared interval.

The experiment must never claim complete recovery of an infinite periodic solution family unless the representation and evaluation method actually support that claim.

---

# 12. Identity Problems

Known mathematical identities should also be tested.

Examples include:

```text
sin²(x) + cos²(x) = 1
```

and equivalent algebraic identities.

These tests are useful because the expected result may not be a single numerical solution.

Instead, the system may need to recognize:

```text
identity
```

as a structural property.

The evaluator must therefore distinguish:

* solution recovery,
* identity recognition,
* structural equivalence.

They are different tasks.

---

# 13. Linear Algebra Problems

The test set should include small linear systems with independently verified solutions.

Example:

```text
Ax = b
```

where:

```text
A
b
```

are supplied to the inversion system but the solution vector is hidden.

The evaluator can later determine:

```text
A x_candidate ≈ b
```

and compare the candidate with the known solution.

This tests whether spectral inversion can operate beyond isolated scalar equations.

---

# 14. Negative Controls

A credible discovery system must be capable of failing.

Therefore the dataset should contain problems where:

* no solution exists,
* supplied constraints are inconsistent,
* candidate generation should fail,
* numerical tolerance should not turn an invalid result into a valid one.

Examples:

```text
x² + 1 = 0
```

under:

```text
x ∈ ℝ
```

or inconsistent systems such as:

```text
x = 1
x = 2
```

The correct behavior is not:

> “Find something close.”

The correct behavior is:

> **Recognize that no valid solution exists within the defined domain and constraints.**

False-positive rate is therefore a primary metric.

---

# 15. Representation-Variant Tests

The same mathematical problem should sometimes be presented in equivalent forms.

For example, mathematically equivalent expressions may differ syntactically.

The system should be tested against:

```text
original representation
equivalent representation
rearranged representation
renamed-variable representation
scaled representation
```

The purpose is to determine whether recovery depends excessively on superficial notation.

The experiment should measure whether mathematically equivalent problems produce:

* equivalent spectral structures,
* related spectral structures,
* materially different structures,
* different recovery behavior.

Any observed difference must be documented rather than hidden.

---

# 16. Training / Development / Blind Separation

The test suite must maintain three conceptual states.

### Development

Used during construction.

```text
KNOWN
TUNABLE
REPEATABLE
```

### Validation

Used to check implementation choices before final freeze.

```text
KNOWN
LIMITED TUNING
SEPARATE FROM FINAL TEST
```

### Blind Test

Used for final evaluation.

```text
HIDDEN
FROZEN
NO TUNING
```

A test result that influenced the design of the algorithm cannot later be presented as an untouched blind result.

---

# 17. Blind Evaluation Protocol

The final evaluation should follow this sequence.

### Step 1 — Freeze the dataset

Freeze:

* target problems,
* domains,
* constraints,
* tolerances,
* representation forms.

### Step 2 — Generate ground truth

Independently establish:

* valid solutions,
* solution multiplicity,
* constraints,
* expected classifications.

### Step 3 — Commit the ground truth

Generate and record its cryptographic hash.

### Step 4 — Freeze the inversion configuration

Record:

* software version,
* configuration,
* parameters,
* random seed if applicable,
* spectral mapping version,
* inversion version.

### Step 5 — Run blind inversion

Provide only:

```text
problem
domain
constraints
tolerance
```

### Step 6 — Freeze candidates

No candidate may be manually removed or modified after seeing the ground truth.

### Step 7 — Reveal ground truth

Make the committed ground-truth dataset available.

### Step 8 — Verify candidates

Use an independent evaluation procedure.

### Step 9 — Calculate metrics

Do not manually interpret individual successes as overall performance.

### Step 10 — Publish failures

Failed cases remain part of the evidence.

---

# 18. Candidate Record

Every generated candidate should contain enough information for independent evaluation.

A conceptual record:

```text
candidate_id
target_id
spectral_coordinates
reconstructed_expression
candidate_value
residual
constraints_checked
constraints_satisfied
generation_method
ranking_score
verification_status
```

The system should never write:

```text
"correct": true
```

during inversion.

Correctness belongs to the evaluation stage.

Instead:

```text
verification_status:
    UNVERIFIED
```

After independent evaluation, it may become:

```text
VALID_EXACT
VALID_APPROXIMATE
INVALID
DUPLICATE
OUT_OF_DOMAIN
CONSTRAINT_VIOLATION
UNRESOLVED
```

---

# 19. Primary Metrics

The experiment should report at least the following.

## Exact Recovery Rate

Percentage of test problems for which an exact valid solution is recovered.

```text
exactly recovered / evaluable test problems
```

---

## Valid-Solution Recovery Rate

Percentage for which at least one mathematically valid candidate is recovered.

This is broader than exact symbolic recovery.

---

## Top-K Recovery

Measure whether a valid solution appears among:

```text
top 1
top 3
top 5
top 10
```

candidate rankings.

This determines whether the system can place useful candidates near the top of its search space.

---

## Multiple-Solution Recall

For problems with known solution sets:

```text
valid solutions recovered
-------------------------
valid solutions available
```

where meaningful and computationally evaluable.

---

## False-Positive Rate

Measure how often the system produces candidates that it would incorrectly classify as valid.

This is especially important for:

* negative controls,
* approximate solutions,
* constrained problems,
* periodic problems.

---

## Constraint Compliance

Measure the percentage of candidates that satisfy all declared constraints.

A mathematically correct candidate outside the allowed domain is not a successful recovery for that test.

---

## Representation Robustness

Measure whether equivalent mathematical representations produce materially different recovery performance.

---

## Reproducibility

Repeated runs with identical inputs and configuration should produce identical or statistically characterized results.

If randomness is intentionally used, the randomization must be recorded and analyzed rather than ignored.

---

# 20. Baseline Comparison

Where conventional mathematical solvers exist, they should be included as comparison baselines.

The purpose is **not** to require spectral inversion to outperform conventional mathematics.

The baseline answers questions such as:

> Does the spectral representation recover information that conventional methods also recover?

and:

> Where does spectral inversion behave differently?

and potentially:

> Does spectral structure provide additional useful information beyond the baseline?

The comparison must be fair.

Do not compare:

```text
highly optimized conventional solver
```

against:

```text
unfinished experimental prototype
```

and call the result meaningful.

Likewise, do not suppress a conventional solver's success because the spectral system is the subject of the experiment.

---

# 21. Independent Verification

A successful spectral candidate must be checked independently.

For example:

```text
SPECTRAL INVERSION
        ↓
CANDIDATE
        ↓
INDEPENDENT MATHEMATICAL CHECK
        ↓
VALID / INVALID
```

For numerical problems, this may involve:

* substitution,
* residual calculation,
* numerical precision checks,
* constraint evaluation.

For symbolic problems, this may involve:

* symbolic simplification,
* substitution,
* algebraic verification,
* independent solver comparison.

The verification mechanism must not simply repeat the same internal reasoning used to generate the candidate.

---

# 22. Discovery vs Recovery

This experiment must carefully distinguish:

### Recovery

The answer is already known independently and the system successfully finds it.

### Discovery

The answer was not known beforehand and the system generates a candidate that survives independent mathematical verification.

LC-06 is primarily a **recovery experiment**.

That is intentional.

A system should demonstrate reliable behavior on known mathematics before claims about unknown mathematics are made.

---

# 23. Expected Failure Modes

The experiment should actively search for:

### Test leakage

The inversion system indirectly receives information derived from hidden solutions.

### Overfitting

The system performs well on development examples but fails on unseen mathematical forms.

### Representation dependence

Equivalent equations produce dramatically different results for superficial reasons.

### False positives

The system generates candidates that appear plausible but fail mathematical verification.

### Constraint violations

Candidates satisfy the equation but violate the declared domain or conditions.

### Incomplete solution recovery

The system finds one solution but misses others.

### Numerical illusion

A candidate appears correct because of an overly generous tolerance.

### Seed dependence

Results change substantially under small changes in random initialization.

### Parameter sensitivity

Small configuration changes produce large changes in recovery performance.

### Circular verification

The same mechanism that generated a candidate is used to declare that candidate correct.

### Ground-truth contamination

The hidden answer influences tuning before the blind run.

Every discovered failure should be recorded.

---

# 24. Success Levels

LC-06 uses a five-level evaluation scale.

### Level 0 — Blind Execution

The system can execute against a hidden test set without receiving the answers.

### Level 1 — Reproducible Candidate Generation

The system consistently produces candidates under equivalent conditions.

### Level 2 — Known-Solution Recovery

The system recovers mathematically valid known solutions on unseen test cases.

### Level 3 — Multiple / Constrained Recovery

The system can recover multiple valid solutions and respect explicit mathematical constraints.

### Level 4 — Robust Blind Generalization

Recovery remains meaningful across unseen representations, problem families, and controlled perturbations.

### Level 5 — Independently Verified Predictive Utility

The system demonstrates a reproducible advantage or useful capability that is not explained by test leakage, conventional solver duplication, or implementation artifacts.

Level 5 is intentionally difficult.

The experiment should not be considered unsuccessful simply because Level 5 is not reached.

---

# 25. Evidence Package

The public evidence package should contain:

```text
06-known-solution-recovery/
├── experiment-definition.md
├── README.md
│
├── inputs/
│   ├── training-targets.json
│   ├── blind-test-targets.json
│   ├── multiple-solution-targets.json
│   ├── constrained-targets.json
│   ├── periodic-targets.json
│   ├── negative-controls.json
│   └── representation-variants.json
│
├── hidden-ground-truth/
│   ├── ground-truth.hash
│   └── solutions.json
│
├── outputs/
│   ├── candidate-solutions.json
│   ├── recovery-results.json
│   ├── verification-results.json
│   └── metrics.json
│
├── analysis/
│   ├── exact-recovery.md
│   ├── multiple-solution-recovery.md
│   ├── constraint-recovery.md
│   ├── representation-invariance.md
│   ├── false-positives.md
│   ├── baseline-comparison.md
│   └── final-analysis.md
│
└── final-report.md
```

During the blind phase, the actual ground-truth solution file should remain private.

After evaluation, it may be released together with the commitment and verification record.

---

# 26. Reproducibility Record

The final report should record:

```text
EXPERIMENT ID:
DATE:
CODE VERSION:
SPECTRAL MAPPER VERSION:
INVERSION ENGINE VERSION:
DATASET VERSION:
GROUND-TRUTH HASH:
CONFIGURATION:
RANDOM SEED:
TOLERANCE:
HARDWARE:
SOFTWARE ENVIRONMENT:
```

Anyone attempting reproduction should be able to determine exactly which configuration produced the published result.

---

# 27. Evidence Interpretation

Results must be categorized carefully.

### Demonstrated

A known mathematical solution was independently recovered and verified.

### Supported

Repeated recovery across a meaningful set of unseen cases suggests a reproducible relationship.

### Interesting

A spectral pattern appears repeatedly but its mathematical meaning remains unclear.

### Hypothesis

A possible explanation is proposed for an observed pattern.

### Failed

The system does not recover the expected result or produces unacceptable false positives.

### Unresolved

The experiment does not provide enough evidence to determine the result.

No category should be silently upgraded.

---

# 28. What Would Count as Interesting

The most interesting outcome is not necessarily the highest raw recovery percentage.

Potentially important observations include:

* equivalent mathematical objects consistently occupy related spectral regions,
* multiple valid solutions form recognizable spectral families,
* constraints produce predictable changes in candidate structure,
* previously unrelated representations converge spectrally,
* spectral distance predicts recovery difficulty,
* inversion identifies candidate structures conventional methods do not prioritize,
* spectral neighborhoods correspond to mathematical solution families,
* certain invariants survive transformations,
* the system generalizes to mathematical forms not represented during development.

These observations would generate hypotheses for later experiments.

They are not automatically mathematical discoveries.

---

# 29. Relationship to LC-07

LC-06 establishes whether the inversion mechanism can recover hidden known answers.

If successful, LC-07 can investigate whether repeated recovery reveals **spectral invariants** associated with mathematical structures.

The progression is therefore:

```text
LC-01
BUILD THE REPRESENTATION
       ↓
LC-02
MAP MATHEMATICS
       ↓
LC-03
MEASURE RESONANCE
       ↓
LC-04
BUILD NETWORKS
       ↓
LC-05
INVERT THE REPRESENTATION
       ↓
LC-06
TEST BLIND RECOVERY
       ↓
LC-07
SEARCH FOR INVARIANTS
```

Each experiment should answer a more difficult question than the previous one.

---

# 30. Transition Criteria

LC-06 should be considered complete only when:

* the blind dataset is frozen,
* the ground truth was committed before evaluation,
* the inversion configuration is recorded,
* the blind run is preserved,
* candidates are frozen before ground-truth disclosure,
* independent verification is complete,
* exact recovery is measured,
* valid-solution recovery is measured,
* multiple-solution recovery is measured where applicable,
* constraint compliance is measured,
* false positives are measured,
* representation robustness is analyzed,
* baseline comparison is documented,
* reproducibility is tested,
* failures are documented,
* limitations are published.

Only then should the program advance to LC-07.

---

# 31. Scientific Boundary

This experiment does **not** establish that the proposed Light Calculator is a universal mathematical computer.

It does **not** establish a new law of mathematics.

It does **not** establish that spectral coordinates are mathematically fundamental.

It does **not** establish that spectral inversion can solve arbitrary mathematical problems.

It does **not** establish a solution to an unsolved problem.

It establishes something narrower and more testable:

> **Whether a proposed spectral representation can support blind recovery of independently known mathematical solutions.**

That is the evidence required before moving from representation and inversion toward genuine mathematical discovery.

---

# 32. Final Principle

> **Do not give the system the answer and call it discovery. Hide the answer, freeze the problem, run the inversion, reveal the ground truth, and let independent mathematics decide whether the candidate was correct.**

**LC-06 is where spectral inversion stops being merely an interesting mechanism and begins facing an actual blind test.**

Build it.

Freeze it.

Hide the answers.

Run it.

Verify it.

Publish the failures.

Then see what the spectrum reveals.
