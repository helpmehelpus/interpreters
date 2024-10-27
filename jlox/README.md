Binding or resolution is one of the first steps in static analysis, which consists in determining what each identifier
refers to, aka their scope.

The front end of the implementation involves lexing, parsing, binding, type checking and symbol table building. It is
specific to the source language. The back end is concerned with architecture the program will run on.

Between the front end and the back end, there may be multiple Intermediate Representations (IR). Examples of IRs:
- Control flow graph (CFG)
- Static single-assignment (SSA)
- continuation-passing style
- three-address code

Common optimizations done on the back end:
- constant propagation
- common subexpression elimination
- loop invariant code motion
- global value numbering
- strength reduction
- scalar replacement of aggregates
- dead code elimination
- loop unrolling

Single-pass compilers produce code as they parse the source.

Tree-walk interpreters traverse the Abstract Syntax Tree and produce code from there. `jlox` applies this method.

Lexer:
    - Different type for each keyword, operator, bit of punctuation and literal type
    - maximal munch: "When two lexical grammar rules can both match a chunk of code that the scanner is looking at, whichever one matches the most characters wins."

Tasks after initial read:
    - Add support for C-style /* ... */ block comments. Handle newlines. Allow nesting
    - Add support for comma expressions (like C)
    - Add support for ternary operator

Representing code:
    - post-order traversal of trees is desirable because we need the numerical values of the sub-trees
    - You can think of the AST as what allows the parser and interpreter to communicate
    - Visitor design pattern: Not about "visting" or traversing. It's about using polymorphic dispatch on the subclasses
    to select the appropriate method on the visitor class. Each subclass of the main class is a "row" that has an accept()
    that routes to the correct visit method.

Parsing:
    - Play string generation from context-free grammar in reverse: given tokens, map them back to the grammar rules
    - Handling precedence: one rule for each precedence level
    - Create rules that match expressions at a given precedence level or higher
    - left-recurssion can be problematic for parsers
    - Recursive descent is a top-down, predictive parsing technique used by GCC and V8 that goes from topmost rules to the leaves
    - Bottom-up parsers like LR start with primary expressions and work their way up
    - Rules map to imperative code in recursive decent. Each rule becomes a function
    - Each method for parsing a rule produces a syntax tree and returns it
    - Synchronization is when the parser aligns its state with the forthcoming tokens after going into panic mode
    - Synchronizing on statement boundaries is common, as they are easy to spot. That's where we catch exceptions
    - Predictive parsing may not be the most adequate if we need to look ahead many tokens