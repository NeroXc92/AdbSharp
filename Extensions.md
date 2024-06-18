# Extensions
Useful extensions for AdbSharp
``` csharp
using AdbSharp.Extensions;
```
## ulong
### FileSizeEx()
Format ulong bytes to readable GB / MB / KB / B:
``` csharp
// Usage:
public static string[] sizes = ["Б", "КБ", "МБ", "ГБ", "ТБ"];

ulong bytes = 218038272;

string str = bytes.FileSizeEx(sizes);
// Output: 207,94 M
```
## string
### DelimiterValue()
Parse delimiter value(s) from string
``` csharp
// Usage:
string toParse = "Battery: 100    Files: 150    Data: aaa_bbb_ccc";

string result = toParse.DelimiterValue("Battery: ");
// Output: 100
```
``` csharp
Dictionary<string, string> results = toParse.DelimiterValue("Battery: ", 
															"Files: ", 
															"Data: ");
// Output:
// "Battery: " : "100"
// "Files: " : "150"
// "Data: " : "aaa_bbb_ccc"
```