# Experiment 02 — Syntax and AST Construction

**System:** Fluxling Code Language (FCL)
**Research Track:** FCL / FluxVM / PrismChain
**Experiment:** 02 of 20
**Status:** 🔵 Research — implementation not yet demonstrated
**Layer:** FCL Language Structure
**Primary Boundary:** Token Stream → Abstract Syntax Tree (AST)
**Depends On:** Experiment 01 — Language Lexical Integrity
**Feeds Into:** Experiment 03 — Semantic Analysis

---

## 1. Purpose

Experiment 02 establishes the structural foundation of the Fluxling Code Language by determining whether a valid FCL token stream can be transformed into a deterministic and structurally faithful **Abstract Syntax Tree (AST)**.

The experiment focuses on the second proposed compiler stage:

```text
FCL SOURCE
    ↓
LEXICAL ANALYSIS
    ↓
TOKEN STREAM
    ↓
SYNTAX ANALYSIS
    ↓
AST
```

Experiment 01 established the question:

> Can FCL recognize its lexical elements?

Experiment 02 asks:

> Can FCL determine how those lexical elements are structurally related?

The experiment does not determine whether the resulting program is semantically valid, executable, secure, or compatible with PrismChain.

It establishes only the syntactic structure required by later stages.

---

# 2. Central Question

> **Can valid FCL token streams be parsed into deterministic abstract syntax trees that preserve the intended structural relationships of the source while rejecting syntactically invalid or ambiguous constructions?**

This includes several subordinate questions:

1. Can FCL recognize function declarations?
2. Can function names and parameters be represented structurally?
3. Can spectral-layer annotations be attached to the appropriate syntactic construct?
4. Can conditional expressions be represented deterministically?
5. Can nested statements be represented without structural ambiguity?
6. Can FCL operators be placed into the correct AST relationships?
7. Can return statements be represented correctly?
8. Can malformed nesting be rejected?
9. Can equivalent source formatting produce equivalent ASTs where the grammar defines them as equivalent?
10. Can syntactically distinct programs be distinguished reliably?

---

# 3. Scientific Position

FCL currently contains a proposed language specification rather than a finalized compiler implementation.

Therefore this experiment must distinguish:

* lexical structure,
* syntactic structure,
* semantic interpretation,
* execution behavior.

A parser may determine that:

```text
user ~~ place
```

is syntactically valid without determining what `~~` means operationally.

Likewise, an AST node may contain:

```text
spectral_layer: 4
```

without establishing what Layer 4 means semantically.

Those questions belong to later experiments.

---

# 4. System Under Test

The proposed system boundary is:

```text
             TOKEN STREAM
                  │
                  ▼
        ┌──────────────────┐
        │    FCL PARSER    │
        │                  │
        │ Grammar rules    │
        │ Precedence       │
        │ Nesting          │
        │ Statements       │
        │ Expressions      │
        │ Declarations     │
        └────────┬─────────┘
                 │
                 ▼
                AST
                 │
                 ▼
       Experiment 03
       Semantic Analysis
```

The parser should consume tokens and produce either:

```text
VALID TOKEN STREAM
        ↓
       AST
```

or:

```text
INVALID TOKEN STREAM
        ↓
SYNTAX ERROR
```

It should not silently reinterpret invalid syntax as valid syntax.

---

# 5. Proposed AST

The FCL compiler specification provides a conceptual AST structure similar to:

```yaml
Function:
  name: MintMoment
  spectral_layer: 4
  body:
    - if_condition: user | emotion
      then:
        - bind: [user, place]
        - memory_mint: moment = encode(user, place, emotion)
        - signal_emit: signal to @network
    - return: moment
```

This is an initial conceptual representation.

It should **not** yet be treated as an immutable implementation contract.

The actual parser may produce a richer or structurally different AST if experimentation demonstrates that the alternative is more precise.

---

# 6. Syntax Boundary

Experiment 02 establishes:

