# Aims for VoltScript Volt MX Middleware

- Provides bootstrap code for handling incoming data from Foundry:

    - Current project directory, required because `CurDir` maps to the directory of the running VoltScript program
    - Session information
    - HTTP request headers
    - Service input parameters and parameters specifically mapped in the integration service
    - HTTP request parameters and all request parameters that are part of the Foundry HTTP request
    - HTTP response headers and device headers

- Provides access to the Volt MX Logger object for writing debug messages to the Volt MX Foundry application logs.
- Utilizes [VoltMX Result Object](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxResultObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for updating the Volt MX Foundry objects.
