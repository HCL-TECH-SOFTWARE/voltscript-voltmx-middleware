# Access VS Code Extension build development features

The Visual Studio Code Build Management Extension provides various functionality for speeding up development.

## atlas.json

The first is an atlas.json snippet template. This can be accessed by creating an atlas.json, typing `foundry-atlas` and accepting the snippet.

The snippet automatically adds the dependencies and repository for VoltMXObjects.

## Foundry script boilerplate

The second is a script snippet template for writing a VoltScript integration service. The snippet:

- Adds required `Use` and `UseVSE` statements.
- Adds a `Sub Initialize` with the boilerplate code for extracting Foundry objects and sending back a response.

This can be accessed by creating a script file, typing `foundry` and accepting the snippet.

## Package for Foundry

This is a command accessed from the Visual Studio Code Command Palette when you are in the `atlas.json` or a `.vss` file. The process:

- Prompts for the project directory.
- Prompts for the location of the `atlas.json``.
- Creates a zip file comprising:
    - `atlas.json`
    - `seti.ini`
    - src directory
    - libs directory
    - vses directory

The zip file is named using the `name` and `version` in the `atlas.json`. For example, if the `name` is *vss-poc* and the `version` is *1.0.0*, the filename of the zip file will be *vss-poc-1.0.0.zip*. The zip file is placed in the root of the project directory and ready to be uploaded to Foundry.
