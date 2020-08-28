# sed Command List

`sed [options] 'address'|'/pattern/'{commands[;commands]} file|stdin`

Options
`-n` : suppress automatic printing of pattern space. (doesn't run step 5 from the execution cycle).
`-r` : use extended regular expressions
`-i` : save changes for string substitution in the same file
`-e` script: add script to the commands to be executed (multiple editing commands)
`-f` script-file:  add the contents of script-file to the commands to be executed

## Pattern : regular expression
## Address : line number `n/m` or $ for last line.
* `n`   : line number `n`.
* `n~m` : get every `m` line starting from `n`.
* `n,m` : get from `n` to `m`.
* `$` : get last line.
* `n,$` : get from `n` to last line.
* /pattern/,`n`: get from pattern to `n`.
* `n`,/pattern/  : get from `n` to pattern.
* /pattern/,`$`: get from pattern to last line.
* /pattern/,+`n` : get pattern and next `n` lines.
* /pattern 1/,/pattern 2/: get from pattern 1 to pattern 2 inclusive.


## Buffers: both are initially empty
* pattern space: working buffer.
* hold space: can store temporal data to be used in the pattern space. It is good to think that initially it holds an empty line. 

## Execution cycle
Each cycle it is executed for each line and continues until the end of file/input is reached.

### For each line
1. Reads a entire line from `stdin`/file.
2. Removes any trailing newline.
3. Places the line in its pattern buffer.
4. Modifies the pattern buffer according to the supplied commands.
5. Prints the pattern buffer to `stdout`.
6. Empties the pattern buffer.

## Basics Commands
* `p` : print data from the pattern buffer
    `sed -n '3p'` : print line number 3.
* `d` : delete the pattern space buffer and immediately starts the next cycle.
    `sed '3d'` : delete line number 3.
* `s/p1/p2/[sub-command]`: Substitutes `p1` with `p2` and optionally runs `sub-commnad`. The `p/d` sub-commands are different from the `p/d` main commands.

## Examples 

* `ranges`
    see Pattern/Address above.
* `p/d` commands:
    prints, deletes the pattern space and starts the next cycle.
    `sed -n '/Violets/p' input.txt` prints the matching line
    `sed -n '/Violets/d' input.txt` removes the matching line
* `;/{}` command:
    semicolon let you specify more than one command. Brackets define a command block.
    `sed -n '1,2{p; d}' input.txt`
* `=` command:
    prints the current line number before printing the pattern space.
    `sed '=' input.txt`
* `n`: command:
    Begins the next cycle. Reads the next line of input into the pattern space.
    `sed '=; n' input.txt`
* `N`: command:
     Appends the next line of input into the pattern space, but without running steps number 5 and 6 of the cycle (see above).
    `sed '=; N' input.txt`
* `P/D` commands:
    If the pattern buffer contains more than one line, it prints/deletes the first one; otherwise, it prints/deletes the current pattern buffer.
    `sed '/are/P' input.txt`
    `sed '/are/D' input.txt`
* `q`
    stops cycle.
* `y///` command:
    replaces character-wise pattern-1 with pattern-2.
    `echo abc | sed 'y/ab/fg/'` results in `fbg`
* `s///p` command:
    substitutes and prints to output.
    `sed 's/foo/bar/p' input.txt`
* `s///I` command:
    substitutes case insensitive
    `sed 's/foo/bar/ip' input.txt`
* `s///w` command:
    substitutes and writes the substitutions to the given file.
    `sed 's/foo/bar/w output.txt' input.txt`
* `w` command:
    writes pattern space to a file.
    `sed 'w output.txt'`
* `r` command:
    append text to pattern space read from filename.
    `sed 'r input.txt'`
* `#`
    comment in a `sed` script
* `-f` option:
    reads a `sed` script
* `l` command:
    shows the pattern space content, useful to debug.
    `sed -n 'N; l; p' input.txt`
* `a` command:
    appends a line after the current line with the given text.
    `sed '2aThis line goes after line 2' input.txt`
* `i` command:
    inserts a line before the current line with the given text.
    `sed '2iThis line goes before line 2' input.txt`
* `c` command:
    changes the current line with the given text.
    `sed '2cThis line is the new line 2' input.txt`
* `h` command:
    replaces the hold space with the content of the pattern space.
* `H` command:
    appends the pattern space to the hold space.
* `g` command:
    replaces the pattern space with the content of the hold space.
* `G` command:
    appends the hold space to the pattern space.
* `x` command:
    swaps the content of the pattern space with the content of the hold space.
* `:` command:
    defines a label.
    `sed -e ':while' -e 'p; p'`
* `b` command:
    jumps to a label.
    `sed -e ':while' -e 'p; p' -e 'bwhile'`
* `t` command:
    jumps to a label, but only if a `s//` command was successful on the last line of input read.
