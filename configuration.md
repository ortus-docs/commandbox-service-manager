# Configuration



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
* **password** - The password of the user above _\(Windows only\)_
* **startType** - one of the strings `auto`, `delayed`, `ondemand`, `disabled`
* **dependOnGroup** - An array of service groups that need started first.  Comma-delimited list when passed the CLI _\(Windows only\)_
* **dependOnService** - An array of other services that need started first.  Comma-delimited list when passed the CLI
* **processPriority** - One of the strings `realtime`, `high`, `aboveNormal`, `normal`, `belowNormal`, `idle` _\(Windows only\)_
* **CPUAffinity** - The string "all" or CPU IDs, starting from 0 such as "0-2,4" which would use the first, second, third, and 5th CPU core. _\(Windows only\)_
* **exitAction** - One of the strings `Restart`, `Ignore`, `Exit`
* **restartDelayMS** - Number of milliseconds to delay restart when `exitAction` is `restart`. 
* **restartThrottleMS** - Throttles how quickly to restart if the app runs for only a short time. Set the number of milliseconds for this threshold. _\(Windows only\)_
* **standardOutPath** - Path to a file to write the "out" logs. Similar to the `server log` but also includes the raw output of the `server start` command itself.  Useful for debugging failed starts.  _\(Windows only\)_
* **errorOutPath** - Path to a file to write the "error" logs. Similar to the `server log` but also includes the raw output of the `server start` command itself.  Useful for debugging failed starts.  Can be set to the same path as the "out" log. _\(Windows only\)_
* **rotateLog** - true/false to enable log rotation _\(Windows only\)_
* **rotateLogOnline** - true/false to enable log rotation while service is running as opposed to only during a restart. _\(Windows only\)_
* **rotateLogSeconds** - Number of seconds between log rotations. _\(Windows only\)_
* **rotateLogKB** - Number of Kilobytes of log file size before rotating. When using online rotation, time is ignored and only file size taken into account. _\(Windows only\)_

Note, the `standardOutPath` and `errorOutPath` can be absolute or relative. When relative, the following logic is used to expand the paths.

* Paths provided from the CLI are relative to the current working directory of the command
* Paths provided in `server.json` are relative to the location of the `server.json` file.
* Paths provided in `server.defaults.service` config defaults are relative to the web root of the server.

On Linux, the systemd journal will be used for the server out.  Any issues with startup can be viewed like so:

```bash
journalctl -u nameOfService
```





