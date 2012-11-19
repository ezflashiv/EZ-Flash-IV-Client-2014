If there is a filetype plugin distributed with Vim that you want to completely disable, make your own (perhaps empty) settings file in `~/.vim/ftplugin/` directory and add this line to it:
```
let b:did_ftplugin = 1
```