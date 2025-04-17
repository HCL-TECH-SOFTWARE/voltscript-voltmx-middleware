# VoltScript Volt MX Middleware

Libraries for integrating with Volt MX Foundry.

## Using dependency management

Dependency management is available in the documentation for each project, but also aggregated here:

### Authentication

You'll need a [Personal Access Token](../howto/writing/archipelago.md#github-personal-access-token) to use GitHub REST APIs. You'll then need to add this to the JSON object in your [atlas-settings.json](../howto/writing/archipelago.md#atlas-settingsjson), in the .vss directory of your user home directory:

```json
    "hcl-github": {
        "type": "github",
        "token": "${env.TOKEN}"
    }
```

For downstream dependencies, you'll need to sign up for the Volt MX Marketplace. Instructions are in the [how-to-guide](https://help.hcltechsw.com/docs/voltscript/early-access/howto/writing/archipelago.html#volt-mx-marketplace-credentials). **NOTE:** Ensure you log into the Volt MX Marketplace via a browser after confirming your account, to ensure the account is properly activated. Otherwise authentication to gain an access token will fail.

You'll then need to add this to the JSON object in your [atlas-settings.json](https://help.hcltechsw.com/docs/voltscript/early-access/howto/writing/archipelago.md#atlas-settingsjson), in the .vss directory of your user home directory:

```json
    "volt-mx-marketplace": {
        "type": "marketplace",
        "username": "YOUR_USERNAME",
        "password": "YOUR_PASSWORD",
        "authUrl": "https://accounts.auth.demo-hclvoltmx.net/login"
    }
```

### Repository

You'll need to add to your **repositories** object in the atlas.json of your project:

```json
        {
            "id": "hcl-github",
            "type": "github",
            "url": "https://api.github.com/repos/HCL-TECH-SOFTWARE"
        }
```

### Dependency

You'll need the relevant dependency to add to your **dependencies** or **testDependencies** object in the atlas.json of your project:

```json
        {
            "library": "voltscript-voltmx-middleware",
            "version": "1.0.5",
            "module": "VoltMXObjects.vss",
            "repository": "hcl-github"
        }
```

## VoltMXObjects

VoltMXObjects is used for parsing the JSON object sent by a Foundry integration service (also also used behind the scenes in pre/postprocessors). The key objects are exposed as global properties. The JSON object will be passed as the context and accessed via ContextVSE:

```voltscript
Dim ctx as New Context()
data = ctx.context
```

The `extractObjects()` function will then parse the JSON object and populate the variables.

### Error Handling and Returning Context

The return output should be a JSON object **and only the JSON object**. This should be `VoltMxResult.toJson()`. Errors should be passed by call `VoltMxResult.setError()`.

## Contributing

See [CONTRIBUTING.md](contributing.md).

## Code of Conduct

See [CODE_OF_CONDUCT.md](code_of_conduct.md).

## Issues and discussions

Let's chat on [OpenNTF Discord](https://openntf.org/discord).

For long-running discussions, use Discussions area in GitHub. For bugs and feature requests **specific to VoltScript VoltMX Middleware** use, Issues area.
