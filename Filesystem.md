# Device.Handle.Filesystem
``` csharp
Filesystem fs = handle.Filesystem;
```
## Methods
Delete file/directory/symlink:
``` csharp
const string path = "/sdcard/Android";
ExitCode exitCode = fs.Delete(path);
```
Copy file/directory from source path to dest path:
``` csharp
const string source = "/sdcard/test.txt";
const string dest = "/sdcard/test1.txt";

ExitCode exitCode = fs.Copy(source, dest);
```
Move file/directory from source path to dest path:
``` csharp
const string source = "/sdcard/dir";
const string dest = "/sdcard/dir1";

ExitCode exitCode = fs.Move(source, dest);
```
Create directory:
``` csharp
const string dir = "/sdcard/My folder";
ExitCode exitCode = fs.CreateDirectory(dir);
```
Create file:
``` csharp
const string file = "/sdcard/Documents/Test.txt";
ExitCode exitCode = fs.CreateFile(file);
```
Check for directory exists:
``` csharp
const string dir = "/sdcard/My folder";

if (fs.DirectoryExists(dir))
{
	// Directory exists
}
else
{
	// Directory not exists
}
```
Check for file exists:
``` csharp
const string file = "/sdcard/My file.txt";

if (fs.FileExists(file))
{
	// File exists
}
else
{
	// File not exists
}
```
Check for symlink exists:
``` csharp
if (fs.SymlinkExists("/data/my_system"))
{
    // Exists
}
else
{
    // Not exists
}
```
Write text to file:
``` csharp
const string file = "/sdcard/1.txt";
const string content = "This is test";

ExitCode exitCode = fs.WriteTextToFile(file, content);
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

if (data != null)
{
	// Success read
}
else
{
	// Error read
}
```
``` csharp
const string file = "/sdcard/1.txt";
string[] data = fs.ReadLinesFromFile(file);
```
Create symlink:
``` csharp
ExitCode exitCode = fs.CreateSymlink("/system", "/data/my_system");
```
Extract archive:
``` csharp
const string archive = "/sdcard/magisk.zip";
ExitCode exitCode = fs.ExtractArchive(archive);
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
ExitCode exitCode = fs.MountPartition(partition);
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
```
Unmount partition:
``` csharp
Partition partition = Partition.MicroSD; // Auto detect microsd partition
fs.UnmountPartition(partition);
```
Check for partition mounted:
``` csharp
Partition partition = Partition.MicroSD;

if (fs.PartitionMounted(partition))
{
    // Mounted
}
else
{
    // not mounted
}
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
		Console.WriteLine("{item}\n");
	}
}
```
Get partition(s) information:
``` csharp
PartitionInfo rootInfo = fs.GetPartitionInfo(Partition.Root);
Console.WriteLine($"{rootInfo}\n");

PartitionInfo systemInfo = fs.GetPartitionInfo(Partition.SystemExt);
Console.WriteLine($"{systemInfo}\n");

PartitionInfo vendorInfo = fs.GetPartitionInfo(Partition.Vendor);
Console.WriteLine($"{vendorInfo}\n");

PartitionInfo internalStorageInfo = fs.GetPartitionInfo(Partition.InternalStorage);
Console.WriteLine($"{internalStorageInfo}\n");

PartitionInfo microsdInfo = fs.GetPartitionInfo(Partition.MicroSD);
Console.WriteLine(microsdInfo);
```
### Output
```
Root
Full path: '/'
Mounted on: '/'
Size: 921,6 M
Used: 842,6 M (91,43%)
Available: 79 M (8,57%)

SystemExt
Full path: '/system_ext'
Mounted on: '/system_ext'
Size: 477 M
Used: 388 M (81,34%)
Available: 89 M (18,66%)

Vendor
Full path: '/vendor'
Mounted on: '/vendor'
Size: 851 M
Used: 767 M (90,13%)
Available: 84 M (9,87%)

InternalStorage
Full path: '/sdcard'
Mounted on: '/storage/emulated'
Size: 102 G
Used: 20 G (19,61%)
Available: 82 G (80,39%)

MicroSD
Full path: '/storage/FDF7-F207'
Mounted on: '/storage/FDF7-F207'
Size: 117 G
Used: 20 G (17,09%)
Available: 97 G (82,91%)
```
CreateCopyTask
You can use WindowsPath, or AndroidPath
pull / push or cp auto detected
``` csharp
string source = "C:\\adb\\x.zip"; // Windows path
string source = "/sdcard/test file.zip"; // Android path

CopyTask copyTask = fs.CreateCopyTask(source, dest);
```
``` csharp
// ProgressRecieved event
copyTask.ProgressRecieved += (s, e) =>
{
    Console.WriteLine($"Copy {e.ProgressPercentage:F0}% | {e.CurrentSize.FileSizeEx()}/{e.TotalSize.FileSizeEx()} | Speed: {e.Speed.FileSizeEx()}/s");
};
```
``` csharp
// Start and wait copy progress
ExitCode exitCode = await copyTask.RunAsync();
```
### Output
```
...
Copy 6% | 12 M/207,94 M | Speed: 9,25 M/s
Copy 7% | 14 M/207,94 M | Speed: 9,25 M/s
Copy 8% | 16,5 M/207,94 M | Speed: 9,25 M/s
Copy 9% | 18,75 M/207,94 M | Speed: 9,25 M/s
Copy 10% | 21,25 M/207,94 M | Speed: 9,25 M/s
Copy 11% | 23,75 M/207,94 M | Speed: 9,25 M/s
Copy 12% | 25,62 M/207,94 M | Speed: 9,25 M/s
Copy 13% | 27,5 M/207,94 M | Speed: 9,25 M/s
Copy 14% | 29,5 M/207,94 M | Speed: 9,25 M/s
Copy 15% | 31,5 M/207,94 M | Speed: 9,25 M/s
Copy 16% | 34 M/207,94 M | Speed: 9,25 M/s
Copy 17% | 36,25 M/207,94 M | Speed: 9,25 M/s
Copy 19% | 39 M/207,94 M | Speed: 29,75 M/s
Copy 20% | 41,5 M/207,94 M | Speed: 29,75 M/s
...
```
``` csharp
// FSCurrentProgressEventArgs class

double ProgressPercentage = e.ProgressPercentage;
ulong TotalSize = e.TotalSize;
ulong CurrentSize = e.CurrentSize;
ulong Speed = e.Speed;
string DestinationPath = e.DestinationPath;
string SourcePath = e.SourcePath;
```
