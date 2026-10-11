# File I/O in C# for Embedded Applications

File Input/Output (I/O) allows you to read from and write to files on the device's storage. Understanding file operations is essential for storing configuration, logs, databases, and user data in embedded systems.

## What is File I/O?

File I/O is the process of reading or writing data from/to files stored on disk or device storage:
- **Readable**: Read data from a file (e.g., read log entries)
- **Writable**: Write data to a file (e.g., save configuration)
- **Read/Write**: Read and write simultaneously (if supported by filesystem)

## Basic File I/O Operations in C# Embedded Development

### Creating the File System Structure

```csharp
// Create a new directory and file if needed
string path = "data/log.txt";
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(path));

// Open a file for reading data
StreamReader reader = System.IO.File.OpenText("config.txt");       // Read text
BinaryReader binaryFile = System.IO.BinaryReader(new StreamReader);   // Read binary
StreamWriter writer = System.IO.File.Create("data.txt");           // Create new file

// Check if file exists and read its contents
if(System.IO.File.Exists("filename.txt")) {
    string content = System.IO.File.ReadAllText("filename.txt");     // Read entire file as text
    
    Console.WriteLine(content);   // Display the entire contents to output
}
```

# File I/O Operations in Embedded C# Development

| **Operation** | **Method** | **Example Use Case** |
|--------------|------------|---------------------|
| **Create New File** | `File.Create()` | Writing configuration, logs |
| **Overwrite File** | `File.OpenWrite()` | Updating saved data |
| **Append Data** | `StreamWriter.Append()` | Adding log entries sequentially |
| **Read Entire File** | `System.IO.File.ReadAllText()` | Displaying config/settings |
| **Read Binary Data** | `BinaryReader` class | Reading sensor logs |
| **Delete File** | `File.Delete()` | Removing archived data |

## Example: Writing to File and Reading Back

```csharp
// Write to file using a StreamWriter
using(streamer) {
    var writer = new StreamReader();           // Open output stream
    foreach(int value in sensorData) {
        writer.WriteLine($"TempReading: {value}");
    }
}

// Read back the entire contents of the file
string content = System.IO.File.ReadAllText("logfile.txt");

Console.WriteLine(content);                  // Print to screen/debugger
```

## Common File Operations

| **Operation** | **Code Sample** | **Purpose** |
|--------------|-----------------|-------------|
| Create new file | `File.Create("data.txt")` | Initialize a blank file for writing |
| Open existing file | `File.OpenText("file.txt")` | Read contents from file |
| Append to existing file | `File.AppendAllText()` | Add multiple lines at once |
| Write single line | `StreamWriter.WriteLine()` | Write one line with newline |
| Read entire text | `System.IO.File.ReadAllText()` | Read one file completely as string |

File I/O operations in C# provide standardized methods for reading and writing data across all types of files.
