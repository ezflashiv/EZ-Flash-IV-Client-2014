If there is a filetype plugin distributed with Vim that you want to completely disable, make your own (perhaps empty) settings file in `~/.vim/ftplugin/` directory and add this line to it:
```
let b:did_ftplugin = 1
```

### Enable/Disable Tabs

Sometimes you just need to quickly move between tabs and spaces:

- `:set expandtab` disables tabs
- `:set noexpandtab` enables tabs

### Search and Replace in Visual block

Select block of text and enter something like this in command mode (probably by pressing `:`):

```
:'<,'>s/red/green/g
```

### Prepend multiple lines with anything

- `Ctrl-v` to switch to Visual Block mode
- `Shift-i` to enter Insert mode compatible with Visual Block mode
- Type anything and exit insert mode

### Rename current file

- `:saveas NEWFILENAME`
- `:!rm -f OLDFILENAME`