
> [!NOTE] Title
> VERY VERY VERY Important
- Anything i can loop over is **enumerable***
- How to  make my object enumerable
	1. In the class that i want to loop over its objects
		1. Data member : a generic list for example or anything that i can loop over naturally
		   `private readonly List<PayItem> _payItems = new()`
		2. A `GetEnumerator()` method 
		   ```C#
		   //METHOD 1
		public IEnumerator<PayItem> GetEnumerator(){
		return _payItems.GetEnumerator();_
		}
		//Note that the enumerator is STATEFUL, so best practice if you're making a CUSTOM enumerator, return a new object of it every time.
		
		//METHOD 2
		//Another version with custom enumerator
		public IEnumerator<PayItem> GetEnumerator(){
     		return new payItemsEnumerator(_PayItems);
     		}
     		
     		//METHOD 3
     		//Finally The Actually True way of creating enumerators
     	public IEnumerator<PayItem> GetEnumerator(){
     		foreach(item in _payItems){
     		yield return item;
     		}
     	}
		
		   ```
CUSTOM Enumerator
MoveNext () is called first (this why \_CurrentIndex = -1)
![[Pasted image 20250210220130.png]]
	3. Recommended : Implement the `IEnumerable`  Interface OR `IEnumerable<PayItem>` generic interface.
## Yield

> [!NOTE] Note
> Iterator Methods : methods that have "Yield" = is not called until **loop** is executed.
****
## Foreach vs normal For loop
- Foreach works fine as we saw
- For
	- ==***Indexer property***== : `public PayItem this[int index] {get => _payItems[index]}` Add this member to your class (from which you create objects that you can iterate over)



---
# => 
## Constructors or methods with a single line
`public Circle(double radius) => _radius = radius;`
## Data members 
`public double Area => Math.PI * _radius * _radius;`

## Creating anonymous functions
```C#
Func<int, int> square = x => x * x;
int result = square(5); // result is 25
```

---
# Delegates Revisited
- Delegates are often compared to function pointers in languages like C or C++
- Object Oriented - Type Safe - Secure
- To ***define*** a delegate, you specify **the return type** and **parameters** that the delegate will encapsulate
public delegate int PerformCalculation(int x, int y);
`public delegate int PerformCalculation(int x, int y);`
```C#
public class Calculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
    public int Subtract(int a, int b)
    {
        return a - b;
    }
}

public class Program
{
    public static void Main()
    {
        Calculator calc = new Calculator();

        // Instantiate the delegate to reference the Add method
        PerformCalculation calcDelegate = calc.Add;

        int result = calcDelegate(5, 3); // result is 8

        // Reassign the delegate to reference the Subtract method
        calcDelegate = calc.Subtract;

        result = calcDelegate(5, 3); // result is 2
    }
}

```
## multicast delegates
Simply using `+` operator you can add more than one function to the same delegate,
And when the delegate is called, all functions are triggered in the same order.

```C#
public delegate void Notify(string message);

public class Messenger
{
    public void DisplayMessage(string message)
    {
        Console.WriteLine(message);
    }

    public void LogMessage(string message)
    {
        // Code to log the message
    }
}

public class Program
{
    public static void Main()
    {
        Messenger messenger = new Messenger();

        Notify notifyDelegate = messenger.DisplayMessage;
        notifyDelegate += messenger.LogMessage;

        notifyDelegate("Hello, World!");

        // Output:
        // Hello, World!
        // (Message is also logged)
    }
}

```
