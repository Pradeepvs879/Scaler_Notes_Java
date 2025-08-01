# **Understanding Interface Components in Java**

In Java, an **interface** is a blueprint for classes that can contain specific types of components. Here's a breakdown of what is allowed inside an interface:

---

## **1. Constant Variables (`public static final`)**

- All variables in an interface are **implicitly `public`, `static`, and `final`** (constants).

- They **cannot be modified** after declaration.

- Example:

 

  interface Constants {

      double PI = 3.14; 

      String APP_NAME = "MyApp";

  }

  ```

---

## **2. Abstract Methods (`public abstract`)**

- Traditional interface methods **without a body** (must be implemented by classes).

- Implicitly `public` and `abstract`.

- Example:

  ```java

  interface Vehicle {

      void start(); // Abstract method Think what is functional interface

      void stop();

  }

  ```

---

## **3. Static Methods (`public static`) (Java 8+)**

- Methods **belonging to the interface itself**, not instances.

- Cannot be overridden (but can be hidden).

- Example:

  ```java

  interface MathUtils {

      static int add(int a, int b) {

          return a + b;

      }

  }

  // Usage:

  int sum = MathUtils.add(5, 3); // Called via interface name

  ```

---

## **4. Default Methods (`public default`) (Java 8+)**

- Provide a **default implementation** for methods.

- Can be **overridden** by implementing classes.

- Example:

  ```java

  interface Logger {

      default void log(String message) {

          System.out.println("LOG: " + message);

      }

  }

  class FileLogger implements Logger {

      // Optional: Override default method

      @Override

      public void log(String msg) {

          System.out.println("FILE LOG: " + msg);

      }

  }

  ```

---

## **5. Private Methods (Java 9+)**

- Used to **split large `default` or `static` methods** into reusable pieces.

- Cannot be accessed outside the interface.

- Example:

  ```java

  interface Payment {

      default void process(double amount) {

          validate(amount);

          System.out.println("Processing $" + amount);

      }

      private void validate(double amount) { // Helper method

          if (amount <= 0) throw new IllegalArgumentException();

      }

  }

  ```

---

## **Summary Table**

| Component          | Syntax Example                  | Notes                                  |

|--------------------|--------------------------------|----------------------------------------|

| **Constants**      | `int MAX_SIZE = 100;`          | `public static final` by default.      |

| **Abstract Methods** | `void start();`              | Must be implemented by classes.        |

| **Static Methods** | `static void print() { ... }`  | Called via `InterfaceName.method()`.   |

| **Default Methods** | `default void log() { ... }` | Can be overridden.                     |

| **Private Methods** | `private void helper() { ... }` | Java 9+, reusable logic.              |

---

## **Key Rules**

- **All members are `public`** (except `private` methods in Java 9+).

- **No constructors or instance fields** (only constants).

- **Default/static methods** reduce the need for abstract classes.

---

### **Example: Complete Interface**

```java

interface Database {

    // Constant

    String DB_NAME = "MySQL";

    // Abstract method

    void connect();

    // Default method

    default void disconnect() {

        System.out.println("Disconnected from " + DB_NAME);

    }

    // Static method

    static boolean isValid(String query) {

        return query != null && !query.isEmpty();

    }

    // Private method (Java 9+)

    private void log(String action) {

        System.out.println("Action: " + action);

    }

}

```

Interfaces provide **flexibility** while enforcing contracts. Java 8+ made them even more powerful with `default` and `static` methods! 🚀

-------------------------
Absolutely, let's break down the **Aggressive Cows problem** and the **binary search logic** using the **Feynman Technique** (explain in the simplest terms possible):

* * * * *
Great! To crack interviews involving **Java Threads and Concurrency**, you'll need to build a solid understanding of the **core multithreading concepts**, as well as how they’re used in real-world problems. Here's a comprehensive list of **topics you should master**, along with an **interview-focused roadmap** for Threads in Java:

---

## ✅ **Java Threads & Concurrency – Interview Preparation Roadmap**

### 🔹 1. **Basics of Threads**

* What is a thread? Process vs Thread
* Creating threads:

  * Using `Thread` class (by extending)
  * Using `Runnable` interface (by implementing)
* Life cycle of a thread (`NEW`, `RUNNABLE`, `BLOCKED`, `WAITING`, `TIMED_WAITING`, `TERMINATED`)
* `start()` vs `run()` method

### 🔹 2. **Thread Methods**

* `sleep()`
* `join()`
* `yield()`
* `interrupt()`
* `isAlive()`, `setPriority()`, `getPriority()`

### 🔹 3. **Thread Synchronization**

* Why synchronization is needed (race conditions)
* `synchronized` keyword:

  * synchronized method
  * synchronized block
  * class-level vs object-level lock
* Intrinsic lock / monitor concept

### 🔹 4. **Inter-thread Communication**

* `wait()`, `notify()`, `notifyAll()` – how and why
* Example: Producer-Consumer problem

### 🔹 5. **Concurrency Utilities (java.util.concurrent)**

* **Executor Framework**

  * `Executor`, `ExecutorService`, `ThreadPoolExecutor`
  * `submit()`, `shutdown()`, `shutdownNow()`

* **Callable and Future**

  * How it differs from Runnable
  * How to retrieve results from threads

* **Locks**

  * `ReentrantLock`
  * Try-lock, fairness policy

* **Other important classes:**

  * `CountDownLatch`
  * `CyclicBarrier`
  * `Semaphore`
  * `BlockingQueue` (e.g. `ArrayBlockingQueue`, `LinkedBlockingQueue`)
  * `ConcurrentHashMap`

### 🔹 6. **Thread Safety**

* What is thread-safe code?
* How to write thread-safe classes
* Atomic variables (`AtomicInteger`, etc.)
* Immutability and threads

### 🔹 7. **Volatile and Atomicity**

* What is the `volatile` keyword?
* When to use `volatile` vs `synchronized`
* Happens-before relationship

### 🔹 8. **Deadlock, Livelock, Starvation**

* What is deadlock? How to prevent it?
* Common scenarios that lead to deadlocks
* Difference between deadlock and livelock

### 🔹 9. **Thread Local Variables**

* `ThreadLocal` class
* Use cases (e.g., user sessions, DB connections)

### 🔹 10. **Best Practices and Common Mistakes**

* Creating too many threads
* Blocking vs non-blocking design
* Handling exceptions in threads
* Clean thread shutdown

---

-> Immutable means something that is unchangeable or unmodifiable

-> In terms of class, when we talk about immutable class it simply means Immutable class's objects when created then its object's values and state cannot be changed.

-> Why use Immutable class

-   Thread safe.

-   Easier to debug and maintain.

-   Popular in functional Programming and Spring frameworks

-> Examples Wrapper classes, String, Primitive objects.

-> How to make a class immutable

-   Make a class Final so that it be cannot extended from another class -> Thereby preventing over riding.

-   All the fields should be private and final so that direct access to the fields is blocked.

-   No Setters.

-   If using mutable object reference in immutable class, make a deep copy of it and then refer
