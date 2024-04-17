---
hide:
    - navigation
---
# Welcome to VoltScript Volt MX Middleware documentation

VoltScript Volt MX Middleware is VoltScript files for integrating with [HCL Volt MX Go](https://opensource.hcltechsw.com/voltmxgo-documentation/index.html){: target="blank"}. Currently, the only library available is **VoltMXObjects.vss**. It's a library for use in Volt MX Foundry integration services for parsing the request content coming into Foundry and passing a JSON result back. In future enhancements, there might be a VoltScript library for making requests to Foundry.

<!--Currently, the only library available is **VoltMXObjects.vss**, a library for use in Volt MX Foundry integration services, for parsing the request content coming into Foundry and passing a JSON result back. However, it is anticipated that future enhancements may include a VoltScript library for making requests to Foundry.-->

To manage the content coming from Foundry, there are various dependencies:

- **ContextVSE** is for parsing the JSON object passed from Foundry.
- **JSONVSE** is necessary for manipulating JSON objects used in communication.
- **VoltScript Collections** is for facilitating easier interaction by enabling incoming content to be parsed into Maps.
- **VoltScript Testing** is only a dependency for unit testing of the framework and isn't a runtime dependency.

---
## What's new

For the latest release information about VoltScript Volt MX Middleware, see [What's new](references/whatsnew.md).

---
## Using via dependency management

For using with dependency management, see [Use dependency management](howto/archipelago.md).

---
## How the documentation is organized

The documentation is based on the [Diátaxis framework](https://diataxis.fr/){: target="_blank" rel="noopener noreferrer”}, which organizes documentation into the following modes to address users' documentation needs at different times and in different circumstances. Below shows an overview that guides you on where to look for needed information:

**[Tutorials](tutorials/index.md)** - Hands-on introduction on how to use VoltScript Volt MX Middleware

**[How-to guides](howto/index.md)** - Practical step-by-step guides for performing tasks and operation

**[Topic guides](topicguides/index.md)** - High-level discussion and explanation of key topics and concepts in VoltScript Volt MX Middleware

**[References](references/index.md)** - Contain API documentation and test reports
