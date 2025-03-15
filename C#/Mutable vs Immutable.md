# 🔄 Mutable vs Immutable in C#

## 📌 Overview  
In C#, objects can be **mutable** (changeable after creation) or **immutable** (cannot be modified after creation). Understanding their differences helps in writing efficient and bug-free code.

---

## 🔍 Key Differences

| Feature                                | 🟢 Mutable                                         | 🔴 Immutable                                      |
|----------------------------------------|----------------------------------------------------|---------------------------------------------------|
| **Can be modified after creation?**    | ✅ Yes                                             | ❌ No                                             |
| **Thread-safe?**                        | ❌ No (unless explicitly handled)                  | ✅ Yes (safe by default)                          |
| **Memory Efficiency**                    | ✅ Uses less memory (in-place updates)             | ❌ Creates new instances (higher memory use)       |
| **Performance**                          | ✅ Faster for frequent changes                     | ❌ Slower due to object creation                  |
| **Predictability**                       | ❌ More risk of unintended changes                 | ✅ Safer and avoids side effects                  |
| **Use case**                             | When frequent modifications are needed            | When immutability provides safety (e.g., functional programming, multi-threading) |

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
✅ Pros of Mutable Objects
Efficient for frequent changes: No need to recreate objects.
Simpler for certain cases: Useful for UI applications with updates.
More memory-efficient: Especially when modifying large collections.
❌ Cons of Mutable Objects
Not thread-safe: Concurrent modifications can lead to issues.
Unexpected side effects: Changes may propagate if object references are shared.
🔒 Immutable Objects
An immutable object cannot be changed after creation. Any modification results in a new object.

✅ Example: Immutable Class (using readonly & init)
csharp
Copy
Edit
public class Person
{
    public string Name { get; init; }  // Immutable property (C# 9+)
    public int Age { get; init; }      // Immutable property

    public Person(string name, int age) => (Name, Age) = (name, age);
}

var person = new Person("John", 30);
// person.Name = "Alice"; // ❌ Error: Cannot modify 'init' property
var updatedPerson = new Person("Alice", 31); // ✅ Create a new instance

Console.WriteLine($"{person.Name}, {person.Age}");           // Output: John, 30
Console.WriteLine($"{updatedPerson.Name}, {updatedPerson.Age}"); // Output: Alice, 31
✅ Pros of Immutable Objects
Thread-safe by default: No locks required.
Predictable behavior: Avoids unintended side effects.
Functional programming friendly: Encourages pure functions.
❌ Cons of Immutable Objects
Higher memory usage: New objects are created on every change.
Performance overhead: Frequent object recreation can be costly.
Less flexible: Requires more thoughtful design.
🆚 Choosing Between Mutable & Immutable
Use Case	Choose Mutable	Choose Immutable
UI Applications	✅ Yes	❌ No
Data Structures (e.g., Lists, Dictionaries)	✅ Yes	❌ No
Multi-threaded Applications	❌ No	✅ Yes
Functional Programming	❌ No	✅ Yes
Performance-sensitive scenarios (e.g., Game Dev)	✅ Yes	❌ No
Configuration or Value Objects	❌ No	✅ Yes
🔄 Hybrid Approach: Using Records (C# 9+)
Records provide immutability with a simple syntax.

✅ Example: Immutable Record (Recommended for DTOs)
csharp
Copy
Edit
public record Person(string Name, int Age);

var person = new Person("John", 30);
var updatedPerson = person with { Age = 31 }; // ✅ Creates a new object with a modified property

Console.WriteLine(person);         // Output: Person { Name = John, Age = 30 }
Console.WriteLine(updatedPerson);  // Output: Person { Name = John, Age = 31 }
Records make immutability easy while allowing changes via with.
Great for DTOs and data transfer objects in APIs.
