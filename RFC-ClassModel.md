### Thoughts:

First of all, I've read myself into PPP and some other things we may shouldn't forget about, so to sum up:
The OSI layers do not contain detailed enough layers. So the file naming "Layer3.lua" and similar aren't too fitting, since the layer does not meet the protocol number.
Layer2 in OSI can actually contain multiple(I can think of 3) protocols: PPP, which depends on PPPoE, which depends on Ethernet. So my first suggestion is to name the files after their protocol:

### Protocols corresponding to OSI layers:

1. Layer
  1. Interface (no idea on how to call it since it's not actually a protocol)
2. Layer
  1. Ethernet
  2. PPPoE (which is optional)
  3. PPP (which also is optional)
3. Layer
  1. IPv4
4. Layer
  1. TCP
  2. UDP

### Approach

So I thought, we would approach this in a more OOP manner, so each interface and each protocol "node" will become an object-like thingy

### Detailed specifications of how to access the objects



#### Eventhook
The Eventhook will inject itself into the computers event stack and allows for listener functions to grab all incoming events

##### Constructor
```lua
--new(autoenable)
--  (summary): Creates new instance of eventhook
--  (1 parameter): auto-enabling the eventhook after construction
--    Default: true
--  (1 return): eventhook object
local ehook = eventhook.new();
```

##### Functions

###### eventhook.enable
```lua
--enable(ehook)
--  (Summary): Enables the eventhook to inject event stack
--  (1 parameter): eventhook instance(object)
eventhook.enable(ehook);
--or
ehook:enable();
```

###### eventhook.disable
```lua
--disable(ehook)
--  (Summary): Disinjects the eventhook disabling it to grab further events
--  (1 parameter): eventhook instance(object)
eventhook.disable(ehook);
--or
ehook:disable();
```

###### eventhook.attach
```lua
--attach(ehook, func)
--  (Summary): Attaches a listener to that eventhook
--  (1 parameter): eventhook instance(object)
--  (2 parameter): listener function, that the eventhook will call, when modem_messages arrive
--  (1 return): index position of that listener
local listenerindex = eventhook.attach(ehook, func);
--or
local listenerindex = ehook:attach(func);
```

###### eventhook.detach
```lua
--detach(ehook, index)
--  (Summary): Detaches a listener from that eventhook.
--  (1 parameter): eventhook instance(object)
--  (2 parameter): index position of listener function
eventhook.detach(ehook, listenerindex);
--or
ehook:detach(listenerindex);
```

##### Usage
```lua
local ehook = eventhook.new(); -- create instance of eventhook
local function onEvent(...) -- define listener function
    -- in ... you get all arguments of all events, that the computer is receiving
    if({...}[1] == "modem_message") then
        -- do stuff with the other args(up to you ;) )
    end
end
local i = ehook:attach(onEvent); -- your listener function will now be called everytime an event is pulled from the stack
-- if you no longer wish to receive events, you can detach from the hook, or disable it
ehook:detach(i); -- this will allow other listeners to continue receiving events
ehook:disable(); -- this will disable event gathering for the whole evenhook, allowing no registered listener to receive events. (this will keep the listeners registered though, for later re-enabling)
```

#### Interface
The interface is bound to a side, will inject itself into the computers event stack(via eventhook above) and is able to hold listener functions to call, when modem_messages arrive.
##### Constructor
```lua
--new(side, hook, auto)
--  (summary): Creates new instance of interface.
--  (1 parameter): Side of the interface
--  (2 parameter): Instance of eventHook for it to hook onto
--  (3 parameter): Auto-enable
--    Default: true
--  (1 return): interface object
local iface = interface.new("left", hookObj, false);
```
##### Functions
###### interface.enable
```lua
--enable(iface)
--  (Summary): Enables the interface to listen for modem_messages
--  (1 parameter): interface instance(object)
interface.enable(iface);
--or
iface:enable();
```
###### interface.disable
```lua
--disable(iface)
--  (Summary): Disables the interface from listening to modem_messages
--  (1 parameter): interface instance(object)
interface.disable(iface);
--or
iface:disable();
```
###### interface.attach
```lua
--attach(iface, func)
--  (Summary): Attaches a listener to that interface
--  (1 parameter): interface instance(object)
--  (2 parameter): listener function, that the interface will call, when modem_messages arrive
--  (1 return): index position of that listener
local listenerindex = interface.attach(iface, func);
--or
local listenerindex = iface:attach(func);
```
###### interface.detach
```lua
--detach(iface, index)
--  (Summary): Detaches a listener from that interface.
--  (1 parameter): interface instance(object)
--  (2 parameter): index position of listener function
interface.detach(iface, listenerindex);
--or
iface:detach(listenerindex);
```
###### interface.send
```lua
--send(iface, message)
--  (Summary): Sends a message from that interface
--  (1 parameter): interface instance(object)
--  (2 parameter): message to be send(should be string)
interface.send(iface, message);
--or
iface:send(message);
```
##### Usage
```lua
local ehook = eventhook.new(); -- create your instance of eventhook
local iface = interface.new("left", ehook) -- create your instance of interface
local function onMessage(message) -- define your listener function
    -- here I get all messages received by interface
    print("Message received: ",message); -- would print out all received messages of the interface it's registered at
end
iface:attach(onMessage); -- register your listener function. You will now get all messages of that interface
iface.send("Hello, my name is Karsten"); -- this will send the message from that interface
```

#### Ethernet
##### Constructor
###### ethernet.new
##### Functions
###### ethernet.enable
###### ethernet.disable
###### ethernet.attach
###### ethernet.detach
###### ethernet.send
##### Usage
```lua
local iface = interface.new(...); -- see above on how to create your interface
local ether = ethernet.new(iface); -- create instance of ethernet protocol node(auto enabled)
local function onFrame(frame) -- define your listener function
    -- here you can handle all frames coming to this ether node(basically to that interface)
end
local index = ether:attach(onFrame); -- this will attach your listener function to that ethernet node
ether:detach(index); -- detaches your listener, without closing the node
ether:disable(); -- disables the node completely, remembering all listeners for later re-enable
```
#### PPPoE
##### Constructor
###### pppoe.new
##### Functions
#### PPP
#### IPv4
#### TCP
#### UDP