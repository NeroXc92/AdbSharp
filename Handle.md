# Device.Handle
``` csharp
Handle handle = device.Handle;
```
Get [Shell](https://github.com/NeroXc92/AdbSharp/blob/main/Shell.md) handle
``` csharp
Shell shell = handle.Shell;
```
Get [Filesystem](https://github.com/NeroXc92/AdbSharp/blob/main/Filesystem.md) handle
``` csharp
Filesystem fs = handle.Filesystem;
```
Get [Media](https://github.com/NeroXc92/AdbSharp/blob/main/Media.md) handle
``` csharp
Media media = handle.Media;
```
## Methods
``` csharp
if (handle.CheckPermission() == Permission.Superuser)
{
	// Device rooted
}
else
{
	// Device non rooted
}
```