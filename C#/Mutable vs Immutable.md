# 🔄 Mutable vs Immutable in C#

## 📌 Overview  
In C#, objects can be **mutable** (changeable after creation) or **immutable** (cannot be modified after creation). Understanding their differences helps in writing efficient and bug-free code.

---

## 🔍 Key Differences

| Feature            | 🟢 Mutable | 🔴 Immutable |
|-------------------|-----------|------------|
| **Can be modified after creation?** | ✅ Yes | ❌ No |
| **Thread-safe?** | ❌ No (unless explicitly handled) | ✅ Yes (safe by default) |
| **Memory Efficiency** | ✅ Uses less memory (in-place updates) | ❌ Creates new instances (higher memory use) |
| **Performance** | ✅ Faster for frequent changes | ❌ Slower due to object creation |
| **Predictability** | ❌ More risk of unintended changes | ✅ Safer and avoids side effects |
| **Use case** | When frequent modifications are needed | When immutability provides safety (e.g., functional programming, multi-threading) |

---

## 🔄 **Mutable Objects**
A **mutable** object allows modification after creation. This is useful when changes are frequent.

### ✅ **Example: Mutable Class**
```csharp
public class Person
{
    public string Name { get; set; }  // Mutable property
    public int Age { get; set; }      // Mutable property
}

var person = new Person { Name = "John", Age = 30 };
person.Name = "Alice"; // ✅ Allowed (modifies existing object)
person.Age = 31;       // ✅ Allowed
Console.WriteLine($"{person.Name}, {person.Age}"); // Output: Alice, 31
