# Get starting
- Download Android Platform Tools by Google: https://dl.google.com/android/repository/platform-tools-latest-windows.zip
- Extract to any location. I use C:\adb

## In C# code:
Create client:
````
Client client = new("C:\\adb\\adb.exe"); // Use adb.exe path
````
Get actual devices list:
````
Device[] devices = await client.GetDevicesAsync();
````
For example, print all devices to console
```` 
foreach (Device device in devices)
{
    Console.WriteLine($"{device}\n");
}
````
```` 
// Output

// Serial number: 5793298f
// Mode: Device
// Model: Redmi 10C
// Codename: fog
// Product: lineage_fog
// Transport id: 1
// Superuser mode: False
// Threads count: 1
// Max threads count: 4
// Threads incrase timeout: 0 ms
````
## Device.Handle
Device object has Handle. It is needed to control the device
```` 
Handle handle = device.Handle;
````