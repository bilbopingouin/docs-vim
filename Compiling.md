# Compiling

VIM is often already pre-installed on Linux systems, otherwise it is convenient to install default versions, e.g.

    aptitude install vim
    
or gvim.exe, etc.

But sometime one may want to compile it oneself.

### Get the sources

With the following commands

``` 
# aptitude install mercurial
$ hg clone https://vim.googlecode.com/hg/ vim
```
  
  
### Compiling

```  
$ cd vim/src
$ make
```
possibly one may want to run

```    
$ make install
```
  
### Flags and options

As of 2015.05.20, the features in default compilation of vim 7.4 contains the following (`:h feature-list`):


    
        vim7.4 default      vim 7.3 debian default (+/-/o)      Difference  Description
        oARP                o                                               ARP support (Amiga only)
        +acl                o                                   #           Access Control List: new rights for files, on recent MSWindows and Unix File System
        -arabic             +                                   #           Edit arabic files
        +autocmd            +                                               Enables :autocmd, adding commands that vim execute on some events: good for, e.g., recognizing filetype
        -balloon_eval       -                                               Allows a debugger or external tool do display dynamic info depending on mouse position: requires GUI. ballon-eval
        -browse             -                                               Enable :browse, open a file selection dialog for some commands. Only works for some versions (e.g. GTK).
        +builtin_terms      ++                                  #           Used builtin-terms (:set term=...). ++ means 'maximal'
        +byte_offset        +                                               go/:goto commands as well as o flag in status line
        +cindent            +                                               C indenting
        -clientserver       -                                               remote invocation/command server/client
        -clipboard          -                                               clipboard support: using * register to copy paste: "*p, "*yy, etc.
        +cmdline_compl      +                                               command line completion
        +cmdline_hist       +                                               command line history
        +cmdline_info       +                                               'showcmd' and 'ruler'
        +comments           +                                               'comments' support: list of strings that define a comment line, e.g. when starting /* ... and typing return, a * is inserted automatically
        -conceal            +                                   #           'conceal' and ':syn-conceal', ... in the synthax, allows to 'hide' some characters
        +cryptv             +                                               support encryption, vim -x file
        -cscope             +                                   #           enables cscope, similar to ctags, but with more functionalities
        +cursorbind         +                                               cursor bind: when moving cursor in one buffer, bound cursors move also, useful for diffs.
        +cursorshape        +                                               allows to control the shape/colour of the cursors t_SI and t_EI
        odebug              o                                               Debugging mode
        odialog_gui         o                                               Support for :confirm with GUI dialog
        +dialog_con         +                                               Support for :confirm with console dialog, e.g. :confirm w foo will ask to confirm if foo exist
        odialog_con_gui     o                                               Support for :confirm with GUI and console dialogs
        +diff               +                                               vimdiff
        +digraphs           +                                               used to enter characters that normally cannot be entered by keyboard (e.g. non-ASCII)
        -dnd                -                                               register ~ contains the last drag and drop text (D'n'D)
        -ebcdic             -                                               alternative for character coding: ASCII/EBCDIC and support for internal script definition
        -emacs_tags         +                                   #           read emacs-tags
        +eval               +                                               expression evaluation
        +ex_extra           +                                               extra Ex commands: :center :left :right (text alignment) :retab (replace tabs with new tabstop value) :normal (normal mode commands in execute line)
        +extra_search       +                                               ':hlsearch' and 'incsearch' options
        -farsi              +                                   #           support of farsi language
        +file_in_path       +                                               'gf', 'C-W f' and <cfile>
        +find_in_path       +                                               include file searches: [I, :isearch, C-W C-I, :checkpath, ...
        +float              +                                               floating point support
        +folding            +                                               folding
        -footer             -                                               gui-footer: messages at the bottom of a gui window
        +fork()             +                                               Unix only: fork shell commands: :fork(cmd) instead of :system(cmd), which is slower
        +gettext            +                                               message translation multi-lang
        oGUI_Athena*        o                                               Unix only: Athena |GUI|
        oGUI_neXtaw*        o                                               Unix only: neXtaw |GUI|         
        oGUI_GTK*           o                                               Unix only: GTK+ |GUI| 
        oGUI_Motif*         o                                               Unix only: Motif |GUI| 
        oGUI_Photon*        o                                               QNX only:  Photon |GUI|
        -hangul_input       -                                               hangul support (Korean)
        +iconv              +                                               iconv() implementation: convert to string
        oiconv/dyn          o                                               iconv-dynamic /dyn implementation
        +insert_expand      +                                               C-X submode of Insert, to allow keyword completion
        +jumplist           +                                               creates a jumplist for C-o/C-i
        -keymap             +                                   #           keyboard mapping in insert mode
        -langmap            +                                   #           keyboard mapping in normal mode
        +libcall            +                                               call functions in run-time library
        +linebreak          +                                               'linebreak', 'breakat' and 'showbreak'
        +lispindent         +                                               sets the indent to LISP standards
        +listcmds           +                                               vim commands for the list of buffers and argument list
        +localmap           +                                               support for mapping local to a buffer
        -lua                -                                               LUA interface
        olua/dyn            o                                               LUA interface /dyn
        +menu               +                                               ':menu' to defined menu (in GUI)
        +mksession          +                                               write a script that restore current editing session
        +modify_fname       +                                               filename modifiers, e.g. %:p
        +mouse              +                                               mouse handling
        -mouseshape         -                                               how the mouse pointer looks like in different modes
        -mouse_dec          -                                               Dec terminal mouse handling
        -mouse_gpm          +                                   #           Linux console mouse handling
        -mouse_jsbterm      -                                   
        -mouse_netterm      +                                   #           netterm mouse handling: mouse generate r,c row and column decimal numbers
        omouse_pterm        o                                               pterm mouse handling (QNX only)
        -mouse_sgr          o                                   #
        -mouse_sysmouse     -                                               BSD console mouse handling
        -mouse_urxvt        +                                   #           urxvt mouse handling
        +mouse_xterm        +                                               xterm mouse handling
        +multi_byte         +                                               16 and 32 bit characters
        omulti_byte_ime     o                                               Win32 input method for multibyte chars
        +multi_lang         +                                               Non-English language support
        -mzscheme           -                                               Mzscheme interface
        omzscheme/dyn       o                                                   "       "       /dyn
        +netbeans_intg      +                                               socket interface for vim integration into and IDE
        oole                o                                               Win32 GUI ole-interface
        +path_extra         +                                               Up/downwards search in path and tags
        -perl               -                                               perl interface
        operl/dyn           o                                                 "     "       /dyn
        +persistent_undo    +                                               'undo-persistence' allow to implement the undofile
        +postscript         +                                               ':hardcopy' command to send lines to postscript to a printer
        +printer            +                                               connection with printer (:hardcopy)
        -profile            +                                   #           vim measures time required to run some command and/or functions
        -python             -                                               python 2 interface
        opython/dyn         o                                                  "   "    "       /dyn
        -python3            -                                               python 2 interface
        opython3/dyn        o                                                  "   "    "       /dyn
        +quickfix           +                                               :make and quickfix commands
        +reltime            +                                               reltime() function, and search timeouts
        -rightleft          +                                   #           right to left typing
        -ruby               -                                               ruby interface
        oruby/dyn           o                                                "      "       /dyn
        +scrollbind         +                                               allows binding scrolling
        +signs              +                                               allows definitions of new signs with 'sign'
        +smartindent        +                                               enables 'smartindent'
        -sniff              -                                               SniFF interface
        +startuptime        +                                               --startuptime argument (good to debug .vimrc)
        +statusline         +                                               allows 'statusline', 'rulerformat' and some parts of 'titlestring' and 'iconstring'
        -sun_workshop       -                                               for Sun virtual workshop
        +syntax             +                                               syntax highlighting
        osystem()           o                                               see fork()
        +tag_binary         +                                               binary search in tags file
        +tag_old_static     +                                               old method for static tags
        -tag_any_white      -                                               any white space allowed in tags file
        -tcl                -                                               TCL interface
        otcl/dyn            o                                                "      "       /dyn
        +terminfo           +                                               uses terminfo instead of termcap
        +termresponse       +                                               support for t_RC and v:termresponse
        +textobjects        +                                               text-objects selection in Visual mode: aw iw ...
        +title              +                                               setting up the window title and icon
        -toolbar            -                                               gui-toolbar
        +user_commands      +                                               user-defined commands
        +vertsplit          +                                               enable :vsplit
        +virtualedit        +                                               enable virtualedit: allows cursor to be placed where there are not characters, e.g. after the last character of the line
        +visual             +                                               enable visual mode
        +visualextra        +                                               enable blockwise-operators
        +viminfo            +                                               viminfo-file
        +vreplace           +                                               gR and gr: virtual replace mode -> alternative to r/R with tab align columns
        +wildignore         +                                               enables wildignore (ignores some files when search in path)
        +wildmenu           +                                               enables wildmenu (command-line completion are enhanced)
        +windows            +                                               more than one window
        +writebackup        +                                               'writebackup' -> *.swp
        -X11                -                                               can restore window title
        -xfontset           -                                               X fontset support
        -xim                -                                               X input method
        -xsmp               -                                               XSMP (X session management) support
        -xterm_clipboard    -                                               xterm clipboard handling
        -xterm_save         -                                               save and restore xterm screen
        -xpm                o                                               pixmap support


I want to get the most recent, but change some settings. I want to add `+profile +mouse_gpm +mouse_netterm +csope +conceal +clipboard +xterm_clipboard`


        $ make distclean
        # aptitude install libx11-dev libxtst-dev libgpm-dev
        $ ./configure --enable-cscope