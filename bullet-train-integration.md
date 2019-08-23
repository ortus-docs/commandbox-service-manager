# Bullet Train Integration

If you are using the [CommandBox Bullet Train](https://www.forgebox.io/view/commandbox-bullet-train) module, the Service Manager will contribute its own bullet train car that shows you the stats of the default server for a given directory.

{% embed url="https://www.forgebox.io/view/commandbox-bullet-train" %}

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

You can change the order the car appears in the prompt using the name `serverService` like so:

```bash
config set modules.commandbox-bullet-train.carOrder=boxVersion,package,serverService,status,execTime
```

