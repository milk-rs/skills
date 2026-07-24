# Documentation

These rules apply to comments and rustdoc in Rust source, and to Markdown maintained by the project. Follow the repository's established documentation structure and formatting conventions first.

## Rust comments and rustdoc

### `module-docs`

Important modules should begin with `//!` documentation that explains the module's purpose, key types, and relationship to neighboring modules.

### `rfc1574-summary`

The first line of a rustdoc comment should be concise and form one sentence. Functions and methods use a third-person singular present-tense verb such as "Returns" or "Creates". Types, modules, and fields use a noun phrase that names the item.

### `rustdoc-api-not-implementation`

Public documentation describes an API's behavior, contract, and usage; it should not expose implementation details that can change. Put maintenance rationale in an ordinary comment when it is not part of the public contract.

### `rustdoc-identifiers`

Wrap types, functions, fields, and other identifiers in backticks. Prefer rustdoc links for Rust items that can be linked.

### `comment-punctuation`

End complete-sentence comments with appropriate punctuation. Labels, short headings, code fragments, and sentence fragments do not need punctuation added for formality.

## Markdown and crate documentation

### `semantic-line-breaks`

For Markdown and longer doc comments, insert line breaks at semantic boundaries. At minimum, break at sentence boundaries; for long sentences, also consider clause boundaries so each line carries one coherent idea. Semantic line breaks make diffs smaller and merge conflicts less noisy. Do not rewrap unrelated paragraphs merely to apply this rule; generated files and repositories with another established wrapping policy take precedence.

### `readme-as-crate-doc`

When a crate published to crates.io should use the same content for its README and crate-level documentation on docs.rs, keep one source of truth and include the README from the crate root:

```rust
#![doc = include_str!("../README.md")]
```

Adjust the path to the actual crate layout, and verify that the README renders correctly in both a Markdown renderer and rustdoc. If the documents target different readers or need different content, maintain them separately instead of forcing them to share a source.