# My build of dwm

dwm (dynamic window manager) is an extremely fast, small, and dynamic window manager for X.

## Installation

```sh 
git clone https://github.com/rpamor/dwm.git
cd dwm
sudo make install
```

## Running dwm

Add the following line to your .xinitrc to start dwm using startx:

    exec dwm

## Using dwm

`MODKEY` is set to `Super` key.

`MODKEY + Shift + Enter` - Opens the terminal

`MODKEY + u` - Unswallow window

## Window Swallowing

Allows "window swallowing". 

Useful tool to avoid cluttering the screen with unusable or less important things.

### Syntax

    dwmswallow SWALLOWER [-c CLASS] [-i INSTANCE] [-t TITLE]

Register window `SWALLOWER` to swallow the next future window whose attributes match the `CLASS` name, `INSTANCE` name and window `TITLE` filters using basic string-matching. An omitted filter will match anything.

You can usually use the `$WINDOWID` environment variable for `SWALLOWER`. Check your terminals if it exports this environment variable.

Run the following command below, if it returns a value, you're all set.

    echo $WINDOWID

### Usage

* Basic

    * Separate commands

            dwmswallow $WINDOWID -c Zathura
            zathura some_pdf_file

    * One-liner

            dwmswallow $WINDOWID; zathura some_pdf_file


* Shell integration using alias

    Create an alias like the following:

        alias s='dwmswallow $WINDOWID;' 

    Then, while in the terminal, you activate swallow for the next program you want to run by typing, `<alias> <prog_name>`. The example below uses zathura for opening some pdf file:

        s zathura some_pdf_file.

* Shell integration using hotkey

    * For `zsh` users, add the following to `~/.zshrc`:

            bindkey '^X^m' accept-line-swallow
            zle -N accept-line-swallow acceptandswallow
            acceptandswallow() {
                dwmswallow $WINDOWID
                zle accept-line
            }

        Now that the binding is in place, whenever you want to activate swallow for any program you want to run in the terminal, press `Ctrl-x + Enter` when running a program instead of just `Enter`.

* Swallowing existing windows

    * using the mouse

        Press `MODKEY + Shift + Left_Mouse_Button` on a window and drag it to another window you want it to swallow.

    * using the command line

            dwmswallow SWALLOWER SWALLOWEE

        Using the command line require that you know the `$WINDOWID` of both the `SWALLOWER` and the `SWALLOWEE`. 
