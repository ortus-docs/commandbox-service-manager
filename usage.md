# Usage

Here is an overview of the new commands this module adds into CommandBox for you.

```bash
server service create
server service remove
server service update
server service start
server service stop
server service restart
server service status
```

Each of the `server service XXX` commands above accept the same three parameters that every other server command accepts.

* `name` - The name of an existing server
* `directory` - The web root of an existing server
* `serverConfigFile` - The path to a `server.json` file. \(name can actually be anything\)

If you provide no params, by default, the commands will find the server in that directory. This is suitable for working with a single server in the current working directory. If you want to manage a service for another directory or you have more than one server defined, you can use the params above to be more specific.

#### `server service create`

Create a new service. To customize the service, pass params, set values in your `server.json` or set global config defaults. Use `--start` to also start the serviec after creating it.

#### `server service remove`

Remove an existing service. Does not affect the CommandBox server itself. Use `--force` to also stop the service if necessary.

#### `server service update`

Update an existing service. To customize the service, pass params, set values in your `server.json` or set global config defaults. Use `--force` to also stop the service if necessary. \(Service will be restarted if it was originally running\)

#### `server service start`

Start a service. Once you start a server via the service, you should also stop and start it via the service as well.

#### `server service stop`

Stop a service. Note, stopping a server directly with `server stop` instead of `server service stop` may cause the service to start again by itself if the `exitAction` is set to `restart`.

#### `server service restart`

Restart a service

#### `server service status`

Get status information for a service. Use `--verbose` to get additional information.

