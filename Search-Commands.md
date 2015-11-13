# Search Commands

### Configurations

Some configuration that makes searching nice

Search ignoring case

    :se ignorecase

normally ignore the case when searching or by replace

    :se smartcase

overrides ignorecase if search pattern contains uppercase:
- to search all case: use only lower case in search
- otherwise will match the case

### Hightlight

Highlighting search matches

    :se hlsearch                             " Highlight search
    :hi search guibg=LightGreen ctermbg=10   " Change color of highlight

Some commands that can be useful:

- space to remove current highlighting

```
:nnoremap <silent> <Space> :nohlsearch<Bar>:echo<CR>
```



### Visual selection

Search visually selected text

    :vmap * y/<C-R>"<CR>
    :vmap # y?<C-R>"<CR>



### Highlight like a search without jumping

`F8` to do like `*` but without moving to the next occurence

    :nnoremap <F8> :let @/='\<<C-R>=expand("<cword>")<CR>\>'<CR>:set hls<CR>

`F8` and visual

    :set guioptions+=a
    :so ~/.vim/scripts/MakePattern.vim
    :vnoremap <silent> <F8> :<C-U>let @/="<C-R>=MakePattern(@*)<CR>"<CR>:set hls<CR>

where `~/.vim/scripts/MakePattern.vim` is

    function! MakePattern(text)  
      let pat = escape(a:text, '\')  
      let pat = substitute(pat, '\_s\+$', '\\s\\*', '')  
      let pat = substitute(pat, '^\_s\+', '\\s\\*', '')  
      let pat = substitute(pat, '\_s\+',  '\\_s\\+', 'g')  
      return '\\V' . escape(pat, '\"')
    endfunction

But this does not seem to work...

### Commands

A few searches commands

- `gd` looks for the definition of a variable (first occurence within a file)
- `/` normal search
- `?` backward search
- `*` search current word (under cursor)
- `#` same as `*` but backward
- `:lvimgrep /pattern/j **/*` search recursively for pattern w/o jumping to the first occurence `:lw` shows the results and `:lcl` hide the results
- `:vimgrepa[dd] /pattern/j **` same as before, but store results in quickfix file: `:copen` to show and `:ccl[ose]` to close. This allows for direct navigation.

### Search across buffers

Search in all current buffers

    :bufdo vimgrepadd yoursearchpattern  % | copen

OR

    command! -nargs=1 Search call setqflist([]) | silent bufdo grepadd! <args> %
    nnoremap <C-n> :cprev<cr>zvzz
    nnoremap <C-p> :cnext<cr>zvzz

but none seems to be working perfectly...
