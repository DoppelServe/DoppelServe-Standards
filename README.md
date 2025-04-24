# DoppelServe-Standards

A comprehensive guide for developing safety-critical applications in C99, based on NASA/JPL's "Power of Ten" rules with additional safety enhancements.

## About

This repository contains programming standards, style guides, and example implementations for safety-critical C99 applications. These standards are designed for systems where reliability, determinism, and correctness are essential requirements.

## Table of Contents

- [Core Safety Principles](#core-safety-principles)
- [Programming Standards](#programming-standards)
- [Styling Guidelines](#styling-guidelines)
- [Example Implementations](#example-implementations)
- [Verification Tools](#verification-tools)
- [Contact](#contact)

## Core Safety Principles

These standards are designed to enable the development of verifiable, reliable software for safety-critical applications. The primary goals are:

1. **Verifiability**: Code should be amenable to rigorous static analysis
2. **Reliability**: Code should behave predictably under all circumstances
3. **Maintainability**: Code should be easy to understand and modify safely
4. **Determinism**: Execution paths and resource usage should be predictable

## Programming Standards

### 1. Control Flow

- **Prohibited constructs**: No `goto`, `setjmp`/`longjmp`, or recursion
- **Permitted constructs**: Only simple loops (`for`, `while`, `do-while`) and conditionals (`if`, `switch`)
- **Nesting limits**: Maximum loop nesting depth of 2 levels

### 2. Bounded Loops

- **Upper bounds**: All loops must have fixed upper bounds
- **Constants**: Use `#define` constants for loop limits
- **Verification**: It must be trivially possible for a checking tool to prove statically that a preset upper-bound on iterations cannot be exceeded

### 3. Memory Management

- **Static allocation**: No dynamic memory allocation after initialization
- **Memory area**: All memory must be statically allocated

### 4. Function Constraints

- **Size limit**: Maximum 50 lines per function (including comments)
- **Responsibility**: Each function must have a single responsibility

### 5. Assertions

- **Density**: Minimum one assertion per function
- **Validation**: Validate all inputs and critical assumptions
- **Side-effects**: Assertions must be side-effect free and defined as Boolean tests
- **Recovery**: When an assertion fails, an explicit recovery action must be taken

### 6. Variable Scope

- **Smallest scope**: Declare variables in the smallest possible scope
- **Global restriction**: No global variables (except `const` with project prefix)

### 7. Error Handling

- **Return values**: Check all non-void function return values
- **Error codes**: Use consistent error codes throughout project

### 8. Preprocessor Restrictions

- **Permitted uses**: Only for header guards and constant definitions
- **Prohibited uses**: No function-like macros

### 9. Pointer Safety

- **Level restriction**: Single-level pointers only
- **Pointer arithmetic**: No pointer arithmetic (use array indexing instead)
- **Function pointers**: Function pointers are not permitted

### 10. Verification

- **Compiler warnings**: Compile with all warnings enabled and treated as errors
- **Static analysis**: Regular static analysis with strict settings
- **Zero warnings**: All code must compile with zero warnings

## Styling Guidelines

### 1. Formatting

- **Indentation**: 2-space indentation (no tabs)
- **Brace style**: K&R brace style
- **Line length**: Maximum 79 characters per line

### 2. Naming Conventions

- **Variables and functions**: `snake_case`
- **Constants**: `UPPER_CASE`
- **Shared constants**: Project prefix for shared constants (`Project_`)

### 3. Code Organization

- **Prototypes**: Prototypes for all functions
- **Struct declarations**: Explicit `struct` declarations (no typedef struct)
- **Header guards**: Using `#ifndef FILENAME_H`

### 4. Documentation

- **Comment style**: Use `/* */` comments only
- **Module documentation**: Clear module-level documentation
- **Function comments**: Function header comments explaining purpose and constraints

## Example Implementations

## Verification Tools

Recommended tools for verifying compliance with these standards:

```bash
gcc -std=c99 -Wall -Wextra -Werror -pedantic -Wshadow -Wstrict-prototypes -Wmissing-prototypes -Wimplicit -Wconversion -Wundef -Wwrite-strings -Wformat=2 -Wformat-security -Warray-bounds -Wnull-dereference -fstack-protector-strong -O2 -D_FORTIFY_SOURCE=2 -D NDEBUG
```

Additional static analysis tools:
- Coverity
- Cppcheck
- SonarQube
- PRQA (Programming Research QA)
- MISRA C checkers

## Contact

- Website: [DoppelServe.com](https://DoppelServe.com) (coming soon)
- Telegram: [t.me/doppelserve](https://t.me/doppelserve)
- GitHub: [DoppelServe](https://github.com/DoppelServe)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

© 2025 DoppelServe. All rights reserved.
