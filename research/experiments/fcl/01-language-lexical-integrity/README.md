# Experiment 01 — Language Lexical Integrity

**System:** Fluxling Code Language (FCL)
**Research Track:** FCL / FluxVM / PrismChain
**Experiment:** 01 of 20
**Status:** 🔵 Research — implementation not yet demonstrated
**Layer:** FCL Language Foundation
**Primary Boundary:** FCL Source → Lexical Token Stream
**Depends On:** FCL language specification
**Feeds Into:** Experiment 02 — Syntax and AST Construction

---

## 1. Purpose

Experiment 01 establishes the lexical foundation of **Fluxling Code Language (FCL)**.

The purpose is to determine whether FCL source code can be transformed into a deterministic, reproducible lexical token stream while preserving every element that is syntactically meaningful to the language.

The experiment focuses on the first stage of the proposed FCL compiler:

```text
FCL SOURCE
    ↓
LEXICAL ANALYSIS
    ↓
TOKEN STREAM
    ↓
SYNTAX ANALYSIS
```

The experiment does **not** attempt to establish whether FCL programs execute correctly.

It asks a narrower and more fundamental question:

> Can FCL reliably recognize and distinguish the symbols, operators, identifiers, literals, spectral annotations, delimiters, and other lexical elements that constitute its source language?

A successful result establishes a trustworthy lexical boundary for subsequent FCL experiments.

---

# 2. Central Question

> **Can FCL source code be lexically tokenized deterministically and without ambiguity, while preserving all syntactically meaningful symbols and rejecting malformed or ambiguous lexical forms in a reproducible manner?**

This question includes several subordinate questions:

1. Are FCL's symbolic operators recognized consistently?
2. Are Unicode-based FCL symbols preserved correctly?
3. Are identifiers recognized consistently?
4. Are spectral-layer annotations such as `*1`–`*7` recognized correctly?
5. Are multi-character operators distinguished from their component characters?
6. Does whitespace affect tokenization only where the language specifies that it should?
7. Are malformed or unsupported symbols rejected deterministically?
8. Is Unicode normalization handled explicitly rather than implicitly?
9. Does identical source produce identical token streams?
10. Can lexical errors be localized precisely enough for later compiler stages?

---

# 3. Scientific Position

FCL is currently a language specification and research program, not a demonstrated compiler implementation.

Therefore this experiment must distinguish between:

* **proposed FCL syntax**
* **implemented lexical behavior**
* **experimentally demonstrated lexical behavior**
* **future language decisions**

The existence of a proposed symbol in an FCL specification does not by itself establish that a compiler recognizes that symbol.

Likewise, successful tokenization of a symbol does not establish the symbol's semantic meaning.

The experiment therefore treats lexical recognition as an independently testable layer.

---

# 4. System Under Test

The proposed system boundary is:

```text
                FCL SOURCE
                    │
                    ▼
          ┌───────────────────┐
          │   FCL LEXER       │
          │                   │
          │ Unicode handling  │
          │ Symbol recognition│
          │ Operator matching │
          │ Identifier rules  │
          │ Literal handling  │
          │ Layer tags        │
          │ Error detection   │
          └─────────┬─────────┘
                    │
                    ▼
             TOKEN STREAM
                    │
                    ▼
        Experiment 02 — AST
```

The lexer is responsible for lexical structure only.

It should not perform:

* semantic type checking
* program execution
* FluxVM execution
* PrismChain computation
* WLB formation
* FractaChain storage
* Rainbow Ring interaction
* Spectral Dyad reasoning

Those belong to later boundaries.

---

# 5. Proposed FCL Lexical Elements

The current FCL specification includes symbolic elements such as:

```text
▲
~~
•=
~~>
✴
::
```

and spectral-layer annotations:

```text
*1
*2
*3
*4
*5
*6
*7
```

An example FCL fragment is:

```text
▲ MintMoment(user, place, emotion):
*4: Memory Layer

if user | emotion:
    user ~~ place
    moment •= encode(user, place, emotion)
    signal ~~> @network
✴ return moment
```

