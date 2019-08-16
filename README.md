# CommandBox Service Manager

This module adds the ability for CommandBox to help you create and manage services for your CommandBox servers.

![](.gitbook/assets/capture1.PNG)

## Purchasing

This module is a commercial module by Ortus Solutions. You can purchase it here: [https://www.ortussolutions.com/products/commandbox-service-manager](https://www.ortussolutions.com/products/commandbox-service-manager)

{% hint style="info" %}
Once purchased we will add your FORGEBOX user to the Service Manager package as a collaborator so you can install, update and use it.
{% endhint %}

## Installation

Once you have been added as a collaborator, you can install the module like so:

```bash
install commandbox-service-manager@ortus
```

The module will be installed as a global/system CommandBox module.  You can update all your system modules or just the service manager like so:

```bash
# Check and update all system dependencies
update --system
# Update only the service manager
update commandbox-service-manager@ortus --system

# List all system dependencies
list --system
# Check for oudated dependencies
outdated --system
```

## Usage

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

### Supported service configuration

Each operating system may vary on which config items they choose to support.

You can provide configuration to the `server service create` and `server service update` commands as CLI parameters like so:

```bash
server service create exitAction=auto standardOutPath=logs/out.txt
```

Or you can put them in your `server.json` like so:

```bash
server set service.exitAction=auto
server set service.standardOutPath=logs/out.txt
```

Or you can set them as global defaults for all services like so:

```bash
config set server.defaults.service.exitAction=auto
config set server.defaults.service.standardOutPath=logs/out.txt
```

* **serviceName** - The name/ID of the service
* **displayName** - The human readable name of the service
* **description** - The description of the service
* **username** - The username to run as.  On Windows, format of `domain\user` or `machine\login`
* **password** - The password of the user above
* **startType** - one of the strings `auto`, `delayed`, `ondemand`, `disabled`
* **dependOnGroup** - An array of service groups that need started first.  Comma-delimited list when passed the CLI
* **dependOnService** - An array of other services that need started first.  Comma-delimited list when passed the CLI
* **processPriority** - One of the strings `realtime`, `high`, `aboveNormal`, `normal`, `belowNormal`, `idle`
* **CPUAffinity** - The string "all" or CPU IDs, starting from 0 such as "0-2,4" which would use the first, second, third, and 5th CPU core
* **exitAction** - One of the strings `Restart`, `Ignore`, `Exit`
* **restartDelayMS** - Number of milliseconds to delay restart when `exitAction` is `restart`. 
* **restartThrottleMS** - Throttles how quickly to restart if the app runs for only a short time. Set the number of milliseconds for this threshold.
* **standardOutPath** - Path to a file to write the "out" logs. Similar to the `server log` but also includes the raw output of the `server start` command itself.  Useful for debugging failed starts.
* **errorOutPath** - Path to a file to write the "error" logs. Similar to the `server log` but also includes the raw output of the `server start` command itself.  Useful for debugging failed starts.  Can be set to the same path as the "out" log.
* **rotateLog** - true/false to enable log rotation
* **rotateLogOnline** - true/false to enable log rotation while service is running as opposed to only during a restart.
* **rotateLogSeconds** - Number of seconds between log rotations.
* **rotateLogKB** - Number of Kilobytes of log file size before rotating. When using online rotation, time is ignored and only file size taken into account

Note, the `standardOutPath` and `errorOutPath` can be absolute or relative. When relative, the following logic is used to expand the paths.

* Paths provided from the CLI are relative to the current working directory of the command
* Paths provided in `server.json` are relative to the location of the `server.json` file.
* Paths provided in `server.defaults.service` config defaults are relative to the web root of the server.

### Supported OS's

* Windows 
* Linux - Under Development
* Mac - Coming Soon.

### Bullet Train

If you are using the CommandBox Bullet Train module, the Service Manager will contribute its own bullet train car that shows you the stats of the default server for a given directory.

```bash
install commandbox-bullet-train
```

You can turn this additional car on or off by setting the following config setting in the bullet train module:

```bash
config set modules.commandbox-bullet-train.serverServiceEnable=false
```

You can customize the background color as well like so:

```bash
config set modules.commandbox-bullet-train.serverServiceBG=grey
```

Remember, the status text in the car can be green, red, yellow, or orange, so choose a color that doesn't render the text unreadable.

You can change the order the car appears in the promp using the name `serverService` like so:

```bash
config set modules.commandbox-bullet-train.carOrder=boxVersion,package,serverService,status,execTime
```

