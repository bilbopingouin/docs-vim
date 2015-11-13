# Various Commands

### marks

- `ma`     sets mark 'a'
- `` `a``    jumps to mark 'a'
- `:marks` list marks

### fold

- `zf`      fold (create) selected lines
- `zd`      delete selected fold
- `zo`      open fold
- `zc`      close fold
- `za`      toggle fold
- `zC`      closes all fold and sub-folds at this point
- `zO`      opens all fold and sub-folds at this point
- `zR`      opens all folds in current file `zr` opens only one fold level in the whole file
- `zM`      closes all folds in current file
- `:set foldmethod=indent` choose some method of automatic folding

More on [wikia](http://vim.wikia.com/wiki/Folding).

### diff

Start diff

    vim -d file1 file2 [...]

Update comparison within vim session

    :diffu[pdate]

Some commands

- `]c` or `[c` jumps to next or previous change
- `do`         diff get (modify current file)
- `dp`         diffput (modify other file)

for git mergetools

- `:diffget RE` take it from remote
- `:diffget BA` take it from BASE
- `:diffget LO` take it from local

### select mode

select is similar to visual but with some differences: writing overwrites selected text

- `gh`      enters select mode from normal mode
- `<C-G>`   enters select mode from visual mode
- `gH`      enters select mode and select a line
- `g <C-H>` enters select block mode

### undo

direct command:

    u   " undo previous

interesting to map

    imap <C-z> <C-O>u " C-z in insert mode undo previous

redo

    <C-r>

But undo can be more advanced, with branches:

- `:undol[ist]`         list list of changes
- `:earlier`            returns to an earlier state
- `g-`                  same
- `:later`              go back to later state
- `g+`                  same as above
- `:echo undotree()`    prints list of changes in a tree

More can be found in [Undo and Redo](http://vim.wikia.com/wiki/Undo_and_Redo) and [Undo branches](http://vim.wikia.com/wiki/Using_undo_branches)

Furthermore, this [script](https://github.com/mbbill/undotree) seems to be a very simple, yet elegant plugin for visualising an undo tree.

### registers

Are a very nice way to store some information.

There are different types:

- `"`      : unamed register: filled as a result of `d` `c` `s` `x` `y` commands
- `0-9`    : numbered registers filled with past yanks/deletes
- `-`      : small delete: fill with last delete (less than a line)
- `a-zA-Z` : named registers, filled when asked by the user

some read-only registers

- `.`      : contains last inserted text
- `%`      : contains name of current file
- `#`      : name of alternate file
- `:`      : most recently executed command
- `/`      : most recent search pattern
- `_`      : /dev/null

one can print the content of a register with

- `<C-r> a` : in insert mode, prints content of register `a`, e.g. `<C-r> %` prints the current filename
- `:put"a`  : in normal mode, inserts content of register `a`, e.g. `:put"%` does as above
- `"ap`     : like normal `p` but uses content of register `a`
- `"aP`     : like normal `P` but uses content of register `a`
- `"ax`     : like normal `x` but uses content of register `a`
- `"add`    : like normal `dd` but uses content of register `a`

stores information on registers

- `:let @a = "yyp"` stores `ypp` in register `a` (or "a)
- `qa`              reccords commands in register `a` ("a). Stops with `q`
- `"ayy`            yank into register `a` (works with other uses of yank)

other use

- `@a`              executes content of register `a`
- `:@a`             same but as Ex commands

A special register is `=` which allows you to type in a command in insert mode try

- `<C-r> = 37+5`            42
- `<C-r> = system("date")`   inserts the date, as Wed Oct 29 16:40:09 CET 2014
- `<C-r> = expand("%:t:r")`  inserts the filename without extension. Eg. for `/path/filename.vim` it inserts `filename`

list and see content of all registers

    :reg

The following registers have actions on copy-paste with the rest of the system (clipboard)
if vim has been compiled with `+clipboard`: `*` and `+` registers.

more info:
- [How to Use Registers](https://stackoverflow.com/questions/1497958/how-to-use-vim-registers)
- [How to Paste](https://stackoverflow.com/questions/3997078/how-to-paste-text-into-vim-command-line/3997110#3997110)
- [wikia:System Clipboard](http://vim.wikia.com/wiki/Accessing_the_system_clipboard)

### Jumps

A lot of commands allows to jump from one file to another or different positions within a file.
It is possible to move around the jump stack with

- `:ju[mps]`          list of jump position
- `<C-o>`             jumps back older position
- `<C-I>` or `<tab>`  jumps forward to newer position

Similarly the changes within the file are also remembered one has

- `:changes`          to list the changes
- `g;`                jumps back to older position in change list
- `g,`                jumps forward to newer position in change list

### closing files

If one wants to close the current buffer (e.g. to open it somewhere else) without leaving vim, one can use any of the following

- `:enew`   edits a new unamed buffer and thus frees the previous buffer
- `:bun`    unload buffer (buffer unload)
- `:bd`     unload buffer and delete it from buffer list (buffer delete)
- `:bw`     like :bd but really remove it from any list (buffer wipeout)

### arguments list

Examples

    :args *.gp
    :tab all

this is an alternative to

    $ vim -p *.gp

which work from within vim itself. Interestingly when callin that function the argument list is filled with all the gp files opens all the gp file in the directory. It replaces the currently opened tabs.

- `:args`           without argument list the argument list
- `:argadd file`    adds file to the argument list
- `:argdel file`    removes file from the argument list
    
### spell-checking
  
Activate spell checking

    :setlocal spell spelllang=en_gb

Deactivate

    :setlocal nospell

Some commands

- `zg` Add word under cursor/visually selected character to local dictionary
- `zug` Undo adding
- `zw` Mark a word as a bad one
- `zuw` Undo previous
- `z=` or `<C-x>` in insert mode Suggest correct word