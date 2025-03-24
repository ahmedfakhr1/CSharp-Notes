# Classes and Objects
- C# 's ==main paradigm is OOP== just like Java
- Naming Properties 
  ```c#
   public string name {get; set;}
   ```
- It used ==. Notation== to access the properties
- Any class we create, by default it inherits the Object Class.

---
# Constructor
```c#

```
- Notice that  constructors don't have a return type, not even *void*
- Uses the key word ==this== , just like JAVA
---
# Namespaces / Folder 
-  Default namespace AND best practice when creating the file of the class, it takes ==the path== of this file as the namespace
  BUT
  It's not a rule, we can change the namespace to what ever we want
- when you want to use ==code== that's written ==in another namespace==, we will need to import the code from this namespace
  `using namespaceName`
- the same namespace can't have class/interface/enum of  the same name(applies to class/interface and all combinations)
## conflicts
conflict happen when you include 2 different namespaces that have the 2 classes with the same name.
when you use the class, the compiler will not know which class you're referring to in your code.
- to solve the problem we can use ==alias== like the following:![[Pasted image 20250117231359.png]]
- we can define which class in which namespace we want to use in our code
  ![[Pasted image 20250117231611.png]]
---
# Access Modifier

> [!NOTE] Project construction
> ==The consoleApp is used as like an entry point==, but real business logic is found in ==ClassLibrary Project Type==

## Adding Project Reference
You add project referenece when you include a namespace form another project
### ** How to Add a Project Reference (Visual Studio)**

1. **Right-click** on the project that needs the reference (`MyApp.UI`).
2. Select **Add → Project Reference**.
3. Check the project you want to reference (`MyApp.Core`).
4. Click **OK**.
## Access Modifiers
### Public - internal - Private
- Public
	- Seen in all project  scope and other projects in the solution (if referenced).
- Internal
	- Inside the project
- Private
	- To the class
	- Note: class can't be private unless it's inside another class
- 
---
# ==Const vs *ReadOnly Variables*==
## Const
- WEIRDLY : Microsoft encourges using PascalCase also with constants
  `public const String MyStringCosntant = "Ahmed"; `
- Can't be overwritten
- ==Compile time constant==
	- Its value is determined at compile time

> [!NOTE] Naming convention for Class Attributes
> _camelCase

## Readonly
- Does not need to be initialized at cration like const
- Can be changed only in the constructor
- ==Runtime constant==
	- Its value is determined at runtime

---
# Static class
- ==Static class== :
	- all members must be static
	- Can't create instance of the static class (can't be instantiated)
	- ==The constructor of the static class is called only once in the entire program (first time you use the static class)==
	- ==The constructor is always public and static by default==
- <mark style="background: #ADCCFFA6;">Non static class</mark>:
	- It's ok to have both static and nonstatic members
	- 
---
# Variable scopes
[[Drawing 2025-01-19 14.53.14.excalidraw]]
## Class level
- If the method is static, it can only access *static attributes/properties of the class*
- Variable decalred on the class level, is seen in the entire class
- ==Can be overriden in a method in the class as the following==
  ==![[Pasted image 20250119144620.png]]==
  ==The console will write "Mohammed" here, but if i want it to write "My name", just print  _name variabe directly without Program_==
## Method level
- You can create a variable in the method but I will not be seen outside this method
- ==A variable in a method can be named same as a variable in the class level==
## Block Level
- ==A variable in a block in a method, can't be named same as a variable in the method level.==
---
#  ==ref vs out Keywords (related to *pass by value* and *pass by reference*)==
## Converting passing by value to passing by reference
- We do that by adding either `ref` or `out`
	- before the passed parameter in the function itself
	- Before the passed parameter in the calling of the function
## What 's the difference between ==ref== and ==out==
- Ref
	- Must be initialized before passing
- Out
	- ==Does not need to be initialized==
	- <mark style="background: #FF5582A6;">BUT</mark> The method called must assign a value to the out parameter in all cases, otherwise error will arise.
## TryParse Method
```c#
int num = 0;
bool isSuccessful = int.tryParse(Console.ReadLine(),out num)

```
---
# EXCEPTION HANDLING
- Rule Of Thumb : if you can just fix the error, just fix it and avoid exceptions.
  
- "Exception" class is extended to a lot of other exception classes
	- `toString()` method.
- Types of Errors
	- Compile error
	- Runtime error (Exceptions)
	- Logical Errors

- We handle exceptions  through try/catch blocks | try/catch/finally
- ==Finally Block :== ALWAYS executes either an exception happens or not.
![[Pasted image 20250119160133.png]]
- If the code in the try block is crashed, the code in the try block  after the crash won't execute.
- ==Throwing exceptions==
  ![[Pasted image 20250119161151.png]]
---
# enums
## Enum creation
![[Pasted image 20250119162146.png]]
- Notice that when you assign a number to an enum member, ==only the members afterwards== are affected.
  
- To get the integer value ![[Pasted image 20250119162953.png]]
## Enum class
### GetNames (), Parse ()
```c#
Enum.GetNames(typeof(Gender)) //returns an array of the gender values in the enum

Enum.Parse(typeof(Gender),"male") //will return a gender type
```
---
# Flags Enum 
![[Pasted image 20250119172725.png]]
- ==Bitwise operations== : & | ^ ~
- ![[Pasted image 20250119175632.png]]
---
# Training apps : File system Command Line
## Listing directories and files
- System.Io namespace
- `Directory. GetDirectories (a path string)` 
	- You can pass an optional arguement that represents a search pattern
	  ![[Pasted image 20250121232907.png]]
	  The two astris say -> get me any directories that include the word "Training"
	  The Same Applies to `GetFiles()` method
