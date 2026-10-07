# Spectral Forge — Experiment 10: Discovery vs Memorization

**Status:** 🔵 Research
**Experiment:** 10
**Implementation Status:** Not yet demonstrated
**System:** Spectral Forge
**Directory:** `research/experiments/spectral-forge/10-discovery-vs-memorization`

---

# 1. Purpose

Experiment 10 investigates whether structures produced or recovered by Spectral Forge represent genuine mathematical or structural discovery, or whether the apparent capability can instead be explained by:

* memorization,
* retrieval,
* template reuse,
* parameter interpolation,
* recombination of known structures,
* hidden reference access,
* training-set leakage,
* or another mechanism that does not require the claimed discovery capability.

This experiment is deliberately skeptical.

A system producing something that appears new is not sufficient evidence that it discovered something new.

Likewise, a system generating a structure that was not explicitly shown during the experiment does not automatically establish that the underlying relationship was discovered.

The central goal is therefore to distinguish:

> **DISCOVERY**

from

> **RETRIEVAL / MEMORIZATION / TEMPLATE REUSE / INTERPOLATION / RECOMBINATION**

using controlled experiments and independent validation.

---

# 2. Central Question

> **When Spectral Forge produces a structure or mathematical relationship that was not supplied as a target, is the result better explained by genuine mathematical/structural discovery than by memorization, retrieval, template reuse, interpolation, or recombination of known information?**

This requires testing not merely whether the output is different.

It requires determining **where the information necessary to produce the output could have come from**.

---

# 3. Scientific Position

Novelty is necessary for some forms of discovery, but novelty alone is not sufficient.

A system can produce an apparently novel object through:

* random generation,
* interpolation,
* recombination,
* parameter variation,
* transformation of known templates,
* retrieval followed by minor modification,
* or memorized procedural rules.

Therefore:

> **Novel output ≠ novel discovery.**

Likewise:

> **Unknown to the researcher ≠ unknown to the system.**

And:

> **Not explicitly provided during execution ≠ not encoded in the system.**

Experiment 10 therefore treats discovery as a claim requiring stronger evidence than visual or superficial novelty.

---

# 4. Key Distinctions

## 4.1 Discovery vs Generation

Generation means producing an output.

Discovery implies that the system has arrived at a previously unspecified structure or relationship that is meaningfully supported by the mathematical problem.

A generator can generate without discovering.

---

## 4.2 Discovery vs Retrieval

Retrieving an existing answer is not discovery.

---

## 4.3 Discovery vs Template Reuse

A new output derived from a known template may be useful and generative without constituting discovery of a new structural relationship.

---

## 4.4 Discovery vs Parameter Variation

Changing:

```text
x → x + Δx
```

does not automatically create a new structural discovery.

---

## 4.5 Discovery vs Interpolation

An output between known examples may be novel as a specific object while remaining entirely explainable from known endpoints.

---

## 4.6 Discovery vs Recombination

Combining known structures may produce something previously unseen.

That may constitute generative novelty, but it is not necessarily discovery of a new mathematical relationship.

---

## 4.7 Discovery vs Memorized Procedure

A system may memorize a general transformation rather than individual answers.

Testing only for exact duplicate outputs therefore does not adequately test memorization.

---

# 5. Hypothesis

The primary hypothesis is:

> **If Spectral Forge performs genuine mathematical or structural discovery, then under appropriately controlled target-free and withheld-information conditions it should produce valid, reproducible structures or relationships that cannot be adequately explained by retrieval, memorization, template reuse, interpolation, recombination, or baseline generation.**

Secondary hypotheses include:

1. Discovery should survive withheld reference structures.
2. Discovery should survive changes in naming and representation.
3. Discovery should survive adversarial reference-set construction.
4. Discovery should produce independently verifiable relationships.
5. Discovery should remain meaningful under controlled perturbation.
6. Discovery should be reproducible or its stochastic behavior characterizable.
7. Discovery should outperform appropriate non-discovery baselines on predefined criteria.
8. Discovery should not depend on hidden access to the target.

These remain hypotheses until experimentally tested.

---

# 6. Definitions

## 6.1 Reference Set

The collection of structures, examples, relationships, or data available to the system before or during an experiment.

## 6.2 Target

The structure or relationship whose discovery is being evaluated.

The target must not be supplied as the answer.

## 6.3 Withheld Target

A target excluded from the system's accessible information during the discovery experiment.

## 6.4 Memorization

Retention and reproduction of previously encountered information rather than deriving the result from the current mathematical conditions.

## 6.5 Retrieval

Identification and reuse of an existing structure or answer.

