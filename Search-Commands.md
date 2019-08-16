# Search Commands

### Configurations

Some configuration that makes searching nice

Search ignoring case

```vim
:set ignorecase
```

normally ignore the case when searching or by replace

```vim
:set smartcase
```

overrides `ignorecase` if search pattern contains uppercase:
- to search all case: use only lower case in search
- otherwise will match the case

Another interesting configuration is the 

```vim
:set incsearch
```

which allows to search the next instance while typing.

### Hightlight

Highlighting search matches

```vim
:se hlsearch                             " Highlight search
:hi search guibg=LightGreen ctermbg=10   " Change color of highlight
```

Some commands that can be useful:

- space to remove current highlighting

```vim
:nnoremap <silent> <Space> :nohlsearch<Bar>:echo<CR>
```



### Visual selection

Search visually selected text

```vim
:vmap * y/<C-R>"<CR>
:vmap # y?<C-R>"<CR>
```



### Highlight like a search without jumping

`F8` to do like `*` but without moving to the next occurence

```vim
:nnoremap <F8> :let @/='\<<C-R>=expand("<cword>")<CR>\>'<CR>:set hls<CR>
```

`F8` and visual

```vim
:set guioptions+=a
:so ~/.vim/scripts/MakePattern.vim
:vnoremap <silent> <F8> :<C-U>let @/="<C-R>=MakePattern(@*)<CR>"<CR>:set hls<CR>
```

where `~/.vim/scripts/MakePattern.vim` is

```vim
function! MakePattern(text)  
  let pat = escape(a:text, '\')  
  let pat = substitute(pat, '\_s\+$', '\\s\\*', '')  
  let pat = substitute(pat, '^\_s\+', '\\s\\*', '')  
  let pat = substitute(pat, '\_s\+',  '\\_s\\+', 'g')  
  return '\\V' . escape(pat, '\"')
endfunction
```

But this does not seem to work...

### Commands

A few searches commands

- `gd` looks for the definition of a variable (first occurence within a file)
- `/` normal search
- `?` backward search
- `*` search current word (under cursor)
- `#` same as `*` but backward
- `g#` and `g*` like their respective commands (without `g`) but does not require an exact match.
- `:lvimgrep /pattern/j **/*` search recursively for pattern w/o jumping to the first occurence `:lw` shows the results and `:lcl` hide the results
- `:vimgrepa[dd] /pattern/j **` same as before, but store results in quickfix file: `:copen` to show and `:ccl[ose]` to close. This allows for direct navigation.
- `n` next occurrence
- `N` previous occurrence

Next and previous depends on the search direction.

It is also possible to reuse directly a search pattern, for example

```vim
/foo
:s//bar/g
```

would replace all instances of `foo` to `bar`.

Similarly to substitute (`:s`), the global command (`:g`) can also reuse the previous search pattern. In particular

```vim
:g/
```

lists all lines containing the search pattern.

See also [Searching tips](https://vim.fandom.com/wiki/Searching)


### Search across buffers

Search in all current buffers

```vim
:bufdo vimgrepadd yoursearchpattern  % | copen
```

or

```vim
command! -nargs=1 Search call setqflist([]) | silent bufdo grepadd! <args> %
nnoremap <C-n> :cprev<cr>zvzz
nnoremap <C-p> :cnext<cr>zvzz
```

but none seems to be working perfectly...