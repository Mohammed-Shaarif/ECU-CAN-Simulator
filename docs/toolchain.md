# Development Toolchain

## Development Environment

- Host OS: Windows
- Linux Environment: Ubuntu 24.04 LTS (WSL2)
- IDE: Visual Studio Code

## Compiler and Build System

| Tool | Version |
|---|---|
| GCC / G++ | 13.3.0 |
| C++ Standard | C++17 |
| CMake | 3.28.3 |
| GNU Make | 4.3 |

## Testing

| Tool | Version |
|---|---|
| GoogleTest | 1.14.0 |
| CTest | Bundled with CMake |

## Code Quality and Static Analysis

| Tool | Version |
|---|---|
| clang-format | 18.1.3 |
| clang-tidy | 18.1.3 |
| cppcheck | 2.13.0 |

## Debugging and Version Control

| Tool | Version |
|---|---|
| GDB | 15.1 |
| Git | 2.43.0 |

## Compiler Warning Flags

The project currently enables:

- `-Wall`
- `-Wextra`
- `-Wconversion`

## Build and Test Commands

Configure:

```bash
cmake -S . -B build
```

Build:

```bash
cmake --build build
```

Run tests:

```bash
ctest --test-dir build --output-on-failure
```

## Initial Verification

- [x] C++17 compilation verified.
- [x] CMake configuration successful.
- [x] GoogleTest integration successful.
- [x] Test executable builds successfully.
- [x] CTest discovers and executes tests.
- [x] Strict compiler warning flags enabled.
- [x] Initial test passes (1/1).

