# Tabs Browsing

Tabs is a great feature of vim! Some commands may be interesting

### Basic

- `:tabne[w]`
- `:tabe[dit] file`
- `:tabn[ext]` / `gt`
- `:tabp[rev]` / `gT`
- `:tabfind`
- `:tabclose`

### Slightly more advanced

- `<C-w> gf`       opens file under cursor in a new tab
- `<C-w> gF`       like previous, but jumps to line number
- `:tabm`          moves a tab
- `:tab help`      opens help in a tab
- `:tabdo {cmd}`   run cmd on all tabs. To some extend it is similar to `:bufo`
- `:tabs`          list all current tabs

### Move current buffer to its own tab
  
When the window is split, one can move the current buffer to its own tab using

    <C-w>T
    
See also [How do I move an existing window to a new tab](https://stackoverflow.com/questions/1758301/how-do-i-move-an-existing-window-to-a-new-tab#1761745)
