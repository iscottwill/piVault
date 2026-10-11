# The Destructor in C# for Embedded Applications

A **destructor** (called a finalizer in some .NET contexts) runs automatically when an object's reference count drops to zero. It performs cleanup tasks to free resources allocated during the object's lifetime.

## What is a Destructor?

A destructor is:
- Special method that runs when an object will no longer be used/created
- Syntax: `~ClassName()`, also known as a **finalizer** in C# (.NET)
- Not part of the standard constructor pattern (doesn't take parameters)
- Used to clean up resources allocated during object lifetime

## Why Use Destructors/Destructors in C# Embedded Systems?

| **Reason** | **Explanation** |
|-----------|-----------------|
| **Free Memory Allocated During Object Lifetime** | Clean up heap memory used by internal objects or buffers |
| **Release Hardware Resources** | Close file handles, close serial ports, free USB connections |
| **Prevent Resource Leaks** | Ensures resources get freed when the object is no longer in use |

## Basic Destructor Syntax and Usage in C# Embedded Development

```csharp
// Example: A class that reads from a sensor using external memory/resources
public sealed class SensorReader {
    private int _bufferSize = 1024;       // Buffer size used during reading (internal storage)
    
    public SensorReader() {              // Constructor – allocates internal storage!
        this._bufferSize = GetDefaultBufferSize();   // Set default value
        
        // Allocate memory for buffer (heap operation)
        this.buffer = System.Array.Empty<byte>(_bufferSize);  // Create internal buffer
    }
    
    private int GetDefaultBufferSize() {                    // Returns default buffer size
        return 1024;              // 1KB buffer by default
    }
    
    ~SensorReader() {           // Destructor - runs when object destroyed!
        // Free the memory used during lifetime (internal variable cleanup)
        System.GC.SuppressFinalize(this);         // Optional: prevent GC from finalizing
        
        Console.WriteLine("Cleaning up SensorReader...");   // Log message
        this.buffer.Dispose();                // Clean up any allocated resources
        
        // If object is no longer referenced, destructor automatically runs!
    }
    
    public void Read() {          // Main method for reading data (uses internal storage)
        // Access to internal buffer via private field (_bufferSize and buffer)
        this.buffer[0] = GetNextByte();     // Read data from hardware into buffer
        
        Console.WriteLine($"Read: {this.buffer.ToArray()}");   // Use stored value here
    }
}
```

## When Does the Destructor Automatically Run in C#?

The destructor runs when:
1. **Last reference to object is lost** → No more objects are using it and no longer hold references!
2. **Object goes out of scope** → Variable holding `SensorReader s = SensorReader()` exits execution!
3. **Garbage collector collects it** → Memory reclaimed by `.NET` system

Example: Object destroyed before going out of scope (explicit or automatic).

## Example: Destroying Objects and Running Destructor Code

```csharp
// Create object instance at startup
SensorReader s1 = new SensorReader();    // Constructor runs, memory allocated

// Use the object for some operations
s1.Read();                 // Read sensor data into internal buffer/memory
        
// When s1 goes out of scope (e.g., variable assignment removed from context),
// destructor automatically calls ~SensorReader().

// Destructor code runs: frees internal buffer/allocated memory!
// This happens when the last reference to object is gone.
```

## The Destructor in C# vs Finalizer Pattern

- In .NET/C#, destructors are **finalizers** - they run when the GC thinks it's safe to destroy an object instance
- Unlike C++, there's no mandatory destructor requirement in C# (but finalizers can help with cleanup)
- For embedded systems using .NET: use **IDisposable** pattern if managing resources manually (e.g., `using` statement)

## Best Practices for Deconstructing Objects in Embedded C# Development

1. **Use `IDisposable` Interface for Manual Resource Cleanup**: Explicitly dispose resources before they're garbage collector'ed
2. **Always Close File Handles/Connections in Destructor or Using Statements**: Prevent leaks when objects go out of scope
3. **Avoid Finalizers When Possible** (unless necessary): They delay cleanup; prefer `try-finally` blocks!

## Example: Destructor and Try-Finally Pattern

```csharp
public sealed class SensorReader {
    private bool _disposed = false;              // Track if object was already disposed
    
    ~SensorReader() {                             // Finalizer for when GC needs to clean up resources
        if (!_isDisposed) {
            Dispose(true);                  // Run dispose code when possible
        
            this._isDisposed = true;        // Mark as cleaned up for finalization
        }
    }
    
    // Explicit disposal method (manual cleanup before GC can free memory)
    public void Dispose() {
        if (!_disposed) {
            ClearBuffer();                 // Free internal buffer (memory on heap)
            _disposed = true;              // Mark cleanup complete
            
            GC.SuppressFinalize(this);           // Prevent destructor from running again
        }
    }
    
    private void ClearBuffer() {                        // Clean up allocated resources
        System.Array.Clear(this.buffer, 0, bufferLength);        // Clear internal array
        
        Console.WriteLine("SensorReader buffer cleaned up");      // Log message
    }
}

// Using using statement to ensure proper cleanup!
using (SReader reader = new SensorReader()) {       // Uses `try-finally` pattern internally
    reader.Read();               // Use the object
    
    // When block ends, destructor or Dispose is automatically called
    // No need to manually call `reader.Dispose()` in most cases
}
```

The destructor (via finalizer pattern + IDisposal) ensures resources get cleaned up properly and prevents resource leaks during embedded C# application lifetime!
