# JSON Sort - Using Label Paths

## Prerequisites

1. Download the VoltScript-Json-Sort repository from GitHub
1. Set up your VS Code environment including running Archipelago - Install Dependencies to ensure you have all of the necessary dependencies available (completed in The Basics tutorial)
1. Basic understanding of VoltScript and Json object structure
1. **Completed Sort Basics Tutorial**

## Objectives

1. Build on knowledge gained in JSON Sort - The Basics tutorial
1. Understand how to use label paths to sort on nested JSON objects
1. Learn how to use `jsonObject.isDescendantPath()` and `jsonObject.getDescendantPath()`

## Introduction

In The Basics tutorial we built a working example using jsonSort(), and used "first level" labels to sort our example JSON array. But what if your JSON array has a "nested" object, similar to the example below - and you want to sort on the City and State?

```JSON
    {
        "company": "Yotz",
        "firstName": "Germaine",
        "lastName": "Pirelli",
        "email": "gpirelli0@gmpg.org",
        "gender": "Agender",
        "salary": "$89175.71",
        "address": {
            "street1": "99106 Upham Center",
            "street2": null,
            "city": "New York City",
            "state": "New York",
            "zip": "10029"
        }
    }
```

That's where *label paths* come in. jsonSort() has the ability for you to provide a delimited "path" to the label on which you wish to sort. And the JsonObject class has methods to help you access these label path values. Let's take a look...

## Before we begin

We're going to build upon the work we did in The Basics tutorial. If you didn't actually complete the tutorial, here's the completed code from it - assuming you've already set up your VS Code environment and loaded the necessary files, simply copy this code and paste it into VS Code.

???example "Completed JSON Sort - The Basics Example"
    ```vbscript
        Option Public
        Option Declare

        Use "VoltScriptJsonSort"

        Sub Initialize()
            Dim parser as New JsonParser()
            Dim dataobj as New JsonObject(true)
            Dim fpath as String
            Dim labels(2) as String
            Dim sortobj as JsonObject
            Dim results(2) as String
            Dim tmpobj as JsonObject
            Dim rvar as Variant, i as Integer, z as Integer

            Try
                fpath = CurDir() & "/src/TEST_DATA1.json"
                Call parser.loadFromFile(fpath)
                Set dataObj = parser.getRootObject()
                Print "count: " & dataObj.childCount()

                labels(0) = "state"
                labels(1) = "city"
                labels(2) = "company"

                z = 10  ' how many example entries to print

                Set sortobj = jsonSort(dataobj, labels(0), False, labels(1), False, labels(2), False, "")
                
                Forall obj in sortobj.GetChildren()   
                    Set tmpobj = obj ' obj is a variant - setting it to tmpobj to give us access to JsonObject methods

                    ' Check to make sure there's a label available
                    ' At any point if something isn't available set the results to `*EMPTY*`
                    If labels(0) = "" Then  
                        results(0) = "*empty*"
                    Else
                        ' Check to make sure the label is a child of the current JSON object
                        If tmpobj.isChild(labels(0)) Then
                            'If it's available, get the Scalar Value of that label
                            rvar = tmpobj.getChild(labels(0)).ScalarValue
                            ' Check to make sure the returned Scalar Value is not EMPTY
                            If isEmpty(rvar) Then 
                                results(0) = "*empty*"
                            Else
                                results(0) = Cstr(rvar)
                            End If
                        End IF
                    End If

                    If labels(1) = "" Then
                        results(1) = "*empty*"
                    Else
                        If tmpobj.isChild(labels(1)) Then
                            rvar = tmpobj.getChild(labels(1)).ScalarValue
                            If isEmpty(rvar) Then 
                                results(1) = "*empty*"
                            Else
                                results(1) = Cstr(rvar)
                            End If
                        End IF
                    End If

                    If labels(2) = "" Then
                        results(2) = "*empty*"
                    Else
                        If tmpobj.isChild(labels(2)) Then
                            rvar = tmpobj.getChild(labels(2)).ScalarValue
                            If isEmpty(rvar) Then 
                                results(2) = "*empty*"
                            Else
                                results(2) = Cstr(rvar)
                            End If
                        End IF
                    End If  

                    ' Once we have all of the values for each label, print it out
                    Print "state: " & results(0) & ", city: " & results(1) & ", company: " & results(2)

                    ' Add a check at the end to exit the loop once we've reached the desired number of sample values
                    i++
                    If i = z Then Exit ForAll
                End Forall

            Catch
                Print "Error " & Error() & " on line " & Erl()
            End Try
        End Sub
    ```

