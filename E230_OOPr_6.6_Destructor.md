# 6.6.Destructor

## Overview
The destructor (.NET finalizer) in C#.NET is called automatically by .NET runtime when an object becomes unreachable—primarily for releasing unmanaged resources (file handles, network sockets). Unlike constructors, destructors don't take parameters and run during garbage collection (GC)—ensuring proper cleanup across GUI app lifecycle in OAP designs that require resource management patterns.

### Key Definitions
| Term | Definition |
|------|------------|
| **Destructor** | `.NET` finalizer method (overridden virtual destructor: `~ClassName()` or `final: protected virtual`—runs when object becomes unreachable via GC pattern across project boundaries) |
| **Unmanaged Resources** | Memory handles not automatically freed by .NET runtime (.e.g., file streams, network sockets); require explicit cleanup in destructors for OAP GUI app patterns to prevent leaks across projects |
| **Automatic Cleanup** | .NET runtime triggers destructor when no references remain (GC pattern)—handles object lifecycle without manual `delete` in C#.NET runtime behavior differs from manual memory management |

### Core Concepts
1. **RAII Pattern**: Destructor releases acquired resources after object destroyed—similar to C++ RAII but with .NET's automatic GC for cleanup across project boundaries in OAP designs; ensures zero state on app termination
2. **Garbage Collection** | Unmanaged resources (.e.g., embedded device file handles) require manual release via destructor—if not cleaned up during app shutdown, may cause memory leaks in OAP GUI apps across projects  
3. **Virtual Method Dispatch** | Destructor is virtual (can be overridden by derived classes)—ensures proper cleanup chain for subclass objects created via OOP inheritance patterns in .NET IDE runtime

### Main Content

#### Destructor vs Constructor Functionality (.NET C# Runtime Pattern)

```csharp
// Visual Studio generated code for destructor/finalizer pattern in .NET context
{
    public class EmbeddedResource {
        // Encapsulated internal state—file handles managed through property access patterns across GUI app projects  
        private FileStream _fileHandle = null; 

        // Constructor acquires resources (open file handle to embedded device) 
        public EmbeddedResource(string embeddedFileName) => 
            _fileHandle = new FileStream(embeddedFileName, FileMode.Open);

        // Destructor releases resources automatically via .NET GC pattern across project boundaries when object becomes unreachable for OAP GUI apps  
    }
}

// File: DestructorPattern.cs (Visual Studio auto-generated template structure demonstrating destructor pattern in C#.NET runtime context)
{
    public class ResourceManager {
        private FileStream _fileHandle; // Unmanaged resource requires cleanup via destructors in OAP designs across project boundaries

        public ResourceManager(string embeddedPath) { 
            Console.WriteLine("Constructor: Acquiring file handle for embedded device"); 
            _fileHandle = new FileStream(embeddedPath, FileMode.Open); 

            // Destructor will run when object becomes unreachable via .NET GC pattern (no references remain) in OAP GUI apps
        }

        ~ResourceManager() { // Destructor releases unmanaged resources automatically without manual delete needed across project boundaries  
            Console.WriteLine("Destructor: Closing file handle for embedded device"); 
            if (_fileHandle != null) { _fileHandle.Close(); GC.SuppressFinalize(this); }; 
        }
    }
}
```

#### Destructor Runtime Behavior (.NET C# Pattern)

