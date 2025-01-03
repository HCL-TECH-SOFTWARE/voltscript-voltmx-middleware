# Add logging

Since version 1.0.5 VoltScript Volt MX Middleware is integrated with VoltScript Logging. This comprises two parts:

- creating logs.
- outputting logs.

!!! warning
    The Volt Foundry image provided in VoltScript Early Access 3 does not support integration with VoltScript Logging. If you are using VoltScript EA3, Volt Foundry code will error when trying to extract the logs.

## Creating logs

Creating logs is done the same as normal in VoleScript, using `globalLogSession.createLogEntry()`. At the end of the VoltScript code, when the VoltMXResult is converted to JSON and sent back, any logs will be extracted and passed back in the `debugMessages` object. Each message will be a JSON  object comprising:

- **level**, 1 - 6, corresponding to the logging level.
- **message**, using the formatter `[{{LIBRARYNAME}}:{{CLASSNAME}}:{{METHODNAME}}:{{LINENUM}}] {{MESSAGE}}`.
- **stack trace** in compact format.

During debugging, the VoltMXResult will be printed out, so you can check the logs there.

## Outputting logs

After being received by Volt Foundry, the logs will be passed to the Java logger in a consistent approach with Java and JavaScript logging. The logs will be added with the corresponding logging level.

By default, only logs above a certain level will be added to the Volt Foundry console. To change the logging level:

- Go to **Environments**.
- Click on the relevant environment. The App Services console will be displayed.
- Go to **Logs**.
- Change the log level for the Root Logger.
- Save the changes.

The logs will then be written to the Volt Foundry console, as with Java and JavaScript logs.

!!! tip
    Setting the logging level for `com.hcl.voltscript` will set a logging level specific to logs from the Volt Foundry VoltScript servlet.

## Additional log writers

Additional log writers can be added to the global log session, if you would like to provide alternate logging options, separate from the Volt Foundry Java loggers.