# Client.AdbServer
``` csharp
AdbServer server = client.Server;
```
Restart adbd with/without root permissions
``` csharp
// restart adbd with root permissions
server.Root = true;

// restart adbd without root permissions
server.Root = false;
```
Restart adbd listening on
``` csharp
// restart adbd listening on USB
server.Listener = Listener.OnUsb;

// restart adbd listening on TCP on PORT
const int port = 25000;

server.Listener = Listener.OnTcpIp;
server.TcpPort = port;
```
Get server's running port
``` csharp
int port = server.Port;
```
## Methods
Start the adb server:
``` csharp
server.Start();
```
Kill the adb server:
``` csharp
server.Kill();
```
Reconnect all devices:
``` csharp
server.Reconnect();
```
Reconnect all offline devices:
``` csharp
server.ReconnectOffline();
```
