# 2020-01-10 07:47 vim-autocommand

## autocmd

Auto commands are a way to tell _Vim_ to run certain commands whenever certain events happen.

## Autocommand structure

```vim
:autocmd BufNewFile * :write 
              ^     ^  ^
              |     |  |
              |     |  command to run
              |     file matching pattern
              event
```
* Special characters like `<cr>` can't be used in the command section. There is a way to get around this though.
* Multiple events can be bound separating the events with a comma.

## Events

### FileType Events

One of the most useful events is the `FileType` event. This event is fired whenever Vim sets a buffer's `filetype`.
