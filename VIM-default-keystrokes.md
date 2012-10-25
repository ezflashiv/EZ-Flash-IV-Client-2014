Below you'll find list of keystrokes/commands built-in VIM by default which I'm using frequently.

## General

#### Normal mode

* `~` - invert case (upper->lower; lower->upper) of current character
* `xp` - swap two characters around
* `CTRL-a, CTRL-x` - increment, decrement next number on same line as the cursor
* `J` - join the next line to the current line

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
