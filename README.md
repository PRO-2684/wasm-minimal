# Wasm Minimal

[![GitHub License](https://img.shields.io/github/license/PRO-2684/rust-wasm-test-2025?logo=opensourceinitiative)](https://github.com/PRO-2684/rust-wasm-test-2025/blob/main/LICENSE)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/PRO-2684/rust-wasm-test-2025/release.yml?logo=githubactions)](https://github.com/PRO-2684/rust-wasm-test-2025/blob/main/.github/workflows/release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/PRO-2684/rust-wasm-test-2025?logo=githubactions)](https://github.com/PRO-2684/rust-wasm-test-2025/releases)
[![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/PRO-2684/rust-wasm-test-2025/total?logo=github)](https://github.com/PRO-2684/rust-wasm-test-2025/releases)
[![Crates.io Version](https://img.shields.io/crates/v/rust-wasm-test-2025?logo=rust)](https://crates.io/crates/rust-wasm-test-2025)
[![Crates.io Total Downloads](https://img.shields.io/crates/d/rust-wasm-test-2025?logo=rust)](https://crates.io/crates/rust-wasm-test-2025)
[![docs.rs](https://img.shields.io/docsrs/rust-wasm-test-2025?logo=rust)](https://docs.rs/rust-wasm-test-2025)

Minimal template and detailed instructions for developing Wasm with Rust.

## Preface

### Why?

The [`rustwasm` organization](https://github.com/rustwasm/) has been [deprecated](https://blog.rust-lang.org/inside-rust/2025/07/21/sunsetting-the-rustwasm-github-org/), its [book](https://rustwasm.github.io/docs/book/) are not properly updated, and successors of tools like `wasm-pack` & `wasm-bindgen` are scattered across the community. Here's an incomplete table for reference:

| Project | Old Maintainer | New Maintainer | Redirect? |
| - | - | - | - |
| `book` | [rustwasm](https://github.com/rustwasm/book) | / | / |
| `wasm-pack` | [rustwasm](https://github.com/rustwasm/wasm-pack) | [drager](https://github.com/drager/wasm-pack) | 🟢 |
| `wasm-bindgen` | [rustwasm](https://github.com/rustwasm/wasm-bindgen) | [wasm-bindgen](https://github.com/wasm-bindgen/wasm-bindgen) | 🟢 |

### Goal

The main goal of this repo is to help you get started on making *minimal* and *modern* Wasm web apps:

- Minimal: You **do not** have to mess with NPM and bundlers like webpack;
- Modern: You'll have **TypeScript** definitions, and generated glue code will support **ES module** syntax, targeting **modern browsers**.

## Setup

### Install Necessary Tools

1. [Install `cargo-binstall`](https://github.com/cargo-bins/cargo-binstall?tab=readme-ov-file#installation)
    - It will help you install pre-compiled Rust binaries, without having to compile them yourself
    - If you do not want it, you can always replace `binstall` with `install` in the following commands
2. Install `wasm-pack`:
    ```bash
    cargo binstall wasm-pack
    ```
3. (Optional) Install `wasm-bindgen-cli`:
    ```bash
    cargo binstall wasm-bindgen-cli
    ```
4. (Optional) Install `wasm-opt` from [Binaryen](https://github.com/WebAssembly/binaryen/releases/), by:
    1. Downloading appropriate archive
    2. Extracting `bin/wasm-opt(.exe)` to a position in your `$PATH`

You can skip steps marked "Optional", and `wasm-pack` will download them ([`wasm-bindgen-cli`](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/command/build.rs#L424-L429), [`wasm-opt`](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/wasm_opt.rs#L54-L64)) to its own [cache directory](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/cache.rs#L9-L15).

### Initialize Your Project

1. Init your Rust project as a library
    ```bash
    cargo new <slug> --lib
    ```
2. Set `lib.crate-type` in your `Cargo.toml`
    ```toml
    [lib]
    crate-type = ["cdylib", "rlib"]
    ```
3. Adding dependency `wasm-bindgen`
    ```bash
    cargo add wasm-bindgen
    ```
4. Adding dependency `web-sys`, with [features](https://github.com/wasm-bindgen/wasm-bindgen/blob/main/crates/web-sys/Cargo.toml#:~:text=[features]) you want
    ```bash
    cargo add web-sys -F <features>
    # To start with, you may want to follow the example at https://wasm-bindgen.github.io/wasm-bindgen/examples/without-a-bundler.html
    cargo add web-sys -F Document,Element,HtmlElement,Node,Window
    ```

## Build Wasm

```bash
wasm-pack build --target web --no-pack
```

Your Wasm and glue code will be ready under `/pkg`:

- `<slug>_bg.wasm`: The wasm file
- `<slug>.js`: The glue code
- `<slug>.d.ts` / `<slug>_bg.wasm.d.ts`: Type definitions

## See

## What's next?

- https://wasm-bindgen.github.io/wasm-bindgen/

## Credits

- [Hello wasm-pack!](https://drager.github.io/wasm-pack/book/)
- [Without a Bundler - The `wasm-bindgen` Guide](https://wasm-bindgen.github.io/wasm-bindgen/examples/without-a-bundler.html)
<!-- - [Command Line Interface - The `wasm-bindgen` Guide](https://wasm-bindgen.github.io/wasm-bindgen/reference/cli.html) -->
- [Rust and WebAssembly](https://rustwasm.github.io/docs/book/) (Archived)
