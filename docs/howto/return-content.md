# Return content

The `VoltMXResult.result` JSON object is used to pass data back to the user.

**opstatus** can be manipulated to return different statuses for use in the Iris application processing. Typically, a successful operation returns an opstatus as 0.

**httpStatusCode** can return a specific HTTP status code, e.g. 200 for success or 400 for bad input.

Volt MX Foundry always returns a JSON object, always including "opstatus" and "httpStatusCode". Everything else is properties within that JSON object and this is accessed via `VoltMXResult.result`. You can use the various JsonVSE methods to add scalars, arrays or objects, all with their various labels.

!!! warning

    Using `VoltMXResult.result.appendToJSONArray()` will throw an error, because `result` is always a JSON object, not a JSON array.

You do not need to explicitly add opstatus and httpStatusCode to the `VoltMXResult.result` object. These will automatically be appended from the relevant properties before the output is printed.

## Access result in postprocessor

In a postprocessor `VoltMxResult.result` will already be seeded with the output from the main integration service. You can access this and manipulate it as required.