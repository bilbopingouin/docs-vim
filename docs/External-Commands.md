# External Commands


<!-- vim-markdown-toc GFM -->

* [Check spelling](#check-spelling)
* [Calculator](#calculator)
	* [Using python](#using-python)
	* [Using the expression register](#using-the-expression-register)
* [Shell interactions](#shell-interactions)
	* [Call a shell](#call-a-shell)
	* [Run a command](#run-a-command)
	* [Insert result of a command](#insert-result-of-a-command)
	* [Get man page](#get-man-page)
	* [Start a terminal](#start-a-terminal)

<!-- vim-markdown-toc -->

### Check spelling


Needs `ispell`, and one can choose the language and keymap.

```
map V :w<CR>:!ispell -d british % <CR>:e!<CR><CR>
```

see also [internal spelling](Various-Commands#spell-checking).

### Calculator
  
Everything can be done in the safe vim environment, including calculation. 

#### Using python

Defining a command

```
:command! -nargs=+ Calc :!python -c "from math import *; print <args>"
```
It can then be used as

```
:Calc 1+1
```

Alternatively, one could do

```
:command! -nargs=+ Calc :r!python -c "from math import *; print <args>"
```

and then the result will be written directly on the file.
    
#### Using the expression register

vim uses many kind of registers. 

For example `<C-r>a` to enter the content of a register `a` in insert mode.

The register `=` is called the expression register.

For example

```
<C-r>=1+1<CR>
```

will insert the content of the operation at the cursor point.

Additionally, there, we can also use a set of builtin functions, for example:

Floating point computation:

| *float-functions*	|					  |
|-----------------------|---------------------------------------  |
|    float2nr()         | convert Float to Number		  |
|    abs()              | absolute value (also works for Number)  |
|    round()            | round off				  |
|    ceil()             | round up				  |
|    floor()            | round down				  |
|    trunc()            | remove value after decimal point	  |
|    fmod()             | remainder of division			  |
|    exp()              | exponential				  |
|    log()              | natural logarithm (logarithm to base e) |
|    log10()            | logarithm to base 10			  |
|    pow()              | value of x to the exponent y		  |
|    sqrt()             | square root				  |
|    sin()              | sine					  |
|    cos()              | cosine				  |
|    tan()              | tangent				  |
|    asin()             | arc sine				  |
|    acos()             | arc cosine				  |
|    atan()             | arc tangent				  |
|    atan2()            | arc tangent				  |
|    sinh()             | hyperbolic sine			  |
|    cosh()             | hyperbolic cosine			  |
|    tanh()             | hyperbolic tangent			  |
|    isnan()            | check for not a number		  |

see also `:help function-list`

### Shell interactions

#### Call a shell

```vim
:sh[ell]
```

#### Run a command

```vim
:!ls *.c  " lists all the C-files of the current directory
```

#### Insert result of a command

```vim
:r!ls *.c  " reads the input.
:.!ls *.c  " alternative producing the same result
```

#### Get man page

```vim
K     " opens the manpage of the command under the cursor
```

#### Start a terminal

Starting with ViM 8, one can run 

```vim
:terminal
```

to run a terminal/shell within vim. But it only works with the `+terminal` option activated when compiling.

### Clang format

`clang-format` is a program based on the `clang` compiler which allows to check the format of the code, or update it. To integrate it in vim, one can use the plugin [vim-clang-format](https://github.com/rhysd/vim-clang-format), or using [ALE](https://github.com/dense-analysis/ale) with the following configuration

```vim
" Run automatic fixes when saving the file
let g:ale_fix_on_save = 1

" List of fixes
let g:ale_fixers = {
   \ '*': ['remove_trailing_lines','trim_whitespace'],
   \ 'c': ['clang-format'],
   \ 'cpp': ['clang-format'],
   \  'python': ['autopep8']
   \}
```

which automatically runs `clang-format` on C or C++ files. `clang-format` can be configured using a `.clang-format` file. See also [ALE configuration](Plugins#ale).

### Clang tidy

`clang-format` is a program based on the `clang` compiler which allows to check the standard of the code, or update it. It can be integrated in vim using [ALE](https://github.com/dense-analysis/ale). See also [ALE configuration](Plugins#ale).

### Indent

On linux, a program call `indent` allows to reformat the code (similar to clang-format). It can be called as [following](https://stackoverflow.com/a/30767640/3337196):

```vim
:%!indent
```

Many settings can be decided. I would suggest the following flags

```bash
indent \
  -nbad              \ # not forcing blank line after a declaration 
  -bap               \ # blank line after procedure
  -bbb               \ # blank line before block comments
  -bbo               \ # break long-line before a boolean
  -nbc               \ # not forcing newline after commas in declaration
  -bl                \ # { placed on the line following the if
  -blf               \ # { placed on the line after the function declaration
  -bli0              \ # { at the same indent than the function
  -bls               \ # { placed on the line after the struct declaration
  -nce               \ # not cuddle 'else', e.g. } else {
  -cli2              \ # case indentation of 2 spaces
  -cp2               \ # comments to the right of #else and #endif
  -ncs               \ # not forcing space after cast
  -di2               \ # declaration indentation
  -i2                \ # indentation
  -ip4               \ # parameter indentation
  -l100               \ # length of line
  -nut               \ # use spaces instead of tabs
  -pcs               \ # space after procedure calls, before '('
  -ppi2              \ # indentation of conditional preprocessors
  -npsl              \ # not procnames at the start of line
  -saf               \ # space after for
  -sai               \ # .. if
  -saw               \ # .. while
  -sbi0              \ # 0 spaces indentation for braces for structs
  -sc                \ # add '*' left of block comment lines
  -nsob              \ # no swallow blank lines
```

Those can also be saved in `.indent.pro`. Simply the list of commands separated by spaces, tabs or newlines. C/C++ comments would be ignored.