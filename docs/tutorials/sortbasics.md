# JSON Sort - The Basics

## Prerequisites
1. Download the VoltScript-Json-Sort repository from GitHub
1. Set up your VS Code environment including running Archipelago - Install Dependencies to ensure you have all of the necessary dependencies available (high level instructions below)
1. Basic understanding of VoltScript and Json object structure

## Objectives
1. Gain experience working with VoltScript in the Visual Studio Code environment
1. Learn about working with VoltScript Extensions - specifically JsonVSE
1. Gain familiarity with using jsonSort() to sort an array of JSON objects

## Project Setup
1. Ensure your atlas-settings.json is set up with authentication for Volt MX Marketplace and github.com
1. Create a folder for the project.
1. Create an atlas.json and complete mandatory elements. Set `sourceDir` to **"src"**, `libsDir` to **""libs"** and `vsesDir` to **"vses"**.
1. In the **repositories** element, add the following repository:

    ```vbscript
    {
            "id": "hcl-github",
            "type": "github",
            "url": "https://api.github.com/repos/HCL-TECH-SOFTWARE"
        }
    ```

1. In the dependencies element, add the following dependency:

    ```vbscript
            {
            "library": "voltscript-testing",
            "version": "latest",
            "module": "VoltScriptTesting.vss",
            "repository": "hcl-github"
        }
    ```
1. Save the atlas.json and ensure no validation errors.
1. Run dependency management (CTRL + SHIFT + P / Cmd + SHIFT + P and choose "VoltScript: Install Dependencies").
1. Ensure **libs** contains "VoltScriptCollections" and **vses** contains the JsonVSE extensions.

## Script Setup
1. Create a VoltScript file in **src** directory called `jsonSortTutorial.vss`.
1. Add `Option Public` and `Option Declare`.
1. Add a USE statement to point to your VotScriptJsonSort.vss library. If you're using this doc repository, then `Use "VoltScriptJsonSort"` (omit the .vss extension) should work.

!!! Note
    The VoltScriptJsonSort library uses the JsonVSE extension, which means that functionality is available for loading and working with Json files and objects.

## Load the Example JSON File
1. Create a Sub Initialize() sub
1. Add a JsonParser object (parser) and a Json data object (dataObj) - these will be used to load our example JSON file into memory as an array of Json objects
1. Add a String variable to hold our file path to our example JSON file (`TEST_DATA1.json`)
1. Set up the path to the example JSON file
1. Set up a Try...Catch block
1. Use the Parser object to load the JSON file into the dataObj object variable
1. Let's add a PRINT statement after the load to make sure we loaded 100 records into our JSON object (dataobj)

    ??? example "load example JSON file into memory"
        ``` vbscript
        Sub Initialize()
            Dim parser as New JsonParser()
            Dim dataobj as New JsonObject(true)
            Dim fpath as String

            Try
                fpath = CurDir() & "/src/TEST_DATA1.json"
                Call parser.loadFromFile(fpath)
                Set dataObj = parser.getRootObject()
                Print "COUNT: " & dataObj.childCount()
                
            Catch
                Print "Error " & Error() & " on line " & Erl()
            End Try
        End Sub
        ```

1. Let's run our code and make sure our JSON file loaded correctly by seeing what count we get. With your cursor in the Initialize() sub, type CTRL+F5, and hit ENTER. A Terminal window will appear at the bottom of VS Code, and you should see where your code was called, and `COUNT: 100` was returned.

## Set Up the Sort Labels
Now that we have our example JSON file loaded into memory, let's set up our labels for sorting. JsonSort() allows you to sort your array of JSON objects up two three levels deep. So, if you open and take a look at `TEST_DATA1.JSON` you'll notice that the JSON objects are basically a contact list. So, let's say that we want to sort first on STATE, then CITY, and finally COMPANY.

