# A list of essentials commands (aka cheat sheet)


<!-- vim-markdown-toc GFM -->

* [Basic/first step](#basicfirst-step)
* [Get help](#get-help)
* [Modes](#modes)
* [Configuration](#configuration)

<!-- vim-markdown-toc -->

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

### Configuration

Use a plugin manager like [vim-plug](https://github.com/junegunn/vim-plug). Details of the installation can be found on the respective plugin description. To get started, edit your `.vimrc` and add the following

```vim
call plug#begin()
Plug 'tpope/vim-sensible'
call plug#end()
```

Follow by the folliwing commands

```vim
:w
:so %
:PlugInstall
```

And there you are, a very basic configuration which will allow to get some basic configuration.
