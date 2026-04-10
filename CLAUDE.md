# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal Neovim configuration using [lazy.nvim](https://github.com/folke/lazy.nvim) as the plugin manager. The namespace is `config`.

## Architecture

Entry point: `init.lua` bootstraps three modules:
- `config.core` — editor options, keymaps, and Python provider path
- `config.lazy` — lazy.nvim setup, imports `config.plugins` and `config.plugins.lsp`
- `config.lsp` — LSP keybindings (via `LspAttach` autocmd) and diagnostic display config

Plugin files live in `lua/config/plugins/` — each file returns a lazy.nvim plugin spec. LSP-specific plugin specs are in `lua/config/plugins/lsp/`.

## Plugin Stack

| Category | Plugin |
|---|---|
| Colorscheme | tokyonight.nvim (night style, custom dark blues) |
| File tree | nvim-tree |
| Fuzzy finder | telescope.nvim |
| LSP | nvim-lspconfig + mason.nvim + mason-lspconfig.nvim |
| Completion | nvim-cmp |
| Formatting | conform.nvim (format-on-save) |
| Linting | nvim-lint |
| Treesitter | nvim-treesitter |
| Git | gitsigns.nvim, lazygit.nvim |
| Status line | lualine.nvim |
| Session | auto-session |

## LSP / Tooling

Mason installs these LSP servers automatically: `html`, `lua_ls`, `yamlls`, `ruff`, `ty`.

Mason-tool-installer installs these formatters: `prettier` (JS/TS/CSS/HTML/JSON/Markdown), `stylua` (Lua), `ruff` (Python).

Formatting runs on save via conform.nvim. Python uses `ruff_fix` + `ruff_format` + `ruff_organize_imports` when ruff is available, falling back to `isort` + `black`.

## Key Bindings

Leader key: `<Space>`

| Key | Action |
|---|---|
| `<leader>mp` | Format file (or range in visual) |
| `<leader>l` | Trigger linting |
| `<leader>rs` | Restart LSP |
| `gR` | LSP references (Telescope) |
| `gd` | LSP definition |
| `gD` | Go to declaration |
| `gi` | LSP implementations |
| `gt` | LSP type definitions |
| `<leader>ca` | Code actions |
| `<leader>rn` | Rename symbol |
| `<leader>d` | Line diagnostics |
| `<leader>D` | Buffer diagnostics |
| `[d` / `]d` | Previous/next diagnostic |
| `K` | Hover documentation |
| `jk` | Exit insert mode |

## Adding a Plugin

Create a new file in `lua/config/plugins/` that returns a lazy.nvim spec table. It will be auto-imported by lazy.nvim.

## Requirements

- A true-color terminal (iTerm2 or similar) for the tokyonight colorscheme to render correctly
- A Nerd Font (e.g. Meslo) for icons
