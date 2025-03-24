# Extension Methods
- Used to *add a behavior(a method for example)* to any *type*(int type for example or dateTime or anything.)*
## How to do it ?
- Create a static class
- Add static method that returns the new value (add ==*the keyword **this***== before the value you will do operations on.)
  ![[IMG-20250214171305508.png]]
- Now you can use the method on the value directly![[IMG-20250214171305800.png]]
Now It's like you have added a method to the `int` class.

## What's "method chaining"
Calling a method on the return of another method
Ex:  `"Ahmed Fakhr".RemoveWhiteSpaces().Reverse();`

## Naming of Extension method
Make sure that the extension method name does not conflict with a method name of the class, because the member method will have higher priority in execution.
## General
- `Ahmed Ahmed Ahmed. Replace ("Ahmed","");`
  This line of code removes ==ALL== Occurrences of "Ahmed"
  
---
# Recursion
> Everything that can be done with recursion can be done with loops
## When Recursion is really useful
- I have a hierarchy and I don't know the limit of this hierarchy, like a tree that i don't know its depth for example.
- Example you want to recursively print the content of each file in a folder and the subfolders in this folder. You don't know all the details of this folder hierarchy
## Side Notes
- Creating a repetition of a string `new String(-,levels)` where *levels* are an integer.
---
# Delegates (Sounds Really Important)(Gives you so much flexibility)
#cleanCode try to make your if-else statement only have if and else and no more.
#cleanCode try to make your methods closed to modification, open for extension
- 

```C#
namespace C__Advanced
{
    internal class Program
    {
        
        static void Main(string[] args)
        {
        	//Step 3 : Usage of The Delegate in different ways
            int num1 = 10;
            int num2 = 20;
            //Different ways to call a function with a delegate parameter.
            //1
            Console.WriteLine(CalculateWithDelegate(num1, num2, Add));c
            //2
            Console.WriteLine(CalculateWithDelegate(num1, num2, delegate (int num1,int num2) { return num1 - num2; }));
            //3
            Console.WriteLine(CalculateWithDelegate(num1, num2, (int num1,int num2)=>num1*num2));// Lambda Expression/Arrow Function
            //4
            Console.WriteLine(CalculateWithDelegate(num1, num2, (num1,num2)=> num1 * num2));// Lambda Expression/Arrow Function
        }


        //Step 1 is creating our delegate, It's like writing the signature of a method in an interface, but add the keyword delegate
        
        public delegate int CalculateDelegate(int a, int b); //the parameters AND Return Type same as Add,Subtract,Multiply,Divide
        
        //Step 2 : Pass the Delegate you created to the method
        public static int CalculateWithDelegate(int item1, int item2, CalculateDelegate del) //CalculateDelegate is a method pointer
        {
            int result = del(item1,item2);
            return result;
        }
        /**
         * Bad Version
         * public static int Calculate(int item1,int item2,char operation) {
            int result = 0;
            if (operation == '+')
                result = item1 + item2;
            else if (operation == '-')
                result = item1 - item2;
            else if (operation == '*')
                result = item1 * item2;
            else if (operation == '/')
                result = item2 / item2;
            else
                throw new ArgumentException("Invalid operation !");
            return result;
        }**/
        public static int Add(int item1, int item2)
        {
            int result = item1+item2;
            return result;
        }
        public static int Subtract(int item1, int item2)
        {
            int result = item1-item2;
            return result;
        }
        public static int Multiply(int item1, int item2)
        {
            int result = item2*item2;
            return result;
        }
        public static int Divide(int item1, int item2)
        {
            int result = item1/item2;
            return result;
        }
    }
}

```
## Multicast feature of delegates

- One delegate calling multiple methods at the same time
	`Console.WriteLine (CalculateWithDelegate (num 1, num 2, Add+Subtract+Multiply-Add)); `
	It wil call all of these, but the one that will return its value is `Multiply` since it's the last one to be invoked
