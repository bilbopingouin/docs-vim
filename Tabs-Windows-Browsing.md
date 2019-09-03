# Buffers / Tabs / Windows Browsing

Vim has great built-in features to browse and work with various files


<!-- vim-markdown-toc GFM -->

* [Buffers](#buffers)
	* [Basic](#basic)
	* [Intermediate](#intermediate)
		* [Workflow](#workflow)
		* [Buffer names](#buffer-names)
* [Tabs](#tabs)
	* [Basic](#basic-1)
	* [Slightly more advanced](#slightly-more-advanced)
	* [Move current buffer to its own tab](#move-current-buffer-to-its-own-tab)
* [Windows browsing](#windows-browsing)
	* [Create windows](#create-windows)
	* [Shift windows](#shift-windows)
	* [Move windows](#move-windows)

<!-- vim-markdown-toc -->

## Buffers

[Some](https://stackoverflow.com/q/26708822/3337196) claim that the ViM-way to handle files is to use buffers. Basically a way for vim to handle files. In a crude way, one file = one buffer. Windows and tabs are different ways to see a buffer. But there are buffer specific commands. 

See, e.g.
- [User buffers effectively](https://stackoverflow.com/a/21338192/3337196)

### Basic

```vim
:ls   " list the open buffer
:bn   "	open (show) the next buffer
:bp   " open (show) the previous buffer
:b N  " open buffer 'N'
:bun  " unload buffer
```

### Intermediate

```vim
:sb N	      " split the window and open the buffer 'N'
:vert sb N    " same as previous but with vertical split
:set hidden   " hide abandonne buffers
:bufdo	...   " run a command on all buffers
```

#### Workflow

When on a modified buffer, the command 

```vim
:bn
```

would be rejected, one would need to set

```vim
:bn!
```

This can be avoided, setting 

```vim
:set hidden
:bn
```

#### Buffer names

Instead of calling the buffer number ('N'), it might be possible to call it using the buffer name. This can also be used from matvhing the name, like



See also [Jumps](Various-Commands#jumps) and [Closing Files](Various-Commands#closing-files).

## Tabs

### Basic

```vim
:tabne[w]	  " create a new tab with an emtpy buffer
:tabe[dit] file	  " create a new tab and open the <file>
:tabn[ext]	  " switch to the next tab (right)
gt		  " same as above but in normal command
:tabp[rev]	  " switch to the previous tab (left)
gT		  " same as above but in normal command
:tabfind	  " Search a tab
:tabclose	  " Close a tab
```

### Slightly more advanced

```vim
<C-w> gf       " opens file under cursor in a new tab
<C-w> gF       " like previous, but jumps to line number
:tabm          " moves a tab
:tab help      " opens help in a tab
:tabdo {cmd}   " run cmd on all tabs. To some extend it is similar to `:bufo`
:tabs          " list all current tabs
```

### Move current buffer to its own tab
  
When the window is split, one can move the current buffer to its own tab using

```vim
<C-w>T
```
    
See also [How do I move an existing window to a new tab](https://stackoverflow.com/questions/1758301/how-do-i-move-an-existing-window-to-a-new-tab#1761745)

## Windows browsing

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

```vim
<C-w>K	" moves windows to top
<C-w>J	" moves windows to bottom
<C-w>H	" moves windows to left
<C-w>L	" moves windows to right
<C-w>T	" moves windows to a tab
```

See also [vim doc: window-moving](http://vimdoc.sourceforge.net/htmldoc/windows.html#window-moving).
