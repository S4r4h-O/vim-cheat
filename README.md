# Vim/Nvim cheatsheet

## 1. Perform operation only on selected lines

Enter V-LINE mode (`V`), selecte the lines, press `:`. If you want to replace
something using regex, it should look like this: `:'<, '>s/pattern/replacement/{gic}`.

## 2. Add "- " to the beginning of many contiguous lines

```vim
:2,7normal I- 
:9,12normal I- 
:22,23normal I- 
```

or (in V-LINE mode) `:'<, '>normal I-`.

## 3. Insert text n times

Execute the sequence `5oItem 0`, being 5 at the beginning any arbitrary number
of your choice. This insert will look like this:

```
Item 0
Item 0
Item 0
Item 0
Item 0
```

## 4. Increment the numbers of a numbered list

Using the previous example, press `vip`, this will select the entire paragraph.
Now press `gCtrl+a`. Your list will look like this:

```
Item 1
Item 2
Item 3
Item 4
Item 5
```

## 5. Inside and around operations

Ex 1. `"Somehing something"`

Ex 2. `(Somehing something)`

Ex 3. `[Somehing something]`

To copy somenthing inside of quotes, parenthesis, braces, brackets or anything
else, press `yi+{|[|(|"`.

To delete and start editing inside something, press `ci+{|[|(|"`.

I think you got it, the same applies to d/D, v/V, etc.

## 6. Organize columns

Suppose you have something like:

```c
int a = 1;
int ab = 2;
int abc = 3;
int abcxyz = 1000;
```

You can make it look like this:

```c
int  a       =  1;
int  ab      =  2;
int  abc     =  3;
int  abcxyz  =  1000;
```

Using the mothods described in 1 or 2, run `:'<, '>%!column -t`.

## 7. File explorer (netrw)

Vim/Nvim comes with a native file explorer called netrw. Open it with `:Ex` or
`:Explore`. Open it in a vertical split with :Vex or in a horizontal split with
`:Sex`. To open a left-side explorer window, use :Lex. To open a horizontal
explorer taking up 30 lines of the terminal, run `:30Sex`. To open a left-side
explorer with a width of 30 columns, run `:30Lex`.

Add to your .vimrc:

```vim
" netrw
let g:netrw_liststyle = 3 "Opens in tree mode
nnoremap <leader>e :<C-u>30Vex<CR>
```

## 8. Terminal

Open the terminal with `:terminal`. You can combine with other commands like
`:10split | terminal ++curwin`.

## 8. File Operations

Copy the entire file with `:silent! %y+`. Delete the entire file without
affecting the registers or clipboard with `:silent! %delete _`

Delete extra space at the end of lines with `:%s/\s\+$//e`.

Save with privileges: `w !sude tee %`

Replace occurrence in all the buffers: `:bufdo %s/foo/bar/g | update`

Changes list: `:changes`. Last change `g;`, next `g,`

## 9. Insert mode navigation

While in insert mode, you can just `<C-m>` to insert a new line below, or break
the current one if you're not at the end. If you want to insert a new line regar
dless of the position, you can use these maps:

```lua
-- nvim
vim.keymap.set("i", "<C-k>", "<C-o>O", { desc = "Insert line above when in insert mode" })
vim.keymap.set("i", "<C-j>", "<C-o>o", { desc = "Insert lines below when in insert mode" })
```

```vim
" vim
inoremap <C-j> <C-o>o
inoremap <C-k> <C-o>O
```

If you want to navigate up and down without leaving insert mode and not using the arrow keys, you can `<C-g>j` and `<C-g>k`. My mappings are:

```lua
-- nvim
vim.keymap.set("i", "<C-n>", "<C-g>j", { desc = "Go to line below in insert mode" })
vim.keymap.set("i", "<C-p>", "<C-g>k", { desc = "Go to line above in insert mode" })
```

```vim
" vim
inoremap <C-n> <C-g>j
inoremap <C-p> <C-g>k
```

If you want to navigate one char backward/forward:

```lua
-- nvim
vim.keymap.set("i", "<A-h>", "<C-o>h", { desc = "Go to previous caracter while in insert mode" })
vim.keymap.set("i", "<A-l>", "<C-o>l", { desc = "Go to previous caracter while in insert mode" })
```

```vim
" vim
inoremap <A-h> <C-o>h
inoremap <A-l> <C-o>l
```

If you want to jump words:

```lua
-- nvim
vim.keymap.set("i", "<C-,>", "<C-o>b", { desc = "Go to previous word in insert mode" })
vim.keymap.set("i", "<C-.>", "<C-o>w", { desc = "Go to next word in insert mode" })
vim.keymap.set("i", "<C-S->>", "<C-o>W", { desc = "Go to next WORD in insert mode" })
vim.keymap.set("i", "<C-S-<>", "<C-o>B", { desc = "Go to previous WORD in insert mode" })
```

```vim
" vim
inoremap <C-,> <C-o>b
inoremap <C-.> <C-o>w
inoremap <C-S->> <C-o>W
inoremap <C-S-<> <C-o>B
```
