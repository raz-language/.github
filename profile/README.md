<div align="center">

<img src="./assets/raz-logo.png" alt="Raz programming language" width="180">

# Raz

**A statically typed systems programming language for fast, safe, predictable native software.**

[![Compiler](https://img.shields.io/badge/compiler-raz-111827?style=flat-square)](https://github.com/raz-language/raz)
[![Packages](https://img.shields.io/badge/packages-registry-111827?style=flat-square)](https://github.com/raz-language/packages)
[![Version](https://img.shields.io/badge/language-1.0-111827?style=flat-square)](https://github.com/raz-language/raz/blob/main/docs/LANGUAGE-STABILITY.md)
[![License](https://img.shields.io/badge/license-Apache--2.0-111827?style=flat-square)](https://github.com/raz-language/raz/blob/main/LICENSE)

[Compiler](https://github.com/raz-language/raz) ·
[Documentation](https://github.com/raz-language/raz/blob/main/docs/README.md) ·
[Getting started](https://github.com/raz-language/raz/blob/main/docs/GETTING-STARTED.md) ·
[Packages](https://github.com/raz-language/packages)

</div>

---

## The Raz language

Raz is a general-purpose systems programming language built around three priorities: **performance, safety, and control.**

It targets software where runtime cost, memory behavior, concurrency, and machine-level access matter — compilers, runtimes, databases, network services, command-line tools, and infrastructure — without giving up modern language design.

Raz 1.0 is a complete native development platform: a self-hosted compiler, a layered standard library, four code-generation backends, a package registry, a formatter, a language server, and reproducible builds.

### Design goals

- **Native performance** with predictable execution and no mandatory tracing garbage collector.
- **Memory safety with explicit control** through ownership, moves, borrowing, non-lexical loan analysis, deterministic destruction, and `unsafe` where low-level access is deliberate.
- **Systems-level control** for runtimes, compilers, networking, storage, and performance-critical applications.
- **Modern abstractions** including generics, traits, associated items, closures, iterators, payload enums, and pattern matching.
- **First-class tooling** built as part of the language rather than bolted on afterwards.
- **Portable targets** — native Windows and Linux, WebAssembly, and RXE bytecode from one compiler pipeline.
- **A cohesive ecosystem** centered on the `raz` toolchain and the official package registry.

---

## Example

Raz uses **type-first declarations**, semicolon-terminated statements, and explicit ownership.

```raz
namespace shapes;

public struct Rect {
    i64 width;
    i64 height;
}

trait Area {
    fn area(Self& self) -> i64;
}

impl Area for Rect {
    fn area(Rect& self) -> i64 {
        return self.width * self.height;
    }
}

fn scale(i64&mut value, i64 factor) {
    *value *= factor;
}

fn main() -> i64 {
    Rect panel = Rect { width: 6, height: 7 };
    i64 total = panel.area();

    scale(&mut total, 2);
    print("computed area");

    return total;
}
```

> Raz 1.0 defines a stable language contract. Syntax, type system, ownership rules, traits and generics, pattern matching, modules, and package interfaces are stable within the 1.x line. See [Language stability](https://github.com/raz-language/raz/blob/main/docs/LANGUAGE-STABILITY.md).

---

## Repositories

| Repository | Purpose |
|---|---|
| **[`raz-language/raz`](https://github.com/raz-language/raz)** | Compiler, language implementation, runtime, standard library, backends, and core developer tools. |
| **[`raz-language/packages`](https://github.com/raz-language/packages)** | Official package registry, package index, and the sources of the official packages. |
| **[`raz-language/.github`](https://github.com/raz-language/.github)** | Organization profile and shared community health files. |

---

## Toolchain

`raz` is the project driver and primary command-line interface.

```text
raz new hello        Create a new package
raz check            Parse, resolve, type-check, and validate
raz build            Build a native artifact
raz run              Build and run a program
raz test             Run test_ functions
raz fmt              Format Raz source
raz doc              Generate API documentation
raz add <package>    Add a dependency from the official registry
raz doctor           Inspect the local toolchain environment
```

The full command surface — backends, targets, workspaces, packaging, and publishing — is documented in the [CLI reference](https://github.com/raz-language/raz/blob/main/docs/CLI.md).

---

## Architecture

The production compiler is written in Raz. Native code is retained only where it belongs: platform, ABI, cryptographic-engine, and backend boundaries.

```text
Raz source
    │
    ▼
Parser + semantic analysis
    │
    ▼
Typed HIR
    │
    ▼
Verified MIR ──────────► diagnostics / language server / tooling
    │
    ├──────── Forge ──────── native object / executable
    ├──────── LLVM ───────── LLVM IR / native object
    ├──────── WebAssembly ── .wasm
    └──────── RXE ────────── .rxe bytecode
```

Forge is the default native backend and is linked in-process. LLVM emits IR from the same verified MIR and delegates native code generation to an external Clang/LLVM toolchain. Every backend shares one frontend and one set of language semantics.

See [Compiler architecture](https://github.com/raz-language/raz/blob/main/docs/ARCHITECTURE.md) and [Backends](https://github.com/raz-language/raz/blob/main/docs/BACKENDS.md).

---

## Packages

The official registry is GitHub-backed and static: immutable, deterministic `.dpk` archives with content-addressed storage, integrity verification, and offline builds.

```text
raz search crypto
raz add crypto
raz add serde@^0.2.0
raz update
```

Published packages include `crypto`, `serde`, `toml`, `regex`, `uuid`, `semver`, `datetime`, `websocket`, `http-router`, `sqlite`, and `postgres`. Browse the registry at [`raz-language/packages`](https://github.com/raz-language/packages).

---

## Documentation

| Guide | Description |
|---|---|
| [Getting Started](https://github.com/raz-language/raz/blob/main/docs/GETTING-STARTED.md) | Practical introduction to the language |
| [Language specification](https://github.com/raz-language/raz/blob/main/docs/LANGUAGE-SPECIFICATION.md) | Normative syntax and semantic rules |
| [CLI reference](https://github.com/raz-language/raz/blob/main/docs/CLI.md) | Project and compiler commands |
| [Package management](https://github.com/raz-language/raz/blob/main/docs/PACKAGE-MANAGEMENT.md) | Dependencies, lockfiles, registries, publishing |
| [Installation](https://github.com/raz-language/raz/blob/main/docs/INSTALLATION.md) | Installers, portable archives, toolchain management |
| [Documentation index](https://github.com/raz-language/raz/blob/main/docs/README.md) | Everything else |

---

## Contributing

Raz is open source and contributions are welcome.

Before opening a pull request, review the contribution guidelines in the repository you are changing and keep changes focused, testable, and consistent with the project's architecture. For bugs and feature proposals, use the issue templates provided by the organization.

Adding a package to the registry follows a separate flow — see [CONTRIBUTING.md](https://github.com/raz-language/packages/blob/main/CONTRIBUTING.md) in the packages repository.

---

## Security

Please do not report security vulnerabilities through public issues.

See the [security policy](https://github.com/raz-language/raz/blob/main/SECURITY.md) for the current reporting process and the areas considered security-relevant.

---

## License

Raz and the official packages are licensed under the [Apache License 2.0](https://github.com/raz-language/raz/blob/main/LICENSE). Forge retains its nested Apache-2.0 license for independent redistribution.

---

<div align="center">

**Raz — fast by design.**

</div>
