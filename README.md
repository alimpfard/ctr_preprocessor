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

