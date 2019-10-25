# Specific Configuration


<!-- vim-markdown-toc GFM -->

* [Incrementation C-A, C-X](#incrementation-c-a-c-x)
* [Abreviations](#abreviations)

<!-- vim-markdown-toc -->

### Incrementation C-A, C-X

#### Number format

When incrementing, numbers starting with 0x are recognised as hexa and the ones starting with 0 as octal. Since I never work with octal numbers and that I sometimes defined decimal starting from 0, I set the formats as

```vim
:se nrformats=hex
```

also possible values are `octal` and `alpha`.

#### Series

To turn

```
5 little monkeys on a bed...
```

to

```
5 little monkeys on a bed...
4 little monkeys on a bed...
3 little monkeys on a bed...
2 little monkeys on a bed...
1 little monkeys on a bed...
```

One can do the following sequence

```vim
qa     " start recording
yyp    " duplicate line
<C-x>  " decrement number
q      " stop recording
3@a    " repeat the record 3 times
```

Or alternatively, on vim8, one ca do

```vim
yy     " yank the line
4p     " paste it 4 times
<C-v>  " visual block
4<Up>  " select line of numbers
g<C-x> " make series
```

See also [Making a list of numbers](https://vim.fandom.com/wiki/Making_a_list_of_numbers).


### Abreviations

Some abbreviations. Particularly useful for mails.

```vim
:ab MfG Mit freundlichen Gruessen

:ab BP bilbopingouin
```
