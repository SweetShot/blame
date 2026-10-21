# Blame

Who changed each line and when, in [rhun](https://rhun.app). A small Rust program built on
[rhun-ext](https://github.com/rhun-editor/extension-protocol/tree/main/rust/rhun-ext).

- **At the cursor**: the line's author and age, as "Ada Lovelace, 3 days ago", in the status bar
  and after the line's text (where rhun draws decoration text). A line you changed and have not
  committed says "You, not committed yet": the blame covers unsaved edits.
- **On hover**: rest the pointer on a line for its commit's author, mail, date and subject.
- **Show File History** and **Show Line History** (also in the editor's menu, for the selected
  lines) list the commits; choose one to open its change to the file in rhun's diff view.
  **Open the Line's Commit** goes straight to the cursor line's commit.
- **Toggle Inline Blame** turns the cursor's blame off and on (also a setting).

Install it from rhun: the extensions button in the title bar, **Install from GitHub…**, then
`rhun-editor/blame`.

## Permissions

It reads the files you have open and the project's Git history, through rhun: rhun runs git for
it, so it needs no git of its own, and a folder opened from a `rhun://` link stays paused for it
until you trust the folder ("Blame: git is paused in this folder"). It changes nothing, has no
internet and runs no programs.

## Build

```sh
cargo build --release
tests/run.sh            # headless, in a fresh repository, against the rhun on your PATH
tests/check.sh          # the protocol's conformance checker
```

While the SDK's source control additions are unreleased, copy `.cargo/config.toml.local` to
`.cargo/config.toml` to build against a checkout of `rhun-editor/extension-protocol` next to this
one (then `Cargo.lock` is not committed: make it with `cargo generate-lockfile` once the SDK's
tag is out, as CI builds with `--locked`). A tag `vX.Y.Z` equal to `version` in `extension.ini` builds Linux, macOS and Windows on their
own runners and publishes what Install from GitHub takes.
