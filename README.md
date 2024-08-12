# Lua Parser README

## Overview

This Lua parser is designed to help you analyze Lua code, tokenize it, and generate an Abstract Syntax Tree (AST). Whether you want to extract identifiers, analyze the structure of Lua code, or perform custom operations on the parsed AST, this parser has you covered.

### Features:
- **Tokenization**: Breaks down Lua code into tokens.
- **Parsing**: Converts tokens into an AST for easy traversal and analysis.
- **Identifier Extraction**: Retrieves all identifiers used in the code.
- **Error Handling**: Provides detailed error messages during parsing.

## Installation

1. Clone or download the repository containing this parser.
2. Make sure you have a compatible Lua environment installed.

## Usage

### 1. Getting Started
To use the parser, you first need to require the parser and tokenizer modules.

```lua
local Parser = require("path.to.parser")
local Tokenizer = require("path.to.tokenizer")
```

### 2. Parsing Lua Code
You can parse Lua code by loading it from a file or directly as a string. The `parse` method will give you an AST.

```lua
local code = [[
    local x = 10
    print(x)
]]

local tokens = Tokenizer.tokenize(code)
local parser = Parser:new(tokens)
local ast = parser:parse()
```

### 3. Loading from a File
If you want to parse Lua code from a file, the parser has a handy method for that.

```lua
local ast = parser:loadFile("path/to/your/file.lua")
```

### 4. Extracting Identifiers
To grab all the identifiers from a Lua file, use the `getIdentifiersAsList` method.

```lua
local identifiers = parser:getIdentifiersAsList("path/to/your/file.lua")
for _, id in ipairs(identifiers) do
    print(id)
end
```

### 5. Custom Parsing
Feel free to extend the parser with your custom methods to handle additional Lua constructs or modify the AST to suit your needs.

```lua
function Parser:parse_custom_structure()
    -- Your custom parsing logic here
end
```

## How It Works

### 1. Tokenization
The `Tokenizer` module breaks Lua code into tokens. Each token represents an element in the code, like keywords, identifiers, operators, and so on.

### 2. Parsing Logic
The parser processes these tokens sequentially to build an AST, a tree-like structure where each node represents a part of the Lua code.

### 3. Error Handling
The parser includes error handling that catches unexpected tokens or syntax issues, providing detailed error messages that pinpoint the problem's location.

## Precedence Table

The parser respects Lua's operator precedence using a predefined table, ensuring expressions are parsed correctly.

```lua
local PRECEDENCE = {
    ["or"] = 1,
    ["and"] = 2,
    ["=="] = 3,
    -- and so on...
}
```

## Customization

You can tweak the parser by modifying methods in the `Parser` table. If you need to add support for new Lua constructs or change how certain expressions are parsed, you can extend or alter the existing methods.

## Example Use Cases

1. **Static Code Analysis**: Analyze Lua code for potential errors or style issues.
2. **Code Transformation**: Modify or generate Lua code by traversing and transforming the AST.
3. **Custom Scripting**: Use the parser in a larger system to support custom scripting languages based on Lua.
