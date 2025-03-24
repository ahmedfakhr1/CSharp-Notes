- MySql -> Database engine / database management system
- SQL -> query language
- Linq works with collections or anything that implements "IEnumerable interface"
# TOC :
- Introduction
- Projection & filtering (select, where, OfType)
- Sorting (OrderBy, OrderByDescending, ThenBy, ThenByDescending, Reverse)
- Quantifiers (All, Any, cointains)
- Partitioning (Skip, skipWhile, Take, TakeWhile, Chunck)
- Set operations (Distinct, DistinctBy, Except, ExceptBy, Intersect, IntersectBy, Union, UnionBy)
- Joins (Join, GroupJoin)
- Grouping (GroupBy, ToLookup)
---
> Functional Programming ?

- LINQ Query Expression always *starts with* `from`
```C#
//Syntactic Sugar
Var result =  from number in numbers 
			  where number>5 
			  select number
			  
//what actually gets executed.
var result = numbers.Where(x=>x>5) //Same result as above
//takes   a delegate/a function    that   takes int   and   return bool.
//Where here is an Extension Method.
```
## Deferred Vs Immediate Execution
- #interviewQuestion ***result value changes*** AUTOMATICALLY WHENEVER ***Numbers change*** through what is called ==**deferred execution**==
	- Result stores the orders, ==*whenever Result is called or checked*==, it executes the order and give me the result.
- How to make it **==immediate execution==** : 
- ```Var result =  (from number in numbers 
			  Where number>5 
			  Select number).ToList();
			  ```
- NOTE : Aggregate functions do **==immediate execution==** 
---
```C#
//Filter Customers first
List<Customer> customers = GetCustomerList();

DateTime cutoffDate = new DateTime(1997, 1, 1);
var orders = from c in customers
where c.Region == "WA"
from o in c.Orders
where o.OrderDate >= cutoffDate
select (c.CustomerID, o.OrderID);

foreach (var order in orders)
{
Console.WriteLine($"Customer: {order.CustomerID}, Order: {order.OrderID}");

}
```