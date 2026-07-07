# Vim/Nvim cheatsheet

## 1. Perform operation only on selected lines

Enter V-LINE mode (`V`), selecte the lines, press `:`. If you want to replace
something using regex, it should look like this: `:'<, '>s/pattern/replacement/{gic}`.

## 2. Add "- " to the beginning of many contiguous lines:

```vim
:2,7normal I- 
:9,12normal I- 
:22,23normal I- 
```

or (in V-LINE mode) `:'<, '>normal I- `.

## 3. Insert text n times

Execute the sequence `5oItem 0`, being 5 at the beginning any arbitrary number
of your choice. This insert will look like this:

Item 0
Item 0
Item 0
Item 0
Item 0

## 4. Increment the numbers of a numbered list

Using the previous example, press `vip`, this will select the entire paragraph.
Now press `gCtrl+a`. Your list will look like this:

Item 1
Item 2
Item 3
Item 4
Item 5

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
