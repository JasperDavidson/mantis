# mantis
A portable, statically-typed assembly language based on a virtual instruction set

Purpose: Serves as a niche intermediate representation between LLVM-IR and assembly language, allowing greater control than LLVM-IR while guaranteeing security

Key Features:
* A core set of portable instructions available for any architecture (i.e. nop, load, store, etc.)
* Ability to extend architecture specific capabilities at runtime or by user request
* Virtual register bank that maps to physical registers from an architecture at runtime
* Static type checking on registers, operand values, etc.
* Extensions for SIMD and processing extras like macros

Core set of instructions:
* Data Movement: nop, load, store, move, push, pop
* Control Flow: call, ret, jmp, beg, bne, blt, bgt, ble, bge
* Arithmetic/Logic: add, sub, mul, div, mod, and, or, xor, not
* Comparison & Testing: cmp, test
* Bitwise & Shifting: shift, rotate
* Other Math/Utility: abs, neg, sext (sign extension), zext (zero extension), min, max
* Floating point & Advanced: is_finite, round, floor, ceiling, trunc, sqr, sqrt, sin, cos, tanu
