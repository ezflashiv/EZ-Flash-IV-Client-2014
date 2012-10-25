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
* `CTRL-u` - move the screen up by half
* `CTRL-d` - move the screen down by half
* `CTRL-f` - move the whole screen down
* `CTRL-b` - move the whole screen up
* `CTRL-e` - move the screen up by one line
* `CTRL-y` - move the screen down by one line
* `zz` - move the screen so that current line would be in the middle
* `zt` - move the screen so that current line would be in the top
* `100zt` - move the screen so that line number **100** would be in the top
* `zb` - move the screen so that current line would be in the bottom
* `''` - move the cursor to previously visited line

#### Visual mode

* `gq` - Break selected line into multiple lines
* `gu` - lowercase line
* `gU` - uppercase line
* `:!ls` - pass selected content to the "ls" command and paste in the output

#### Command mode

* `:set paste` - enables paste mode which disables all automatic formatting. Highly useful when pasting some preformatted piece of code.
* `:set nopaste` - disables paste mode
* `:set ft=javascript` - set the filetype of current file to "javascript"
* `:!date` - run `date` command in your shell and print the output
* `:read !date` - run `date` command in your shell and paste the output in editor
* `:read !curl --silent http://example.com/file.txt` - download a file via **curl** and paste it's content in editor

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
* `:bd` - delete current buffer
* `:bd2` - delete buffer number 2