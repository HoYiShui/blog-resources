---
title: Vimtutor is all you need
date: 2024-04-16 15:06:23
categories: [tutorial]
tags: [vim]
lang: en
cover: https://ooo.0x0.ooo/2024/04/16/Om8J7S.png
---
# How to learn Vim? Vimtutor!



## Configure vim

[vim-plugin](https://www.linode.com/docs/guides/introduction-to-vim-customization/#integrate-plug-ins)

[change vim colorscheme](https://www.linode.com/docs/guides/vim-color-schemes/#install-manually)

[one-dark](https://vimawesome.com/plugin/onedark-vim)



## Learn Vim

For learning vim editor, you need:

```
vimtutor
```

It has seven lession and may take 25 ~ 30 minutes for finish the exercise in vim tutor.

> Actually you may need nearly 2 hours for the first exercise, but it is worthy.



### Lesson 1

- The cursor is moved using either the arrow keys or the hjkl keys.

  - `h` (left)
  - `j` (down) 
  - `k` (up)
  - `l` (right)

- To **start** Vim from the shell prompt type:

  ```
   vim filename
  ```

- To **exit** Vim:

- type:     \<ESC>  `:q!`     \<ENTER>  to trash all changes.

- type:    \<ESC>   `:wq`     \<ENTER>  to save the changes.

- To **delete** the character at the cursor type:  `x`

- To **insert** or **append** text type:

  - `i`     type inserted text        \<ESC>        insert **before** the cursor
  - `A`    type appended text      \<ESC>        append **after** the cursor

NOTE: Pressing \<ESC> will place you in **normal mode** or will cancel an unwanted and partially completed command.



### Lesson 2

- To **delete**:

  - from the cursor up to the **next word**, type:  `dw`

    > `dw` means cut from here to next word

  - from the cursor to the **end** of the **word**, type:  `de`

    > `de` means cut from here to the end of the current word

  - from the cursor to the **beginning** of a **line**, type: `d0`

  - from the cursor to the **end **of a **line**, type:   `d$`

  - the **whole line**,  type:    `dd`

- To **move** the cursor:

  - `w`, `e`, `0`, `$`

  > these four motion preformance as "delete" described above.

- To **repeat** a motion prepend it with a number:   `number motion`

- The format for a change command is: `operator   [number]   motion`

  > operator  - is what to do, such as  `d`  for delete
  > [number] - is an optional count to repeat the motion
  > motion     - moves over the text to operate on, such as  `w` (word), `$` (to the end of line), etc.

- To **undo**: 

  - **a** previous actions, type:  `u`  (lowercase u)
  - **all** the changes on **a line**, type:  `U`  (capital U)
  - the **undo's**, type:  `CTRL-R`



### Lesson 3

- To **put back** text that has just been deleted, type `p` . 

  > This puts the deleted text **after** the cursor.
  >
  > If a line was deleted it will go on the line below the cursor.

- To **replace** the character under the cursor, type   `r`   and then the character you want to have there.

- The **change** operator allows you to change from the cursor to where the motion takes you.  

  - `ce`  to change from the cursor to the **end** of the **word**
  - `c$`  to change to the **end** of the **line**.

- The format for change:

  - `c  [number]  motion`



### Lesson 4

- To show **location** in the file, type `CTRL-G`.

  - `G` moves to the **end** of the file.

  - `#G` moves to the **#** line. 

    > \# is a number of the target line

  - `gg` moves to the **first** line of the file.

- To search **forward** a phrase, type `/phrase`.

- To search **backward** a phrase, type `?phrase`.

  - `n` for find next in **same** direction.
  - `N` for find next in **opposite** direction.
  - `CTRL-O` takes back to **older** positions.
  - `CTRL-I` takes to **newer** positions.

- To goes to the **(), [], {}** matched, type `%`.

- To substitute the phrase, type `:s/old/new`.

  > For all `:` commands must be finished by hitting `<ENTER>` 

  - for all substitute **on a line**, type `:s/old/new/g`

  - for all substitute **between two line**, type `:#,#s/old/new/g`

    > \#, # means two line numbers, maybe need `CTRL-G` to confirm them.

  - for all substitute **in file**, type `:%S/old/new/g`

  - for ask for confirmation eachtime add 'c' `:%s/old/new`



### Lesson 5

- To executes an external command, type `:!<command>`

- Some file **IO** command:

  - To **read**  a external disk file into current file, type `:r <filename>`

  - To **write** a external disk file from current file, type `:w <filename>`

    > This command would write the whole file into target disk file.

  - When you want to read, \<filename> also can be redirected, like `:r !ls`

    > This command means read the output of shell command `ls` into current vim file.

  - When you want to write,  `v` into visual mode and `motion` select any text, then `:w <filename>` 

    > Just save you select in visual mode.



### Lesson 6

- To **open **(new) a line and start insert mode:
  - Type `o` to open **Below** the cursor
  - Type `O` to open **Above** the cursor
- Combine locate and insert motion:
  - using `w` and `i`, you can move cursor to the first of word and insert before it.
  - using `e` and `a`, you can move cursor to the end of word and insert (or append) after it.
- To yank (**copy**) and puts (**paste**)
  - Type `y` and `p`.
  - you can compose them with other motion, like `yw` can copy one word.
- To enter **replace** mode, type `R` and you can directly cover the previous text by type in new text.
- To set option, using `:set <option>`
  - `ic`   or  `ignorecase`, it **ignore** upper/lower case when searching.
  - `is`   or  `incsearch`,   it show **partial** matches for a search phrases.
  - `hls` or  `hlsearch` ,    it **highlight** all matching phrases.
- To unset option, just prepend "no", like `:set noic`



### Lesson 7

- To Get help,  type`:help`
  - Jump between two windows using `CTRL-W CTRL-W`
  - Quit by `:q`
- To Configure Vim, you need to create a **.vimrc** file
  - The example vimrc file: `$VIMRUNTIME/vimrc_example.vim`
- When typing a  `:`  command, press **CTRL-D** to see possible completions.
  - Press **\<TAB\>** to use one completion.





### Other Feature

#### Fold by syntax

In `~/.vimrc`

```bash
set foldmethod=syntax
```

The most useful commands for working with folds are:

- `z o` opens a fold at the cursor.
- `z Shift+o` opens all folds at the cursor.
- `z c` closes a fold at the cursor.
- `z m` increases the `foldlevel` by one.
- `z Shift+m` closes all open folds.
- `z r` decreases the `foldlevel` by one.
- `z Shift+r` decreases the `foldlevel` to zero -- all folds will be open.

