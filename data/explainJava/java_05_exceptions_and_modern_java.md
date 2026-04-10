# Java Programming Language — Exception Handling & Modern Java

## Exception Handling

Exceptions are events that disrupt normal program flow. Java uses a robust try-catch-finally system.

### Exception Hierarchy
```
Throwable
├── Error (don't catch — JVM problems)
│   ├── OutOfMemoryError
│   └── StackOverflowError
└── Exception
    ├── RuntimeException (unchecked)
    │   ├── NullPointerException
    │   ├── ArrayIndexOutOfBoundsException
    │   ├── IllegalArgumentException
    │   └── ClassCastException
    └── Checked Exceptions (must handle)
        ├── IOException
        ├── SQLException
        └── FileNotFoundException
```

---

### Try-Catch-Finally

```java
try {
    int result = 10 / 0;           // throws ArithmeticException
    String s = null;
    s.length();                    // throws NullPointerException
} catch (ArithmeticException e) {
    System.out.println("Math error: " + e.getMessage());
} catch (NullPointerException e) {
    System.out.println("Null value: " + e.getMessage());
} catch (Exception e) {
    System.out.println("General error: " + e.getMessage());
} finally {
    System.out.println("This always runs"); // cleanup code
}
```

### Multi-catch (Java 7+)
```java
try {
    // risky code
} catch (IOException | SQLException e) {
    System.out.println("IO or SQL error: " + e.getMessage());
}
```

### Try-with-Resources (Java 7+)
Automatically closes resources:
```java
try (FileReader fr = new FileReader("file.txt");
     BufferedReader br = new BufferedReader(fr)) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
// No need to manually close fr and br
```

### Custom Exceptions
```java
public class InsufficientFundsException extends Exception {
    private double amount;

    public InsufficientFundsException(double amount) {
        super("Insufficient funds. Short by: " + amount);
        this.amount = amount;
    }

    public double getAmount() { return amount; }
}

// Using it
public void withdraw(double amount) throws InsufficientFundsException {
    if (amount > balance) {
        throw new InsufficientFundsException(amount - balance);
    }
    balance -= amount;
}
```

---

## Modern Java Features

### Pattern Matching for instanceof (Java 16+)
```java
// Old way
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.length());
}

// New way
if (obj instanceof String s) {
    System.out.println(s.length()); // s is already a String
}
```

### Switch Expressions (Java 14+)
```java
// Old switch statement
int numLetters;
switch (day) {
    case "MONDAY":
    case "FRIDAY": numLetters = 6; break;
    default: numLetters = -1;
}

// New switch expression
int numLetters = switch (day) {
    case "MONDAY", "FRIDAY" -> 6;
    case "TUESDAY" -> 7;
    case "THURSDAY", "SATURDAY" -> 8;
    case "WEDNESDAY" -> 9;
    default -> throw new IllegalArgumentException("Unknown: " + day);
};
```

### Text Blocks (Java 15+)
```java
String json = """
    {
        "name": "Alice",
        "age": 30,
        "city": "Karachi"
    }
    """;

String html = """
    <html>
        <body>
            <h1>Hello, World!</h1>
        </body>
    </html>
    """;
```

### Virtual Threads (Java 21)
Lightweight threads for high-concurrency servers:
```java
// Traditional thread
Thread t = new Thread(() -> System.out.println("Hello"));
t.start();

// Virtual thread (Java 21)
Thread vt = Thread.ofVirtual().start(() -> System.out.println("Hello"));

// Executor with virtual threads
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    for (int i = 0; i < 10_000; i++) {
        executor.submit(() -> handleRequest());
    }
}
```

---

## Concurrency

```java
// Runnable
Thread t = new Thread(() -> {
    for (int i = 0; i < 5; i++) {
        System.out.println("Thread: " + i);
    }
});
t.start();
t.join(); // wait for completion

// ExecutorService
ExecutorService pool = Executors.newFixedThreadPool(4);
Future<Integer> future = pool.submit(() -> {
    return expensiveCalculation();
});
int result = future.get(); // blocks until done
pool.shutdown();

// CompletableFuture (non-blocking)
CompletableFuture<String> cf = CompletableFuture
    .supplyAsync(() -> fetchData())
    .thenApply(data -> processData(data))
    .thenApply(result -> formatResult(result));

cf.thenAccept(System.out::println);
```

---

## Java Build Tools

| Tool | Config File | Command |
|---|---|---|
| **Maven** | `pom.xml` | `mvn compile`, `mvn test`, `mvn package` |
| **Gradle** | `build.gradle` | `gradle build`, `gradle test` |

```xml
<!-- Maven pom.xml example -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>3.2.0</version>
</dependency>
```

---

## Summary

Java's exception handling provides robust error management, while modern Java features (pattern matching, records, virtual threads, text blocks) have made the language much more productive and expressive. Java continues to evolve rapidly while maintaining its legendary backward compatibility.
