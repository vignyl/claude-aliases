<div align="center">

# claude-aliases

**One-letter shortcuts to launch [Claude Code](https://claude.ai/code) with the model you actually want.**

[![Shell](https://img.shields.io/badge/shell-bash%20%7C%20zsh-89e051?logo=gnu-bash&logoColor=white)](#install)
[![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Linux%20%7C%20WSL-blue)](#install)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](#license)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

</div>

---

## Why

Typing `claude --dangerously-skip-permissions --model claude-opus-4-6` ten times a day gets old. This repo installs four tiny shell aliases so you can launch Claude Code with the right model in **three keystrokes**.

```bash
cco    # Opus, for the hard stuff
ccs    # Sonnet, the daily driver
cch    # Haiku, fast and cheap
ccf5   # Fable 5, the new creative model
```

That's it. No config, no wrapper script, no dependencies beyond the `claude` CLI you already have.

---

## Table of contents

- [Aliases](#aliases)
- [Install](#install)
- [Manual install](#manual-install)
- [Uninstall](#uninstall)
- [How it works](#how-it-works)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## Aliases

| Alias  | Model      | Model ID              | Best for                                              |
|--------|------------|-----------------------|-------------------------------------------------------|
| `cco`  | **Opus**   | `claude-opus-4-6`     | Complex reasoning, architecture, hard debugging       |
| `ccs`  | **Sonnet** | `sonnet` (latest)     | Day-to-day coding, balanced speed/quality             |
| `cch`  | **Haiku**  | `haiku` (latest)      | Quick edits, simple lookups, low-cost batch work      |
| `ccf5` | **Fable 5**| `claude-fable-5`      | Creative writing, prose, narrative-heavy tasks        |

All aliases pass `--dangerously-skip-permissions` so Claude Code runs without per-tool prompts. Drop that flag in [`raccourcis.sh`](./raccourcis.sh) if you'd rather keep prompts on.

---

## Install

One line, detects your shell, idempotent.

```bash
curl -fsSL https://raw.githubusercontent.com/videvjs/claude-aliases/main/install.sh | bash
```

The installer:
- detects `zsh`, `bash`, or falls back to `.profile`,
- appends the aliases to the right rc file,
- skips silently if they're already there.

Reload your shell or `source` the rc file, then:

```bash
ccs "explain this repo"
```

---

## Manual install

Prefer to copy/paste? Add this to your `~/.zshrc` or `~/.bash_profile`:

```bash
# Claude Code aliases
alias ccf5='claude --dangerously-skip-permissions --model claude-fable-5'
alias ccs='claude --dangerously-skip-permissions --model sonnet'
alias cco='claude --dangerously-skip-permissions --model claude-opus-4-6'
alias cch='claude --dangerously-skip-permissions --model haiku'
```

Then `source ~/.zshrc` (or `source ~/.bash_profile`).

---

## Uninstall

Open your shell rc file and remove the `# Claude Code aliases` block. Or one-liner on macOS / Linux:

```bash
sed -i.bak '/# Claude Code aliases/,/alias cch=/d' ~/.zshrc   # or ~/.bash_profile
```

A `.bak` copy is kept just in case.

---

## How it works

Each alias is a one-line wrapper:

```bash
alias ccs='claude --dangerously-skip-permissions --model sonnet'
```

- `claude` is the [Claude Code CLI](https://docs.claude.com/en/docs/claude-code).
- `--model <id>` pins the model for the session.
- `--dangerously-skip-permissions` bypasses per-tool confirmation prompts.

Generic IDs (`sonnet`, `haiku`) automatically resolve to the latest version of that model line. Pinned IDs (`claude-opus-4-6`, `claude-fable-5`) lock you to a specific snapshot, which is useful when you want reproducible behavior.

---

## FAQ

**Why `ccf5` and not `ccf`?**
Fable is brand new and the `5` makes the version explicit — if Fable 6 ships later, we can add `ccf6` without breaking anyone's muscle memory.

**`--dangerously-skip-permissions` sounds scary. Is it safe?**
It skips the per-tool approval prompts inside Claude Code. It does **not** disable sandboxing or remove safety guardrails. If you'd rather be asked before every file write or shell command, edit the aliases and drop the flag.

**Does this work on Windows?**
On WSL or Git Bash, yes. On native PowerShell, no — these are POSIX shell aliases. A PowerShell port would be a welcome PR.

**My alias collides with another tool.**
Rename them. The whole point is that they're three characters of muscle memory — pick three characters you don't already use.

**Can I add my own model?**
Yes. Aliases are just text. Add a line, give it a name, you're done.

---

## Contributing

PRs welcome. Good first contributions:

- New model aliases as Anthropic ships them.
- PowerShell / Fish shell variants of `install.sh`.
- Better duplicate detection in the installer.

Please keep the spirit of the project: **tiny, no dependencies, copy-pasteable**.

---

## License

MIT — see [`LICENSE`](./LICENSE) if present, otherwise consider this a permissive "do whatever you want" notice. Attribution appreciated, not required.
