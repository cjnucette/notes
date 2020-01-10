# 2020-01-08 11:24 vim-map

## map[!]

`map`: creates a key map that works in _normal, visual, select_ and _operator-pending_ modes.

`map!`: creates a key map that works in _insert_ and _command-line_ modes.

## special keys when using nmap

`<C-r><C-w>` or `expand(<cword>)`: returns the current keyword under the cursor.

## special keys when using imap

* `<C-o>`: Goes to normal mode executes the command and returns to insert mode. If the cursor is in the last character in a line in insert mode, then <C-o> moves the cursor one character to the left.

* `<C-\><C-o>`: Same as <C-o> but it doesn't move the cursor. But the now the cursor may be placed on a character beyond the end of line. Both of this commands create a new undo point.

* `gi`: If the cursor position was moved by the map and no new text was inserted, then you can use this command to restart the insert mode from the previous position where the insert mode was last stopped.

* `<C-r>=`: Inserts the result of an expression in insert mode.

## special keys when using vmap

Next:
[vim-autocommand](~/notes/vim-autocommand.md)
