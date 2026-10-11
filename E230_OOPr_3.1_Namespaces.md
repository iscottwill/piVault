# 3.1.Namespaces

## Overview
Namespaces provide a structured way to organize related types, methods, and code in OOP projects. They prevent naming conflicts by grouping identifiers under hierarchy-based names. In .NET/C#, namespaces are essential for managing large-scale applications with multiple component libraries.

### Key Definitions
| Term | Definition |
|------|------------|
| **Namespace** | Container for organizing related classes, interfaces, and types within a project structure |
| **Name Collisions** | When two classes have identical names across different projects (e.g., `System.Console` vs custom `Console`) |
| **Public API Exposure** | Namespaces can expose their public types as external references or packages for reuse |

### Core Concepts
1. **Organization Hierarchy**: Classes, interfaces, and enums are grouped into logical categories using namespace declarations
2. **Avoids Collision Conflicts**: Each member (class/variable/method) can be uniquely identified via fully qualified names like `MyApp.CoreClasses.UserManager`
3. **File Namespace Structure**: In OOP .NET projects, the namespace typically matches the file folder structure (`.csproj` project folders)

### Main Content

#### Namespace Declaration vs Public Type Exports

```csharp
// Multiple classes in same namespace
namespace MyApp {
    public class Calculator { } // Available as "MyApp.Calculator"
    public class UserRepository { } // Also available as "MyApp.UserRepository"
    
    // Alternative: Direct type references if using fully qualified names
    System.Runtime.Versioner.MyAssembly.Calc(); 
}
```

#### Namespace Hierarchy Structure (.NET OOP)

```xml
<!-- .csproj project structure for namespace organization -->
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net6.0</TargetFramework>
        <!-- Root namespace matches folder structure -->
    </PropertyGroup>
    
    <ItemGroup>
        <Compile Include="CoreClasses.cs" />
        <Compile Include="DataInterfaces.cs" />
    </ItemGroup>
</Project>

<!-- CoreClasses.cs namespace declaration follows file path naming convention -->
namespace MyApp.Models {
    public class ShoppingCart { /* ... */ }
}
```

#### Namespace vs Global Scope Comparison

| Feature | Global Scope (e-type reference) | Namespace-Scoped type |
|---------|--------------------------------|------------------------|
| **Type Name Clarity** | Conflicts if multiple types with same name exist | Unambiguous via `FullyQualifiedTypeName` |
| **Visibility Control** | Less flexible for large-scale APIs | Precise access modifiers (`public`, `internal`) can be applied within namespace |
| **Import Pattern** | Uses `<Using>` directives for common namespaces | Can use `using` statements to simplify code with multiple names |

### Examples and Applications

#### Example 1: Namespace Organization in .NET OOP Projects

```csharp
// File: Models/ShoppingCart.cs (namespace declaration matches file/folder)
namespace MyApp.Models {
    public class ShoppingCart {
        // Internal state field using namespace-qualified visibility
        private double _discountFactor = 0.95; 
        
        // Public accessor exposes value through the same namespace's type context
        public decimal TotalPrice => CalculateTotal(); 
    }
}

// File: Services/PricingService.cs (service namespace)
namespace MyApp.Services {
    public interface IPricingService {
        // External API exposed through namespace
        string ProcessBilling(decimal amount);
        
        // Implementation in separate service class
        public bool ValidatePayment() { } // Internal type visibility control
    }

    public class PricingServiceImpl : IPricingService {
        private double _taxRate = 0.08;

        // Service method accessible via external consumer API
        public string ProcessBilling(decimal amount) => 
            $"Total: ${amount * (1 + _taxRate):F2}";
    }
}

```

#### Namespace vs Type Resolution Pattern

| Access Pattern | Usage Example | Visibility |
|---------------|---------------|------------|
| **Using Alias** | `using MyApp.Models.ShopingCart;` | Direct reference (`ShoppingCart`) |
| **Fully Qualified** | `MyApp.Models.ShoppingCart` | Requires explicit resolution |
| **Global Scope** | No namespace, just `Calculator class` | Type accessible without prefix (limited collisions) |

### Examples and Applications

#### Example 2: Large-Scale .NET Project File Organization (.csproj Structure)

```xml
<!-- Visual Studio project file for OOP development -->
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFramework>net6.0</TargetFramework>
        <RootNamespace>MyEnterpriseApp</RootNamespace> <!-- Matches namespace root name -->
    </PropertyGroup>
    
    <ItemGroup>
        <!-- Multiple namespaces in one project -->
        <Compile Include="src\DataAccess\DAL.cs" />
        <Compile Include="src\Services\Auth\.cs" />
        <Compile Include="CoreClasses\Product\.cs" />
    </ItemGroup>
    
    <!-- Namespace hierarchy matches folder structure pattern -->
</Project>

<!-- Code file demonstrates naming conventions and type accessibility patterns -->
// src\DataAccess\DAL.cs (namespace: MyApp.DataProviders)
namespace MyApp.DataProviders {
    public class DatabaseRepository { } // Accessible via MyApp.DataProviders.IDB 
}
```

### Important Notes & Reminders

- **Naming Convention**: Typically, namespaces are named after the project/class name (e.g., `MyCompany.MyProject.ApplicationCore`) or match file structure conventions in Visual Studio
- **Using Directives**: Use `using` statements to reduce verbosity when importing specific types from multiple namespaces; avoid excessive namespace imports if it causes collisions
- **Visibility Control**: Internal namespaces (not publicly exposed) use `internal`, `protected`, and `private` modifiers more restrictively than public APIs that may be referenced by external consumers
- **Namespace vs Class Naming**: Differentiate between namespace (project-level organization) and class name (type identifier); ensure clarity and avoid potential naming conflicts

## Quiz / Review Questions
1. What is a key benefit of using namespaces when organizing types in OOP C# development?
2. How do fully-qualified names like `MyApp.CoreClasses.UserManager` help prevent type name collisions?
3. What's the typical relationship between namespace declarations and file folder structures in a .NET project?
4. Which modifier can be used to control external API visibility within an internal namespace context?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_TypeVisibilityModifiers]] [[#Reference_ProjectStructureOOP]]