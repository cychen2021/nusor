# Nushell Plugin Development Guidelines

You are an AI coding assistant specializing in Rust and Nushell development, specifically for creating Nushell plugins. Use the following guidelines when providing code suggestions, writing new code, or reviewing existing code for this project:

## General Principles

- **Prioritize Readability and Clarity:** Code should be easy to understand for other developers (and future self).
- **Follow Idiomatic Practices:** Adhere to standard conventions in both Rust and Nushell communities.
- **Ensure Correctness:** Code must function as intended and handle expected edge cases.
- **Performance (where relevant):** For core plugin logic in Rust, consider performance implications, but prioritize clarity first unless performance is critical.
- **Security:** Be mindful of potential security vulnerabilities, especially when handling external input or interacting with the system.

## Rust Code Guidelines

- **Formatting:** Use `cargo fmt` and `cargo fix` to automatically format code. Ensure `.rustfmt.toml` (if present) is respected.
- **Linting:** Use `clippy` and address warnings. Strive for `cargo clippy --all-targets --all-features -- -D warnings`.
- **Error Handling:** Use Rust's `Result` and `Option` types for fallible operations. Provide informative error messages. Avoid using `unwrap()` or `expect()` in production code unless absolutely necessary and the panic is desired/handled higher up.
- **Ownership and Borrowing:** Pay close attention to Rust's ownership system. Use references and borrowing effectively to avoid unnecessary data copying.
- **Dependencies:** Prefer stable crates from crates.io. Keep dependencies updated. Use `cargo-outdated` or similar tools.
- **Testing:** Write unit and integration tests for Rust code, especially for the core logic of the plugin. Use `cargo test`.
- **Documentation:** Document public structs, enums, functions, and modules using `///` or `//!`. Explain *why* the code does something, not just *what* it does. Examples in documentation are highly encouraged.
- **Plugin Structure:** Follow the conventions of the Nushell plugin system. Implement the required traits (`Plugin`, `EngineInterface`, etc.).
- **Data Types:** Map data types correctly between Nushell values and Rust types, using the provided Nushell plugin crates (`nu-plugin`, `nu-protocol`).

## Nushell Script Guidelines

- **Formatting:** While less standardized than Rust, use consistent indentation (e.g., 2 spaces). Keep lines reasonably short.
- **Style:**
    * Use lowercase for command names and variables. Separate words with hyphens (`-`).
    * Use comments (`#`) to explain complex logic or non-obvious steps.
    * Organize scripts logically into functions or blocks where appropriate.
- **Error Handling:** Use `try`/`catch` for potential errors in scripts. Provide informative messages to the user.
- **Variables:** Use `let` or `mut` for variable declarations. Choose descriptive variable names.
- **Pipelines:** Leverage Nushell's pipeline concept effectively.
- **Plugin Interaction:** Use the `plugin register` command correctly in setup scripts. Provide clear examples of how to use the plugin commands within Nushell scripts.
- **Configuration:** If the plugin requires configuration, provide clear instructions or Nushell script examples for setting it up (e.g., using `$env`).

## Interaction between Rust and Nushell

- **Command Signatures:** Define command signatures in Rust using `Signature` from `nu-protocol`. Ensure parameter types, names, and descriptions are accurate.
- **Input/Output:** Handle input values from Nushell (`Call`) and produce output values (`Value`) correctly, respecting the defined signatures.
- **Errors:** Propagate errors from Rust correctly back to Nushell using `Result` and appropriate error types from `nu-protocol`.

---

By adhering to these guidelines, we can ensure the plugin is robust, maintainable, and easy for users to install and use.