# Server Services

This module can be used to create an OS service for a given CommandBox Server.  This allows the server to start when your computer boots and be controlled by the operating system's service manager.  Each service will only control a single CommandBox server, but you can create as many as you like. &#x20;

The simplest form of this is to `cd` into the web root for a server and run this command:

```bash
server service create --start
```

This will create a service and start it for you.  Once you've created a service for a given server, use the service to start and stop the server.