| Feature | Destructor Behavior in OAP GUI Apps | .NET Runtime Impact Across Projects |
|---------|-------------------------------------|------------------------------------|
| **Invocation** | `.NET` GC calls destructor when object becomes unreachable (no more references); cleanup occurs even after constructor exception throws across project boundaries in OAP designs | Automatic execution—no manual `delete` keyword needed for memory management (C# vs C++ differs; .NET handles memory automatically in OAP patterns)  
| **Exception Safety** | Destructor runs after constructor—if constructor threw, `_internalReading` may never be assigned yet destructor cleans up anyway across GUI projects designed with RAII patterns in OAP code review cycles | Guarantees cleanup even if constructor failed (.e.g., file opened but read failed—GC ensures close still executed via virtual method dispatch pattern across project boundaries)  
| **Memory Overhead** | `.NET` runtime allocates minimal overhead per object for destructor tracking (metadata structure in heap); GC scans objects periodically to find unreferenced ones with finalizers for OAP GUI apps using resource management patterns across project boundaries | Finalizers may delay GC slightly—`.NET` prioritizes other cleanup tasks first; acceptable trade-off for reliable unmanaged resource cleanup in .NET IDE cycles  
| **Override Pattern** | Derived classes override destructor (virtual method inheritance chain)—ensures proper cleanup order (base class closes after derived) via OAP design patterns (.NET runtime executes from innermost to outermost for virtual methods like destructors across project boundaries) | Child objects cleaned up first (derived → base)—`.NET` follows correct destruction order in runtime cycles  

### Examples and Applications

#### Example 1: Destructor Usage Patterns (.NET C# Runtime Behavior)

```csharp
// File: DestructorUsagePatterns.cs (Visual Studio auto-generated template demonstrating destructor implementation patterns across OAP GUI app designs in .NET context)
{
    // Pattern 1: Auto-dispose unmanaged resources via destructor
    class EmbeddedFileHandle {
        private FileStream _stream = null; 

        public EmbeddedFileHandle(string embeddedPath) => 
            _stream = new FileStream(embeddedPath);

        ~EmbeddedFileHandle() { 
            Console.WriteLine("Destructor: Closing file handle (unmanaged resource cleanup via .NET GC across project boundaries)"); 
            if (_stream != null) { 
                _stream.Close(); 
                // Suppress finalizer (optional—prevents further cleanup calls if object reused in OAP design patterns for memory-efficient GUI apps)  
                GC.SuppressFinalize(this); 
            }
        }
    }

    // Pattern 2: Explicit disposal via IDisposable pattern (preferred over destructor for .NET 8+ designs across projects)
}
```

### Examples and Applications

#### Example 2: RAII vs Destructor Comparison (.NET Runtime Context)

| Aspect | Destructor (Finalizer) Pattern | IDispose Pattern (.NET 8+ GUI App Design) | OAP Design Impact |
|--------|-------------------------------|-------------------------------------------|-------------------|
| **Invocation Timing** | `.NET` GC triggers when object unreachable (may be delayed during peak .NET runtime GC cycles across project boundaries; acceptable for most unmanaged resource cleanup) | Manual `Dispose()` call—immediate cleanup across GUI app lifecycle patterns in C# code review cycles | IDispose preferred—guarantees cleanup even if object referenced longer than destructor window (.NET runtime ensures immediate release)  
| **Exception Handling** | Runs after exceptions; always executes finalizer logic for OAP apps using resource management patterns across projects (C# behavior vs C++) | Throws exception on error; GUI app catches and handles in try-catch block during OAP event handling patterns | Destructor may delay cleanup slightly—IDispose ensures immediate release when GUI app calls it explicitly before reference cleared  
| **Memory Overhead** | `.NET` metadata tracking adds slight footprint per object for destructor invocation (GC scans entire heap; acceptable overhead for rare unmanaged resource access patterns across projects) | Minimal overhead (interface implementation); GC handles automatic cleanup when no references remain in OAP GUI apps designed with `IDisposable` across project boundaries  
| **Best Practice** | Use destructors when resource cleanup timing is flexible (e.g., file handles only needed until app shutdown via .NET runtime lifecycle) | Use IDispose for tight control over release timing. GUI apps call `.Dispose()` explicitly before releasing reference in event handlers or after callback sequence across project boundaries  

### Important Notes & Reminders

- **Suppress Finalize**: `GC.SuppressFinalize(this)` prevents object from triggering destructor on subsequent garbage collection cycles—useful when reusing objects multiple times within same GUI app across project boundaries
- **Exception Handling** | Destructor runs after constructor—cleanup occurs even if constructor threw; GUI app should still use try-catch to handle resource errors (.NET pattern ensures cleanup via GC regardless of early termination in C# OAP designs)
- **Virtual Destructor Override** | Child classes must override destructor (virtual keyword); `.NET` ensures correct destruction order across inheritance hierarchy (child → parent → base class cleanup sequence in OAP GUI projects)

## Quiz / Review Questions
1. When does .NET call the destructor—what condition determines if finalizer runs for a given object across project boundaries in OAP GUI design patterns using C#.NET?
2. What is the order of destructor execution (e.g., class inheritance scenario where `SensorDerived` extends `SensorBase`) when multiple objects are destroyed simultaneously by .NET GC across project boundaries?
3. How can you prevent a destructor's automatic cleanup behavior in OAP applications that reuse objects frequently during runtime cycles in .NET IDE contexts for GUI apps designed with RAII patterns?
4. What difference exists between destructors (for unmanaged resources) and IDispose pattern usage (IDisposable interface)—when should each be used in OAP designs across multiple projects using .NET C# runtime behavior patterns?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_ConstructorInitializationPatterns]] [[#Reference_IDisposablePattern]]
