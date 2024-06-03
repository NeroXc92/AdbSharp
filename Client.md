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
Device[] devices = client.GetDevices();
```
``` csharp
Device[] devices = await client.GetDevicesAsync();
```
Connect to remote Wi-Fi device using IP and port:
``` csharp
string ip = "192.168.0.5";
int port = 65001;

ExitCode exitCode = client.Connect(ip, port);
```
``` csharp
ExitCode exitCode = await client.ConnectAsync(ip, port);
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
