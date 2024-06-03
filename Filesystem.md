# File system
``` csharp
Filesystem fs = handle.Filesystem;
```
## Methods
Copy file/directory from source path to dest path:
``` csharp
const string source = "/sdcard/test.txt";
const string dest = "/sdcard/test1.txt";

fs.Copy(source, dest);
```
Move file/directory from source path to dest path:
``` csharp
const string source = "/sdcard/dir";
const string dest = "/sdcard/dir1";

fs.Move(source, dest);
```
Create directory:
``` csharp
const string dir = "/sdcard/My folder";

fs.CreateDirectory(dir);
```
Create file:
``` csharp
const string file = "/sdcard/Documents/Test.txt";

fs.CreateFile(file);
```
Check for directory exists:
``` csharp
const string dir = "/sdcard/My folder";

if (fs.DirectoryExists(dir))
{
	
}
```
Check for file exists:
``` csharp
const string file = "/sdcard/My file.txt";

if (fs.FileExists(file))
{
	
}
```
Write text to file:
``` csharp
const string file = "/sdcard/1.txt";
const string content = "This is test";

fs.WriteTextToFile(file, content);
```
``` csharp
const string file = "/sdcard/1.txt";
const List<string> lines = 
[
	"Hello",
	"World"
];

fs.WriteLinesToFile(file, lines);
```
Read text from file:
``` csharp
const string file = "/sdcard/1.txt";

string data = fs.ReadTextFromFile(file);
```
``` csharp
const string file = "/sdcard/1.txt";

string[] data = fs.ReadLinesFromFile(file);
```
Push file/directory from PC to device:
``` csharp
const string source = @"C:\adb\test.img";
const string dest = "/sdcard/";

fs.Push(source, dest);
```
Pull file/directory from device to PC:
``` csharp
const string source = "/sdcard/test.img";
const string dest = @"C:\adb";

fs.Pull(source, dest);
```
Get directory content:
``` csharp
// For old devices (simple struct)
LsItem[] items = fs.GetDirectory<LsItem>("sdcard");
LsItem item = items[0];

// string item.FullPath
// string item.Name
// bool item.IsSymlink
// ItemType item.Type
```
``` csharp
// For new devices (very informative struct)
LsLongItem[] items = fs.GetDirectory<LsLongItem>("sdcard");
LsLongItem item = items[0];

// string FullPath
// string Name
// bool IsSymlink
// Permissions Owners
// Permissions Groups 
// Permissions Others 
// string Owner
// string Group
// DateTime CreationDateTime
// int HardLinksCount
// ulong Size
// ItemType Type

```
``` csharp
// ItemType can be

// File
// Directory
```