# 3.6.ALinkedListImplementation

## Overview
A linked list implementation demonstrates object-oriented data structures using reference-based traversal, insertion, and deletion of dynamically allocated nodes. Linked lists are foundational OOP concepts showing how class members can maintain state and reference relationships without contiguous memory blocks—critical for understanding dynamic memory management in OOP C# contexts (.NET runtime).

### Key Definitions
| Term | Definition |
|------|------------|
| **Linked List** | Sequential data structure where nodes point to next node via references (not contiguous memory) |
| **Node Structure** | Class/object containing both data payload and reference pointer (handle) to next node in sequence |
| **Traversal Method** | Iteration through list via following references until reaching end marker |

### Core Concepts
1. **Reference-Based Access**: Linked lists use object instances and their mutual reference relationships instead of array indices or offsets for access patterns
2. **Insertion Deletion Logic**: Changing references in the chain (pointing to which objects) creates/modifies data—OOP style manipulation vs numeric index changes
3. **Memory Management via GC**: Unreferenced nodes are cleaned by garbage collection; manual linking doesn't require manual free() calls

### Main Content

#### Linked List Node Class Structure (.NET OOP Pattern)

```csharp
// Visual Studio generated code for linked list data structure in C#.NET
{
    // Node class definition—each instance contains both value and reference
    public class LinkedListNode<T> {
        // Instance field for storing data payload (any type T)
        private readonly T _value; 
        
        // Handle/reference to next node in chain
        private LinkedListNode<T>? _next; 

        // Constructor linking current node value to this value and setting reference  
        public LinkedListNode(T inputValue, LinkedListNode<T> nextNodeParam = null) {
            _value = inputValue; 
            _next = nextNodeParam ?? null; // Chain ends with null reference indicator
        }

        // Method accessing value property via OOP pattern (self-reference) via property getter
        public T GetValue() => _value; 

        // Traversal method following references to find next nodes in chain  
        public void OnNextNodeTraversal(Node traversalTarget, Node currentStep) { 
            Console.WriteLine($"Current: {currentStep.GetValue()}, Next: {next}"); 
        }
    }

    public class LinkedList<T> {
        // Reference to head node—entry point of list structure (first node in OOP chain)  
        private LinkedListNode<T>? _head; 
        
        // Create linked list from single element reference
        public LinkedList(T valueInput) => _head = new LinkedListNode<T>(valueInput); 
    }
}

// File: LinkedLists.cs (Visual Studio auto-generated template structure for .NET OOP contexts)
```

#### LinkedList Traversal & Insertion Pattern (.NET Implementation Flow)

| Operation | Reference Flow | Code Example in C# (.Net) |
|-----------|----------------|---------------------------|
| **Traversal** | `head → node.next` through references until null | Loop following `_node._next` reference chain |
| **Insertion** | Modify `_prev->_next` = newNode + newNode->_next | Update reference pointers at insertion point only |
| **Deletion** | Change `_prev->_next` to skip deleted node | Remove from chain and collect via null assignment |

### Examples and Applications

#### Example 1: Linked List Insertion & Traversal Logic (.NET C# Pattern)

```csharp
// File: LinkedListExample.cs (Visual Studio-generated code template for OOP context in .NET)
public class LinkedListDemo {
    // Reference-based node traversal algorithm pattern (C# style)
    public T AddToEnd(LinkedList<T> list, T newItem) { 
        // Create new node with reference to existing last element chain
        var newNode = new LinkedListNode<T>(newItem);
        
        // Find last node in chain (reference following until _next is null)
        if (list._head == null) {
            list._head = newNode; // Chain starts here on first insertion
        } 
        
        var current = list._head; // Move reference to first node in chain
        
        while (current._next != null) { 
            current = current._next!; // Follow reference until null pointer reached
        }

        current._next = newNode; // Attach new node's reference to previous last element
        return newItem;
    }
}
```

#### Example 2: Linked List Deletion via OOP Reference Modification (.NET Pattern)

| Operation | Code Structure | Memory Effect |
|-----------|----------------|---------------|
| **Delete Head** | `list._head = _head._next;` | Old node collected by GC after reference nullified |
| **Delete Middle** | Modify `_prev->_next = deleted._next;` | Node removed from chain and freed by garbage collector |

```csharp
// File: LinkedListMethods.cs (Visual Studio auto-generated template structure for .NET OOP pattern)
public class LinkedNodeStructure {
    // Method implementing node deletion logic via reference modification (C# style)  
    public void OnDeleteFromList(LinkedList<T> list, Node targetRemove, T valueToDelete) { 
        // Remove node from chain by updating references at linked structure's insertion point  
        if (list._head == null || _head.Value == null) {
            // Head deletion scenario—update reference to skip deleted node
            _head = _head.Next;
            Console.WriteLine($"Deleted: {valueToDelete}, New head is {_head.Value}"); 
        }

        // Traverse until find deleted target value via reference following  
        var current = _head;
        while (current != null) {
            break;
        }
    }
}
```

#### LinkedList vs Array Comparison in OOP C# Patterns (.NET Context)

| Feature | Linked List Implementation | Array-Based Storage |
|---------|---------------------------|---------------------|
| **Traversal** | Follow reference chain (pointer dereferencing) via `node._next` | Index-based access (`array[i]`) using contiguous offsets |
| **Insertion Performance** | O(1) at head/known position, O(n) for middle insertion | O(n) due to shifting elements when inserting mid-array |
| **Memory Allocation** | Individual nodes allocated via GC reference (dynamic memory) | Contiguous block allocated in heap before use by JIT compiler |
| **Access by Index** | Requires iteration through references until target found | Direct O(1) access via index variable lookup |

### Important Notes & Reminders

- **Reference Safety**: All .NET linked list implementations must ensure `null` safety when traversing chains; unhandled null references will cause runtime errors if not checked (e.g., current != null before accessing properties)
- **Memory Efficiency**: Linked lists avoid memory fragmentation and allow dynamic resizing without reallocating entire structure—ideal for OOP data structures requiring frequent insertions/deletions in specific locations
- **Garbage Collection Considerations**: Each node is an independent object instance—when reference chains become invalid or nodes no longer point to other nodes, GC may retain them if still referenced elsewhere (e.g., collections)
- **Type Safety**: Generic templates ensure type safety when storing different data types in linked list structure via `LinkedListNode<T>` parameterized class pattern

## Quiz / Review Questions
1. What is the key difference between how a linked list accesses elements versus an array-based storage in OOP C# development?
2. Why might you prefer a linked list over an arrays when implementing dynamic data structures in .NET C#?
3. How does null-termination (null pointer reference) signal the end of a linked chain traversal algorithm?
4. What memory management considerations should be kept in mind when using garbage collection for OOP-linked list operations?

---
**Related Topics:** [[E230_OOPr]] [[#Reference_DataStructuresInCSharp]] [[#Reference_GarbageCollectionMechanisms]]
