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
CreateProcess:
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