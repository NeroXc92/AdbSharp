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
Mount partition:
``` csharp
string partition = "system_root";

fs.MountPartition(partition);
```
``` csharp
Partition partition = Partition.System; // Auto detect system partition

fs.MountPartition(partition);
```
Mount partition to R/W or R/O:
``` csharp
string partition = "system_root";
MountOptions options = MountOptions.ReadWrite;

ExitCode exitCode = fs.MountPartition(partition, options);

if (exitCode == ExitCode.Success)
{ 
    // Success remounted to R/W
}
else
{
    // Error mount
}
```
Unmount partition:
``` csharp
Partition partition = Partition.MicroSD; // Auto detect microsd partition

fs.UnmountPartition(partition);
```
Get directory content:
ItemType can be File, Directory
``` csharp
LsItem[] items = fs.GetDirectory<LsItem>("sdcard"); // For old devices (simple struct)
```
``` csharp
LsLongItem[] items = fs.GetDirectory<LsLongItem>("sdcard"); // For new devices (informative struct)
```
``` csharp
if (items == null)
{
	// Error get directory (For example, not permissions)
	// For give superuser permissions, set device Permission = Permission.Superuser
}
else if (items.Count == 0)
{
	// Directory is empty
}
else
{
	// Success
	
	// Print all items (his info)
	foreach (LsLongItem item in items)
	{
		Console.WriteLine(item);
	}
}
```