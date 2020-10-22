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

### Revert lines

Over the whole file with

```vim
:g/^/m0
```

Over a given range with

```vim
:'<,'>g/^/m'<
```

This uses the [global command](#global_command) with the `m`ove command. For the complete file command, each line are moved to the position 0, meaning before the first line. For the ranged command, it will be moved **after** the first line of the range (meaning the first line stays untouched).


