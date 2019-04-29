# Plugins

### Twitvim configuration commands

    let twitvim_browser_cmd = 'iceweasel'let twitvim_count = 50


### List of notable plugins
  
- alternate: allows easy switch between .c and .h files
- cvim: adds a lot of functionalities to vim for C/C++ development. It tends to be a bit too intrusive for when not working with C
- DrawIt: allows to draw diagrams within vim
- echofunc: together with tags, it allows to echo the function declaration in C/C++. (§)
- fugitive: a few commands for git, like adding the branch name in the vim status bar. (§)
- recover: adds an option "Compare" when recovering from a swap file
- solarized: colorscheme for vim. (§)
- ttagecho: similar to echofunc.
- twitvim: allows to interact with the twitter API from within vim. 
- undotree: allows a graphical visualisation of the undo history (useful when using a combination or undo/redo together with branches). (§)
- vim-games: 4 games in one. (§)
- vim-surround: allows to surround words or sentences with signs and/or tags as well as edit them. Great for HTML/XML things. (§)
- vim-latex: transforms vim into a LaTeX IDE. As for cvim, it might be considered too intrusive, namely defining too many things, making it unpracticable when editing other types of documents.
  
§ currently loaded
  
### vim-surround

Some commands
    
- change surrounding: `cs+pattern+new-pattern`
  - `cs"'`        changes "hello" into 'hello'
  - `cs"<q>`      changes "hello" into <q>hello</q>
  - `cst"`        changes <q>hello</q> into "hello"
  - `cs"[`        changes "hello" into [ hello ]
  - `cs"]`        changes "hello" into [hello]
- remove surrounding: ds+pattern
  - `ds"`         changes "hello" into hello
        
- insert surrounding: ys+range+pattern
  - `ysiw]`       changes hello into [hello]
        
  - `iw`      text object
  - `s`       sentence
    
- surround visual: 
  - `S)`          surrounds selected text by ( and )
        
as a pattern it is possible to use `t` (tag) as illustrated above. If it is the new pattern, it will ask which one it is.
    
