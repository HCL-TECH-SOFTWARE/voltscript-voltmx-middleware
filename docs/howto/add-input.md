# Add input parameters

In a preprocessor, you may wish to programmatically add input parameters for a subsequent external REST service. This might be used, for example, to set a login token to an environment variable that is passed to Foundry when the server is started. The following code will allow you to do this:

```vbscript
Dim token as String
token = Environ$("dbToken")
Call VoltMxResult.addInputParam("token", token)
```

!!! note
    The same function is available on `VoltMxRequest` object. But that function just calls the corresponding function in VoltMxResult.

!!! note
    If required, request and header parameters can also be added via `VoltMxResult.addRequestParam()`. A corresponding function again exists in `VoltMxRequest`, but again just call the `VoltMxResult` version.

!!! warning
    `VoltMxResult.addHeaderParam()` does not modify the header parameters passed to an external REST service. Instead it is used to set a header parameter in the response.