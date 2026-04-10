# Java Programming Language — Syntax & Data Types

## Primitive Data Types

Java has 8 primitive types — they are **not objects**:

| Type | Size | Range | Example |
|---|---|---|---|
| `byte` | 8-bit | -128 to 127 | `byte b = 100;` |
| `short` | 16-bit | -32,768 to 32,767 | `short s = 1000;` |
| `int` | 32-bit | ~-2B to 2B | `int i = 42;` |
| `long` | 64-bit | Very large | `long l = 99L;` |
| `float` | 32-bit | ~6-7 decimal digits | `float f = 3.14f;` |
| `double` | 64-bit | ~15 decimal digits | `double d = 3.14;` |
| `char` | 16-bit | Unicode character | `char c = 'A';` |
| `boolean` | 1-bit | true/false | `boolean flag = true;` |

---

## Variables

```java
// Declaration and initialization
int age = 25;
double salary = 75000.50;
String name = "Alice";
boolean isActive = true;

// var (type inference — Java 10+)
var city = "Karachi";     // inferred as String
var count = 0;            // inferred as int

// Final (constant)
final double PI = 3.14159;
```

---

## Wrapper Classes

Every primitive has an **object wrapper** (used in collections, generics):

| Primitive | Wrapper |
|---|---|
| `int` | `Integer` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |
| `long` | `Long` |

```java
Integer x = 42;           // autoboxing
int y = x;                // unboxing
String s = Integer.toString(42);
int parsed = Integer.parseInt("100");
```

---

## Strings

Strings in Java are **immutable objects**.

```java
String greeting = "Hello, World!";

// Methods
greeting.length()          // 13
greeting.toUpperCase()     // "HELLO, WORLD!"
greeting.substring(0, 5)   // "Hello"
greeting.contains("World") // true
greeting.replace("World", "Java") // "Hello, Java!"
greeting.split(", ")       // ["Hello", "World!"]
greeting.trim()            // removes whitespace
greeting.charAt(0)         // 'H'
```

### StringBuilder (mutable)
```java
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(", ");
sb.append("World!");
String result = sb.toString(); // "Hello, World!"
```

---

## Arrays

```java
// Fixed-size, same type
int[] scores = {90, 85, 78, 92};
String[] fruits = new String[3];
fruits[0] = "Apple";

System.out.println(scores.length);   // 4
System.out.println(scores[0]);       // 90

// 2D Array
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
System.out.println(matrix[1][2]); // 6
```

---

## Type Casting

```java
// Widening (automatic)
int i = 100;
double d = i;  // 100.0

// Narrowing (explicit)
double pi = 3.14;
int truncated = (int) pi;  // 3

// String conversions
String s = String.valueOf(42);    // int to String
int n = Integer.parseInt("42");   // String to int
double x = Double.parseDouble("3.14");
```

---

## Operators

```java
// Arithmetic
int result = 10 + 3;   // 13
int mod    = 10 % 3;   // 1

// Comparison
boolean eq  = (5 == 5);  // true
boolean neq = (5 != 4);  // true
boolean gt  = (5 > 3);   // true

// Logical
boolean and = true && false;  // false
boolean or  = true || false;  // true
boolean not = !true;          // false

// Ternary
String label = age >= 18 ? "Adult" : "Minor";

// Null coalescing (Objects.requireNonNullElse — Java 9+)
String name = Objects.requireNonNullElse(input, "default");
```

---

## Summary

Java's type system is strict and explicit. Understanding primitives, wrappers, and how Java handles strings and arrays is foundational to writing correct and efficient Java code.
