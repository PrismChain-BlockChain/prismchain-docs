# 05 — Spectral Inversion

**Experiment ID:** `LC-05`
**Status:** 🟣 Experimental
**Type:** Inverse Mathematics / Candidate Discovery

---

# 1. Purpose

Experiment 05 tests whether the proposed Light Calculator can operate in the reverse direction.

The first experiments followed:

```text
MATHEMATICAL OBJECT
        ↓
SPECTRAL REPRESENTATION
        ↓
RESONANCE
        ↓
NETWORK
```

LC-05 reverses that direction:

```text
TARGET MATHEMATICAL OUTCOME
        ↓
SPECTRAL INVERSION
        ↓
CANDIDATE SPECTRAL STRUCTURES
        ↓
CANDIDATE MATHEMATICAL OBJECTS
        ↓
VERIFICATION
```

The purpose is to determine whether starting from a desired result can produce useful candidate mathematical structures that can then be independently tested.

This is the first experiment in which the system is explicitly used as a **search mechanism** rather than only a representation or analysis mechanism.

---

# 2. Research Question

Given a target mathematical outcome:

$$
T
$$

can the spectral inversion engine produce one or more candidate spectral representations:

$$
S_1,S_2,\ldots,S_n
$$

such that mapping or reconstructing those candidates produces mathematical objects capable of satisfying the target?

Conceptually:

$$
T \rightarrow S^{-1}(T)
$$

The critical question is:

> **Does inversion produce useful candidate structures, or does it merely generate arbitrary points in spectral space?**

---

# 3. Primary Hypothesis

> A target mathematical condition may constrain spectral space sufficiently to produce candidate spectral structures that can be tested against the original mathematical problem.

This is a hypothesis.

The experiment does not assume that every mathematical target has:

* a unique spectral representation
* a valid inverse
* a closed-form inverse
* a physically meaningful inverse
* a mathematically useful inverse

Multiple solutions may exist.

No solution may exist.

The inversion process must be capable of returning:

```text
NO CANDIDATE
```

without treating that result as failure of the mathematics itself.

---

# 4. What Inversion Means Here

Inversion does not mean:

> “The computer magically solves the equation.”

Instead, inversion means:

> **Given a desired mathematical condition, search the spectral representation space for candidate structures that satisfy or approximate that condition.**

The distinction is critical.

The system generates candidates.

Conventional mathematics determines whether those candidates actually satisfy the target.

---

# 5. Forward vs Inverse

The forward process is:

$$
M \rightarrow S(M)
$$

The inverse process is:

$$
T \rightarrow S^{-1}(T)
$$

The two processes should eventually be tested against each other.

For a known mathematical object \(M\):

```text
M
↓
FORWARD MAPPING
↓
S(M)
↓
INVERSION
↓
CANDIDATE
↓
COMPARE WITH M
```

This provides a controlled environment before attempting difficult mathematical problems.

---

# 6. Existing Instrument

LC-05 should use the existing:

**`spectral_inversion_engine.py`**

from the Spectral Math Suite.

The experiment should not create a separate inversion engine unless the existing implementation is demonstrated to be insufficient.

The existing tool accepts:

* target output / solution vector
* constraints
* spectral search parameters

and produces candidate spectral coordinates.

The exact implementation behavior must be measured during the experiment rather than assumed from its name.

---

# 7. Inversion Dataset

LC-05 should begin with targets whose correct mathematical solutions are already known.

This is essential.

The experiment must first answer:

> **Can the inversion system recover known solutions?**

before asking whether it can discover unknown ones.

The dataset should progress from simple to difficult.

---

# 8. Dataset Level 1 — Simple Scalar Targets

Examples:

$$
x=5
$$

$$
x^2=25
$$

$$
x+3=10
$$

$$
2x=14
$$

The correct solutions are independently known.

These establish the basic inversion behavior.

---

# 9. Dataset Level 2 — Multiple Solutions

Use equations with more than one solution.

Example:

$$
x^2=4
$$

