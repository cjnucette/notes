# Lua Variables

`Lua` is a dynamic typed language. This means that you don't have to specify the type of the variable when it is defined. However; variables in `lua` can hold values of the following types:
  * `nil` - no value. This is the default value of variables. 
  * Number - 64bit double-precision floating-point numbers.
  * String - Stores sequence of characters. Delimiters: 'chars', "chars", [[chars]] this last is used for multi-line strings.
  * Boolean - true, false, nil evaluates to false, and everything else evaluates to true.
  * Table - The only data structure in `lua`, can be used to represent record, lists, dictionaries, etc. `{}` are used create a table. Use `key = value` pairs to define a record or just the value to define an indexed array which starts at 1.
  * Function - first order function. Can be stored in a variable, passed as a function parameter, and as a return value.
  * Userdata - Use to represent new data types.
  * Thread - store co-routine instances in variables.
