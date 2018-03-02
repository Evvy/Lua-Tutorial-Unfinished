# Lua Tutorial
Table of contents
=================

   * [Scopes](#scopes)
      * [Local Scope](#local-scope)
      * [Global Scope](#global-scope)
    * [Data Types](#data-types)
      * [Strings](#strings)
      * [Booleans](#booleans)
      * [Numbers](#numbers)
      * [Nil](#nil)
      * [Functions](#functions)
      * [Tables](#tables)
      * [Userdata and Threads](#userdata-and-threads)
   * [Scopes](#scopes)
      * [Local Scope](#local-scope)
      * [Global Scope](#global-scope)
      
The lua interpreter is case sensitive. This means that identifier names containing lowercase letters will be treated as being different and separate from those containing uppercase letters.
However, lua is not as syntax sensitive as many other languages. You can for instance include or exclude parentheses, commas and semicolons as you may find it practical or pleasing.

In most languages it is common to use semicolons to end of a statement, whether it's a variable or a function.

Example in Javascript:
```javascript
function greetUser() {
  alert("Hello there!");
}
greetUser();
```
Example in PHP:
```php
<?php
function greetUser() {
    echo "Hello there!";
}
greetUser();
?>
```
In Lua, semicolons can be included in the code, but is **not** required.
Semicolons are generally used for multi-line statements, such as:
```lua
a = 4; b = 3; c = a * b
```

# Scopes:
More on scopes, coming soon!

## Local Scope:
```lua
local x = 5
```
## Global Scope
```lua
global y = true
```
Global scopes can also be written as ```y = true```, as this is the default syntax.

# Data Types:
More on data types, coming soon!

The type function gives the type name of a given value:
```lua
print(type("Hello world"))  -- Returns string
print(type(10.4*3))         -- Returns number
print(type(print))          -- Returns function
print(type(type))           -- Returns function
print(type(true))           -- Returns boolean
print(type(nil))            -- Returns nil (Same as null)
print(type(type(X)))        -- Returns string
```

Creating functions (Two ways):
First way: 
```lua
local tellName = function() end
```
```end``` defines the end of a block
To invoking the function, simply do: 
```lua
tellName();
```
To call a variable inside the function block, use the keyword return
2nd way: local function tellName() end
Example of a function with stored value in a variable:
```lua
local function simpleMath(a, b, c, d)
  local answer = (a * b) + (c / d)
  return answer
end
local tellAnswer = simpleMath(2, 6, 6, 2)
print(tellAnswer)
```

# IF statements
Example:
```lua
if (not b) then b = 3 end
Alternative:
```lua
b = b or 3
```
In the example above parentheses are used to define a condition
However, this is not required in lua, and can therefor be excluded if desired


# Variable argument list
Example:
```lua
local function simpleMath(a, b, c, d, ...)
  local a, b, c, d = ...
  local answer = (a * b) + (c / d)
  return answer
end
print(simpleMath(2, 6, 6, 2, 3))
```
In the example above, the first 4 values will be designated to their matching arguments
However the 5th argument will be stored in the argument list for later use
If you wanted to only use the variable c for instance, you could convert
the other variables into so-called dummy variables by using the underscore
```Example: ```lualocal _, _, c, _ = ...``````
-- Using the select function:
-- local f, g, h, i = select(7, ...)
-- This would get the 7th element of an argument list and store it into the variable f
-- The following elements would be stored into g, h and i
-- The 11th element and onward would not be stored in any variable and therefor return a nil


-- Arrays/Tables (Table = Array + Hash Table)
-- Array = Index and value pairs
-- Hash Table = Key and value pairs
-- Example: local choices = {9, 3, 5, 2}
-- Lua, unlike some other programming languages uses indexing starting from 0 and onwards.
-- Javascript uses 0 as a starting point for instance
-- To access let's say the number 5 in this table, we'll be using the following code:
-- choices[3]. This can also be assigned to a variable such as: local a = choices[3]
-- Index outside of the visible array, returns a value of nil
-- You can however give a specific index a value, such as options[10] = 3
-- This will not affect index 5-9 as they will still remain with the value of nil
-- Example of a hash table:
-- local choices = {
--  ['size'] = 10,
--  ['xOffset'] = 10,
--  ['yOffset'] = 10,
--  ['color'] = {r = 0.5, g = 0.2, b = 0.6, a = 1},
--  class = "Priest",
-- }
-- To access the size index simply do: options['size']
-- To access the class of warrior do: choices.class


-- Pop/Push and Stacks
-- Stacks are abstract datatypes that contains indexes like a stack of books.
-- Pop removes the top data block from the stack.
-- Push puts a new data block on top of the stack.
-- Example:
-- local choices = {
--   push = function(self, arg)
--     local n = #self
--     self[n + 1] = arg
--   end,
--
--   pop = function(self)
--     local n = #self
--     if (n > 0) then
--       local rtn = self[n]
--       self[n] = nil
--       return rtn
--     end
--   end
-- }

-- Colons after a table variables tells lua that the right-hand side of the variable
-- contains a function call. Colons should therefor only be used in this context
-- This will automatically generate a self-referecial variable to go inside the parameter
Example: ```lua print(choices:pop())```
This is a replacement for: ```lua print(choices.pop(choices))```

# Loops (for loop (2 types))
For loop example:
```lua
for startValue, endValue, stepValue do
  -- do something
end
```
In this case startValue, endValue, stepValue can be viewed as arguments/parameters
The code to execute will be placed between the do and end (start and stop points of the block)
Numeric for loop: the startValue, endValue and stepValue have to be connected to a variable
```lua
for i = i, 10, i do
  -- do something
end
```
The ```i``` in this case does not have to be made local as it is already local to the for loop.
If you choose to exclude the stepValue, it will be set to 1 as default.
Generic for loop:

