# project path
<!-- keep the format -->
- We follow thr tutorial  Rust_to_Wasm [![alt text][1]](https://developer.mozilla.org/en-US/docs/WebAssembly/Guides/Rust_to_Wasm)
<!-- keep the format -->
## Install package
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cargo uninstall wasm-pack
# enable sccache local already installed
export RUSTC_WRAPPER=sccache
cargo install wasm-pack
```
<!-- end of bash code block -->
<!-- keep the format -->
## Building our WebAssembly package -- inside the actual folder, divergent from tutorial
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
# enable sccache local already installed
export RUSTC_WRAPPER=sccache
#cargo new --lib hello-wasm
cargo init --lib .
```
<!-- keep the format -->
## Replace ./src/lib.rs with the following
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cat > ./src/lib.rs << 'EOF'
use wasm_bindgen::prelude::*;

#[wasm_bindgen]
extern "C" {
    pub fn alert(s: &str);
}

#[wasm_bindgen]
pub fn greet(name: &str) {
    alert(&format!("Hello, {}!", name));
}
EOF
```
<!-- end of bash code block -->
<!-- keep the format -->
## Modify Cargo.toml - Compiling our code to WebAssembly
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cat > ./Cargo.toml << 'EOF'
[package]
name = "hello-wasm"
version = "0.1.0"
authors = ["trapapa <trapapa@gmx.com>"]
description = "A sample project with wasm-pack"
license = "MIT/Apache-2.0"
repository = "https://github.com/yourgithubusername/hello-wasm"
edition = "2024"

[lib]
crate-type = ["cdylib"]

[dependencies]
wasm-bindgen = "0.2"
EOF
```
<!-- end of bash code block -->
<!-- keep the format -->

<!-- keep the format -->

>[!NOTE]
>Symbol to mark web external links [![alt text][1]](./README.md)
<!-- spell-checker: disable  -->
<!-- spell-checker: disable  -->
<!-- keep the format -->
<!-- make folder and download the link sign vai curl -->
<!-- mkdir -p img && curl --create-dirs --output-dir img -O  "https://raw.githubusercontent.com/MathiasStadler/link_symbol_svg/refs/heads/main/link_symbol.svg"-->
<!-- Link sign - Don't Found a better way :-( - You know a better method? - **send me a email** -->
[1]: ./img/link_symbol.svg
<!-- keep the format -->