This example is useful as a fixture because it combines:

* Unicode symbols
* identifiers
* punctuation
* keywords
* operators
* spectral context
* indentation/whitespace
* function-like syntax
* literals or symbolic references
* multi-character operators

The exact lexical classification of individual elements remains subject to implementation and subsequent specification refinement.

---

# 6. Lexical Integrity

For this experiment, **lexical integrity** means that the lexer preserves the distinction between all lexical elements required by the FCL grammar.

A lexically valid source program should produce a token sequence that is:

1. deterministic,
2. ordered,
3. complete with respect to meaningful source elements,
4. unambiguous under the current lexical specification,
5. reproducible,
6. traceable back to source positions,
7. resistant to accidental Unicode transformations,
8. suitable for deterministic parsing.

A lexer must not silently transform one lexical construct into another.

---

# 7. Critical Distinctions

This experiment establishes several boundaries.

### 7.1 Lexical Recognition ≠ Syntax

Recognizing:

```text
~~>
```

does not establish that it is valid in every syntactic position.

That belongs to syntax analysis.

---

### 7.2 Syntax ≠ Semantics

Recognizing:

```text
*4
```

does not establish what spectral layer 4 means semantically.

That belongs to semantic analysis.

---

### 7.3 Lexical Recognition ≠ Execution

Recognizing:

```text
MINT
```

does not demonstrate that a mint operation can actually execute.

Execution belongs to FluxVM and later PrismChain experiments.

---

### 7.4 Symbol Recognition ≠ Physical Light Encoding

Recognizing:

```text
▲
```

as an FCL source symbol does not establish that the symbol is physically encoded through a wavelength, phase, amplitude, polarization, or photonic carrier.

Those remain separate research questions.

---

### 7.5 Unicode Representation ≠ Physical Spectrum

A Unicode character representing a spectral concept is a software representation.

It is not itself a physical wavelength.

---

### 7.6 Tokenization ≠ Language Completeness

A lexer can successfully tokenize a language that is still incomplete.

This experiment therefore does not attempt to prove that the complete FCL language has been defined.

---

# 8. Hypothesis

### Primary Hypothesis

> **FCL source can be transformed into a deterministic lexical representation in which every defined lexical construct has a unique or explicitly resolved token interpretation, Unicode symbols are preserved correctly, malformed constructs are rejected predictably, and identical source produces identical token output.**

### Secondary Hypotheses

1. FCL's symbolic operators can be recognized without ambiguity.
2. Multi-character operators can be distinguished from individual characters.
3. Spectral-layer annotations can be lexically isolated.
4. Unicode normalization can be controlled explicitly.
5. Source positions can be preserved through tokenization.
6. Invalid lexical sequences can be rejected without corrupting surrounding tokens.
7. Equivalent source representations behave consistently only where equivalence is explicitly defined.

---

# 9. Proposed Token Categories

The implementation may evolve, but the experiment should investigate at least the following conceptual categories:

```text
KEYWORD
IDENTIFIER
OPERATOR
SYMBOL
DELIMITER
LITERAL
SPECTRAL_TAG
ANNOTATION
WHITESPACE
NEWLINE
COMMENT
ERROR
EOF
```

These categories are experimental abstractions rather than an assertion that the final compiler must use these exact names.

---

# 10. Symbol Integrity Tests

The lexer should independently test every currently proposed symbolic construct.

At minimum:

```text
▲
~~
•=
~~>
✴
::
```

For each symbol, test:

1. isolated occurrence,
2. occurrence at beginning of source,
3. occurrence at end of source,
4. occurrence between identifiers,
5. repeated occurrence,
6. adjacent occurrence,
7. occurrence without whitespace,
8. occurrence with whitespace,
9. occurrence across line boundaries where applicable,
10. malformed variants.

Example fixture family:

```text
a ~~ b
a~~b
a ~~> b
a~~>b
a •= b
a•=b
```

