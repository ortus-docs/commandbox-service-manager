# Installation

Once you have been granted access to the package on ForgeBox, you can install the module like so:

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

## 

