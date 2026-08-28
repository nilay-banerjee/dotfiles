# tmux

`tmux/.tmux.conf`. The big deviation from stock: **prefix is `Ctrl-a`**, not
`Ctrl-b` (pairs with Caps-as-Ctrl — the whole chord sits on the home row).

## Bindings (prefix first unless noted)

| Keys | What |
|---|---|
| `\|` | split horizontally (keeps current path) |
| `-` | split vertically (keeps current path) |
| `h` / `j` / `k` / `l` | resize pane left/down/up/right by 5 (repeatable) |
| `m` | toggle pane zoom (repeatable) |
| `r` | reload the config |
| `Ctrl-h/j/k/l` (no prefix) | move between tmux panes AND nvim splits (vim-tmux-navigator) |

Copy mode is vi-style: `v` begins selection, `y` yanks. Mouse is on, but
drag-end no longer auto-copies (the default binding is removed so selections
survive).

## Plugins (via TPM)

- **vim-tmux-navigator** — the seamless `Ctrl-h/j/k/l` navigation across
  tmux/nvim; needs the matching nvim side, which the nvim config loads
- **tmux-resurrect + tmux-continuum** — sessions survive reboots; continuum
  autosaves every 15 minutes and restores on tmux start, resurrect captures
  pane contents too
- **themepack** — powerline cyan status line

TPM itself lives at `~/.tmux/plugins/tpm`; noob-cli clones it and installs the
plugins during setup. Inside tmux: `prefix + I` installs plugins, `prefix + U`
updates them.

## Other settings

256-color terminal, 10k line history, `allow-passthrough on` (lets programs
like image protocols through), and `GPG_TTY` set per-pane so GPG signing
prompts land in the right terminal.
