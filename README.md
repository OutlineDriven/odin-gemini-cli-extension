# odin-gemini-cli-extension
ODIN [as a Gemini CLI Extension] - Outline Driven development approach for agentic INtelligence

## Prerequisites

```bash
# Install Rust Compiler, pass if you already have cargo
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Install Core CLI Utils with Full Optimizations
export RUSTFLAGS="-C target-cpu=native -C opt-level=3 -C codegen-units=1 -C strip=symbols"

cargo install lsd
cargo install ast-grep
cargo install ripgrep
cargo install fd-find
cargo install --locked bat
cargo install git-delta
cargo install tokei
cargo install --locked --bin jj jj-cli
```

## Official Extension Installation (Recommended now!)

```bash
gemini extensions install https://github.com/OutlineDriven/odin-gemini-cli-extension
```

That easy.

### Additional Settings Customization (Optional)

```shell
git clone https://github.com/OutlineDriven/odin-gemini-cli-extension
cp ./odin-gemini-cli-extension/settings.json ~/.gemini/settings.json
```