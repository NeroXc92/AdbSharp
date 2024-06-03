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
### Output
```
Adb path: 'C:\adb\adb.exe'
Adb directory: 'C:\adb'
MAX_PATH_SYMBOLS: 31400
```