## Change the file path and labels

The first thing we need to do is change the file path to point to our new JSON data file. After that, let's modify the labels we use for the sort to use paths. We also need to specify the *delimiter* we're using to separate the parts of the label path - in this case we're using a forward slash (`/`).

!!! Note
    The default delimiter is a forward slash; but since a forward slash is an allowed character in a JSON label, you may need to provide a different delimiter.

1. Change the `fpath` variable so that it points to `TEST_DATA2.json`
1. Change `labels(0)` to `company`
1. Change `labels(1)` to `address/state`
1. Change `labels(2)` to `address/city`
1. Create a new string variable called `delim`, and set it to a forward slash (`/`)

The beginning of your code should now look something like this...

```vbscript
    Dim parser as New JsonParser()
    Dim dataobj as New JsonObject(true)
    Dim fpath as String
    Dim labels(2) as String
    Dim sortobj as JsonObject
    Dim results(2) as String
    Dim tmpobj as JsonObject
    Dim rvar as Variant, i as Integer, z as Integer
    Dim delim as string

    Try
        fpath = CurDir() & "/src/TEST_DATA2.json"
        Call parser.loadFromFile(fpath)
        Set dataObj = parser.getRootObject()
        Print "count: " & dataObj.childCount()

        labels(0) = "company"
        labels(1) = "address/state"
        labels(2) = "address/city"
        delim = "/"
```

## Verifying and retrieving label path values

In our Basics code we used `jsonObject.isChild()` and `jsonObject.getChild()` to verify and retrieve label values; however these calls only work for first-level labels. In order for us to access values from a label path, we need to use different calls - `jsonObject.isDescendantPath()` and `jsonObject.getDescendantPath()`.

!!! Note
    `jsonObject.isDescendantPath()` and `jsonObject.getDescendantPath()` will work with first-level labels as well, such as `company` in our example.

We will need to replace all calls to `isChild()` with `isDescendantPath()`, and all calls to `getChild()` with `getDescendantPath()`. We also need to add the `delim` parameter to the `jsonSort()` call.

1. Change the last parameter of the `jsonSort()` call from and empty string (`""`) to `delim`
1. In each of the three label blocks, change `tmpobj.isChild` to `tmpobj.isDescendantPath`
1. In each of the three label blocks, change `tmpobj.getChild` to `tmpobj.getDescendantPath`

The call to `jsonSort()` should now look like this:

```vbscript
    Set sortobj = jsonSort(dataobj, labels(0), False, labels(1), False, labels(2), False, delim)
```

And each of the label code blocks should look like this:

```vbscript
    If labels(0) = "" Then  
        results(0) = "*empty*"
    Else
        ' Check to make sure the label is a child of the current JSON object
        If tmpobj.isDescendantPath(labels(0)) Then
            'If it's available, get the Scalar Value of that label
            rvar = tmpobj.getDescendantPath(labels(0)).ScalarValue
            ' Check to make sure the returned Scalar Value is not EMPTY
            If isEmpty(rvar) Then 
                results(0) = "*empty*"
            Else
                results(0) = Cstr(rvar)
            End If
        End IF
    End If
```

### One more thing to fix

The last small change we need to make is the example printout labels. Change the Print line from this:

```vbscript
    Print "state: " & results(0) & ", city: " & results(1) & ", company: " & results(2)
```

To this:

```vbscript
    Print "company: " & results(0) & ", state: " & results(1) & ", city: " & results(2)
```

## Test our code

Now let's take a look at our results. With your cursor in your code, type CTRL + F5, and hit ENTER. You should get results like this:

```bash
count: 100
company: *empty*, state: California, city: Salinas
company: *empty*, state: California, city: San Jose
company: *empty*, state: California, city: San Mateo
company: *empty*, state: Connecticut, city: Stamford
company: *empty*, state: New Mexico, city: Albuquerque
company: *empty*, state: New York, city: Brooklyn
company: *empty*, state: New York, city: Rochester
company: *empty*, state: Oregon, city: Beaverton
company: *empty*, state: Texas, city: Garland
company: *empty*, state: Texas, city: Houston
```

