!!! note

    Due to the multi-step processing overhead necessary for Foundry to run VoltScript code: 
    
    1. Foundry marshals the request context
    1. Foundry sends the request context to VoltScript
    1. VoltScript unmarshals the request context
    1. **VoltScript processes the data**
    1. VoltScript marshals the response JSON
    1. VoltScript sends response JSON back to Foundry
    1. Foundry unmarshals the response JSON
    1. Foundry parses the response and determines the next operation

    *VoltScript* Pre or Post Processors for *VoltScript* Integration Services are therefore **not supported in Foundry.**  Any such validation, logic, or processing code should instead be added directly to the VoltScript Integration Service code.  