The purpose is to determine whether whitespace changes lexical interpretation.

---

# 11. Multi-Character Operator Integrity

Multi-character operators are a critical lexical boundary.

For example:

```text
~~>
```

contains characters that may individually have meaning elsewhere.

The lexer must determine whether:

```text
~~>
```

is:

```text
ONE TOKEN
```

or:

```text
~~
>
```

according to the actual lexical specification.

The same principle applies to:

```text
•=
::
```

and every other multi-character construct.

The experiment should explicitly test **longest valid token matching** where that rule is adopted.

If longest-match behavior is not adopted, the alternative rule must be explicitly documented and experimentally tested.

---

# 12. Unicode Integrity

Unicode is a first-class experimental concern because FCL intentionally uses symbolic characters.

The lexer must not assume that visually similar characters are necessarily identical characters.

Tests should include:

* exact Unicode code point,
* visually similar character,
* composed vs decomposed sequences where applicable,
* normalization forms,
* unexpected Unicode whitespace,
* zero-width characters,
* Unicode lookalikes,
* Unicode punctuation substitutions,
* unsupported symbolic characters.

For example, a visually similar symbol must not automatically be accepted as equivalent merely because it appears identical to a human observer.

The experiment should explicitly document the normalization policy:

```text
RAW SOURCE
    ↓
NORMALIZATION POLICY
    ↓
LEXICAL ANALYSIS
```

or:

```text
RAW SOURCE
    ↓
LEXICAL ANALYSIS
```

if FCL deliberately requires byte/code-point exactness.

The choice must be explicit.

---

# 13. Spectral Layer Tag Tests

The proposed FCL syntax includes spectral annotations:

```text
*1
*2
*3
*4
*5
*6
*7
```

The experiment should test:

```text
*1
*2
*3
*4
*5
*6
*7
```

and invalid forms such as:

```text
*0
*8
*01
*1x
**
*
```

where applicable to the specification.

The purpose is to establish whether the lexer can distinguish:

```text
SPECTRAL_TAG
```

from:

```text
OPERATOR + INTEGER
```

or another lexical interpretation.

This experiment does not determine the semantic meaning of each spectral layer.

---

# 14. Identifier Tests

Identifiers should be tested for:

* ordinary alphabetic names,
* numeric suffixes,
* underscores if permitted,
* Unicode identifiers if permitted,
* reserved words,
* case sensitivity,
* leading digits,
* empty identifiers,
* identifier/operator adjacency,
* identifier/symbol adjacency.

Example fixtures:

```text
user
place
emotion
moment
signal
network
user1
user_1
1user
```

The exact accepted forms must be determined by the FCL lexical specification.

---

# 15. Keyword Tests

Proposed language constructs such as:

```text
if
return
```

must be tested separately from ordinary identifiers.

For example:

```text
if
return
iff
returned
if_value
```

The lexer must not incorrectly classify an identifier merely because it begins with a keyword.

The distinction between:

```text
KEYWORD
```

and:

```text
IDENTIFIER
```

must be deterministic.

---

# 16. Delimiter Tests

The current FCL examples include conventional delimiters such as:

```text
(
)
,
:
```

The experiment should determine whether each is:

* a standalone token,
* part of another token,
* ignored under a particular context,
* syntactically meaningful only at a later stage.

Tests should include adjacent delimiters:

```text
(user,place,emotion)
```

and separated forms:

```text
(user, place, emotion)
```

---

# 17. Whitespace Tests

Whitespace behavior must be explicitly established.

Test:

```text
a~~b
a ~~ b
a  ~~  b
a\t~~\tb
```

and newline variants.

The experiment should determine whether whitespace is:

* discarded,
* preserved,
* represented as tokens,
* syntactically significant,
* significant only for diagnostics.

No assumption should be made that whitespace is irrelevant.

---

# 18. Newline Tests

Test:

```text
a
b
```

versus:

```text
a b
```

and symbolic constructs split across lines where applicable.

Examples:

```text
a ~~
b
```

