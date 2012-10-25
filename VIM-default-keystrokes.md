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
* `CTRL-M` - move cursor to the middle of the screen
* `CTRL-H` - move cursor to the top of the screen
* `CTRL-L` - move cursor to the bottom of the screen

#### Visual mode

* `gq` - Break selected line into multiple lines
* `gu` - lowercase line
* `gU` - uppercase line

#### Command mode

* `:set paste` - enables paste mode which disables all automatic formatting. Highly useful when pasting some preformatted piece of code.
* `:set nopaste` - disables paste mode

## Macros

#### Recording a macro

* Press `q`
* Press any letter or number to assign macro to
* Start typing commands to save in macro
* Finish recording by pressing `q`

#### Using an existing macro

* Press `@`
* Press letter or number that represents desired macro