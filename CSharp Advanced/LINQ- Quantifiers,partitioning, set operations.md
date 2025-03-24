# Quantifiers
- Return Boolean always.
- They are immediate execution methods
## ==All==
- All items must satisfy the condition
`var result = numbers.All(x=>x>0)`
## ==Any==
- If any item satisfy the condition, it returns instantly and doesn't continue with the rest.
- Returns True, if it met an item that satisfies the condition
### Any (without a condition)
- Returns true if the list has items.
- Returns false if the list is empty
## ==Contains==
### For primitive data types
- Searches for a value in the list
	- Found returns True
	- Not Found returns False
 `var result = numbers.Contains(50)`
### For Objects
- Checks for reference equality NOT value.

---
# Partitioning/Pagination (not supported in sugar syntax/Query Syntax)
- Returns first 4 elements of the list.
	- `var result = numbers.Take(4)`
- Takes Last 4 elements
	- `var result = numbers.TakeLast(4)`
- Skip and Take
	`var result = numbers.Skip(6).Take(4)`
	- Skip 6 elements and take the 4 after those 6.
- TakeWhile()
	- Takes the elements as long as they satisfy the condition, once it hits an element that doesn't, it finishes.
	- `var result = number.TakeWhile(x=>x>7)`
- SkipWhile()
	- Skip as long as a certain condition is satisfied.
- SkipLast ()
	- Skip last n elements.
- Chunck()
	- Takes a list and resturns several lists
	- `var chuncks = numbers.Chunck(3)` split the array into several arrays, each one has 3 elements.
	- Final chunk may have fewer elements if the total isn’t divisible by the chunk size.
	- Useful for parallel processing (splitting data into several chuncks and give each thread a chunck)
- Set

---
# Set Operations

- Distinct() -> used with primitive DataTypes
	- 
- Except () -> used with primitive DataTypes
	- `var query = numbers.Except(new List<int>{1,2,3}).OrderBy(x=>x)`
	- **returns** elements of *the numbers list* that are not in *the second list*
-  Intersect ()-> used with primitive DataTypes
	- `var query = numbers.Intersect(new List<int>{1,2,3}).OrderBy(x=>x)`
	- **Returns** elements that are ==*common*== in both lists.
- Union()
	- `var query = numbers.Union(new List<int>{1,2,3}).OrderBy(x=>x)`
	- Combines both lists BUT the common items between the two lists are mentioned only ONCE.
- DistinctBy () -> used with Objects
- ExceptBy () -> used with Objects
-  IntersectBy ()-> used with Objects
---
### Find the first element

This sample uses `First` to return the first matching element as a `Product`, instead of as a sequence containing a `Product`.
```C#
List<Product> products = GetProductList();

Product product12 = (from p in products
where p.ProductID == 12
select p)
.First();
Console.WriteLine(product12);

// returns the first element, or the default value if the array is empty
int firstNumOrDefault = numbers.FirstOrDefault();
Console.WriteLine(firstNumOrDefault);

```
### Find the first matching element

This sample uses `First` to find the first element in the array that starts with 'o'.
```C#
string[] strings = { "zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine" };
string startsWithO = strings.First(s => s[0] == 'o');
Console.WriteLine($"A string starting with 'o': {startsWithO}");
// returning first matching element or default.
Product product789 = products.FirstOrDefault(p => p.ProductID == 789);
```
### ElementAt (int index)

### Generating Sequences
##### **Key Differences**

| Method                            | Purpose                               | Example                                           |
| --------------------------------- | ------------------------------------- | ------------------------------------------------- |
| `Enumerable.Range(start, count)`  | Generates a sequence of numbers       | `Enumerable.Range(1, 5) → {1, 2, 3, 4, 5}`        |
| `Enumerable.Repeat(value, count)` | Repeats the same value multiple times | `Enumerable.Repeat("Hi", 3) → {"Hi", "Hi", "Hi"}` |


## Group by all elements matching a condition

This sample uses `All` to return a grouped a list of products only for categories that have all of their products in stock.
```C#
List<Product> products = GetProductList();
var productGroups = from p in products
group p by p.Category into g
where g.All(p => p.UnitsInStock > 0)
select (Category: g.Key, Products: g);




foreach (var group in productGroups)
{
Console.WriteLine(group.Category);
foreach (var product in group.Products)
{
Console.WriteLine($"\t{product}");

}

}
```