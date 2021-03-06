---
title: OCP Review 2.3 - Polymorphism and Design
layout: post
tags: [java, ocp, polymorphism, design]
date: 2018-09-07
---


## Polymorphism

- we can "see" only the part of the object we're interested in
- at runtime, if we call a method, the __true__ one is the method from the instance class, not the reference one

---

## Casting

- no need to cast if upcasting (from a specialzed version to a general one)
- need to cast if downcasting
- use `instanceof`
- can only cast inheritance-related classes

```java
String s = "";
Object o = s;
        
String s1 = (String) o;

```

# Design Principles

> a design principle is an established idea or best practice that facilitates software development

---

## Encapsulation

- almost always related to information hiding
- invariants about internal data: property or truth that is maintained after data is modified

---

## Invariants

- For a Person:
    - all people have names
    - all living people has age between 0...150 

```java
class Person {
    String name;
    int age;
}
```

---

## JavaBeans


---

## Inheritance vs Composition

- Inheritance: IS-A
    - instanceof operator
- Composition: HAS-A
    - look at properties

---

## Stupid inheritance

```java
class Person {
    String name;
    int age;
}

class Car extends Person {
    String color;
}
```

---

## Object composition: Delegation

---

## Design patterns

- creational patterns
- 4 showed in the book
- only Singleton & Inmutable Object in the exam


---

## Singleton

- allow only one instance of that class in memory

```java
class PrintJobsManager {
    private int remainingJobs;
    
    private static PrintJobsManager sharedInstance = new PrintJobsManager();
    
    public static synchronized PrintJobsManager sharedPrintJobsManager() {
        return sharedInstance;
    }
    
    private PrintJobsManager() {}
    
    public synchronized void addPrintJob(String s) {
        remainingJobs = remainingJobs + 1;
    }
    
    public synchronized int getRemainingJobs() {
        return remainingJobs;
    }
}
```

---

## Singleton is effectively final

- we don't have any constructor now!

```java
class A extends PrintJobsManager {
    A() {
        super();    // FAILS
    }
}

```

---

## Double-Checked Locking


```java
class PrintJobsManager {
    private int remainingJobs;

    private static volatile PrintJobsManager sharedInstance;

    // Double-Checked Locking
    public static PrintJobsManager sharedPrintJobsManager() {
        if (sharedInstance == null) {
            synchronized (PrintJobsManager.class) {
                sharedInstance = new PrintJobsManager();
            }
        }
        return sharedInstance;
    }

    private PrintJobsManager() {}

    public synchronized void addPrintJob(String s) {
        remainingJobs = remainingJobs + 1;
    }

    public synchronized int getRemainingJobs() {
        return remainingJobs;
    }
}
```

---

## Volatile?

- Nice discussion here: http://stackoverflow.com/questions/7855700/why-is-volatile-used-in-this-example-of-double-checked-locking


```java
public final class Singleton {
    private Singleton() {}
    public static Singleton getInstance() {
        return LazyHolder.INSTANCE;
    }
    private static class LazyHolder {
        private static final Singleton INSTANCE = new Singleton(); // gets initialized once, before all threads start
    }
}

```

---

## Inmutable Objects

1. use constructor to set all properties
1. mark all instance variables as `private` and `final`
1. only use getters, not setters
1. don't allow referenced mutable objects to be modified or accessed directly
1. prevent methods from being overridden


```java
class City {
    private String name;

    public City(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

---

## Inmutable Objects

- all instance vars must be private
- if not: we can change it

```java
City seville = new City("Seville");
seville.population = 100;
System.out.println(seville.getName());

class City {
    private String name;
    int population;     // should be private to avoid direct access!

    public City(String name) {
        this(name, 0);
    }

    public City(String name, int population) {
        this.name = name;
        this.population = population;
    }

    public String getName() {
        return name;
    }
}
```

---

## Inmutable Objects

- better encapsulated version

```java
class City {
    private final String name;
    private final int population;

    public City(String name) {
        this(name, 0);  // chained constructors
    }

    public City(String name, int population) {
        this.name = name;
        this.population = population;
    }

    public String getName() {
        return name;
    }
}
```

---

## Inmutable Objects: adding referenced objects

```java
List<String> streets = new LinkedList<>();

streets.add("Torricelli");
streets.add("Sierpes");
streets.add("Constitución");

City seville = new City("Seville", 800_000, streets);
seville.getStreets().forEach(System.out::println);

seville.getStreets().add("Wall Street");    // we can mutate the list!
seville.getStreets().forEach(System.out::println);

streets.clear();     // even worse, we have stored the reference, so we can change from outside
seville.getStreets().forEach(System.out::println);

class City {
    private final String name;
    private final int population;
    private final List<String> streets;

    public City(String name) {
        this(name, 0);  // chained constructors
    }

    public City(String name, int population) {
        this(name, population, null);
    }

    public City(String name, int population, List<String> streets) {
        this.name = name;
        this.population = population;
        this.streets = streets;
    }

    public String getName() {
        return name;
    }

    public int getPopulation() {
        return population;
    }

    public List<String> getStreets() {
        return streets;
    }
}
```

---

## Solution

```java
class City {
    private final String name;
    private final int population;
    private final List<String> streets;

    public City(String name) {
        this(name, 0);  // chained constructors
    }

    public City(String name, int population) {
        this(name, population, null);
    }

    public City(String name, int population, List<String> streets) {
        this.name = name;
        this.population = population;
        this.streets = Collections.unmodifiableList(streets);
    }

    public String getName() {
        return name;
    }

    public int getPopulation() {
        return population;
    }

    public List<String> getStreets() {
        return streets;
    }
}


```

---

## Builder pattern

```java
class Person {
    private String name;
    private String address;
    private int age;

    public static class Builder {
        private String name;
        private String address;
        private int age;

        public Person build() {
            return new Person(name, address, age);
        }

        public Builder setName(String name) {
            this.name = name;
            return this;
        }

        public Builder setAddress(String address) {
            this.address = address;
            return this;
        }

        public Builder setAge(int age) {
            this.age = age;
            return this;
        }
    }

    private Person(String name, String address, int age) {
        this.name = name;
        this.address = address;
        this.age = age;
    }

    public String getName() { return name; }

    public String getAddress() { return address; }

    public int getAge() { return age; }
}
```