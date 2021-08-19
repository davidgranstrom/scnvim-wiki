# Execute SuperCollider code from lua code in NeoVim config 

SCNvim exposes some really handy functions that allows you to execute SuperCollider code from keymappings or your settings to create your own hacks. 

## scnvim.send
`send` is for sending SuperCollider code from Nvim to sclang without getting any feedback into Nvim again. This version posts things to the post window.

```lua
-- Play a sine wave
local code = "play{SinOsc.ar(110)}"
require'scnvim'.send(expr)
```

`send_silent` is a function equivalent to the above but it does not post to the post window when called.

## scnvim.eval

`eval` allows the user to evaluate SuperCollider code and get the return value inside of lua and use it for something useful.

An example that asks the server how many output channels it's got and prints it in Nvim:

```lua
-- Code to be evaluated
local supercollider_code = "s.options.numOutputBusChannels"

-- This function will be called with the return value of the supercollider code above
local callback = function (returnVal) print("SuperCollider server has " .. returnVal .. " channels") end

require'scnvim'.eval(supercollider_code, callback)
```
## Using the functions in a keymap

```lua
-- SuperCollider code. Note: double quotes need to be escaped like below
local sc_code = "\"play{SinOsc.ar(110, mul: 0.25}\""

-- Normal mode mapping
local opts = { nowait = true, noremap = true, silent = false }
local lhs = "<F11>" -- The key to be mapped
local rhs = "<cmd> lua require'scnvim'.send(" .. sc_code .. ")" -- The thing that will be executed by said key
vim.api.nvim_buf_set_keymap(0, "n", lhs, rhs, opts)
```
