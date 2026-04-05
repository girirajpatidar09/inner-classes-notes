##  Nested Classes (Inner Classes)

Nested classes are classes defined **inside another class**.

---

##  Categories of Nested Classes

###  1. Non-Static Nested Classes

These are also called **Inner Classes**

---

#### a️⃣ Instance Inner Class

- Defined inside a class (non-static)
- Requires an **outer class object** to access

---

#### b️⃣ Local Inner Class

- Defined **inside a method**
- Accessible only within that method

---

#### c️⃣ Anonymous Inner Class

- Class without a name  
- Used for **one-time use**

---

#####  Types of Anonymous Inner Classes

1. **Extending a Class**

```java
class A {
    void show() {
        System.out.println("A");
    }
}

A obj = new A() {
    void show() {
        System.out.println("Anonymous A");
    }
};
```

---

2. **Implementing an Interface**

```java
interface Test {
    void display();
}

Test obj = new Test() {
    public void display() {
        System.out.println("Hello");
    }
};
```

---

3. **Defined Inside Method Argument**

```java
interface Test {
    void display();
}

void method(Test t) {
    t.display();
}

method(new Test() {
    public void display() {
        System.out.println("Inside argument");
    }
});
```

---

###  2. Static Nested Class

- Declared using `static` keyword  


```java
class Outer {
    static class Inner {
        void show() {
            System.out.println("Static Nested Class");
        }
    }
}
```

---


# Instance Inner class 


##  Example 1: Instance Inner Class

---

###  Code

```java
class Demo1 {

    class A {
        
    }
}
```

---

##  Output (Generated Class Files)

```text
Demo1.class
Demo1$A.class
```

---



##  Example 2: 

---

###  Code

```java
class demo {

    class A {
        
    }

    public static void main(String ar[]) {
        System.out.println("Main Method");
    }
}
```

---

## ▶️ Execution

```bash
java demo.java
java demo
```

---

## Output

```text
Main Method
```

---

##  Trying to Run Inner Class

```bash
java demo$A
```

---

##  Error

```text
Error: Main method not found in class demo$A, please define the main method as:
   public static void main(String[] args)
or a JavaFX application class must extend javafx.application.Application
```

---



##  Example 3:

---

###  Code

```java
class demo {

    class A {

        public static void main(String ar[]) {
            System.out.println("Instance Inner Class");
        }
    }

    public static void main(String ar[]) {
        System.out.println("Main Method");
    }
}
```

---

## ▶️ Compilation

```bash
javac demo.java
```

---

## ▶️ Run Outer Class

```bash
java demo
```

###  Output

```text
Main Method
```

---

## ▶️ Run Inner Class

```bash
java demo$A
```

### Output

```text
Instance Inner Class
```

---


##  Static Members in Instance Inner Class (Java 16+)

---

###  Before Java 16

- Instance inner classes **cannot have static members**
- Only **static final constants** were allowed



##  Summary

| Feature                    | Before Java 16 | Java 16+ |
|--------------------------- |--------------- |----------|
| Static variables           |  Not allowed   |  Allowed |
| Static methods             |  Not allowed   |  Allowed |
| Static final constants     |  Allowed       |  Allowed |




##  Example 4: Creating Object of Instance Inner Class

---

###  Code

```java
class demo {

    class A {

        public void show() {
            System.out.println("Inner class A");
        }
    }

    public static void main(String ar[]) {

        // 🔹 Syntax 1
        demo d = new demo();
        demo.A a = d.new A();
        a.show();

        // 🔹 Syntax 2
        demo d1 = new demo();
        A a1 = d1.new A();
        a1.show();
    }
}
```

---

##  Output

```text
Inner class A
Inner class A
```

---


##  Example 5: Inner Class in Different Class

---

###  Code

```java
class A {

    class B {

        public void show() {
            System.out.println("Inner class B");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        // ✅ Correct Syntax
        A a = new A();
        A.B b = a.new B();
        b.show();

        // ❌ Wrong Syntax
        A a1 = new A();
        B b1 = a1.new B(); // ❌ Compile-time error
        b1.show();
    }
}
```

---

##  Output

```text
Inner class B
```

---

##  Explanation

###  Correct Way

```java
A.B b = a.new B();
```

- `A.B` → Inner class B belongs to class A  
- Must use **OuterClass.InnerClass** format  

---

###  Wrong Way

```java
B b1 = a1.new B(); // ❌ Error
```

👉 Error because:
- `B` is **not visible directly**
- It belongs to class `A`

---


##  Example 6: Accessing Inner Class from Outer Class

---

### Code

```java
class A {

    int x = 1250;

    void show2() {
        System.out.println("show 2....");
    }

    class B {

        void show3() {
            System.out.println("class B show 3 method");
        }
    }

    void show1() {
        show2();                     // calling outer class method
        System.out.println("x=" + x); // accessing outer variable

        B b = new B();              // creating inner class object
        b.show3();                  // calling inner class method
    }
}

class show {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show1();
    }
}
```

---

## 🖥️ Output

```text
show 2....
x=1250
class B show 3 method
```

---


##  Example 7: Accessing Inner Class from Static Method

---

###  Code

