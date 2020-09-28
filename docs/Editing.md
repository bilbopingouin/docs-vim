# Editing


<!-- vim-markdown-toc GFM -->

* [Sort lines](#sort-lines)
* [Global command](#global-command)
  * [Delete last line if empty](#delete-last-line-if-empty)

<!-- vim-markdown-toc -->

### Sort lines

Using

```vim
:(range)sort u
```

or numerical

```vim
:(range)sort n
```

See also
- [Sort lines](https://vim.fandom.com/wiki/Sort_lines)
- `:help sort`


### Global command

A not so well known but powerful command, `:g`. It follows the principle

```vim
:[range]g/pattern/command
```

#### Delete last line if empty

The following command will delete the last line of the file if it is empty.

```vim
:$g/^$/d
```


