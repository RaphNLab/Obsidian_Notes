## Authorize user to connect via SSH without password request


```
$host: ssh-keygen
$host: ssh-copy-id pi@ip-addr
$host: cat ~/.ssh/id-rsa.pub //Show Local public key

check the key on the target device
$target: cat ~/.ssh/authorized_keys

```

# **How to log with systemd**

I can have access to all log over systemd using **printf** and **fprintf**
```
printf(const char *format, ...) // I can only redirect the output to stdout

fprintf(FILE *stream, const char *format, ...) // I can select the log output (stderror, stdout)
```

# Changing print colours:

[https://misc.flogisoft.com/bash/tip_colors_and_formatting](https://misc.flogisoft.com/bash/tip_colors_and_formatting)


Je peux dire a Systemd que apres 5 echech il devrait redemarer le systeme (Si je ne t'envoi pas un keep-alive au bout de 30s redemarre l'application)
See [sestemd.service](https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html)

Tu run an application under Linux the command fork, 

USB Mux
+ Setting 1 
![[Pasted image 20250331002810.png]]

# Tmux commands

* ctrl+space :luc_arrow_big_down:
* ctrl+space z : 
* ctrl+space | : Split vertical
* ctrl+space - : Split horizontal
* tmux a : Attach
* tmux ls : List my sessions 
* tmux new -s "session name" 
* tmux a -t toto : Attach to terminal session named "toto"


# Configure  powerline
```
Install powerline first
sudo apt install powerline

Enter the following into .bashrc

# Powerline configuration (by jma) if [ -f /usr/share/powerline/bindings/bash/powerline.sh ]; then powerline-daemon -q POWERLINE_BASH_CONTINUATION=1 POWERLINE_BASH_SELECT=1 source /usr/share/powerline/bindings/bash/powerline.sh fi
```
Result looks as follows:
![[Pasted image 20250331020107.png]]



# Configure tmux


```                 
Install tmux first
sudo apt install tmux


Create and paste the following content to .tmux.conf located in ~/

# Set prefix to Ctrl-Space instead of Ctrl-b
unbind C-b
set -g prefix C-Space
bind Space send-prefix

# Split windows using | and -
unbind '"'
unbind %
bind | split-window -h
bind - split-window -v

#configure powerline
set -g default-terminal "screen-256color"
source "/usr/share/powerline/bindings/tmux/powerline.conf"

##### JMA List of plugins #####
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Allow to save session
set -g @plugin 'tmux-plug

# Fixing locale
set -g utf8 on
set -g status-utf8 on
```



Frame buffer vs Open GL

## VI tutorial

Basic Usage:

1. Starting `vi`: To open a file in `vi`, use the command `vi <filename>`. If the file exists, it will be opened; if not, a new file will be created. 
2. **Entering Insert Mode:** Press the `i` key to enter insert mode, where you can start typing and editing the file. 
3. **Exiting Insert Mode:** Press the `Esc` key to return to command mode. 

- **Saving and Quitting:**
    
    - To save the file and exit, press `Esc`, type `:wq`, and press Enter. 
    - To save and quit, you can also use the keyboard shortcut `ZZ`. 
    - To quit without saving, press `Esc`, type `:q!`, and press Enter. 
    

- **Basic Navigation:**
    - `h`: Move left. 
    - `j`: Move down. 
    - `k`: Move up. 
    - `l`: Move right. 
    

Other Useful Commands:
- `:` (colon): Enter last-line mode, used for saving, quitting, searching, and other commands.
- `x`: Delete the character under the cursor.
- `d`: Delete text (can be combined with movement commands, e.g., `dd` to delete the current line).
- `r`: Replace the character under the cursor.
- `p`: Paste from the buffer (cut and paste).
- `/`: Search for a string within the file.
- `n`: Find the next occurrence of the search string.
- `.`: Repeat the last command. 

Important Notes:

- `vi` is a powerful but can be challenging for beginners due to its keyboard-driven interface. 
- It's crucial to learn the basics of the different modes and common commands. 
- Practice and familiarity are key to mastering `vi`. 
- There is also `Vim`, an enhanced version of `vi` with more features, which may be installed on your system instead of `vi`.

# Setup Direnv

This is a tool used to set, activate and deactivate environment variables. In the folder you like to set specific environment variable, create a file named *.envrc* and add all environment variables you like to it. Once you quit the directory, these environment variables are not more available.

### To install direnv:
```
sudo apt install direnv
```

Add the following line to your *.bashrc*

```
eval "$(direnv hook bash)"
```

Save your changes and source the *.bashrc* file.
```
$host: source .bashrc
```

