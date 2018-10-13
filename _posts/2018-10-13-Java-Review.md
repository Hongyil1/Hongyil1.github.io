---
layout:     post
title:      Java Review 1
subtitle:   prepare for interview
date:       2018-10-13
author:     Hongyi
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Java
---

# Getting start
## Compilation
**javac** is the Java compiler included in the Java Development Kit(JDK) from Oracle. The compiler accepts source code written by user in Java language and produces Java bytecode conforming to the Java Virtual Machine(JVM).

A **.class** file is a compiled **.java** file. **.java** is all text and is human readable. **.class** file is for JVM.

<img width="231" alt="capture" src="https://user-images.githubusercontent.com/22671087/46899227-783a1700-cedc-11e8-93f5-1aaa5726284f.PNG">

## Primitive Types
<img width="389" alt="capture" src="https://user-images.githubusercontent.com/22671087/46899276-00b8b780-cedd-11e8-82dd-198d14cb1ba9.PNG">

## Varibales
Variable names begin with a letter, and follow with letters, digits, and underscores. E.g. height, windowHeight.

Each variable **must** be declared, specifying its type.

# Input/Output
## Operations for booleans
**&&** (and) is true iff both operands are

**||** (or) is true iff either operand is

**!** (not) is true iff its operand is false

## String
String is a class type, so strings are **objects**.

Certain letters after backslash are treated specially:

- \n: newline (end current line)
- \r: return (go to start of current line)
- \b: backspace
- \t: tab character

### String Operations
You can use **+** to append two strings. If either operand is a string, it will turn the other into a string.

Other operations:

- **s.length()** returns the length of the string
- **s.toUpperCase()** returns ALL UPPER CASE version of string
- **s.toLowerCase()** RETURNS all lower case VERSION
- **s.substring(i,j)** returns the substring of s from character i through j-1, counting the first character as 0. E.g., "smiles".substring(1,5) is "mile"
- **s.equals(s2)** returns true iff s and s2 are identical
- **s.indexOf(s2)** returns the first position of s2 in s

## Pre/Post Increment/Decrement
**++x** is a special expression that increments x (for any variable x) and returns the incremented value. E.g., if x is 7, ++x is 8, and after that, x is 8. **(increase then return)**

**--x** (pre-decrement) is similar: it decrements x and returns it.

**x++** (post-increment) returns x and then increments it. E.g., if x is 7, x++ is 7, and after that, x is 8. **(return then increase)**

**x--** (post-decrement) returns x and then decrements it.

```
i = 0;
a = i++; // a = 0, i = 1

i = 0;
b = ++i; // b = 1; i = 1
```
**There is no difference when used in for loop**

## Type Conversion
Primitive operations work on operands of the same type. But Java can convert types for you automatically.
<img width="350" alt="capture" src="https://user-images.githubusercontent.com/22671087/46899509-05cb3600-cee0-11e8-9aea-b1bb15db0c03.PNG">

### Casting
Narrowing conversions are also possible. But they must be performed explicitly using a cast

**Cast** is specified by writing the name of the type to convert to in parentheses before the value to be converted. 
```
int sum;
int count;
double average = (double)sum/ count;
```

## Formatted Output
System.out.printf(format-string , args...); E.g.: System.out.printf("Average: %5.2f", average);

**format-string** is an ordinary string, but can contain format specifiers, one for each of the args:
- Format specifier begins with %,
- may have a number specifying how to format the next value in the args... list
- ends with a letter specifying the type of the value

### Format Letters
<img width="371" alt="capture" src="https://user-images.githubusercontent.com/22671087/46899632-1a5bfe00-cee1-11e8-8401-091f4bff9ca2.PNG">

## Reading Console input
**Scanner** class:
```
import java.util.Scanner

class Demo{

    public static void main(String[] args){
        Scanner keyboard = new Scanner(System.in);
        String line = keyboard.nextLine();
    }
}
```
Other methods to read from a Scanner variable keyboard:

<img width="360" alt="capture" src="https://user-images.githubusercontent.com/22671087/46899698-41ff9600-cee2-11e8-8a63-d7c368ecc9be.PNG">