```text
a
~~
b
```

The lexer must either define or explicitly reject such constructs.

---

# 19. Comment Tests

If FCL supports comments, comments must be lexically tested.

At minimum:

```text
comment before code
code followed by comment
comment between tokens
comment containing FCL symbols
comment containing Unicode symbols
comment containing apparent operators
```

For example, a comment containing:

```text
~~>
```

must not accidentally generate an executable operator token if comments are defined as lexically ignored.

If comments are not yet specified, the experiment should mark comment handling as **unresolved**, rather than silently inventing syntax.

---

# 20. Literal Tests

If FCL supports literals, test each defined literal class.

Potential classes include:

```text
INTEGER
FLOAT
STRING
BOOLEAN
NULL/NONE
BYTE
WAVE VALUE
SIGNAL VALUE
```

These are only candidate categories until the language specification establishes them.

The experiment must not assume unsupported literal types.

Tests should include:

* valid literals,
* malformed literals,
* boundary values,
* adjacent identifiers,
* adjacent operators,
* Unicode content where permitted,
* escaping rules where applicable.

---

# 21. Malformed Symbol Tests

A robust lexer must not merely recognize valid source.

It must also identify invalid source.

Test cases should include:

```text
~
~
~
•>
=
=>
>>
<<
***
*8
invalid Unicode symbol
truncated operator
unknown operator
```

The exact malformed corpus should evolve with the lexical specification.

Each rejected input should produce:

* error category,
* source location,
* offending sequence,
* lexer version,
* normalization mode,
* deterministic error result.

---

# 22. Ambiguity Tests

Ambiguity is one of the most important targets of this experiment.

Construct source fixtures where two lexical interpretations could plausibly occur.

For example:

```text
a~~>b
```

Potential interpretations might include:

```text
[IDENTIFIER][OPERATOR][IDENTIFIER]
```

or:

```text
[IDENTIFIER][OPERATOR_A][OPERATOR_B][IDENTIFIER]
```

The actual lexer must resolve this according to an explicit lexical rule.

Every identified ambiguity must result in one of:

1. deterministic resolution,
2. explicit lexical error,
3. specification revision.

Silent ambiguity is a failure.

---

# 23. Unicode Normalization Experiment

A dedicated normalization matrix should be created.

For each Unicode-sensitive token:

```text
RAW FORM
NFC
NFD
NFKC
NFKD
```

should be compared where meaningful.

The experiment should determine:

* whether all forms are accepted,
* whether only one form is accepted,
* whether normalization occurs before lexing,
* whether normalization changes token identity,
* whether normalization can alter source semantics,
* whether source hashes are calculated before or after normalization.

This is particularly important if FCL source is eventually hashed, signed, compiled, or referenced by PrismChain.

---

# 24. Source Position Integrity

Each token should preserve sufficient source-location information to identify its origin.

At minimum:

```text
source identifier
line
column
start offset
end offset
token type
token value
```

where practical.

The experiment should verify that Unicode characters do not cause incorrect source positioning.

This matters because one visible character may not correspond to one byte.

---

# 25. Determinism Test

Given identical source:

```text
SOURCE X
```

run the lexer repeatedly.

Expected result:

```text
TOKEN_STREAM_1
=
TOKEN_STREAM_2
=
TOKEN_STREAM_3
...
```

The comparison should include:

* token order,
* token type,
* token value,
* source location,
* error state,
* normalization state.

Any nondeterministic result requires investigation.

---

# 26. Token Stream Canonicalization

Where appropriate, the experiment should establish a canonical representation of the token stream.

Example conceptual representation:

```text
[
  {
    "type": "SYMBOL",
    "value": "▲",
    "line": 1,
    "column": 1
  },
  {
    "type": "IDENTIFIER",
    "value": "MintMoment",
    "line": 1,
    "column": 3
  }
]
```

This is illustrative rather than a locked schema.

The actual implementation may use another representation.

The important property is that equivalent lexical results can be compared deterministically.

---

