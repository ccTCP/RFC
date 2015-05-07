##What is it?

The idea of the daemon would be to run a background process that will manage connections. Once a modem message gets registered, the daemon will notify the targeted app about the message.

##How it works:

There are several requirements if this is to work properly:

1. A kernel function that notifies specific apps `Kernel.notify(app,...)`
2. Driver support

When a `modem_message` event gets caught, the kernel will check whether there is a special driver to handle modem messages. If there is the event will be sent to the driver. However this same event will also be sent to the other coroutines, since some may be using the modem API. The driver will the queue an ccTCP event with the related data.

The role of the driver is to collect the single frames/packets coming from the network and form a (internet packets are divided into smaller units(packets), insert the name of the bigger entity here). In order to use the service, the app should start a new ccTCP instance like this: (should it connect on a per app basis or on a connection basis?)

```lua
local connection = ccTCP.new(protocol)
```

The instance will then be used in this manner:

1. Sending:

```lua
connection.send(receiver,message)
```

2. Receiving:

```lua
connection.receive([timeout?], otherDataWeHaveToSpecify)
```

Be sure to comment
