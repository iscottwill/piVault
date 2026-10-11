# 6.1.EncapsulationInheritancePolymorphism

## Overview
These three core OOP principles—encapsulation, inheritance, and polymorphism—are foundational to C#.NET programming, enabling modular, maintainable code structures that hide internal details and promote reuse. Understanding their interplay is critical for designing class hierarchies with proper access control, method overriding behaviors, and runtime type dispatch in .NET GUI/embedded applications.

### Key Definitions
| Term | Definition |
|------|------------|
| **Encapsulation** | Hiding internal implementation details via private/protected members accessible only through controlled interfaces (public/private API design) |
| **Inheritance** | Parent-child class relationship where child inherits parent's properties and methods—supports code reuse in OAP applications by avoiding duplication of logic |
| **Polymorphism** | Single interface (method call) with multiple implementations (e.g., `Base.Draw()` may render differently for derived classes); .NET enables polymorphic behavior via virtual methods + method overriding at runtime |

### Core Concepts
1. **Encapsulation Controls Access**: Internal data members (`internal`) remain protected from external access; API surfaces control exposure scope in OOP design patterns in C#.NET contexts
2. **Runtime vs Compile-Time Inheritance**: Child methods are linked during compile time when overridden (runtime dispatch uses JIT), creating flexible behavior modification without recompiling parent class logic
3. **Virtual Method Dispatch**: Polymorphic calls resolve to correct implementation at runtime based on object type—allows extensibility for new .NET classes derived from base types in OAP applications

### Main Content

#### Encapsulation Access Control Patterns (.NET C# API Design)

```csharp
// Visual Studio generated code for encapsulation/inheritance/polymorphism patterns
{
    // Base class demonstrates encapsulation (private data + public interface) and virtual methods for polymorphic behavior  
    public class AnimalBase {
        private int _age = 0; // Encapsulated data (not directly accessible outside class scope via .NET access control) 
        
        // Property provides controlled access to internal state via getter/setter pairs (OAP design pattern)  
        public int OnGetAge() => _age; 
        public void OnSetAge(int value) => _age = value; 

        // Virtual method enables runtime polymorphic dispatch for derived classes in .NET OOP context  
        public virtual void PerformSound(object sender, EventArgs e) { 
            Console.WriteLine("Base class sound"); // Polymorphic callback (virtual implementation default behavior)  
        }
    }

    // Derived class overrides virtual method with new behavior at runtime via inheritance  
}
```

#### Access Control & Virtual Method Dispatch (.NET OOP Runtime Context)

| Feature | Behavior | Example Usage in .NET GUI Apps |
|---------|----------|-------------------------------|
| **Encapsulation** | Private members hidden; public/private API exposed for controlled access (e.g., `GetAge()` reads internal `_age` field) | Keeps user data protected from direct modification via GUI app state changes in OAP applications using event-driven callback patterns |
| **Inheritance (Base/Child)** | Child gains all parent member definitions—can extend rather than duplicate functionality (OOP design reduces code duplication; inheritance is automatic, no need to manually specify which methods are inherited) | Enables common .NET framework classes (`Animal`, `User`) to be extended with subclass-specific behavior by overriding base class implementations in GUI apps |
| **Polymorphic Method Calls** | Runtime resolves virtual method dispatch correctly for derived objects (OAP applications can safely call method without knowing exact derived type at compile time; enables extensibility for adding new .NET classes) | Allows GUI to handle animal types uniformly via `OnPerformSound()` method—each subclass's behavior determined by runtime OOP inheritance chain analysis in .NET JIT compiler |

### Examples and Applications

#### Example 1: Encapsulation + Inheritance (OAP Class Design Pattern)

