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


🔍 Where is Memory Allocated?
📝 Stack Memory (For Local Variables & References)
obj (a reference to the Storage object) is stored in the stack.
🏗 Heap Memory (For Objects & Reference Type Data)
The Storage object itself is allocated in the heap.
Data (an int) is a value type, but since it's inside a class, it is stored within the heap object.
Name (a string) is a reference type, so only a reference is stored inside Storage, while the actual string "Example" is stored in another location on the heap.