## 6.6 Template Reuse

Application of an existing structural pattern to a new instance.

## 6.7 Parameter Interpolation

Construction of an output by navigating between known examples or known parameter values.

## 6.8 Recombination

Combining known components or structures into a new configuration.

## 6.9 Structural Novelty

A result that is not equivalent to an existing reference structure under the experiment's predefined equivalence relation.

## 6.10 Mathematical Discovery

A candidate relationship or structure that is:

1. not supplied as a target,
2. not adequately explained by retrieval or known transformation,
3. mathematically valid,
4. independently verifiable,
5. and supported by evidence that it follows from the investigated conditions.

The final definition may evolve with actual research.

---

# 7. Discovery Levels

Discovery should not be treated as binary.

A useful preliminary hierarchy is:

### Level 0 — Exact Retrieval

The output is an existing reference.

### Level 1 — Equivalent Retrieval

The output differs superficially but is mathematically or structurally equivalent to a reference.

### Level 2 — Parameter Variation

The output is a known structure with changed parameters.

### Level 3 — Novel Combination

Known components are recombined into a previously unseen configuration.

### Level 4 — Novel Structure

The output is structurally distinct from known references.

### Level 5 — Novel Relationship

The system identifies a relationship not explicitly supplied and independently validates it.

### Level 6 — Potential Mathematical Discovery

The discovered relationship survives independent verification, alternative derivation, adversarial testing, and broader evaluation.

Level 6 should be used extremely conservatively.

---

# 8. System Under Test

The system under test is Spectral Forge.

The experiment may evaluate both forward and inverse modes:

```text
OBJECTIVE + CONSTRAINTS
        ↓
SPECTRAL MATHEMATICS
        ↓
SPECTRAL FORGE
        ↓
NEW STRUCTURE
```

and:

```text
EXISTING STRUCTURE
        ↓
SPECTRAL FORGE
        ↓
DISCOVERED REPRESENTATION
        ↓
MATHEMATICAL RELATIONSHIP
```

The experiment must identify which mechanism produced the claimed discovery.

---

# 9. Information Boundary

The information boundary is one of the most important components of this experiment.

Before execution, document:

* accessible reference structures,
* inaccessible structures,
* training data where relevant,
* generated data,
* mathematical definitions,
* objective,
* constraints,
* external resources,
* software dependencies,
* model weights where applicable,
* and any prior derived representations.

The experiment must make a serious attempt to answer:

> **What information was actually available to Spectral Forge?**

A result cannot be classified as a strong discovery if the target or an equivalent representation was secretly available.

---

# 10. Experimental Design

## Step 1 — Construct the Reference Set

Create a frozen reference set.

The set should include:

* known structures,
* related structures,
* near-neighbor structures,
* templates,
* parameterized families,
* and adversarial examples where appropriate.

---

## Step 2 — Withhold Targets

Select targets that are inaccessible during the discovery phase.

Targets should be selected before execution.

---

## Step 3 — Define Discovery Criteria

Before generating results, define:

* structural validity,
* mathematical validity,
* novelty,
* equivalence,
* acceptable similarity,
* reconstruction criteria,
* predictive criteria,
* and evidence required for discovery classification.

---

## Step 4 — Run Spectral Forge

Provide only the permitted information.

The system must not receive the hidden target.

---

## Step 5 — Evaluate Output

Determine:

* Is it valid?
* Is it structurally novel?
* Is it mathematically meaningful?
* Is it equivalent to a reference?
* Is it a transformed template?
* Is it an interpolation?
* Is it a recombination?
* Can the result be independently reconstructed?

---

## Step 6 — Attempt Explanation by Simpler Mechanisms

Before labeling a result discovery, attempt to explain it through:

1. exact retrieval,
2. nearest-neighbor retrieval,
3. template transformation,
4. parameter interpolation,
5. recombination,
6. known mathematical transformation,
7. random generation,
8. generic optimization,
9. domain-specific baseline.

If a simpler mechanism explains the result, the discovery claim should be downgraded.

---

# 11. Controls

## Control A — Exact Retrieval

Give a retrieval system access to the same reference set.

Purpose:

> Establish the strongest expected memorization/retrieval baseline.

---

## Control B — Template Generator

Construct outputs using known templates.

Purpose:

> Determine how much apparent novelty can arise through template reuse.

---

## Control C — Parameter Interpolation

Interpolate between known structures.

Purpose:

> Measure novelty that can arise without structural discovery.

---

## Control D — Template Recombination

Combine known components.

Purpose:

> Establish the baseline for combinatorial novelty.

---

## Control E — Random Generator

Generate candidates randomly within the valid domain.

