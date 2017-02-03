# dbg-gdb package

An interactive GDB debugger for Atom

![Debug screenshot](http://i.imgur.com/BdBA0yR.png)

## How to use

1. Right click on an executable in the treeview, select `Debug this file`, and click `Save`
2. Toggle breakpoints by clicking beside line numbers or pressing `F9`
3. Press `F5`, and select the executable
4. ...
5. Profit!

## Service: `dbgProvider`

Creates a `dbgProvider` for GDB, see [basic dbgProvider  service description](https://github.com/31i73/atom-dbg#consumed-service-dbgprovider)

## Supported options
> `path` - The path to the file to debug  
> `args` - *Optional*. An array of arguments to pass to the file being debugged  
> `cwd` - *Optional*. The working directory to use when debugging  
> `env_vars` - *Optional*. An array of environmental variables, ex: ['VAR1=9', 'VAR2=thing', ...]  

For a list of features and all available keyboard shortcuts, please see [dbg](https://atom.io/packages/dbg)