```text
TOKENS
  ↓
GRAMMATICAL STRUCTURE
```

It does not establish:

```text
GRAMMATICAL STRUCTURE
  ↓
MEANING
```

Therefore the following distinctions are essential.

### Syntax ≠ Semantics

A parser determines whether something conforms to grammar.

A semantic analyzer determines whether that structure is meaningful under FCL's rules.

---

### AST ≠ Bytecode

The AST represents source structure.

SLIS represents a later intermediate instruction representation.

---

### AST ≠ Execution

A valid AST does not mean the program can execute.

---

### AST ≠ PrismChain Computation

A valid FCL program does not automatically become a PrismChain computation.

---

### AST ≠ Physical Light

A spectral annotation in an AST is a symbolic program construct, not proof of physical spectral encoding.

---

# 7. Hypothesis

### Primary Hypothesis

> **A formally defined FCL grammar can transform valid token streams into deterministic ASTs that preserve declaration structure, nesting, operator relationships, spectral context, and statement ordering while rejecting syntactically invalid constructs.**

### Secondary Hypotheses

1. FCL function declarations can be represented deterministically.
2. Parameters can be associated with their declarations.
3. Conditional structures can be represented without ambiguity.
4. Nested statements preserve source ordering.
5. Operators retain their syntactic relationships.
6. Spectral-layer annotations can be attached to the correct syntactic scope.
7. Equivalent formatting produces structurally equivalent ASTs when permitted by the grammar.
8. Invalid nesting is detected rather than silently repaired.

---

# 8. Proposed Grammar Domains

The experiment should investigate at least these structural categories:

```text
PROGRAM
FUNCTION
PARAMETER_LIST
BLOCK
STATEMENT
EXPRESSION
CONDITION
BINDING
ASSIGNMENT
MEMORY_OPERATION
SIGNAL_OPERATION
RETURN
SPECTRAL_CONTEXT
LITERAL
IDENTIFIER
```

These are experimental categories.

The final grammar may consolidate, split, or rename them.

---

# 9. Function Declaration Tests

The conceptual FCL syntax includes:

```text
▲ MintMoment(user, place, emotion):
```

The parser should determine whether this represents:

```text
FUNCTION
 ├── NAME
 │    └── MintMoment
 ├── PARAMETERS
 │    ├── user
 │    ├── place
 │    └── emotion
 └── BODY
```

Test variations should include:

```text
▲ MintMoment():
▲ MintMoment(user):
▲ MintMoment(user, place):
▲ MintMoment(user, place, emotion):
```

and malformed forms such as:

```text
▲
▲ MintMoment(
▲ MintMoment(user
▲ MintMoment(user,)
▲ MintMoment(,user)
```

The parser must distinguish valid grammar from malformed structure.

---

# 10. Function Name Tests

Test:

```text
▲ MintMoment():
▲ mintMoment():
▲ MINTMOMENT():
▲ Mint_Moment():
```

where each form is either accepted or rejected according to the defined identifier grammar.

The experiment should not assume case sensitivity without specification.

---

# 11. Parameter Structure

Parameters should be tested for:

* zero parameters,
* one parameter,
* multiple parameters,
* duplicate parameters,
* malformed separators,
* missing delimiters,
* invalid identifiers,
* nested or unexpected expressions.

For example:

```text
MintMoment(user, place, emotion)
```

should preserve:

```text
[
  user,
  place,
  emotion
]
```

in source order.

Whether duplicate parameters are syntactically valid or semantically invalid must be explicitly distinguished.

---

# 12. Block Construction

FCL requires a deterministic representation of statement grouping.

The parser should test:

```text
function:
    statement
    statement
    statement
```

against malformed structures such as:

```text
function:
statement
    statement
```

if indentation is syntactically meaningful.

If FCL ultimately uses explicit delimiters rather than indentation, that must instead be reflected in the grammar.

The experiment should determine the actual structural mechanism rather than assuming one.

---

