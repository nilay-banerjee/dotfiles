# dotfiles

Configs for every machine I use, managed by [noob-cli](https://github.com/nilay-banerjee/noob-cli).
The live paths in `$HOME` are symlinks into this repo, so editing `~/.zshrc` edits
the repo copy and `git diff` here shows exactly what changed on this machine.

## Fresh machine

```sh
curl -fsSL https://raw.githubusercontent.com/nilay-banerjee/noob-cli/main/install.sh | sh
noob-cli
```

That installs everything, clones this repo to `~/dotfiles`, and links every config
below. To only link configs on a machine that already has the tools:

```sh
noob-cli dotfiles link
```

## What links where

| Live path | Repo path |
|---|---|
| `~/.zshrc` | `zsh/.zshrc` |
| `~/.p10k.zsh` | `zsh/.p10k.zsh` |
| `~/.tmux.conf` | `tmux/.tmux.conf` |
| `~/.gitconfig` | `git/.gitconfig` |
| `~/.config/nvim` | `config/nvim` |
| `~/.config/aerospace` | `config/aerospace` |
| `~/.config/lazygit` | `config/lazygit` |
| `~/Library/Application Support/lazygit/config.yml` | `config/lazygit/config.yml` |
| `~/.config/ghostty` | `config/ghostty` |
| `~/Library/Application Support/com.mitchellh.ghostty/config` | `ghostty/config` |

The two `Application Support` entries exist because macOS builds of lazygit and
Ghostty read from there, not from `~/.config`. Both resolve to the same tracked
file, so the ambiguity doesn't matter.

## Per-config notes

**zsh** — expects oh-my-zsh at `~/.oh-my-zsh` with zsh-autosuggestions,
zsh-syntax-highlighting, and powerlevel10k cloned into its `custom/` tree, plus
`~/fzf-git.sh` and `fd` for the fzf integration. noob-cli clones and installs all
of it; the `.zshrc` guards machine-specific lines (uv, nvm) so missing tools don't
break shell startup. The prompt needs MesloLGS Nerd Font (`font-meslo-lg-nerd-font`
cask).

**nvim** — lazy.nvim bootstraps itself on first open and installs every plugin
from `lazy-lock.json`. To keep machines on identical plugin versions, treat the
lockfile as the source of truth: run `:Lazy restore` after pulling, and only
commit lockfile changes when deliberately upgrading plugins.

**lazygit** — renders diffs through delta (`git-delta`). The `diffRenderers` key
needs lazygit >= 0.62; older versions reject the config outright.

**git** — `core.pager = delta` with side-by-side on. Side-by-side silently falls
back to unified view in narrow terminals, which looks like delta is off but isn't.
Credentials come from the gh credential helper and live outside this repo.

**aerospace** — tiling window manager config; `start-at-login = true` makes it
self-register on first launch.

**ghostty** — font and theme; expects the same Meslo Nerd Font as the prompt.

## Day-to-day

Edit configs at their live paths as usual, then commit here:

```sh
cd ~/dotfiles && git add -A && git commit && git push
```

On other machines: `git -C ~/dotfiles pull`. Run `noob-cli doctor` any time to
verify links, clones, and sync state — it reports "N commits behind" when a pull
is due.

One recurring gotcha: newer app versions sometimes rewrite their own config on
first launch (lazygit migrated `paging` to `diffRenderers`, nvim plugins update
the lockfile). When `doctor` reports a dirty repo right after setting up a
machine, that's usually what happened. Match the app version across machines,
commit the migration once, pull everywhere.

## Deliberately untracked

Secrets and machine-local state never land here: `~/.git-credentials`, API keys,
lazygit's `state.yml`, shell history, `~/.cache`. Anything that would need a
secret (like lumen's AI provider key) gets configured per machine.
