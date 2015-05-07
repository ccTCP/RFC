##What is it?

The idea of the daemon would be to run a background process that will manage connections. Once a modem message gets registered, the daemon will notify the targeted app about the message.

##How it works:

There are several requirements if this is to work properly:

1. A kernel function that notifies specific apps `Kernel.notify(app,...)`
2. Driver support

When a `modem_message` event gets caught, the kernel will check whether there is a special driver to handle modem messages. If there is the event will be sent to the driver. However this same event will also be sent to the other coroutines, since some may be using the modem API.