# 13. Indentation and Whitespace

Because the current conceptual FCL examples use indentation, indentation must be experimentally investigated.

Questions include:

* Is indentation syntactically meaningful?
* Is indentation merely formatting?
* Are blocks determined by indentation level?
* Are tabs allowed?
* Are spaces required?
* Are mixed tabs/spaces rejected?
* Does inconsistent indentation produce syntax errors?

Example:

```text
if user | emotion:
    user ~~ place
    moment •= encode(user, place, emotion)
```

must have a deterministic block representation.

If indentation is not ultimately part of FCL syntax, that conclusion should be explicitly documented.

---

# 14. Conditional Structure

The current conceptual syntax includes:

```text
if user | emotion:
```

The parser should determine the structural relationship:

```text
IF
├── CONDITION
│   └── user | emotion
└── BODY
    ├── ...
    └── ...
```

Tests should include:

```text
if user:
if emotion:
if user | emotion:
if user | emotion | place:
```

and malformed forms:

```text
if:
if user |:
if | emotion:
if (user:
if user):
```

The parser should distinguish syntax errors from later semantic errors.

---

# 15. Operator Precedence

FCL's symbolic operators may eventually participate in expressions.

The experiment must determine whether operators such as:

```text
|
~~
•=
~~>
```

have defined precedence or associativity.

For example:

```text
a | b ~~ c
```

could potentially admit multiple structural interpretations.

The parser must not choose an interpretation arbitrarily.

The experiment should establish:

```text
OPERATOR PRECEDENCE
+
ASSOCIATIVITY
+
GROUPING RULES
```

for every operator that participates in expressions.

If precedence remains unresolved, the grammar must mark the construct as unresolved rather than silently selecting one interpretation.

---

# 16. Explicit Grouping

If FCL permits grouping constructs, test:

```text
(a | b)
(a ~~ b)
(a | b) ~~ c
a | (b ~~ c)
```

The resulting ASTs should preserve explicit grouping.

For example:

```text
(a | b) ~~ c
```

must not be structurally identical to:

```text
a | (b ~~ c)
```

unless the grammar explicitly establishes equivalence.

---

# 17. Binding Structure

The conceptual FCL example contains:

```text
user ~~ place
```

The parser should represent the relationship without prematurely deciding its semantic meaning.

Conceptually:

```yaml
Bind:
  left: user
  right: place
```

The actual node name is implementation-dependent.

The important property is that the AST preserves the operator and its operands.

---

# 18. Assignment / Memory Structure

The example contains:

```text
moment •= encode(user, place, emotion)
```

The parser should determine whether this represents a syntactic assignment-like structure:

```text
Assignment
├── Target
│   └── moment
└── Expression
    └── encode(...)
```

The parser must not yet decide whether `•=` means:

* memory minting,
* state mutation,
* accumulation,
* spectral operation,
* or another semantic action.

That belongs to semantic analysis.

---

# 19. Function Call Structure

The parser should recognize structures such as:

```text
encode(user, place, emotion)
```

as an expression with:

```text
CALL
├── FUNCTION
│   └── encode
└── ARGUMENTS
    ├── user
    ├── place
    └── emotion
```

Tests should include:

```text
encode()
encode(user)
encode(user, place)
encode(user, place, emotion)
```

and malformed calls.

---

# 20. Signal Structure

The example contains:

```text
signal ~~> @network
```

The parser should preserve:

```text
LEFT OPERAND
OPERATOR
RIGHT OPERAND
```

without assuming that `~~>` necessarily performs network transmission.

A conceptual AST could be:

```yaml
SignalOperation:
  source: signal
  target: "@network"
```

but this is only one possible representation.

The semantic interpretation belongs to Experiment 03 and later experiments.

---

# 21. Return Structure

The example ends with:

```text
✴ return moment
```

The parser should establish the relationship between the symbolic prefix and the return statement.

Potential structure:

```text
RETURN
└── moment
```

