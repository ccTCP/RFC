This is free and unencumbered documentation released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this documentation, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

In jurisdictions that recognize copyright laws, the author or authors
of this documentation dedicate any and all copyright interest in the
documentation to the public domain. We make this dedication for the benefit
of the public at large and to the detriment of our heirs and
successors. We intend this dedication to be an overt act of
relinquishment in perpetuity of all present and future rights to this
documentation under copyright law.

THE DOCUMENTATION IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS BE LIABLE FOR ANY CLAIM, DAMAGES OR
OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE,
ARISING FROM, OUT OF OR IN CONNECTION WITH THE DOCUMENTATION OR THE USE OR
OTHER DEALINGS IN THE DOCUMENTATION.

# Interface


## Constructor `local obj = interface.new(side, ehook, autoEnable)`

### Summary
Will create a new instance of interface

### Parameters
- `side` The side of the modem, that this object is allocated to.
- `ehook` An instance of the eventhook class for the interface to inject to.
- `autoEnable` Specifies, wether the interface should be enabled within process of construction. Anything other than `false` will be treated as `true`.

### Returns
- `obj` The object itself

### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
```

### Additional behaviour
- Will raise error, when side is not a valid side
- Will raise error, when no eventhook is provided


## Members
- `side` The side it's allocated to.
- `ehook` A reference to the ehook it's injecting on.
- `ehookIndex` The index of it's own listener within `ehook`.
- `autoDisabled` Whether it should auto-enable after reattachment.
- `modemWrap` The peripheral handle of own modem.
- `listeners` Attached listener functions to call onto.


## Functions


### `interface.enable(iface)`

#### Summary
This will enable your interface, wrapping the modem allocated to.

#### Parameters
- `iface` The object itself

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook, false);
iface:enable();
```

#### Additional behaviour
- Will raise error, when no interface provided.
- Will raise error, when no modem is wrappable at side allocated to.
- Will do nothing, when interface provided is already enabled.


### `interface.disable(iface)`

#### Summary
This will disable the interface, unwrapping the modem allocated to.

#### Parameters
- `iface` The object itself.

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
iface:disable();
```

#### Additional behaviour
- Will raise error, when no interface is provided.
- Will do nothing, when interface provided is already disabled.


### `local index = interface.attach(iface, func)`

#### Summary
This will register a listener function for that interface to call onto, when a modem_message arrives at that interface.

#### Parameters
- `iface` The object itself.
- `func` The listener function to call onto.

#### Returns
- `index` The position of the listener function within that interface(used to detach it below).

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
local function onMessage(...) end
iface:attach(onMessage);
```

#### Additional behaviour
- Will raise error, when no interface provided.
- Will raise error, when no listener function provided.


### `interface.detach(iface, index)`

#### Summary
This will remove a listener function at specified index from interface.

#### Parameters
- `iface` The object itself.
- `index` The position in the listeners list of interface.

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
local function onMessage(...) end
local index = iface:attach(onMessage);
iface:detach(index);
```

#### Additional behaviour
- Will raise error, when no interface provided.
- Will raise error, when no index provided.
- Will do nothing, when no listener is registered at given index.


### `interface.send(iface, message)`

#### Summary
This will send the message from the modem specified at construction.

#### Parameters
- `iface` The object itself. Must be enabled to be valid!
- `message` The message to be sent. Must be string to be valid.

#### Returns
- nothing

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
iface:send("I like networking... and trains");
```

#### Additional behaviour
- Will raise error, when no valid interface provided.
- Will raise error, when no valid message is provided.


### `local side = interface.getSide(iface)`

#### Summary
Used to retrieve the side specified at construction.

#### Parameters
- `iface` The object itself.

#### Returns
- `side` The side specified at construction.

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
local side = iface:getSide() -- will be "left"
```

#### Additional behaviour
- Will raise error, when no interface provided.


### `local ehook = interface.getEventhook(iface)`

#### Summary
Used to retrieve the eventhook specified at construction.

#### Parameters
- `iface` The object itself.

#### Returns
- `ehook` The eventhook specified at construction.

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
local ehook2 = iface:getEventhook() -- will be "ehook"
```

#### Additional behaviour
- Will raise error, when no interface provided.


### `local isEnabled = interface.isEnabled(iface)`

#### Summary
Used to check, whether the interface is enabled

#### Parameters
- `iface` The object itself.

#### Returns
- `isEnabled` A bool, telling the status of the interface.

#### Usage
```lua
local ehook = eventhook.new();
local iface = interface.new("left", ehook);
local isEnabled = iface:isEnabled() -- will be true
```

#### Additional behaviour
- Will raise error, when no interface provided.



## Additional behaviour
- The interface will auto-disable, when the peripheral is removed.
- If a modem is re-attached at registered location after auto-disable, it will auto-enable again.