```java
class A {

    int x = 1250;

    void show2() {
        System.out.println("show 2....");
    }

    class B {

        void show3() {
            System.out.println("class B show 3 method");
        }
    }

    static void show1() {

        A a = new A();          // create outer class object

        a.show2();              // access non-static method
        System.out.println("x=" + a.x); // access instance variable

        B b = a.new B();        // create inner class object using outer object
        b.show3();
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show1(); // static method call (can also use A.show1())
    }
}
```

---

##  Output

```text
show 2....
x=1250
class B show 3 method
```

---


## 📌 Example 8: Multi-Level Inner Class

---

### 📦 Code

```java
class A {

    class B {

        class C {

            public void show() {
                System.out.println("class C");
            }
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();          // Outer class object

        A.B b = a.new B();      // Inner class B object

        A.B.C c = b.new C();    // Inner class C object

        c.show();
    }
}
```

---

## 🖥️ Output

```text
class C
```

---


## 📌 Example 9: `this` Keyword in Inner Class

---

### 📦 Code

```java
class A {

    int x = 10;

    class B {

        int x = 20;

        public void show() {

            int x = 30;

            System.out.println("x=" + x);           // local variable
            System.out.println("x=" + this.x);      // B's variable
            System.out.println("x=" + B.this.x);    // B's variable (explicit)
            System.out.println("x=" + A.this.x);    // A's variable
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        A.B b = a.new B();
        b.show();
    }
}
```

---

## 🖥️ Output

```text
x=30
x=20
x=20
x=10
```

---



## 📌 Example 10: Accessing Private Members of Outer Class

---

### 📦 Code

```java
class A {

    private int x = 10;

    class B {

        public void show() {
            System.out.println("x=" + x);
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        A.B b = a.new B();
        b.show();
    }
}
```

---

##  Output

```text
x=10
```

---


##  Example 11: Private Top-Level Class (Invalid ❌)

---

###  Code

```java
private class A {

    int x = 10;
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
    }
}
```

---

##  Error

```text
Modifier 'private' not allowed here
```

---


##  Modifiers for Classes in Java

---

##  Modifiers for Outer (Top-Level) Class

Allowed modifiers:

- `public`
- `<default>` (no modifier)
- `final`
- `abstract`
- `strictfp`

---


##  Modifiers for Inner Class

Allowed modifiers:

- `public`
- `<default>` (no modifier)
- `private`
- `protected`
- `static`
- `final`
- `abstract`
- `strictfp`

---


##  Example 12: Private Inner Class Access (Invalid ❌)

---

###  Code

```java
class A {

    private class B {

        public void show1() {
            System.out.println("Inner class B");
        }
    }
}

class show {

    public static void main(String ar[]) {

        A a = new A();

        A.B b = a.new B(); // ❌ Error
        b.show1();
    }
}
```

---

##  Error

```text
B has private access in A
```

---


##  Example 13: Using Private Inner Class 

---

###  Code

```java
class A {

    private class B {

        public void show() {
            System.out.println("Private inner class B");
        }
    }

    public void show1() {

        B b = new B();  // accessing private inner class inside outer class
        b.show();
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        a.show1(); // calling outer class method
    }
}
```

---

##  Output

```text
Private inner class B
```

---

##  Example: Creating Inner Class Object (Shortcut Way)

---

###  Code

```java
class A {

    class B {

        public void show() {
            System.out.println("class B inside class A");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        // 🔹 Traditional Way
        // A a = new A();
        // A.B b = a.new B();
        // b.show();

        // 🔥 Shortcut Way
        new A().new B().show();
    }
}
```

---

##  Output

```text
class B inside class A
```

---


##  Example: Multi-Level Inner Class (Shortcut Way)

---

### 📦 Code

```java
class A {

    class B {

        class C {

            public void show() {
                System.out.println("class C inside B inside A");
            }
        }
    }
}

class demo {

    public static void main(String ar[]) {

        // 🔹 Traditional Way
        // A a = new A();
        // A.B b = a.new B();
        // A.B.C c = b.new C();
        // c.show();

        // 🔥 Shortcut Way
        new A().new B().new C().show();
    }
}
```

---

##  Output

```text
class C inside B inside A
```

---


##  Example: We can Make Static block inside instance inner class

---

###  Code

```java
class A {

    class B {

        static {
            System.out.println("static block");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        A.B b = a.new B();
    }
}
```

---

##  Output

```text
static block
```

---



##  Example: Instance Initialization Block (Outer + Inner Class)

---

###  Code

```java
class A {

    {
        System.out.println("Class A instance block");
    }

    class B {

        {
            System.out.println("Class B instance block");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();        // creates object of A
        A.B b = a.new B();   // creates object of inner class B
    }
}
```

---

## ️ Output

```text
Class A instance block
Class B instance block
```

---


##  Example: Execution Order (Instance Block + Constructor + Inner Class)

---

###  Code

```java
class A {

    A() {
        System.out.println("Class A constructor");
    }

    {
        System.out.println("Class A instance block");
    }

    class B {

        B() {
            System.out.println("Class B constructor");
        }

        {
            System.out.println("Class B instance block");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();        // create object of A
        A.B b = a.new B();   // create object of B
    }
}
```

