# ghostty + aerospace

## ghostty (`ghostty/config`)

- MesloLGS Nerd Font Mono at 19pt (the p10k prompt's glyphs need it)
- "Nocturnal Winter" theme, 0.9 background opacity
- `macos-option-as-alt = true` — this is what makes `Alt-j/k` line-moving work
  in nvim and `Alt-<key>` reach AeroSpace... except where Ghostty unbinds:
  `alt+left` / `alt+right` are unbound so the shell's `Alt-arrow` word-jump
  bindings (in `.zshrc`) receive them
- `confirm-close-surface = false` — no close-tab nagging

macOS Ghostty reads `~/Library/Application Support/com.mitchellh.ghostty/config`;
Linux would read `~/.config/ghostty`. Both are linked to repo copies.

## aerospace (`config/aerospace/aerospace.toml`)

Tiling window manager, starts at login, tiles by default with 5px gaps.

| Keys | What |
|---|---|
| `Ctrl-Alt-h/j/k/l` | focus window left/down/up/right |
| `Alt-Shift-h/j/k/l` | move window |
| `Alt-minus` / `Alt-equal` | shrink / grow |
| `Alt-slash` | tiles layout, `Alt-comma` accordion |
| `Alt-1..9`, `Alt-a..z` | jump to workspace (all persistent) |

Focus keys use `Ctrl-Alt` instead of plain `Alt` to avoid colliding with the
terminal/nvim `Alt` bindings above. Mouse follows focus across monitors.
First launch asks for Accessibility permission — that's macOS, unavoidable.