with the symbolic marker represented separately if the grammar requires it.

The parser must not assume that `✴` itself means execution, synchronization, or a physical spectral event.

---

# 22. Spectral Context

The conceptual syntax contains:

```text
*4: Memory Layer
```

Experiment 02 should determine its syntactic structure.

Possible conceptual representation:

```yaml
SpectralContext:
  layer: 4
  annotation: "Memory Layer"
```

The parser should determine whether the context applies to:

* the following statement,
* the following block,
* the function,
* the current scope,
* or another syntactic region.

That relationship must be established by grammar.

Its semantic meaning belongs to Experiment 04.

---

# 23. Nested Structure

FCL must be tested with nested structures.

Example:

```text
function:
    if condition:
        operation
        operation
    return value
```

The AST must preserve:

```text
FUNCTION
└── BODY
    ├── IF
    │   └── BODY
    │       ├── OPERATION
    │       └── OPERATION
    └── RETURN
```

A parser failure that flattens or misorders nested structures is a structural integrity failure.

---

# 24. Statement Ordering

The AST must preserve source order where order is syntactically meaningful.

For:

```text
a
b
c
```

the parser should not produce:

```text
b
a
c
```

or another reordered representation.

This becomes particularly important later when FCL instructions are compiled into SLIS.

---

# 25. Empty Structures

Test:

```text
▲ Empty():
```

with an empty body.

Also test:

```text
if condition:
```

with no body where the grammar would otherwise require one.

The parser should either:

* represent the empty structure explicitly if legal,
* or reject it deterministically.

---

# 26. Syntax Error Recovery

A parser may eventually implement error recovery for developer usability.

However, recovery must not conceal invalid syntax.

For example:

```text
▲ MintMoment(user place):
```

should not silently become:

```text
▲ MintMoment(user, place):
```

unless automatic correction is explicitly outside the parser and clearly reported.

The experiment should distinguish:

```text
ERROR DETECTION
```

from:

```text
ERROR RECOVERY
```

and:

```text
AUTOMATIC CORRECTION
```

These are not equivalent behaviors.

---

# 27. AST Canonicalization

A canonical AST representation should be developed so that structurally equivalent programs can be compared.

Example conceptual representation:

```json
{
  "type": "Function",
  "name": "MintMoment",
  "parameters": [
    "user",
    "place",
    "emotion"
  ],
  "body": []
}
```

This is illustrative rather than a locked schema.

The final AST representation should emerge from implementation and testing.

---

# 28. Formatting Equivalence

If the grammar allows formatting differences, test:

```text
encode(user,place,emotion)
```

and:

```text
encode(user, place, emotion)
```

If both are valid and semantically equivalent, their AST structures should be equivalent.

Likewise, formatting-only differences should not create artificial semantic distinctions.

However, if whitespace or indentation is syntactically meaningful, the parser must preserve those distinctions.

---

# 29. Structural Non-Equivalence

The parser must also demonstrate that structurally different programs remain distinguishable.

For example:

```text
a | (b ~~ c)
```

must remain structurally distinct from:

```text
(a | b) ~~ c
```

when the grammar assigns different structures.

This test prevents over-aggressive AST normalization.

---

# 30. Round-Trip Testing

Where an FCL pretty-printer or source serializer exists, the experiment should investigate:

```text
SOURCE
 ↓
TOKENS
 ↓
AST
 ↓
CANONICAL SOURCE
```

The reconstructed source should parse into an equivalent AST.

Conceptually:

```text
AST₁
=
PARSE(PRINT(AST₁))
```

This does not require byte-for-byte source equality.

The important property is structural equivalence.

---

# 31. AST Stability Under Formatting

Test multiple source representations that differ only in permitted formatting:

```text
SOURCE A
SOURCE B
SOURCE C
```

Then compare:

```text
AST(A)
AST(B)
AST(C)
```

If the grammar considers the representations equivalent:

```text
AST(A) = AST(B) = AST(C)
```

