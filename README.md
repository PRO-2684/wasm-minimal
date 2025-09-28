# rust-wasm-test-2025

[![GitHub License](https://img.shields.io/github/license/PRO-2684/rust-wasm-test-2025?logo=opensourceinitiative)](https://github.com/PRO-2684/rust-wasm-test-2025/blob/main/LICENSE)
[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/PRO-2684/rust-wasm-test-2025/release.yml?logo=githubactions)](https://github.com/PRO-2684/rust-wasm-test-2025/blob/main/.github/workflows/release.yml)
[![GitHub Release](https://img.shields.io/github/v/release/PRO-2684/rust-wasm-test-2025?logo=githubactions)](https://github.com/PRO-2684/rust-wasm-test-2025/releases)
[![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/PRO-2684/rust-wasm-test-2025/total?logo=github)](https://github.com/PRO-2684/rust-wasm-test-2025/releases)
[![Crates.io Version](https://img.shields.io/crates/v/rust-wasm-test-2025?logo=rust)](https://crates.io/crates/rust-wasm-test-2025)
[![Crates.io Total Downloads](https://img.shields.io/crates/d/rust-wasm-test-2025?logo=rust)](https://crates.io/crates/rust-wasm-test-2025)
[![docs.rs](https://img.shields.io/docsrs/rust-wasm-test-2025?logo=rust)](https://docs.rs/rust-wasm-test-2025)

<!-- - Issue: [Deprecated `rustwasm` org](https://blog.rust-lang.org/inside-rust/2025/07/21/sunsetting-the-rustwasm-github-org/).
    - [New `wasm-pack`](https://github.com/drager/wasm-pack)
    - [New `wasm-bindgen`](https://github.com/wasm-bindgen/wasm-bindgen)
- Note: Without bundler; On browser only.
- Ref: [Without a Bundler - The `wasm-bindgen` Guide](https://wasm-bindgen.github.io/wasm-bindgen/examples/without-a-bundler.html) -->

## Setup

<!-- > Ref: [Deprecated setup instructions](https://rustwasm.github.io/docs/book/game-of-life/setup.html)
> TODO: [New instructions](https://drager.github.io/wasm-pack/book/) -->

1. Init your Rust project as normal
2. Install `wasm-pack`
    - `cargo binstall wasm-pack`
3. [Install `wasm-bindgen-cli`](https://github.com/wasm-bindgen/wasm-bindgen?tab=readme-ov-file#install-wasm-bindgen-cli)
    - `cargo binstall wasm-bindgen-cli`
    - If not installed, `wasm-pack` will [download it](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/command/build.rs#L424-L429) to [its cache](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/cache.rs#L9-L15)
4. Install `wasm-opt` from [Binaryen](https://github.com/WebAssembly/binaryen/releases/)
    - Download and extract `bin/wasm-opt` to a position in your `$PATH`
    - If not installed, `wasm-pack` will [download it](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/wasm_opt.rs#L54-L64) to [its cache](https://github.com/drager/wasm-pack/blob/cd1718aa7babb656796b8aae3c177ddacce28028/src/cache.rs#L9-L15)
5. Adding dependencies `wasm-bindgen` & `web-sys`
    - `cargo add wasm-bindgen`
    - `cargo add web-sys`, with [features](https://github.com/wasm-bindgen/wasm-bindgen/blob/ba94c0dc77e6e6a911efe318d85d4df3f36c0cb2/crates/web-sys/Cargo.toml#L45) you want
        - To start with, you may want to follow [the example](https://wasm-bindgen.github.io/wasm-bindgen/examples/without-a-bundler.html): features = ['Document', 'Element', 'HtmlElement', 'Node', 'Window']
6. Set `lib.crate-type` in your `Cargo.toml`
    ```toml
    [lib]
    crate-type = ["cdylib", "rlib"]
    ```

## Build Wasm

<!-- Tweaking generated JS glue code: [Command Line Interface - The `wasm-bindgen` Guide](https://wasm-bindgen.github.io/wasm-bindgen/reference/cli.html) -->

1. `wasm-pack build --target web --no-pack`
    - The first run needs to download [`binaryen`](https://github.com/WebAssembly/binaryen/releases/) from GitHub, so:
        - Ensure you've got a stable connection (it doesn't recognize `HTTP(S)_PROXY`), or
        - Install it before running this command (?), or
        - Disable wasm optimizations by adding `wasm-opt = false` under `[package]` in your `Cargo.toml`, or
        - Pass `--no-opt` argument
2. Your wasm is now ready at `/target/wasm32-unknown-unknown/release/<slug>.wasm`
