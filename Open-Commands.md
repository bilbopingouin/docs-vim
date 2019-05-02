# Opening Commands

### clean state

Ignoring the configuration

    vim -u NONE

### diff

    vim -d file1 file2

See also [Diff in Various-Commands](Various-Commands#diff).

### RO

    vim -R file # opens in read only still modifiable
    vim -M file # opens non modifiable

### multiple files

    vim file1 file2    # creates a list of arguments (:args) which can be accessed with :next and :prev
    vim -o file1 file2 # a window for each file. Horizontal split
    vim -O file1 file2 # a window for each file. Vertical split
    vim -p file1 file2 # a tab for each file

### open at a given position

    vim file +N        # opens file at line N.
    vim file +/pattern # opens file at first occurence of 'pattern'

### tags

    vim -t pattern 

see also [vim: programming](Programming)


### no swap

    vim -n [file]

### easy mode

    vim -y [file]

### encrypt mode

    vim -x [file]

### recovery mode

    vim -r [file]

### run commands

    vim +{cmd} vim -c{cmd}
    vim --cmd={cmd} # this precedes the .vimrc

### create a script automatically

    vim -w scriptname file # all vim commands are stored in the script

### Open file within vim
  
#### Open an existing file:

    :e[dit] path/file.name
    
#### Create a new file/buffer:

    :enew [path/file.name]
    
#### Browse for an existing file to open:

    :e[dit] .
    
#### Open a file in a new tab:

    :tabe[dit] path/file.name
    
#### Open a new file with an empty buffer:

    :tabnew [path/file.name]
    
#### Open a new file in a new split window (horizontal)

    :new [path/file.name]
    
#### Open a new file in a new split window (vertical)

    :vert new [path/file.name]
    :vne[w] [path/file.name]
    
#### Open an existing file within a new split window (horizontal)

    :sp[lit] path/file.name
    :new path/file.name
    
#### Open an existing file within a new split window (vertical)

    :vne[w] path/file.name
        
### Open several files each within its own tab
  
Open all files in the arg list:

    :tab all
    
Set the argument list and open them:

    :arg[s] **/*.c | tab all

opens all the C files within the sub-directories
and closes the currently opened file
    
Set the argument list and open them, keeping currently opened files

    :arga[dd] **/*.c | tab all

Adds the found C files within the sub-dir to the list of arguments
and opens all of them within tabs, or split windows.
    
See also: 

    :help argument-list
    :help :all
        
### Buffer list
  
List the buffers opened

    :ls
    
Jump to the previous buffer

    :bp

Jump to the next buffer

    :bn
    
Jump to the buffer N

    :bN
    
See also [How to effectively work with multiple files in vim](https://stackoverflow.com/questions/53664/how-to-effectively-work-with-multiple-files-in-vim)
