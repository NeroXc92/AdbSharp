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
Check device for rooted
``` csharp
device.Permission = Permission.Auto;

if (device.Permission == Permission.Superuser)
{
    // Rooted
}
else
{
    // Not rooted
}
```