# Foundry processing

Foundry sends HTTP requests across to the VoltScript runtime for processing. The approach is the same for preprocessors, integration services and postprocessors.

``` mermaid
sequenceDiagram
    autonumber
    UI->>Foundry: REST service request
    Foundry->>Foundry: Convert context to JSON
    Foundry->>VoltScript: Send HTTP request with Foundry context
    VoltScript->>VoltScript: Process custom VoltScript code
    VoltScript->>Foundry: Send result JSON object
    Foundry->>Foundry: Parse response and continue, if appropriate
    Foundry->>UI: Send response / error
```

--8<-- "prepost.md"

For a preprocessor, if the code ends with `return false`, an abort signal is sent back to Foundry in the `VoltMXResult`. On finding that, Foundry aborts the integration service and no further steps in the process will be performed. So the processing is:

```mermaid
sequenceDiagram
    participant UI
    participant Foundry
    participant is as Integration Service 
    autonumber
    UI->>Foundry: REST service request
    Foundry->>is: Trigger preprocessor
    is->>Foundry: Sends result
    opt return false
    Foundry->>UI: Send response
    end
    Foundry->>is: Trigger main integration service
    is->>Foundry: Send result
    Foundry->>is: Trigger postprocessor
    is->>Foundry: Send result
    Foundry->>UI: Send response
```