```c#

//Another Example
namespace C__Advanced
{
    internal class Program
    {
        public class Employee {
            public string Name { get; set; }
            public int BasicSalary { get; set; }
            public int Deductions { get; set; }
            public int bonus { get; set; }

            /**
             * Say you want to filter the salaries being Displayed
             * 1. >2000 & <5000
             * 2. for people who have birthdays in Jan
             * etc
             * 
             * Including a paramter to this function will tight-couple the business rule to the method
             * which is not acceptable.
             * 
             * How To Solve it ?
             * Delegates, How ?
             * you create a delegate that takes an employee object and return a boolean to decide to calculate the salary
             * for that employee or not.
             * 
             * Notice : Delegates that return boolean is called "Predicate"
             * **/

            public delegate bool Predicate(Employee e);
            public static void CalculateSalaries(List<Employee> employees,Predicate predicate)
            {
                foreach (Employee emp in employees)
                {
                    if (predicate(emp))
                    {
                        var Salary = emp.BasicSalary + emp.bonus - emp.Deductions;
                        Console.WriteLine("Salary is " + Salary);
                    }
                }
            }
        }
        static void Main(string[] args)
        {
            List<Employee> employees = new List<Employee>();
            for (int i = 0; i < 100; i++) {
                employees.Add(new Employee
                {

                    Name = $"{i}",
                    BasicSalary = Random.Shared.Next(1000, 5001),
                    Deductions = Random.Shared.Next(0, 500),
                    bonus = Random.Shared.Next(0, 10001)

                });
            }
            Employee.CalculateSalaries(employees,(Employee e) => { return e.BasicSalary <= 2000; });



        }
    }
}

```

---
# Events

- Something happened, you raised the event (broadcast it in the microphone).
- Very usefull in keeping the single responsibility priniciple for every class
	- Ex: a class has a single mission(calculating salary), when he does this mission, It will say it did and has nothing to do with anything else(printing/logging the salary for example).'
## Implementation of Events
- Every Event must have a delegate.
- Trigger/raise/fire an event.
- Event Handler : The code the will be executed when the event happens.
#GeneralCodingAdvice someObject?. Method (param 1, param 2); // ? Method () won't be called if EmployeeSalaryCalculated is null.

Focused publisher code
```c#
//Step 1 : Creating a delegate to represent the signature of the event handler
//event handlers don't return data // this is why it's almost always `void`
delegate void EmployeeSalaryCalculatedEventHandler(Employee employee,int salary);
//Step 2 : Create the Event
//EmployeeSalaryCalculatedEventHandler identifies the signature of the event handler.
public event EmployeeSalaryCalculatedEventHandler EmployeeSalaryCalculated;
//Step 3 : Fire the Event
EmployeeSalaryCalculated?.Invoke(emp, Salary); // ? Invoke() won't be called if EmployeeSalaryCalculated is null.
```

Entire publisher Code
```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using static C__Advanced.Program;

namespace C__Advanced
{
    internal class SalaryCalculator
    {
        //Step 2 : Create the Event
        //EmployeeSalaryCalculatedEventHandler identifies the signature of the event handler.
        public event EmployeeSalaryCalculatedEventHandler EmployeeSalaryCalculated;

        public delegate bool Predicate(Employee e);
        public void CalculateSalaries(List<Employee> employees, Predicate predicate)
        {
            foreach (Employee emp in employees)
            {
                if (predicate(emp))
                {
                    var Salary = emp.BasicSalary + emp.Bonus - emp.Deductions;
                    //Step 3 : Fire the Event
                    EmployeeSalaryCalculated?.Invoke(emp, Salary); // ? Invoke() won't be called if EmployeeSalaryCalculated is null.
                }
            }
        }
    }
    //Step 1 : Creating a delegate to represent the signature of the event handler
    //event don't return data // this is why it's almost always `void`
    delegate void EmployeeSalaryCalculatedEventHandler(Employee employee,int salary);
}

```

Focused subscriber code
```c#
//Step 1 (Multicast Delegate)
            Calculator.EmployeeSalaryCalculated += LogEmployeeSalary;
            Calculator.EmployeeSalaryCalculated += (employee,salary)=>Console.WriteLine($"Payslip sent to emplyee {employee.Name}");
//Step 2 : Implementation the handler
        private static void LogEmployeeSalary(Employee employee, int salary)
        {
            Console.WriteLine($"Salary for employee {employee} = {salary}");
        }     
```


Entire Subscriber Code

```c#
namespace C__Advanced
{
    internal class Program
    {
        static void Main(string[] args)
        {
            List<Employee> employees = new List<Employee>();
            for (int i = 0; i < 100; i++) {
                employees.Add(new Employee
                {

                    Name = $"{i}",
                    BasicSalary = Random.Shared.Next(1000, 5001),
                    Deductions = Random.Shared.Next(0, 500),
                    Bonus = Random.Shared.Next(0, 10001)

                });
            }
            var Calculator = new SalaryCalculator();
            //Step 1 (Multicast Delegate)
            Calculator.EmployeeSalaryCalculated += LogEmployeeSalary;
            Calculator.EmployeeSalaryCalculated += (employee,salary)=>Console.WriteLine($"Payslip sent to emplyee {employee.Name}");
            Calculator.CalculateSalaries(employees,(Employee e) => { return e.BasicSalary <= 2000; });
        }
        //Step 2 : Implementation the handler
        private static void LogEmployeeSalary(Employee employee, int salary)
        {
            Console.WriteLine($"Salary for employee {employee} = {salary}");
        }
    }
}

```

