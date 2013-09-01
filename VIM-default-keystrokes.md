Below you'll find list of keystrokes/commands built-in VIM by default which I'm using frequently.
It is important to note that most (maybe even all) VIM commands related to text search/manipulation affect only first occurence by default.

## General

#### Normal mode

* `~` - invert case (upper->lower; lower->upper) of current character
* `xp` - swap two characters around
* `dj` - cut current line and next line
* `CTRL-a, CTRL-x` - increment, decrement next number on same line as the cursor
* `J` - join the next line to the current line
* `f(` - moves the cursor to the first occurence of "("
* `t(` - moves the cursor right before the first occurence of "("
* `di"` - removes the contents that is being wrapped by double quotes on the same line
* `ci"` - removes the contents that is being wrapped by double quotes on the same line and switches to **Insert mode**
* `da"` - removes the double quotes with contents inside
* `M` - move cursor to the middle of the screen
* `H` - move cursor to the top of the screen
* `3H` - move cursor to the 3rd line from top
* `L` - move cursor to the bottom of the screen
* `3L` - move cursor to the 3rd line from bottom
* `CTRL-u` - scroll up by half
* `CTRL-d` - scroll down by half
* `CTRL-b` - scroll the whole screen up
* `CTRL-f` - scroll the whole screen down
* `CTRL-e` - scroll up by one line
* `CTRL-y` - scroll down by one line
* `zz` - move the screen so that current line would be in the middle
* `zt` - move the screen so that current line would be in the top
* `100zt` - move the screen so that line number **100** would be in the top
* `zb` - move the screen so that current line would be in the bottom
* `' '` - move the cursor to previously visited line
* `> >` - indent current line
* `2 > >` - indent current line and next line
* `< <` - remove one indent for current line
* `= =` - auto-indent current line
* `= G` - auto-indent everything from current line to the end of file
* `zf5j` - fold current line and 5 more lines below it
* `za` - toggle fold
* `zo` - expand fold
* `zc` - collapse fold
* `zR` - unfold all
* `zM` - fold all
* `gq$` - break current line into multiple lines according to `set formatoptions` settings

#### Visual mode

* `gq` - Break selected line into multiple lines according to `set formatoptions` settings
* `gu` - lowercase line
* `gU` - uppercase line
* `o` - move the cursor the the opposite end of selection (very useful if you want to add/remove selection from opposite side)
* `:!ls` - pass selected content to the "ls" command and paste in the output

#### Command mode

* `:verbose set SETTING` - show trace for setting `SETTING` (replace with any desired, like `gdefault`, `paste` etc)
* `:set paste` - enables paste mode which disables all automatic formatting. Highly useful when pasting some preformatted piece of code
* `:set nopaste` - disables paste mode
* `:set list` - show tabs (displayed as "^I") and line endings (displayed as "$")
* `:set ft=javascript` - set the filetype of current file to "javascript"
* `:!date` - run `date` command in your shell and print the output
* `:read !date` - run `date` command in your shell and paste the output in editor
* `:read !curl --silent http://example.com/file.txt` - download a file via **curl** and paste it's content in editor
* `:set scrollbind!` or `:set scb!` - toggle synchronous scrolling. When enabled on 2+ splits, they will scroll simultaneously. Use `Ctrl-e` or `Ctrl-y` to scroll up and down by one line or use any other scrolling keystrokes
* `:set gdefault` - enable `g` flag by default. So for example if searching and replacing with this setting enabled, `g` flag will be used by default (enabling search and replace more than once per line)
* `:%s/this/that/g` - Replace every occurrence in file of `this` to `that` (note that if `gdefault` setting is turned on, then `g` flag should be avoided, or it will give an opposite effect)
* `:g/this/d` - delete all lines containing word `this`. Replace `this` with REGEX pattern and `d` with any other command (like `:g/^this\s*$/p` to print all lines that start with `this` and have spaces until the end of the line)
* `:g!/this/d` - delete all lines the DO NOT contain word `this`

#### Insert mode

* `CTRL-t, CTRL-d` - add indentation, remove indentation for current line

## Macros

#### Recording a macro

* Press `q`
* Press any letter or number to assign macro to
* Start typing commands to save in macro
* Finish recording by pressing `q`

#### Using an existing macro

* Press `@`
* Press letter or number that represents desired macro or `@` to run last executed macro

## Markers

#### Saving a marker

* Press `m`
* Press any letter or number to assign marker to

#### Move cursor to a saved marker

* Press `'`
* Press letter or number that represents desired marker

## Buffers

* `:ls` - prints all buffers
* `:bf` - switch to the first buffer
* `:bp` - switch to previous buffer
* `:bn` - switch to next buffer
* `:b#` - switch to last visited buffer
* `:b2` - switch to buffer number 2
* `:bd` - delete current buffer (in other words close the file)
* `:bd2` - delete buffer number 2

## Splits

* `:sp file.txt` - split current window horizontally and open **file.txt**
* `:vs file.txt` - split current window vertically and open **file.txt**
* `:sb2` - split current window horizontally and open in it buffer number 2
* `:vert sb2` - split current window vertically and open in it buffer number 2
* `CTRL-w l` - navigate to the closest window from the right
* `CTRL-w h` - navigate to the closest window from the left
* `CTRL-w j` - navigate to the closest window from the bottom
* `CTRL-w k` - navigate to the closest window from the top
* `CTRL-w L` - move current window to the most right
* `CTRL-w H` - move current window to the most left
* `CTRL-w J` - move current window to the most bottom
* `CTRL-w K` - move current window to the most top
* `CTRL-w +` - increase the height of current window by one line
* `CTRL-w -` - decrease the height of current window by one line
* `CTRL-w >` - increase the width of current window by one column
* `CTRL-w <` - decrease the width of current window by one column
* `CTRL-w =` - equally distribute the heights and the widths between visible windows
* `CTRL-w T` - moves current window to a new separate tab

## Tabs

* `:tabe file.txt` - create a new tab and open in it **file.txt**
* `gt` - move to the next tab
* `gT` - move to the previous tab