with:

$$
x=2
$$

and:

$$
x=-2
$$

The inversion system must not be evaluated as successful merely because it finds one candidate if the target mathematically contains multiple valid solutions.

Record:

* number of candidates
* valid candidates
* invalid candidates
* missed solutions

---

# 10. Dataset Level 3 — Polynomial Systems

Examples:

$$
x^2-5x+6=0
$$

which has:

$$
x=2
$$

and:

$$
x=3
$$

Additional polynomial systems should follow.

The purpose is to determine whether inversion scales beyond trivial one-step equations.

---

# 11. Dataset Level 4 — Trigonometric Targets

Examples:

$$
\sin(x)=0
$$

or:

$$
\cos(x)=1
$$

These introduce periodicity and therefore multiple mathematically equivalent solution families.

The inversion system must record domain and periodicity conditions.

A candidate should never be called “the solution” when infinitely many valid solutions exist.

---

# 12. Dataset Level 5 — Optimization Targets

Define a target such as:

> Minimize \(f(x)\) subject to constraints.

For example:

$$
f(x)=x^2
$$

with the known minimum:

$$
x=0
$$

The experiment asks whether inversion can identify candidate spectral structures corresponding to the known optimum.

Optimization should be introduced only after equation solving works reliably.

---

# 13. Dataset Level 6 — Structural Targets

The inversion engine should eventually receive targets defined by properties rather than explicit numerical answers.

Examples:

```text id="o3ck3a"
TARGET:
Find an object with a specified symmetry.

TARGET:
Find a function satisfying a specified transformation.

TARGET:
Find a structure satisfying a resonance constraint.

TARGET:
Find a mathematical object belonging to a specified spectral region.
```

This begins shifting the experiment from solving known equations toward discovering mathematical structures.

---

# 14. Ground Truth

Every early inversion target must have an independently established answer.

Example:

```json id="z6t8j0"
{
  "target_id": "INV-001",
  "problem": "x + 3 = 10",
  "known_solution": "x = 7",
  "solution_type": "exact",
  "domain": "real"
}
```

For multiple solutions:

```json id="f0x2cb"
{
  "target_id": "INV-002",
  "problem": "x^2 = 4",
  "known_solutions": [
    "x = -2",
    "x = 2"
  ],
  "solution_type": "multiple",
  "domain": "real"
}
```

Ground truth must remain separate from inversion output.

---

# 15. Test 1 — Deterministic Inversion

Run the same target repeatedly.

Measure whether:

$$
T \rightarrow S^{-1}(T)
$$

produces the same candidate set under identical conditions.

Record:

* candidate coordinates
* candidate count
* ranking
* score
* runtime
* convergence

If stochastic search is used, record the random seed and distribution of results.

---

# 16. Test 2 — Known Solution Recovery

Give the engine targets with known solutions.

Determine:

* whether a valid candidate is produced
* how close the candidate is to the known solution
* whether the correct solution ranks highly
* how many false candidates are produced
* how many valid solutions are missed

This becomes the fundamental validation test for inversion.

---

# 17. Test 3 — Exact vs Approximate Recovery

Separate:

### Exact recovery

The candidate satisfies the mathematical target exactly.

### Numerical recovery

The candidate satisfies the target within a defined tolerance.

### Spectral proximity

The candidate is close in spectral space but does not satisfy the mathematical target.

These categories must never be merged.

For example:

```text id="iqm7za"
SPECTRALLY CLOSE
        ≠
MATHEMATICALLY VALID
```

---

# 18. Test 4 — Multiple-Solution Recovery

Use targets with multiple valid solutions.

Measure:

$$
Recall =
\frac{\text{valid solutions recovered}}
{\text{known valid solutions}}
$$

A system that repeatedly finds only one of many valid solutions must be reported accordingly.

This test is particularly important for periodic functions and nonlinear equations.

---

# 19. Test 5 — Constraint Handling

Introduce constraints.

Example:

$$
x^2=4
$$

with:

