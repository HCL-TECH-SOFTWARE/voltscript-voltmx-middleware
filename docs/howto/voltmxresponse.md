# Retrieve metadata from external REST service

The `VoltMxResponse` object is used in a postprocessor to access the headers and device headers from the external REST service call.

!!! note

    The `VoltMxResponse` object is **not** used to retrieve the body response from the external REST service. Use the `VoltMXResult.result` JSON object for this.

## Check return status

You can check the response code returned by using `VoltMxResponse.getStatusCode()`. The following code would abort processing if status code was not 200.

``` vbscript
If (VoltMxResponse.getStatusCode != 200) Then Return
```

## Header parameters

Response header parameters can also be accessed and manipulated. Of course, headers will currently be blank unless running in a postprocessor.

- `VoltMxResponse.getHeaderParam()` will retrieve a parameter from the main response.
- `VoltMxResult.addHeaderParam()` can add a header. The is also called by the corresponding function in `VoltMxResponse`.
- `VoltMxResponse.getDeviceHeaderParam()` will retrieve a device header parameter from the main response.
- `VoltMxResult.addDeviceHeaderParam()` can add a device header. The is also called by the corresponding function in `VoltMxResponse`.