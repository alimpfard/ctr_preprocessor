# Ctr Preprocessor

A Text Preprocessor with less than magical powers!

### configuration
The configuration can either be supplied by a config file encoded in json, or via the commandline arguments:

`--command_format <format>` The format (regex) of the commands to intercept, e.g. `\#%s`
- Please note that the `%s` must be present in the format.


`--oformat <format>` The format for the name of the output file, e.g. `%{f}_%{e}.%{d}.out`
- Available formatting elements are: 
-   - `%{F}` the whole file name before preprocessing
-   - `%{f}` the file name without the last extension
-   - `%{e}` the extension of the file

`--config <config>` The config file to use (Will override the cmdline arguments)

`--interp_all <True|False>` whether all macros should interpolate their values

### Macros

Currently only a few macros are present:
* `+ <text>`: Text copied verbatim into the output file, but would allow substitution if interp_all is enabled.
* `- <text>`: Text __not__ copied into the output file, but still accessible to the substitution system.
* `e <expr>`: Evaluate citron expression discarding the value.
* `d <name> <expr>`: Defines a variable 
* `p <expr>`: Prints the value of an expression into the output. (\*)
* `call <name> <expr>*`: calls a function with the given values and prints the value in the output (\*)

_\*_ Should the value be an array, it will be expanded with newlines first; 
These macros respect the indentation they are placed at, and expand to their respective indentation level.

#### example

##### config:
```json
{
    "command_format": "\\#%s",
    "oformat": "%{f}.out",
    "interp_all": false
}
```
input file:
```
Test
#- This will not be copied verbatim
#+ This will, however.
#d test $#-2
    #p [test] * 4
```

output file:
```
Test
 #+ This will, however.
     This will not be copied verbatim
 This will, however.
     This will not be copied verbatim
 This will, however.
     This will not be copied verbatim
 This will, however.
     This will not be copied verbatim
 This will, however.

```