Now notice that the company tags all say `"*empty*"` - that's because some of our company values are `null`. `jsonObject.getDescendantPath()` will return EMPTY if the value is NULL, and then we can use `isEmpty()` to check for and EMPTY value.

Just to make sure some values are being returned for `company`, let's reverse the sort order of `company`. Do this by changing the isDescending flag for label1 in `jsonSort()` to `True`:

```vbscript
    Set sortobj = jsonSort(dataobj, labels(0), True, labels(1), False, labels(2), False, delim)
```

Now when we run our code, we get this:

```bash
count: 100
company: Zooxo, state: California, city: San Francisco
company: Zoonder, state: New York, city: Flushing     
company: Zoomzone, state: Georgia, city: Cumming      
company: Zoombox, state: New York, city: New York City
company: Zoombeat, state: Michigan, city: Flint
company: Youspan, state: Arizona, city: Scottsdale
company: Yotz, state: New York, city: New York City
company: Yombu, state: Nevada, city: Henderson
company: Yodel, state: New York, city: New York City
company: Yakidoo, state: Georgia, city: Atlanta
```

## Conclusion

Now you have a basic understanding of how `jsonSort()` can be used to easily and quickly sort your array of JSON objects, up to three levels deep, and even with nested JSON objects using label paths.

For reference, here is the completed code for this Tutorial:

???example "Completed JSON Sort - The Label Paths Example"
    ```vbscript
        Option Public
        Option Declare

        Use "VoltScriptJsonSort"

        Sub Initialize()
            Dim parser as New JsonParser()
            Dim dataobj as New JsonObject(true)
            Dim fpath as String
            Dim labels(2) as String
            Dim sortobj as JsonObject
            Dim results(2) as String
            Dim tmpobj as JsonObject
            Dim rvar as Variant, i as Integer, z as Integer
            Dim delim as string

            Try
                fpath = CurDir() & "/src/TEST_DATA2.json"
                Call parser.loadFromFile(fpath)
                Set dataObj = parser.getRootObject()
                Print "count: " & dataObj.childCount()

                labels(0) = "company"
                labels(1) = "address/state"
                labels(2) = "address/city"
                delim = "/"

                z = 10  ' how many example entries to print

                Set sortobj = jsonSort(dataobj, labels(0), True, labels(1), False, labels(2), False, delim)
                
                Forall obj in sortobj.GetChildren()   
                    Set tmpobj = obj ' obj is a variant - setting it to tmpobj to give us access to JsonObject methods

                    ' Check to make sure there's a label available
                    ' At any point if something isn't available set the results to `*EMPTY*`
                    If labels(0) = "" Then  
                        results(0) = "*empty*"
                    Else
                        ' Check to make sure the label is a child of the current JSON object
                        If tmpobj.isDescendantPath(labels(0)) Then
                            'If it's available, get the Scalar Value of that label
                            rvar = tmpobj.getDescendantPath(labels(0)).ScalarValue
                            ' Check to make sure the returned Scalar Value is not EMPTY
                            If isEmpty(rvar) Then 
                                results(0) = "*empty*"
                            Else
                                results(0) = Cstr(rvar)
                            End If
                        End IF
                    End If

                    If labels(1) = "" Then
                        results(1) = "*empty*"
                    Else
                        If tmpobj.isDescendantPath(labels(1)) Then
                            rvar = tmpobj.getDescendantPath(labels(1)).ScalarValue
                            If isEmpty(rvar) Then 
                                results(1) = "*empty*"
                            Else
                                results(1) = Cstr(rvar)
                            End If
                        End IF
                    End If

                    If labels(2) = "" Then
                        results(2) = "*empty*"
                    Else
                        If tmpobj.isDescendantPath(labels(2)) Then
                            rvar = tmpobj.getDescendantPath(labels(2)).ScalarValue
                            If isEmpty(rvar) Then 
                                results(2) = "*empty*"
                            Else
                                results(2) = Cstr(rvar)
                            End If
                        End IF
                    End If  

                    ' Once we have all of the values for each label, print it out
                    Print "company: " & results(0) & ", state: " & results(1) & ", city: " & results(2)

                    ' Add a check at the end to exit the loop once we've reached the desired number of sample values
                    i++
                    If i = z Then Exit ForAll
                End Forall

            Catch
                Print "Error " & Error() & " on line " & Erl()
            End Try
        End Sub
    ```
