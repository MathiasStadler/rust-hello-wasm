# project path
<!-- keep the format -->
- We follow the tutorial - Rust_to_Wasm [![alt text][1]](https://developer.mozilla.org/en-US/docs/WebAssembly/Guides/Rust_to_Wasm)
<!-- keep the format -->
## Used the last stable version of rust/cargo/rustup
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
rustup update
```
<!-- end of bash code block -->
<!-- keep the format -->
<!-- keep the format -->
## Show which toolchain is active
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
rustup show
# or better
rustup show |sed -n '/active toolchain/,/^$/p'
```
<!-- end of bash code block -->
<!-- keep the format -->
## Switch between Rust toolchains - Check again - See previous step [![alt text][1]](https://stackoverflow.com/questions/58226545/how-to-switch-between-rust-toolchains)
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
rustup override set nightly
rustup override set stable
# another toolchain by name
rustup override set 1.85.0-x86_64-unknown-linux-gnu
```
<!-- end of bash code block -->
<!-- keep the format -->
## Install package used sccache - Reduces compilation time immensely
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cargo uninstall wasm-pack
# Enable sccache if it local already installed
# Reduces compilation time immensely
export RUSTC_WRAPPER=sccache
time cargo install wasm-pack
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
<!-- end of bash code block -->
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
name = "rust-hello-wasm"
version = "0.1.0"
authors = ["Mathias Stadler <stadler-mathias@web.de>"]
description = "A sample project with wasm-pack"
license = "MIT/Apache-2.0"
repository = "https://github.com/MathiasStadler/rust-hello-wasm"
edition = "2024"

[lib]
crate-type = ["cdylib"]

[dependencies]
wasm-bindgen = "0.2"
EOF
```
<!-- end of bash code block -->
<!-- keep the format -->
## Building the package
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
# inside bash
wasm-pack build --target web

```
<!-- end of bash code block -->
<!-- keep the format -->
## Creating index.html
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cat > ./index.html<< 'EOF'
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="utf-8" />
    <title>hello-wasm example</title>
  </head>
  <body>
    <script type="module">
      <!-- import init, { greet } from "./pkg/hello_wasm.js"; --->
      import init, { greet } from "./pkg/rust_hello_wasm.js";
      init().then(() => {
        greet("WebAssembly");
      });
    </script>
  </body>
</html>
EOF
```
<!-- end of bash code block -->
<!-- keep the format -->
## Start with trunk [![alt text][1]](https://crates.io/crates/trunk)
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
trunk serve
```
<!-- end of bash code block -->
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