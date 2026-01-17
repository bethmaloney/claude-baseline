# C/C++ Baseline

Claude Code permissions template for C and C++ projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `gcc` | GNU C compiler |
| `g++` | GNU C++ compiler |
| `clang` | LLVM C compiler |
| `clang++` | LLVM C++ compiler |
| `make` | GNU Make build tool |
| `cmake` | Cross-platform build system generator |
| `ninja` | Fast build system |
| `meson` | Modern build system |
| `gdb` | GNU debugger |
| `lldb` | LLVM debugger |
| `valgrind` | Memory debugging and profiling |
| `ccache` | Compiler cache for faster rebuilds |
| `clang-format` | Code formatter |
| `clang-tidy` | Linter and static analyzer |
| `cppcheck` | Static analysis tool |
| `bear` | Generate compilation database |
| `conan` | C/C++ package manager |
| `vcpkg` | Microsoft C/C++ package manager |
| `pkg-config` | Library configuration tool |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `secrets/**` / `**/secrets/**` | Explicit secrets directories |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/cpp/settings.json
```

## Customization Ideas

- Add `bazel` for Bazel build system
- Add `xmake` for xmake build system
- Add `scons` for SCons build system
- Add `premake5` for Premake
- Add `zig` for Zig compiler (C/C++ compatible)
- Add `emcc` / `em++` for Emscripten (WebAssembly)
- Add `nvcc` for CUDA projects
- Add `hipcc` for AMD ROCm projects
