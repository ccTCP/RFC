##What is it?

The idea of the daemon would be to run a background process that will manage connections. Once a modem message gets registered, the daemon will notify the targeted app about the message.

##How it works:

There are several requirements if this is to work properly:

1. A kernel function that notifies specific apps `Kernel.notify(app,...)`

'''lua  
Kernel.notify()  
'''  

```lua
--new(autoenable)
--  (summary): Creates new instance of eventhook
--  (1 parameter): auto-enabling the eventhook after construction
--    Default: true
--  (1 return): eventhook object
local ehook = eventhook.new();
```