# 27. Test Corpus

The experiment should create a version-controlled lexical fixture corpus.

Suggested structure:

```text
fixtures/
├── valid/
│   ├── symbols/
│   ├── operators/
│   ├── identifiers/
│   ├── spectral-tags/
│   ├── delimiters/
│   ├── whitespace/
│   ├── unicode/
│   └── combined/
│
├── invalid/
│   ├── malformed-symbols/
│   ├── malformed-operators/
│   ├── invalid-spectral-tags/
│   ├── invalid-identifiers/
│   ├── unicode-errors/
│   └── ambiguous-forms/
│
└── golden/
    ├── token-streams/
    └── errors/
```

The fixture corpus itself becomes part of the evidence.

---

# 28. Controls

The experiment should include several controls.

### Control A — Plain ASCII

Use source containing only conventional ASCII identifiers and punctuation.

Purpose:

Establish baseline lexer behavior independent of FCL's Unicode symbols.

---

### Control B — Unicode Symbols

Use only defined FCL Unicode symbols.

Purpose:

Determine whether Unicode introduces lexical instability.

---

### Control C — Equivalent Formatting

Compare:

```text
a~~>b
```

with:

```text
a ~~> b
```

Purpose:

Determine whether formatting changes tokenization.

---

### Control D — Repeated Compilation

Run identical fixtures repeatedly.

Purpose:

Test deterministic output.

---

### Control E — Invalid Input

Provide deliberately malformed source.

Purpose:

Ensure failure is deterministic rather than silent recovery.

---

# 29. Negative Controls

Negative controls are essential.

The lexer should reject or explicitly classify as unsupported:

* undefined operators,
* undefined symbols,
* malformed spectral tags,
* invalid Unicode lookalikes,
* truncated multi-character operators,
* illegal identifier forms,
* malformed literals,
* unsupported normalization forms if applicable.

A negative control is successful when the invalid construct is **not silently accepted as a different valid construct**.

---

# 30. Measurements

The experiment should record measurable outcomes.

### Lexical Accuracy

```text
correctly classified tokens
/
total expected tokens
```

### Rejection Accuracy

```text
correctly rejected invalid inputs
/
total invalid inputs
```

### Ambiguity Rate

```text
ambiguous fixtures
/
total lexical fixtures
```

Target:

```text
0 unresolved ambiguities
```

for the finalized lexical specification.

### Determinism Rate

```text
identical token streams
/
repeated identical runs
```

Target:

```text
100%
```

for deterministic lexical behavior.

### Position Accuracy

Percentage of tokens whose reported source positions match the fixture ground truth.

---

# 31. Reproducibility

Every experiment run should record a reproducibility manifest.

Suggested fields:

```text
EXPERIMENT_ID
RUN_ID
FCL_VERSION
LEXER_VERSION
SOURCE_FIXTURE_VERSION
NORMALIZATION_MODE
ENCODING
PLATFORM
RUNTIME_VERSION
CONFIGURATION
INPUT_HASH
TOKEN_STREAM_HASH
ERROR_OUTPUT_HASH
TIMESTAMP
```

Where deterministic execution is expected, identical inputs and configuration should produce identical outputs.

---

# 32. Evidence Requirements

A successful implementation of this experiment should produce an evidence package containing:

```text
01-language-lexical-integrity/
├── README.md
├── fixtures/
├── expected/
├── token-streams/
├── errors/
├── manifests/
├── run-results/
└── hashes/
```

At minimum, evidence should demonstrate:

1. valid source tokenization,
2. invalid source rejection,
3. Unicode handling,
4. operator disambiguation,
5. spectral-tag handling,
6. source-position preservation,
7. deterministic repetition,
8. reproducible error behavior.

---

# 33. Acceptance Criteria

Experiment 01 may be considered **demonstrated** only when the implementation satisfies the following.

### AC-01 — Deterministic Tokenization

Identical source produces identical token streams under identical configuration.

### AC-02 — Symbol Recognition