$$
x>0
$$

The expected solution becomes:

$$
x=2
$$

Test:

* domain constraints
* inequalities
* bounds
* symmetry constraints
* structural constraints

The system must demonstrate that constraints actually affect candidate generation.

---

# 20. Test 6 — Constraint Sensitivity

Change one constraint at a time.

Example:

```text id="5r5z7f"
TARGET:
x² = 4

CONSTRAINT A:
x > 0

CONSTRAINT B:
x < 0

CONSTRAINT C:
-10 < x < 10
```

Compare candidate sets.

The purpose is to determine whether inversion responds predictably to changes in the search conditions.

---

# 21. Test 7 — Forward/Inverse Consistency

This is one of the most important LC-05 tests.

Start with a known mathematical object:

$$
M
$$

Map it forward:

$$
M \rightarrow S(M)
$$

Then invert the resulting target.

The system should produce candidates that can be compared against the original object.

Conceptually:

```text id="2c5m0r"
KNOWN MATHEMATICAL OBJECT
          ↓
      FORWARD MAP
          ↓
   SPECTRAL REPRESENTATION
          ↓
       INVERSION
          ↓
     CANDIDATE SET
          ↓
      COMPARISON
```

Possible outcomes:

* exact recovery
* equivalent recovery
* structurally related recovery
* approximate recovery
* unrelated candidates
* no candidate

Every outcome is informative.

---

# 22. Test 8 — Perturbed Target

Take a known target and slightly modify it.

Example:

$$
x^2=25
$$

then:

$$
x^2=25.001
$$

then:

$$
x^2=25.1
$$

Observe whether candidate spectral coordinates move smoothly or undergo structural changes.

This tests whether inversion is sensitive to target perturbation.

---

# 23. Test 9 — Target Ambiguity

Provide targets that admit multiple mathematical interpretations.

For example:

$$
x^2
$$

may represent:

* an expression
* a function
* a geometric relationship
* part of an equation

The inversion system must not silently choose an interpretation when the target specification is ambiguous.

The target schema should explicitly define:

```text
OBJECTIVE TYPE
DOMAIN
VARIABLES
CONSTRAINTS
TARGET CONDITION
TOLERANCE
```

---

# 24. Test 10 — Candidate Diversity

Measure how many distinct candidates inversion produces.

Record:

* total candidates
* unique candidates
* duplicate candidates
* clusters
* candidate scores
* valid candidates
* invalid candidates

The purpose is to determine whether inversion explores meaningful alternative structures or repeatedly converges on the same local solution.

---

# 25. Test 11 — Candidate Ranking

If the engine ranks candidates, test whether ranking corresponds to mathematical validity.

For example:

```text id="x2x0kh"
RANK 1 → VALID
RANK 2 → VALID
RANK 3 → INVALID
RANK 4 → VALID
```

Measure:

* top-1 accuracy
* top-5 recovery
* top-10 recovery
* mean reciprocal rank where appropriate
* valid-candidate distribution

Do not optimize these metrics before establishing the baseline.

---

# 26. Test 12 — Search-Space Coverage

Determine how much of the available spectral space is explored.

Record:

* search bounds
* number of samples
* candidate density
* unexplored regions
* convergence regions

A failure to find a known solution may mean:

1. the inversion model is wrong
2. the search space is insufficient
3. the constraints are incorrect
4. the target representation is incorrect
5. the solution is difficult to reach
6. the implementation is broken

The experiment must distinguish these possibilities.

---

# 27. Test 13 — Search-Parameter Sensitivity

Vary inversion parameters.

Record how candidate results change with:

* search range
* resolution
* iteration count
* convergence threshold
* resonance threshold
* coordinate weighting
* initialization
* random seed

A candidate that appears only under one arbitrary parameter configuration should be treated cautiously.

---

# 28. Test 14 — Independent Verification

Every candidate solution must be passed back through conventional mathematics.

Conceptually:

