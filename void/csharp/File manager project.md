`For learning purposes`

While learning c# _(which is very similar to java)_ I had the idea of making a file manager because i came across the namespace `System.IO`. 

To list or enumerate directories we would have many choices and we have to make the choice based on our needs, for example, if we do need to list the top level directories a suitable choice would be the function `Directory.EnumerateDirectories`. 

Other options : 
- `Directory.EnumerateFiles`

> Both functions have an overload that accepts a parameter to specify the search pattern files and directories should match, also, they have another overload that accepts a parameter to indicate whether to recursively travers a specified folder and all of it's subfolders. 

Example : 
```cs
IEnumerable<string> allFilesInAllFolders = Directory.EnumerateFiles("desktop", "*.txt", SearchOption.AllDirectories);
```

