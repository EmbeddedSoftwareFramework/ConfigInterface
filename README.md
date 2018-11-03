# Config Publisher
## Objective
An application sends config publisher message requesting latest config when starting. Config publisher creates the config if non-existent and publishes it in a shared memory which the application needs to subscribe to. Therefore the application can get callback when the shared memory is created and/or changed.

## Priorities
An instance of config publisher needs to be running if other applications depend on it, therefore config publisher should have high priority when starting target/host.

## Data structure in files
Recipe files should be constructed with valid JSON syntax. Each "config variable" needs to provide the following values: value, description. An example below for recipe applicationName.json:
```json
{
    "configVariableName": {
        "value": "this can be of any type, bool/int/double/string, not objects",
        "description": "Configured instance name or some"
    },
    "object": {
        "subDataName": {
            "value": "meter",
            "description": "Voltage/ampere meter"
        },
        "subIntName": {
            "value": 42,
            "description": "Max meter value, if above an alarm is raised"
        },
        "subDoubleName": {
            "value": 4.2,
            "description": "Meter gain"
        }
    }
}
```

Created config file named applicationInstance.json is in the following format:
```json
{
    "configVariableName": {
        "value": "this can be of any type, bool/int/double/string, not objects",
        "description": "Configured instance name or some"
    },
    "object": {
        "key1": {
            "subDataName": {
                "value": "Voltage meter",
                "description": "Voltage/ampere meter"
            },
            "subIntName": {
                "value": 24,
                "description": "Max meter value, if above an alarm is raised"
            },
            "subDoubleName": {
                "value": 2.4,
                "description": "Meter gain"
            }
        },
        "key2": {
            "subDataName": {
                "value": "Ampere meter",
                "description": "Voltage/ampere meter"
            },
            "subIntName": {
                "value": 42,
                "description": "Max meter value, if above an alarm is raised"
            },
            "subDoubleName": {
                "value": 4.2,
                "description": "Meter gain"
            }
        }
    }
}
```

## Paths
Recipe files are stored under /var/embedded/recipes/config/applicationName.json
Config files are stored under /var/embedded/config/applicationName/applicationInstance.json

## Config creator for developers
An gui is made accessible for developers to create their needed recipe, therefore as an application developer you should never need to create manually the json recipe file. 
