## Reload tmux config

`Ctrl+b :source-file ~/.tmux.conf`
or from shell:
`tmux source-file ~/.tmux.conf`

## Manipulate Windows

#### Command mode (`Ctrl+b :`)

* `swap-window -s 3 -t 1` - reorder windows so that window #3 takes place of window #1 and vice versa
* `swap-window -t 0` - reorder windows so that current window takes place of window #0 and vice versa