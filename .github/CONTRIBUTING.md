# Contributing to Raz

Thank you for contributing to the Raz programming language and ecosystem.

## Before you begin

Please search existing issues and pull requests before opening new work. For substantial language, compiler, runtime, or package-system changes, open an issue first so the design can be discussed before implementation begins.

## Development principles

Contributions should preserve the core direction of the project:

- performance, safety, and explicit control
- clear compiler ownership boundaries
- portable Windows and Linux support
- deterministic behavior where practical
- general compiler infrastructure instead of benchmark-specific shortcuts
- durable documentation rather than pass-by-pass build logs
- focused changes with tests and clear failure behavior

## Pull requests

A good pull request should:

1. solve one coherent problem;
2. explain the motivation and design;
3. include or update relevant tests;
4. avoid unrelated formatting or refactors;
5. preserve existing public behavior unless the change intentionally updates it;
6. update user/developer documentation when behavior changes.

Small, reviewable commits are preferred.

## Compiler and language changes

Changes to syntax, semantics, type checking, ownership, traits, generics, pattern matching, MIR, diagnostics, optimization policy, or language tooling should be implemented in Raz-owned compiler code whenever that layer already exists.

Native C/C++ code should remain limited to platform, ABI, runtime, backend, bootstrap, or other permanent low-level boundaries.

## Testing

Run the narrowest relevant tests first. Full bootstrap and self-host validation may be substantially more expensive and should be used when the change warrants it.

When reporting results, include:

- platform
- compiler/toolchain versions when relevant
- command executed
- pass/fail result
- any known limitations

## Style

Follow the formatting and naming conventions already used by the repository you are changing. Avoid introducing an unrelated style into adjacent code.

## Documentation

Documentation should describe enduring architecture, language behavior, usage, interfaces, and design decisions. Progress history should go in release notes, changelogs, or engineering notes rather than permanent reference documentation.
