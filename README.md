# Neovim Kickstart Config

This repo contains my custom Neovim config, built on top of [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim). It's designed to provide a clean, modern setup with LSP support, autocomplete, formatting, and everything else you'd expect from a serious Neovim setup.

> [!IMPORTANT]
> Since the original video was recorded, Neovim has been updated to **v0.11.2** (as of 2025-07-13), and this config has been adapted accordingly.  
> If you're still on Neovim **v0.10.x**, use the legacy setup on the [v0.10.1 branch](https://github.com/hendrikmi/neovim-kickstart-config/tree/v0.10.1).

### 🎥 Full Setup Walkthrough

Want to follow along and set this up from scratch? Watch the full video guide:

[![Full Neovim Setup from Scratch in 2025](https://img.youtube.com/vi/KYDG3AHgYEs/0.jpg)](https://youtu.be/KYDG3AHgYEs?si=I71UjuoQg2fHLGyu)


# kickstart.nvim

## Introduction

A starting point for Neovim that is:

* Small
* Single-file
* Completely Documented

**NOT** a Neovim distribution, but instead a starting point for your configuration.

## Installation

### Install Neovim

Kickstart.nvim targets *only* the latest
['stable'](https://github.com/neovim/neovim/releases/tag/stable) and latest
['nightly'](https://github.com/neovim/neovim/releases/tag/nightly) of Neovim.
If you are experiencing issues, please make sure you have the latest versions.

### Install External Dependencies

External Requirements:
- Basic utils: `git`, `make`, `unzip`, C Compiler (`gcc`)
- [ripgrep](https://github.com/BurntSushi/ripgrep#installation),
  [fd-find](https://github.com/sharkdp/fd#installation)
- Clipboard tool (xclip/xsel/win32yank or other depending on the platform)
- A [Nerd Font](https://www.nerdfonts.com/): optional, provides various icons
  - if you have it set `vim.g.have_nerd_font` in `init.lua` to true
- Emoji fonts (Ubuntu only, and only if you want emoji!) `sudo apt install fonts-noto-color-emoji`
- Language Setup:
  - If you want to write Typescript, you need `npm`
  - If you want to write Golang, you will need `go`
  - etc.

> [!NOTE]
> See [Install Recipes](#Install-Recipes) for additional Windows and Linux specific notes
> and quick install snippets

### Install Kickstart

> [!NOTE]
> [Backup](#FAQ) your previous configuration (if any exists)

Neovim's configurations are located under the following paths, depending on your OS:

| OS | PATH |
| :- | :--- |
| Linux, MacOS | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |
| Windows (cmd)| `%localappdata%\nvim\` |
| Windows (powershell)| `$env:LOCALAPPDATA\nvim\` |

#### Recommended Step

[Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) this repo
so that you have your own copy that you can modify, then install by cloning the
fork to your machine using one of the commands below, depending on your OS.

> [!NOTE]
> Your fork's URL will be something like this:
> `https://github.com/<your_github_username>/kickstart.nvim.git`

You likely want to remove `lazy-lock.json` from your fork's `.gitignore` file
too - it's ignored in the kickstart repo to make maintenance easier, but it's
[recommended to track it in version control](https://lazy.folke.io/usage/lockfile).

#### Clone kickstart.nvim

> [!NOTE]
> If following the recommended step above (i.e., forking the repo), replace
> `nvim-lua` with `<your_github_username>` in the commands below

<details><summary> Linux and Mac </summary>

```sh
git clone https://github.com/zkdots/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

</details>

<details><summary> Windows </summary>

If you're using `cmd.exe`:

```
git clone https://github.com/zkdots/kickstart.nvim.git "%localappdata%\nvim"
```

If you're using `powershell.exe`

```
git clone https://github.com/zkdots/kickstart.nvim.git "${env:LOCALAPPDATA}\nvim"
```

</details>

### Post Installation

Start Neovim

```sh
nvim
```

That's it! Lazy will install all the plugins you have. Use `:Lazy` to view
the current plugin status. Hit `q` to close the window.

#### Read The Friendly Documentation

Read through the `init.lua` file in your configuration folder for more
information about extending and exploring Neovim. That also includes
examples of adding popularly requested plugins.

> [!NOTE]
> For more information about a particular plugin check its repository's documentation.


### Getting Started

[The Only Video You Need to Get Started with Neovim](https://youtu.be/m8C0Cq9Uv9o)

### FAQ

* What should I do if I already have a pre-existing Neovim configuration?
  * You should back it up and then delete all associated files.
  * This includes your existing init.lua and the Neovim files in `~/.local`
    which can be deleted with `rm -rf ~/.local/share/nvim/`
* Can I keep my existing configuration in parallel to kickstart?
  * Yes! You can use [NVIM_APPNAME](https://neovim.io/doc/user/starting.html#%24NVIM_APPNAME)`=nvim-NAME`
    to maintain multiple configurations. For example, you can install the kickstart
    configuration in `~/.config/nvim-kickstart` and create an alias:
    ```
    alias nvim-kickstart='NVIM_APPNAME="nvim-kickstart" nvim'
    ```
    When you run Neovim using `nvim-kickstart` alias it will use the alternative
    config directory and the matching local directory
    `~/.local/share/nvim-kickstart`. You can apply this approach to any Neovim
    distribution that you would like to try out.
* What if I want to "uninstall" this configuration:
  * See [lazy.nvim uninstall](https://lazy.folke.io/usage#-uninstalling) information
* Why is the kickstart `init.lua` a single file? Wouldn't it make sense to split it into multiple files?
  * The main purpose of kickstart is to serve as a teaching tool and a reference
    configuration that someone can easily use to `git clone` as a basis for their own.
    As you progress in learning Neovim and Lua, you might consider splitting `init.lua`
    into smaller parts. A fork of kickstart that does this while maintaining the
    same functionality is available here:
    * [kickstart-modular.nvim](https://github.com/dam9000/kickstart-modular.nvim)
  * Discussions on this topic can be found here:
    * [Restructure the configuration](https://github.com/nvim-lua/kickstart.nvim/issues/218)
    * [Reorganize init.lua into a multi-file setup](https://github.com/nvim-lua/kickstart.nvim/pull/473)

### Install Recipes

Below you can find OS specific install instructions for Neovim and dependencies.

After installing all the dependencies continue with the [Install Kickstart](#Install-Kickstart) step.

#### Windows Installation

<details><summary>Windows with Microsoft C++ Build Tools and CMake</summary>
Installation may require installing build tools and updating the run command for `telescope-fzf-native`

See `telescope-fzf-native` documentation for [more details](https://github.com/nvim-telescope/telescope-fzf-native.nvim#installation)

This requires:

- Install CMake and the Microsoft C++ Build Tools on Windows

```lua
{'nvim-telescope/telescope-fzf-native.nvim', build = 'cmake -S. -Bbuild -DCMAKE_BUILD_TYPE=Release && cmake --build build --config Release && cmake --install build --prefix build' }
```
</details>
<details><summary>Windows with gcc/make using chocolatey</summary>
Alternatively, one can install gcc and make which don't require changing the config,
the easiest way is to use choco:

1. install [chocolatey](https://chocolatey.org/install)
either follow the instructions on the page or use winget,
run in cmd as **admin**:
```
winget install --accept-source-agreements chocolatey.chocolatey
```

2. install all requirements using choco, exit the previous cmd and
open a new one so that choco path is set, and run in cmd as **admin**:
```
choco install -y neovim git ripgrep wget fd unzip gzip mingw make
```
</details>
<details><summary>WSL (Windows Subsystem for Linux)</summary>

```
wsl --install
wsl
sudo add-apt-repository ppa:neovim-ppa/unstable -y
sudo apt update
sudo apt install make gcc ripgrep unzip git xclip neovim
```
</details>

#### Linux Install
<details><summary>Ubuntu Install Steps</summary>

```
sudo add-apt-repository ppa:neovim-ppa/unstable -y
sudo apt update
sudo apt install make gcc ripgrep unzip git xclip neovim
```
</details>
<details><summary>Debian Install Steps</summary>

```
sudo apt update
sudo apt install make gcc ripgrep unzip git xclip curl

# Now we install nvim
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux-x86_64.tar.gz
sudo rm -rf /opt/nvim-linux-x86_64
sudo mkdir -p /opt/nvim-linux-x86_64
sudo chmod a+rX /opt/nvim-linux-x86_64
sudo tar -C /opt -xzf nvim-linux-x86_64.tar.gz

# make it available in /usr/local/bin, distro installs to /usr/bin
sudo ln -sf /opt/nvim-linux-x86_64/bin/nvim /usr/local/bin/
```
</details>
<details><summary>Fedora Install Steps</summary>

```
sudo dnf install -y gcc make git ripgrep fd-find unzip neovim
```
</details>

<details><summary>Arch Install Steps</summary>

```
sudo pacman -S --noconfirm --needed gcc make git ripgrep fd unzip neovim
```
</details>

# Vim Shortcuts


## General & Leader Settings

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| Set Leader            | Global          | `<Space>`          | Leader key prefix (used in mappings)     |
| Disable Space         | Normal/Visual   | `<Space>`          | Disable default Space (no effect)        |

## File Operations

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| Save file             | Normal          | `Ctrl+s`           | Save current file                        |
| Save (no autocommand) | Normal          | `Space` + `s` `n`  | Save without auto-formatting             |
| Quit file             | Normal          | `Ctrl+q`           | Quit file                                |

## Buffer Management

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| Next buffer           | Normal          | `Tab`              | Switch to next buffer                    |
| Prev buffer           | Normal          | `Shift+Tab`        | Switch to previous buffer                |
| New buffer            | Normal          | `Space` + `b`      | Open a new buffer                        |
| Close buffer          | Normal          | `Space` + `x`      | Force close current buffer               |

## Window/Split Management

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| Split vertically      | Normal          | `Space` + `v`      | Vertical split                           |
| Split horizontally    | Normal          | `Space` + `h`      | Horizontal split                         |
| Make splits equal     | Normal          | `Space` + `se`     | Make all splits equal size               |
| Close split           | Normal          | `Space` + `xs`     | Close current split window               |
| Resize up             | Normal          | `Up Arrow`         | Decrease window height by 2 lines        |
| Resize down           | Normal          | `Down Arrow`       | Increase window height by 2 lines        |
| Resize left           | Normal          | `Left Arrow`       | Decrease window width by 2 columns       |
| Resize right          | Normal          | `Right Arrow`      | Increase window width by 2 columns       |
| Go split up           | Normal          | `Ctrl+k`           | Focus window above                       |
| Go split down         | Normal          | `Ctrl+j`           | Focus window below                       |
| Go split left         | Normal          | `Ctrl+h`           | Focus window left                        |
| Go split right        | Normal          | `Ctrl+l`           | Focus window right                       |

## Tab Management

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| New tab               | Normal          | `Space` + `to`     | Open new tab                             |
| Close tab             | Normal          | `Space` + `tx`     | Close current tab                        |
| Next tab              | Normal          | `Space` + `tn`     | Switch to next tab                       |
| Previous tab          | Normal          | `Space` + `tp`     | Switch to previous tab                   |

## Navigation & Editing

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| Delete w/o yank       | Normal          | `x`                | Delete char, don't copy                  |
| Scroll down & center  | Normal          | `Ctrl+d`           | Half-page down, center cursor            |
| Scroll up & center    | Normal          | `Ctrl+u`           | Half-page up, center cursor              |
| Find next & center    | Normal          | `n`                | Next search, center cursor               |
| Find prev & center    | Normal          | `N`                | Prev search, center cursor               |
| Toggle line wrap      | Normal          | `Space` + `lw`     | Toggle line wrapping                     |
| Indent left, stay     | Visual          | `<`                | Indent selection left, remain selected   |
| Indent right, stay    | Visual          | `>`                | Indent selection right, remain selected  |
| Paste (keep yank)     | Visual          | `p`                | Paste over, keep original clipboard      |

## Diagnostics

| Shortcut              | Mode            | Keys               | Action                                   |
|-----------------------|-----------------|--------------------|------------------------------------------|
| Previous diagnostic   | Normal          | `[d`               | Jump to previous diagnostic (with float) |
| Next diagnostic       | Normal          | `]d`               | Jump to next diagnostic (with float)     |
| Show diagnostic       | Normal          | `Space` + `d`      | Show floating diagnostic message         |
| Diagnostics list      | Normal          | `Space` + `q`      | Open diagnostics in location list        |


# Plugins shortcuts

## Autocompletion Shortcuts

| Shortcut       | Mode(s)      | Action                                                                              |
|----------------|--------------|-------------------------------------------------------------------------------------|
| `Ctrl+n`       | Insert       | Select next completion item                                                          |
| `Ctrl+p`       | Insert       | Select previous completion item                                                      |
| `Ctrl+b`       | Insert       | Scroll documentation window backward by 4 lines                                      |
| `Ctrl+f`       | Insert       | Scroll documentation window forward by 4 lines                                       |
| `Ctrl+y`       | Insert       | Confirm selection (accept completion, trigger snippet/LSP auto-import)               |
| `Ctrl+Space`   | Insert       | Manually trigger completion menu                                                     |
| `Ctrl+l`       | Insert/Sel   | Expand/move to next snippet placeholder (Luasnip)                                    |
| `Ctrl+h`       | Insert/Sel   | Move to previous snippet placeholder (Luasnip)                                       |
| `Tab`          | Insert/Sel   | Next completion item, expand/jump in snippet, or insert Tab if nothing is available  |
| `Shift+Tab`    | Insert/Sel   | Previous completion item, jump back in snippet, or insert Shift+Tab                  |

## Comment.nvim Shortcuts

| Shortcut      | Mode        | Action                                                     |
|---------------|-------------|------------------------------------------------------------|
| Ctrl+/        | Normal      | Toggle comment on current line (linewise)                  |
| Ctrl+_        | Normal      | Toggle comment on current line (linewise)                  |
| Ctrl+c        | Normal      | Toggle comment on current line (linewise)                  |
| Ctrl+/        | Visual      | Toggle comment on selection (linewise)                     |
| Ctrl+_        | Visual      | Toggle comment on selection (linewise)                     |
| Ctrl+c        | Visual      | Toggle comment on selection (linewise)                     |

## Neovim LSP Keybindings

| Shortcut       | Mode           | Action                                                                |
|----------------|----------------|-----------------------------------------------------------------------|
| `gd`           | Normal         | Go to definition (using Telescope picker)                            |
| `gr`           | Normal         | Find references (using Telescope picker)                             |
| `gI`           | Normal         | Go to implementation (using Telescope picker)                        |
| `<leader>D`    | Normal         | Go to type definition (using Telescope picker)                       |
| `<leader>ds`   | Normal         | List document symbols (using Telescope picker)                       |
| `<leader>ws`   | Normal         | List workspace symbols (using Telescope picker)                      |
| `<leader>rn`   | Normal         | Rename symbol under cursor                                            |
| `<leader>ca`   | Normal, Visual | Perform code action                                                  |
| `gD`           | Normal         | Go to declaration                                                    |
| `<leader>th`   | Normal         | Toggle inlay hints (if supported by the LSP client)                  |

### Additional Notes

- These mappings are **buffer-local**, set up automatically when an LSP attaches.
- `<leader>` corresponds to your configured leader key (often set to `<Space>`).
- Reference highlighting under the cursor is automatically enabled if supported by the LSP.
- The code action mapping works in both normal and visual modes.
- Inlay hints toggle keybinding (`<leader>th`) only applies if your language server supports inlay hints.

Feel free to include this snippet directly in your docs to help users understand and remember the key LSP-related commands in your Neovim setup.

## Neo-tree File Explorer Shortcuts

### Global/Custom Mappings

| Shortcut        | Mode   | Action                                      |
|-----------------|--------|---------------------------------------------|
| `\`             | Normal | Reveal current file in Neo-tree (left pane) |
| `<leader>e`     | Normal | Toggle Neo-tree file explorer (left pane)   |
| `<leader>ngs`   | Normal | Open Neo-tree git status in floating window |

---

### Neo-tree Window Mappings (Default)

| Shortcut               | Mode   | Action                                               |
|------------------------|--------|------------------------------------------------------|
| `<space>`              | Normal | Toggle node (expand/collapse folder)                 |
| `<cr>`, `<2-LeftMouse>`, `l`   | Normal | Open file/folder                               |
| `S`                    | Normal | Open file in split                                   |
| `s`                    | Normal | Open file in vertical split                          |
| `t`                    | Normal | Open file in new tab                                 |
| `w`                    | Normal | Open file using window picker                        |
| `P`                    | Normal | Preview file (floating window)                       |
| `C`                    | Normal | Close folder/node                                    |
| `z`                    | Normal | Close all folders/nodes                              |
| `a`                    | Normal | Add a new file                                       |
| `A`                    | Normal | Add a new directory                                  |
| `d`                    | Normal | Delete                                               |
| `r`                    | Normal | Rename                                               |
| `y`                    | Normal | Copy to clipboard                                    |
| `x`                    | Normal | Cut to clipboard                                     |
| `p`                    | Normal | Paste from clipboard                                 |
| `c`                    | Normal | Copy (prompt for destination)                        |
| `m`                    | Normal | Move (prompt for destination)                        |
| `q`                    | Normal | Close Neo-tree window                                |
| `R`                    | Normal | Refresh tree                                         |
| `<`, `>`               | Normal | Switch between sources (filesystem, buffers, git)    |
| `i`                    | Normal | Show file details                                    |
| `?`                    | Normal | Show help                                            |

---

### Filesystem-Specific Mappings

| Shortcut             | Mode   | Action                                   |
|----------------------|--------|------------------------------------------|
| `<bs>`               | Normal | Go up one directory                      |
| `.`                  | Normal | Set root to current selection            |
| `H`                  | Normal | Toggle hidden files                      |
| `/`                  | Normal | Fuzzy finder (filter files)              |
| `D`                  | Normal | Fuzzy finder (in directories only)       |
| `#`                  | Normal | Fuzzy sort (with fzy algorithm)          |
| `f`                  | Normal | Filter files on submit                   |
| `<c-x>`              | Normal | Clear filter                             |
| `[g`                 | Normal | Previous git modified file               |
| `]g`                 | Normal | Next git modified file                   |

---

### Buffers & Git Status Windows

#### Buffer Source

| Shortcut    | Mode   | Action                |
|-------------|--------|-----------------------|
| `bd`        | Normal | Delete buffer         |
| `<bs>`      | Normal | Navigate up           |
| `.`         | Normal | Set root              |

#### Git Status Source (Floating)

| Shortcut      | Mode   | Action                        |
|---------------|--------|-------------------------------|
| `A`           | Normal | Git add all                   |
| `gu`          | Normal | Git unstage file              |
| `ga`          | Normal | Git add file                  |
| `gr`          | Normal | Git revert file               |
| `gc`          | Normal | Git commit                    |
| `gp`          | Normal | Git push                      |
| `gg`          | Normal | Git commit and push           |

---

### Fuzzy Finder Popup

| Shortcut    | Mode         | Action                         |
|-------------|--------------|-------------------------------|
| `<down>`, `Ctrl+n` | Fuzzy popup | Move selection down        |
| `<up>`, `Ctrl+p`   | Fuzzy popup | Move selection up          |


## Telescope.nvim Keybindings

| Shortcut           | Mode   | Action                                               |
|--------------------|--------|-----------------------------------------------------|
| `<leader>sh`       | Normal | Search help tags                                    |
| `<leader>sk`       | Normal | Search keymaps                                      |
| `<leader>sf`       | Normal | Find files (honors ignore patterns, shows hidden)   |
| `<leader>ss`       | Normal | Select a Telescope builtin/picker                   |
| `<leader>sw`       | Normal | Search for word under cursor                        |
| `<leader>sg`       | Normal | Live grep across project                            |
| `<leader>sd`       | Normal | Search diagnostics (LSP/Linters)                    |
| `<leader>sr`       | Normal | Resume previous Telescope search                    |
| `<leader>s.`       | Normal | Open recently opened files                          |
| `<leader><leader>` | Normal | List open buffers                                   |
| `<leader>/`        | Normal | Fuzzy find in current buffer (dropdown, no preview) |
| `<leader>s/`       | Normal | Live grep in open files only                        |

---

### Telescope Picker Window (Insert Mode)

| Shortcut    | Mode     | Action                       |
|-------------|----------|------------------------------|
| `Ctrl+k`    | Insert   | Move to previous result      |
| `Ctrl+j`    | Insert   | Move to next result          |
| `Ctrl+l`    | Insert   | Select default (open entry)  |
| `Ctrl+/`    | Insert   | Show Telescope keymaps help  |

---

### Notes

- `<leader>` is your leader key (often `<Space>`).
- All mappings are in **normal** mode unless otherwise specified.
- Within Telescope, type `?` in normal mode or press `Ctrl+/` in insert mode for interactive help specific to the picker.
- Live grep and file finders are configured to ignore common directories (e.g., `node_modules`, `.git`, `.venv`) and include hidden files.
- Some extensions (e.g., `fzf`, `ui-select`) are loaded automatically if available and improve performance or UI.

You can paste this block in your project docs to help users navigate your powerful fuzzy finder setup!





