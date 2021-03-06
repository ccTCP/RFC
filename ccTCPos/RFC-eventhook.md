This is free and unencumbered documentation released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or distribute this documentation, either in source code form or as a compiled binary, for any purpose, commercial or non-commercial, and by any means.

In jurisdictions that recognize copyright laws, the author or authors of this documentation dedicate any and all copyright interest in the documentation to the public domain. We make this dedication for the benefit of the public at large and to the detriment of our heirs and successors. We intend this dedication to be an overt act of relinquishment in perpetuity of all present and future rights to this documentation under copyright law.

THE DOCUMENTATION IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE DOCUMENTATION OR THE USE OR OTHER DEALINGS IN THE DOCUMENTATION.

# Eventhook
The Eventhook will inject itself into the computers event stack and allows for listener functions to grab all incoming events.


## Constructor `local obj = eventhook.new(autoEnable)`

### Summary
Creates a new instance of eventhook.

### Parameters
- `autoEnable` Specifies, whether the eventhook will enable itself as part of the construction. Any other value than `false` will be treated as `true`.

### Returns
- `obj` The object itself.

### Usage
```lua
local ehook = eventhook.new();
```

### Additional behaviour
- Will raise error, when environment does not offer os.pullEvent.


## Members
- `listeners` List of listener function.
- `counter` Index counter.
- `ospullEventBackup` Backup, to restore from.


## Functions


### `eventhook.enable(ehook)`

#### Summary
This will enable the eventhook, allowing registered listeners to receive all incoming events.

#### Parameters
- `ehook` The object itself.

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new(false);
ehook:enable();
```

#### Additional behaviour
- Will raise error, when no eventhook is provided.
- Will do nothing, when the eventhook is already enabled.


### `eventhook.disable(ehook)`

#### Summary
This will disable the eventhook, no longer allowing registered Listeners to receive events.

#### Parameters
- `ehook` The object itself.

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new();
ehook:disable();
```

#### Additional behaviour
- Will raise an error, when no eventhook is provided.
- Will do nothing, when the eventhook is already disabled.


### `local index = eventhook.attach(ehook, func)`

#### Summary
This will register a listener function to the eventhook, that it will be calling on, when an event reaches the computer.

#### Parameters
- `ehook` The object itself.
- `func` The listener function that is called on.

#### Returns
- `index` The index position of the listener registered.

#### Usage
```lua
local ehook = eventhook.new();
local function onEvent(...) end
ehook:attach(onEvent);
```

#### Additional behaviour
- Will raise error, when no eventhook is provided.
- Will raise error, when no listener function is provided.


### `eventhook.detach(ehook, index)`

#### Summary
This will remove a listener function from that eventhook.

#### Parameters
- `ehook` The object itself.
- `index` The index position of the listener function to be removed. This will be provided at attachment(see usage below).

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new();
local function onEvent(...) end
local index = ehook:attach(onEvent);
ehook:detach(index);
```

#### Additional behaviour
- Will raise error, when no eventhook is provided.
- Will raise error, when no index is provided.
- Will raise error, when index does not match registered function.

### `local isEnabled = eventhook.isEnabled(ehook)`

#### Summary
To check, whether the eventhook is currently active/enabled.

#### Parameters
- `ehook` The object itself.

#### Returns
- `isEnabled` Boolean, telling whether the eventhook if enabled

#### Usage
```lua
local ehook = eventhook.new();
local isEnabled = ehook:isEnabled(); -- would be true
ehook:disable();
isEnabled = ehook.isEnabled(); -- would be false
```

#### Additional behaviour
- Will raise error, when no eventhook provided.
