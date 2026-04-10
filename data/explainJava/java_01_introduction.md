# Java Programming Language — Introduction

## What is Java?

Java is a **high-level, class-based, object-oriented** programming language designed to have as few implementation dependencies as possible. It was created by **James Gosling** at Sun Microsystems (now Oracle) and released in **1995**.

The famous Java motto:
> **"Write Once, Run Anywhere"** (WORA)

This is possible because Java code compiles to **bytecode**, which runs on the **Java Virtual Machine (JVM)** — and JVMs exist for virtually every platform.

---

## Key Characteristics

| Feature | Description |
|---|---|
| **Object-Oriented** | Everything is an object (except primitives) |
| **Platform Independent** | Runs on any OS with a JVM |
| **Statically Typed** | Types checked at compile time |
| **Strongly Typed** | No implicit type coercion |
| **Garbage Collected** | Automatic memory management |
| **Multi-threaded** | Built-in threading support |
| **Robust** | Strong type checking, exception handling |
| **Secure** | No pointers, sandboxed execution |

---

## How Java Works

```
Source Code (.java)
       ↓
  Java Compiler (javac)
       ↓
   Bytecode (.class)
       ↓
Java Virtual Machine (JVM)
       ↓
  Native Machine Code
```

---

## Hello, World in Java

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Explanation:**
- `public class HelloWorld` — Class name must match filename
- `public static void main(String[] args)` — Entry point of every Java program
- `System.out.println()` — Prints a line to standard output
- Every statement ends with `;`

---

## Java Ecosystem

### Java SE (Standard Edition)
Core Java — the fundamental APIs and JVM.

### Java EE / Jakarta EE (Enterprise Edition)
For large-scale enterprise apps — web servers, transactions, messaging.

### Java ME (Micro Edition)
For embedded and mobile devices.

### Spring Framework
The most popular Java framework for building web apps and microservices.

---

## Where Java is Used

- **Enterprise Applications** — Banking, insurance, ERP systems
- **Android Development** — Android was built on Java
- **Web Backends** — REST APIs, microservices
- **Big Data** — Hadoop, Spark (written in Java/Scala)
- **Scientific Computing**
- **Embedded Systems**

---

## Notable Systems Written in Java

- **Minecraft** — The original game
- **LinkedIn** — Backend services
- **Netflix** — Backend microservices
- **Amazon** — Core backend services
- **Hadoop & Spark** — Big data processing

---

## Java Versions

| Version | Year | Notable Features |
|---|---|---|
| Java 5 | 2004 | Generics, annotations, autoboxing |
| Java 8 | 2014 | Lambdas, streams, Optional |
| Java 11 | 2018 | LTS release, var in lambdas |
| Java 17 | 2021 | LTS, sealed classes, pattern matching |
| Java 21 | 2023 | LTS, virtual threads, record patterns |

---

## Summary

Java has stood the test of time for over 30 years. It remains one of the most widely used programming languages in the world — particularly in enterprise, Android, and large-scale backend development — thanks to its stability, performance, and massive ecosystem.