Purpose:

> Determine whether validity and superficial novelty can arise without mathematical discovery.

---

## Control F — Generic Optimizer

Use a general optimization mechanism without the proposed Spectral Forge mechanism.

Purpose:

> Determine whether the result depends specifically on the spectral methodology.

---

## Control G — Reference-Removed Forge

Remove selected reference classes.

Purpose:

> Test whether the result depends on access to particular examples.

---

# 12. Test Classes

## Test Class 1 — Withheld Structure Discovery

A target structure is completely withheld.

The system must derive a valid candidate from the available mathematical conditions.

---

## Test Class 2 — Withheld Combination

Individual components are known, but their specific combination is withheld.

This distinguishes:

* simple recombination,
* structured synthesis,
* and potentially novel relationships.

---

## Test Class 3 — Withheld Parameter Region

Known structures exist around a region, but the target lies outside the observed parameter values.

Purpose:

> Distinguish interpolation from extrapolative structure generation.

---

## Test Class 4 — Representation Renaming

Rename variables, structures, or components without changing their mathematical relationships.

Purpose:

> Test whether the system depends on semantic labels rather than mathematical structure.

---

## Test Class 5 — Adversarial Reference Set

Construct a reference set containing highly similar but incorrect candidates.

Purpose:

> Test whether Forge follows mathematical constraints or simply chooses the nearest familiar structure.

---

## Test Class 6 — Template Removal

Remove the closest known template.

Purpose:

> Test whether generation remains possible without direct structural scaffolding.

---

## Test Class 7 — Structural Perturbation

Perturb known examples before making them available.

Purpose:

> Test whether the system tracks underlying relationships rather than memorized surface patterns.

---

## Test Class 8 — Hidden Evaluation

The final validator or target comparison remains hidden from the system.

Purpose:

> Reduce the possibility of optimizing directly against the evaluation mechanism.

---

## Test Class 9 — Independent Reconstruction

Provide the discovered result to an independent implementation or researcher.

Ask:

> Can the claimed relationship be reconstructed from the reported mathematical conditions?

---

## Test Class 10 — Repeated Discovery

Repeat the discovery problem across:

* random seeds,
* equivalent representations,
* reordered inputs,
* different environments,
* and related problem instances.

Purpose:

> Determine whether the result is a reproducible phenomenon rather than a one-time artifact.

---

# 13. Anti-Memorization Tests

A strong experiment should use multiple anti-memorization strategies.

## 13.1 Withheld Examples

The target is never present in the accessible reference set.

## 13.2 Withheld Combinations

Components are available individually but not in the target configuration.

## 13.3 Withheld Parameter Regions

The system cannot simply interpolate through the target region.

## 13.4 Randomized Naming

Rename structures and variables.

## 13.5 Structural Perturbation

Modify superficial features while preserving mathematical relationships.

## 13.6 Adversarial Near-Neighbors

Provide highly similar incorrect examples.

## 13.7 Template Removal

Remove the most obvious structural template.

## 13.8 Independent Validator

Use a validator that did not participate in generation.

## 13.9 Blind Evaluation

Keep the target and evaluation criteria hidden where practical.

## 13.10 Cross-Domain Testing

Repeat the methodology in a structurally different domain.

A strong result should survive several of these tests.

---

# 14. Measurements

Measurements should include both novelty and explanatory alternatives.

### Exact Match Rate

Percentage of outputs identical to references.

### Equivalence Rate

Percentage mathematically equivalent to references.

### Nearest-Reference Distance

Distance from the closest known structure.

### Template Similarity

Similarity to known templates.

### Parameter Distance

Distance from known parameter configurations.

### Novelty Rate

Percentage satisfying the predefined novelty criterion.

### Validity Rate

Percentage satisfying mathematical and structural validity criteria.

### Constraint Satisfaction

Percentage satisfying all hard constraints.

### Independent Verification Rate

Percentage independently validated.

### Reconstruction Rate

Percentage for which the discovered relationship can regenerate or explain the observed structure.

### Predictive Value

Whether the discovered relationship predicts withheld properties or examples.

### Baseline Advantage

Difference between Forge performance and non-discovery baselines.

### Reproducibility

Stability of discovery across repeated runs.

---

# 15. Discovery Evidence Ladder

A candidate result should accumulate evidence progressively.

### Stage 1 — Output Difference

The output differs from known examples.

This is weak evidence.

### Stage 2 — Structural Novelty

The output is not equivalent to known references.

Stronger, but still insufficient.

### Stage 3 — Mathematical Validity

The output satisfies formal mathematical conditions.

Necessary, but still insufficient.

