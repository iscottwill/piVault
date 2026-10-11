# 3.2.References

## Overview
Reference variables in OOP store handles/pointers to objects, enabling data encapsulation and method invocation through the reference system rather than direct data access. Understanding how references work is essential for implementing correct object relationships and avoiding unintended memory leaks or null pointer errors.

### Key Definitions
| Term | Definition |
|------|------------|
| **Reference Variable** | A variable that stores a pointer/identifier to an object instance rather than the object's actual data value |
| **Object Instance** | An independent unit of data and behavior created by instantiating a class |
| **Null Reference Exception** | Error thrown when attempting to access properties/methods of null reference in .NET/C# types |

### Core Concepts
1. **Reference Semantics**: Objects don't exist as their actual values; instead, variables store handles pointing to instances in memory
2. **Variable Assignment & Copy**: Assigning `varA = varB` doesn't copy data; both references now point to same object internally
3. **Garbage Collection (GC)**: Reference-based objects must be collected when no variable holds their reference

### Main Content

#### Reference Variable Behavior in C# OOP

| Operation | Effect on References | Memory Impact |
|-----------|---------------------|---------------|
| `varA = varB` | Both references now point to **same** object instance | No duplication of data; shared reference only (GC managed) |
| `obj.Property = 5` | Property change affects **all** references pointing to that same object instance | Minimal memory impact (only changes value, not structure) |

#### Object Creation & Reference Assignment Pattern

```csharp
// Visual Studio OOP code structure for reference handling
class PersonOOP {
    // Public property accessible from outside class references
    public string Name => "John"; // Data stored in object instance
    
    // Internal field not directly accessible via external classes
    private int _age = 0;
    
    // Constructor initializes this new object instance's data
    public PersonOOP(int ageValue) {
        _age = ageValue; 
    }

    // Method for invoking operations on the object through references
    public void UpdateAge(int newValue) => _age = newValue; 
}

// Creating reference variables to point to objects
var person1 = new PersonOOP(25); // var1 points to first instance of PersonOOP class
var person2 = person1!; // Assign same object (reference) via null-safe operator (!)

// After assignment, both references point to same object in heap memory
Console.WriteLine(person1.Name); // Accessible through either reference
```

#### Reference Memory Management Pattern (.NET GC)

```csharp
// Example: Automatic garbage collection when references are no longer used
public class AutoDisposeReferenceExample {
    public void CreateObjectInstance() {
        var tempObj = new ObjectInstance(); // Allocate on heap, create instance
        
        // After variable goes out of scope (or is assigned null), GC will collect it
        // Memory becomes available for reuse, freeing space from this allocation
        tempObj = null; // Preventing garbage collection of tempObj explicitly
    }
}
```

#### Null Safety Considerations with C# Reference Type Handling

| Operation | Effect | Exception Scenario |
|-----------|--------|-------------------|
| `var obj: T` | Declares reference-typed variable (e.g. classes in .NET) | May point to null value initially |
| `null! reference` | Forces non-null value using null safety operator | Unsafe if object actually is null at runtime |

### Examples and Applications

#### Example 1: Object Reference Assignment Chain (.NET OOP Pattern)

```csharp
// File: OOPExample.cs (visual studio generated code template)
public class ReferentialChainExample {
    // Multiple reference variables assigned to same object instance
    private PersonOOP _primaryInstance = new PersonOOP(30); // Create first person instance
    
    // Second variable points to same object instance after assignment
    public PersonOOP PrimaryReference => _primaryInstance!; 
}
// Access via either reference works identically
```

#### Example 2: Shared Reference Between Multiple Variables (Single Object Instance)

| Variable | Holds Reference To |
|----------|-------------------|
| `PersonOOP o1` | Same object instance as `o2` and `o3` |
| `PersonOOP o2` | Same object instance as `o1` and `o3` |
| `PersonOOP o3` | Same object instance as `o1` and `o2` |

```csharp
// Visual Studio generated code for reference behavior demonstration
public class ReferenceDemo {
    public PersonOOP GetSingleInstance() {
        PersonOOP refOne = new PersonOOP(25);
        
        // Both references now point to same object in heap memory
        refTwo = refOne;
        
        Console.WriteLine(refOne.Name); // "John" - same instance via both refs
        Console.WriteLine(refTwo.Name); // Also prints "John" (same object)
    }

    // After variable assignments complete, both references point to same PersonOOP instance
}
```

### Important Notes & Reminders

- **No Value Copies on Assignment**: When assigning a reference, only the reference value is copied—not the entire object data. This creates shared memory usage across all assigned references pointing to the same object instance
- **Null Reference Safety**: .NET handles null checks implicitly; attempt accessing properties/methods of `null` triggers exception handling (not just crash on older versions)
- **Garbage Collection Considerations**: Unreferenced objects are eligible for GC after variable assignments complete and no more references point to them; memory management is automatic in OOP C# development environments
- **Use Null-Safety Operator** (`!`) to avoid runtime null checks when explicitly requiring non-null guarantees: `obj.method()` can be simplified by using `var obj = value!`

## Quiz / Review Questions
1. What happens to two variables after assigning `refB = refA` in C# reference-typed OOP?
2. Why is the null-safety operator (`!`) used when creating new object instances in some cases?
3. Which exception would occur if you tried to call a method on a null reference variable in .NET C#?
4. In what scenario does garbage collection automatically reclaim an object's memory in OOP?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_NullPointerSafety]] [[#Reference_ObjectInstanceState]]