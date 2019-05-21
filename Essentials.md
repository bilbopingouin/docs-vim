# A list of essentials commands (aka cheat sheet)

### Basic/first step

- Open a file

  ```bash
  vim file.txt
  ```

- Edit a file

  ```vim
  i      " inserts where the cursor is
  (enter some text)
  <esc>  " stops inserting

- Save & close

  ```vim
  :wq
  ```

### Get help

When lost, use

```vim
:help!
```

Or more specifically

```vim
:help :diff
```

### Modes

vim uses different modes (see [Learning the vi Editor/vim Modes](https://en.wikibooks.org/wiki/Learning_the_vi_Editor/Vim/Modes)), each with its own set of commands and instruction. 

The following modes are available:
- normal (`<ESC>` from most modes)
  ```vim
  :help Normal-mode
  ```
- insert (`i` from normal mode)
  ```vim
  :help Insert-mode
  ```
- visual (`v` from normal mode, or `<c-v>` for block visual mode)
  ```vim
  :help Visual-mode
  ```
- select (e.g. `gh` or `gH` from normal mode) similar to the visual mode
  ```vim
  :help Select-mode
  ```
- command line (`:` from normal mode)
  ```vim
  :help Command-line-mode
  ```
- Ex-mode (`Q` from normal mode) similar to the command line mode
  ```vim
  :help Ex-mode
  ```