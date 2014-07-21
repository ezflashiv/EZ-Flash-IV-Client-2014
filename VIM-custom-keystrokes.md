[My dotfiles repo](https://github.com/sergeylukin/dotfiles) includes custom VIM & Plugins configuration which helps coding/typing even faster

Below is a list of custom keystrokes set in configuration

Note that you can override any of these by creating & editing `~/.vimrc.local` file

## General

#### Normal mode

* `,` - So called `<leader>`, is used in combination with other keys to call different actions
* `;` - Switch from **normal mode** to **command mode**
* `<leader>h` - Cancel highlighted selections
* `<leader>q` - Format all file lines
* `<leader>r` - Reload opened files
* `<leader>da` - Delete all buffers
* `<leader>ev` - Open ~/.vimrc file in new tab - very fast & useful
* `<leader>so` - Reload ~/.vimrc file without restarting VIM

#### Visual mode

* `<space>` - Fold/Unfold selected lines

#### Insert mode

* `jj` - Switch from **insert mode** to **normal mode**
* `<leader><tab>` - Code completion popup

#### Command mode

* `:ff` - Open current file in Firefox


## Plugin NERDTree

#### Normal mode

* `<leader>n` OR `<F3>` - Open/Hide NERDTree browser


## Plugin Sparkup (zencoding)

#### Normal mode

* `Ctrl-e` - Execute mapping
* `Ctrl-n` - Next mapping


## Plugin tComment (commenting blocks of text/code)

#### Normal mode

* `<leader>c` - Comment selected lines/letters


## Plugin RSpec

#### Normal mode

* `<leader>s` - Run RSpec


## Markdown (requires /usr/local/bin/Markdown.pl)

#### Normal mode

* `<leader>md` - convert markdown into HTML in current file


## Plugin [PHP-CS-Fixer](https://github.com/stephpy/vim-php-cs-fixer)

#### Normal mode

* `<leader>ff` - Format current PHP file according to PSR-0, PSR-1, PSR-2 standards
* `<leader>fd` - Format current directory with PHP files according to PSR-0, PSR-1, PSR-2 standards