# Control
## If
if statement decides whether or not to execute a statement based on a boolean expression.
```
if (x < 0) {
    x = -x;
} else if (x == 0) {
    x = x + 1;
} else {
    x = x - 1;
}
```
**Ternary Operator**: expr1 ? expr2 : expr3; E.g. lesser = x < y ? x : y;

If expr1 is true value is expr2; If expr1 is false value is expr3.

## Switch
```
switch (ch) {
    case '.':
        System.out.print("dot ");
        break;
    case '-':
        System.out.print("dash ");
        break;
    case ' ':
        System.out.println();
        break;
    default:
        System.out.println("\nbad character '" + ch + "'");
        break;
}
```

## While
```
public class WhileExample{
    public static void main(String[] args) {
        int i = 1;
        int limit = 10;
        int sum = 0;
        while (i <= limit) {
            sum += i;
            ++i;
        }
        System.out.println("The sum is" + sum);
    }
}
```

## Do while
do *Statement* while (expr): First execute Statement. Then if expr is true, go back and do it again.
```
public class dowhileExample {
    public static void main (String[] args){
        int i = 1;
        int limit = 10;
        int sum = 0;
        do {
            sum += i;
            ++i;
        } while (i <= limit);
        System.out.println("The sum is " + sum);
    }
}
```

## For
for (init ; test ; update) *Statement*
```
public class forExample {
    public static void main(String[] args) {
        int limit = 10;
        int sum = 0;
        for (int i = 0; i <= limit; i++){
            sum += i;
        }
        System.out.prinln("The sum is " + sum);
    }
}
```

## break and continue
**break** terminates the (innermost) loop immediately.

**continue** immediately returns to the top of the innermost loop and continues from there.

**Syste.exit(0)** immediately exit whole program.

# Methods
A **method** is an operation defined by a class

Java supports two kinds of methods:
- Class or static methods, and
- Instance or non-static methods

## Class methods
Form: Class .method (expr1 , expr2 , ...). The exprs, called arguments, provide data for the
method to use.

### The Math Class
The Math class is a library of class methods and constants, including: 

<img width="384" alt="capture" src="https://user-images.githubusercontent.com/22671087/46900709-1a182e80-cef2-11e8-833c-c4a99a3323ba.PNG">

### Wrapper Classes
For each primitive type, there is a *warpper class* that defines some useful class methods:

<img width="182" alt="capture" src="https://user-images.githubusercontent.com/22671087/46900735-94e14980-cef2-11e8-8a7e-1599d6ada9db.PNG">

### Covert from Primitive to String
<img width="295" alt="capture" src="https://user-images.githubusercontent.com/22671087/46900745-d3770400-cef2-11e8-85ab-907d04165c13.PNG">

### Parsing Numeric Strings
<img width="297" alt="capture" src="https://user-images.githubusercontent.com/22671087/46900766-44b6b700-cef3-11e8-856d-b81e04cf5313.PNG">

### The main Method
The main is a class method. Java executes the main method when running an application.

### Defining Class Methods
```
public static type name (type1 var1, type2 var2, ...) {
    .
    .
}
```
Each var is called a parameter. Type of corresponding arguments and parameters must match.

```
public class Hypot2 {
    public static void main(String[] args) {
        double side1 = Double.parseDouble(args[0]);
        double side2 = Double.parseDouble(args[1]);
        double hypot = hypot(side1, side2);
        System.out.println(hypot);
    }
    
    public static double hypot(double side1, double side2) {
        return Math.sqrt(side1*side1 + side2*side2);
    }
}
```

## When to define Methods
- When a method gets too big (more than can be easily viewed at once, more than ≈ 60 lines)
- When you repeat similar code multiple times
- When you can give a good name to a chunk of code (e.g., hypot)

## Overloading
*abs*, *min*, and *max* methods all work on all of double, float, int, and long types.

**Overloading**: when a method name has multiple definitions, each with different signature. Java automatically selects the method whose signature matches the call. Method name plus number and types of arguments togerther called the method signature. Signature is used to decide which method to call.

