# C/C++ Development Rules

## Standards
- C: C11 or later; C++: C++17 or later (specify target)
- Follow MISRA C/C++ or Google C++ Style Guide consistently
- Enable all warnings: `-Wall -Wextra -Wpedantic -Werror`

## Memory Management
- Prefer RAII and smart pointers (`std::unique_ptr`, `std::shared_ptr`) in C++
- Never raw `new`/`delete`; use `std::make_unique`/`std::make_shared`
- In C: pair every `malloc` with `free`; use cleanup labels or goto for error paths
- Always initialize pointers to `NULL`/`nullptr`
- Check all allocations; handle OOM gracefully

## Pointers & References
- Use `const` aggressively; mark parameters `const` when unmodified
- Null-check before dereferencing; never assume valid pointers
- Prefer references over pointers when null is not an option
- Avoid raw owning pointers; document ownership semantics clearly

## Headers & Includes
- Include only what you use; no transitive dependencies in headers
- Use include guards (`#pragma once`) or `#ifndef` guards consistently
- Forward-declare when possible; minimize header dependencies
- PIMPL idiom for large public headers

## Naming
- Files: `snake_case.c`, `snake_case.h`, `snake_case.cpp`
- Functions/variables: `snake_case`
- Classes/structs: `PascalCase`
- Constants/macros: `UPPER_SNAKE_CASE`
- Enums: `PascalCase` with `UPPER_SNAKE_CASE` members

## Error Handling
- Return error codes or use exceptions consistently (pick one per project)
- In C: check every function return; propagate errors up
- In C++: prefer exceptions for exceptional cases; use `std::expected` (C++23) when available
- Never silently swallow errors

## Concurrency
- Use `std::thread`, `std::mutex`, `std::atomic` in C++
- Prefer `std::lock_guard`/`std::unique_lock` over raw mutex
- Avoid data races; document thread safety guarantees
- In C: use pthreads; prefer lock-free structures when possible

## Build & Compilation
- Use CMake for C++ projects; Makefile for C projects
- Separate debug/release builds; enable sanitizers in debug (`-fsanitize=address,undefined`)
- Link-time optimization (`-flto`) for release builds
- Static analysis: `clang-tidy`, `cppcheck` every build

## Testing
- Use Google Test (GTest) or Catch2 for C++
- Use Unity or CMock for C
- Test edge cases: null inputs, empty containers, boundary values
- Memory leak detection: Valgrind (Linux), AddressSanitizer (all platforms)

## Performance
- Profile before optimizing; measure with `perf`, `VTune`, or `valgrind --tool=callgrind`
- Prefer `std::vector`/`std::string` over raw arrays when size is dynamic
- Avoid virtual calls in hot paths; use CRTP or templates when possible
- Cache-friendly data layout; align structures for SIMD when needed

## Security
- Never use `strcpy`/`strcat`/`gets`; use `strncpy`/`strncat`/`fgets` or `std::string`
- Validate all buffer sizes; prevent buffer overflows
- Use `constexpr`/`consteval` for compile-time computation when possible
- Enable ASLR, stack canaries, and FORTIFY_SOURCE in builds
