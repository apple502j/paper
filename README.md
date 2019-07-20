# paper - Compiling PaperFOrmat (PFO) documents
## Requirements
- Basic use: Py(3.6+)
- `setup.py`: pngquant installed, and `scratchapi2` package

## PFO Format
### Standard
- One empty line represents a `<br>`.
- `//` disables parsing for one line.
- `||` is a one-line-comment which will be omitted when compiling.

### Special Variables
- `{{ss}}` for `//`
- `{{ll}}` for `||`
- `{{cYear}}`, `{{cMonth}}`, `{{cDay}}`, `{{cHour}}`, `{{cMinute}}` - The time when the page was compiled at.

### Custom tags
**Custom tags** are defined with regex and replacer. Replacer can be a function that takes converter as positional argument, regex-matched items as args and kwargs. It also can be a string. When string is passed, `{0}` will be replaced with the first argument, and so on, for args and kwargs. **Only one custom tag should be put in a line.**

## How to use
### setup.py
`setup.py` **must** define a function `get_compiler()`. It should take no arguments and return an instance of `compiler.Compiler`. You may want to add tags there.

These hooks can be used:
- `before_compile(compiler)`
- `before_folder_write(compiler, dirname, filename)`
- `before_file_write(compiler, filename)`
- `after_compile(compiler)`

For example, this example handles PNG compression in before_compile hook.

### GenericData
`Compiler.misc` is a GenericData. It can be used when you want to use the value between tags and hooks.

### CLI
This is a CLI-based utility, so you use this like `python3 compiler.py <dirname-or-filename>`. When dirname is specified, any files in that directory (not subdirectory) with the extension `.pfo` will be compiled.

Compiled files will have extension of `.html`.