```
public class Test {
    public static void main(String []args){
        int a = 1;
        int b = 2;
        int c = 3;
        Test t1 = new Test();
        System.out.println(t1.addNumber(a, b, c));
    }

    public int addNumber(int a, int b){
        return a + b;
    }
    
    // overload
    public double addNumber(double a, double b) {
        return a + b;
    }
    
    // overload
    public int addNumber(int a, int b, int c){
        return a + b + c;
    }
}
```
### Limitations of Overloading
- You cannot define two methods with the same name and all the same argument types
- You cannot overload based on return type, only parameter types
```
public int addNumber(int a, int b){
    return a + b;
}

public double addNumber(int a, int b) {
    return a + b;
}

----------------------------------------------
error: method addNumber(int,int) is already defined in class test
```
- Beware of combining overloading with automatic type conversion

## public and private
- The keyword *public* in method header means the method may be used by any method in any class.
- The keyword *private* in header means the method may only be used from within that class.
- Best practice: make methods private unless they need to be public

## Local Varibales
- Scope: where variable can be referenced 
- Variables declared inside methods are local to the method (cannot be used outside) Cannot be referenced before declaration is executed
- Variable’s value is forgotten when it goes out of scope; gets a fresh value next time in scope
- Variable declared inside a block is scoped to that block. Parameters are also local to the method
- Local variables cannot be declared public or private

## Class Variables
- Class variable is a variable that is local to a class
- Created when program starts, exists until exit
- Value survives through message calls and returns. Value is unchanged until reassigned
- Can be declared either public or private. It should almost always be private. Too difficult to control if every method in every class can modify it.

```
public class ClassVar {
    private static String name = "Someone"; // class variable
    public static void main(String[] args) {
        greet("Hello");
        setName("Kitty");
        greet("Hello");
        greet("Aloha");
    }
    
    private static void setName(String name) {
        ClassVar.name = name; // 2 vars called name!
    }
    
    private static void greet(String greeting) {
        System.out.printf("%s, %s!%n", greeting, name);
    }
}
-----------------------------------------------------------------
Hello, Someone!
Hello, Kitty!
Aloha, Kitty!
```

# Immutable Objects
## Objects
- Each object is an instance of some class.
- An object holds some data (state) and supports some operations.

### Creating New Objects
New Class (expr1, expr2) or Class var = new Class (expr1, expr2, ..)

E.g. Scanner kbd = new Scanner(System.in);

### Using Objects
object.method(args1, args2)

### null
- null is special value that means "there is no object here."
```
String s = ...  // String is an object
if (s != null) {
    System.out.println("the string is " + s);
}
```
## Class
Classes contain:
- Instance variables, which hold the data of an object
- (Instance) methods, which define the operations (code) of an object

Each object has its own value for each instance varibale.

All objects of a class have the same methods.

### Declaring Instance Variables
- Declare instance variable inside class, but outside any method
- Form: private type name;
```
public class Person {
    private String familyName;
    private String givenName;
    ...
}
```

### Assigning and Using Instance Variablesa
- can be assigned by name: object.name = ..
- Local variables live in a **method**; static variables live in a **class**; instance variables live in a **object**.
Local varibale only live while method is executing, they should be initialised every time method executes; Instance variables live as long as object is around, ther must be initialised when declared or when object is created; static variable lives as long as the program is running, they must be initialised where declared, which is executed when program starts; 

### Accessors
If you declare instance variables private. An accessor is a very simple method written for this purpose.
```
public class Person {
    private String familyName;
    private String givenName;
    ...
    public String getFullName() {
        return familyName + ", " + givenName;
    }...
    
    public String getFamilyName() {
        return familyName;
    }
}
```

## Constructors
Constructors are special methods responsible for initialising instance varibales.
```
public ClassName(type1 var1, ...){
    ...
}
```
**Constructor** always have the smae name as class.

## this
- Inside a method, special keyword **this** always holds the object the current message was sent to.
- Inside constructor, **this** is the object being created.
```
//Constructor
public Person(String givenName, String FamilyName) {
    this.givenName = givenName;
    this.familyName = familyName;
}
```