### Stage 4 — Baseline Separation

Known retrieval/template/interpolation/recombination mechanisms cannot adequately explain the result.

### Stage 5 — Independent Verification

An independent validator confirms the result.

### Stage 6 — Predictive Power

The discovered relationship predicts withheld observations or structures.

### Stage 7 — Independent Reconstruction

Another researcher or implementation can reproduce the discovery from the documented conditions.

### Stage 8 — Cross-Context Survival

The relationship remains valid under controlled perturbations, representations, or domains.

Only at the upper levels should strong discovery language be considered.

---

# 16. Negative Controls

Negative controls should include:

* targets directly supplied to the system,
* targets equivalent to known templates,
* trivial parameter changes,
* intentionally duplicated references,
* impossible mathematical conditions,
* contradictory constraints,
* corrupted reference sets,
* shuffled relationships,
* misleading near-neighbor structures,
* and invalid targets.

The system should not receive discovery credit for reproducing information that the experimental design intentionally made available.

---

# 17. Acceptance Criteria

Experiment 10 should not classify a result as strong discovery unless:

1. The target was defined before execution.
2. The target was withheld from the system.
3. The accessible information boundary is documented.
4. Reference sets are frozen.
5. Novelty criteria are predefined.
6. Mathematical validity is independently verified.
7. Retrieval is tested as an alternative explanation.
8. Template reuse is tested.
9. Parameter interpolation is tested where relevant.
10. Recombination is tested where relevant.
11. Random and generic baselines are included where appropriate.
12. At least one strong anti-memorization condition is satisfied.
13. The result is independently validated.
14. Repeated execution characterizes reproducibility.
15. The result demonstrates value beyond merely being different.
16. Simpler explanations have been explicitly tested.
17. Any remaining uncertainty is recorded.

---

# 18. Failure Conditions

A discovery claim should be rejected or downgraded if:

* the target was accessible,
* an equivalent target was accessible,
* a template directly explains the result,
* interpolation explains the result,
* recombination fully explains the result,
* retrieval performs equally well,
* random generation performs equally well,
* the result is mathematically invalid,
* novelty exists only under a superficial metric,
* the validator depends on the generator,
* the result cannot be reproduced,
* hidden information is discovered after execution,
* or the claimed relationship cannot be independently verified.

A negative result is scientifically useful.

For example:

> “Spectral Forge produced novel structures, but all observed novelty was explained by template recombination.”

would be a valuable result.

It narrows the actual capability.

---

# 19. Implementation vs Specification

This experiment does not assume that Spectral Forge contains an explicit “discovery detector.”

The actual implementation may use:

* graph comparison,
* symbolic equivalence,
* structural fingerprints,
* mathematical invariants,
* nearest-neighbor analysis,
* representation distance,
* independent theorem checking,
* reconstruction tests,
* predictive holdouts,
* or other mechanisms.

The experimental framework should determine which mechanisms are necessary.

The implementation should not be designed to guarantee a discovery classification.

The classification must emerge from evidence.

---

# 20. Relationship to Previous Experiments

Experiment 10 builds directly on the previous nine experiments.

### Experiment 01 — Forward Design

Established the question of constructing structures from objectives and constraints.

Experiment 10 asks whether apparently new constructions are genuinely new or derivable from known templates.

### Experiment 02 — Inverse Discovery

Introduced inverse mathematical discovery.

Experiment 10 asks whether the discovered representation is genuinely inferred or simply reconstructed from memorized examples.

### Experiment 03 — Constraint Satisfaction

Provides formal conditions for validity.

Experiment 10 uses those conditions to distinguish valid discovery from arbitrary novelty.

### Experiment 04 — Structure Generation

Provides the generative foundation.

Experiment 10 investigates the origin of generated novelty.

### Experiment 05 — Forward–Inverse Consistency

Provides a mechanism for reconstructing relationships.

Experiment 10 asks whether consistency survives when known answers are withheld.

### Experiment 06 — Novel Structure Discovery

Experiment 06 established novelty as a research target.

Experiment 10 now applies a much stricter standard:

> **Novelty must be separated from memorization and known transformations.**

### Experiment 07 — Cross-Domain Generality

Provides a powerful anti-memorization dimension.

A mechanism that survives meaningful domain changes provides stronger evidence than one restricted to a single familiar domain.

### Experiment 08 — Reproducibility

Provides the requirement that discovery claims must survive independent reconstruction.

### Experiment 09 — Sensitivity and Perturbation

Provides another diagnostic.

A memorized or brittle mechanism may respond differently from a system actually following underlying mathematical relationships.

---

# 21. Relationship to Future Experiments

