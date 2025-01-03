# Aims for VoltScript Volt MX Middleware

- Provides bootstrap code for handling incoming data from Foundry:

    - Current project directory, required because `CurDir` maps to the directory of the running VoltScript program
    - Session information
    - HTTP request headers
    - Service input parameters and parameters specifically mapped in the integration service
    - HTTP request parameters and all request parameters that are part of the Foundry HTTP request
    - HTTP response headers and device headers

- Integrate Volt MX Logging seamlessly with the normal Volt MX Foundry logging.
- Utilizes [VoltMX Result Object](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxResultObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for updating the Volt MX Foundry objects.
