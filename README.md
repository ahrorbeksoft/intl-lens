<div align="center">

# 🌍 zed-i18n

**Finally, i18n-ally for Zed Editor.**

[![Rust](https://img.shields.io/badge/rust-1.70+-orange.svg)](https://www.rust-lang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Zed](https://img.shields.io/badge/zed-extension-purple.svg)](https://zed.dev)

Stop guessing what `t("common.buttons.submit")` means.<br/>
**See translations inline. Catch missing keys instantly. Ship with confidence.**

[Features](#-features) · [Install](#-installation) · [Configure](#-configuration) · [Contribute](#-contributing)

</div>

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔍 **Inline Hints** | See translation values right next to your i18n keys |
| 💬 **Hover Preview** | View all locale translations in a beautiful popup |
| ⚠️ **Missing Key Detection** | Get warnings for undefined translation keys |
| 🌐 **Incomplete Coverage** | Know which locales are missing translations |
| ⚡ **Autocomplete** | Type `t("` and get instant key suggestions with previews |
| 🎯 **Go to Definition** | Jump directly to the translation in your locale file |
| 🔄 **Auto Reload** | Changes to translation files are picked up automatically |

## 🎬 Demo

```tsx
// Before: What does this even mean? 🤔
<button>{t("common.actions.submit")}</button>

// After: Crystal clear! ✨
<button>{t("common.actions.submit")}</button>  // → Submit
```

**Hover over any i18n key to see:**
```
🌍 common.actions.submit

en: Submit
vi: Gửi
ja: 送信
---
```

## 🚀 Installation

### Quick Start (Build from Source)

```bash
git clone https://github.com/user/zed-i18n.git
cd zed-i18n
cargo build --release -p i18n-lsp
ln -sf $(pwd)/target/release/i18n-lsp ~/.local/bin/
```

### Configure Zed

Add to `~/.config/zed/settings.json`:

```jsonc
{
  "lsp": {
    "i18n-lsp": {
      "binary": { "path": "i18n-lsp" }
    }
  },
  "languages": {
    "TSX": {
      "language_servers": ["typescript-language-server", "i18n-lsp", "..."]
    },
    "TypeScript": {
      "language_servers": ["typescript-language-server", "i18n-lsp", "..."]
    }
  }
}
```

**Restart Zed. Done. 🎉**

## 🎯 Supported Frameworks

Works out of the box with:

| Framework | Patterns |
|-----------|----------|
| **react-i18next** | `t("key")` `useTranslation()` `<Trans i18nKey="key">` |
| **i18next** | `t("key")` `i18n.t("key")` |
| **vue-i18n** | `$t("key")` `t("key")` |
| **react-intl** | `formatMessage({ id: "key" })` |
| **Custom** | Configure your own patterns! |

## ⚙️ Configuration

Create `.i18n-ally.json` in your project root:

```json
{
  "localePaths": ["src/locales", "public/locales"],
  "sourceLocale": "en"
}
```

<details>
<summary><strong>📋 All Options</strong></summary>

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `localePaths` | `string[]` | `["locales", "i18n", ...]` | Where to find translation files |
| `sourceLocale` | `string` | `"en"` | Your primary language |
| `keyStyle` | `"nested" \| "flat"` | `"auto"` | JSON structure style |
| `functionPatterns` | `string[]` | See below | Custom regex patterns |

</details>

<details>
<summary><strong>🔧 Custom Function Patterns</strong></summary>

```json
{
  "functionPatterns": [
    "t\\s*\\(\\s*[\"']([^\"']+)[\"']",
    "translate\\s*\\(\\s*[\"']([^\"']+)[\"']",
    "i18n\\.get\\s*\\(\\s*[\"']([^\"']+)[\"']"
  ]
}
```

</details>

## 📁 Supported File Formats

| Format | Extensions |
|--------|------------|
| JSON | `.json` |
| YAML | `.yaml` `.yml` |

**Nested structure:**
```
locales/
├── en/
│   └── common.json
├── vi/
│   └── common.json
└── ja/
    └── common.json
```

**Or flat structure:**
```
locales/
├── en.json
├── vi.json
└── ja.json
```

## 🛠️ Development

```bash
cargo test          # Run tests
cargo build         # Debug build
cargo build -r      # Release build

# Run with debug logging
RUST_LOG=debug ./target/release/i18n-lsp
```

## 🤝 Contributing

Contributions are welcome! Here's how:

1. Fork the repository
2. Create your feature branch (`git checkout -b feat/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feat/amazing-feature`)
5. Open a Pull Request

### Ideas for Contribution

- [ ] Extract hardcoded strings to translation files
- [ ] Support for more file formats (TOML, PO)
- [ ] Namespace support for large projects
- [ ] Translation file validation
- [ ] Integration with translation services

## 📄 License

MIT © [Trong Nguyen](https://github.com/user)

---

<div align="center">

**If this project helps you, consider giving it a ⭐**

[Report Bug](https://github.com/user/zed-i18n/issues) · [Request Feature](https://github.com/user/zed-i18n/issues)

</div>
