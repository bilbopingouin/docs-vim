# External Commands

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

