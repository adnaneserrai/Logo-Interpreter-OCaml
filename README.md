**Logo Language Interpreter - OCaml**



University Project (L2 Computer Science - University of Poitiers) for the ITLP (Introduction to Programming Language Theory) course.





**Project Overview**



The goal was to build a functional interpreter for the Logo language, allowing a "turtle" to draw shapes based on specific commands.

* Lexical Analysis: Handled with OCamllex.
* Parsing: Abstract Syntax Tree (AST) generated via OCamlyacc.
* Interpretation: Recursive evaluation of the AST to execute commands.





**Technical Features**



* Core Commands: `Forward`, `Backward`, `Left`, `Right`, `Clear`.
* Control Structures: Support for `Repeat` loops and nested instructions.
* Variables \& Logic: Implementation of variables (e.g., `:a`) and conditional statements (`If...Then...Else`).
* Functional Programming: Entirely developed in \*\*OCaml\*\*.





**How to run**



1\. Ensure you have OCaml and Make installed.

2\. Compile the project:

&#x20;  ```bash

&#x20;  make

&#x20;  ```

3\. Run the interpreter with a Logo file:

&#x20;  ```bash

&#x20;  ./logo < your\_script.logo

&#x20;  ```