All currently defined FCL lexical symbols are correctly recognized.

### AC-03 — Operator Recognition

Defined operators are distinguished from their component characters according to an explicit rule.

### AC-04 — Unicode Integrity

FCL Unicode symbols are handled according to an explicitly documented normalization and encoding policy.

### AC-05 — Spectral Tag Recognition

Valid spectral-layer annotations are distinguished from invalid forms.

### AC-06 — Identifier Integrity

Valid and invalid identifiers are classified consistently.

### AC-07 — Error Localization

Lexical failures identify the relevant source location and offending construct.

### AC-08 — Invalid Input Rejection

Malformed lexical constructs do not silently become unrelated valid constructs.

### AC-09 — Position Integrity

Token source positions remain correct across Unicode and multiline input.

### AC-10 — Reproducibility

The experiment can be independently rerun using the recorded fixtures and manifest.

---

# 34. Failure Conditions

The experiment fails if any of the following occur without an explicitly accepted specification rule:

* identical source produces different token streams,
* Unicode symbols are silently altered,
* visually similar Unicode symbols are incorrectly treated as equivalent,
* multi-character operators are inconsistently tokenized,
* malformed spectral tags are accepted,
* invalid operators are silently reinterpreted,
* source positions become incorrect,
* lexical errors depend on irrelevant formatting,
* comments accidentally generate executable tokens,
* undefined symbols are silently accepted,
* normalization changes lexical meaning unexpectedly,
* the lexer performs semantic interpretation,
* lexical behavior depends on hidden external state.

---

# 35. Implementation vs Specification

This experiment must preserve the distinction between the current FCL specification and the implementation that eventually emerges.

The specification may currently propose symbols such as:

```text
▲
~~
•=
~~>
✴
::
```

and spectral tags:

```text
*1–*7
```

but the experiment itself determines whether those constructs can be implemented consistently.

If implementation reveals that:

* a symbol is ambiguous,
* an operator requires a different grammar,
* Unicode normalization introduces hazards,
* a lexical construct should be changed,
* a proposed token class is unnecessary,

the specification should be revised to reflect the experimentally demonstrated system.

The implementation is therefore not required to conform blindly to an untested early specification.

Instead:

```text
SPECIFICATION
      ↓
IMPLEMENTATION
      ↓
EXPERIMENT
      ↓
EVIDENCE
      ↓
SPECIFICATION REFINEMENT
```

---

# 36. Relationship to Experiment 02

Experiment 01 establishes:

```text
SOURCE
  ↓
TOKENS
```

Experiment 02 will establish:

```text
TOKENS
  ↓
ABSTRACT SYNTAX TREE
```

Experiment 02 should not compensate for unresolved lexical ambiguity.

If Experiment 01 cannot reliably distinguish two constructs, the appropriate response is to resolve the lexical specification before treating the parser as authoritative.

---

# 37. Relationship to Later Experiments

The lexical boundary supports the entire downstream FCL pipeline:

```text
Experiment 01
Lexical Integrity
        ↓
Experiment 02
Syntax / AST
        ↓
Experiment 03
Semantic Analysis
        ↓
Experiment 04
Spectral Layer Semantics
        ↓
Experiment 05
SLIS Generation
        ↓
Experiment 06
Bytecode Integrity
        ↓
Experiment 07
FluxVM Execution
        ↓
...
        ↓
Experiment 20
End-to-End FCL / PrismChain Ecosystem
```

A failure in lexical integrity can propagate into every subsequent stage.

Therefore this experiment is intentionally narrow and foundational.

---

# 38. What This Experiment Does Not Prove

Successful lexical integrity does **not** prove:

* that FCL is semantically meaningful,
* that FCL programs are executable,
* that FluxVM exists or is correct,
* that SLIS is correct,
* that FCL maps to the seven PrismChain layers,
* that FCL produces valid White Light Blocks,
* that FCL interacts correctly with FractaChain,
* that FCL interacts correctly with Rainbow Ring,
* that Spectral Dyad can reason over FCL,
* that Fluxlings exist as autonomous agents,
* that FCL is physically encoded in light,
* that FCL provides quantum communication,
* that FCL provides quantum security,
* that FCL provides photonic execution,
* that FCL reproduces biological or cognitive spectral systems.

