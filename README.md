# LEARNING BASH

## Set up config files!
copy the files in the configfiles/ directory to ~/
```bash
cd ./configfiles
cp .bashrc .bash_aliases .tmux.conf ~
```
after doing that, either restart your shell or run
```bash
source ~/.bashrc
```
to test that the new .bashrc has loaded, try running the `cls` alias, which will clear the screen if it has been set.

## Command line basics
* **command input history** - you can access previously entered commands using the up/down arrow keys
* **tab completion** - commands and directories can be automatically completed by pressing tab if there is only one match to what is entered. If there are multiple matches you can hit tab twice in succession to see all matches
* **working directory** - the working directory is typically displayed ahead of the prompt. this is the directory that relative paths will start from. You can use `pwd` to print the working directory and . represents the working directory when at the start of a path
* **home directory** - denoted by ~, the user's home directory is where the shell will expect certain configuration files
* **root directory** - the root of the file system; any full absolute path must begin with the root directory, /
* **parent directory** - use .. to represent the parent directory; in a relative path, it can be used repeatedly (e.g. ~/../../some_dir)
* **ls** - lists the contents of the provided directory (or the working directory if none provided); add -a to include hidden files/directories (begin with .) and -l to display more information about permissions, size, etc.
* **cd** - changes the working directory to the path provided

## Try tmux!
1. Run `tmux -2` to launch a tmux session
2. At the bottom you should see one window labeled `1:bash*` - the asterisk indicated your current shell instance
3. Commands for navigation within tmux use a "prefix" key combination which is used before the command key. By default the prefix is ctrl-b, but the included .tmux.conf file rebinds this to ctrl-a. It also rebinds other things, and going forward this guide will reference only the rebound commands. Press ctrl-a then c to create a new window within tmux. You should see a `2:bash*` in the bottom bar now.
4. Run `htop`, a tool for monitoring running processes and resource usage. You should be able to interact with the options at the bottom by clicking on them. Click on `F5 tree` to see your processes displayed in a tree hierarchy.
5. Notice that there are two instances of `-bash` under `tmux -2`, and one of those instances has `-htop` nested within it. Every pane/window within tmux is a shell instance, and any applications/tools/commands you run will run within that instance - when you exit an interactive application it will return to the shell that spawned it. Click on the `tmux -2` process, or move to it with the up/down arrow keys to select it. Then click `F6 Collapse` to collapse it. You can also use alt+F6. Some keys/inputs will require alt (or something similar) in combination because they have functionality from the OS outside of your shell client that cannot be directly overriden. In order to expand it again, you can do the same or you can click on it in the list if it is still selected (otherwise click on it twice to select and then expand).
6. Let's go back to our first window. Input shift + left arrow (or right arrow) - no prefix is required for this binding. When there are more than two, the window will cycle in the direction of the arrow.
7. You can create panes within windows. Input the prefix and " to split a new pane vertically. The new pane will launch another bash instance with the same working directory that tmux originally was launched from. Input the prefix and % to split a new pane horizontally. You can use the prefix followed by an arrow key to move between panes.
8. tmux sessions persist as long as the host shell is running. Note the name of your session in brackets in the lower left. By default it should be "0". Input the prefix and d to detach from your session. Now, after detaching, run `tmux ls` to list active tmux sessions. You should see "0: 2 windows". To re-attach to the session, now run `tmux a -t 0` (-t specifies the target session to attach to, which is "0"). Upon returning, you should be in the same window and pane you were when you detached.
9. You can also run commands for tmux by typing them. Input the prefix and : to enter a command this way. Let's rename our session. Type `rename-session hello` and hit enter. In the lower left you will now see `[hello]`.
10. Let's close 2 of our panes. To close the active pane, input the prefix and x, then y to confirm. Once you are back down to a single pane, enter the command `list-commands` using the method from the previous step. The window will now display a full list of commands. You can scroll through them using the up/down arrows or pgup/pgdn. Press q to exit back to the current pane. You can also use `list-keys` to view all current key bindings. The : command entry also supports command input history (use up/down arrow) and tab completion of command names.
