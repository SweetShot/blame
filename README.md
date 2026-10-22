# Blame

Who changed each line and when, in [rhun](https://rhun.app). A small Rust program built on
[rhun-ext](https://github.com/rhun-editor/extension-protocol/tree/main/rust/rhun-ext).

- **At the cursor**: the line's author, age and commit subject after the line's text, as
  "Ada Lovelace, 3 days ago • Fix the parser" in a muted color, and "Blame: Ada Lovelace, 3 days ago"
  in the status bar. A line you changed and have not committed says "You, not committed yet": the
  blame covers unsaved edits.
- **On hover**: rest the pointer on a line for its commit's author, mail, date and subject.
- **Show File History** and **Show Line History** (also in the editor's menu, for the selected
  lines) list the commits; choose one to open its change to the file in rhun's diff view.
  **Open the Line's Commit** goes straight to the cursor line's commit.
- **Toggle Inline Blame** turns the cursor's blame off and on (and a setting, below).

Install it from rhun's Extensions page (the extensions button in the title bar): **Install from
GitHub…**, then `rhun-editor/blame`. Or take `blame-TARGET.tar.gz` for your system from the
[latest release](https://github.com/rhun-editor/blame/releases/latest) and use **Install** >
**From an Archive**. It needs rhun 0.18 (extension protocol 1.1: Git data and decorations).

## Settings

**Inline blame**, on by default: the author and age of the cursor's line after its text and in
the status bar. It is on the extension's page (Extensions), or in `~/.config/rhun/extensions.ini`:

```ini
[rhun-editor/blame]
setting.inline = no
```

**Toggle Inline Blame** turns it off and on until the extension restarts, without changing the
setting.

## Permissions

It reads the files you have open and the project's Git history, through rhun: rhun runs git for
it, so it needs no git of its own, and a folder opened from a `rhun://` link stays paused for it
until you trust the folder ("Blame: git is paused in this folder"). It changes nothing, has no
internet and runs no programs.

## Build and test

```sh
cargo test
cargo build --release
tests/run.sh [RHUN]     # headless, in a fresh repository, against the rhun on your PATH
tests/check.sh          # the protocol's conformance checker (needs Go)
```

`tests/run.sh` makes a Git repository with two commits by two authors and runs
`tests/basic.txt`: the cursor line's blame, the hover card, an unsaved edit, and a line's history
opening rhun's diff. To build against a checkout of `rhun-editor/extension-protocol` next to this
one, copy `.cargo/config.toml.local` to `.cargo/config.toml`. A tag `vX.Y.Z` equal to `version`
in `extension.ini` builds Linux, macOS and Windows on their own runners and publishes what
Install from GitHub takes.
