# 5.2.FileI/O

## Overview
File I/O in C#.NET enables persistence of program data to disk (JSON config files, log entries, database exports) via .NET's Stream/File API classes—critical for OOP applications needing to store state between execution cycles rather than relying solely on in-memory objects. Proper file handling patterns prevent data loss on crash and ensure consistent access when GUI processes user input.

### Key Definitions
| Term | Definition |
|------|------------|
| **File Stream** | .NET abstraction layer for reading/writing data through file system (e.g., `FileStream`, `BinaryReader`/`BinaryWriter`) |
| **File Mode** | Opens file with specified access rights (`OpenMode.OpenRead` vs `OpenMode.Append`)—determines if existing content is preserved or overwritten in OOP persistence logic |
| **File Path Structure** | Organized directory hierarchy where each file stores specific data type (e.g., configuration files, log entries) for maintainable code readability in .NET projects |

### Core Concepts
1. **Read/Write Permission Handling**: Files may require read-only permissions (config data), append-only mode (logs), or over-write scenarios depending on application state management needs in OOP design patterns
2. **Cross-Platform Compatibility**: C# uses unified `System.IO` API classes for Windows/Linux/macOS file systems—single code pattern works across all supported .NET runtime platforms
3. **Error Recovery** | Stream/File operations may fail due to missing directories, permission errors, or disk full conditions—requires try-catch patterns in OOP exception handlers

### Main Content

#### File I/O Implementation Patterns (.NET C# Context)

```csharp
// Visual Studio generated code for file I/O methods in .NET OOP context
{
    // FileReadWrite class encapsulates read/write operations for persistent data storage  
    public class FileReadWrite {
        private int _bufferSize = 1024; // Common buffer size used across all streaming operations (OOP pattern)

        // Constructor sets up file stream properties and encoding preferences (e.g., UTF-8 via Encoding.Bytes in .NET API)  
        public FileReadWrite(string filePath, FileMode mode, Encoding charset = default) {
            var stream = CreateFileStream(filePath); 
        }
    }

    // StreamFile class manages binary data conversion between text format and byte-level storage (OOP abstraction)  
}
```

### Examples and Applications

#### Example 1: File Read/Write for Persistent Configuration (.NET C# File Pattern)

| Feature | Code Implementation | Effect on OAP Application |
|---------|--------------------|--------------------------|
| **File Mode** | `StreamMode.Open` (overwrite) vs `OpenOrCreate` (create if not exists) for initial data setup | Ensures configuration persists across GUI app restarts without manual intervention |
| **Encoding Selection** | UTF-8 encoding ensures cross-platform character set compatibility when storing JSON configs to files in .NET OOP patterns | Prevents file corruption from locale-specific character encoding issues on Windows/Linux/macOS systems |

```csharp
// File: FileIOMethods.cs (Visual Studio auto-generated template structure for C#.NET file I/O operations in OAP applications)
{
    class ConfigurationFileReadWrite {
        // Constructor creates new file stream and handles read/write permissions via try-catch patterns  
        public Stream CreateStream(string fileName, FileMode openMode) => 
            Stream.Open(fileName, FileMode.OpenOrCreate);

        // Method reads all bytes from configuration file into byte array for OOP state loading (e.g., loading JSON from file in GUI app)  
        public byte[] ReadAllFromConfigFile(FileSystemPath filePath) => 
            BinaryReader.ReadAllBytes(filePath); 

        // Event handler triggers when new file content is written to disk via stream operations  
    }
    
    // File Write method: writes bytes to file through output stream channel (e.g., GUI export data to JSON text file)  
}

// File: ConfigurationIO.cs (Visual Studio generated code for persistent configuration files in OOP design pattern)
{
    class ConfigFileReadWrite {
        public byte[] ReadAllBytes(string filePath, Encoding charset = Encoding.UTF8) => 
            FileStream.ReadAllText(filePath); 

        public void WriteToConfig(string fileName, byte[] data) => 
            Stream.WriteLine(data);
    }
}
```

### Examples and Application Patterns (.NET File Persistence in OOP Design)

| Feature | Code Structure | OAP Use Case |
|---------|---------------|--------------|
| **JSON Config** | Uses `System.Text.Json` to serialize/deserialize objects (e.g., GUI app settings) into compact text files across platforms | Stores user-selected preferences, connection parameters in cross-platform apps |
| **Log Entry** | Writes timestamp + message to file using `Stream.WriteLine()` pattern; timestamps maintain chronological order for debugging purposes in OAP applications | Creates persistent audit trail of GUI operations and GUI state changes over time |
| **File Locking** | Uses lock-based synchronization (e.g., mutex objects) to prevent multiple processes from accessing same config file simultaneously | Prevents concurrent read/write conflicts when GUI app runs in multiple threads or user sessions |

### Examples and Applications

#### Example 2: Log File Writing via File Stream (.NET C# OAP Pattern)

```csharp
// File: LoggingFileIOMethods.cs (Visual Studio auto-generated template for file logging using .NET APIs in OOP contexts)
{
    class LoggerStream {
        // StreamWrite method appends timestamps and messages to .NET log file (append-only mode by default)  
        public void AppendLogEntry(string timestamp, string msg) => 
            File.WriteLine($"[{timestamp}] {msg}", "logs/");

        // Event handler triggers callback when GUI displays error via .NET exception handling framework in OOP pattern  
    }
}

// File: LogFileIOMethods.cs (Visual Studio auto-generated template for persistent logging files using JSON/text format in C#.net)
{
    class Logger {
        public void WriteLog(string timestamp, string msg) => 
            Console.WriteLine($"[{timestamp}] {msg}"); 

        // Append mode ensures new logs don't overwrite old entries in .NET GUI app  
    }
    
    // Example: GUI displays error via stream callback (e.g., exception caught in OOP try-catch pattern)  
}

// File: ErrorLogging.cs (Visual Studio auto-generated template for capturing and writing errors to log files using C# .NET runtime APIs)
{
    class ErrorHandler {
        public void OnError(string errorMsg, StackTrace frameCount = 0) => 
            Console.WriteLine($"Error: {errorMsg}. Stack trace: {frameCount}"); // GUI displays error via callback

        private void TryCATCH(string msg) {
            try { /* operation code */ } catch (Exception e) => 
                OnError(e.Message, e.StackTrace.Length); // Writes to .NET log file via System.IO API  
        }
    }
}

### Important Notes & Reminders

- **Directory Creation**: Files must exist in existing directories; create parent dirs via `System.IO` utilities if missing for OOP apps storing config/log data across platforms
- **File Permissions**: Windows may require admin privileges to write to protected system folders (.NET uses OS-specific permission checks—handle gracefully)
- **Encoding Consistency**: UTF-8 is safest .NET format; always specify encoding explicitly when reading/writing files in cross-platform OAP GUI apps
- **Backup Recovery** | Store multiple versions of config files (e.g., backup + current) to enable OOP applications to recover from corrupted/overwritten data on .NET runtime

## Quiz / Review Questions
1. What happens when you try to read a file that doesn't yet exist using `Open` (.NET `FileStream` API)?
2. How does appending mode (`OpenMode.Append`) differ from regular over-write for log files in OAP applications?
3. Why might JSON serialization be preferred over plain text format when storing configuration data in .NET C# file I/O operations?
4. What is the recommended pattern for closing (disposing of) a file stream after reading/writing data to ensure proper cleanup in your OOP GUI app?.

---
**Related Topics:** [[E230_OOPr]] [[#Reference_StreamingNetworkProtocol]] [[#Reference_ExceptionHandlingInCSharp]]
