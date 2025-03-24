# Joins (Similar to SQL Inner Join)
```c#
Var query = from employee in employees
join department in departments
on employee.DepartmentId equals department.Id
Select new {EmployeeName = employee.Name,DepartmentName = department.Name}
```
- Similar to "Inner Join" in SQL, the deprtmentID value must exist in both lists in order to show up in our query
## Method Syntax
```C#
Var query = employees.Join(departments,e=>e.DepartmentId,d=>d.Id,(e,d)=>new{EmployeeName=e.Name,DepartmentName = d.Name})
```
---
# Group     By
```C#
var query =  from employee in employees
group employee by employee.DepartmentId

foreach(var group in query){
//
var employeeNames = string.join(",",group.select(x=>x.Name).ToArray())
//printing each group details
Console.WriteLine($"Group {group.Key} : {employeeNames}")
}
```
- **==*Returns SEVERAL groups/lists*==** of employees, ==***each group has a unique departmentId (aka. Key)***==
---
#interviewQuestion 
Difference between Iqueriable and Ienumerable
Ienumerable:
You have your actual  data in memory, you can operate on it right away
IQueryable:
You don't have the actual data yet, the data is remotely stored in a database for example AND you only have the data model.



> [!NOTE] Select Method
>  - The `Select` method in LINQ requires a **lambda expression** or a **delegate** to specify how to project each element in the collection.
>  - `Name` alone is not a valid expression or delegate. It must be wrapped in a lambda expression (e.g., `x => x.Name`).
