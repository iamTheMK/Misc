# Readonly References: Memory Perspective in C#

## Overview
In C#, the `readonly` keyword can be applied to fields. When used on reference type fields, it guarantees that the **reference** (i.e., the pointer to the object in memory) cannot be changed after initialization. However, the object that the reference points to can still be modified if it is mutable.

---

## Memory Perspective: Reference vs. Object

### How Objects Are Stored in Memory
- **Heap Allocation:**  
  Objects in C# (i.e., instances of classes) are stored on the heap. The heap contains the actual data (the object's fields and properties).

- **Reference Variables:**  
  A variable of a reference type holds a pointer (reference) to the memory location on the heap where the object is stored.

### What `readonly` Guarantees
- **Immutable Reference:**  
  When you declare a field as `readonly`, you are ensuring that the reference (the pointer stored in that field) cannot be changed after it has been assigned in the declaration or constructor. In other words, the variable will always point to the same memory address.

- **Mutable Object Content:**  
  Even though the reference is fixed, if the object itself is mutable (i.e., its internal state can change), then the fields within the object can be modified. This means that while you cannot point the readonly field to a different object, you can still modify the object's data at that memory location.

---

## Example

Consider the following example:

```csharp
public class Person
{
    public string Name { get; set; } // Mutable property
}

public class MyClass
{
    public readonly Person MyPerson; // Readonly field

    public MyClass(Person person)
    {
        MyPerson = person; // Assignment allowed only here
    }
}

public class Program
{
    public static void Main()
    {
        // Create a new Person object
        var person = new Person { Name = "John" };
        var myClass = new MyClass(person);

        // The reference stored in myClass.MyPerson is immutable:
        // myClass.MyPerson = new Person { Name = "Alice" }; // Error: Cannot reassign a readonly field

        // However, the object's internal state is mutable:
        myClass.MyPerson.Name = "Alice"; // Allowed: Changing the object's property

        Console.WriteLine(myClass.MyPerson.Name); // Output: Alice
    }
}
