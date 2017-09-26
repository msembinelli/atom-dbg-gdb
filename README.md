# dbg-gdb-custom-server package

An interactive GDB debugger for Atom.

dbg-gdb-custom-server additions:

Based on dbg-gdb, but removes some of the hardcoded start commands, and provides an option for a debug server. Great for debugging remote embedded targets.

Removed commands: 'set mi-async on' && 'set target-async on' as these cause problems for remote targets.

![Debug screenshot](http://i.imgur.com/XcI592U.png)

## How to use

1. Right click on an executable in the treeview, select `Debug this file`, and click `Save`
2. (Optional) Customize the gdb_executable, gdb_arguments, server_executable, and server_arguments if your device is a remote/embedded target.
3. Toggle breakpoints by clicking beside line numbers or pressing `F9`
4. Press `F5`, and select the executable
5. ...
6. Profit!

## Service: `dbgProvider`

Creates a `dbgProvider` for GDB, see [basic dbgProvider  service description](https://github.com/31i73/atom-dbg#consumed-service-dbgprovider)

## Supported options
> `path` - *Optional*. The path to the file to debug  
> `args` - *Optional*. An array of arguments to pass to the file being debugged  
> `cwd` - *Optional*. The working directory to use when debugging  
> `env_vars` - *Optional*. An array of environmental variables, ex: ['VAR1=9', 'VAR2=thing', ...]  
> `gdb_executable` - *Optional*. The full command used to execute gdb (defaults to 'gdb')  
> `gdb_arguments` - *Optional*. An array of extra arguments to pass to gdb (note that the arguments ['-quiet', '--interpreter=mi2'] are always included first)  
> `gdb_commands` - *Optional*. An array of commands to pass to gdb, once active (these are executed last of all, but right before '-exec-run')  
> `server_executable` - *Optional*. Starts a remote GDB server of your choice, ex: 'JLinkGDBServerCL')  
> `server_arguments` - *Optional*. An array of extra arguments to pass to the remote GDB server ex: ['-if', 'swd', '-device', 'nRF52832_xxAA'])  

For a list of features and all available keyboard shortcuts, please see [dbg](https://atom.io/packages/dbg) and [dbg-gdb](https://atom.io/packages/dbg-gdb)

## Example .atom-dbg.cson for nRF52 Embedded Target
```
"out\\out.axf":
	debugger: "dbg-gdb-custom-server"
	gdb_executable: 'arm-none-eabi-gdb'
	gdb_commands: ['target remote localhost:2331', 'monitor speed 1000',
                       'monitor clrbp', 'monitor reset', 'monitor halt',
                       'monitor regs', 'monitor flash breakpoints 1',
                       'monitor semihosting enable', 'monitor semihosting IOClient 1',
                       'monitor SWO DisableTarget 0xFFFFFFFF',
                       'monitor SWO EnableTarget 0 0 0x1 0']
	path: "out\\out.axf"
	cwd: "out"
	server_executable: 'JLinkGDBServerCL'
	server_arguments: ['-if', 'swd', '-device', 'nRF52832_xxAA',
	                   '-endian', 'little', '-speed', '1000', '-port',
                           '2331', '-swoport', '2332', '-telnetport',
                           '2333', '-vd', '-ir', '-localhostonly', '1',
                           '-singlerun', '-strict', '-timeout', '0']
```
