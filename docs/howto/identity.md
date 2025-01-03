# Use Identity Service tokens

If the integration service has an identity service mapped to it, the tokens are also passed to the VoltScript code.

## KeepVSE

For authenticating via KeepVSE, you do not need to extract and pass the token. KeepVSE does this for you, you just need to instantiate the `KeepServer` object and specify the server URL, for example:

``` vbscript
Dim server as New KeepServer()
server.serverURL = "http://localhost:8080/api/v1/"
```

!!! note
    To write integration tests, pass the logged in KeepServer object to a function. In your integration test, log into the KeepServer manually using `KeepServer.login()` and you can verify the rest of your function runs as expected.

## Other backends

For other backends, you will need to extract the token from the identity service manually. This can be done with `VoltMxRequest.getIdentityParam()`.