---

##  Output

```text
Class A instance block
Class A constructor
Class B instance block
Class B constructor
```

---


##  Example: Inheritance in Inner Classes

---

### Code

```java
class A {

    class B {

        public void show1() {
            System.out.println("show 1 method");
        }
    }

    class C extends B {

        public void show2() {
            System.out.println("show 2 method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();

        A.C c = a.new C(); // creating object of inner class C

        c.show1(); // inherited method from B
        c.show2(); // method of C
    }
}
```

---

##  Output

```text
show 1 method
show 2 method
```

---



##  Example: Constructor Order in Inner Class Inheritance

---

###  Code

```java
class A {

    class B {

        B() {
            System.out.println("Class B constructor");
        }
    }

    class C extends B {

        C() {
            System.out.println("Class C constructor");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        A.C c = a.new C(); // creating object of C
    }
}
```

---

## ️ Output

```text
Class B constructor
Class C constructor
```

---

##  Example: Inner Class inside Abstract Class

---

###  Code

```java
abstract class A {

    class B {

        public void show() {
            System.out.println("class B show method");
        }
    }
}

class C extends A {

}

class demo {

    public static void main(String ar[]) {

        C c = new C();

        C.B b = c.new B(); // accessing inner class B
        b.show();
    }
}
```

---

## Output

```text
class B show method
```

---


## 📌 Example: Inner Class with Same Name as Outer Subclass (Name Conflict)

---

### 📦 Code

```java
abstract class A {

    class B {

        public void show() {
            System.out.println("class B show method");
        }
    }
}

// ⚠️ Subclass name is also B
class B extends A {

}

class demo {

    public static void main(String ar[]) {

        B b = new B();

        B.B b1 = b.new B(); // accessing inner class B
        b1.show();
    }
}
```

---

## 🖥️ Output

```text
class B show method
```

---


##  Example: Inner Class with Same Name as Outer Class (Invalid ❌)

---

### 📦 Code

```java
class A {

    class A {   // ❌ Error

        public void show() {
            System.out.println("class B show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        A.A a1 = a.new A();
        a1.show();
    }
}
```

---

## 💥 Error

```text
error: class A is already defined in package unnamed package
```

---


##  Example: Abstract Inner Class Instantiation (Invalid ❌)

---

###  Code

```java
class A {

    abstract class B {

        public void show() {
            System.out.println("class B show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();

        A.B b = a.new B(); // ❌ Error (cannot instantiate abstract class)
        b.show();
    }
}
```

---

##  Error

```text
B is abstract; cannot be instantiated
```

---


##  Example: Abstract Inner Class (Correct Usage ✅)

---

###  Code

```java
class A {

    abstract class B {

        public void show() {
            System.out.println("class B show method");
        }
    }

    class C extends B {
        // no override needed (method already implemented)
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();

        A.C c = a.new C(); // creating object of subclass
        c.show();
    }
}
```

---

##  Output

```text
class B show method
```

---


##  Example: Abstract Method in Non-Abstract Inner Class (Invalid ❌)

---

###  Code

```java
class A {

    class B {

        abstract void show(); // ❌ Error
    }
}

class demo {

    public static void main(String ar[]) {

    }
}
```

---

##  Error

```text
A.B is not abstract and does not override abstract method show() in A.B
```

---


##  Example: Abstract Inner Class with Abstract Method (Valid ✅)

---

### 📦 Code

```java
class A {

    abstract class B {

        abstract void show();
    }
}

class demo {

    public static void main(String ar[]) {

        // No object created
    }
}
```

---

##  Output

```text
Program compile and run successfully.
```


---


##  Example: Subclass Not Implementing Abstract Method (Invalid ❌)

---

### 📦 Code

```java
class A {

    abstract class B {

        abstract void show();
    }

    class C extends B {   // ❌ Error

    }
}

class demo {

    public static void main(String ar[]) {

    }
}
```

---

##  Error

```text
A.C is not abstract and does not override abstract method show() in A.B
```

---



## 📌 Example: Implementing Abstract Method in Inner Class (Correct ✅)

---

### 📦 Code

```java
class A {

    abstract class B {

        abstract void show();
    }

    class C extends B {

        void show() {
            System.out.println("Class C");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();

        A.C c = a.new C(); // creating object of C
        c.show();
    }
}
```

---

## 🖥️ Output

```text
Class C
```

---

# Local Inner class 

##  Local Inner Class (No Object Creation)

---

###  Code

```java
class A {

    void show() {

        class B {

            void show2() {
                System.out.println("show 2 method");
            }
        }

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

## Output

```text
class A show method
```

---



##  Local Inner Class (With Object Creation)

---

###  Code

```java
class A {