```text id="07m6vl"
SPECTRAL CANDIDATE
        ↓
RECONSTRUCTION
        ↓
MATHEMATICAL OBJECT
        ↓
CONVENTIONAL VERIFICATION
        ↓
VALID / INVALID
```

This closes the inverse loop.

The inversion engine cannot certify its own answer.

---

# 29. Test 15 — False Candidate Analysis

Collect candidates that appear spectrally promising but fail mathematical verification.

Analyze why.

Possible causes:

* spectral distance is insufficient
* resonance is misleading
* target representation is incomplete
* search resolution is too low
* constraints are incomplete
* inverse mapping is non-unique
* numerical approximation creates artifacts

False candidates are valuable diagnostic information.

---

# 30. Test 16 — Known-Answer Blind Test

After tuning the inversion process on a training set, freeze the parameters.

Then provide targets from a holdout set.

The system must operate without access to the known answer.

After candidate generation, compare against the hidden ground truth.

This prevents overfitting.

---

# 31. Test 17 — Cross-Domain Inversion

After simple inversion is validated, test multiple mathematical domains.

Examples:

```text id="1r6l95"
ALGEBRA
TRIGONOMETRY
CALCULUS
GEOMETRY
LINEAR ALGEBRA
NUMBER THEORY
```

Determine whether inversion behavior is domain-specific.

Do not assume a method that works for algebra will work for number theory.

---

# 32. Test 18 — Structural Inversion

Move beyond explicit numerical solutions.

Define a target property such as:

```text id="6h8g2m"
TARGET:
Find a mathematical object exhibiting symmetry X.

TARGET:
Find an object satisfying transformation Y.

TARGET:
Find a structure resonating with target object Z.
```

The engine should return candidate structures.

These candidates then become subjects for conventional mathematical analysis.

This is where inversion begins transitioning from **known-answer recovery** toward **discovery**.

---

# 33. Test 19 — Novel Candidate Generation

Once known-answer recovery is established, permit the inversion engine to search without a predetermined answer.

The output is not:

> “The system solved the problem.”

The output is:

> **Candidate mathematical structures satisfying the specified target conditions.**

Each candidate receives a status:

```text id="oq5r7m"
GENERATED
UNVERIFIED
```

The next research stage determines whether the candidate has mathematical significance.

---

# 34. Test 20 — Discovery Candidate Workflow

Use:

```text id="c5m6u3"
TARGET
  ↓
INVERSION
  ↓
CANDIDATES
  ↓
FILTER
  ↓
CONVENTIONAL VERIFICATION
  ↓
REPRODUCTION
  ↓
KNOWN-MATHEMATICS CHECK
  ↓
HYPOTHESIS
  ↓
NEW EXPERIMENT
```

An inversion candidate becomes interesting when it:

1. satisfies the target,
2. survives independent verification,
3. reproduces,
4. is not an artifact,
5. reveals a relationship not already encoded into the search.

---

# 35. Candidate Record

Every candidate should have a complete record.

Example:

```json id="l7e3kq"
{
  "candidate_id": "INV-CAND-001",
  "target_id": "INV-021",
  "spectral_coordinates": {},
  "candidate_score": 0.91,
  "constraints_satisfied": [],
  "mathematical_verification": "pending",
  "replication_count": 0,
  "conventional_analysis": "pending",
  "status": "unverified"
}
```

Do not promote:

```text
unverified
```

to:

```text
verified
```

without independent evidence.

---

# 36. Candidate Classification

Every inversion output should be classified as one of:

```text id="u0m1gc"
VALID EXACT
VALID APPROXIMATE
EQUIVALENT SOLUTION
STRUCTURALLY RELATED
INVALID
DUPLICATE
UNRESOLVED
```

This prevents all outputs from being treated as successes.

---

# 37. Metrics

Record at minimum:

### Recovery

* valid candidate rate
* exact recovery rate
* approximate recovery rate
* solution recall
* false candidate rate

### Search

* search space
* search coverage
* candidate count
* candidate diversity
* convergence rate

### Stability