This experiment establishes only the lexical boundary.

---

# 39. Limitations

Several limitations are expected.

### Language Evolution

FCL is still under development. Lexical rules may change as implementation reveals better structures.

### Unicode Complexity

Unicode introduces normalization, encoding, confusable characters, and source-position challenges.

### Specification Incompleteness

Some FCL constructs remain conceptual rather than formally defined.

### No Physical Validation

The experiment operates on symbolic source code, not physical photons.

### No Execution Validation

The experiment does not execute FCL instructions.

### No PrismChain Validation

The experiment does not demonstrate PrismChain computation.

---

# 40. Evidence Interpretation

Results should be reported using the project's evidence language.

For example:

### 🟢 Demonstrated

If repeated implementation tests establish deterministic tokenization for a defined fixture set.

### 🔵 Research

If a lexical behavior has been specified but not yet implemented or experimentally demonstrated.

### 🟣 Experimental

If an implementation exists and testing is actively being conducted.

### 🟡 Hypothesis / Planned

If a lexical feature is proposed but not sufficiently defined.

### 🔴 Private

If implementation details are intentionally withheld from public documentation.

The experiment should never convert a proposed FCL feature into a demonstrated capability merely because it appears in a specification.

---

# 41. Recommended First Implementation Fixture

The first meaningful integration fixture should be the existing conceptual FCL example:

```text
▲ MintMoment(user, place, emotion):
*4: Memory Layer

if user | emotion:
    user ~~ place
    moment •= encode(user, place, emotion)
    signal ~~> @network
✴ return moment
```

The first implementation goal is **not** to execute this program.

It is to produce a deterministic token stream for it.

Conceptually:

```text
SOURCE
  ↓
LEXER
  ↓
TOKENS
  ↓
TOKEN STREAM HASH
```

The resulting token stream becomes a baseline artifact for subsequent experiments.

---

# 42. Recommended Evidence Sequence

The experiment should proceed in the following order:

```text
1. ASCII baseline
        ↓
2. FCL Unicode symbols
        ↓
3. Individual operators
        ↓
4. Multi-character operators
        ↓
5. Spectral tags
        ↓
6. Identifiers and keywords
        ↓
7. Delimiters
        ↓
8. Whitespace/newlines
        ↓
9. Unicode normalization
        ↓
10. Malformed input
        ↓
11. Ambiguity testing
        ↓
12. Full FCL fixture
        ↓
13. Repeated deterministic runs
        ↓
14. Evidence packaging
```

This progression minimizes the risk of confusing multiple lexical failures simultaneously.

---

# 43. Research Outcome

The desired outcome is not merely:

> “The lexer works.”

The desired outcome is a documented lexical contract that establishes:

```text
WHAT FCL RECOGNIZES
        +
WHAT FCL REJECTS
        +
HOW FCL REPRESENTS TOKENS
        +
HOW FCL HANDLES UNICODE
        +
HOW FCL RESOLVES AMBIGUITY
        +
HOW FCL REPORTS ERRORS
        +
HOW FCL REPRODUCES RESULTS
```

That contract becomes the foundation upon which syntax and AST construction can be tested.

---

# 44. Final Principle

> **A language cannot reason about what it cannot reliably recognize.**

Experiment 01 therefore establishes the first computational boundary of FCL:

```text
SOURCE
   ↓
LEXICAL RECOGNITION
   ↓
DETERMINISTIC TOKEN STREAM
```

Before FCL can construct syntax, assign spectral meaning, generate SLIS, execute through FluxVM, interact with PrismChain, or participate in the broader PrismChain ecosystem, it must first demonstrate that its own symbolic language can be recognized faithfully.

**The first evidence of FCL is not execution. It is lexical integrity.**
