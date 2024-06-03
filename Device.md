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
// Can be:

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
// Can be:

// None,
// Normal,
// Superuser
```
## Methods
Disconnect
``` csharp
device.Disconnect();
```
Connect back
``` csharp
device.Connect();
```
ToString
``` csharp
Console.WriteLine(device);
```
### Output
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