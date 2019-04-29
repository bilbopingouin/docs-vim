# Browsing

Opening a directory with vim starts the netrw process.

`F1` provides related help

A few commands are worth remembering:

- `mf` - toggles marking of a file
- `mu` - unmarks all
- `me` - opens all marked file (accessible via :next and :prev)
- `mx` - execute a command on all selected files
- `d` - creates a new directory
- `D` - deletes a file
- `o` or `v` or `p` allows to open the file in a split window (`p` opens RO)
- `t` open the file in a new tab (`T` does it in the background)
- `i` change view: vertical / long / horizontal / tree (note that opening files and tree view is not optimum)
- `a` shows/hides files from a list (notes that `gh` does the same for dot-files) and `<C-h>` allows to edit that file list

note that with `t`, `o`, `P`, `v` or `enter` (which essentially does one of the previous depending on `g:netrw_browse_split`), the file/buffer is loaded in memory. Thus, it appears in `:files`. But it is not the case with `p`. For browsing a large number of files, `p` is probably preferable then.


It is also possible to call the browsing ayntime using one of the following

- `:E[xplore]`
- `:Ve[xplore]` splits vertically and run Explore
- `:Te[xplore]` run Explore in a tab
- `:Re[xplore]` returns to the last exploration (after opening a file)


One can also define a few variables in a `.vimrc`:

```vim
map <F9> :Vexplore<CR>                " calls Vexplore faster
let g:netrw_list_hide = '^\.[a-zA-Z]' " hide linux hidden files: toggle with 'a'
let g:netrw_preview   = 1             " split vertically for previews: opens vertically using 'p'
let g:netrw_alto      = 1             " split above/below for opening: using 'o'
let g:netrw_liststyle = 3             " defaults showing tree: toggle using 'i', careful when opening
let g:netrw_winsize   = 30            " browing window occupy 30% after opening file
```

[Reference](https://stackoverflow.com/questions/5006950/setting-netrw-like-nerdtree).
