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

Create a new service. To customize the service, pass params, set values in your `server.json` or set global config defaults. Use `--start` to also start the service after creating it.

{% hint style="warning" %}
Note: you must be using an **Administrator** user \(Windows\) or **root** \(\*nix\) to create services. You can start box as such, but keep in mind on \*nix, this changes your runtime user, and thus your CommandBox home.
{% endhint %}

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

## CommandBox Home

CommandBox installs system modules and saves settings and servers into a `.CommandBox` folder inside the home directory of the current user running the `box` process.  For instance, a `brad` user on Windows and \*nix might have their CommandBox home in these locations:

```bash
C:/Users/brad/.Commandbox/
/home/brad/.CommandBox/
```

What happens when you run a Windows service as the "Local System" account \(the default\) or a Linux service as `root` \(required to bind to ports below 1024\) is the CommandBox home directory changes to match the new user that the process runs as.  

```bash
C:/Windows/System32/config/systemprofile/.CommandBox/
/root/.CommandBox/
```

This is unexpected and often times catches people off guard.  This "second" installation of CommandBox will not have your modules like [CFConfig](https://www.forgebox.io/view/commandbox-cfconfig) or [HostUpdater](https://www.forgebox.io/view/commandbox-hostupdater) installed, neither will it have any default config settings or servers present as all of this data is stored on a per-user basis.  

This can be made to work, but is undesirable since it prevents you from running `server start` inside CommandBox as yourself and getting the same results.  The easy fix is to lock all users into using the same CommandBox home dir.  To do this, choose a folder that has read/write permissions to all users who need to use CommandBox.  Then create a `commandbox.properties` file in the same directory as your `box` or `box.exe` binary.  Add a line defining a property called `commandbox_home` that points to the shared home dir.  Remember to either use forward slashes or escape all backslashes.

```bash
commandbox_home=E:\\CommandBox
or
commandbox_home=E:/CommandBox
or
commandbox_home=/opt/box/.CommandBox
```

This setting will take affect on your next run of `box` and a new, empty home will be created there.  if you wish, you can transfer all your settings, by stopping CommandBox and all servers, manually copying over the current `.CommandBox` folder to the new location first.  CommandBox will pick up the folder and use it if it's already there and everything inside is portable.

