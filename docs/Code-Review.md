# Code Review

Most of those commands are already listed somewhere else, but in order to regroup them together, here we are.


<!-- vim-markdown-toc GFM -->

* [Generate tags](#generate-tags)
* [Browsing](#browsing)
* [File jumping](#file-jumping)
* [Searching for the files](#searching-for-the-files)
* [marking points](#marking-points)
* [folding](#folding)
* [Combining `cscope`, `ctag` and `vim`](#combining-cscope-ctag-and-vim)
	* [cscope](#cscope)
	* [cscope and vim](#cscope-and-vim)
	* [ctags](#ctags)
	* [Vim, cscope and ctags](#vim-cscope-and-ctags)
	* [Specific configuration](#specific-configuration)

<!-- vim-markdown-toc -->

### Generate tags

Tag files are a way to jump more easily to functions/objects definitions.

Generate a sort of toc of all the functions defined in the recognised files

    $ ctags -R

or

    $ ctags -R --fields=+ilmS path

It's often a good idea to run that command outside of a git repo, or use a global gitignore to ignore the `tags` file thus created.

It is then possible to call vim using

    $ vim -t main  

to get to the main function, regardless where that function is defined!

In `.vimrc` a few commands are useful (see [Ref.](http://amix.dk/blog/post/19329))

```vim
let Tlist_Ctags_Cmd = "/usr/bin/ctags"
let Tlist_WinWidth = 50
map <leader>tl :TlistToggle<cr>
" Regenerating the current tags set
map <leader>tu :!/usr/bin/ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>

" List matches in interactive mode
map <leader>tm [I:let nr = input("Which one: ")<Bar>exe "normal " . nr ."[\t"<CR>
```

Some useful commands related to it
- `:tag function`	  jumps to the definition of that function
- `:tag /function`	  list all the matching tags
- `<C-]>`		  jumps to the tag of the function of the cursor
- `:tags`		  list the stack (previous) of tag jumps
- `<C-t>` or `:po[p]`	  jumps to previous entry in tag stack
- `:tag`		  jumps to newer tag
- `:0tag`		  jumps to most recent
- `:tj  [pattern]`	  list all matching tag or jump to it when there is only one
- `g]`			  list all tags related to the cursor position
- `:pt[ags]` or `<C-w> }` shows tag in a preview window (close with `<C-w> z` or `:pcl[ose]`)

See also [Browsing programs with tags](http://vim.wikia.com/wiki/Browsing_programs_with_tags)


### Browsing

With current configuration, `<F9>` allows to start a file browser on the left of vim window

- `t`	  to open in a new tab
- `P`	  to open in a previous panel
    
- `p`	  to split the screen open file RO 
    
- `<F9>`  to remove browsing

More can be found with `:h netrw`.

### File jumping    

From the `a.vim` plugin,
- `:A`	  switches to header
- `:AT`	  switches to header in a new tab

Built-in functions
- `<C-w>, f` opens file under cursor
- `<C-o>`    jumps back
    
### Searching for the files

- `:lvimgrep **/* bob`	searches bob recursively in all files
- `:lopen`		open the result list
- `:lcl[ose]`		close the result list
- `<C-Right>`		jumps to next element in location list
- `<C-Left>`		jumps to previous element in location list
    
### marking points

- `ma`	    marks a point `a`
- `` `a``	    jumps to point `a`
- `:marks` shows the list of marks

See also [Various Commands](Various-Commands#marks)
    
### folding

- `zR` opens all folds
- `zO` opens a single fold (with sub folds)
- `zc` closes a single fold
- `zM` closes all folds in current line

### Combining `cscope`, `ctag` and `vim`

References

- [cscope, ctags, & vim](https://www.fsl.cs.sunysb.edu/~rick/cscope.html)
- [cscope, ctags and vim](http://www.pragmarallel.com/?p=223)
- [The Vim/Cscope tutorial](http://cscope.sourceforge.net/cscope_vim_tutorial.html)
- [How to use cscope?](https://stackoverflow.com/questions/3828157/how-to-use-cscope)
- [Effortless Ctags with Git](https://tbaggery.com/2011/08/08/effortless-ctags-with-git.html)

#### cscope

As a standalone, one can use `cscope` as

    $ cscope -R
    
with simple help provided in `man cscope` or `cscope --help`.

One gets:

> Find this C symbol:  
  Find this global definition:  
  Find functions called by this function:  
  Find functions calling this function:  
  Find this text string:  
  Change this text string:  
  Find this egrep pattern:  
  Find this file:  
  Find files #including this file:  
  Find assignments to this symbol:
  
We can enter the function/symbol in the appropriate line (using arrows) and then press `<enter>`.
The result appears at the top of the shell. It's possible to switch between the result and search functions using `<tab>`.
When pressing `<enter>` on a result line, the file will be opened at the given line (`vim` by default).
To leave, one needs to use `<C-d>`.

One can navigate more rapidly using a database. This could be done using the following commands

```bash
$ find /path/project/dir -name '*.[ch]' -print > /path/project/dir/cscope.files
$ cscope -b -q
```
    
And then run `cscope` again will provide faster results.

See also: [cscope](https://vim.fandom.com/wiki/Cscope).

#### cscope and vim

There is a plugin file provided for `cscope` as [cscope_maps.vim](http://cscope.sourceforge.net/cscope_maps.vim).

And `vim` should be compiled with `+cscope`.

#### ctags

There is an [Exuberant CTAGS](http://ctags.sourceforge.net/) plugin for `vim`.

Example usage (see also above)

    ctags -R -h="h.c.cu" --c-kinds=+p --if0=yes --totals=yes -f tags

#### Vim, cscope and ctags

- Generate the databases

  ```bash
  $ find /dir -name '*.[ch]' -print > cscope.files
  $ cscope -b
  $ ctags -L cscope.files -R -h="h.c.cu" --c-kinds=+p --if0=yes --totals=yes -f tags
  ```
    
- Usage: some useful commands

  - `<C-\>s`    shows the list of usage of a given symbol
  - `<C-\>c`    Find functions calling this function
  - `<C-\>g`    Find this definition
  - `<C-\>d`    Find functions called by this function
  - `<C-\>t`    Find this text string
  - `<C-\>e`    Find this egrep pattern
  - `<C-\>f`    Find this file
  - `<C-\>i`    Find files #including this file
  - `<C-t>`     jumps back
    
- Keep DB up to date

  One can use some scripts to update it regularly, but for starter, I will keep it manually.

#### Specific configuration

We can configure the following command

```vim
<C-d> ::exec("tselect ".expand("<cword>"))<CR>
```

which allows to search the current word's definition.

### FZF

[Fuzzy Finder](https://github.com/junegunn/fzf.vim) adapted for vim. It offers various commands to search files or other elements. In particular,

- `:Files` allows to search the file names in sub directories
- `:Maps` search in the defined maps
- `Rg` content of files

### Any-jump

Uses rg or ag to search for code elements. More on [github](https://github.com/pechorin/any-jump.vim). 

Simply use `<leader>j` on any element within a code.
