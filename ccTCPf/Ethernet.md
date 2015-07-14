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

#Ethernet (node)

## Constructor `local obj = ethernet.new(iface, autoEnable)`

### Summary
Will create a brand new instance of an ethernet node.

### Parameters
- `iface` Instance of underlying interface, the node will append on.
- `autoEnable` Specifies, whether die ethernet node should be enabled within the process of construction. Anything other than `false` will be treated as `true´.

### Returns
- `obj` The object itself.

### Usage
```lua
local iface = interface.new(...); -- see the documentation of interface
local ether = ethernet.new(iface);
```

### Additional behaviour
- Will raise error, when no interface is provided.


## Members
- `iface` The interface, the ethernet node is allocated to/injected in.
- `ifaceIndex` The index of it's own listener within `iface`.
- `address` The address on which to listen on.
- `triggerAll` Boolean, specifying wether frames with wrong destination are still elevated to listeners.
- `listeners` Attached listener functions to call onto.

## Functions


### `ethernet.enable(ether)`

#### Summary
This will enable the ethernet node.

#### Parameters
- `ether` The object itself.

#### Returns
- nothing

#### Usage
```lua
local iface = ...
local ether = ethernet.new(iface, false); -- will keep it disabled after construction
ether:enable(); -- Will enable it afterwards
```

#### Additional behaviour
- Will raise error, when no ethernet ndoe is provided.
- Will do nothing, when node was already enabled.


### `ethernet.disable(ether)`

#### Summary
This will disable the ethernet node.

#### Parameters
- `ether` The object itself.

#### Returns
- nothing

#### Usage
```lua
local iface = ...
local ether = ethernet.new(iface); -- will auto-enable it
ether:disable(); -- Will disable it afterwards
```

#### Additional behaviour
- Will raise error, when no ethernet ndoe is provided.
- Will do nothing, when node was already disabled.
