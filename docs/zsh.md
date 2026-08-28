# zsh

`zsh/.zshrc` + `zsh/.p10k.zsh`. Framework is oh-my-zsh, prompt is
powerlevel10k (instant-prompt block at the top must stay first; zoxide's init
must stay last — both are load-order constraints, not style).

## What noob-cli provides

The zshrc assumes these exist, all cloned/installed during setup: oh-my-zsh at
`~/.oh-my-zsh`, zsh-autosuggestions + zsh-syntax-highlighting +
powerlevel10k in its `custom/` tree, `~/fzf-git.sh`, and the `fd`, `fzf`,
`eza`, `bat`, `zoxide` binaries. The prompt needs MesloLGS Nerd Font.

## omz plugins

`git zsh-autosuggestions zsh-syntax-highlighting web-search wd macos
alias-finder aliases ruby rails yarn bundler brew node` — the work-stack ones
(ruby/rails/yarn/bundler) provide aliases only, harmless on machines without
those tools.

## Aliases and functions

| Name | What |
|---|---|
| `ls` | eza long view with git status and icons |
| `cat` | bat |
| `cd` | zoxide (`z`) — frecency jumps, `cd foo` works from anywhere |
| `lg` | lazygit |
| `rd` / `bd` / `pd` | npm / bun / pnpm run dev |
| `ggpull` | git pull origin master |
| `gclone` | git clone |
| `mkdircd <dir>` | mkdir + cd |
| `nclone <repo>` | clone from neetozone org, mise trust, cd in |
| `july` | open Claude Code in the July vault from anywhere |

## fzf setup

`fzf --zsh` wires Ctrl-T (files), Ctrl-R (history), Alt-C (cd). All candidate
generation goes through `fd` (hidden files included, `.git` excluded).
Previews: bat for files, eza tree for dirs. fzf-git.sh adds git-aware pickers
(branches, hashes, remotes) on `Ctrl-G` prefixed chords. Custom night-blue
color theme via `FZF_DEFAULT_OPTS`.

## Version managers

Both mise and nvm are active. Node currently comes from nvm (`~/.nvm`); mise
handles per-project runtimes (`mise trust` in nclone). The nvm block is
guarded, so machines without `~/.nvm` skip it cleanly.

## PATH

`~/.local/bin` (noob-cli and uv installs), GNU make's gnubin (so `make` is GNU
make 4.x, not Apple's 3.81), postgresql@18 binaries, tunnelto. The uv env file
is sourced only if present.
