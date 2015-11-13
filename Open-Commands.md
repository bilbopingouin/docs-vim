# Opening Commands

### diff

    vim -d file1 file2

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

    vim -t pattern # see also vim: programming

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
