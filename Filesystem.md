# Device.Handle.Filesystem
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
Extract archive:
``` csharp
const string archive = "/sdcard/magisk.zip";

fs.ExtractArchive(archive);
```
Extract archive to destination directory:
``` csharp
const string archive = "/sdcard/magisk.zip";
const string dest = "/sdcard/Magisk";

fs.ExtractArchive(archive, dest);
```
Get directory content:
ItemType can be File, Directory
``` csharp
List<LsItem> items = fs.GetDirectory<LsItem>("sdcard"); // For old devices (simple struct)
```
``` csharp
List<LsLongItem> items = fs.GetDirectory<LsLongItem>("sdcard"); // For new devices (informative struct)
```
``` csharp
// Print all long items (his info)
List<LsLongItem> items = await fs.GetDirectoryAsync<LsLongItem>("sdcard");
foreach (LsLongItem item in items)
{
    Console.WriteLine($"{item}\n");
}
```
```
Name: 'test.zip'
Type: File
Full path: '/sdcard/test.zip'
Is symlink: False
Owner: root
Group: everybody
Creation date time: 02.06.2024 0:30:00
Hard links count: 1
Size: 1093182886 bytes

...
```
``` csharp
// Print all simple items (his info)
List<LsItem> items = await fs.GetDirectoryAsync<LsItem>("sdcard");
foreach (LsItem item in items)
{
    Console.WriteLine($"{item}\n");
}
```
```
Name: 'ViperFX.RE.5.7.apk'
Type: File
Full path: '/sdcard/ViperFX.RE.5.7.apk'
Is symlink: False

...
```