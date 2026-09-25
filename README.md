# Loom

Loom is a small, C-family imperative language for short, straightforward
procedural programs. It favors a minimal keyword set, brace-delimited
blocks, and semicolon-terminated statements, keeping the grammar easy to
parse without sacrificing readability.

This repository holds the design and, starting in Part 2, the
implementation of Loom.

## Team

- [Name 1] — Grammar & language design lead
- [Name 2] — Core language features (arithmetic, expressions, variables, print)
- [Name 3] — Control flow and functions (if/else, while, functions, scope)
- [Name 4] — Sample programs, testing, documentation, extension feature (arrays)

*Replace the bracketed names with your actual names/GitHub usernames before
your first commit.*

## Status

- **Part 1 — Language Design & Grammar:** done. Full write-up in
  [`design/loom-part1-design.md`](design/loom-part1-design.md).
- **Part 2 onward:** implementation starts in [`src/`](src/).

## Repository layout

```
.
├── design/     Design documents (Part 1 and later write-ups)
├── src/        Interpreter/compiler source (Part 2+)
├── tests/      Test programs and expected output
└── examples/   Sample Loom programs (.loom files)
```

## A taste of Loom

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

More sample programs live in [`examples/`](examples/).

## AI use

AI tools (Claude, Anthropic) were used during the design phase to help
brainstorm language features, draft the grammar, and write sample
programs — all reviewed and approved by the group. See the AI Use
Statement in the design document for details.
