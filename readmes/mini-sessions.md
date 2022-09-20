<img src="https://github.com/echasnovski/media/blob/main/mini.nvim/logo/logo_sessions.png" style="width: 100%"/>

<!-- badges: start -->
[![GitHub license](https://badgen.net/github/license/echasnovski/mini.nvim)](https://github.com/echasnovski/mini.nvim/blob/main/LICENSE)
<!-- [![GitHub tag](https://badgen.net/github/tag/echasnovski/mini.sessions)](https://github.com/echasnovski/mini.sessions/tags/) -->
<!-- [![Current version](https://badgen.net/badge/Current%20version/development/cyan)](https://github.com/echasnovski/mini.sessions/blob/main/CHANGELOG.md) -->
<!-- badges: end -->

**Session management (read, write, delete)**

See more details in [help file](../doc/mini-sessions.txt).

This is a part of [mini.nvim](https://github.com/echasnovski/mini.nvim) library. See its repository page to learn about common design principles and configuration recipes.

If you want to help this project grow but don't know where to start, check out [contributing guides](../CONTRIBUTING.md) or leave a Github star for 'mini.nvim' project and/or any standalone Git repositories.

## Demo

https://user-images.githubusercontent.com/24854248/173045087-3d18affc-c76f-4d22-8afc-fef687166ef0.mp4

## Features

- Works using `:mksession` (meaning `sessionoptions` is fully respected).
- Implements both global (from configured directory) and local (from current directory) sessions.
- Autoread default session (local if detected, latest otherwise) if Neovim was called without intention to show something else.
- Autowrite current session before quitting Neovim.
- Configurable severity level of all actions.

## Installation

<!-- This plugin can be installed as part of 'mini.nvim' library (**recommended**) or as a standalone Git repository. -->

There are two branches to install from:

- `main` (default, **recommended**) will have latest development version of plugin. All changes since last stable release should be perceived as being in beta testing phase (meaning they already passed alpha-testing and are moderately settled).
- `stable` will be updated only upon releases with code tested during public beta-testing phase in `main` branch.

Here are code snippets for some common installation methods (use only one):

- Using [wbthomason/packer.nvim](https://github.com/wbthomason/packer.nvim):

<table>
    <thead>
        <tr>
            <!-- <th>Github repo</th> -->
            <th>Branch</th> <th>Code snippet</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <!-- <td rowspan=2>'mini.nvim' library</td> -->
            <td>Main</td> <td><code>use 'echasnovski/mini.nvim'</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>use { 'echasnovski/mini.nvim', branch = 'stable' }</code></td>
        </tr>
        <!-- <tr> -->
        <!--     <td rowspan=2>Standalone plugin</td> <td>Main</td> <td><code>use 'echasnovski/mini.sessions'</code></td> -->
        <!-- </tr> -->
        <!-- <tr> -->
        <!--     <td>Stable</td> <td><code>use { 'echasnovski/mini.sessions', branch = 'stable' }</code></td> -->
        <!-- </tr> -->
    </tbody>
</table>

- Using [junegunn/vim-plug](https://github.com/junegunn/vim-plug):

<table>
    <thead>
        <tr>
            <!-- <th>Github repo</th> -->
            <th>Branch</th> <th>Code snippet</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <!-- <td rowspan=2>'mini.nvim' library</td> -->
            <td>Main</td> <td><code>Plug 'echasnovski/mini.nvim'</code></td>
        </tr>
        <tr>
            <td>Stable</td> <td><code>Plug 'echasnovski/mini.nvim', { 'branch': 'stable' }</code></td>
        </tr>
        <!-- <tr> -->
        <!--     <td rowspan=2>Standalone plugin</td> <td>Main</td> <td><code>Plug 'echasnovski/mini.sessions'</code></td> -->
        <!-- </tr> -->
        <!-- <tr> -->
        <!--     <td>Stable</td> <td><code>Plug 'echasnovski/mini.sessions', { 'branch': 'stable' }</code></td> -->
        <!-- </tr> -->
    </tbody>
</table>

**Important**: don't forget to call `require('mini.sessions').setup()` to enable its functionality.

**Note**: if you are on Windows, there might be problems with too long file paths (like `error: unable to create file <some file name>: Filename too long`). Try doing one of the following:
- Enable corresponding git global config value: `git config --system core.longpaths true`. Then try to reinstall.
- Install plugin in other place with shorter path.

## Default config

```lua
-- No need to copy this inside `setup()`. Will be used automatically.
{
  -- Whether to read latest session if Neovim opened without file arguments
  autoread = false,

  -- Whether to write current session before quitting Neovim
  autowrite = true,

  -- Directory where global sessions are stored (use `''` to disable)
  directory = --<"session" subdir of user data directory from |stdpath()|>,

  -- File for local session (use `''` to disable)
  file = 'Session.vim',

  -- Whether to force possibly harmful actions (meaning depends on function)
  force = { read = false, write = true, delete = false },

  -- Hook functions for actions. Default `nil` means 'do nothing'.
  hooks = {
    -- Before successful action
    pre = { read = nil, write = nil, delete = nil },
    -- After successful action
    post = { read = nil, write = nil, delete = nil },
  },

  -- Whether to print session path after action
  verbose = { read = false, write = true, delete = true },
}
```

## Similar plugins

- [mhinz/vim-startify](https://github.com/mhinz/vim-startify)
- [Shatur/neovim-session-manager](https://github.com/Shatur/neovim-session-manager)