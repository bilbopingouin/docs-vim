# Configuration

### Leader character

Leader is a character often used as a prefix for other commands.

By default, it is the character `\`, but on some keyboards (e.g. French one) that key is
not easily accessed. It can be changed to something else with
```
let mapleader = ','
```

### Print last command at the bottom line

```
set showcmd         " see that we have typed the leader and other commands
                    " not sure that work...
```

### Status line

The status line can be configured and customised. For example, one can

```
set statusline=%<%f\ %h%m%r%=%-14.(%l,%c%V%)\ %P
```

I can see the line/columns as well as the position within the file. Using `<C-g>`, I can also get some info on the file.


### Cursor

Show positions of the cursor within the file

```
set ruler
```

### backspace

As default backspace behave like in vi, which is not the typical behaviour of backspace. The usual behaviour can be obtained using

```
set backspace=indent,eol,start
```

### Line break on the right of screens.

In vim the lines are wrapped when arriving at the right end of a window. Should the word be cut or not?

Keeping full words can be done with
```
set lbr
```

### Indentation

Code is always better presented with the correct indentation. But the POSIX/Linux standard is that a `<Tab>` is 8 `<Space>`s. This is a lot, especially on smaller/splitted screens.
That behaviour can be improved by the following settings

Keep the linux standart (when using other editors: less, a2ps...)
```
set tabstop=8
```

Make it using spaces in indenting: so that it looks reasonnable (8 spaces being much too large).
```
set softtabstop=2
set shiftwidth=2
set noet
```
    
Typing `<Tab>` will then produce two `<Space>`s, and automatic indenting as well. But when 4 `<Tab>`s or 8 `<Space>`s are introduced a real `<Tab>` appears. That way, file edited with this configuration can still be seen by others and respect the standard.

Note that the `noet` (no expandtab) may lead to mixed spaces and tabs (not suitable for Python3).

See also: vim: [programming](Programming)
