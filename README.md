# mantis
A portable, statically-typed assembly language based on a virtual instruction set

Purpose: Serves as a niche intermediate representation between LLVM-IR and assembly language, allowing greater control than LLVM-IR while guaranteeing security

### Why types?
The idea for creating a typed assembly language came from the namesake research paper on it - TAL (https://dl.acm.org/doi/10.1145/319301.319345). A large motivation for this project is the search for an assembly language that can be verified for correctness and safety, while also allowing low-level compiler optimizations to be applied to it. This would benefit edge applications where the safety of the program must be checked before it is ran (it must be "certified"), yet has limited memory - Mantis would provide a smaller memory footprint while still guaranteeing safety.

### Key Features
- A core set of portable instructions available for any architecture (i.e. nop, load, store, etc.)
- Ability to extend architecture specific capabilities at runtime or by user request
- Virtual register bank that maps to physical registers from an architecture at runtime
- Static type checking on registers, operand values, etc.
- Extensions for SIMD and processing extras like macros

### Core set of instructions
- Data Movement: nop, load, store, move, push, pop
- Control Flow: call, ret, jmp, beg, bne, blt, bgt, ble, bge
- Arithmetic/Logic: add, sub, mul, div, mod, and, or, xor, not
- Comparison & Testing: cmp, test
- Bitwise & Shifting: shift, rotate
- Other Math/Utility: abs, neg, sext (sign extension), zext (zero extension), min, max
- Floating point & Advanced: is_finite, round, floor, ceiling, trunc, sqr, sqrt, sin, cos, tanu

### Language and Syntax
- Operations work from left to right
- Register Operations
  - mov r1, 10 - moves 10 into r1
  - add r1, r2, 5 - moves r2 + 5 into r1
  - sub r3, r2, r1 - moves r2 - r1 into r3
- Memory Access
  - store [r4], r1 - stores the value of r1 in the memory address r4
  - load r1, [r5] - loads the value at the memory address r5 into r1
  - Square brackets - [rX] - indicates memory access
- Control Flow
  - cmp r1, r2 - compares the values in r1 and r2
  - jeq _label - jumps to the specified label if the cmp was equal
  - jmp _label - unconditional jump to the specified label
- Function Calls + Stack
  - call _func - Calls the function _func
  - ret - return from a function
  - push r1 - Push the value of r1 onto the stack
  - pop r2 - Pop the value from the stack and place it into r2
- Type System
  - .int r1 - r1 holds an integer
  - .ptr r1 r2 - r1 is a pointer to r2
  - **Ideally far more types and complex systems like polymorphism and function pointers, this is just for a stage 1**
