# Session attributes

You may wish to get or set session attributes. If set, these will be available to all subsequent requests for the same Foundry session. The following code could be used to lazy load authentication to an external database:

``` vbscript
Dim token as String
token = VoltMxSession.getAttribute("dbToken")
If (token = "") Then
    ' Do something to populate the token variable
    Call VoltMxResult.addSessionAttribute("dbToken", token)
End If
' Do something with the token
```

`VoltMxSession.addAttribute()` is also available, but it just calls `VoltMxResult.addSessionAttribute()`.