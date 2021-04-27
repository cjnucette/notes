# Nvim Plugin with Lua

1. In the project directory create a folder named `plugin`.  
Run: `$ mkdir plugin`

2. In the `plugin` directory create a file with the name of your plugin with an extension `.vim`  
Run: `touch plugin-name.vim`

3. Create a `lua\plugin-name` directory in the project directory.  
Run: `$ mkdir -p lua\plugin-name`

4. Then create a file named `init.lua` within the previous directory.  
Run: `$ touch init.lua`

5. Set the runtime path to the project directory, which is  where the `plugin`  and `lua` directory should be located.  
Run: `$ nvim --cmd "set rtp+=$(pwd)"`

