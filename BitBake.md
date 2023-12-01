Bitbake is sensitive to the original directory layout.  If you rename a directory you will get the following error:

> 	_The following layer directories do not exist:_

It can be fixed by editing the layers in `bblayers.conf`

If `bblayers.conf` doesn't exist then Bitbake expects `BBPATH` and `BBFILES` are set in the environment.

# Options

`bitbake -e` : Outputs entire build configuration.
`bitbake RECIPE -e` : Outputs build configuration for specified _RECIPE_.

`bitbake -g RECIPE` : Generate dependency graph for *RECIPE*

`bitbake -S SIGNATURE_HANDLER`: Dump signature information.
	For example:
		- `bitbake RECIPE -cCOMMAND -Snone`
		- `bitbake RECIPE -cCOMMAND -Sprintdiff`

For comprehensive list of options, see [Usage and syntax](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-intro.html#usage-and-syntax).

# Datastore

## [Functions for Accessing Datastore Variables](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#functions-for-accessing-datastore-variables)
Access Datastore using these functions in `.bb` files.

`d.getVar("X", expand=False)`
- Returns the value of variable "X". Using "expand=True" expands the value.

`d.setVar("X", "value")`
- Sets the variable "X" to "value".

`d.appendVar("X", "value")`
- Adds "value" to the end of the variable "X".

`d.prependVar("X", "value")`
- Adds "value" to the start of the variable "X".

`d.delVar("X")`
- Deletes the variable "X" from the datastore.

`d.renameVar("X", "Y")`
- Renames the variable "X" to "Y".

`d.getVarFlag("X", flag, expand=False)`
- Gets then named flag from the variable "X". Using "expand=True" expands the named flag.

`d.setVarFlag("X", flag, "value")`
- Sets the named flag for variable "X" to "value".

`d.appendVarFlag("X", flag, "value")`
- Appends "value" to the named flag on the variable "X".

`d.prependVarFlag("X", flag, "value")`
- Prepends "value" to the named flag on the variable "X".

`d.delVarFlag("X", flag)`
- Deletes the named flag on the variable "X" from the datastore.

`d.setVarFlags("X", flagsdict)`
- Sets the flags specified in the `flagsdict()` parameter. `setVarFlags` does not clear previous flags. Think of this operation as `addVarFlags`.

`d.getVarFlags("X")`
- Returns a `flagsdict` of the flags for the variable "X".

`d.delVarFlags("X")`
- Deletes all the flags for the variable "X".

# Dependencies

Add dependency:
```
PACKAGE_ARCHS[vardeps] = "MACHINE"
```

Exclude dependency:
```
PACKAGE_ARCHS[vardepsexclude] = "MACHINE"
```

# Variables

## Setting Variables

Set value.  Expands on use.
```
A = ${ANOTHER_VARIABLE}
```

Set value.  Expands immediately.
```
A := ${ANOTHER_VARIABLE}
```

Set default value:
```
A ?= aval
```
This sets `A` to `aval` only if `A` is not already set.

There is a weaker version which is. 
```
A ??= eval
```
This sets `A` only if it is not set and does it immediately.  It can be overriden by following `??=` sets.

See [Variable Expansion](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#variable-expansion) and below for more details.

## Appending and Prepending

`+=` - Append with space
`=+` - Prepend with space
`.=` Append without space
`=.` Prepend without space
`:append` - Append without space.  Use internal space to use space.  See:
```
D = dval
D:append = " additional data"
```
D becomes "dval additional data".  Similarily for `:prepend`

See [Sections on appending and prepending](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#appending-and-prepending-with-spaces).

## Removal

`VAR:remove` - Removes all items in specified list.

## Export Variables

Export variables to environment.
```
export ENV_VARIABLE
ENV_VARIABLE = "value fro the environment"

do_foo() {
    bbplain "$ENV_VARIABLE"
}
```
See [Section 3.2](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#exporting-variables-to-the-environment).  Also, see [Examples section](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#examples) for detailed examples.

# `require` vs. `include`

`require` will throw an error if the specified file isn't found while `include` will not.

# Functions

## BitBake Functions

Python functions are prefixed with `python` while shell functions have no prefix.

## Normal Python Functions

Defined like a normal Python function.  For example, it doesn't require `python` prefix and doesn't use curly braces.

See [relevant section](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#python-functions) for more details.

# Variable Flags

Used to configure task's functionality and dependencies.  See [Variable Flags](https://docs.yoctoproject.org/bitbake/2.2/bitbake-user-manual/bitbake-user-manual-metadata.html#variable-flags) in the documentation.

`[noexec]` - Set to `1` to skip specified task.