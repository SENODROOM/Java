# Java Programming Language — Collections & Streams

## The Collections Framework

Java provides a rich set of data structures in `java.util`.

```
Collection (interface)
├── List — ordered, allows duplicates
│   ├── ArrayList
│   ├── LinkedList
│   └── Vector
├── Set — unique elements
│   ├── HashSet
│   ├── LinkedHashSet
│   └── TreeSet (sorted)
└── Queue
    ├── LinkedList
    └── PriorityQueue

Map (separate hierarchy)
├── HashMap
├── LinkedHashMap
└── TreeMap (sorted)
```

---

## List

```java
import java.util.*;

// ArrayList — dynamic array, fast random access
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Mango");
fruits.add(1, "Cherry");   // insert at index
fruits.remove("Banana");    // remove by value
fruits.remove(0);           // remove by index

System.out.println(fruits.size());     // size
System.out.println(fruits.get(0));     // get by index
System.out.println(fruits.contains("Mango")); // true
System.out.println(fruits.indexOf("Mango"));  // index

// Iterate
for (String fruit : fruits) {
    System.out.println(fruit);
}

// Sort
Collections.sort(fruits);
fruits.sort(Comparator.reverseOrder());

// Immutable list (Java 9+)
List<String> immutable = List.of("A", "B", "C");
```

---

## Set

```java
// HashSet — unordered, unique
Set<Integer> numbers = new HashSet<>();
numbers.add(1);
numbers.add(2);
numbers.add(2); // duplicate — ignored!
System.out.println(numbers.size()); // 2

// TreeSet — sorted, unique
Set<String> sorted = new TreeSet<>();
sorted.add("banana");
sorted.add("apple");
sorted.add("cherry");
System.out.println(sorted); // [apple, banana, cherry]
```

---

## Map

```java
// HashMap — key-value pairs, unordered
Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 95);
scores.put("Bob", 87);
scores.put("Carol", 92);

scores.get("Alice");          // 95
scores.getOrDefault("Dave", 0); // 0 if not found
scores.containsKey("Bob");    // true
scores.remove("Carol");

// Iterate
for (Map.Entry<String, Integer> entry : scores.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}

// Immutable map (Java 9+)
Map<String, Integer> fixed = Map.of("A", 1, "B", 2);
```

---

## Generics

Generics enable type-safe collections.

```java
// Generic class
public class Box<T> {
    private T value;
    public void set(T value) { this.value = value; }
    public T get() { return value; }
}

Box<String> strBox = new Box<>();
strBox.set("Hello");
String s = strBox.get(); // No casting needed

// Generic method
public <T extends Comparable<T>> T max(T a, T b) {
    return a.compareTo(b) > 0 ? a : b;
}
```

---

## Streams API (Java 8+)

Streams allow **functional-style** processing of collections.

```java
import java.util.stream.*;

List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Filter and collect
List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());

// Map (transform)
List<String> strings = numbers.stream()
    .map(n -> "item-" + n)
    .collect(Collectors.toList());

// Reduce
int sum = numbers.stream()
    .reduce(0, Integer::sum);

// Count
long count = numbers.stream()
    .filter(n -> n > 5)
    .count();

// Average
OptionalDouble avg = numbers.stream()
    .mapToInt(Integer::intValue)
    .average();

// Sort and limit
List<Integer> top3 = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .limit(3)
    .collect(Collectors.toList());

// Any/all/none match
boolean anyBig  = numbers.stream().anyMatch(n -> n > 9);
boolean allPos  = numbers.stream().allMatch(n -> n > 0);
boolean noneNeg = numbers.stream().noneMatch(n -> n < 0);

// GroupBy
Map<Boolean, List<Integer>> grouped = numbers.stream()
    .collect(Collectors.partitioningBy(n -> n % 2 == 0));
// {true=[2,4,6,8,10], false=[1,3,5,7,9]}
```

---

## Lambdas and Functional Interfaces

```java
// Lambda syntax
Runnable r = () -> System.out.println("Running!");

// Function<T, R>
Function<String, Integer> strlen = s -> s.length();
strlen.apply("Hello"); // 5

// Predicate<T>
Predicate<Integer> isEven = n -> n % 2 == 0;
isEven.test(4); // true

// BiFunction<T, U, R>
BiFunction<Integer, Integer, Integer> add = (a, b) -> a + b;
add.apply(3, 4); // 7
```

---

## Optional (Java 8+)

Avoids NullPointerException by wrapping potentially null values.

```java
Optional<String> name = Optional.of("Alice");
Optional<String> empty = Optional.empty();

name.isPresent();              // true
name.get();                    // "Alice"
name.orElse("Unknown");        // "Alice"
empty.orElse("Unknown");       // "Unknown"
name.map(String::toUpperCase); // Optional["ALICE"]
```

---

## Summary

Java's collections framework and the Streams API form the backbone of modern Java programming. Mastering them unlocks powerful, concise, and expressive ways to process and manage data.
