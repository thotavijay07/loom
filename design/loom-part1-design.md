# Final Project – Part 1: Language Design & Grammar

**Language: Loom**

*Group Members: [Add group member names here]*

## 1. Language Name and Description

Loom is a small, C-family imperative language for short, straightforward
procedural programs. The name comes from how a program comes together:
statements like declarations, expressions, conditionals, and loops get
woven together in sequence to form the finished program. We kept the
keyword set small and stuck with brace-delimited blocks and
semicolon-terminated statements, mainly so the grammar would stay easy to
parse without making the code harder to read.

## 2. List of Keywords

Loom reserves the following nine keywords. Reserved words cannot be used
as identifiers.

- `let` — declares and initializes a variable
- `if` — begins a conditional statement
- `else` — begins the alternate branch of a conditional
- `while` — begins a loop
- `func` — defines a function
- `return` — returns a value from a function
- `print` — outputs the value of an expression
- `true` — boolean literal
- `false` — boolean literal

## 3. Operators and Delimiters

**Arithmetic operators**

| Op | Meaning |
|----|---------|
| `+` | addition |
| `-` | subtraction (also unary negation) |
| `*` | multiplication |
| `/` | division |

**Comparison operators**

| Op | Meaning |
|----|---------|
| `==` | equal to |
| `!=` | not equal to |
| `<`  | less than |
| `>`  | greater than |
| `<=` | less than or equal to |
| `>=` | greater than or equal to |

**Assignment operator**

| Op | Meaning |
|----|---------|
| `=` | assigns the value on the right to the variable on the left |

**Delimiters**

| Delim | Meaning |
|-------|---------|
| `( )` | group expressions and enclose function parameters/arguments |
| `{ }` | enclose statement blocks |
| `;`   | terminates a statement |
| `,`   | separates parameters and arguments |

**Comments**

`//` starts a single-line comment; everything to the end of the line is
ignored by the parser.

## 4. Variable Declaration and Assignment Syntax

A variable is declared with `let` and an initializer. Once declared, it
can be reassigned without `let`:

```
let x = 10;           // declaration
x = x + 1;             // reassignment (no "let")
let isReady = true;    // boolean value
```

Loom is dynamically typed at this stage: a variable's type is determined
by the value it currently holds (number or boolean).

## 5. Control-Structure Syntax

**if / else**

```
if (x < y) {
    print(x);
} else {
    print(y);
}
```

**while**

```
while (i < 10) {
    i = i + 1;
}
```

## 6. Function Syntax

Functions are declared with `func`, take zero or more comma-separated
parameters, and return a value with `return`. Variables declared inside a
function, including its parameters, are local to that function. That's
Loom's scope rule for now: nothing declared inside a function is visible
outside it.

```
func add(a, b) {
    let result = a + b;
    return result;
}

let total = add(3, 4);   // total = 7; "result" above is not visible here
```

## 7. Sample Programs

**Program 1 — Arithmetic and if/else**

```
let x = 10;
let y = 20;
if (x < y) {
    print(x + y);
} else {
    print(x - y);
}
// Output: 30
```

**Program 2 — while loop**

```
let i = 0;
let sum = 0;
while (i < 5) {
    sum = sum + i;
    i = i + 1;
}
print(sum);
// Output: 10
```

**Program 3 — Function with parameters, return value, and scope**

```
func square(n) {
    let result = n * n;
    return result;
}

let value = 6;
let squared = square(value);
print(squared);
// Output: 36
```

## 8. Initial BNF/EBNF Grammar

Notation: `{ X }` means zero or more repetitions of X, `[ X ]` means X is
optional, and `|` separates alternatives, following standard EBNF
conventions.

```ebnf
<program>              ::= { <statement> }
<statement>            ::= <assignment>
                          | <print-statement>
                          | <if-statement>
                          | <while-statement>
                          | <function-definition>
                          | <return-statement>
                          | <function-call> ";"

<assignment>           ::= [ "let" ] <identifier> "=" <expression> ";"

<expression>           ::= <simple-expression> [ <relop> <simple-expression> ]
<relop>                ::= "==" | "!=" | "<" | ">" | "<=" | ">="
<simple-expression>    ::= <term> { ( "+" | "-" ) <term> }
<term>                 ::= <factor> { ( "*" | "/" ) <factor> }
<factor>               ::= <number>
                          | <identifier>
                          | <function-call>
                          | "(" <expression> ")"
                          | "-" <factor>
                          | <boolean-literal>

<boolean-literal>      ::= "true" | "false"

<print-statement>      ::= "print" "(" <expression> ")" ";"

<if-statement>          ::= "if" "(" <expression> ")" "{" { <statement> } "}"
                          [ "else" "{" { <statement> } "}" ]

<while-statement>       ::= "while" "(" <expression> ")" "{" { <statement> } "}"

<function-definition>   ::= "func" <identifier> "(" [ <parameter-list> ] ")"
                          "{" { <statement> } "}"

<parameter-list>        ::= <identifier> { "," <identifier> }

<function-call>         ::= <identifier> "(" [ <argument-list> ] ")"
<argument-list>         ::= <expression> { "," <expression> }
<return-statement>      ::= "return" [ <expression> ] ";"

<identifier>             ::= <letter> { <letter> | <digit> | "_" }
<number>                 ::= <digit> { <digit> } [ "." <digit> { <digit> } ]
<letter>                 ::= "a" | ... | "z" | "A" | ... | "Z"
<digit>                  ::= "0" | "1" | ... | "9"
```

## 9. Proposed Additional / Extension Feature

**Chosen feature: Arrays.** Loom will be extended to support fixed-size,
zero-indexed arrays of numbers, including literal creation, indexed
access, and indexed assignment:

```
let nums = [1, 2, 3, 4];
print(nums[0]);       // 1
nums[1] = 10;          // update in place
print(nums[1]);        // 10
```

This will require two grammar additions once implementation begins:

```ebnf
<array-literal>   ::= "[" [ <expression> { "," <expression> } ] "]"
<array-access>    ::= <identifier> "[" <expression> "]"
```

`<factor>` will be extended to include `<array-access>` and
`<array-literal>`, and `<assignment>` will be extended to allow an
`<array-access>` as its target. We chose arrays because they let sample
programs demonstrate iteration over structured data (e.g., summing an
array with a while loop) without adding new keywords.

## 10. Initial Responsibilities of Each Group Member

*Roles below are our initial division of labor for the design phase and
the start of implementation; we expect responsibilities to shift as the
six-week project progresses.*

| Group Member | Initial Responsibility |
|---|---|
| [Name 1] | Grammar & language design lead — owns the BNF/EBNF grammar and keeps syntax consistent across features |
| [Name 2] | Core language features — arithmetic, expressions, variables, and print statements |
| [Name 3] | Control flow and functions — if/else, while, function definitions/calls, and scope |
| [Name 4] | Sample programs, testing, documentation, GitHub repository setup, and the extension feature (arrays) |

*Replace the bracketed names above with actual group members before
submitting; add or remove rows to match your group size.*

## 11. GitHub Repository

You're in it. All group members have been added as collaborators, and
commit history reflects each person's contributions.

## 12. AI Use Statement

Claude (Anthropic) was used during the design phase to help brainstorm
language features, draft the initial BNF/EBNF grammar, write the sample
programs, and organize this document into the format required by the
assignment. All AI-assisted content was reviewed, tested by hand-tracing
the sample programs against the grammar, and approved by the group before
submission. Final decisions about the language's design — including its
name, keyword set, and chosen extension feature — were made by the group.
