# Get Starting
- Download Android Platform Tools by Google: https://dl.google.com/android/repository/platform-tools-latest-windows.zip
- Extract to any location. I use C:\adb

## In C# Code:
Add usings:
```csharp
using AdbSharp;
using AdbSharp.Devices;
using AdbSharp.Server;
using AdbSharp.Structs;
using AdbSharp.Enums;
using AdbSharp.Extensions;
using AdbSharp.Interfaces;
```

Create client:
```csharp
Client client = new(@"C:\adb\adb.exe"); // Use adb.exe path
```

Get actual devices list:
```csharp
Device[] devices = await client.GetDevicesAsync();
```

For example, print all devices to console
```csharp
foreach (Device device in devices)
{
    Console.WriteLine($"{device}\n");
}
```

### Output
```
Serial number: 5793298f
Mode: Device
Model: Redmi 10C
Codename: fog
Product: lineage_fog
Transport id: 1
Superuser mode: False
Threads count: 1
Max threads count: 4
Threads incrase timeout: 0 ms
```

## Device.Handle
Device object has Handle. It is needed to control the device
```csharp
Handle handle = device.Handle;
```