# Usage

Here is an overview of the new commands this module adds into CommandBox for you.

```bash
task service create
task service remove
task service update
task service start
task service stop
task service restart
task service status
```

Each of the `task service XXX` commands above accept the `taskFile` parameter that points to the Task Runner. &#x20;

``

If you provide no params, the default is `task.cfc`.  If you want to create a service for a task of a different name or in a different folder, you will need to provide this parameter.

#### `server service create`

Create a new service. To customize the service, pass params, set values in your `task.cfc` in a struct located in `this.service`. &#x20;

{% hint style="warning" %}
Note: you must be using an **Administrator** user (Windows) or **root** (\*nix) to create services. You can start box as such, but keep in mind on \*nix, this changes your runtime user, and thus your CommandBox home.
{% endhint %}

#### `server service remove`

Remove an existing service. Does not affect the `task.cfc` itself. Use `--force` to also stop the service if necessary.

#### `server service update`

Update an existing service. To customize the service, pass params, or set them in the `task.cfc` in a `this.service` struct at the top of the CFC.  Use `--force` to also stop the service if necessary. (Service will be restarted if it was originally running)

#### `server service start`

Start a service. Once you start a task via the service, you should also stop and start it via the service as well.

#### `server service stop`

Stop a service. Note, killing the task process directly instead of `server service stop` may cause the service to start again by itself if the `exitAction` is set to `restart`.

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

What happens when you run a Windows service as the "Local System" account (the default) or a Linux service as `root` (required to bind to ports below 1024) is the CommandBox home directory changes to match the new user that the process runs as. &#x20;

```bash
C:/Windows/System32/config/systemprofile/.CommandBox/
/root/.CommandBox/
```

This is unexpected and often times catches people off guard.  This "second" installation of CommandBox will not have your modules installed, neither will it have any default config settings as all of this data is stored on a per-user basis. &#x20;

This can be made to work, but is undesirable since it prevents you from running `task run` inside CommandBox as yourself and getting the same results.  The easy fix is to lock all users into using the same CommandBox home dir.  To do this, choose a folder that has read/write permissions to all users who need to use CommandBox.  Then create a `commandbox.properties` file in the same directory as your `box` or `box.exe` binary.  Add a line defining a property called `commandbox_home` that points to the shared home dir.  Remember to either use forward slashes or escape all backslashes.

```bash
commandbox_home=E:\\CommandBox
or
commandbox_home=E:/CommandBox
or
commandbox_home=/opt/box/.CommandBox
```

This setting will take affect on your next run of `box` and a new, empty home will be created there.  if you wish, you can transfer all your settings, by stopping CommandBox and all servers, manually copying over the current `.CommandBox` folder to the new location first.  CommandBox will pick up the folder and use it if it's already there and everything inside is portable.