Experiment 10 establishes a foundation for later research into:

* adversarial integrity,
* discovery reliability,
* mathematical relationship extraction,
* independent scientific validation,
* and end-to-end Spectral Forge behavior.

Future experiments may investigate whether candidate discoveries:

* survive adversarial conditions,
* generate new predictions,
* transfer across domains,
* produce interpretable mathematical structures,
* or contribute to broader computational systems.

---

# 22. What This Experiment Does Not Prove

Even a strong Experiment 10 result does **not** automatically prove:

* artificial general intelligence,
* consciousness,
* universal mathematical reasoning,
* universal discovery,
* autonomous scientific research,
* correctness of every discovered relationship,
* uniqueness of the discovery,
* superiority over human researchers,
* new fundamental mathematics,
* PrismChain functionality,
* Rainbow Ring functionality,
* Spectral Dyad functionality,
* or production readiness.

It establishes evidence about a much narrower question:

> **Whether the observed result is better explained by discovery than by known forms of information reuse.**

---

# 23. Limitations

No finite experiment can prove the complete absence of memorization.

A system may contain information in forms that the experiment does not detect.

Likewise, determining whether a transformation constitutes “discovery” can depend on the chosen mathematical and structural definitions.

Therefore:

* anti-memorization tests should be layered,
* information boundaries should be explicit,
* baseline mechanisms should be strong,
* claims should remain proportional to evidence,
* and unresolved explanations should remain visible.

The experiment should never convert:

> “We did not find evidence of memorization”

into:

> “Memorization is impossible.”

---

# 24. Evidence Package

A completed evidence package should contain, where applicable:

```text
10-discovery-vs-memorization/
├── README.md
├── experiment-specification.md
├── information-boundary/
├── reference-set/
├── withheld-targets/
├── target-generation/
├── configurations/
├── baseline-retrieval/
├── baseline-template/
├── baseline-interpolation/
├── baseline-recombination/
├── baseline-random/
├── baseline-generic/
├── forge-results/
├── novelty-analysis/
├── equivalence-analysis/
├── anti-memorization/
├── independent-validation/
├── reproduction/
├── failure-cases/
└── FINAL-RESULTS.md
```

The evidence package should preserve both successful and rejected discovery candidates.

Rejected candidates are important because they demonstrate that the experiment did not simply label every unusual output as discovery.

---

# 25. Suggested Discovery Manifest

A machine-readable manifest may contain:

```text
experiment_id
source_commit
environment
reference_set_hash
withheld_target_hash
information_boundary
configuration_hash
random_seed
output_hash
nearest_reference
nearest_reference_distance
equivalence_result
template_similarity
parameter_distance
novelty_class
mathematical_validity
constraint_satisfaction
baseline_retrieval_result
baseline_template_result
baseline_interpolation_result
baseline_recombination_result
baseline_random_result
independent_validation_result
reconstruction_result
predictive_holdout_result
reproduction_result
discovery_level
uncertainties
```

The exact schema should evolve with implementation.

---

# 26. Interpretation Framework

Results should be reported using conservative categories.

### Category A — Explained by Retrieval

No discovery claim.

### Category B — Explained by Transformation

The output is produced by a known transformation, template, interpolation, or recombination.

### Category C — Novel Generation

The output is structurally novel but the mechanism remains explainable without claiming mathematical discovery.

### Category D — Candidate Discovery

The output is novel, mathematically valid, independently verified, and not adequately explained by tested baselines.

### Category E — Supported Discovery

The candidate survives repeated testing, anti-memorization controls, independent reconstruction, and predictive evaluation.

### Category F — Potential New Mathematical Relationship

Reserved for cases where a relationship survives unusually strong mathematical and independent scrutiny.

This final category should be extremely rare.

---

# 27. Core Scientific Principle

The experiment must enforce a higher standard than:

> “The output looks new.”

The relevant question is:

> **What evidence shows that the result could not have been obtained simply by reusing information already available to the system?**

The stronger the alternative explanations, the stronger the discovery evidence must become.

---

# 28. Final Principle

> **Novel output is not automatically novel discovery.**

A structure can be new because it was:

* retrieved,
* transformed,
* interpolated,
* recombined,
* randomized,
* or genuinely discovered.

Spectral Forge research must distinguish these mechanisms rather than collapsing them into a single category called “generation.”

The scientific objective is therefore not to make Spectral Forge appear capable of discovery.

It is to determine, through controlled evidence, **whether discovery is actually occurring, what kind of discovery it is, and what simpler explanations have been ruled out.**

> **Discovery must survive the question: “Where did the information come from?”**
