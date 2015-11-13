# Programming

### indenting

Indent with respects with C programming

    :se cindent

Probably better still

    au FileType c,cpp set cindent " activates cindent but only for these types of files

See also the [indentation configuration](Configuration#indentation)


### Syntax highlighting

See colours of the syntax

    if &t_Co > 1	
      syntax enable
    endif

### un/comment in Visual

    let b:comment_leader = '' " default value
    au FileType vim     let b:comment_leader = '" '
    au FileType c,css   let b:comment_leader = '// '
    au FileType cpp     let b:comment_leader = '// '
    au FileType sh,make let b:comment_leader = '# '
    au FileType tex     let b:comment_leader = '% '
    au FileType vhdl    let b:comment_leader = '-- '
    au FileType python  let b:comment_leader = '# '
    au FileType ruby    let b:comment_leader = '# '
    au FileType javascript    let b:comment_leader = '// '

    noremap ,c : <C-B>sil <C-E>s/^/<C-R>=escape(b:comment_leader,'\/')<CR>/<CR>:noh<CR>
    noremap ,u : <C-B>sil <C-E>s/^\V<C-R>=escape(b:comment_leader,'\/')<CR>//e<CR>:noh<CR>

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

    :so ~/.vim/scripts/ReadSkeleton.vim
    nmap <F4> :call ReadSkeleton()<cr>
    let Skeleton_path = "~/.vim/templates"
    with ~/.vim/scripts/ReadSkeleton.vim as
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

### Compilation

- Manual way

  Compile and show result in a split screen in `.vimrc`:

    map <F7> :w<enter>:tabnew<enter>:r!make<enter>

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

    au FileType c,cpp set makeprg=make\ %:r

  then calling 'make' will result in either calling the Makefile OR using default

    au FileType c,cpp nmap <F7> :make<CR>

    
### Run compiled/script
  
    au FileType c,cpp               nmap <buffer> <C-l> :!./%<<CR>
    au FileType python,perl,bash,sh nmap <buffer> <C-l> :!./%<CR>
    au FileType gnuplot             nmap <buffer> <C-l> :!gnuplot %<CR>
    au FileType octave              nmap <buffer> <C-l> :!octave %<CR>
    
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

    let Tlist_Ctags_Cmd = "/usr/bin/ctags"
    let Tlist_WinWidth = 50
    map <leader>tl :TlistToggle<cr>
    " Regenerating the current tags set
    map <leader>tu :!/usr/bin/ctags -R --c++-kinds=+p --fields=+iaS --extra=+q .<CR>

List matches in interactive mode

    map <leader>tm [I:let nr = input("Which one: ")<Bar>exe "normal " . nr ."[\t"<CR>

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

More in the [wikia](http://vim.wikia.com/wiki/Browsing_programs_with_tags)

