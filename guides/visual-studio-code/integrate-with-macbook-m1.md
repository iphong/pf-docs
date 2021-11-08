# Integrate with Macbook M1

In VS Code add folder pfcore and pfserver to workspace

![](<../../.gitbook/assets/Screen Shot 2021-11-03 at 16.30.15.png>)

Then in the Run & Debug tab, create new configurations for each project fiolder as following:

#### pfcore configurations

```javascript
// pfcore
{
    "version": "0.2.0",
    "configurations": [
        {
            "command": "yarn start",
            "name": "run app",
            "request": "launch",
            "type": "node-terminal",
            "presentation": {
                "hidden": true
            }
        }
    ]
}
```

#### pfserver configurations

```javascript
// pfserver
{
    "version": "0.2.0",
    "configurations": [
        {
            "command": "docker-compose -f docker-compose.yml up",
            "name": "run docker",
            "request": "launch",
            "type": "node-terminal",
            "presentation": {
                "hidden": true
            }
        },
        {
            "command": "yarn watch",
            "name": "run server",
            "request": "launch",
            "type": "node-terminal",
            "presentation": {
                "hidden": true
            }
        }
    ]
}
```

#### Workspace configuration

```javascript
{
    "folders": [
        {
            "path": "pfcore"
        },
        {
            "path": "pfserver"
        }
    ],
    "launch": {
        "version": "0.2.0",
        "compounds": [
            {
                "name": "start",
                "configurations": [
                    {
                        "name": "run docker",
                        "folder": "pfserver"
                    },
                    {
                        "name": "run server",
                        "folder": "pfserver"
                    },
                    {
                        "name": "run app",
                        "folder": "pfcore"
                    }
                ],
                "presentation": {
                    "hidden": false,
                    "group": "all",
                    "order": 1
                },
                "stopAll": true
            }
        ],
        "configurations": []
    },
    "settings": {
        "liveServer.settings.multiRootWorkspaceName": "pfcore"
    }
}

```

#### Then select the configuration to run

![](<../../.gitbook/assets/Screen Shot 2021-11-03 at 16.49.01.png>)

#### Now press the play icon on your M1 Macbook

