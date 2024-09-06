# Volt MX Objects 

The Volt MX Objects are a set of VoltScript Classes used for integrating with Volt MX Foundry. They are middleware specific classes, targeted specifically for VoltScript Integration Services. 

These classes are contained within the [VoltMXObjects Library Module](../references/apidoc/index.html){: target="_blank" rel="noopener noreferrer"}, and are instantiated when the [extractObjects()](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library.html#VoltMXObjects.extractObjects-){: target="_blank" rel="noopener noreferrer"} method is called.  

!!! note "Important"
    If the *extractObject()* method is not called, these objects will not be instantiated correctly; which will result in erratic behavior or failure of your VoltScript code. 


## VoltMX Classes 
The VoltMX Classes are as follows:

- [**VoltMX Logger Object**](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxLoggerObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for passing debug messages back to Foundry's Java logger.

- [**VoltMX Request Object**](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxRequestObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for interacting with the Foundry request.

- [**VoltMX Response Object**](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxResponseObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for interacting with the Volt MX response.

- [**VoltMX Result Object**](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxResultObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for manipulating integration service results and passing content back to Foundry.

- [**VoltMX Session Object**](../references/apidoc/VoltMXObjects_VSID/VoltMXObjects_Library/VoltMxSessionObject_ObjectClass.html){: target="_blank" rel="noopener noreferrer"} for interacting with Foundry session content.
