# The Vim Register

An operation that removes text automatically saves the removed text into the register. For example: `y`, `x`, `c`,`d`, etc. To access the register in **normal** mode you use `"<register>`. For example `"0p` to paste the content of register `0` after the cursor.`ctrl-r <register>` can be used to insert the content of the given register while in **insert** mode.

## The unnamed register (`""`)
`""`: Is the default register. It stores the last text you yanked, changed, or deleted. `p` and `P` automatically reads this register. It is equivalent to `""p`.

## The numbered registers (`0-9`)
They automatically fill themselves up in ascending order. The are 2 different numbered registers: The yanked register (`0`) and the numbered registers (`1-9`).

* The yanked register (`0`): If you yank an entire line of text (`yy`), Vim actually saves that text in two registers.
    1. The unnamed register.
    2. The yanked register

    They will be replaced every time a yank operation is performed. Other operation will not be stored in register `0`.

* The numbered register (`1-9`): When you change or delete a text that is a least one line long, for example (`dd`), that text will be stored in the numbered registers sorted by the most recent.

## The small delete register (`-`)
Changes or deletions less than one line are not stored in the numbered registers `0-9`, but in the small delete register. For example (`dw`, `cw`,`x`).

## The named register (`a-z`)
It can store yanked, deleted, and changed text into registers `a-z`. Unlike the previous 3 register types you've seen which automatically stores text into registers, you have to explicitly tell Vim to use the named register, giving you full control.

  * **Lowercase named register**: Stores the text into the register. For example `"ayiw`: yanks the current word into the `a` register, replacing the previous content.
  * **Uppercase named register**: Appends the text into the register. For example `"Ayiw`: yanks the current word into the `a` register, appending to the previous content.

## The read-only registers (`:`, `.`, `%`)
Vim has three read-only registers: `:`, `.`, and `%`. They are pretty simple to use:
  * `.`: Stores the last inserted text
  * `:`: Stores the last executed command
  * `%`: Stores the name of the current file 

