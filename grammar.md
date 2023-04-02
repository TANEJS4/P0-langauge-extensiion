### The P0 Grammar
The original P0 Grammar, for reference.
```
selector ::= { "[" expression "]" | "." ident}
factor ::= ident selector | integer | "(" expression ")" | "{" [expression {"," expression}] "}" | ("¬" | "#" | "∁") factor
term ::= factor {("×" | "div" | "mod" | "∩" | "and") factor}
simpleExpression ::= ["+" | "-"] term {("+" | "-" | "∪" | "or") term}
expression ::= simpleExpression
    {("=" | "≠" | "<" | "≤" | ">" | "≥" | "∈" | "⊆" | "⊇") simpleExpression}
statementList ::= statement {";" statement}
statementBlock ::= statementList {statementList}
statementSuite ::= statementList | INDENT statementBlock DEDENT
statement ::=
    ident selector ":=" expression |
    ident {"," ident} (":=" expression {"," expression} |
        "←" ident "(" [expression {"," expression}] ")") |
    "if" expression "then" statementSuite ["else" statementSuite] |
    "while" expression "do" statementSuite
type ::=
    ident |
    "[" expression ".." expression "]" "→" type |
    "(" typedIds ")" |
    "set" "[" expression ".." expression "]"
typedIds ::= ident ":" type {"," ident ":" type}
declarations ::= 
    {"const" ident "=" expression}
    {"type" ident "=" type}
    {"var" typedIds}
    {"procedure" ident "(" [typedIds] ")" [ "→" "(" typedIds ")" ] body}
body ::= INDENT declarations (statementBlock | INDENT statementBlock DEDENT) DEDENT
program ::= declarations "program" ident body
```

### Adding Simple Predicates
Simple predicates are expressions combined with conjunctions (`∧`) and disjunctions (`∨`).

```
simplePredicate ::= expression {(∧ | ∨) (expression | simplePredicate)}
```

### Adding Preconditions, Postconditions, Invariants
#### Invariant
Add an optional clause in `statement` before the loop construct.
```
statement ::=
    ident selector ":=" expression |
    ident {"," ident} (":=" expression {"," expression} |
        "←" ident "(" [expression {"," expression}] ")") |
    "if" expression "then" statementSuite ["else" statementSuite] |
    {"invariant" expression} "while" expression "do" statementSuite
```

#### Precondition, Postcondition
We add two more options to `statement`.
```
statement ::=
    ident selector ":=" expression |
    ident {"," ident} (":=" expression {"," expression} |
        "←" ident "(" [expression {"," expression}] ")") |
    "if" expression "then" statementSuite ["else" statementSuite] |
    {"invariant" expression} "while" expression "do" statementSuite |
    "ensure" expression |
    "require" expression
```