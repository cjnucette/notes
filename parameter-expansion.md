# Parameter expansion

* __:-__ if parameter is not set, use _defaultValue_.
    ``` bash
      var=${parameter:-defaultValue}
    ```
* __:=__ if parameter is unset, then assign value to parameter. this operator can't be used with positional parameters: $1, $2, ..., etc. 
    ``` bash
      var=${parameter:=Value}
    ```
* __:?__ the script is stopped and the given error message is displayed.
    ``` bash
      ${var:?Error var is not defined}
    ```
* __#__ as prefix returns the variable length
    ``` bash
      ${#var}
    ```
* __# (shortest) or ## (longest)__ as infix removes the given _pattern_ from _var_
    ``` bash
      ${var#pattern}

      f="/etc/resolv.conf"
      ${f#*/} # returns etc/resolv.conf
      ${f##*/} # returns resolv.conf
    ```
* __% and %%__ works as # and ##, except it applies to the back of _var_.
    ``` bash
      ${var%pattern}

      f="/etc.resolv.conf"
      ${f%.*} # returns /etc.resolv
      ${f%%.*} # returns /etc 
    ```
* __/pattern/replacement__ replaces pattern with replacement in _var_ single occurrence.
* __//pattern/replacement__ replaces pattern with replacement in _var_ all occurrences.
    ``` bash
      ${var/pattern/replacement}
    ```
* __:offset:length__ returns the substring beginning at _offset_ and _length_ characters long, or to the end of the string if _length_ is not given.
    ``` bash
      ${var:offset:length}
    ```
* __!pattern__ returns all the variables names that match _pattern_.
    ``` bash
      ${!VECH*} # returns any variable which name starts with VECH
    ```
* __^__ capitalize the value of _var_, __^^__ converts to uppercase the value of _var_.
    ``` bash
      name="carlos"
      echo ${name^} # Carlos
      echo ${name^^} # CARLOS
  ```
* __,__ convert the first character to lowercase, __,,__ convert all characters to lowercase.
    ``` bash
      name="CARLOS"
      echo ${name,} # cARLOS
      echo ${name,,} # carlos
    ```