* parameter sensitivity
* seed sensitivity
* representation sensitivity
* constraint sensitivity

### Verification

* independently verified candidates
* invalid candidates
* unresolved candidates

### Efficiency

* runtime
* memory
* evaluations
* convergence iterations

---

# 38. Success Levels

## Level 0 — Candidate Generation

The inversion engine produces candidate spectral coordinates.

---

## Level 1 — Deterministic Inversion

Repeated identical runs produce reproducible candidates.

---

## Level 2 — Known-Solution Recovery

Known mathematical solutions are recovered reliably.

---

## Level 3 — Constraint-Aware Recovery

The engine responds correctly to mathematical constraints and multiple-solution conditions.

---

## Level 4 — Structural Inversion

The engine produces useful candidate structures for targets defined by mathematical properties rather than simple numerical answers.

---

## Level 5 — Discovery Utility

Inversion produces a previously unrecognized candidate mathematical structure that:

* satisfies the target,
* survives independent verification,
* reproduces,
* and leads to a genuinely new mathematical hypothesis.

---

# 39. Failure Conditions

Record failures including:

* no candidates for known solvable targets
* candidates fail conventional verification
* results depend excessively on search parameters
* correct solutions are consistently missed
* multiple valid solutions collapse into one without explanation
* false candidates dominate
* inversion reproduces only trivial transformations
* candidate generation cannot be independently reproduced
* apparent discoveries disappear under blind testing

Failure does not mean inversion is impossible.

It identifies which part of the inverse model requires investigation.

---

# 40. Evidence Package

The public evidence package should contain:

```text id="lq6b9v"
05-spectral-inversion/
├── experiment-definition.md
├── README.md
│
├── inputs/
│   ├── known-targets.json
│   ├── multiple-solution-targets.json
│   ├── constrained-targets.json
│   ├── perturbation-targets.json
│   ├── structural-targets.json
│   └── holdout-targets.json
│
├── outputs/
│   ├── candidate-solutions.json
│   ├── candidate-scores.json
│   ├── recovery-results.json
│   ├── verification-results.json
│   └── search-statistics.json
│
├── visualizations/
│   ├── inversion-space.png
│   ├── candidate-clusters.png
│   └── target-vs-candidate.png
│
├── analysis/
│   ├── deterministic-inversion.md
│   ├── known-solution-recovery.md
│   ├── multiple-solution-analysis.md
│   ├── constraint-analysis.md
│   ├── perturbation-analysis.md
│   ├── parameter-sensitivity.md
│   ├── false-candidates.md
│   ├── holdout-results.md
│   └── discovery-candidates.md
│
└── final-report.md
```

---

# 41. Reproducibility Record

Every inversion run should record:

```text id="5wyk9e"
INVERSION ENGINE VERSION:
MAPPER VERSION:
DATASET VERSION:
TARGET VERSION:
DOMAIN:
CONSTRAINTS:
SEARCH BOUNDS:
SEARCH RESOLUTION:
ITERATION LIMIT:
CONVERGENCE THRESHOLD:
DISTANCE MODEL:
RESONANCE MODEL:
RANDOM SEED:
SOFTWARE VERSION:
RUNTIME ENVIRONMENT:
DATE:
```

If a parameter is automatically selected, the selection mechanism must also be recorded.

---

# 42. Public Evidence Boundary

The public experiment should expose:

* target definitions
* constraints
* candidate spectral outputs
* verification methodology
* verified results
* failed candidates
* search statistics
* reproducibility information
* limitations

Private implementation may retain:

* proprietary optimization
* unreleased search heuristics
* private model architectures
* undisclosed acceleration techniques
* protected discovery tooling

The public evidence must still distinguish what was actually demonstrated from what remains proprietary.

---

# 43. Relationship to the Light Calculator

LC-05 changes the direction of the research loop.

Previous experiments:

```text id="i2n5i4"
MATHEMATICS
     ↓
SPECTRAL SPACE
     ↓
RELATIONSHIPS
```

