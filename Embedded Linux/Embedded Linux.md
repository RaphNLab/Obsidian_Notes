

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



# Confugure tmux


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