[Ref.](http://www.vim.org/scripts/script.php?script_id=1697)
    
### echofunc

run

    ctags -R --fields=+ilmS
    
when entering a function, and typing the `(,` the function declaration will be shown
  
[Ref.](http://www.vim.org/scripts/script.php?script_id=1735)
  
### vim-games
  
[Ref.](https://github.com/jmanoel7/vim-games)

contains
  
- [Tetris](http://www.vim.org/scripts/script.php?script_id=172)
        
  - `<leader>te`  start 
  - `h`           left
  - `l`           right
  - `i/k`         flip
  - `j`           down
  - `<space>`     drop
  - `q`           leave

- [Sudoku](http://www.vim.org/scripts/script.php?script_id=3553)
        
`:SudokuEasy` starts it. It requires python options
        
- [Sokoban](http://www.vim.org/scripts/script.php?script_id=211)
        
`:Sokoban` starts it

### pathogen
  
Allows to keep plugins each in its separate directory.

[Ref.](https://www.vim.org/scripts/script.php?script_id=2332)

Install

    cp pathogen.vim .vim/autoload/

Config (in .vimrc, at the top, add)

    call pathogen#runtime_append_all_bundles()
    call pathogen#helptags()
        
### Fugitive

References

- [Vimcasts](http://vimcasts.org/categories/git/)
- [VI.SE](https://vi.stackexchange.com/questions/17117/diffpatch-using-the-output-of-git-diff-directly)

General git command

    :Git

For example

    :Git log
    :Git tree           Using the .gitconfig alias

Help

    :help fugitive-commands

Combining with vim

    :Git add %
    :Git rm %
    :Git mv % new-name
    :Git checkout %

But fugitive has specific commands for those

    :Gwrite
    :Gremove
    :Gmove new-name
    :Gread

and those are slightly more advanced (buffer cleanup and/or reopening, etc.)
Note that path are either relative to the current directory or the root of the git repo

    :Gmove ../npath/nname
    :Gmove /npath/nname

Other commands

    :Gcommit        | git commit
    :Gblame         | git blame on the current file, but with split window
    :Gstatus        updates automatically
	<C-n>       jumps to the next file
	-           runs git add on the current file
		    or git reset if was already staged
	p           git add --patch
	<enter>     opens the selected file
	C           git commit
    :Gdiff              vimdiff with split window
	:Gwrite         on working copy: runs git add
			on indexed copy: runs git reset
	:Gread          inversed of Gwrite
	:w              on indexed. If some diffget was done, that change gets staged
	on a conflicted file, shows 3-ways diff
	:Gdiff <hash>       vimdiff on the current file with past modifs
	:Gdiff branch-name  same
    :Gedit
	:Gedit :path/file               opens indexed version of file
	:Gedit :0                       opens indexed version of current file
	:Gedit branchname:path/file     opens file from an another branch
	works on all git objects (blobs/trees/commits/tags)
	:Gedit <commit-hash>
	    <enter>                     opens the commit indicated on the line (parent)
					opens the tree whose hash is on that line
					inspects the blob of the tree
					runs vimdiff when selecting diff-line on a commit buffer
	    a                           does a git ls-tree on the currently selected tree
	    C                           opens the commit object of the current tree
	:Gedit <commit-hash>:file/name  opens the version of the given file during the commit
    :Gbrowse                        opens GitHub
    :Glog                           prints git log for the given file and fill the quicklist
	:cnext                      jumps to the previous version of the file
	:cprev                      jumps to the more recent version of the file
	:copen                      open the quickfix windows
	:Glog -10
	:Glog -10 --reverse
	:Glog -1 --until=yesterday
	:Glog --                    git log of all the commits
	:Glog -- %                  list of commits that affects the current file in the quickfix
	:Glog --grep=pattern --     only lists commits which have pattern in the description
	:Glog -Spattern             lists commits where pattern was added or removed from code
    :Ggrep              git grep and fill the quickfix window
	:Ggrep pattern              looks for 'pattern' in all tracked files
	:Ggrep pattern branch-name  looks for 'pattern' in branch 'branch-name'
	
Avoid increasing a list of buffers too much:

    autocmd BufReadPost fugitive://* set bufhidden=delete
    
### Alignments
  
- Own implementation (aka not plugin)

```vim
" http://www.ibm.com/developerworks/library/l-vim-script-2/index.html
function! AlignAssignments ()
    "Patterns needed to locate assignment operators...
    let ASSIGN_OP   = '[-+*/%|&]\?=\@<!=[=~]\@!'
    let ASSIGN_LINE = '^\(.\{-}\)\s*\(' . ASSIGN_OP . '\)'

    "Locate block of code to be considered (same indentation, no blanks)
    let indent_pat = '^' . matchstr(getline('.'), '^\s*') . '\S'
    let firstline  = search('^\%('. indent_pat . '\)\@!','bnW') + 1
    let lastline   = search('^\%('. indent_pat . '\)\@!', 'nW') - 1
    if lastline < 0
        let lastline = line('$')
    endif

    "Find the column at which the operators should be aligned...
    let max_align_col = 0
    let max_op_width  = 0
    for linetext in getline(firstline, lastline)
        "Does this line have an assignment in it?
        let left_width = match(linetext, '\s*' . ASSIGN_OP)
    
        "If so, track the maximal assignment column and operator width...
        if left_width >= 0
            let max_align_col = max([max_align_col, left_width])

	    let op_width      = strlen(matchstr(linetext, ASSIGN_OP))
	    let max_op_width  = max([max_op_width, op_width+1])
	endif
    endfor

    "Code needed to reformat lines so as to align operators...
    let FORMATTER = '\=printf("%-*s%*s", max_align_col, submatch(1),
    \                                    max_op_width,  submatch(2))'

    " Reformat lines with operators aligned in the appropriate column...
    for linenum in range(firstline, lastline)
        let oldline = getline(linenum)
        let newline = substitute(oldline, ASSIGN_LINE, FORMATTER, "")
        call setline(linenum, newline)
    endfor
endfunction

nmap <silent>  ;=  :call AlignAssignments()<CR>
```

turns
    a = 1;
    b2 = 3;
into
    a  = 1;
    b2 = 3;
    
- Align / AlignMaps

[Ref. vim.org](https://www.vim.org/scripts/script.php?script%5Fid=294)
    
There are many commands like

```
:[range]Align =         Align on the = signs
:[range]Align =*+-      Align on the * + or - signs
```
	
And some shortcuts, usually `<leader>t` followed by

    `=`           Align assigments
    `,`           Align on commas
    `sp`          Align on spaces
    `t`           Align on tabs

Some other use `<leader>a` followed by

    `com`         C-comments
    `dec`         C functions declarations (parameters)

