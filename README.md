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
## 2.0 Get to Know TOML: Key-Value Pairs
### 2.1 Strings, Numbers, and Booleans
### 2.2 Tables
### 2.3 Times and Dates
### 2.4 Arrays
## 3.0 Load TOML With Python
### 3.1 Read TOML Documents With tomli and tomllib
### 3.2 Compare TOML Types and Python Types
### 3.3 Use Configuration Files in Your Projects
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