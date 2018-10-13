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


























 
