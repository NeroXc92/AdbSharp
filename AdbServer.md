# Client.AdbServer
``` csharp
AdbServer server = client.Server;
```
Restart adbd with/without root permissions
``` csharp

try
{
	// restart adbd with root permissions
	server.Root = true;

	// restart adbd without root permissions
	server.Root = false;

  // Success
}
catch (AdbSharpException ex)
{
	// Error
}
```
Restart adbd listening on
``` csharp
// restart adbd listening on USB
try
{
	server.Listener = Listener.OnUsb;
  
  // Success
}
catch (AdbSharpException ex)
{
	// Error
}
```
``` csharp
// restart adbd listening on TCP on PORT
const int port = 25000;

try
{
	server.Listener = Listener.OnTcpIp;
	server.TcpPort = port;

  // Success
}
catch (AdbSharpException ex)
{
	// Error
}
```

Get server's running port
``` csharp
int port = server.Port;
```
## Methods
Start the adb server:
``` csharp
ExitCode exitCode = server.Start();

if (exitCode == ExitCode.Success)
{
    // Success
}
else
{
    // Error
}
```
Kill the adb server:
``` csharp
ExitCode exitCode = server.Kill();

if (exitCode == ExitCode.Success)
{
    // Success
}
else
{
    // Error
}
```
Reconnect all devices:
``` csharp
ExitCode exitCode = server.Reconnect();

if (exitCode == ExitCode.Success)
{
    // Success
}
else
{
    // Error
}
```
Reconnect all offline devices:
``` csharp
ExitCode exitCode = server.ReconnectOffline();

if (exitCode == ExitCode.Success)
{
    // Success
}
else
{
    // Error
}
```