1. Begin by adding a String array variable with three elements to hold our sort labels. Using this array will make it easier to read, and easier for us to change the labels around later. Let's call this string array `labels()`
1. Now set up the values in our labels() array of `state`, then `city`, then `company`

Now our TRY block should look something like this...

??? example "try block with labels defined"
    ```vbscript
    Try
        fpath = CurDir() & "/src/TEST_DATA1.json"
        Call parser.loadFromFile(fpath)
        Set dataObj = parser.getRootObject()
        Print "count: " & dataObj.childCount()

        labels(0) = "state"
        labels(1) = "city"
        labels(2) = "company"
    ```

## Sort the JSON Array using jsonSort()
We're ready to sort our array. Now the signature for the `jsonSort()` function is as follows:

```vbscript
Function jsonSort(dataObj as JsonObject, _ 
    lbl1 as String, lbl1Desc as Boolean, lbl2 as String, lbl2Desc as Boolean, _
    lbl3 as String, lbl3Desc as Boolean, delim as String) as JsonObject
```

Where:

* `dataObj` - The JSON object to be sorted
* `lbl1` - The first label to sort on
* `lbl1Desc` - True if the sort should be descending, False if ascending
* `lbl2` - The second label to sort on. Optional. If not provided, lbl2 will be set to ""
* `lbl2Desc` - True if the sort should be descending, False if ascending
* `lbl3` - The third label to sort on. Optional. If not provided, lbl3 will be set to ""
* `lbl3Desc` - True if the sort should be descending, False if ascending
* `delim` - The delimiter to use for the labels. Optional. If not provided, delim will be set to "/"

Now let's add jsonSort() to our code.

1. Add a new JsonObject variable called `sortobj`. Your DIM statement should look like `Dim sortobj as JsonObject`
1. Call `jsonSort` setting the result to our new `sortobj` variable.
1. For this first time, let's set all of the Ascending/Descending flags to False, so they will all be sorted to Ascending
1. You can set the `delim` parameter to an empty string (""), as we're not using it right now. The new line should look like this:

    ```vbscript
        Set sortobj = jsonSort(dataobj, labels(0), False, labels(1), False, labels(2), False, "")
    ```

1. You could try running the code again at this point (using CTRL + F5, ENTER) to make sure you have no errors if you want.

Now that we have it sorted, let's add some code to print out a sample size of our sorted array, to make sure it worked.

## Print A Sample of the Output
We can print out a subset of our sorted JSON object array to make sure it worked correctly. Let's build a loop with a preset number of records that we would like to print out.

### Set Up the Variables
Let's begin by setting up the variables we'll need for this loop. They include:

* `results()` - a String array of three elements to hold our results
* `tmpObj` - a temporary JSON Object used to access each child object as we iterate through the array
* `rvar` - a variant to hold the Scalar Value of the corresponding label during iteration
* `i` and `z` - Integer variables used to limit our iteration

Your updated variable declarations should look something like this:

```vbscript
    Dim parser as New JsonParser()
    Dim dataobj as New JsonObject(true)
    Dim fpath as String
    Dim labels(2) as String
    Dim sortobj as JsonObject
    Dim results(2) as String
    Dim tmpobj as JsonObject
    Dim rvar as Variant, i as Integer, z as Integer
```
Now that we have our variables declared, let's begin building our output loop.

### Building the Output Loop
We're going to use a Forall loop to print a sample of our sorted JSON object array. Within this look we need to do the following *for each label*:

* Check to make sure there's a label available
* Check to make sure the label is a child of the current JSON object
* If it's available, get the Scalar Value of that label
* Check to make sure the returned Scalar Value is not EMPTY
* At any point if something isn't available set the results to `*EMPTY*`, otherwise set the results to the retrieved value
* Once we have all of the values for each label, print it out
* Add a check at the end to exit the loop once we've reached the desired number of sample values

Now, that's a lot of stuff to consider. Given the size of this, here's an example of the completed code that you can copy, paste, run, and study to understand how it all works.

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