If the grammar considers them distinct:

```text
AST(A) ≠ AST(B)
```

The result must follow explicit grammar rules.

---

# 32. Invalid Syntax Corpus

The experiment should establish an invalid syntax corpus.

Suggested categories:

```text
invalid/
├── missing-delimiter/
├── missing-operand/
├── malformed-function/
├── malformed-parameter-list/
├── malformed-condition/
├── malformed-block/
├── malformed-nesting/
├── invalid-spectral-context/
├── invalid-return/
├── invalid-expression/
└── ambiguous-grammar/
```

Each fixture should have an expected parser result.

---

# 33. Ambiguous Grammar Tests

The parser must explicitly test grammar ambiguity.

Examples include:

```text
a | b | c
```

```text
a ~~ b ~~ c
```

```text
a ~~> b ~~> c
```

```text
if a | b:
```

The purpose is to determine whether the grammar provides:

* precedence,
* associativity,
* explicit grouping,
* contextual disambiguation,
* or rejection.

An unresolved ambiguity should never be hidden by the implementation.

---

# 34. AST Integrity Tests

The resulting AST should be tested for:

### Node completeness

Every syntactically meaningful source construct appears in the AST.

### Node ordering

Statements preserve required source order.

### Parent-child integrity

Nested constructs have correct parent-child relationships.

### Operator integrity

Operators remain associated with their operands.

### Scope integrity

Nested blocks remain inside their intended syntactic scopes.

### Spectral-context integrity

Spectral annotations remain associated with their defined syntactic region.

### Identifier integrity

Identifier names are preserved exactly according to language rules.

---

# 35. Controls

### Control A — Simple Function

```text
▲ Test():
```

Purpose:

Establish minimum function structure.

### Control B — Function With Parameters

```text
▲ Test(a, b):
```

Purpose:

Test parameter parsing.

### Control C — Simple Expression

```text
a ~~ b
```

Purpose:

Test basic expression structure.

### Control D — Nested Structure

```text
if condition:
    a ~~ b
```

Purpose:

Test hierarchical AST construction.

### Control E — Full Conceptual Fixture

Use the current `MintMoment` example.

Purpose:

Test combined grammar behavior.

---

# 36. Negative Controls

Negative controls should include:

```text
▲
▲ Test(
▲ Test(a,
▲ Test(,a):
if:
if a |:
a ~~>
a •=
return
```

and other malformed constructs discovered during implementation.

A negative control succeeds when invalid syntax is rejected or explicitly classified according to a documented grammar rule.

---

# 37. Measurements

### Parse Success Rate

```text
valid fixtures correctly parsed
/
total valid fixtures
```

### Syntax Rejection Rate

```text
invalid fixtures correctly rejected
/
total invalid fixtures
```

### AST Fidelity

Percentage of expected structural relationships correctly represented.

### Determinism

```text
identical parse results
/
repeated identical parses
```

Target for deterministic parsing:

```text
100%
```

### Error Localization

Percentage of syntax errors whose reported locations correspond to the expected malformed construct.

---

# 38. Reproducibility Manifest

Each parser run should record:

```text
EXPERIMENT_ID
RUN_ID
FCL_VERSION
LEXER_VERSION
PARSER_VERSION
GRAMMAR_VERSION
SOURCE_FIXTURE_VERSION
NORMALIZATION_MODE
INPUT_HASH
TOKEN_STREAM_HASH
AST_HASH
ERROR_OUTPUT_HASH
RUNTIME_VERSION
PLATFORM
CONFIGURATION
TIMESTAMP
```

This allows AST results to be reproduced after implementation changes.

---

# 39. Evidence Package

A completed experiment should produce evidence similar to:

```text
02-syntax-and-ast-construction/
├── README.md
├── grammar/
├── fixtures/
│   ├── valid/
│   └── invalid/
├── token-inputs/
├── ast-outputs/
├── expected/
├── errors/
├── manifests/
├── comparisons/
└── hashes/
```

