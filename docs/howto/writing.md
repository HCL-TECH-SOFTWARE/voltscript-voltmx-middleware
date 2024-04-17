# Write VoltScript Volt MX Middleware functions

VoltScript can be used in Integration Services or pre- and postprocessors.

- Integration services are REST service operations coded completely in VoltScript.
- VoltScript preprocessors are VoltScript functions run *before* triggering an external REST service call. They return true (the default) to continue processing or false to abort processing.
- VoltScript postprocessors are VoltScript functions run *after* triggering an external REST service call. Typically they will be used to manipulate the result from the REST service call. There is no subsequent process, so `Return False` has no effect.

A VoltScript integration service is uploaded to Foundry as a zip file. Each main script maps to an operation.

When writing your main script, the **Foundry boilerplate** snippet can be accessed by typing "foundry". This snippet can be used to populate a VoltScript script with code to parse incoming Foundry JSON object and return the result back to Foundry. This can be accessed by typing `foundry boilerplate` in an empty .vss file. For details on what the boilerplate does, see [Understanding the boilerplate](../topicguides/boilerplate.md).

Comment blocks identify where you should put your custom code.

!!! note
    A single main script could be used for multiple operations, if desired. processing might vary based on a query string parameter passed, for example.