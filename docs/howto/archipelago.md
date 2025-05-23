# Use dependency management

!!!info
    For generic how-to information about VoltScript Dependency Management, see [VoltScript documentation](https://help.hcltechsw.com/docs/voltscript/early-access/howto/writing/archipelago.html){: target="_blank" rel="noopener noreferrer"}.

Dependency management is available in the documentation for each project, but also aggregated here:

## Authentication

You'll need a [Personal Access Token](https://help.hcltechsw.com/docs/voltscript/early-access/howto/writing/archipelago.md#github-personal-access-token) to use GitHub REST APIs. You'll then need to add the following to the JSON object in your [atlas-settings.json](https://help.hcltechsw.com/docs/voltscript/early-access/howto/writing/archipelago.md#atlas-settingsjson) in the `.vss` directory of your user home directory:

```json
    "hcl-github": {
        "type": "github",
        "token": "${env.TOKEN}"
    },
    "volt-mx-marketplace": {
        "type": "marketplace",
        "username": "YOUR_USERNAME",
        "password": "YOUR_PASSWORD",
        "authUrl": "https://accounts.auth.demo-hclvoltmx.net/login"
    }
```

!!!tip
    Hard-coding your Personal Access Token in the atlas-settings.json file works well for initial setup and testing, but is **not recommended** for production.  The recommended method is to store your Personal Access Token as an environment variable, and then reference that variable using the **${env.VARIABLE_NAME}** pattern as demonstrated below

```json
"hcl-github": {
    "type": "github",
    "token": "${env.TOKEN}"
}
```

## Repository

You'll need to add the following to your **repositories** object in the `atlas.json` of your project:

```json
{
    "id": "hcl-github",
    "type": "github",
    "url": "https://api.github.com/repos/HCL-TECH-SOFTWARE"
}
```

## Dependency

You'll need to add the following relevant dependency to your **dependencies** object in the `atlas.json` of your project:

```json
        {
            "library": "voltscript-voltmx-middleware",
            "version": "1.0.5",
            "module": "VoltMXObjects.vss",
            "repository": "hcl-github"
        }
```