The evidence package should make it possible to independently determine:

```text
SOURCE
  ↓
TOKENS
  ↓
AST
```

without relying on undocumented parser behavior.

---

# 40. Acceptance Criteria

Experiment 02 may be considered **demonstrated** when:

### AC-01 — Deterministic Parsing

Identical token streams produce identical ASTs under identical configuration.

### AC-02 — Valid Syntax Recognition

Defined valid FCL constructs parse successfully.

### AC-03 — Invalid Syntax Rejection

Malformed constructs are rejected deterministically.

### AC-04 — Structural Fidelity

The AST preserves the intended hierarchy of the source program.

### AC-05 — Ordering Integrity

Syntactically ordered statements remain ordered.

### AC-06 — Operator Integrity

Operators remain structurally associated with their correct operands.

### AC-07 — Scope Integrity

Nested structures remain within the correct syntactic scope.

### AC-08 — Spectral Context Integrity

Defined spectral annotations attach to the correct syntactic construct.

### AC-09 — Error Localization

Syntax errors can be traced to the relevant source location.

### AC-10 — Reproducibility

The experiment can be independently repeated from its versioned fixtures and manifests.

---

# 41. Failure Conditions

The experiment fails if:

* identical token streams produce different ASTs,
* valid structures are silently discarded,
* source ordering is corrupted,
* nested structures are flattened incorrectly,
* operators are attached to incorrect operands,
* malformed syntax is silently repaired,
* grammar ambiguity is resolved without an explicit rule,
* spectral annotations attach to unintended scopes,
* parser behavior depends on undocumented external state,
* semantic meaning is silently embedded into syntax parsing,
* AST generation changes because of irrelevant formatting when formatting is not syntactically meaningful.

---

# 42. Implementation vs Specification

The current conceptual AST is not a permanent implementation contract.

The implementation may reveal that a better AST requires:

* additional nodes,
* fewer nodes,
* explicit operator nodes,
* explicit scope nodes,
* separate annotation nodes,
* richer source metadata,
* different spectral-context representation,
* different expression structures.

Those changes should be accepted when supported by evidence.

The correct development loop is:

```text
PROPOSED GRAMMAR
       ↓
PARSER IMPLEMENTATION
       ↓
STRUCTURAL TESTS
       ↓
EVIDENCE
       ↓
GRAMMAR REFINEMENT
       ↓
AST SPECIFICATION
```

The specification should eventually describe the implementation that survives experimentation.

---

# 43. Relationship to Experiment 01

Experiment 01 establishes:

```text
FCL SOURCE
    ↓
TOKEN STREAM
```

Experiment 02 begins with that token stream.

Therefore Experiment 02 should not silently compensate for unresolved lexical problems.

If the parser discovers that:

```text
~~>
```

can be tokenized in multiple incompatible ways, the issue belongs at the lexical boundary and should be returned to Experiment 01.

The two experiments therefore form a controlled chain:

```text
LEXICAL INTEGRITY
        ↓
SYNTAX INTEGRITY
```

---

# 44. Relationship to Experiment 03

Experiment 03 will establish:

```text
AST
 ↓
SEMANTIC ANALYSIS
```

The parser should therefore avoid making semantic decisions prematurely.

For example, the parser may recognize:

```text
moment •= encode(...)
```

as an AST operation.

It should not decide that `•=` necessarily means:

> mint memory

unless that meaning is part of syntax itself, which should be explicitly justified.

Semantic interpretation belongs to Experiment 03.

---

# 45. Relationship to Later FCL Experiments

The dependency chain is:

```text
01 — Lexical Integrity
          ↓
02 — Syntax / AST
          ↓
03 — Semantic Analysis
          ↓
04 — Spectral Layer Semantics
          ↓
05 — SLIS Generation
          ↓
06 — Bytecode Integrity
          ↓
07 — FluxVM Execution
          ↓
08 — Register / State Integrity
          ↓
09 — Control Flow
          ↓
10 — Memory Operations
          ↓
11 — Signal Operations
          ↓
12 — Reproducibility
          ↓
13 — PrismChain Execution
          ↓
...
```

