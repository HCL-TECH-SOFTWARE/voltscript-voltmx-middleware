# FAQs

## Print statements

Volt MX Foundry passes a JSON object across to the VoltScript runtime and expects a JSON object in return. Additional `Print` statements in your VoltScript code returns an invalid JSON object that corrupts the output.