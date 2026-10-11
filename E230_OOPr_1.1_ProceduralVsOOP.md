# 1.1.ProceduralProgrammingVsObjectOrientedProgramming

## Overview
This foundational topic compares procedural programming (imperative/structured) with object-oriented programming (OOP), highlighting key structural, design, and maintenance differences between these paradigms. Understanding the distinction is critical when choosing an appropriate approach for software development.

### Key Definitions
| Term | Definition |
|------|------------|
| **Procedural Programming** | Programming paradigm based on procedures/functions that operate on data in a sequential manner |
| **Object-Oriented Programming** | Paradigm organizing code around "objects" that bundle data and behavior together |
| **Procedural Abstraction** | Hiding details, focusing on what operations accomplish rather than how |
| **Encapsulation** | Bundling of related data (fields/attributes) and methods into a single conceptual unit |

### Core Concepts
1. **Data-Centric vs Behavior-Centric**: Procedural programming focuses on manipulating data through functions; OOP focuses on objects possessing both data and behavioral capabilities
2. **Modularity Differences**: Procedures create functional modularity based on functions; classes create object-based modularity with encapsulation
3. **State Management**: Procedural programs maintain global/modifiable state; each object in OOP has its own independent instance state

### Main Content

#### Data Handling Approach

| Approach | Typical Structure | Communication Style |
|----------|------------------|---------------------|
| **Procedural** | Global variables, functions call each other | Direct data passing via parameters/return values |
| **Object-Oriented** | Encapsulated objects, methods on instances | Message passing (calls) between objects |

#### Object Identity & State Persistence

- **Procedural**: Variables exist in function scope; local state is ephemeral without global variables
- **OOP**: Each instantiated object has persistent state across method calls and program execution phases

### Examples and Applications

#### Example: Data Transformation vs Object Interaction

**Procedural Approach:**
```csharp
// Global or module-level data manipulated through functions
double calculatePrice(double quantity, double rate) 
{
    // Logic operates on raw data values
}

// Single global price stored directly in program
global double currentPrice;
```

**Object-Oriented Approach:**
```csharp
// Each ShoppingCart maintains its own state independently
var cart = new ShoppingCart();
cart.AddToCart(item1);
cart.TotalPriceChanged += UpdateUI; // Event notification
```

### Important Notes & Reminders

- **Pros of OOP**: Strong encapsulation supports complex systems with multiple data sources; objects naturally maintain independent, persistent state that doesn't get modified through global variables
- **Cons of OOP**: Increased runtime overhead from object creation/disposal mechanisms; harder to reason about code flow in very large systems compared to procedural
- **Best Use Case for Procedural**: Small scripts or utility functions where overhead is irrelevant and modularity requirements are minimal
- **Best Use Case for OOP**: Mid-to-large enterprise systems requiring maintainability of complex state transitions across multiple actors

## Quiz / Review Questions
1. Explain the fundamental difference in how procedural and object-oriented programs manage data access
2. Define the "encapsulation" concept as it appears in object-OOP compared to its absence in programming
3. What is a practical advantage of using class-based structure versus global variable manipulation?
4. Describe when you would choose procedural over OOP for project design

---
**Related Topics:** [[E230_OOPr]] [[#Reference_ClassicDesign]] [[#Reference_StateManagement]]