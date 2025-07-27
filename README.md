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

-------------------------
Absolutely, let's break down the **Aggressive Cows problem** and the **binary search logic** using the **Feynman Technique** (explain in the simplest terms possible):

* * * * *

🐄💥 Aggressive Cows Problem -- Explained Like You're 5
------------------------------------------------------

### 👀 Problem Statement (In Simple Words):

-   You are given **N stalls** (positions are given in an array).

-   You have to place **K cows** in these stalls.

-   The cows are **aggressive**, so you want to **keep them as far apart as possible**.

-   Your goal is to **maximize the minimum distance** between any two cows.

* * * * *

### 🎯 What Does "Maximum Minimum Distance" Mean?

Let's say stall positions are: `[1, 2, 4, 8, 9]`

Suppose we place 3 cows in stalls like this:

-   Cow1 at 1

-   Cow2 at 4

-   Cow3 at 8

Then, distances between cows:

-   Between Cow1 & Cow2 = 3

-   Between Cow2 & Cow3 = 4

👉 The **minimum** of these is 3

So for this arrangement, the **minimum distance = 3**.\
Your task: find the **largest** such minimum possible.

* * * * *

💡 Core Idea: Use Binary Search on Distance
-------------------------------------------

### Why Binary Search?

You are searching for the **maximum possible minimum distance** between cows. So, you binary search on the **answer space** (i.e., the distance itself), not on array indices.

* * * * *

### 🪜 Steps:

1.  **Sort the stall positions**

2.  Binary search on distance:

    -   `low = 1` (minimum possible distance)

    -   `high = max possible distance = stalls[n-1] - stalls[0]`

3.  For each `mid` (i.e., a guess for minimum distance):

    -   Check: **Can we place all `k` cows such that the distance between any two cows is at least `mid`?**

    -   If **yes**, go **right** (try a bigger distance)

    -   If **no**, go **left** (try a smaller distance)

* * * * *

🤯 The Confusing Part: When to go Left or Right?
------------------------------------------------

Let's clear that up with a golden rule:

| Can you place **≥ k cows** with distance `mid`? | Meaning | What to do? |
| --- | --- | --- |
| ✅ Yes | It **might be possible** to place cows even **farther apart** | Try **larger** distance → `low = mid + 1` |
| ❌ No | Distance is **too big**, cows can't be placed that far | Try **smaller** distance → `high = mid - 1` |

You're basically **trying to stretch** the cows apart as much as possible without breaking the rule.

* * * * *

👨‍🏫 Dry Run Example
---------------------

### Input:

```
stalls = [1, 2, 4, 8, 9]
k = 3

```

### Step 1: Sort stalls: `[1, 2, 4, 8, 9]`

### Step 2: Initialize:

-   `low = 1`

-   `high = 8` (9 - 1)

We now binary search between 1 and 8

* * * * *

### Try `mid = 4`:

Try placing cows with **at least 4** distance:

-   Place cow1 at 1

-   Next stall ≥ 1+4 = 5 → stall 8 → cow2

-   Next stall ≥ 8+4 = 12 → ❌ no more stalls

Only 2 cows placed → ❌ Not enough → Try smaller distance

🧭 Move **left** → `high = mid - 1 = 3`

* * * * *

### Try `mid = 2`:

-   cow1 at 1

-   next ≥ 3 → 4 → cow2

-   next ≥ 6 → 8 → cow3

✅ All 3 cows placed

🧭 Try bigger → `low = mid + 1 = 3`, `ans = 2`

* * * * *

### Try `mid = 3`:

-   cow1 at 1

-   next ≥ 4 → 4 → cow2

-   next ≥ 7 → 8 → cow3

✅ 3 cows placed → try bigger → `low = 4`, `ans = 3`

Now `low > high` → stop.

### ✅ Final Answer: `3`

* * * * *

🧠 Summary:
-----------

### What You're Searching?

-   The **maximum possible minimum distance** between cows.

### How You Decide Direction in Binary Search?

| If you can place `k` cows or more | Go right → `low = mid + 1` (try bigger distance) |\
| If you can't place `k` cows | Go left → `high = mid - 1` (distance too big) |

* * * * *

Want to implement this yourself or walk through more examples?
