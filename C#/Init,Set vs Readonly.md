# 🆚 `init` vs `private set` vs No Set vs `readonly` in C#

## 📌 Overview  
In C#, different property access modifiers determine how and when values can be modified. This guide explains the differences between:  

- `init` (Immutable after initialization)  
- `private set` (Modifiable only within the class)  
- No Set (Completely immutable without a setter)  
- `readonly` (Runtime constant)  

---

## 🔍 Key Differences  

| Feature          | 🟢 `init` | 🔵 `private set` | 🟠 No Set | 🔴 `readonly` |
|-----------------|-----------|-----------------|-----------|-------------|
| **Modifiable at Declaration** | ✅ Yes | ✅ Yes | ❌ No | ✅ Yes |
| **Modifiable in Constructor** | ✅ Yes | ✅ Yes | ❌ No | ✅ Yes |
| **Modifiable in Class Methods** | ❌ No | ✅ Yes | ❌ No | ❌ No |
| **Modifiable Outside the Class** | ❌ No | ❌ No | ❌ No | ❌ No |
| **Requires Backing Property** | ❌ No | ❌ No | ✅ Yes (or computed) | ❌ No |
| **Immutable After Initialization** | ✅ Yes | ❌ No | ✅ Yes | ✅ Yes |
| **Runtime Constant** | ❌ No | ❌ No | ❌ No | ✅ Yes |

---

## 📌 Explanation & Examples  

### 1️⃣ `init` (Immutable After Initialization)  
✔️ **Can be modified**: At **declaration** or **in the constructor**  
❌ **Cannot be modified**: In **class methods** or **outside the class**  
🔹 Introduced in **C# 9** for **record types** and immutable objects.  

#### ✅ Example:
```csharp
public class Person
{
    public string Name { get; init; } = "John"; // Can be modified only during initialization
}

var person = new Person { Name = "Alice" }; // ✅ Allowed
person.Name = "Bob"; // ❌ Error: Cannot modify 'init' property after initialization
```

---

### 2️⃣ `private set` (Modifiable Only Inside Class)  
✔️ **Can be modified**: At declaration, constructor, and inside class methods  
❌ **Cannot be modified**: Outside the class (via an instance)  

#### ✅ Example:
```csharp
public class Person
{
    public string Name { get; private set; } = "John";
    
    public void UpdateName(string newName)
    {
        Name = newName; // ✅ Allowed within the class
    }
}

var person = new Person();
person.Name = "Alice"; // ❌ Error: Property has a private setter
person.UpdateName("Alice"); // ✅ Allowed via a method inside the class
```

---

### 3️⃣ No Set (Completely Immutable)  
✔️ **Can be modified**: Only via a backing field or computed property  
❌ **Cannot be modified**: Directly at declaration, constructor, or class methods  

#### ✅ Example:
```csharp
public class Person
{
    private string _name = "John"; // Backing field
    public string Name => _name; // Read-only computed property
}

var person = new Person();
person.Name = "Alice"; // ❌ Error: Cannot assign to a read-only property
```

✅ **Alternative using computed property:**
```csharp
public class Rectangle
{
    public int Width { get; }
    public int Height { get; }

    public int Area => Width * Height; // No setter, dynamically computed

    public Rectangle(int width, int height)
    {
        Width = width;
        Height = height;
    }
}

var rect = new Rectangle(5, 10);
Console.WriteLine(rect.Area); // Output: 50
```

---

### 4️⃣ `readonly` (Runtime Constant)  
✔️ **Can be modified**: At declaration or in the constructor  
❌ **Cannot be modified**: After initialization  
🔹 **Different from `const`** because `readonly` is evaluated at runtime, not compile-time.  

#### ✅ Example:
```csharp
public class Person
{
    public readonly string Name = "John";

    public Person(string name)
    {
        Name = name; // ✅ Allowed in constructor
    }
}

var person = new Person("Alice");
person.Name = "Bob"; // ❌ Error: Cannot modify a readonly field
```

✅ **Difference between `readonly` and `const`:**
```csharp
public class Example
{
    public const double Pi = 3.14159; // Compile-time constant
    public readonly double RuntimeValue; // Runtime constant

    public Example()
    {
        RuntimeValue = DateTime.Now.Second; // ✅ Allowed in constructor
    }
}
```

---

## 🎯 Key Takeaways  
✔️ Use `init` for properties that should be immutable after object creation.  
✔️ Use `private set` when modifications should be restricted to within the class.  
✔️ Use no setter when values should be entirely read-only or dynamically computed.  
✔️ Use `readonly` for fields that should only be set at initialization but not changed later.  

---

## 🚀 Summary  

| Modifier       | Best Use Case |
|---------------|--------------|
| `init`        | Immutable after object creation |
| `private set` | Modifiable only inside the class |
| No Setter     | Fully read-only properties (computed or backing field required) |
| `readonly`    | Runtime constants, set only at declaration or constructor |

🚀 **Choose the right modifier based on your immutability and access control needs!**
