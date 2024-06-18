# Device.Handle.Shell
Executes in exec-out or shell any command.
``` csharp
Shell shell = handle.Shell;
```
## Methods
Run:
``` csharp
const string command = "echo Hello world";
ShellResult result = shell.Run(command);
```
``` csharp
// Print output
Console.WriteLine(result);
```
``` csharp
// Check for success execution
if (result.ExitCode == 0) // or ExitCode.Success
{
	// Success
}
else if (result.ExitCode == 1) // or ExitCode.Error
{
	// Error
}
else
{
	// if (result.ExitCode == 2) // or ExitCode.None 
	// Execution, exit code not exist
}
```
Run use ShellStartInfo:
``` csharp
ShellStartInfo info = new()
{ 
    FileName = "echo",
    Arguments = "Hello world",
    Permission = Permission.Superuser
};

ShellResult result = shell.Run(info);
```
CreateProcess (ShellProcess):
``` csharp
ShellProcess process = shell.CreateProcess();
process.StartInfo.FileName = "echo";
process.StartInfo.Arguments = "Hello world";
process.StartInfo.Permission = Permission.Normal;
process.StartInfo.UseExecOut = false;
```
``` csharp
// Run process
process.Run();
```
``` csharp
// Async read output in realtime
process.OutputDataRecieved += (s, e) =>
{
    string line = e.Data;
    Console.WriteLine(line);
};
```
``` csharp
// Read output to end (not need use WaitForExit)
string data = process.Output.ReadToEnd();
```
``` csharp
// Wait for exit
process.WaitForExit();
```
``` csharp
// Force kill the process
process.Kill();
```
``` csharp
// Check for process is running
bool isRunning = !process.HasExited;
```
``` csharp
// Check for success execution
ExitCode exitcode = process.ExitCode;
```
``` csharp
// Close and dispose ShellProcess
process.Dispose();
```
CreateSession (ShellSession):
``` csharp
ShellSession shellSession = device1.Handle.Shell.CreateSession();
shellSession.OutputDataRecieved += (s, e) =>
{
    Console.WriteLine(e.Data);
};
shellSession.Start();
```
``` csharp
// For example emulate adb shell
while (true)
{
    string command = Console.ReadLine()!;
    
    ExitCode exitCode = await shellSession.RunAsync(command);
    
    // Check for success execution
    if (exitCode == ExitCode.Success)
    {
        // Success
    }
    else
    {
        // Error
    }
}
```
``` csharp
// For example, run multiple commands
_ = await shellSession.RunAsync("echo Hello World!");
_ = await shellSession.RunAsync("cd system");
_ = await shellSession.RunAsync("cd app");
_ = await shellSession.RunAsync("ls");
```
``` csharp
// Close and dispose ShellSession
shellSession.Dispose();
```
