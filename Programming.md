# Programming

### indenting

Activate indent

```vim
:filetype indent on
```

Deactivate indent

```vim
:filetype indent off
```

See also [Ref](http://vimdoc.sourceforge.net/htmldoc/usr_30.html#30.3)

Indent with respects with C programming

```vim
:se cindent
```

Probably better still

```vim
au FileType c,cpp set cindent " activates cindent but only for these types of files
```

See also the [indentation configuration](Configuration#indentation)

The various indent methods are
- `autoindent`:     keep the previous line indent
- `smartindent`:    like autoindent, but with some cindent recognition
- `cindent`:        more clever than previous and configurable
- `indentexpr`:     more flexible version
- `noindent`:       no automatic indentation
    
cindent options:
- `cinkeys`:    keys trigger in insert mode  
  default: `0{,0},0),:,0#,!^F,o,O,e`  
  indent if  
  - `{`, `}`, `)` or `#` as first character in a line
  - `:`   after a label/case
  - `<ctrl-F>`
  - `<CR>`, `o` or `O` (not in insert)
  - `e`   second e of `else` at the start of a line
- `cinword`:    keywords 
  default: `if,else,while,do,for,switch` 
- `cinoptions`: prefered indent style  
  default value: '' (empty)  
  specific default: `>s,e0,n0,f0,{0,}0,^0,L-1,:s,=s,l0,b0,gs,hs,N0,ps,ts,is,+s,c3,C0,/0,(2s,us,U0,w0,W0,k0,m0,j0,J0,)20,*70,#0`
  - `>s`: normal indent set to shiftwidth
  - `e0`: indent inside of brace (offset to normal), can have e2 or e-2 to add or remove two spaces
  - `n0`: indent after an if
  - `f0`: opening brace as start of line
  - `{0`: brace inside of braces
  - `}0`: difference between closing and opening brace
  - `^0`: prevailing inside a set of braces
  - `L-1`:labels (goto)
  - `:s`: case label
  - `=s`: case content
  - `l0`: case content / statements
  - `b0`: break w.r.t. case label
  - `gs`: public/private of C++
  - `hs`: like =s for public/private of C++
  - `N0`: Namespace C++
  - `ps`: K&R-style func(a,b)  
    int a;  
    int b;  
  - `ts`: return type in function declaration
  - `is`: C++ base-class & constructor
  - `+s`: continuation line
  - `c3`: comments
  - `C0`: comments override
  - `/0`: Comment lines
  - `(2s`: Unclosed parentheses
  - `us`: Same as above but deeper
  - `U0`: Unclosed parentheses
  - `w0`: Unclosed parentheses
  - `W0`: Unclosed parentheses
  - `k0`: if unclosed parentheses
  - `m0`: opening/closing parentheses
  - `j0`: Java anonymous class
  - `J0`: Javascript object
  - `)20`: Max lines for search closing parentheses
  - `*70`: Max lines searching for closing comment
  - `#0`: # are preprocessors and not comments
		
Removing indent when pasting

```vim
set paste
```

Re-enabling

```vim
set nopaste
```

Toggling

```vim
set pastetoggle=<F10>
```
    
### Tab/spaces

Keep the linux standart (when using other editors: less, a2ps...)

```vim
:se tabstop=8
```

Make it using spaces in indenting: so that it looks reasonnable
(8 spaces being much too large).

```vim
:se softtabstop=2
:se shiftwidth=2
:se noet
```

From the manual:

> There are four main ways to use tabs in Vim:  
    1. Always keep 'tabstop' at 8, set 'softtabstop' and 'shiftwidth' to 4
       (or 3 or whatever you prefer) and use 'noexpandtab'.  Then Vim
       will use a mix of tabs and spaces, but typing <Tab> and <BS> will
       behave like a tab appears every 4 (or 3) characters.  
    2. Set 'tabstop' and 'shiftwidth' to whatever you prefer and use
       'expandtab'.  This way you will always insert spaces.  The
       formatting will never be messed up when 'tabstop' is changed.  
    3. Set 'tabstop' and 'shiftwidth' to whatever you prefer and use a
       |modeline| to set these values when editing the file again.  Only
       works when using Vim to edit the file.  
    4. Always set 'tabstop' and 'shiftwidth' to the same value, and
       'noexpandtab'.  This should then work (for initial indents only)
       for any tabstop setting that people use.  It might be nice to have
       tabs after the first non-blank inserted as spaces if you do this
       though.  Otherwise aligned comments will be wrong when 'tabstop' is
       changed.

- `tabstop`:        number of spaces that a tab counts for (how a tab is shown)
- `softtabstop`:    number of spaces that a tab counts for when editing (pressing <tab>) / inserts a mix of tabs and spaces
- `shiftwidth`:     number of spaces for indentation
- `expandtab`:      inserts spaces instead of actual tabs
- `retab`:          replace tabs with N white spaces defined by tabstop

See [Vim-doc](http://vimdoc.sourceforge.net/htmldoc/usr_30.html#30.5)

Convert tabs to spaces

```vim
:set expandtab
:retab!
```

Convert spaces to tabs

```vim
:set noexpandtab
:retab!
```

The option 'list' allows to visualize the tabs/spaces

```vim
:set list
```

We will have `^I` to indicate a tab, and `$` to mark the end of the line. `:help 'line'`
It is possible to customize the output as, e.g., 

```vim
:set listchars=tab:▸_,eol:¬,space:·
```

See more on `:help 'listchars'`
It is also possible to change the colour by using

```vim
:hi NonText ctermfg=darkgrey
:hi SpecialKey ctermfg=darkgrey
```
 
### Syntax highlighting

See colours of the syntax

```vim
if &t_Co > 1	
  syntax enable
endif
```

### un/comment in Visual

Insert a line comment at the beginning of the line.

```vim
let b:comment_leader = '' " default value
au FileType vim		let b:comment_leader = '" '
au FileType c,css   	let b:comment_leader = '// '
au FileType cpp     	let b:comment_leader = '// '
au FileType sh,make 	let b:comment_leader = '# '
au FileType tex     	let b:comment_leader = '% '
au FileType vhdl    	let b:comment_leader = '-- '
au FileType python  	let b:comment_leader = '# '
au FileType ruby    	let b:comment_leader = '# '
au FileType javascript  let b:comment_leader = '// '

noremap ,c : <C-B>sil <C-E>s/^/<C-R>=escape(b:comment_leader,'\/')<CR>/<CR>:noh<CR>
noremap ,u : <C-B>sil <C-E>s/^\V<C-R>=escape(b:comment_leader,'\/')<CR>//e<CR>:noh<CR>
```

The drawback is that it requires to define them for each language.

### C inserting

The plugin: `c-plugin`

    filetype plugin on

Documentation:
- [The Geek Stuff](http://www.thegeekstuff.com/2009/01/tutorial-make-vim-as-your-cc-ide-using-cvim-plugin/)
- [Cheat Sheet](http://lug.fh-swf.de/vim/vim-c/c-hotkeys.pdf) (PDF)
- [ViM.org](http://www.vim.org/scripts/script.php?script_id=213)

As `vim-latex`, this is too invasive! I can use a cheap solution

    noremap <leader>hc :r ~/.vim/templates/chead.c<CR>
    noremap <leader>fc :r ~/.vim/templates/cfunc.c<CR>

other alternative

```vim
source ~/.vim/scripts/ReadSkeleton.vim

nmap <F4> :call ReadSkeleton()<cr>

let Skeleton_path = "~/.vim/templates"
```

with ~/.vim/scripts/ReadSkeleton.vim as

```vim
function! ReadSkeleton()
  if exists ("g:Skeleton_path")
    let skeleton_path = g:Skeleton_path
  else
    let skeleton_path = getcwd()
  endif
  let filenameList = split (glob ( skeleton_path . "/*.*") , "\n")
  let filenameList = insert (filenameList, "Select skeleton to load")
  let choiceList = copy (filenameList)
  let choiceList = map (choiceList, 'index(filenameList,v:val) .". ". v:val')
  let choiceList[0] = "Select skeleton to load"
  let listLen = len(choiceList)
  let choiceList = add (choiceList, listLen . ". Browse for some other folder (gui ONLY)")
  let choice = inputlist(choiceList)
  let skeletonName = ""
  if choice == listLen
    "Do the browse thingie if possible
    if has("browse")
      let skeletonName = browse(0,"Select session to restore",skeleton_path,"")
      echo skeletonName
    endif
  elseif choice > 0
    "Load the file
    let skeletonName = filenameList[choice]
    echo "setting skeletonName to ".skeletonName
  endif
  if skeletonName != ""
    execute "0read " . skeletonName
  endif
endfunction
```

It might be interesting, when using templates, to insert some values automatically. E.g.

```vim
function! SetTemplValues()
    if search("|YEAR|") != 0
	:echo "Substitute |YEAR|"
	:%s/|YEAR|/\=strftime("%Y")/g
    endif
    if search("|DATE|") != 0
	:echo "Substitute |DATE|"
	:%s/|DATE|/\=strftime("%Y-%m-%d")/g
    endif
    if search("TIME") != 0
	:echo "Substitute |TIME|"
	:%s/|TIME|/\=strftime("%H:%M")/g
    endif
    if search("|FILENAME|") != 0
	:echo "Substitute |FILENAME|"
	:%s/|FILENAME|/\=expand("%:t")/g
    endif
    if search("|MODULE|") != 0
	:echo "Substitute |MODULE|"
	:%s/|MODULE|/\=input("Module name: ")/g
    endif
    if search("|AUTHOR|") != 0
	:echo "Substitute |AUTHOR|"
	if exists("g:author_name") != 0
	    :%s/|AUTHOR|/\=expand(g:author_name)/g
	else
	    :%s/|AUTHOR|/\=input("Author name: ")/g
	    :echo "."
	endif
    endif
    if search("|AUTHSHORT|") != 0
	:echo "Substitute |AUTHSHORT|"
	if exists("g:author_short") != 0
	    :%s/|AUTHSHORT|/\=expand(g:author_short)/g
	else
	    :%s/|AUTHSHORT|/\=input("Author short name: ")/g
	    :echo "."
	endif
    endif
    if search("|EMAIL|") != 0
	:echo "Substitute |EMAIL|"
	if exists("g:author_short") != 0
	    :%s/|EMAIL|/\=expand(g:author_email)/g
	else
	    :%s/|EMAIL|/\=input("Email address: ")/g
	    :echo "."
	endif
    endif
    if search("|COMPANY|") != 0
	:echo "Substitute |COMPANY|"
	if exists("g:author_short") != 0
	    :%s/|COMPANY|/\=expand(g:author_company)/g
	else
	    :%s/|COMPANY|/\=input("Company name: ")/g
	    :echo "."
	endif
    endif
    if search("<CURSOR>") != 0
	:echo "Reaching <CURSOR>"
	:call search("<CURSOR>")
	:normal 8x
	:startinsert
    endif
endfunction
```


### Compiling

- Manual way

  Compile and show result in a split screen in `.vimrc`:

  ```vim
  map <F7> :w<enter>:tabnew<enter>:r!make<enter>
  ```

- Quickfix

  If a Makefile is defined, run

      :make

  then the errors are stored in the quickfix error file some commands are then useful

  - `:copen` 	" open error list
  - `:ccl[ose]` "close error list
  - `:cl`       " list errors
  - `:col`     	" open old error file
  - `:cnew` 	" open new error file
  - `:cr`      	" jump to first error
  - `:cn`     	" jump to next error
  - `:cp`     	" jump to previous error
  - `:cnf`    	" jump to first error in next file
    
  This can be compiled with the default compilation options

  Since there are some default compilation one can also

  ```vim
  au FileType c,cpp set makeprg=make\ %:r
  ```

  then calling 'make' will result in either calling the Makefile OR using default

  ```vim
  au FileType c,cpp nmap <F7> :make<CR>
  ```

    
### Run compiled/script
  
```vim
au FileType c,cpp               nmap <buffer> <C-l> :!./%<<CR>
au FileType python,perl,bash,sh nmap <buffer> <C-l> :!./%<CR>
au FileType gnuplot             nmap <buffer> <C-l> :!gnuplot %<CR>
au FileType octave              nmap <buffer> <C-l> :!octave %<CR>
```
    
For auto-executable scripts one can run

    :!chmod +x %

to make the script executable before.


### Switch fast between files for C/C++ code

[Script Reference](http://www.vim.org/scripts/script.php?script_id=31)

### Using ctags

    $ ctags -R     

will generate a sort of toc of all the functions defined in the recognised files.

It is then possible to call vim using

    $ vim -t main

to get to the main function, regardless where that function is defined!

In .vimrc a few commands are useful, see [that reference](http://amix.dk/blog/post/19329)

For taglist plugin

```vim
let Tlist_Ctags_Cmd = "/usr/bin/ctags"
let Tlist_WinWidth = 50
map <leader>tl :TlistToggle<cr>

" Regenerating the current tags set
map <leader>tu :!/usr/bin/ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>
```

List matches in interactive mode

```vim
map <leader>tm [I:let nr = input("Which one: ")<Bar>exe "normal " . nr ."[\t"<CR>
```

Some useful commands related to it
- `:tag function`         jumps to the definition of that function
- `:tag /function`        list all the matching tags
- `<C-]>`                 jumps to the tag of the function of the cursor
- `:tags`                 list the stack (previous) of tag jumps
- `<C-t>` or `:po[p]`     jumps to previous entry in tag stack
- `:tag`                  jumps to newer tag
- `:0tag`                 jumps to most recent
- `:tj  [pattern]`        list all matching tag or jump to it when there is only one
- `g]`                    list all tags related to the cursor position
- `:pt[ags]` or `<C-w> }` shows tag in a preview window (close with <C-w> z or :pcl[ose])

More in the [wikia](http://vim.wikia.com/wiki/Browsing_programs_with_tags) and [Code_review](code-review)