LC-05 adds:

```text id="r9e0fz"
TARGET
     ↓
SPECTRAL SPACE
     ↓
CANDIDATE
     ↓
MATHEMATICS
```

The combined system becomes:

```text id="0c2j9y"
              ┌───────────────┐
              │               ↓
MATHEMATICS → SPECTRAL SPACE → MATHEMATICS
              ↑               │
              └──── INVERSE ──┘
```

The ability to move in both directions is a major research milestone.

---

# 44. Relationship to LC-06

LC-05 establishes whether inversion can generate candidates.

LC-06 asks a stricter question:

> **Can the system recover known mathematical solutions without being given the answer?**

This is the formal **Known-Solution Recovery** experiment.

The distinction is important.

LC-05 develops and characterizes the inverse mechanism.

LC-06 independently evaluates its ability to recover known solutions.

---

# 45. Relationship to Unsolved Mathematics

LC-05 must not begin with an unsolved problem.

The proper progression is:

```text id="4ak2ay"
KNOWN TARGET
      ↓
KNOWN SOLUTION
      ↓
INVERSION
      ↓
RECOVERY
      ↓
BLIND TEST
      ↓
STRUCTURAL TARGET
      ↓
NOVEL CANDIDATE
      ↓
INDEPENDENT VERIFICATION
      ↓
ONLY THEN
      ↓
DIFFICULT / OPEN PROBLEMS
```

This prevents the research program from confusing an interesting computational output with a mathematical solution.

---

# 46. Relationship to Spectral Dyad

The Spectral Dyad may eventually use inversion to explore candidate regions.

Its role is:

```text id="g7c3p8"
TARGET
   ↓
SPECTRAL INVERSION
   ↓
CANDIDATES
   ↓
DYAD OBSERVATION
   ↓
CANDIDATE RANKING / HYPOTHESIS
   ↓
CONVENTIONAL VERIFICATION
```

The Dyad can guide exploration.

It cannot declare a candidate mathematically valid.

---

# 47. Relationship to PrismChain

Important inversion runs may later be recorded as evidence.

Possible committed information:

```text id="k6e2z9"
TARGET HASH
CONSTRAINT HASH
INVERSION VERSION
PARAMETER HASH
CANDIDATE HASH
VERIFICATION RESULT HASH
EVIDENCE PACKAGE HASH
```

This allows a later researcher to establish exactly which computational run produced a candidate.

PrismChain records the computational history.

It does not certify mathematical truth.

---

# 48. Transition Criteria to LC-06

LC-05 should transition to LC-06 only after:

1. The inversion engine produces reproducible candidates.
2. Known simple targets have been tested.
3. Multiple-solution targets have been tested.
4. Constraints have been tested.
5. Forward/inverse consistency has been measured.
6. Search-parameter sensitivity has been documented.
7. False candidates have been analyzed.
8. Conventional verification is integrated into the workflow.
9. Holdout targets can be tested without changing parameters.
10. Candidate status is clearly separated into generated, verified, invalid, and unresolved.
11. The inversion configuration is frozen for the known-solution recovery experiment.

---

# 49. Next Experiment

The next experiment is:

**LC-06 — Known-Solution Recovery**

Its purpose is to provide a harder independent test.

Instead of asking:

> “Can inversion generate candidates?”

LC-06 asks:

> **“When given a target whose solution is already known to us but hidden from the system, can the spectral method recover it?”**

That experiment becomes the bridge between:

```text
INVERSE REPRESENTATION
```

and:

```text
ACTUAL PROBLEM-SOLVING UTILITY
```

---

# 50. Final Principle

> **Inversion does not prove an answer. It generates candidates that mathematics must judge.**

The Light Calculator should not be given credit for a solution simply because a point in spectral space looks promising.

A candidate must return to ordinary mathematics.

It must be checked.

It must reproduce.

It must survive controls.

And if it is genuinely new, it must withstand attempts to disprove it.

**Search backward. Generate candidates. Verify forward.**
