```C#
var result = from number in Numbers
			 order by number
			 where number > 2
			 select number
			 
			 
var result = from number in Numbers
			 order by number ascending
			 where number > 2
			 select number
			 
var result = from number in Numbers
			 order by number descending
			 where number > 2
			 select number
			 

var result = Numbers.OrderByAscending(x=>x).Where(x=>x>2);
//-----------------------------------------------------------------
// Can we change order between order and where ?
/**YES, basically if order before where, It will order then filter
but when we write order after where, It will order the filtered results WHICH IS BETTER.
**/
var result = from number in Numbers
		     where number > 2
			 order by number
			 select number
			 
```

## Orderby thenby
```C#
query = employees.OrderBy(x=>x.Name).ThenBy(x=>x.Age).ThenBy(x=>x.Salary);
//Same As
query = from employee in employees orderby employee.Name,employee.Age,employee.Salary select employee
```

## orderby orderby VS orderby thenby

- Same result but
	- Orderby thenby has BETTER Performance
	- More readable and expressive
## Reverse ()
- Simply Reverse the list
- ==ONLY done in method sentence.==

```c#
query = employees.OrderBy(x=>x.Name).ThenBy(x=>x.Age).ThenBy(x=>x.Salary).Reverse();
```

## Selecting specific Object members

```C#
query = employees.OrderBy(x=>x.Name).ThenBy(x=>x.Age).ThenBy(x=>x.Salary).Reverse()
.Select(x=>new{x.Name,x.Age});
//similar in syntactic sugar
var query = from e in employees orderby e.Name, e.Age, e.Salary descending select new { e.Name, e.Age };
/**
Here we created ANONYMOUS Object with fields Name,Age and ignored the salary field.
**/
```
## OfType
```C#
// Given that employees is a class and we have 2 other classes that extend the employee class named contractor and ceo
//and i want to filter based on this class
query = employees.OfType<Contractor>().OrderBy(x=>x.Name).ThenBy(x=>x.Age).ThenBy(x=>x.Salary).Reverse()
.Select(x=>new{x.Name,x.Age});

query = employees.Where(x=>x is Contractor).OrderBy(x=>x.Name).ThenBy(x=>x.Age).ThenBy(x=>x.Salary).Reverse()
.Select(x=>new{x.Name,x.Age});
//Conclusion
OfType<Contractor>() //Same as
Where(x=>x is Contractor)
```
### Difference between OfType and Where
- **OfType\<Contractor>()**
  - Filters the collection **and** casts items to `Contractor`
  - Returns `IEnumerable<Contractor>`.

-  **Where (x => x is Contractor)**
  -  **Only** filters items by type.
  - Returns the original type (e.g., `IEnumerable<Employee>`), so manual casting is needed.

---
# Aggreagators
Count
Count elements matching a condition
Count all elements that are members of a group

Sum numeric elements
Sum a projection from a sequence `double totalChars = words.Sum(w => w.Length);`

Minimum of a sequence
Minimum of a projection `int shortestWord = words.Min(w => w.Length);`
Minimum in each group
==Finding elements matching the minimum==
```C#
var categories = from p in products
group p by p.Category into g
let minPrice = g.Min(p => p.UnitPrice)
select (Category: g.Key, CheapestProducts: g.Where(p => p.UnitPrice == minPrice));
```

Maximum of a sequence
Maximum of a projection
Maximum in each group
Finding elements matching the maximum

Average of a numeric sequence
Average of a projection
Average in each group

1. Aggregate value from all elements of a sequence
2.  `double product = doubles.Aggregate((runningProduct, nextFactor) => runningProduct * nextFactor);`
3.  
   ```C#
double endBalance =
attemptedWithdrawals.Aggregate(startBalance,
(balance, nextWithdrawal) =>
((nextWithdrawal <= balance) ? (balance - nextWithdrawal) : balance));
```

Sequence Operations
1. SequenceEqual
2. Concat
3. Zip -> used for performing operations between 2 sequences and return a result sequence
   `int dotProduct = vectorA.Zip(vectorB, (a, b) => a * b).Sum();`

Lazy and eager execution
```C#
// Sequence operators form first-class queries that
// are not executed until you enumerate over them.
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };
int i = 0;
var q = from n in numbers
select ++i;
// Note, the local variable 'i' is not incremented
// until each element is evaluated (as a side-effect):
foreach (var v in q)
{
Console.WriteLine($"v = {v}, i = {i}");
}
```
```C#
// Methods like ToList() cause the query to be
// executed immediately, caching the results.

  

int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };

  

int i = 0;

var q = (from n in numbers

select ++i)

.ToList();

  

// The local variable i has already been fully

// incremented before we iterate the results:

foreach (var v in q)

{

Console.WriteLine($"v = {v}, i = {i}");

}
```



