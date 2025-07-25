# **Understanding Interface Components in Java**

In Java, an **interface** is a blueprint for classes that can contain specific types of components. Here's a breakdown of what is allowed inside an interface:

---

## **1. Constant Variables (`public static final`)**

- All variables in an interface are **implicitly `public`, `static`, and `final`** (constants).

- They **cannot be modified** after declaration.

- Example:

  ```java

  interface Constants {

      double PI = 3.14; // Automatically public static final

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

      void start(); // Abstract method (no implementation)

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
