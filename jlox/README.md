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