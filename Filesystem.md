# Device.Handle.Filesystem
``` csharp
Filesystem fs = handle.Filesystem;
```
## Methods
Copy file/directory from source path to dest path:
``` csharp
const string source = "/sdcard/test.txt";
const string dest = "/sdcard/test1.txt";

ExitCode exitCode = fs.Copy(source, dest);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
```
Move file/directory from source path to dest path:
``` csharp
const string source = "/sdcard/dir";
const string dest = "/sdcard/dir1";

ExitCode exitCode = fs.Move(source, dest);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
```
Create directory:
``` csharp
const string dir = "/sdcard/My folder";

ExitCode exitCode = fs.CreateDirectory(dir);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
```
Create file:
``` csharp
const string file = "/sdcard/Documents/Test.txt";

ExitCode exitCode = fs.CreateFile(file);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
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
Write text to file:
``` csharp
const string file = "/sdcard/1.txt";
const string content = "This is test";

ExitCode exitCode = fs.WriteTextToFile(file, content);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
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
Push file/directory from PC to device:
``` csharp
const string source = @"C:\adb\test.img";
const string dest = "/sdcard/";

ExitCode exitCode = fs.Push(source, dest);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
```
Pull file/directory from device to PC:
``` csharp
const string source = "/sdcard/test.img";
const string dest = @"C:\adb";

ExitCode exitCode = fs.Pull(source, dest);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
```
Extract archive:
``` csharp
const string archive = "/sdcard/magisk.zip";

ExitCode exitCode = fs.ExtractArchive(archive);

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
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

if (exitCode == ExitCode.Success)
{
	// Success
}
else
{
	// Error
}
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
Get partition information:
``` csharp
DfPartition root = DfPartition.Root;
DfPartition internalStorage = DfPartition.InternalStorage;
DfPartition microsd = DfPartition.MicroSD;

PartitionInfo rootInfo = await fs.GetPartitionInfoAsync(root);
PartitionInfo internalStorageInfo = await fs.GetPartitionInfoAsync(internalStorage);
PartitionInfo microsdInfo = await fs.GetPartitionInfoAsync(microsd);

if (rootInfo == null && internalStorageInfo == null && microsdInfo == null)
{
	// Error get partition info
}
else
{
	Console.WriteLine($"{rootInfo}\n");
	Console.WriteLine($"{internalStorageInfo}\n");
	Console.WriteLine(microsdInfo);
}
```
### Output
```
Partition: Root
Full path: '/'
Mounted on: '/'
Size: 1028653056 bytes
Used: 927989760 bytes
Available: 82837504 bytes
Using percentage: 92%

Partition: InternalStorage 
Full path: '/sdcard'
Mounted on: '/storage/emulated'
Size: 109521666048 bytes
Used: 50465865728 bytes
Available: 59055800320 bytes
Using percentage: 46%

Partition: MicroSD
Full path: '/storage/FDF7-F207'
Mounted on: '/storage/FDF7-F207'
Size: 125627793408 bytes
Used: 18253611008 bytes
Available: 107374182400 bytes
Using percentage: 15%
```