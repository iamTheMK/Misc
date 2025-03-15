# 📌 Memory Allocation Breakdown in C#

## 🔹 Code Example
```csharp
public class Storage
{
    public int Data; // Value type (stored on heap as part of the object)
    public string Name; // Reference type (stored separately on heap, reference in object)
}

Storage obj = new Storage();
obj.Data = 100;
obj.Name = "Example";
```

🔍 Where is Memory Allocated?
📝 Stack Memory (For Local Variables & References)
obj (a reference to the Storage object) is stored in the stack.
🏗 Heap Memory (For Objects & Reference Type Data)
The Storage object itself is allocated in the heap.
Data (an int) is a value type, but since it's inside a class, it is stored within the heap object.
Name (a string) is a reference type, so only a reference is stored inside Storage, while the actual string "Example" is stored in another location on the heap.

🔄 Memory Layout Representation
vbnet
Copy
Edit
Stack:
    obj  ----->  [Storage object reference] (Points to Heap)

Heap:
    [ Storage Object ]
    ├── Data (100) [Stored within the object]
    ├── Name [Reference to "Example" in Heap]
    
    [ "Example" String (Stored separately) ]
📌 Key Takeaways

Objects (reference types) are stored in the heap, while their references are stored in the stack.
Value types inside reference types are part of the heap object.
Strings in C# are immutable and stored separately in the heap.
