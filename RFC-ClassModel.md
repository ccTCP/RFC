### Thoughts:

First of all, I've read myself into PPP and some other things we may shouldn't forget about, so to sum up:
The OSI layers do not contain detailed enough layers. So the file naming "Layer3.lua" and similar aren't too fitting, since the layer does not meet the protocol number.
Layer2 in OSI can actually contain multiple(I can think of 3) protocols: PPP, which depends on PPPoE, which depends on Ethernet. So my first suggestion is to name the files after their protocol:

### Protocols corresponding to OSI layers:

1. Layer
  1. Ethernet
2. Layer
  1. Ethernet
3. Layer
  1. TCP/IPv4
4. Layer
  1. TCP/IPv4
  2. UDP

### Approach

So I thought, we would approach this in a more OOP manner, so each interface and each protocol "node" will become an object-like thingy

### Detailed specifications of how to access the objects
#### Eventhook
#### Ethernet @ L1 (depends on Eventhook for event oriented implementation)
#### Ethernet @ L2 (depends on Ethernet @ L1)
#### TCP/IP(depends on Ethernet @ L2)
#### UDP(depends on Ethernet @ L2)

I would like to expand on the subject a little bit:

Class initialization:
`local Instance = ccTCPf.initialize()`

Connection starting:
```lua
local httpconnection = Instance.http.new(address,otherargs)`
local ethernetconection = Instance.ethernet.new(args)
```