- `Directory. GetFiles (a path string)`
- `Directory. GetFileSystemEntries` : return both directories and files
##  Getting info about directories or files
- `var dirInfo = new DirectoryInfo(path)`
- `var fileInfo = new FileInfo(path)`
The objects created have all the info we would need
## Check if file/folder exist
`File.Exists(path)`
## Creating directory
Creates a directory at the given path.
`Directory.CreateDirectory(path)`
## Printing a file
- `File.ReadAllText(path)`
- `File.ReadAllBytes(path)`
## Delete a Directory
- `Directory.delete(path,recursive=true)` : deletes the directory and its content
- `Directory.delete(path)` : Deletes ONLY an EMPTY directory
---
# Training App : Simple Maths Expression Evaluator
- Like creating first two phases in a compiler (lexical Analysis - Syntax Analysis) -> building our syntax tree for a maths expression
- Learned the usage of classes in a real problem
- Learnt parsing characters one by one and extracting tokens.
---
# Abstract Classes
## Syntax
- Inheritance ![[Pasted image 20250122162458.png]]
- You declare a class or a method abstract through adding `abstract` keyword after the access modifier.
- You MUST use `override` keyword in the ==subclass/child class/derived class== to override the method in the ==super/base/parent class==
## Sealed keyword
- A `sealed` class can't be inherited
  
*Multiple inheritance is prohibited in c#*

---
# Virtual and Protected Members

> [!NOTE] Overriding methods
> You can ONLY override either *virtual* or *abstract* Methods of the parent class
> 
- **==Base Keyword :==** You can access the elements in the base class from the child class  using `base.` keyword [something like `super` keyword in java]
  ![[Pasted image 20250122163737.png]]
---
# <mark style="background: #FF5582A6;">Member Hiding/Shadowing</mark>
- In the base class you don't use the `virtual` keyword
- In the child class you  don't use `override` keyword, instead you use `new` keyword.
- What difference does this make:
	- When variable type is the base class : You Access the base class method
	- When the  variable type is the child class : you access the child class method.
- So *methods accessed* change based on *the variable/reference type*.
- 
---
# Interface
- You ***==inherit==*** a class but you ***==implement==*** an interface
- .NET core is highly dependent on dependency injection design pattern

> [!NOTE] Important Note regarding abstract Classes and Interfaces
> ![[Pasted image 20250123182843.png]]

## What is an interface ?
- Interface is a contract between
	- Client code / The code that use those methods/properties
	- The code that implements these methods/properties
- Some Interfaces define a characteristic of a class like `edible,restartable,etc..`

## Methods
- Methods are  `public abstract` by default (you don't write them)
## Properties
## Classes that Implement an interface
- Methods must be kept public as you can't narrow the access modifier

## Naming Convention
- Name the interface like I + name of the interface 
	- Example `IDevice, IHome, IPerson`

## Implicit / Explicit Implementation
![[Pasted image 20250123183232.png]]
If the ==Reference Type== Is:
	==Interface== (IDevice): call the explicit Method.
	==Subclass== (Computer): Call the Implicit Method.
When do we use it ?
	If the class implements two interfaces and there's a method in both interfaces, so you want to make an implementation of the method when the reference type is an interface AND another implementation when the reference type is the other interface AND another implementation when the reference type is the subclass itself.
## Interface vs Abstract Class
- Abstract classes have constructor, Interfaces don't
- You can implement multiple interfaces, but inherit only one class
- 
### Before C# 8
- You can't write code in Interface methods
- All methods are public
### After C# 8
- You can write code in interface methods (Default Implementation)
- You can add access modifiers to methods/members.
- You can add field/attributes (static by default)
---
# ArrayList
- NOT fixed size
- NOT strongly typed (takes "object" type)
- Values of the ArrayList are boxed into Object
- Declaration : `ArrayList list = new ArrayList()`
1. Add
	- `list.add(anything/anytype)`
	- Adding a collection of elements to the array
	    `list.addRange(new int[]{1,2,3})`
	    
2. `Insert (index, value)`
3. `InsertRange ()`
4. `Remove ()` : remove the first element that matches tha passed parameter
5. `RemoveAt ()` : remove the element at the passed index
6. `RemoveRange ()` : takes the *start index* and the number of elements to remove from this *start index*
7. `IndexOf(value,OPTIONAL start index to search from)` : return the index of that value, returns -1 if not found
8. 
## ==Boxing and Unboxing==
- Boxing (value -> Object) ![[Pasted image 20250123203549.png]]
- Unboxing through ==type casting== ![[Pasted image 20250123203634.png]]

---
# Generic List 
- "Generics" is an advanced topic
- Works with arrays under the hood, *not Linkedlists*
- `var list = new List<int>()`
	- Takes one type only
	- Doesn't require unboxing unlike ArrayList.
- `list.Capacity` : to set, get the capacity
- Methods : Add, AddRange, Insert, InsertRange, Clear, Remove, RemoveAt, IndexOf, Contains().
# Dictionary/Map/HashMap
- `var dict = new Dictionary<string,string>()`
- Appending a key value pair `dict.Add("gmail","ahmedfakhr59@gmail.com")`
- Getting a value :  `dict["gmail"]`
- `ContainsKey()` : important to check if the key is already there or not
- <mark style="background: #FF5582A6;">To add or read a value from a dictionary, you need to add a check to see if it's there or not to avoid crashing</mark>
- Methods that start with "Try" like TryParse, TryGetValue
	- return a boolean
	- If it succeeded, you pass a variable with "out" to output the value in this variable ![[Pasted image 20250123213647.png]]

> [!NOTE] Advice
> Open Source Code and look at it, very very helpful

---
# Stacks and Queues
```c#
var stack = new Stack<int>();
stack.Push(1)
stack.Pop()
stack.Count // number of elements in the stack
stack.Peek()

```
---
# Training App
- 
