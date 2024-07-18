# Understanding the boilerplate

The **Foundry boilerplate** snippet provides the boilerplate code for a VoltScript integration service in Foundry.

## Boilerplate snippet

```vb linenums="1"
Option Declare
Option Public

Use "../libs/VoltMXObjects"
UseVSE "*ContextVSE"

Sub Initialize
    Dim ctx as New Context()
    Dim data as String

    Try
        data = ctx.Context
        Call extractObjects(data, false)

        '****************
        'START OF FOUNDRY HANDLER
        '****************
        
        '****************
        'END OF FOUNDRY HANDLER
        '****************

    Catch
        Call VoltMxResult.setErrorMessage(getErrorMsg("VOLTSCRIPT_CONNECTOR: "))
    Finally
        Print VoltMxResult.toJson().toString(false)
    End Try
End Sub

Private Function getErrorMsg(prefix as String) as String
    If (Instr(Error(), "line ") > 0) Then
        Return Error()
    End If
    Return prefix & " ERROR: " & Error() & " (" & Err() & "), line " & Erl()
End Function
```

## Explanation

- Options are set in line 1 and 2.
- Dependencies are added in lines 4 and 5.
- Context is created in line 8 and the data loaded into the `data` string at line 12.

    - If a JWT token is passed in the context, this automatically get passed to a new `KeepServer` object.

- `extractObjects()` function is called at line 13 to load the passed JSON object into VoltMXRequest, VoltMXSession, VoltMXResponse and VoltMXResult objects.
- Custom code can be entered in the area between the comments, at line 18.
- If an error occurs, `VoltMXResult.setMessage()` is called at line 24, parsing the error using the `getErrorMsg()` function.
- The VoltMXResult object is converted to a JSON string and printed out. The VoltScript runtime passes this back to Foundry.
