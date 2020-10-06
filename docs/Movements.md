# Movements

In ViM, one can move around quite efficiently, it might be useful to know some commands.

<!-- vim-markdown-toc GFM -->

* [Lines](#lines)
* [Words](#words)
* [Various](#various)

<!-- vim-markdown-toc -->

This isn't an exhaustive list, one should refer to 

- In-line help
  ```vim
  :help motion.txt
  ```
- [All the right moves](https://vim.fandom.com/wiki/All_the_right_moves)

It should be noted that the movements can also be used in combination to e.g. 
- `y` (yank), 
- `d` (deletes),
- `v` (select)
- `c` (deletes and insert).

### Lines

Up/Down lines can be done using

```vim
j	   " one line down
<Down>	   " arrow-key move down
k	   " one line up
<Up>	   " arrow-key move up
<PageUp>   " page up
<PageDown> " page down
```

Top/bottom

```vim
G	  " bottom of the file
gg	  " top of the file
```

Horizontal movements

```vim
0	        " begining of the line
$	        " end of the line
h	        " one character to the left
<Left>    " one character to the left
l	        " one character to the right
<Right>   " one character to the right
```

### Words

Movements can also include words.

```vim
w	    " forward to beginning of words
e	    " forward to end of words
b	    " backward to beginning of words
ge    " backward to end of words
```

Using capitalized movements, usually ends on the adjacent space.

### Text objects

There are some movements that very useful for text, like

```vim
ciw   " Delete a single word and switch to insert mode
```

They arte built on the following combination: 
- command (e.g. `c`, `v`, ...)
- `i`/`a`: 'a' / inner. The difference resides in counting the white spaces or not
- range:
  - `w` for words,
  - `W` for WORDs (differs in the types of characters considered),
  - `s` for sentence,
  - `p` for paragraph,
  - `[`/`]` for a `[..]` block,
  - `(`/`)`/`b` for a `(..)` block,
  - `<`/`>` for a `<..>` block,
  - `{`/`}`/`B` for a `{..}` block,
  - `t` for a tag block (HTML/XML-type tags),
  - `"`/`'`/`` ` `` for a quoted string



### Various

Some other move commands are useful and do not fall in the previous categories.

```vim
%	" on a parenthesis, jumps to matching parenthesis
)	" forward to beginning of sentence
(	" backward to beginning of sentence
```