Experiment 02 therefore represents the structural bridge between FCL's source language and its future executable representation.

---

# 46. What This Experiment Does Not Prove

A successful AST parser does **not** prove:

* that FCL semantics are correct,
* that FCL programs execute,
* that FluxVM exists,
* that FluxVM executes correctly,
* that SLIS generation is correct,
* that FCL maps correctly to PrismChain's seven layers,
* that FCL produces White Light Blocks,
* that FCL interacts with FractaChain,
* that FCL interacts with Rainbow Ring,
* that Spectral Dyad can reason over FCL,
* that Fluxlings are autonomous agents,
* that FCL is physically encoded in light,
* that FCL is a quantum communication protocol,
* that FCL provides quantum security,
* that FCL performs photonic computation.

It establishes only syntactic structural integrity.

---

# 47. Limitations

### Evolving Grammar

FCL remains an experimental language. Grammar decisions may change.

### Incomplete Semantic Specification

Some syntactic constructs currently have only proposed meanings.

### Unicode Complexity

Lexical normalization remains an upstream dependency.

### No Execution

The AST is not executed during this experiment.

### No Physical Layer

No physical optical or photonic behavior is tested.

### No PrismChain Layer

No PrismChain computation is required for this experiment.

---

# 48. Recommended First Implementation Fixture

The primary fixture should remain:

```text
▲ MintMoment(user, place, emotion):
*4: Memory Layer

if user | emotion:
    user ~~ place
    moment •= encode(user, place, emotion)
    signal ~~> @network
✴ return moment
```

The implementation target is:

```text
FCL SOURCE
    ↓
LEXER
    ↓
TOKEN STREAM
    ↓
PARSER
    ↓
AST
```

The first result should be a versioned AST artifact.

No execution is required.

---

# 49. Recommended Evidence Sequence

Proceed in increasing structural complexity:

```text
1. Empty program
        ↓
2. Single identifier
        ↓
3. Single expression
        ↓
4. Simple function
        ↓
5. Function parameters
        ↓
6. Simple block
        ↓
7. Conditional
        ↓
8. Nested conditional
        ↓
9. Function calls
        ↓
10. Binding / assignment
        ↓
11. Signal operation
        ↓
12. Return
        ↓
13. Spectral context
        ↓
14. Nested combined program
        ↓
15. Invalid syntax corpus
        ↓
16. Ambiguous grammar corpus
        ↓
17. Full MintMoment fixture
        ↓
18. Deterministic repeated parsing
```

This sequence makes structural failures easier to isolate.

---

# 50. Research Outcome

The desired outcome is not simply:

> “The parser works.”

The desired outcome is a defensible structural contract describing:

```text
WHAT CONSTITUTES A VALID FCL PROGRAM
              +
HOW TOKENS ARE STRUCTURED
              +
HOW NESTING IS REPRESENTED
              +
HOW OPERATORS RELATE TO OPERANDS
              +
HOW FUNCTIONS AND BLOCKS ARE REPRESENTED
              +
HOW SPECTRAL CONTEXT IS ATTACHED
              +
HOW INVALID STRUCTURE IS REJECTED
              +
HOW AST RESULTS ARE REPRODUCED
```

That contract becomes the foundation for semantic analysis.

---

# 51. Final Principle

> **A language becomes structurally meaningful when its symbols can be assembled into an unambiguous representation of relationships.**

Experiment 01 established that FCL must reliably recognize its symbols.

Experiment 02 establishes the next boundary:

```text
TOKENS
   ↓
STRUCTURE
   ↓
AST
```

Only after that structural representation is reliable should FCL attempt to determine what those structures mean.

**The second evidence of FCL is not execution. It is structural integrity.**
