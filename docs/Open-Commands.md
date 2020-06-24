# Opening Commands


<!-- vim-markdown-toc GFM -->

* [clean state](#clean-state)
* [diff](#diff)
* [RO](#ro)
* [multiple files](#multiple-files)
* [open at a given position](#open-at-a-given-position)
* [tags](#tags)
* [no swap](#no-swap)
* [easy mode](#easy-mode)
* [encrypt mode](#encrypt-mode)
* [recovery mode](#recovery-mode)
* [run commands](#run-commands)
* [create a script automatically](#create-a-script-automatically)
* [Open file within vim](#open-file-within-vim)
	* [Open an existing file:](#open-an-existing-file)
	* [Create a new file/buffer:](#create-a-new-filebuffer)
	* [Browse for an existing file to open:](#browse-for-an-existing-file-to-open)
	* [Open a file in a new tab:](#open-a-file-in-a-new-tab)
	* [Open a new file with an empty buffer:](#open-a-new-file-with-an-empty-buffer)
	* [Open a new file in a new split window (horizontal)](#open-a-new-file-in-a-new-split-window-horizontal)
	* [Open a new file in a new split window (vertical)](#open-a-new-file-in-a-new-split-window-vertical)
	* [Open an existing file within a new split window (horizontal)](#open-an-existing-file-within-a-new-split-window-horizontal)
	* [Open an existing file within a new split window (vertical)](#open-an-existing-file-within-a-new-split-window-vertical)
* [Open several files each within its own tab](#open-several-files-each-within-its-own-tab)
* [Buffer list](#buffer-list)
* [Sessions](#sessions)

<!-- vim-markdown-toc -->

### clean state

Ignoring the configuration

```bash
vim -u NONE
```

### diff

```bash
vim -d file1 file2
```

See also [Diff in Various-Commands](Various-Commands#diff).

### RO

```bash
vim -R file # opens in read only still modifiable
vim -M file # opens non modifiable
```

### multiple files

```bash
vim file1 file2    # creates a list of arguments (:args) which can be accessed with :next and :prev
vim -o file1 file2 # a window for each file. Horizontal split
vim -O file1 file2 # a window for each file. Vertical split
vim -p file1 file2 # a tab for each file
```

### open at a given position

```bash
vim file +N        # opens file at line N.
vim file +/pattern # opens file at first occurence of 'pattern'
```

### tags

```bash
vim -t pattern 
```

see also [vim: programming](Programming)


### no swap

```bash
vim -n [file]
```

### easy mode

```bash
vim -y [file]
```

### encrypt mode

```bash
vim -x [file]
```

### recovery mode

```bash
vim -r [file]
```

When opening a file, vim may warn of a different version existing (due to crash or open somewhere else, etc.). On option is to use [Recover.vim](https://github.com/chrisbra/Recover.vim), which offers the option to compare the saved version and the automatically saved (recover) version.

### run commands

```bash
vim +{cmd} vim -c{cmd}
vim --cmd={cmd} # this precedes the .vimrc
```

### create a script automatically

```bash
vim -w scriptname file # all vim commands are stored in the script
```

### Open file within vim
  
#### Open an existing file:

```vim
:e[dit] path/file.name
```
    
#### Create a new file/buffer:

```vim
:enew [path/file.name]
```
    
#### Browse for an existing file to open:

```vim
:e[dit] .
```
    
#### Open a file in a new tab:

```vim
:tabe[dit] path/file.name
```
    
#### Open a new file with an empty buffer:

```vim
:tabnew [path/file.name]
```
    
#### Open a new file in a new split window (horizontal)

```vim
:new [path/file.name]
```
    
#### Open a new file in a new split window (vertical)

```vim
:vert new [path/file.name]
:vne[w] [path/file.name]
```
    
#### Open an existing file within a new split window (horizontal)

```vim
:sp[lit] path/file.name
:new path/file.name
```
    
#### Open an existing file within a new split window (vertical)

```vim
:vne[w] path/file.name
```
        
### Open several files each within its own tab
  
Open all files in the arg list:

```vim
:tab all
```
    
Set the argument list and open them:

```vim
:arg[s] **/*.c | tab all
```

opens all the C files within the sub-directories
and closes the currently opened file
    
Set the argument list and open them, keeping currently opened files

```vim
:arga[dd] **/*.c | tab all
```

Adds the found C files within the sub-dir to the list of arguments
and opens all of them within tabs, or split windows.
    
See also: 

```vim
:help argument-list
:help :all
```
        
### Buffer list
  
List the buffers opened

```vim
:ls
```
    
Jump to the previous buffer

```vim
:bp
```

Jump to the next buffer

```vim
:bn
```
    
Jump to the buffer N

```vim
:bN
```
    
See also [How to effectively work with multiple files in vim](https://stackoverflow.com/questions/53664/how-to-effectively-work-with-multiple-files-in-vim)

### Sessions

It is possible to save the current sessions (all currently open views).

It can be started running

```vim
:mks[ession][!] [file]
```

The info about the current session will be stored in the `file` (if omitted, it uses `Session.vim`). The session can be reopened using

```bash
vim -S session-filename.vim
```

or, from within `vim` as

```vim
:so[urce] session-filename.vim
```

See also

- `:help :mksession`
- [How to auto save vim session on quit and auto reload on start including split window state?](https://stackoverflow.com/q/5142099/3337196)
