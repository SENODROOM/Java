# Java Programming Language — Object-Oriented Programming

## The Four Pillars of OOP

1. **Encapsulation** — Bundling data and methods, hiding internals
2. **Inheritance** — Deriving new classes from existing ones
3. **Polymorphism** — One interface, many implementations
4. **Abstraction** — Hiding complexity, exposing essentials

---

## Classes and Objects

```java
public class Car {
    // Fields (attributes)
    private String brand;
    private int year;
    private double speed;

    // Constructor
    public Car(String brand, int year) {
        this.brand = brand;
        this.year = year;
        this.speed = 0;
    }

    // Methods
    public void accelerate(double amount) {
        this.speed += amount;
    }

    // Getters and Setters (Encapsulation)
    public String getBrand() { return brand; }
    public void setBrand(String brand) { this.brand = brand; }
    public double getSpeed() { return speed; }

    @Override
    public String toString() {
        return brand + " (" + year + ") - Speed: " + speed;
    }
}

// Creating objects
Car myCar = new Car("Toyota", 2022);
myCar.accelerate(60.0);
System.out.println(myCar); // Toyota (2022) - Speed: 60.0
```

---

## Inheritance

```java
public class ElectricCar extends Car {
    private int batteryRange;

    public ElectricCar(String brand, int year, int range) {
        super(brand, year); // call parent constructor
        this.batteryRange = range;
    }

    // Override parent method
    @Override
    public void accelerate(double amount) {
        super.accelerate(amount * 1.2); // EVs accelerate faster
    }

    public int getBatteryRange() { return batteryRange; }
}

ElectricCar tesla = new ElectricCar("Tesla", 2023, 400);
tesla.accelerate(50.0);
System.out.println(tesla.getSpeed()); // 60.0
```

---

## Interfaces

An interface defines a **contract** — what a class must do, not how.

```java
public interface Flyable {
    void fly();
    void land();
    
    default String getStatus() {
        return "In the air";
    }
}

public interface Swimmable {
    void swim();
}

// A class can implement multiple interfaces
public class Duck extends Animal implements Flyable, Swimmable {
    @Override
    public void fly() { System.out.println("Duck flying!"); }
    
    @Override
    public void land() { System.out.println("Duck landing!"); }
    
    @Override
    public void swim() { System.out.println("Duck swimming!"); }
}
```

---

## Abstract Classes

Between a class and an interface — can have abstract methods AND concrete methods.

```java
public abstract class Shape {
    protected String color;

    public Shape(String color) {
        this.color = color;
    }

    // Abstract method — subclasses must implement
    public abstract double area();

    // Concrete method — shared by all shapes
    public void display() {
        System.out.println("Shape: " + color + ", Area: " + area());
    }
}

public class Circle extends Shape {
    private double radius;

    public Circle(String color, double radius) {
        super(color);
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}
```

---

## Polymorphism

```java
Shape[] shapes = {
    new Circle("Red", 5),
    new Rectangle("Blue", 4, 6),
    new Triangle("Green", 3, 4)
};

for (Shape s : shapes) {
    s.display(); // calls the correct area() for each shape
}
```

---

## Records (Java 16+)

Immutable data classes with auto-generated constructor, getters, equals, hashCode, toString.

```java
public record Point(double x, double y) {}

Point p = new Point(3.0, 4.0);
System.out.println(p.x());  // 3.0
System.out.println(p);      // Point[x=3.0, y=4.0]
```

---

## Sealed Classes (Java 17+)

Restricts which classes can extend a class.

```java
public sealed class Result permits Success, Failure {}
public final class Success extends Result { String value; }
public final class Failure extends Result { String error; }
```

---

## Enums

```java
public enum DayOfWeek {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY,
    FRIDAY, SATURDAY, SUNDAY;

    public boolean isWeekend() {
        return this == SATURDAY || this == SUNDAY;
    }
}

DayOfWeek day = DayOfWeek.SATURDAY;
System.out.println(day.isWeekend()); // true
```

---

## Summary

Java's OOP model is one of the most complete in any language. Understanding classes, inheritance, interfaces, and polymorphism is the key to writing flexible, maintainable Java applications.