## Null Pointer Exception
- If you forget to check that an object is not null before sending it a message or accessing its instance variables, you will get a null pointer exception.

## Immutable Objects
- Immutable objects cannot be changed once they are created.
- To be immutable, a class must not have any public methods that modify the object (just constructor).
- **String** class is immutable. Primitive types are also immutable.
- Best practice: make classes immutable if possible

## Final
Add **final** keyword to instance variables before type. The Java will only let you set it once.
```
public class ImmutablePerson {
    private final String familyName;
    private final String givenName;
    
    public ImmutablePerson(String familyName, String givenName) {
        this.familyName = familyName;
        this.givenName = givenName;
    }
```

## Class vs. Instance Messages
- An instance message is sent an individual object
- A class message is sent to the whole class. Not to any individual object
- So a class method does not have (cannot use) **this**
- Class method **cannot** access instance variables! Class methods cannot use instance methods (without specifying object. in front)
- but instance methods **can** use class methods

# Mutable Objects
## How to test
- **Unit testing**: testing that individual classes and methods behave correctly. For each aspect of the specification, write code to
establish the conditions of that aspect, and check that the result is as expected.
- **Regression testing**: running a suite of tests whenever you modify your code, looking for new bugs.
- Ensure that **corner cases** (situations where things happen differently than usual) are tested Where there are **boundary conditions**, test just before, at, and just after the boundary.

## Mutable Objects and Classes
- Instance variables not declared *final* can be modified by methods.
- Mutable objects must be understood in terms of their behaviour in memory.

## Memory
- Computer memory is a long sequence of bytes. Computer can access any byte by its address (its position in the sequence).
- A short is stored over 2 bytes, an int over 4, etc.
- Computer reads multiple bytes at once and assembles into a short, int, double, etc

### Objects
- An object is stored in memory by storing its **instance variables**
- An object at memory address 3270 with 2 int variables holding 5 and 10 might appear in memory as following
- Actual values of a byte are 0-255 or -128-127, not 0-99
- Actual addresses are much larger than this illustration
<img width="95" alt="capture" src="https://user-images.githubusercontent.com/22671087/46905641-72771c80-cf42-11e8-9974-192364e34404.PNG">

### References (Pointers)
- Object types are stored by storing their address. E.g., to store a String, a variable holds its address, not its content. 
- We show the string stored at 7192, but it could be anywhere in memory. E.g., an object with int and String variables holding 5 and "Bo Peep" would be stored as at right
- The address of an object is called a *reference* or *pointer* to it.

### Depicting Objects
- If a variable foo holds (a reference to) this object, it could be depicted as
<img width="265" alt="capture" src="https://user-images.githubusercontent.com/22671087/46905728-6d669d00-cf43-11e8-8dfa-b30c334999c0.PNG">

```
public class Person {
    private int age;
    private String name;
    public Person(int age, String name) {
        this.age = age; this.name = name;
    }
    
    public String toString() {
        return name + ", age " + age;
    }
    
    public static void main(String args[]) {
        Person foo = new Person(5, "Bo Peep");
        ...
    }
}
```

### Changing objects
With immutable *Person* class, only way to change the object foo points to is assign a new object
```
public static void main(String args[]) {
    Person foo = new Person(5, "Bo Peep");
    foo = new Person(3, "Shaun Sheep");
}
```
<img width="241" alt="capture" src="https://user-images.githubusercontent.com/22671087/46905782-1b724700-cf44-11e8-8196-37231b5d4618.PNG">

## Garbage Collection
- No variable (or object) points to orginal object
- Java has a *garbage collector(GC)* that "reclaims" such objects so the memory can be used again.

### Mutators
If instance variable is not declared *final*, methods can reassign it.
```
public void setAge(int age){
    this.age = age;
}
public int getAge() {
    return this.age;
}

public static void main(String args[]) {
    Person foo = new Person(5, "Bo Peep");
    foo.setAge(6);
}
```
<img width="225" alt="capture" src="https://user-images.githubusercontent.com/22671087/46905836-fdf1ad00-cf44-11e8-8736-5b2c17238fce.PNG">

## Mutating aliased objects

























 
