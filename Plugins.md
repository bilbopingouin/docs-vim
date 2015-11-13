# Plugins

### Twitvim configuration commands

    let twitvim_browser_cmd = 'iceweasel'let twitvim_count = 50


### List of notable plugins
  
- alternate: allows easy switch between .c and .h files
- cvim: adds a lot of functionalities to vim for C/C++ development. It tends to be a bit too intrusive for when not working with C
- echofunc: together with tags, it allows to echo the function declaration in C/C++. (§)
- fugitive: a few commands for git, like adding the branch name in the vim status bar. (§)
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
        
`:SudokuEasy` starts it. It does not work here, because it requires python options
        
- [Sokoban](http://www.vim.org/scripts/script.php?script_id=211)
        
`:Sokoban` starts it