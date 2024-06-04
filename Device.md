# Device
``` csharp
Device device = devices[0];
```
Get serial number
``` csharp
string serial = device.SerialNumber;
```
Get mode
``` csharp
Mode mode = device.Mode;
// Device,
// Recovery,
// Unauthorized,
// Unknown,
// Offline,
// Sideload
```
Get model
``` csharp
string model = device.Model;
```
Get product
``` csharp
string product = device.Product;
```
Get codename
``` csharp
string codename = device.Codename;
```
Get transport ID
``` csharp
string transportId = device.TransportId;
```
Set superuser mode
``` csharp
device.Permission = Permission.Superuser;
// None,
// Normal,
// Superuser
```
Set initial threads count
``` csharp
device.InitialThreads = 2;
```
Set maximum threads count (threads will increase gradually to this amount)
``` csharp
device.MaxThreads = 7;
```
Get [Handle](https://github.com/NeroXc92/AdbSharp/blob/main/Handle.md)
``` csharp
Handle handle = device.Handle;
```
## Methods
Disconnect
``` csharp
ExitCode exitCode = device.Disconnect();

if (exitCode == ExitCode.Success)
{
    // Success
}
else
{
    // Error
}
```
Connect back
``` csharp
ExitCode exitCode = device.Connect();

if (exitCode == ExitCode.Success)
{
    // Success
}
else
{
    // Error
}
```
ToString
``` csharp
Console.WriteLine(device);
```
```
Serial number: 5793298f
Mode: Device
Model: Redmi 10C
Codename: fog
Product: lineage_fog
Transport id: 1
Permission: Superuser
Threads count: 1
Max threads count: 4
Threads incrase timeout: 0 ms
```