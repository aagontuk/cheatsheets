### Automatic Variables ###

* $@ - Filename of the target.
* $< - The name of the first prerequisites.
* $? - Name of all the prerequisites that are newer than the target.
* $^ - Name of all the prerequisites.
* $+ - Same as `$^` with duplicate prerequisites.

### VPATH and vpath ###

Path to search the targets.

### Assignments to variables ###

* `=`  - Recursively expanded assignment. `${VAR} = ${VAR} val` not allowed.
* `:=` - Simply expanded assignment. `${VAR} = ${VAR} val` allowed.
* `?=` - Only assign if doesn't exist.
* `!=` - Execute a shell script and assign output to variable. Can
       be replaced with `{VAR} := $(shell command)`