---
# Multithreading Basics

- Thread : Single Sequention flow of activities.
- #advice By default any thread that you make, make it ==*background thread*==.
- Main thread: any process has main thread that first starts that executes the code of this process.
- Operations that take long time better seperated in a seperate thread other then the main thread.
- The Goal of Multithreading is to increase responsiveness of the app to the user, no the performance of the app.
- ***==Reverse effect :==*** Increasing threads, can increase context switching which may affect the performance
- ==Foreground threads vs background threads==
	- `th1.IsBackground = true` to make the thread background thread
	- WHAT IS BACKGROUND THREAD ? A normal thread but when the main thread ends or the user ends the program, the program will end and we won't care about that thread
	- By default any thread that you make, make it background thread.
- 

## Demo
- The Method that is executed by the thread is takes ***no args*** or ***one arg of type object***.
- Context switching
- Threads take turns on the cores of the cpu
```c#
//creation of thread
var thr1 = new thread(ProcessBatch1); //ProcessBatch1 and ProcessBatch1 are methods
var thr2 = new thread(ProcessBatch2);

// starting the thread
thr1.Start();
thr2.Start();

//How to create a lock in c#
private static Object _lock = new Object();

private static void ProcessBatch1(){
//Add the code you want to be executed without interruption in the lock block
lock(_lock){
Console.ForegroundColor = ConsoleColour.red;
for (int i = 0;i<1000;i++){
Console.WriteLine(i)
}
Console.ForegroundColor = ConsoleColour.white;
}

}
private static void ProcessBatch2(){

lock(_lock){
Console.ForegroundColor = ConsoleColour.green;
for (int i = 1001;i<2000;i++){
Console.WriteLine(i)
}
Console.ForegroundColor = ConsoleColour.white;
}

}

```

## ==Another way to create+start+make the thread background thread threads==
```c#
ThreadPool.QueueUserWorkItem(ProcessBatch1);
ThreadPool.QueueUserWorkItem(ProcessBatch2);
```
### Cancellation of threads using ==cancellation token==
1. Create a cancellatin token
2. Pass the token to the threads
3. Whenever you call `cts.cancel()`, threads will stop.
![[IMG-20250214171306153.png]]
![[IMG-20250214171306408.png]] ``
To make cancel request to the threads =>  `cts.cancel();`

## ==Thread Priority==
`thr1.Priority= ThreadPriority.Lowest;`
`thr2.Priority= ThreadPriority.Highest;`



---
# Task-Based Asynchronous pattern (TAP)

- Task : Code Block that will be executed asynchronously.
- Synchronous : blocking.
- Asynchronous : non-blocking.
## Task. Run ()
1. **Usage**:
    
    - You pass a delegate (e.g., a lambda expression or method) to `Task.Run`, which contains the code to execute asynchronously.
        
2. **Returns a `Task`**:
    - The returned `Task` can be awaited using the `await` keyword, making it easy to work with asynchronous programmin
```c#
Task.Run(() => PerformCalculation(5, 10)); // Example
// The `PerformCalculation` method is executed asynchronously on a background thread.
```
## General
- Make The method you want to execute asynchronously : to return ==***Task***== .
- Adding async to the method signature is like it's void, I don't have to return anything
- ***==Await==*** is used to wait for another task to finish
	- Only used in a `async Task` function
- A Scenario : you are in the main thread, in `ProcessBatch()` function which is an async function
	- There's `await` line in this method
	- All code BEFORE the `await` line is executed synchronously in the main thread (aka. *Caller Thread*)
	- All Code AFTER the `await` line : is put on a new thread and gets blocked until the task in the `await` line is finished AND the control goes back to the caller thread (main thread) to continue execution.
	- Explainatory diagram ![[IMG-20250214171306633.png]]
## Awaiting on multiple tasks
1. `await Task.WhenAll(task1,task2)`
2. When any of the tasks is finished, continue the execution `await Task.WhenAny(task1,task2)`
3. 
## Continuation

> [!NOTE] Note
> If the task returns result(integer for example), if you want the result, you need to await the task.

![[IMG-20250214171307090.png]]

## Task Status

## Task Cancellation
![[IMG-20250214171307447.png]]
#advice Use a single cancellation token for all your tasks
- When you await on a  task that supports *cancelltion*, await in a try/catch block.
---
