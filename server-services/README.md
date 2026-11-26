# Server Services

This module can be used to create an OS service for a given CommandBox Server.  This allows the server to start when your computer boots and be controlled by the operating system's service manager.  Each service will only control a single CommandBox server, but you can create as many as you like. &#x20;

The simplest form of this is to `cd` into the web root for a server and run this command:

```bash
server service create --start
```

This will create a service and start it for you.  Once you've created a service for a given server, use the service to start and stop the server.

On macOS the kind of service depends on the account that creates it:

* **as your normal user** - a per-user LaunchAgent, installed in `~/Library/LaunchAgents` and managed in the `gui/<uid>` launchd domain.  Nothing needs elevation, and the server runs as you.  It only runs while you are logged in.
* **as root** (`sudo box server service create ...`) - a system LaunchDaemon in `/Library/LaunchDaemons`, managed in the `system` domain.  It starts at boot with nobody logged in, and runs as root unless you pass `username` to run it as another account.

On Windows and Linux, creating a service requires an Administrator account or `root`.
