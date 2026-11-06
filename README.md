# Logo Interpreter in OCaml

An interpreter for a French-keyword dialect of the **Logo** language, written in OCaml. It covers the full pipeline: lexical analysis with `ocamllex`, parsing into an abstract syntax tree with `ocamlyacc`, and recursive evaluation that drives a "turtle" across a 2D plane.

University project, 2nd year BSc Computer Science (L2), University of Poitiers, *Introduction to Programming Language Theory* (ITLP) course, 2025–26.

## Features

- **Lexer** ([`logo_lexer.mll`](src/logo_lexer.mll)): signed integers, identifiers, keywords, `--` line comments, and errors for unrecognized characters.
- **Parser** ([`logo_parser.mly`](src/logo_parser.mly)): LALR grammar producing a typed AST, with left-associative sequencing (`;`).
- **Interpreter** ([`logo_ast.ml`](src/logo_ast.ml)): purely functional evaluation over an immutable state (environment + turtle).
  - Arithmetic expressions `+ - * /`, with a division-by-zero check
  - Variables (`Def x 10`, read with `:x`)
  - Loops (`Repete n [ ... ]`), implemented with a tail-recursive `iterate`
  - Conditionals (`Si (cond) Alors ... Sinon ... FinSi`) with `=`, `<`, `>`
- **REPL** ([`repl_logo.ml`](src/repl_logo.ml)): an interactive loop that prints the turtle state and environment after each program and recovers from lexical and syntax errors.

## Language reference

| Logo keyword | Meaning |
|---|---|
| `Avance e` / `Recule e` | Move forward / backward by `e` |
| `Gauche e` / `Droite e` | Turn left / right by `e` degrees |
| `Dessine` / `Deplace` | Pen down / pen up |
| `Efface` | Reset the turtle |
| `Def x e` | Bind variable `x` to the value of `e` |
| `:x` | Read variable `x` |
| `Repete e [ i ]` | Repeat instruction `i` `e` times |
| `Si (a op b) Alors i1 Sinon i2 FinSi` | Conditional, `op` ∈ `=`, `<`, `>` |
| `i1 ; i2` | Sequence |
| `.` | End of program |

Compound arithmetic is fully parenthesized, e.g. `(360 / :cotes)`.

### Example: regular polygon

```logo
Efface ;
Avance 200 ; Gauche 90 ; Avance 220 ; Dessine ;
Def cotes 10 ;
Si (:cotes > 2) Alors Repete :cotes [Avance 60; Droite (360 / :cotes)]
Sinon Avance 60 FinSi .
```

More in [`examples/`](examples).

## Build and run

Requirements: OCaml (with `ocamllex` and `ocamlyacc`) and `make`.

```bash
cd src
make
./repl_logo
```

Then type (or paste) a program at the `:>` prompt, ending it with `.`, for example the content of [`examples/polygon.logo`](examples/polygon.logo). Press `Ctrl+C` to quit.

By default the turtle runs in text mode and its position is printed after each program. To get a graphical window, install the OCaml `graphics` library and follow the comments at the top of [`src/Makefile`](src/Makefile).

## Repository layout

```
src/        Final version of the interpreter
steps/      The project's step-by-step progression (one folder per exercise question)
examples/   Sample Logo programs
docs/       Original assignment (in French)
```

`env.ml`, `geometry.ml`, `turtle.ml`, `turtle_graphic.ml` and the `Makefile` were provided by the course, and `logo_ast.ml` / `repl_logo.ml` started from provided skeletons. The lexer, the parser, and the language extensions in the AST and interpreter (arithmetic, loops, conditionals) are my own work.
