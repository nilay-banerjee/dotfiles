# nvim

Lua config under `config/nvim/lua/noobie/`, plugins managed by lazy.nvim.
Structure: `core/` (options, keymaps) loads first, then `lazy.lua` bootstraps
lazy.nvim (cloning it on first run) and imports everything in `plugins/`.

## Options (`core/options.lua`)

Relative + absolute line numbers, 2-space indent with expandtab, no wrap,
smart-case search, cursorline, true color, permanent sign column, system
clipboard (`unnamedplus`), splits open right/below, no swapfiles.

## Keymaps (`core/keymaps.lua`)

Leader is Space.

| Keys | What |
|---|---|
| `jk` (insert) | Escape |
| `<leader>nh` | clear search highlight |
| `<leader>sv` / `sh` / `se` / `sx` | split vertical / horizontal / equalize / close |
| `<leader>to` / `tx` / `tn` / `tp` / `tf` | tab open / close / next / prev / buffer-to-tab |
| `Alt-j` / `Alt-k` (normal + visual) | move line/block down / up |
| `<leader>tw` | toggle wrap |

`Alt-j/k` works in Ghostty because its config sets `macos-option-as-alt = true`.
Plugins add their own maps (telescope on `<leader>f*`, nvim-tree, lazygit) —
which-key pops up the full list after the leader key.

## Plugins (`plugins/`)

One file per plugin. The notable ones:

- **telescope** — fuzzy finding (uses `rg` and `fd` from the server tier)
- **nvim-cmp + lsp/mason + lspconfig** — completion and language servers;
  mason installs servers on demand (some need `node`)
- **treesitter** — syntax; **formatting** (conform) and **linting** (nvim-lint)
- **nvim-tree** — file explorer; **lualine** + **bufferline** — status/tabs
- **lazygit** — opens lazygit in a floating window
- **auto-session** — restores sessions per directory
- **colorscheme** — the theme; **alpha** — start screen
- **discord-rpc (cord.nvim)** — Discord rich presence, builds its helper on install
- quality-of-life: autopairs, surround, substitute, comment, gitsigns,
  indent-blankline, todo-comments, trouble, vim-maximizer, which-key, dressing

## Version pinning

`lazy-lock.json` pins every plugin commit. After pulling the repo on any
machine, run `:Lazy restore` to sync installed plugins to the lockfile. Only
commit lockfile changes when deliberately upgrading (`:Lazy update`, test,
commit). If nvim looks broken right after an update, `:Lazy restore` on the
committed lockfile is the undo button.

## Fresh machine behavior

First `nvim` launch clones lazy.nvim, then installs every plugin from the
lockfile — takes a minute, needs git and network. cord.nvim runs a build step.
Mason-installed LSP servers arrive lazily as filetypes open.
