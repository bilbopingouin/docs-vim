# ViM Scripting 


<!-- vim-markdown-toc GFM -->

* [Variables](#variables)
  * [Range](#range)
* [Functions](#functions)

<!-- vim-markdown-toc -->

## Variables 

### Range

Variables have defined range, which is normally indicated as a prefix to the variable name.

``` vim
g:var   " global variable
a:var   " function argument
l:var   " local to a function
b:var   " local to a buffer
w:var   " local to a window
t:var   " local to a tab
v:var   " predefined by ViM
```

See also [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/chapters/20.html).

## Functions

A function in ViM script is defined as 

``` vim
function! FunctionNameAdd(a,b)
  let l:res = a:a+a:b
  return l:res
endfunction
```

See also:
- [Learn Vimscript the Hard Way](https://learnvimscriptthehardway.stevelosh.com/chapters/23.html)
- [Write your own Vim function](https://vim.fandom.com/wiki/Write_your_own_Vim_function)