```csharp
// File: BaseChildInheritance.cs (Visual Studio auto-generated template structure demonstrating OOP encapsulation/inheritance/polymorphism in C#.NET context)
{
    // Base class uses encapsulation to hide internal data behind controlled access methods via .NET's public/private modifier keywords  
    public class AnimalBase {
        private int _age;

        // Encapsulated method exposes only part of state (OAP design pattern for GUI apps) 
        public int OnGetAge() => _age; 

        // Virtual method enables polymorphic override in derived classes later through runtime type dispatch in JIT-compiled .NET code  
    }
}

// File: AnimalClassDerivation.cs (Visual Studio auto-generated template structure showing parent/child inheritance relationships in C#/.NET)
{
    class Dog : AnimalBase { // Inheritance declaration: Dog derives from AnimalBase  
        private int _leashes = 0; // Additional child-specific data member for GUI state tracking
        
        protected override void OnPerformSound(object sender, EventArgs e) { 
            Console.WriteLine("Dog barks!"); // Override base method with custom behavior (child specific logic in OAP design) 
        }
    }

    class Bird : AnimalBase { // Inheritance declaration: Bird derives from AnimalBase  
        private int _flightDistance = 0;
        
        protected override void OnPerformSound(object sender, EventArgs e) { 
            Console.WriteLine("Bird chirps!"); // Different logic for bird type via polymorphism at runtime in .NET OAP context
        }

        // Encapsulation continues—private state members (_leashes, _flightDistance) not directly accessible from GUI code except via OAP setter patterns  
    }
}
```

### Examples and Applications

#### Example 2: Polymorphic Behavior at Runtime (Virtual Methods in C#/.NET Context)

| Method Call | Runtime Behavior (.NET JIT Analysis) | GUI Response Pattern |
|------------|--------------------------------------|----------------------|
| **`animal.PerformSound()`** | JIT resolves to child's `OnPerformSound()` method based on object type (e.g., Dog vs Bird class at runtime); enables extensibility for adding new animal types in OAP apps without recompiling base class code | GUI displays appropriate sound message based on derived object type; supports dynamic behavior through inheritance/polymorphism without modifying parent logic |

```csharp
// File: PolymorphicBehavior.cs (Visual Studio auto-generated template demonstrating polymorphism patterns in C#/.NET GUI app context)
{
    // GUI method accepts any animal-type variable—runtime dispatch determines correct implementation per subclass at runtime via OAP pattern  
    public void OnHandleSoundEvent(AnimalBase animalType, object sender, EventArgs e) { 
        animalType.OnPerformSound(sender, e); // Virtual method dispatched correctly per subclass type (runtime analysis in JIT-compiled code) 
    }

    class Cat : AnimalBase {
        private int _meowCount = 0; 

        protected override void OnPerformSound(object sender, EventArgs e) => 
            Console.WriteLine($"Cat meows! Count: {_meowCount}"); // Different behavior for cat (overridden via child class inheritance)  
    }

    // GUI event handler pattern supports dynamic object types (e.g., Dog, Bird classes derived from same base type in OAP applications)
}
```

### Important Notes & Reminders

- **Access Modifiers**: Use `private`, `protected`, and `internal` carefully—encapsulation prevents direct access to internal data; GUI apps can still modify via .NET's getter/setter methods (OOP design pattern)
- **Virtual vs Static Methods**: Non-virtual methods are resolved at compile time (fast); virtual methods use JIT dispatch for extensibility in OAP applications (polymorphic behavior requires runtime analysis)
- **Seal Classes** | `abstract` classes can't be instantiated directly; used as base types only (e.g., abstract interfaces like `BaseGUI`, `EmbeddedDevice` patterns in .NET GUI apps). Child classes implement virtual methods at runtime for polymorphic behavior through inheritance hierarchy in OAP designs
- **Derived Methods**: Override keyword is required for child class to replace parent implementation; otherwise method call still invokes parent's original code (runtime dispatch via JIT analysis)

## Quiz / Review Questions
1. What is the key difference between private and protected access modifiers when designing a .NET GUI app's inheritance hierarchy in C#?
2. Why might you use virtual methods instead of static methods for polymorphic behavior in an OAP application that needs extensibility across multiple derived classes?
3. How does .NET's JIT compiler determine which implementation (base vs child class) to dispatch when calling a virtual method via GUI callback?
4. What happens if you try to instantiate an abstract class directly in your OAP application—what error behavior do you expect (.NET runtime)?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_InheritancePolymorphismInCSharp]] [[#Reference_VirtualMethodsJITCompileTime]]
