# A Linked List Implementation using C# Templates for Embedded Applications

Linked lists are a common data structure in computer science. Implementing them as classes allows storing dynamically-sized sequences of elements without pre-allocating memory blocks.

## What is a Linked List?

A linked list is a sequential data structure where each node stores:
1. The actual **data** (the information)
2. A **link/reference** to the next node in the sequence

This allows dynamic sizing and flexible insertions/deletions without requiring contiguous memory blocks.

## Implementing Simple Linked List in C#

```csharp
// Node class - each element in the chain
public class LinkedListNode<T> {
    public T Value { get; set; }
    public LinkedListNode<T> Next { get; set; }
    
    public LinkedListNode(T value) {
        Value = value;
        Next = null; // Initially points to nothing
    }
}

// Linked list container class
public class LinkedList<T> {
    private LinkedListNode<T> head { get; set; }
    
    // Add element to the end
    public void Add(T value) {
        LinkedListNode<T> newNode = new LinkedListNode<T>(value);
        
        // Empty list
        if (head == null) {
            head = newNode;
            return;
        }
        
        // Append to last node
        LinkedListNode<T> temp = head;
        while(temp.Next != null) {
            temp = temp.Next;
        }
        temp.Next = newNode;
    }
    
    public void Display() {
        Console.Write("List: ");
        LinkedListNode<T> temp = head;
        while(temp != null) {
            Console.Write($"{temp.Value} -> ");
            temp = temp.Next;
        }
        Console.WriteLine();
    }
    
    // Returns count of elements in the list
    public int Count() {
        int count = 0;
        LinkedListNode<T> temp = head;
        while(temp != null) {
            count++;
            temp = temp.Next;
        }
        return count;
    }
}
```

## Using a Linked List in C# Embedded Application

```csharp
// Example of using linked list
LinkedList<int> inventoryList = new LinkedList<int>();
inventoryList.Add(10);      // Add item ID 10
inventoryList.Add(5);       // Add item ID 5
inventoryList.Add(34);      // Add item ID 34

inventoryList.Display();    // Output: List: 10 -> 5 -> 34 -> 
Console.WriteLine($"Total items: {inventoryList.Count()}"); // Output: Total items: 3

// Access elements sequentially
int current = inventoryList.head.Value;       // First element
current = inventoryList.head.Next.Value;      // Second element
```

## Why Use Linked Lists in C# Embedded Development?

- **Dynamic Sizing**: No need to resize or reallocate when adding/removing items at runtime
- **Insert/Delete Efficiency**: O(1) complexity for insertion/deletion if you already have a reference to a node
- **Memory Efficiency**: Store data where needed without gaps or unused memory blocks
- **Traversal Logic**: Access elements in order or from middle (not just beginning like arrays)

## Tradeoffs of Linked Lists

| **Pros** | **Cons** |
|----------|---------|
| Dynamic sizing | Cannot access element by index in O(1) time |
| Efficient insertions at known location | Linear traversal to find elements |
| No memory gaps or reallocation needed | Higher overhead due to extra reference storage |

For embedded systems, linked lists offer good flexibility and can be optimized for low-memory environments when combined with template types.
