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

It should be noted that the movements can also be used in combination to e.g. `y` (yank), `d` (deletes) or `c` (deletes and insert).

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

Vertical movements

```vim
0	  " begining of the line
$	  " end of the line
h	  " one character to the left
<Left>	  " one character to the left
l	  " one character to the right
<Right>	  " one character to the right
```

### Words

Movements can also include words.

```vim
w	  " forward to beginning of words
e	  " forward to end of words
b	  " backward to beginning of words
ge	  " backward to end of words
```

### Various

Some other move commands are useful and do not fall in the previous categories.

```vim
%	" on a parenthesis, jumps to matching parenthesis
)	" forward to beginning of sentence
(	" backward to beginning of sentence
```
