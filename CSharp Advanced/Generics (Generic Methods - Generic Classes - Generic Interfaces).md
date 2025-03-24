## Generic List vs Array List
- ***Type Safety*** : Generic List is **typed** which is better of course
- **Performance*** : Due to *"Boxing"* and *"Unboxing"* in arraylist, performance might be affected

# Why Generics ?
- Helps with ***reusability of code***
- Increase code ***readability*** and ***maintainability***

## How to make my class GENERIC ?

```C#
public class GenericList<T>{
private readonly List<T> _items = new();

public void Add(T item){
_items.Add(item);
}
public void Remove(T item){
_items.Remove(item);
}

public Count => _items.Count
}
```

## Generic constraints 

- `where T : INumber<T\>` → the generic must be a number (int, long, float, decimal)

> [!NOTE] Important Note
> Here I am saying  that the generic T can be "INumber" or anything that implements it, Same goes if  it was a class : then the generic T can be objects of that class or any objects that extends that class.

- Where T : Class → the Generic must be of reference type (for either a class or interface)
- Where T : Class, new () → 
	- the Generic must be of reference type (for either ***a class or interface***)
	- The class must have a ***parameterless constructor***
### Generic Method
```C#
// I want to create a generic add method (adds int,floats,decimal and long)
public static T Add<T>(T num1,T num2) where T : INumber<T> //T must be INumber
{
return num1+num2;
}
```
