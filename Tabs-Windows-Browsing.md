# Tabs Browsing

Tabs is a great feature of vim! Some commands may be interesting


<!-- vim-markdown-toc GFM -->

		* [Basic](#basic)
		* [Slightly more advanced](#slightly-more-advanced)
		* [Move current buffer to its own tab](#move-current-buffer-to-its-own-tab)
* [Windows browsing](#windows-browsing)
		* [Create windows](#create-windows)
		* [Shift windows](#shift-windows)
		* [Move windows](#move-windows)

<!-- vim-markdown-toc -->

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

# Windows browsing

### Create windows

One can split the window into smaller windows using vertical and horizontal scripts. See [Open file within vim](Open-Commands#open-file-within-vim).

### Shift windows

It is then possible to move the windows around, for example, using

```vim
<C-w> r
```
moves the windows "clockwise".

See also [vim doc: window-moving](http://vimdoc.sourceforge.net/htmldoc/windows.html#window-moving).

### Move windows

It is also possible to set the windows to a given position:

- `<C-w>K` moves windows to top
- `<C-w>J` moves windows to bottom
- `<C-w>H` moves windows to left
- `<C-w>L` moves windows to right
- `<C-w>T` moves windows to a tab

See also [vim doc: window-moving](http://vimdoc.sourceforge.net/htmldoc/windows.html#window-moving).