    void show() {

        class B {

            void show2() {
                System.out.println("show B method");
            }
        }

        B b1 = new B();
        b1.show2();

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Output

```text
show B method
class A show method
```

---



##  Local Inner Class Scope (Invalid Usage ❌)

---

###  Code

```java
class A {

    void show() {

        class B {

            void show2() {
                System.out.println("show B method");
            }
        }
    }

    void show1() {

        B b1 = new B(); // ❌ Error
        b1.show2();
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show1();
    }
}
```

---

##  Error

```text
cannot find symbol
symbol: class B
```

---


## 📌 Multiple Local Inner Classes in Different Methods

---

### 📦 Code

```java
class A {

    void show() {

        class B {
        }
    }

    void show1() {

        class B {
        }
    }

    void show2() {

        class C {
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
    }
}
```

---



### .class files be like 

- demo.class 
- A$1B .class
- A$2B.class
- A$1C.class
- A.class 

---



##  Local Inner Class inside Constructor

---

###  Code

```java
class A {

    A() {

        class B {

            public void show() {
                System.out.println("class B show method");
            }
        }

        B b = new B();
        b.show();

        System.out.println("class A constructor");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
    }
}
```

---

##  Output

```text
class B show method
class A constructor
```

---


##  Local Inner Class inside Instance Block

---

###  Code

```java
class A {

    {
        class B {

            public void show() {
                System.out.println("class B show method");
            }
        }

        B b = new B();
        b.show();

        System.out.println("class A constructor");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
    }
}
```

---

## Output

```text
class B show method
class A constructor
```

---




##  Local Inner Class inside Static Block

---

###  Code

```java
class A {

    static {

        class B {

            public void show() {
                System.out.println("class B show method");
            }
        }

        B b = new B();
        b.show();

        System.out.println("class A static block");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
    }
}
```

---

##  Output

```text
class B show method
class A static block
```

---



##  Local Inner Class inside `if` Block

---

###  Code

```java
class A {

    void show() {

        if (true) {

            class B {

                public void show1() {
                    System.out.println("class B show1 method");
                }
            }

            B b = new B();
            b.show1();

            System.out.println("class A constructor");
        } else {
            System.out.println("Giriraj Patidar");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Output

```text
class B show1 method
class A constructor
```

---


##  Local Inner Class inside Loop

---

###  Code

```java
class A {

    void show() {

        for (int i = 1; i <= 5; i++) {

            class B {

                public void show1() {
                    System.out.println("class B show1 method");
                }
            }

            B b = new B();
            b.show1();

            System.out.println("class A constructor");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Output

```text
class B show1 method
class A constructor
class B show1 method
class A constructor
class B show1 method
class A constructor
class B show1 method
class A constructor
class B show1 method
class A constructor
```

---


##  Local Inner Class Accessing Outer Class Members

---

###  Code

```java
class A {

    int x = 10;
    static int y = 25;

    void show() {

        class B {

            public void show1() {
                System.out.println("x=" + x);
                System.out.println("y=" + y);
            }
        }

        B b = new B();
        b.show1();

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Output

```text
x=10
y=25
class A show method
```

---

## Accessing non static data from in local inner class inside static methods

---

###  Code

```java
class A {

    int x = 10;
    static int y = 25;

    static void show() {

        class B {

            public void show1() {
                System.out.println("x=" + x); // ❌ Error
                System.out.println("y=" + y); // ✅ Allowed
            }
        }

        B b = new B();
        b.show1();

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Error

```text
non-static variable x cannot be referenced from a static context
```

---



##  Local Inner Class inside Static Method 

---

### 📦 Code

```java
class A {

    static int y = 25;

    static void show() {

        class B {

            public void show1() {
                System.out.println("y=" + y);
            }
        }

        B b = new B();
        b.show1();

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        // A a1 = new A();
		// a1.show();
		
        A.show(); // better way to call static method
		
    }
}
```

---

##  Output

```text
y=25
class A show method
```

---


## 📌 Local Inner Class with Local Variable (Effectively Final Concept)

---

### 📦 Code

```java
class A {

    void show() {

        int y = 25;

        class B {

            public void show1() {
                System.out.println("y=" + y);
            }
        }

        B b = new B();
        b.show1();

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

## 🖥️ Output

```text
y=25
class A show method
```

---

## 💡 Explanation

### 🔹 Local Variable Access

```java
int y = 25;
```

👉 Used inside local inner class:

```java
System.out.println("y=" + y);
```

---

##  Important Concept

> Local inner class can access local variables **only if they are final or effectively final**

---

## 🔹 What is “Effectively Final”?

👉 A variable is **effectively final** if:

- Its value is assigned **once**
- It is **not modified later**

```java
int y = 25; // ✔ effectively final
```

---

## ⚠️ Java Version Difference

### ❌ Java 7 and Earlier

```java
final int y = 25; // compulsory
```

👉 Must explicitly declare `final`

---

###  Java 8 and Later

```java
int y = 25; // enough
```

👉 Compiler treats it as **effectively final**

---

##  Invalid Case

```java
int y = 25;
y = 30; // ❌ now not effectively final
```

👉 This will cause **compile-time error**

---

##  Key Understanding

| Java Version | Requirement        |
|--------------|-------------------|
| Java 7       | Must be `final`   |
| Java 8+      | Effectively final |

---

##  Interview Line

> “Local variables accessed inside inner classes must be final or effectively final; Java 8 introduced effectively final to remove the need for explicit final keyword.”

---




##  Modifying Local Variable in Inner Class (Invalid ❌)

---

###  Code

```java
class A {

    void show() {

        int y = 25;

        class B {

            public void show1() {

                y = 50; // ❌ Error
                System.out.println("y=" + y);
            }
        }

        B b = new B();
        b.show1();

        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

## Error

```text
local variables referenced from an inner class must be final or effectively final
```

---

## ❓ Why this error occurs?

👉 You declared:

```java
int y = 25;
```

👉 Then modified it:

```java
y = 50; // ❌
```

👉 So `y` is **not effectively final anymore**

---

## 🔥 Important Rule

> Local variables used inside inner class must be:
```text
final OR effectively final
```

---

## 🎯 What is wrong here?

```text
Initial value → 25
Changed value → 50
```

👉 Variable is modified → ❌ Not allowed

---

## ✅ Correct Solutions

---

### ✔️ Option 1: Do NOT Modify Variable

```java
int y = 25;

class B {
    public void show1() {
        System.out.println("y=" + y); // ✅ allowed
    }
}
```

---

### ✔️ Option 2: Use Wrapper Object 🔥

```java
class A {

    void show() {

        final int[] y = {25};

        class B {

            public void show1() {
                y[0] = 50; // ✅ allowed
                System.out.println("y=" + y[0]);
            }
        }

        B b = new B();
        b.show1();
    }
}
```

---

## 💡 Why wrapper works?

👉 Reference is final, but internal value can change ✔️

---

## 🎯 Key Understanding

| Case                          | Allowed |
|-------------------------------|--------|
| Read local variable           | ✅     |
| Modify local variable         | ❌     |
| Use effectively final         | ✅     |
| Use wrapper (array/object)    | ✅     |

---

##  Interview Line

> “Local variables used in inner classes must be final or effectively final; they cannot be modified, but their state can be changed using wrapper objects.”

---




##  Local Inner Class Without Using Local Variable

---

###  Code

```java
class A {

    void show() {

        int y = 25;

        class B {

            public void show1() {
                System.out.println("Giriaj patidar");
            }
        }

        B b = new B();
        b.show1();

        y = 55; // modifying local variable
        System.out.println("y=" + y);
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

## ️ Output

```text
Giriaj patidar
y=55
```

---

##  Explanation

### 🔹 Key Point

- Local variable `y` is **NOT used inside inner class `B`**

```java
System.out.println("Giriaj patidar");
```

👉 So **no effectively final rule applied**

---

### 🔹 Modification Allowed

```java
y = 55; // ✅ allowed
```

👉 Because:
- `y` is not accessed inside inner class  
- So it can be modified freely  

---

##  Important Concept

> Effectively final rule applies **only when variable is used inside inner class**

---

##  Key Understanding

| Case                              | Result |
|-----------------------------------|--------|
| Variable used inside inner class  | ❌ Must be final |
| Variable NOT used                 | ✅ Can modify |

---

##  Interview Line

> “A local variable can be modified freely if it is not accessed inside the inner class; otherwise, it must be final 
or effectively final.”

---




## 📌 Local Inner Class Using Variable (Error Case ❌)

---

### 📦 Code

```java
class A {

    void show() {

        int y = 25;

        class B {

            public void show1() {
                System.out.println(y); // ❌ Error
            }
        }

        B b = new B();
        b.show1();

        y = 55; // modifying variable
        System.out.println("y=" + y);
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Error

```text
local variables referenced from an inner class must be final or effectively final
```

---

##  Why this error occurs?

👉 You are doing 2 things:

```java
System.out.println(y); // using y inside inner class
y = 55;                // modifying y later
```

👉 So:

```text
y is NOT effectively final ❌
```

---

##  Important Rule

> If a local variable is used inside an inner class,  
> it must be **final or effectively final**

---

##  Problem Explained

```text
Step 1: y = 25   ✔
Step 2: used in inner class ✔
Step 3: y = 55   ❌ modified
```

👉 Once used → it must NOT change

---

##  Correct Solutions

---

###  Option 1: Do NOT Modify Variable

```java
int y = 25;

class B {
    public void show1() {
        System.out.println(y); // ✅ allowed
    }
}

// no modification
```

---

###  Option 2: Use Wrapper (Advanced )

```java
final int[] y = {25};

class B {
    public void show1() {
        System.out.println(y[0]);
    }
}

y[0] = 55; // ✅ allowed
```

---

##  Key Understanding

| Action                          | Allowed |
|---------------------------------|--------|
| Use variable in inner class     | ✅     |
| Modify variable after use       | ❌     |
| Keep variable effectively final | ✅     |

---

##  Interview Line

> “If a local variable is accessed inside an inner class, it must not be modified afterward; otherwise, it must be declared final or remain effectively final.”

---


#  Anonymous inner class :

1. Anonymous inner class that extends a class 



##  Example 

---



### 📦 Code

```java
abstract class A {

    public void show() {
        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A(); // ❌ Error
        a1.show();
    }
}
```

---

## 💥 Error

```text
A is abstract; cannot be instantiated
```

---



##  Example :

### 📦 Code

```java
abstract class A {

    public void show() {
        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A() { }; // ✅ Anonymous Inner Class
        a1.show();
    }
}
```

---

## ️ Output

```text
class A show method
```

---



##  Object Creation vs Anonymous Inner Class

---

## 🔹 Example 1: Normal Class

```java
class A {
    public void show() {
        System.out.println("class A show method");
    }
}

class B extends A {
}

class demo {
    public static void main(String ar[]) {
        A a1 = new B();
        a1.show();
    }
}
```

---

## 🔹 Example 2: Abstract Class + Subclass

```java
abstract class A {
    public void show() {
        System.out.println("class A show method");
    }
}

class B extends A {
}

class demo {
    public static void main(String ar[]) {
        A a1 = new B();
        a1.show();
    }
}
```

---

## 🔹 Example 3: Anonymous Inner Class 🔥

```java
abstract class A {
    public void show() {
        System.out.println("class A show method");
    }
}

class demo {
    public static void main(String ar[]) {
        A a1 = new A() { }; // anonymous inner class
        a1.show();
    }
}
```

---

##  Output (All Cases)

```text
class A show method
```

---

#  Difference Between

##  1. Normal Object Creation

```java
A a1 = new A();
```

###  Explanation

1. Object of **class A** is created  
2. Reference variable `a1` holds object of class A  
3. No inheritance or hidden class involved  

---

##  2. Anonymous Inner Class

```java
A a1 = new A() { };
```

###  Explanation

1. A **new unnamed (anonymous) class** is created  
2. This class **extends A**
3. Object of this anonymous class is created  
4. Reference variable of type `A` holds this object  

---





##  Anonymous Inner Class with Abstract Methods

---

##  Example 1: Missing Implementation (Invalid)

###  Code

```java
abstract class A {

    abstract public void show();
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A() {  // ❌ Error
        };
    }
}
```

---

##  Error

```text
<anonymous demo$1> is not abstract and does not override abstract method show() in A
```

---




##  Example 2: Correct Implementation

### 📦 Code

```java
abstract class A {

    abstract public void show();
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A() {

            public void show() {
                System.out.println("show method");
            }
        };

        a1.show();
    }
}
```

---

##  Output

```text
show method
```

---

##  Example 3: Multiple Anonymous Objects

### 📦 Code

```java
abstract class A {

    abstract public void show();
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A() {
            public void show() {
                System.out.println("show method");
            }
        };

        a1.show();

        A a2 = new A() {
            public void show() {
                System.out.println("show method repeat");
            }
        };

        a2.show();
    }
}
```

---

## 🖥️ Output

```text
show method
show method repeat
```

---



##  Example 4: Method with Return Value

### 📦 Code

```java
abstract class A {

    abstract public int cube(int x);
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A() {

            public int cube(int x) {
                return x * x * x;
            }
        };

        int result = a1.cube(10);
        System.out.println(result);
    }
}
```

---

##  Output

```text
1000
```

---



##  Anonymous Inner Class – Direct Method Call & Errors

---

## Example 1: Direct Method Call (Valid)

### 📦 Code

```java
abstract class A {

    abstract public void show();
}

class demo {

    public static void main(String ar[]) {

        new A() {

            public void show() {
                System.out.println("show method");
            }

        }.show(); // direct call
    }
}
```

---

## 🖥️ Output

```text
show method
```

---



##  Example 2: Wrong Assignment (Invalid)

### 📦 Code

```java
abstract class A {

    abstract public void show();
}

class demo {

    public static void main(String ar[]) {

        A a = new A() {

            public void show() {
                System.out.println("show method");
            }

        }.show(); // ❌ Error
    }
}
```

---

## 💥 Error

```text
incompatible types: void cannot be converted to A
```

---



##  Example 3: Returning Value (Valid)

### 📦 Code

```java
abstract class A {

    abstract public int cube(int x);
}

class demo {

    public static void main(String ar[]) {

        int x = new A() {

            public int cube(int x) {
                return x * x * x;
            }

        }.cube(10);

        System.out.println(x);
    }
}
```

---

## 🖥️ Output

```text
1000
```

---



## ❌ Example 4: Wrong Assignment (Invalid)

### 📦 Code
```java
abstract class A {

    abstract public int cube(int x);
}

class demo {

    public static void main(String ar[]) {

        int x = new A() { // ❌ Error

            public int cube(int x) {
                return x * x * x;
            }
        };
    }
}
```

---

## 💥 Error

```text
incompatible types: <anonymous A> cannot be converted to int
```

---



## 📌 Anonymous Inner Class – Real Use Case (Method Override for Specific Object)

---

## 🔹 Example 1: Normal Inheritance (All Objects Same Behavior)

### 📦 Code

```java
class Employee {

    public void cName() {
        System.out.println("Softwaves Tech");
    }

    public void sal() {
        System.out.println("50,000");
    }
}

class Employee2 extends Employee {

    public void sal() {
        System.out.println("70,000");
    }
}

class demo {

    public static void main(String ar[]) {

        Employee abhi = new Employee2();
        Employee sita = new Employee2();
        Employee gita = new Employee2();

        abhi.cName();
        abhi.sal();

        sita.cName();
        sita.sal();

        gita.cName();
        gita.sal();
    }
}
```

---

## 🖥️ Output

```text
Softwaves Tech
70,000
Softwaves Tech
70,000
Softwaves Tech
70,000
```

---

## 💡 Problem

👉 All objects (`abhi`, `sita`, `gita`) have **same salary (70,000)**  
👉 But requirement:

```text
Only abhi → 70,000
Others → 50,000
```

---

# 🔥 Example 2: Using Anonymous Inner Class (Best Solution ✅)

### 📦 Code

```java
class Employee {

    public void cName() {
        System.out.println("Softwaves Tech");
    }

    public void sal() {
        System.out.println("50,000");
    }
}

class demo {

    public static void main(String ar[]) {

        Employee abhi = new Employee() {

            public void sal() {
                System.out.println("70,000"); // overridden only for abhi
            }
        };

        Employee sita = new Employee();
        Employee gita = new Employee();

        abhi.cName();
        abhi.sal();

        sita.cName();
        sita.sal();

        gita.cName();
        gita.sal();
    }
}
```

---

## 🖥️ Output

```text
Softwaves Tech
70,000
Softwaves Tech
50,000
Softwaves Tech
50,000
```

---


## 📌 Adapter Class in Java

---

### 💡 Definition

An **Adapter Class** is an **abstract class** that provides **default (empty) implementation of an interface**.

👉 It allows us to override **only the required methods**, instead of implementing all methods of the interface.

---

## 🔥 Why Adapter Class?

👉 Normally, when we implement an interface:

```java
interface MyInterface {
    void m1();
    void m2();
    void m3();
}
```

👉 We must implement **all methods** ❌

---

## ❌ Without Adapter Class

```java
class Test implements MyInterface {

    public void m1() {
        System.out.println("m1");
    }

    public void m2() {
    }

    public void m3() {
    }
}
```

👉 Unnecessary boilerplate code 😓  

---

## ✅ With Adapter Class

```java
abstract class MyAdapter implements MyInterface {

    public void m1() {}
    public void m2() {}
    public void m3() {}
}
```

---

### 🔹 Now use Adapter

```java
class Test extends MyAdapter {

    public void m1() {
        System.out.println("Only required method");
    }
}
```

---

## 🖥️ Output

```text
Only required method
```

---



2. Annonymous inner class that implement a interface



## 📌 Interface + Anonymous Inner Class

---

## ❌ Example 1: Direct Object Creation (Invalid)

### 📦 Code

```java
interface inter1 {

    public void show();
}

class demo {

    public static void main(String ar[]) {

        inter1 i = new inter1(); // ❌ Error
    }
}
```

---

## 💥 Error

```text
inter1 is abstract; cannot be instantiated
```

---


## ✅ Example 2: Using Implementation Class

### 📦 Code

```java
interface inter1 {

    public void show();
}

class A implements inter1 {

    public void show() {
        System.out.println("class A show method");
    }
}

class demo {

    public static void main(String ar[]) {

        A a1 = new A();
        a1.show();
    }
}
```

---

##  Output

```text
class A show method
```

---

##  Example 3: Anonymous Class Without Implementation

### 📦 Code

```java
interface inter1 {

    public void show();
}

class demo {

    public static void main(String ar[]) {

        inter1 i = new inter1() {  // ❌ Error
        };
    }
}
```

---

##  Error

```text
<anonymous demo$1> is not abstract and does not override abstract method show() in inter1
```

---



##  Example 4: Anonymous Inner Class (Correct 🔥)

### 📦 Code

```java
interface inter1 {

    public void show();
}

class demo {

    public static void main(String ar[]) {

        inter1 i = new inter1() {

            public void show() {
                System.out.println("show method");
            }
        };

        i.show();
    }
}
```

---

## ️ Output

```text
show method
```

---



# Static Inner  class  :



##  Static Nested Class Example

---

###  Code

```java
class demo {

    static class A {

        public void show() {
            System.out.println("class A show method");
        }
    }

    public static void main(String ar[]) {

        A a1 = new A(); // creating object of static nested class
        a1.show();
    }
}
```

---

##  Output

```text
class A show method
```

---




##  Example : Static Nested Class Access Error ❌

---

### 📦 Code

```java
class A {

    static class B {

        public void show() {
            System.out.println("class B show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        B b1 = new B(); // ❌ Error
        b1.show();
    }
}
```

---

## 💥 Error

```text
cannot find symbol
symbol: class B
```

---




##  Static Nested Class (Correct Usage ✅)

---

### 📦 Code

```java
class A {

    static class B {

        public void show() {
            System.out.println("class B show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A.B b1 = new A.B(); // creating object of static nested class
        b1.show();
    }
}
```

---

##  Output

```text
class B show method
```

---


## 📌 Static Nested Class with Static Member

---

### 📦 Code

```java
class A {

    static class B {

        static int x = 10;

        public void show() {
            System.out.println("x=" + x);
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A.B b1 = new A.B();
        b1.show();
    }
}
```

---

## 🖥️ Output

```text
x=10
```

---


## 📌 Static Nested Class with Static Method

---

### 📦 Code

```java
class A {

    static class B {

        public static void show() {
            System.out.println("static method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A.B.show(); // calling static method
    }
}
```

---

## 🖥️ Output

```text
static method
```

---


## 📌 Static Nested Class with `main()` Method

---

### 📦 Code

```java
class A {

    static class B {

        public static void main(String ar[]) {
            System.out.println("static method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        // No code here
    }
}
```

---

## 🖥️ Output (How to Run)

### ▶ Run Outer Class

```bash
java demo
```

```text
(no output)
```

---

### ▶ Run Nested Class

```bash
java A$B
```

```text
static method
```

---



## 📌 Static Nested Class Accessing Outer Members (Error ❌)

---

### 📦 Code

```java
class A {

    int x = 10;
    static int y = 20;

    static class B {

        public void show() {

            System.out.println("x=" + x); // ❌ Error
            System.out.println("y=" + y); // ✅ Allowed
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A.B b1 = new A.B();
        b1.show();
    }
}
```

---

## 💥 Error

```text
non-static variable x cannot be referenced from a static context
```

---

## ❓ Why this error occurs?

👉 `B` is a **static nested class**

```java
static class B
```

👉 So inside `B`:
- ❌ Cannot access instance variable `x` directly  
- ✅ Can access static variable `y`  

---

## 🔥 Important Rule

> Static nested class can access only **static members of outer class directly**

---

## 🎯 Problem Line

```java
System.out.println("x=" + x); // ❌
```

👉 `x` is instance variable → needs object  

---

## ✅ Correct Solutions

---

### ✔️ Option 1: Create Object of Outer Class

```java
static class B {

    public void show() {

        A a = new A();

        System.out.println("x=" + a.x); // ✅ fixed
        System.out.println("y=" + y);
    }
}
```

---

###  Option 2: Make `x` Static

```java
static int x = 10;
```

👉 Now directly accessible ✔️  

---

## ️ Correct Output

```text
x=10
y=20
```

---



## 📌 Interface Inside Class (Error Case ❌)

---

### 📦 Code

```java
class A {

    interface inter1 {

        void show();
    }

    class B implements inter1 {

        // ❌ No implementation
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        A.B b = a.new B();
    }
}
```

---

## 💥 Error

```text
A.B is not abstract and does not override abstract method show() in inter1
```

---



##  Interface Inside Class (Correct Usage ✅)

---

### 📦 Code

```java
class A {

    interface inter1 {

        void show();
    }

    class B implements inter1 {

        public void show() {
            System.out.println("class B show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();

        A.B b = a.new B(); // creating object of inner class
        b.show();
    }
}
```

---

##  Output

```text
class B show method
```

---



##  Interface Inside Class (Implemented Outside Class ✅)

---

### 📦 Code

```java
class A {

    interface inter1 {

        void show();
    }
}

class B implements A.inter1 {

    public void show() {
        System.out.println("class B show method");
    }
}

class demo {

    public static void main(String ar[]) {

        B b = new B();
        b.show();
    }
}
```

---

##  Output

```text
class B show method
```

---


##  Static Nested Class with Static Method (Best Usage ✅)

---

### 📦 Code

```java
class A {

    static class B {

        public static void show() {
            System.out.println("class B show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A.B.show(); // direct static method call
    }
}
```

---

##  Output

```text
class B show method
```

---




##  Static Nested Class with `main()` + Instance Method

---

### 📦 Code

```java
class A {

    static class B {

        public static void main(String ar[]) {
            // empty main
        }

        public void show() {
            System.out.println("Giriraj Patidar");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        A.B b = new A.B(); // object creation
        b.show();

        System.out.println("Main method");
    }
}
```

---

##  Output (Running `demo`)

```text
Giriraj Patidar
Main method
```

---



##  Nested Interface (Interface inside Interface) ✅

---

### 📦 Code

```java
interface inter1 {

    void show1();

    interface inter2 {

        void show2();
    }
}

class A implements inter1 {

    public void show1() {
        System.out.println("class A");
    }
}

class B implements inter1.inter2 {

    public void show2() {
        System.out.println("class B");
    }
}

class demo {

    public static void main(String ar[]) {

        A a = new A();
        a.show1();

        B b = new B();
        b.show2();
    }
}
```

---

## ️ Output

```text
class A
class B
```

---


##  Class Inside Interface (Nested Class in Interface) 

---

### 📦 Code

```java
interface inter1 {

    class A {

        public void show() {
            System.out.println("show method");
        }
    }
}

class demo {

    public static void main(String ar[]) {

        inter1.A a = new inter1.A(); // accessing nested class
        a.show();
        a.show();
    }
}
```

---

##  Output

```text
show method
show method
```

---



##  Class Inside Interface → Always `public static` ✅

---

### 📦 Code

```java
interface inter1 {

    class A {

        public void show() {
            System.out.println("show method");
        }
    }
}

class B implements inter1 {
}

class demo {

    public static void main(String ar[]) {

        B.A a = new B.A(); // accessing nested class
        a.show();
    }
}
```

---

## ️ Output

```text
show method
```

---


##  Class Inside Interface → Inheritance (extends) ✅

---

### 📦 Code

```java
interface inter1 {

    class A {

        public void show() {
            System.out.println("show method");
        }
    }
}

class B extends inter1.A {
}

class demo {

    public static void main(String ar[]) {

        B b = new B();
        b.show();
    }
}
```

---

##  Output

```text
show method
```

---

