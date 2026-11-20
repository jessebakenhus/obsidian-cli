# obsidian-cli

`obs` is a single zsh script for working with your [Obsidian](https://obsidian.md) vault from the terminal. It reads, edits, creates and moves notes and folders, including nested subfolders. It needs no dependencies and no Obsidian plugin.

## Install

```zsh
git clone https://github.com/jessebakenhus/obsidian-cli.git ~/obsidian-cli
mkdir -p ~/.local/bin && ln -s ~/obsidian-cli/obs ~/.local/bin/obs
```

`~/.local/bin` must be on your `PATH`.

## Vault location

On macOS, `obs` finds your vault automatically from Obsidian's config file. If you have several vaults, or use Linux, set the vault yourself:

```zsh
export OBS_VAULT="$HOME/path/to/vault"
```

## Usage

All paths are relative to the vault root. Notes without a file extension get `.md` added.

| Command | What it does |
| --- | --- |
| `obs ls [folder]` | List a folder |
| `obs tree [folder]` | List all files recursively |
| `obs read <note>` | Print a note |
| `obs edit <note>` | Open a note in `$EDITOR` and create it if missing |
| `obs new <note> [text]` | Create a note; text can also come from stdin |
| `obs append <note> <text>` | Append text to a note; text can also come from stdin |
| `obs mkdir <folder>` | Create a folder, including parent folders |
| `obs mv <old> <new>` | Move or rename a note or folder |
| `obs search <term>` | Search all notes, ignoring case |

```zsh
obs new Projects/2026/Q4/Plan "# Plan"
echo "- [ ] first task" | obs append Projects/2026/Q4/Plan
obs read Projects/2026/Q4/Plan
obs mv Projects/2026/Q4/Plan Archive/Plan
obs search "first task"
```

## Safety

- `new` and `mv` never overwrite an existing file.
- Paths that start with `/` or contain `..` are rejected, so `obs` cannot write outside your vault.
- `obs` has no delete command, on purpose.
- Hidden folders such as `.obsidian` are skipped by `tree` and `search`.

## Limitations

- `obs mv` does not update `[[wikilinks]]` that point to the moved note. Move notes inside Obsidian if you need links updated.
- The script's help text and messages are in German.

## License

[MIT](LICENSE)
