# Character Encoding


<!-- vim-markdown-toc GFM -->

* [Keyboard mapping for exotic keyboards inputs](#keyboard-mapping-for-exotic-keyboards-inputs)
* [scripts](#scripts)
* [File format](#file-format)
* [Digraphs](#digraphs)

<!-- vim-markdown-toc -->

### Keyboard mapping for exotic keyboards inputs


It is possible to map the keys, if the behaviour is not as expected.

```vim
if $LANG == 'ja_JP.EUC-JP'
  " echo "Running Japanese"
  :se term=builtin_ansi
  map OQ        <F2>
  map OR        <F3>
  imap OQ       <F2>
  imap OR       <F3>
  " for end/home keys
  " to know the code, type in edit mode C-v and then the key
  map ^[OH  <Home>  
  map ^[OF  <End>  
  imap ^[OH <Home>  
  imap ^[OF <End>
  " for PageUp/PageDown  
  " to know the code, type C-k and then the key
  map [6~ <PageDown>  
  map [5~ <PageUp>  
  imap [6~ <PageDown>  
  imap [5~ <PageUp>  
  "map <PageUp> <C-U>  
  "map <PageDown> <C-D>
endif

"Japanese characters
if has("multi_byte")
  set encoding=utf-8                   " how vim shall represent characters internally
  setglobal fileencoding=utf-8         " empty is also OK (defaults to same as 'encoding'). Or you may want to set one of the ucs encodings (which
                                       " may use less disk space if you use only "alphabetic" scripts such as Latin, Greek, Cyrillic, Hebrew or Arabic, and
                                       " not "ideographic" scripts like Chinese, Japanese or Korean. With the ucs encodings it is usually better
  set bomb                             " to also set 'bomb' on ('byte-order-mark" option, irrelevant for utf-8 but not for ucs)
  set termencoding=iso-8859-15         " or whatever is appropriate to your locale (iso-8859-15 is Latin1 + Euro currency sign)
  set fileencodings=ucs-bom,iso-8859-15,iso-8859-3,utf-8
                                       " or whatever is appropriate to the kinds of files you want to edit
                                       " 'fileencodings' defines the heuristic to set 'fillencoding' (local to buffer) when reading an existing file. The first one that matches will be used.
                                       " ucs-bom is "ucs with byte-order-mark"; it must not come after ucs-8 if you want it to be used
else
  echoerr "Sorry, this version of (g)vim was not compiled with +multi_byte"
endif
```

In "replace" mode, one utf character (one or more data bytes) replaces one utf character (which need not use the same number of bytes) 
In "normal" mode, ga shows the character under the cursor as text, decimal, octal and hex; `g8` shows which byte(s) is/are used to represent it
In "insert" or "replace" mode, 
- any character defined on your keyboard can be entered the usual way (even with dead keys if you have them, e.g. âêîôû  äëïöü)
- any character which has a "digraph" (there are a huge lot of them, see `:dig` after setting `enc=utf-8`) can be entered with a `Ctrl-K` prefix
- any utf character at all can be entered with a `Ctrl-V` prefix, either `<Ctrl-V> u aaaa` or `<Ctrl-V> U bbbbbbbb`, with 0 <= aaaa <= FFFF, or 0 <= bbbbbbbb <= 7FFFFFFF

Unicode can be used to create html "body text", at least for Netscape 6 and probably for IE; but on my machine it doesn't display properly as "title text" (i.e., between `<title></title>` tags in the  `<head>` part).

Gvim will display it properly if you have the fonts for it, provided that you set 'guifont' to some fixed-width font which has the glyphs you want to use (Courier New is OK for French, German, Greek, Russian and more, but I'm not sure about Hebrew or Arabic; its glyphs are of a more "fixed" width than those of, e.g. Lucida Console: the latter can be annoying if you need bold Cyrillic writing).

---

### scripts

Change German characters to LaTeX

```vim
function! Deu2utf()

  " Removing ignorecase to avoid problems
  :let l:icase = 0
  :if (&ignorecase)
    :set noignorecase
    :let l:icase = 1
    :echo "* Unset ignorecase *"
  :endif

  " Simply replace to LaTeX commands
  " Umlauts
  :echo "Replacing Ä"  
  :%s/Ä/\\"A/ge  
  :echo "Replacing Ö"  
  :%s/Ö/\\"O/ge  
  :echo "Replacing Ü"  
  :%s/Ü/\\"U/ge  
  :echo "Replacing ä"  
  :%s/ä/\\"a/ge  
  :echo "Replacing ö"  
  :%s/ö/\\"o/ge  
  :echo "Replacing ü"  
  :%s/ü/\\"u/ge 

  " "ss" problematic since we don't want to delete the following space
  :echo "Replacing ß"
  :%s/ß\ /\\ss\\\ /ge             " if it is followed by a space: gem\"a\ss
  :%s/ß\([a-zA-Z]\)/\\ss\ \1/ge   " if it is followed by a letter


  " quotation marks: please note that one needs "\usepackage[ngerman]{babel}" to get them.
  :echo "Replacing quotation marks"  :%s/„/\\glqq\ /ge  :%s/“/\\grqq\ /ge

  " Set back the user configuration
  :if l:icase == 1:set ignorecase:echo "* Reset ignorecase *":endif

endfunction
```

### File format

A file can be saved in various format, for example in dos (with <CR>+<LF>) or unix format. The format from the current file can be set as

```vim
set ff=dos
```

But the file could also be reopened setting the right format as

```vim
:e ++ff=unix
```

See also:
- [See line breaks and carriage returns in editor](https://stackoverflow.com/q/3860519/3337196)
- [Convert DOS line endings to Linux line endings in vim](https://stackoverflow.com/q/82726/3337196)

### Digraphs

Some characters that cannot usually be entered by a normal keyboard are defined. It can be used in insert mode with, e.g.

```vim
<C-k>BB
```

Alternatively, one can use 

```vim
:set digraph
i
B<BS>B
```

Both method would produce the character: `¦`. 

A list of such characters have already been defined and can be seen using

```vim
:dig[raph]
```

See also 

```vim
:help digraph
```
