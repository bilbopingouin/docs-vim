# Syntax / Coloring



## Syntax


## Colours

### Find the colours available

One could use the following code

```vim
let num = &t_Co-1
while num >= 0
    exec 'hi col_'.num.' ctermbg='.num.' ctermfg=white'
    exec 'syn match col_'.num.' "ctermbg='.num.':...." containedIn=ALL'
    call append(0, 'ctermbg='.num.':....')
    let num = num - 1
endwhile
```

In a file, and sumply running `:so filename`. This will show all the different colours available. The code is adapted from [Vim's wiki](https://vim.fandom.com/wiki/Xterm256_color_names_for_console_Vim).

### Colours names

Some colours have specific names, in particular:

- black
- blue
- brown
- cyan
- darkblue
- darkcyan
- darkgray
- darkgreen
- darkgrey
- darkmagenta
- darkred
- darkyellow
- gray
- green
- grey
- lightblue
- lightcyan
- lightgray
- lightgreen
- lightgrey
- lightmagenta
- lightred
- magenta
- red
- white
- yellow

### Test configuration

Run the following

```vim
:runtime syntax/colortest.vim
:so %
```

See also `:h colortest`.
