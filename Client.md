# Client
``` csharp
const string path_to_adb = @"C:\adb\adb.exe";
Client client = new(path_to_adb);
```
Change path to adb.exe:
``` csharp
client.AdbPath = @"D:\tools\adb.exe";
```
## Methods
Get actual devices list:
``` csharp
List<Device> devices = client.GetDevices();
```
Get device by serial:
``` csharp
string serial_number = "your_serial";

Device device1 = devices.Find(x => x.SerialNumber == serial_number)!;
```
Get device by model:
``` csharp
string model = "Redmi 10C";

Device device1 = devices.Find(x => x.Model == model)!;
```
``` csharp
if (device1 != null)
{
    // device found
}
else
{
    // device not found
}
```
Connect to remote Wi-Fi device using IP and port:
``` csharp
string ip = "192.168.0.5";
int port = 65001;

client.Connect(ip, port);
```
ToString
``` csharp
Console.WriteLine(client);
```
```
Adb path: 'C:\adb\adb.exe'
Adb directory: 'C:\adb'
MAX_PATH_SYMBOLS: 31400
```
