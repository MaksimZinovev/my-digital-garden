---
{"dg-publish":true,"permalink":"/javascript/chatgpt-parse-csv-file/","tags":["javascript"],"created":"","updated":""}
---


I have a table in  csv file with 3 columns: "parameter", "value", "description". 
Second row:
- "email"
- "myemail@gmail.com"
- "user email"

Third row:
- "url"
- "myurl.com"
- "website url"
  
Write JavaSript function to parse data from csv file so that each parameter can be accessed like this
```js

const userEmail = data.email;
const baseurl = data.url;
 ```
Use this function ReadTextFromFile() which can  read data from a text file: 

```js
function ReadTextFromFile()
{
  var sPath = "D:\Files\MyFile.txt";

  // Opens the specified file for reading
  var myFile = aqFile.OpenTextFile(sPath, aqFile.faRead, aqFile.ctUnicode);
  Log.Message("File by lines:");

  // Reads text lines from the file and posts them to the test log
  while(! myFile.IsEndOfFile())
  {
    s = myFile.ReadLine();
    Log.Message(s);
  }

  // Closes the file
  myFile.Close();
}
```
The `aqTextFile` object provides programming access to text files. The objects of this type are returned by the [`OpenTextFile`](https://support.smartbear.com/testcomplete/docs/reference/program-objects/aqfile/opentextfile.html) method.


Also use the `aqString.GetListItem` method that returns an item at the specified index in the string list where items are delimited by the [`aqString.ListSeparator`](https://support.smartbear.com/testcomplete/docs/reference/program-objects/aqstring/listseparator.html)

Example:


```js
function GetListItemSample()
{
  var str = "0;1;1;2;3;5;8;13;21;34";
  aqString.ListSeparator = ";";

  for (var i = 0; i < aqString.GetListLength(str); i++)
    Log.Message(aqString.GetListItem(str, i));
}
```



Another implementation

```js
function ReadTextFromFile() {
  var sPath = "D:\Files\MyFile.txt";
  var data = {};

  try {
    // Opens the specified file for reading
    var myFile = aqFile.OpenTextFile(sPath, aqFile.faRead, aqFile.ctUnicode);

    while (!myFile.IsEndOfFile()) {
      var line = myFile.ReadLine();

      // Get the list items from the line
      aqString.ListSeparator = ",";
      var parameter = aqString.GetListItem(line, 0);
      var value = aqString.GetListItem(line, 1);
      var description = aqString.GetListItem(line, 2);

      // Store the data as a property of the data object
      data[parameter] = value;
    }

    // Closes the file
    myFile.Close();
  } catch (error) {
    Log.Error("Error reading from file: " + error);
  }

  return data;
}

```
