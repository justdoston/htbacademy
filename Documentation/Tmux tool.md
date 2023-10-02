# Exploitation Attempts
We need tmux-logging tool to do that.
To install tmux logging tool:

```bash
git clone https://github.com/tmux-plugins/tmux-logging ~/clone/path
```
Add this line to the bottom of .tmux.conf:
```bash
run-shell ~/clone/path/logging.tmux
```
Reload TMUX environment:
```bash
# type this in terminal
$ tmux source-file ~/.tmux.conf
```

Create new session -> `tmux new -s setup`
Start logging -> `[Ctrl] + [B]  followed by [Shift] + [P]`
Stop logging -> `exit`
