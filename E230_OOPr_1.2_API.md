# 1.2.TheApplicationProgrammingInterfaceAPI

## Overview
The Application Programming Interface (API) defines how software components communicate with each other. In OOP contexts, APIs are exposed through classes and public methods that objects can interact with. Understanding API design principles is crucial for creating maintainable, extensible systems.

### Key Definitions
| Term | Definition |
|------|------------|
| **Application Programming Interface (API)** | A defined set of rules specifying how external programs will work together |
| **Public Method** | A method accessible outside the class to be used by external code |
| **Internal Method** | Method that can only be accessed from within the defining class |
| **Public Property** | A data field accessible via getter/setter methods but not directly visible |

### Core Concepts
1. **Contract-Based Design**: APIs define a contract—what operations are available and what they guarantee to return or modify
2. **Abstraction Hiding**: Well-designed APIs hide implementation complexity from consumers while exposing only necessary functionality
3. **Interface vs Implementation API Pattern** (OOP context): Use "public methods" that implement an abstract interface rather than exposing internal details

### Main Content

#### API Access Control Patterns

```csharp
// Public API Method - Accessible externally
public static string GetUserEmail(string userName) {
    return userDatabase.GetByUserName(userName).EmailAddress;
}

// Protected Method - Accessible within same class hierarchy
protected virtual void ProcessData() { /* internal logic */ }

// Internal Method - Accessible only within the class
internal int GetPrivateValue() => 42; // not externally callable
```

#### API Versioning Considerations
When designing APIs for OOP in C#, maintain backward compatibility:

| Old API Style | New API Compatibility Approach |
|---------------|-------------------------------|
| Single method signature with parameters | Accept optional parameters or return new object type instead of modifying existing |
| Global class names | Renamed to "IUserManager" interface pattern |
| Direct property access (not recommended) | Use accessor/property wrappers for control |

#### API Contract Guidelines

For public methods/APIs:
- **Always** clearly state parameters and return types via documentation
- Never assume the external caller has knowledge of internal implementation
- Test thoroughly for edge cases in argument validation
- Consider exceptions as a communication mechanism (not just errors)

### Examples and Applications

#### Example 1: Public Class API Design

```csharp
// Well-designed public interface for ShoppingCart
public class ShoppingCart {
    // Public getter - returns data without internal state modification
    public int TotalCount { get; } = 0;
    
    // Public method - changes object state through encapsulated logic
    public void AddItem(Product item) { 
        items.Add(item);
        NotifyTotalUpdate();
    }
}

// Internal API for class structure (not exposed to consumers)
private int CalculateDiscount() { /* logic */ }
```

### Important Notes & Reminders

- **API Documentation Is Essential**: Every public method needs clear signature and documentation comments explaining behavior
- **Interface Patterns**: In some C# OOP patterns, prefer `I[Verb]` interfaces for defining public contracts instead of classes
- **Exception Handling**: Document which exceptions may be thrown by public APIs—users must handle them appropriately
- **Avoid Overly Accessible Public Methods**: Every public method exposed becomes a contract that consumers depend on
- **Backward Breaking Changes**: Use semantic versioning patterns when modifying or removing from API surface area

## Quiz / Review Questions
1. When should you expose a class member as publicly accessible vs using internal access control?
2. Why might an OOP system prefer interface-based design over class-based design APIs in some cases?
3. What is the difference between public and protected visibility modifiers in .NET class structure?
4. How do exceptions serve as part of the API contract in C# code design?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_MethodVisibility]] [[#Reference_ExceptionHandlingAPIs]]