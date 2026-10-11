# Input and Output (I/O) Streams in C# for Embedded Applications

Streams are a unified interface to various devices, allowing you to read from or write to any data source through a consistent pattern. They're fundamental to embedded C# development.

## What is an I/O Stream?

Think of streams as "pipes" that transfer data one byte at a time:
- **Input Stream**: Reads character-by-character (or bytes) from file, keyboard, serial port
- **Output Stream**: Writes characters/bytes to file, display, serial port
- **Bidirectional Streams**: Read and write both simultaneously

```csharp
// Open a file for reading text data
StreamReader reader = File.Open("data.txt", FileMode.Open);

// Or open for writing new content
StreamWriter writer = File.Open("output.txt", FileMode.Create);

// Or use stream over network, serial port, etc.
NetworkStream stream = new NetworkStream(streamAddress);
BinaryReader readerStream = new BinaryReader(stream);
```

## Key Stream Types in C# Embedded Development

| **Type** | **Example** | **Usage** |
|----------|-------------|-----------|
| FileReader/FileWriter | `System.IO` classes for files | Reading/writing from/to file system |
| Network stream | `NetworkStream` class | Serial port, TCP/UDP communication |
| Stream over embedded devices | `System.IO.StreamDevice` | Device I/O operations |

## Key Methods in Input Streams

```csharp
// Open a text file for reading and return as stream
StreamReader reader = File.OpenText("filename.txt");

// Read data from input stream
string text = reader.ReadLine();       // Read entire line
int bytesAvailable = reader.BytesRemaining;  // Bytes still available to read

// Convert binary data to text or vice versa
string binString = System.Text.Encoding.UTF8.GetString(rawBytes);
byte[] utf8Bytes = System.Text.Encoding.UTF8.GetBytes(stringToConvert);

// Write characters or bytes to destination stream
writer.Write("Hello");                // Writes a single string to file
writer.Write(byteArray);              // Writes entire array as binary data
```

## Key Methods in Output Streams

```csharp
// Open a text file for writing
StreamWriter writer = File.OpenWrite("output.txt");

// Write various types of data to the stream using streams
writer.WriteLine("Line 1");           // Add newline at end of line
writer.Write("Line 2                ");    // No newline appended

// Close the output stream (disposes resources)
writer.Close();

// Write string or bytes to the specified binary input stream
writer.Write(binData);
```

Streams in C# provide standardized interfaces for reading and writing across all types of devices. Understanding how they work is crucial for embedded developers managing multiple data sources simultaneously.
