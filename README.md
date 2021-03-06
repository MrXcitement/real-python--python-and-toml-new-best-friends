# Python and TOML: New best friends
https://realpython.com/python-toml/

## Summary
A [Real Python](https://realpython.com) tutorial that teaches about TOML, what it is and how to use it.
This repository provides a place to work throught the examples in the tutorial.

## 1.0 Use TOML as a Configuration Format
- TOML: Tom’s Obvious Minimal Language
- Configuration file format

### 1.1 Configurations and Configuration Files
- Configuration files allow an app to change behavior without changeing source code.
- Seperation of code and settings.
- Increase knowledge of system configurability
- Decrease *magic values* in the system
- Example config file:
```ini
player_x_color = blue
player_o_color = green
board_size     = 3
server_url     = https://tictactoe.example.com/
```
- Benifits from moving settings to config file:
    - Explicit *names* to values
    - *Visibity* to values
    - Simpler to *change* values
- You may want more organization of your configuration
    - Some items may go together
    - Some items may not be *configurable*, ie ```board_size```
    - Some items *could* be changed, say the ```url``` might be changed if *power* use has another server to use.
- Revised config file with section names
```ini
[user]
player_x_color = blue
player_o_color = green

[contant]
board_state = 3

[server]
url = https://tictactoe.example.com/
```
- By adding section headings, each config item should be more clearer
- Many config file formats
    - INI is often used on windows
    - plain-text, human readable, variety of formats on Unix/macOS
    - XML, JSON, YAML can be used as config files, however they are fidly due to be designed for data interchange or serialization instead of config.
### 1.2 TOML: Tom’s Obvious Minimal Language
- First release 0.1.0 in 2013
- Focus: minimal config file format, human readable.
- popular among python tools: [Black](https://black.readthedocs.io/), [pytest](https://docs.pytest.org/),[mypy](https://mypy.readthedocs.io/) and [isort](https://black.readthedocs.io/)
- [TOML parsers](https://github.com/toml-lang/toml/wiki#implementations) available for many languages
- TOML config
```TOML
[user]
player_x_color = "blue"
player_o_color = "green"

[contant]
board_state = 3

[server]
url = "https://tictactoe.example.com/"
```
- Advantage over INI files, there is a *specification* for the file format.
- TOML has *types* so the config setting: player_x_color is assigned a *string* type with the value of "blue"
- A criticisim is that the human editing a TOML file will need to know about types
- TOML is *not* meant to be used as a data interchange or serialization format.
- TOML has some restrictions
    - All *keys* are strings
    - No *null* type
    - Whitespace may be important, could impact compression
- Primary (*Always*!?) use TOML for config
### 1.3 TOML Schema Validation
- Syntax requirements
- *Schema* requirements
    - url may be required
    - colors may be optional
- TOML does not include a schema language
- *Schema* will need to be validated manually
- Use a method that validates your config.
- Could use Python 3.10's patern matching to simplify
- Use other libraries that provide data validation, like *pydantic* if your configuration is more complicated
- [Taplo](https://taplo.tamasfe.dev/) is a rust and javascript library and cli that provides validation and is availbale as a VSCode extension [Even Better TOML](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml)
## 2.0 Get to Know TOML: Key-Value Pairs
- built around [key-value pairs](https://toml.io/en/v1.0.0#keyvalue-pair), this maps well to hash tables
- values have specific types
    - [String](https://toml.io/en/v1.0.0#string)
    - [Integer](https://toml.io/en/v1.0.0#integer)
    - [Float](https://toml.io/en/v1.0.0#float)
    - [Boolean](https://toml.io/en/v1.0.0#boolean)
    - [Offset Date-Time](https://toml.io/en/v1.0.0#offset-date-time)
    - [Local Date-Time](https://toml.io/en/v1.0.0#local-date-time)
    - [Local Date](https://toml.io/en/v1.0.0#local-date)
    - [Local Time](https://toml.io/en/v1.0.0#local-time)
    - [Array](https://toml.io/en/v1.0.0#array)
    - [Inline Table](https://toml.io/en/v1.0.0#inline-table)
- [Tables](https://toml.io/en/v1.0.0#tables) and [Array of Tables](https://toml.io/en/v1.0.0#array-of-tables) can be used to *categorize* or *organize* several key-value pairs.
- A bare minimum TOML file must have a *key-value* pair
- The *value* has a type infered by it's format
```TOML
key_string = "string"
key_integer = 42
key_float = 42.0
```
- The *key* is always a string
```TOML
greeting = "Hello, TOML!"
42 = "Life, the universe, and everything"
```
- TOML documents *must* be encoded in UTF-8
- Add quotation marks around keys to force keys to use unicode.
```TOML
"realpython.com" = "Real Python"
"blåbærsyltetøy" = "blueberry jam"
"Tom Preston-Werner" = "creator"
```
- In general you shoud use *bare* keys without quotes
- Dots in unquoted keys trigger grouping by splitting at each dot
```TOML
player_x.symbol = 'X'
player_x.color  = "purple"
```
- Here `symbol` and `color` are grouped in a section named `player_x`
### 2.1 Strings, Numbers, and Booleans
- TOML syntax similar to Python's
- String can use double quotes, single quotes
    - Single quotes are *literal* strings, escape codes not interpreted.
    - Double quotes allow special escape characters, allows escaped unicode characters to be interpreted
- Strings can use triple quotes, either double or single, this allows multiple line strings to be specified
- Numbers are either *integer* or *floating point*
- *Integer* values ae whole numbers, can use `_` character for readability of large numbers.
```TOML
number = 42
negative = -8
large = 60_481_729
```
- *Floating-point* are decimal numbers, integer, dot, fractional parts
- Floats can use scientific notation
- TOML also supports special values like infinity or NaN
```TOML
number = 3.11
googol = 1e100
mole = 6.22e23
negative_infinity = -inf
not-a-number = nan
```
- Non-negative integers can be hex, oct or bin using a 0x, 0o, or 0b prefix.
- Boolean values are represented as `true` or `false` must be all lowercase.
### 2.2 Tables
- Since TOML documents consist of *key-value* pairs they would be stored in a *hash table* data structure.
- In python that would be dictionary or dictionary-like data structure
- To organize the *key-value* pairs, we can use *tables*
- Three ways to specify *tables*
    - use *regular tables* with *headers* to seperate the *key-value* pairs into tables, should be default table type
    - use *dotted key tables* when you need to specify *key-value* pairs that are closely tied to the parent
    - use *inline tables* for very small tables
- Only use *dotted key tables* or *inline tables* when they clarify intent
- Example tables
```TOML
[user]
player_x.color = "blue"
player_o.color = "green"

[constant]
board_size = 3

[server]
url = "https://tictactoe.example.com"
```
- Table headers: user, constant and server
- Dotted key tables: player_x and player_o
- Example `[user]` table with nested regular, not dotted key tables
```TOML
[user]

    [user.player_x]
    color = "blue"

    [user.player_o]
    color = "green"
```
- For this case, the *dotted key tables* seem to be clearer.
- Note that the full name of the nested table must be used, indentation is only used above to make it more readable.
- Example `[user]` table with an additional key for the `[user.player_x]` and `[user.player_o]` tables
```TOML
[user]

    [user.player_x]
    symbol = "X"
    color = "blue"

    [user.player_o]
    symbol = "O"
    color = "green"
```
- Clarity two different player tables and the *key-value* pairs for each one
- Example `[user]` table with *dotted key tables* instead of nested as above.
```TOML
[user]
player_x.symbol = "X"
player_x.color = "blue"
player_o.symbol = "O"
player_o.color = "green"
```
- Example `[user]` table with *inline tables*
```TOML
[user]
player_x = { symbol = "X", color = "blue" }
player_o = { symbol = "O", color = "green" }
```
- TOML documents are defined as a nameless root table
- *key-pairs* defined at before any *table* header are defined in the root table.
- a *table* includes all *key-value* pairs until the next *table* header
- Be aware that indentation can confuse you to think a *key-value* pair is in a table that it is not.
- I would recomend *not* indenting the TOML file.
### 2.3 Times and Dates
- Four date representations
    - An *offset date-time* is a timestamp with time zone information, representing a specific instant in time.
    - A *local date-time* is a timestamp without time zone information.
    - A *local date* is a date without any time zone information. You typically use this to represent a full day.
    - A *local time* is a time with any date or time zone information. You use a local time to represent a time of day.
- Representation based on [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339)
- Example of each time and date representations
```TOML
offset_date-time     = 2021-01-12 01:23:45+01:00
offset_date-time_utc = 2021-01-12 00:23:45Z
local_date-time      = 2021-01-12 01:23:45
local_date           = 2021-01-12
local_time           = 01:23:45
local_time_with_us   = 01:23:45.654321
```
### 2.4 Arrays
- An ordered list of values
- Specify with square braces
```TOML
packages = ["tomllib", "tomli", "tomli_w", "tomlkit"]
```
- Arrays can contain
    - Any data type, including Arrays
    - Different data types in an array
- Arrays can span multiple lines
- You can use a trailing comma after last element
- Arrays of tables can be written inline
```TOML
players = [
    { symbol = "X", color = "blue", ai = true },
    { symbol = "O", color = "green", ai = false },
]
```
- However, it is *recomended* to use the double square bracket syntax instead.
```TOML
[[players]]
symbol = "X"
color = "blue"
ai = true

[[players]]
symbol = "O"
color = "green"
ai = false
```
- This is more readable and is the same as the inline table syntax above.
## 3.0 Load TOML With Python
### 3.1 Read TOML Documents With tomli and tomllib
- [tomli](https://pypi.org/project/tomli/)
- [tomllib](https://docs.python.org/3.11/library/tomllib.html)
- TOML support will be in Python 3.11+
- The builtin module will be based on `tomllib`
- Create a simple toml file [tic_tac_toe.toml](./tic_tac_toe.toml)
- `tomli` module only has two functions: `load` and `loads`
- `load` will read a [file object] into a dictionary
    - The file must be open in binary mode, ie `mode=rb`
- `loads` will read a properly encoded python string into a dictionary
    - You can create a triple quoted string to test `loads`
    - Make sure if you read text from a file to encode it as "utf-8"
        - Path('pathname').read_text(encoding="utf-8")
- To handle the transition to `tomllib` you can:
```Python
try:
    import tomllib
except ModuleNotFoundError:
    import tomli as tomllib
```
### 3.2 Compare TOML Types and Python Types
- TOML specification mentions some requirements on its own types.
    - A TOML file must be a valid UTF-8 encoded Unicode document.
    - Arbitrary 64-bit signed integers (from −2^63 to 2^63−1) should be accepted and handled losslessly.
    - Floats should be implemented as IEEE 754 binary64 values.
- Python types are a close match for the above requiremnts
    - file handling usually defaults to using UTF-8
    - Integers are implements as arbitrary-precision integers, which handle the required range and much larger numbers
    - Floats follow IEEE 754
- Python's tomllib [documentation](https://docs.python.org/3.11/library/tomllib.html#conversion-table) has a TOML <-> Python conversion table.
- `load` and `loads` functions provide a paramter to determine how a `float` is parsed. If you need greater precision you may need this parameter.
### 3.3 Use Configuration Files in Your Projects
- Config files:
    - *names* values and concepts
    - provides more *visibility* for specific values
    - makes values simpler to *change*
- How to use?
    - make sure config is *parsed once*
    - how to access from *different modules*
- Wrap config in a Python Module resolves these questions.
- Create a `config` folder and place the config file in it
- Create an `__init__.py` file in the `config` folder
- In the `__init__.py` read the config file into a dictionary
- Example [__init__.py](./config/__init__.py)
## 4.0 Dump Python Objects as TOML
### 4.1 Convert Dictionaries to TOML
### 4.2 Write TOML Documents With tomli_w
## 5.0 Create New TOML Documents
### 5.1 Format and Style TOML Documents
### 5.2 Create TOML From Scratch With tomlkit
## 6.0 Update Existing TOML Documents
### 6.1 Represent TOML as tomlkit Objects
### 6.2 Read and Write TOML Losslessly
## 7.0 Conclusion