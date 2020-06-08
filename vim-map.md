# 2020-01-08 11:24 vim-map


## Special keys and functions when using normal mode map

### map[!]

* `map`: creates a key map that works in _normal, visual, select_ and _operator-pending_ modes.

* `map!`: creates a key map that works in _insert_ and _command-line_ modes.

### Special keys
* `<C-r><C-w>`: returns the current keyword under the cursor.

### Special functions 
* `expand(<cword>)`: returns the current keyword under the cursor.


## Special keys and functions when using insert mode map

### imap and inoremap

* `imap`: creates a key map that works in _insert_ mode.
* `inoremap`: Same as above but doesn't recurse the {rhs}.

### Special keys
* `<C-o>`: Goes to normal mode executes the command and returns to insert mode. If the cursor is in the last character in a line in insert mode, then <C-o> moves the cursor one character to the left.

* `<C-\><C-o>`: Same as <C-o> but it doesn't move the cursor. But the now the cursor may be placed on a character beyond the end of line. Both of this commands create a new undo point.

* `gi`: If the cursor position was moved by the map and no new text was inserted, then you can use this command to restart the insert mode from the previous position where the insert mode was last stopped.

* `<C-r>=`: Inserts the result of an expression in insert mode.

## Special keys and functions when using visual mode map

### vmap and vnoremap.

* `vmap`: Creates a key map in _visual_ and _select_ modes.
* `vnoremap`: Same as above but doesn't recurse {rhs}.

### Special keys
* `'<`: Is a Vim mark that represents the first _line_ of a visual region.
* `'>`: Represents the last _line_ of a visual region.
* `` `< ``: Represents the beginner of the _character position_ of the visual region.
* `` `> ``: Represents the end of the _character position_ of the visual region.
* `<C-r>`: If we want to use the visually selected text in our map, then you can yank the text and then use it in our map: `vnoremap g/ y/<C-r>"<CR>`. `<C-r>"`: inserts the content of the _unnamed register_ (").
* `<C-u>`: If for any reason you need to remove the select region marks when executing an `Ex` (`:`) command, then use this command. It deletes every character from the beginning of the line until the current cursor position.
* `gv`: When you enter the command mode using `:` in visual mode, the visual mode is stopped. If you want to re-enter the visual mode from a function invoked from a map, you can use this command.

### Special functions
* `visualmode()`: Is a function that returns the current visual mode: _v_ character-wise visual, _V_: line-wise visual, _\<C-v>_: block-wise visual.

### Notes
* The maps created with `vmap` and `vnoremap` commands work in both Visual and Select mode. To create a map that works only in Visual mode use `xmap` or `xnoremap`, to create a map that works only in Select mode use `smap` or `snoremap`.


## Special keys and functions when using command-line mode map

### cmap and cnoremap

* `cmap`: Create a key map in _command-line_ mode.
* `cnoremap`: Same as above without recurse {rhs}.

`cmap` and `cnoremap`: Are maps that work in command-line mode that works in the following command prompts: 

* `:`: Ex command prompt.
* `/`, `?`: Forward and Backward search.
* `>`: Debug prompt.
* `@`: input() prompt.
* `:insert` and `:append`: prompts.

### Special functions
* `getcmdtype()`: Let you distinguish between the above prompts in your map.
* `setcmdpos()`: Let you changed the location of the cursor in the command-line.
* `getcmdline()`: Let you get the current command-line.

### Special Keys: 
* `<C-r>=`: Inserts the value returned by the invoked function at the current location in the command-line.
* `<C-\e>`: Replaces the entire command-line with the value returned by the invoked function.
* `cnoremap <expr> <C-F6> Cmdfunc()`: Using this map, the value returned by Cmdfunc() is inserted at the current location in the command-line.

### Notes
* It is preferable to use a non-printable control character for invoking a command-line mode map. Otherwise, the map may interfere with the printable characters used in the Vim Ex commands.
* If the `paste` option is set, then command-line mode maps are disabled.

## Special keys and functions when using operator-pending mode map

### omap and onoremap

You can create maps that work when waiting for a motion command or text object from an operator command. 

### Notes
* To change the starting location of the operator from a operator-pending mode map, you can start visual mode and select the desired range of characters. One disadvantage in starting visual mode is that the previous visual region will be lost.

## Mapping Mouse Events

 


Next:
[vim-autocommand](~/notes/vim-autocommand.md)
