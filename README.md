# zed-i18n

🌍 Internationalization (i18n) support for [Zed Editor](https://zed.dev) - similar to [i18n-ally](https://github.com/lokalise/i18n-ally) but built for Zed using LSP.

## Features

- **Hover** - See translation values in all locales when hovering over i18n keys
- **Diagnostics** - Warnings for missing translations and incomplete locale coverage
- **Completions** - Autocomplete translation keys with preview
- **Go-to-Definition** - Jump directly to translation files

## Supported Frameworks

| Framework | Function Patterns |
|-----------|-------------------|
| react-i18next | `t("key")`, `<Trans i18nKey="key">` |
| i18next | `t("key")`, `i18n.t("key")` |
| vue-i18n | `$t("key")` |
| react-intl | `formatMessage({ id: "key" })` |

## Installation

### Option 1: Install from Zed Extensions (Coming Soon)

Search for "i18n Ally" in Zed's extension marketplace.

### Option 2: Build from Source

```bash
# Clone the repository
git clone https://github.com/user/zed-i18n.git
cd zed-i18n

# Build the LSP server
cargo build --release -p i18n-lsp

# Add to PATH
ln -sf $(pwd)/target/release/i18n-lsp ~/.local/bin/i18n-lsp
```

Then add to your Zed settings (`~/.config/zed/settings.json`):

```json
{
  "lsp": {
    "i18n-lsp": {
      "binary": {
        "path": "/path/to/i18n-lsp"
      }
    }
  },
  "languages": {
    "TypeScript": {
      "language_servers": ["typescript-language-server", "i18n-lsp", "..."]
    },
    "TSX": {
      "language_servers": ["typescript-language-server", "i18n-lsp", "..."]
    },
    "JavaScript": {
      "language_servers": ["typescript-language-server", "i18n-lsp", "..."]
    }
  }
}
```

## Configuration

Create `.i18n-ally.json` in your project root:

```json
{
  "localePaths": [
    "src/locales",
    "public/locales"
  ],
  "sourceLocale": "en",
  "keyStyle": "nested"
}
```

### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `localePaths` | `string[]` | `["locales", "i18n", ...]` | Directories containing translation files |
| `sourceLocale` | `string` | `"en"` | Primary locale for translations |
| `keyStyle` | `"nested" \| "flat" \| "auto"` | `"auto"` | Key format in translation files |
| `namespaceEnabled` | `boolean` | `false` | Enable namespace support |
| `functionPatterns` | `string[]` | (see below) | Regex patterns to detect i18n keys |

### Default Function Patterns

```json
[
  "t\\s*\\(\\s*[\"']([^\"']+)[\"']",
  "i18n\\.t\\s*\\(\\s*[\"']([^\"']+)[\"']",
  "\\$t\\s*\\(\\s*[\"']([^\"']+)[\"']",
  "formatMessage\\s*\\(\\s*\\{\\s*id:\\s*[\"']([^\"']+)[\"']",
  "<Trans\\s+i18nKey\\s*=\\s*[\"']([^\"']+)[\"']"
]
```

## Translation File Structure

### Nested JSON (default)

```
locales/
├── en/
│   └── common.json
└── vi/
    └── common.json
```

```json
{
  "greeting": "Hello",
  "buttons": {
    "submit": "Submit",
    "cancel": "Cancel"
  }
}
```

### Flat JSON

```json
{
  "greeting": "Hello",
  "buttons.submit": "Submit",
  "buttons.cancel": "Cancel"
}
```

## Development

```bash
# Run tests
cargo test

# Build debug
cargo build -p i18n-lsp

# Build release
cargo build --release -p i18n-lsp

# Run with debug logging
RUST_LOG=debug ./target/release/i18n-lsp
```

## Project Structure

```
zed-i18n/
├── crates/
│   ├── i18n-lsp/           # LSP server (Rust binary)
│   │   └── src/
│   │       ├── main.rs
│   │       ├── backend.rs  # LSP handlers
│   │       ├── config.rs   # Configuration
│   │       └── i18n/       # Core i18n logic
│   │           ├── parser.rs
│   │           ├── store.rs
│   │           └── key_finder.rs
│   └── zed-i18n-extension/ # Zed extension (WASM)
└── Cargo.toml
```

## License

MIT
