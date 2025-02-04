# dired.nvim

A file browser inspired from Emacs Dired for neovim.

## Screenshots

![output](https://user-images.githubusercontent.com/24680989/216357118-d7d1ecaf-b7bd-4894-9b5e-1c71f40e0dc3.gif)

Different types of files in dired.nvim
![Screenshot from 2023-02-02 20-16-20](https://user-images.githubusercontent.com/24680989/216356401-ae181f74-2aee-434d-9ef6-abdb23ec29e2.png)
![Screenshot from 2023-02-02 20-15-57](https://user-images.githubusercontent.com/24680989/216356422-43a7f103-e82a-4d29-bf90-3278f61866f4.png)



## Installation

Requires [Neovim 0.6](https://github.com/neovim/neovim/releases/tag/v0.6.0) or
higher.

> [Packer.nvim](https://github.com/wbthomason/packer.nvim)
```lua
use {
    "X3eRo0/dired.nvim",
    requires = "MunifTanjim/nui.nvim",
    config = function()
        require("dired").setup {
            path_separator = "/",
            show_banner = false,
            show_icons = false,
            show_hidden = true,
            show_dot_dirs = true,
            show_colors = true,
        }
    end
}
```

### Setup
You can require this plugin and use it like this.
```lua
-- Neovim configuration for the 'dired' plugin

-- Set up the 'dired' plugin with custom options
require("dired").setup({
    path_separator = "/",                -- Use '/' as the path separator
    show_hidden = true,                  -- Show hidden files
    show_icons = false,                  -- Show icons (patched font required)
    show_banner = false,                 -- Do not show the banner
    hide_details = false,                -- Show file details by default
    sort_order = "name",                 -- Sort files by name by default

    -- Define keybindings for various 'dired' actions
    keybinds = {
        dired_enter = "<cr>",
        dired_back = "-",
        dired_up = "_",
        dired_rename = "R",
        -- ... (add more keybindings as needed)
        dired_quit = "q",
    },

    -- Define colors for different file types and attributes
    colors = {
        DiredDimText = { link = {}, bg = "NONE", fg = "505050", gui = "NONE" },
        DiredDirectoryName = { link = {}, bg = "NONE", fg = "9370DB", gui = "NONE" },
        -- ... (define more colors as needed)
        DiredMoveFile = { link = {}, bg = "NONE", fg = "ff3399", gui = "bold" },
    },
})
```

## Usage

Run the command `:Dired` to open a buffer for your current
directory. Press `-` in any buffer to open a directory buffer for its parent.
Editing a directory will also open up a buffer, overriding Netrw.

# Commands

You can use the following commands to add in your custom keybinds.

| Command              | Description                                            |
|----------------------|--------------------------------------------------------|
| Dired                | Open Dired UI (dir completion)                          |
| DiredRename          | Rename file/directory under cursor (file completion)   |
| DiredDelete          | Delete file/directory under cursor (file completion)   |
| DiredMark            | Mark file/directory under cursor (file completion)     |
| DiredDeleteRange     | Delete selected files/directories (visual)             |
| DiredDeleteMarked    | Delete marked files/directories                         |
| DiredMarkRange       | Mark a range of files/directories (visual)             |
| DiredGoBack          | Navigate back in the directory history                 |
| DiredGoUp            | Move up to the parent directory                        |
| DiredCopy            | Copy the file/directory under the cursor               |
| DiredCopyRange       | Copy selected files/directories (visual)              |
| DiredCopyMarked      | Copy marked files/directories                          |
| DiredMove            | Move the file/directory under the cursor               |
| DiredMoveRange       | Move selected files/directories (visual)              |
| DiredMoveMarked      | Move marked files/directories                          |
| DiredPaste           | Paste copied or moved files in the current directory   |
| DiredEnter           | Open the file or directory at the cursor               |
| DiredCreate          | Create a new directory                                 |
| DiredToggleHidden    | Toggle the visibility of hidden files                  |
| DiredToggleSortOrder  | Toggle the sorting order of files and directories      |
| DiredToggleColors    | Toggle the display of colors                            |
| DiredToggleHideDetails| Toggle hiding/showing file details                      |
| DiredQuit            | Quit the 'dired' interface                              |

# Keybinding

Inside a directory buffer, there are the following keybindings:
| Keybinding        | Description                                       |
|-------------------|---------------------------------------------------|
| **`<CR>`**| Open the file or directory at the cursor.         |
| **`d`**| Create new directories and files.                 |
| **`M`**| Mark directories and files (both in normal and visual mode). |
| **`C`**| Copy files.                                       |
| **`X`**| Move files.                                       |
| **`P`**| Paste files in the current directory.             |
| **`D`**| Delete directories and files (both in normal and visual mode). |
| **`R`**| Rename directories and files.                     |
| **`MD`**| Delete marked files.                              |
| **`MC`**| Copy marked files.                                |
| **`MX`**| Move marked files.                                |
| **`-`**| Open the parent directory.                        |
| **`.`**| Toggle show_hidden.                               |
| **`,`**| Change sort_order.                                |
| **`c`**| Toggle colors.                                    |
| **`_`**| Move selection up one line.                       |
| **`,`**| Toggle color display.                             |
| **`(`**| Toggle hiding/showing file details.               |
| **`q`**| Quit the 'dired' interface.                       |

The default keybinds are given below.
```lua
{
    dired_enter = "<cr>",
    dired_back = "-",
    dired_up = "_",
    dired_rename = "R",
    dired_create = "d",
    dired_delete = "D",
    dired_delete_range = "D",
    dired_copy = "C",
    dired_copy_range = "C",
    dired_copy_marked = "MC",
    dired_move = "X",
    dired_move_range = "X",
    dired_move_marked = "MX",
    dired_paste = "P",
    dired_mark = "M",
    dired_mark_range = "M",
    dired_delete_marked = "MD",
    dired_toggle_hidden = ".",
    dired_toggle_sort_order = ",",
    dired_toggle_colors = "c",
    dired_toggle_hide_details = "(",
    dired_quit = "q",
}
```

# Colors

You can change the colors of each component in the output by specifiying 
a table of options for each Hightlight group used in Dired.

```lua
local DiredDimText = {
    link = {},
    bg = "232323",
    fg = "f3f3f3"
    gui = "bold",
}
```

The options are explained below.
| Option | Descript |
|--------|----------|
| link | A list of highlight groups to link to, in order of priority. The first one that exists will be used. |
| bg | The background color to use, in hex, if the highlight group is not defined and it is not linked to another group.|
| fg | The foreground color to use, in hex, if the highlight group is not defined and it is not linked to another group.|
| gui | The gui to use, if the highlight group is not defined and it is not linked to another group. |

The gui arg is described in syntax.txt and valid arguments are defined in attr-list ``:h attr-list``
```
gui={attr-list}
	These give the attributes to use in the GUI mode.
	See |attr-list| for a description.
	Note that "bold" can be used here and by using a bold font.  They
	have the same effect.
	Note that the attributes are ignored for the "Normal" group.

```

attr-list is a comma-separated list (without spaces) of the
following items (in any order):


| Option | Description |
|--------|-------------|
|bold||
|underline||
|undercurl|curly underline
|underdouble|double underline|
|underdotted|dotted underline|
|underdashed|dashed underline|
|strikethrough||
|reverse||
|inverse|same as reverse|
|italic||
|standout||
|altfont||
|nocombine|override attributes instead of combining them|
|NONE|no attributes used (used to reset it)|

The default color configuration is given below
```lua
{
    DiredDimText = { link = {}, bg = "NONE", fg = "505050", gui = "NONE" },
    DiredDirectoryName = { link = {}, bg = "NONE", fg = "9370DB", gui = "NONE" },
    DiredDotfile = { link = {}, bg = "NONE", fg = "626262" },
    DiredFadeText1 = { link = {}, bg = "NONE", fg = "626262", gui = "NONE" },
    DiredFadeText2 = { link = {}, bg = "NONE", fg = "444444", gui = "NONE" },
    DiredSize = { link = { "Normal" }, bg = "NONE", fg = "None", gui = "NONE" },
    DiredUsername = { link = {}, bg = "NONE", fg = "87CEFA", gui = "bold" },
    DiredMonth = { link = { "Normal" }, bg = "NONE", fg = "None", gui = "bold" },
    DiredDay = { link = { "Normal" }, bg = "NONE", fg = "None", gui = "bold" },
    DiredFileName = { link = {}, bg = "NONE", fg = "NONE", gui = "NONE" },
    DiredFileSuid = { link = {}, bg = "ff6666", fg = "000000", gui = "bold" },
    DiredNormal = { link = { "Normal" }, bg = "NONE", fg = "NONE", gui = "NONE" },
    DiredNormalBold = { link = {}, bg = "NONE", fg = "ffffff", gui = "bold" },
    DiredSymbolicLink = { link = {}, bg = "NONE", fg = "33ccff", gui = "bold" },
    DiredBrokenLink = { link = {}, bg = "2e2e1f", fg = "ff1a1a", gui = "bold" },
    DiredSymbolicLinkTarget = { link = {}, bg = "5bd75b", fg = "000000", gui = "bold" },
    DiredBrokenLinkTarget = { link = {}, bg = "2e2e1f", fg = "ff1a1a", gui = "bold" },
    DiredFileExecutable = { link = {}, bg = "NONE", fg = "5bd75b", gui = "bold" },
    DiredMarkedFile = { link = {}, bg = "NONE", fg = "a8b103", gui = "bold" },
    DiredCopyFile = { link = {}, bg = "NONE", fg = "ff8533", gui = "bold" },
    DiredMoveFile = { link = {}, bg = "NONE", fg = "ff3399", gui = "bold" },
}
```

## TODO

1. Allow changing file permissions.
