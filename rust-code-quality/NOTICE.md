# Provenance and adaptation boundary

## Primary sources

The structure and some rules in this skill are informed by the Asterinas Coding Guidelines:

- <https://github.com/asterinas/asterinas/tree/main/book/src/to-contribute/coding-guidelines>
- <https://github.com/asterinas/asterinas/blob/main/book/src/to-contribute/coding-guidelines/how-guidelines-are-written.md>
- <https://github.com/asterinas/asterinas/blob/main/.agents/skills/aster-code-review/SKILL.md>
- <https://github.com/asterinas/asterinas/blob/main/.agents/skills/aster-code-review/spec/coding_guidelines.md>

The original system is organized by reviewer persona and requires guidelines to be concrete, concise, grounded, and relevant. This skill preserves those principles while adapting the material for general Rust implementation, refactoring, and self-review.

## Adaptation

The following ideas are retained as general principles:

- Minimize the time required to understand code.
- Manage complexity, coupling, and implicit state.
- Use types to encode invariants.
- Use Rust-native ownership, RAII, error propagation, and trait design.
- Make unsafe code, concurrency, resource lifetimes, and testing boundaries explicit.
- Justify performance work with evidence rather than intuition.

The following are not general Rust rules and are intentionally excluded:

- Whether a particular directory permits or denies unsafe code
- OSTD logging macros and `__log_prefix`
- Asterinas workspace dependency conventions
- Linux syscall compatibility documentation
- Architecture-specific assembly, calling conventions, and hardware rules
- Project-specific commit, PR, CI, and release processes

The current repository's explicit conventions take precedence over this skill. When project rules conflict with this skill, follow the project contract and record the reason when needed.

## Source use

The links provide provenance for the ideas and examples; they do not require other repositories to adopt Asterinas-specific constraints. Before redistributing or reproducing source text, verify the upstream repository's license and attribution requirements.