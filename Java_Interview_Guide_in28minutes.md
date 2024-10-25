# Interface

- An interface defines a contract for responsibilities (methods) of a class.
- It is a way to specify a contract for what a class must do, without dictating how it should do it.
- Example in Java api : Map interface, Collection interface.
- An interface is declared by using the keyword interface. Look at the example below: Flyable is an
interface.

```java
interface InterfaceName {
    // Abstract method (implicitly public and abstract)
    void abstractMethod();
    
    // Default method (introduced in Java 8)
    default void defaultMethod() {
        System.out.println("This is a default method");
    }
    
    // Static method (introduced in Java 8)
    static void staticMethod() {
        System.out.println("This is a static method");
    }

    // Constant (implicitly public, static, final)
    int CONSTANT = 100;
}

```
- A class that implements an interface must provide concrete implementations for all the interface's abstract methods.

```java 
class MyClass implements InterfaceName {
    // Implementing abstract method
    @Override
    public void abstractMethod() {
        System.out.println("Implemented abstract method");
    }
}

public class Main {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.abstractMethod();  // Output: Implemented abstract method
        
        // Calling default method
        obj.defaultMethod();  // Output: This is a default method
        
        // Calling static method (via interface name)
        InterfaceName.staticMethod();  // Output: This is a static method
    }
}
```
- Multiple Interfaces: A class can implement multiple interfaces, enabling multiple inheritance behavior:

```java 
class MyClass implements Interface1, Interface2 {
    // Must implement methods from both interfaces
}
```
- Variables in an interface are always public, static, final. Variables in an interface cannot be declared private.
- Interface methods are by default public and abstract. Before Java 8, A concrete method (fully defined method) cannot be created in an interface

```java
interface ExampleInterface1 {
//By default - public abstract. No other modifier allowed
void method1();//method1 is public and abstract
//private void method6();//COMPILER ERROR!
//This method, uncommented, would have given COMPILER ERROR!

//in Java 7. Allowed from Java 8.
default void method5() {
System.out .println("Method5");
}
}
```
- An interface can extend another interface. 
- An interface cannot extend a class.
- A class can implement multiple interfaces. It should implement all the method declared in all Interfaces being implemented.
```java
public class HashMap<K,V> extends AbstractMap<K,V>
implements Map<K,V>, Cloneable, Serializable
```
- Interfaces cannot have constructors because they cannot be instantiated directly.
- An interface cannot contain instance fields, only constants (public static final).
- **Default Methods** (Java 8 and later): An interface can have default methods, which are methods with a body. These allow interfaces to provide default behavior without forcing implementing classes to override them.
- **Static methods** (Java 8 and later): Interfaces can also have static methods, which can be called on the interface itself rather than on an instance of the class.

# Abstract class

- An abstract class is a class that cannot be instantiated, but must be inherited from. An abstract class may be fully implemented, but is more usually partially implemented or not implemented at all, thereby encapsulating common functionality for inherited classes.
 ```java
 bstract class Animal {  // Abstract class
    // Abstract method (no implementation)
    public abstract void sound();

    // Concrete method (has an implementation)
    public void sleep() {
        System.out.println("This animal is sleeping.");
    }
}

class Dog extends Animal {  // Concrete subclass of Animal
    // Implementing the abstract method
    public void sound() {
        System.out.println("Woof Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();  // Creating an object of Dog
        myDog.sound();  // Output: Woof Woof!
        myDog.sleep();  // Output: This animal is sleeping.
    }
}
```
- If you want to provide common, implemented functionality among all implementations of your
component, use an abstract class. Abstract classes allow you to partially implement your class.
- An example of an abstract class in the JDK is **AbstractMap**, which is part of the Collections
Framework. Its subclasses (which include **HashMap**, **TreeMap**, and **ConcurrentHashMap**) share
many methods (including **get**, **put**, **isEmpty**, **containsKey**, and **containsValue**) that AbstractMap defines.
- Example abstract method : *public abstract Set> entrySet()*;
- Consider using abstract classes and inheritance when our problem makes the evidence “A is a B”. For example, “Dog is an Animal”, “Lamborghini is a Car”, etc.

# When do you use an interface? #
- If the problem needs to be solved using multiple inheritances and is composed of different class hierarchies.
- When unrelated classes implement our interface. For example, Comparable provides the compareTo() method that can be overridden to compare two objects.
- Consider using the interface when our problem makes the statement “A is capable of [doing this]”. For example, “Clonable is capable of cloning an object”, “Drawable is capable of drawing a shape”, etc.
