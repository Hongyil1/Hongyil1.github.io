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








