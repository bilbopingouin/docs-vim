# Configuration

### Leader character

```
" leader
let mapleader = ',' " default is \ but on a French keyboard , is easier
set showcmd         " see that we have typed the leader and other commands
                    " not sure that work...
```

### Status line

```
"Set the status line
set statusline=%<%f\ %h%m%r%=%-14.(%l,%c%V%)\ %P
```
I can see the line/columns as well as the position within the file. Using `<C-g>`, I can also get some info on the file.


### Cursor

Show positions of the cursor within the file

    :se ruler

### backspace

As default backspace behave like in vi, which is not the typical behaviour of backspace

```
" For backspace to delete the previous character
set backspace=indent,eol,start
```

### Line break on the right of screens.

In vim the lines are wrapped when arriving at the right end of a window. Should the word be cut or not?

```
" Not cutting the end of the words
:se lbr
```

### Indentation

Code is always better presented with the correct indentation. But the POSIX/Linux standard is that a <Tab> is 8 <Space>s. This is a lot, especially on smaller/splitted screens.
That behaviour can be improved by setting:

```
" Keep the linux standart (when using other editors: less, a2ps...)
:se tabstop=8
" Make it using spaces in indenting: so that it looks reasonnable
"(8 spaces being much too large).
:se softtabstop=2
:se shiftwidth=2
:se noet
```
    
Typing <Tab> will then produce two <Space>s, and automatic indenting as well. But when 4 <Tab>s or 8 <Space>s are introduced a real <Tab> appears. That way, file edited with this configuration can still be seen by others and respect the standard.

See also: vim: [programming](Programming)