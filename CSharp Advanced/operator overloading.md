- You have a class you just created and want it to support add, sub, multiply/divide operation in a certain behaviour.
- How to do it ?
	1. Public
	2. Static
	3. <ReturnType\>
	4. Operator
	5. +
```C#
public static Point operator +(Point p1,Point p2){ //must be PUBLIC STATIC
return new Point(p1.x+p2.x,p1.y+p2.y);
}
```
# Comparison Operators
- They are defined in pairs
	- If you implement >, you mist implement <
	- If you implement >=, you mist implement <=
	- If you implement \==, you mist implement !==
```C#
public static bool operator >(Point p1,Point p2){
return p1.x>p2.x || p1.y>p2.y;
}
public static bool operator <(Point p1,Point p2){
return p1.x<p2.x || p1.y<p2.y;
}
```


> [!NOTE] Note
>  == operator is defined by default on objects since it compares the references of the two objects NOT the actual object value.
# ==Conversion Operatorsc==
- Basically defines the behavior of the object when assigned a value other than its own type
	For Example `Point p = 5;`
- Implicit Conversion
```C#
public static implicit operator Point(int x){
return new Point(x,x);
} 
//Example: Point p = 5;
```
- Explicit Conversion
```C#
public static explicit operator Point(int x){
return new Point(x,x); //Example: Point p = (Point)5;
}
```
