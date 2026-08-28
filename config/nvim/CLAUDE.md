# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal Neovim configuration using **lazy.nvim** as the plugin manager, organized under the `noobie` namespace.

## Architecture

### Entry Point
`init.lua` loads two modules:
- `noobie.core` — editor options and core keymaps (no plugin dependencies)
- `noobie.lazy` — bootstraps lazy.nvim and loads all plugin specs

### Directory Structure
```
lua/noobie/
├── core/           # options.lua + keymaps.lua (loaded before plugins)
├── lazy.lua        # lazy.nvim bootstrap and plugin loader
└── plugins/        # one file per plugin
    ├── lsp/        # lspconfig.lua + mason.lua
    └── *.lua       # individual plugin configs
```

### Configuration Conventions
- Each plugin lives in its own file under `lua/noobie/plugins/`
- LSP-related configs are separated into `plugins/lsp/`
- **Leader key:** `<Space>`
- All custom keymaps follow `<leader>` prefix patterns
- Plugins are configured with lazy-loading (event/cmd/keys-triggered)

## Key Plugin Categories

### LSP & Language Support (Mason-managed)
Installed servers: `ts_ls`, `html`, `cssls`, `tailwindcss`, `svelte`, `graphql`, `emmet_ls`, `prismals`, `pyright`, `ruby_lsp`, `lua_ls`
Installed tools: `prettier`, `stylua`, `eslint_d`

### Core Keymaps to Know
- `<leader>ff/fr/fs/fc` — Telescope: find files/recent/grep/word
- `<leader>ee/ef` — NvimTree: toggle/focus on file
- `<leader>mp` — Format with Conform (also runs on save)
- `<leader>lg` — LazyGit
- `<leader>xw/xd` — Trouble: workspace/document diagnostics
- `gd/gR/gi/gt` — LSP: definition/references/implementations/types
- `<leader>ca/<leader>rn` — LSP: code action/rename
- `]h/[h` — Git hunk navigation
- `<leader>wr/<leader>ws` — Session restore/save

## Making Changes

### Adding a New Plugin
Create a new file `lua/noobie/plugins/plugin-name.lua` returning a lazy.nvim plugin spec table. lazy.nvim auto-discovers all specs under `noobie.plugins`.

### Adding a New LSP Server
1. Add the server name to the `servers` table in `plugins/lsp/mason.lua`
2. Add any server-specific `opts` in `plugins/lsp/lspconfig.lua` if needed

### Modifying Keymaps
- Core (non-plugin) keymaps: `lua/noobie/core/keymaps.lua`
- Plugin keymaps: in the respective plugin file's `keys` table or `on_attach`/setup callback
- LSP keymaps: `plugins/lsp/lspconfig.lua` in the `on_attach` function

### Testing Config Changes
Reload Neovim or use `:source %` for single-file changes. For plugin changes, use `:Lazy sync` or `:Lazy reload <plugin>`.
