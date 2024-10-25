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

# Modifiers #
What is default class modifier?
- A class is called a Default Class is when there is no access modifier specified on a class.
- Default classes are visible inside the same package only.
- Default access is also called Package access.
Example
```java
package com.rithus.classmodifiers.defaultaccess.a;
/* No public before class. So this class has default access*/
class DefaultAccessClass {
//Default access is also called package access
}
```
Another Class in Same Package: Has access to default class
```java
package com.rithus.classmodifiers.defaultaccess.a;
public class AnotherClassInSamePackage {
//DefaultAccessClass and AnotherClassInSamePackage
//are in same package.
//So, DefaultAccessClass is visible.
//An instance of the class can be created.
DefaultAccessClass defaultAccess;
}
```
Class in Different Package: NO access to default class
```java
package com.rithus.classmodifiers.defaultaccess.b;
public class ClassInDifferentPackage {
//Class DefaultAccessClass and Class ClassInDifferentPackage
//are in different packages (*.a and *.b)
//So, DefaultAccessClass is not visible to ClassInDifferentPackage
//Below line of code will cause compilation error if uncommented
//DefaultAccessClass defaultAccess; //COMPILE ERROR!!
}
```
## What is private access modifier? ##
- Private variables and methods can be accessed only in the class they are declared.
- Private variables and methods from SuperClass are NOT available in SubClass.

## What is default or package access modifier? ##
a. Default variables and methods can be accessed in the same package Classes.
b. Default variables and methods from SuperClass are available only to SubClasses in same package.

## What is protected access modifier? ##
a. Protected variables and methods can be accessed in the same package Classes.
b. Protected variables and methods from SuperClass are available to SubClass in any package

# What is public access modifier? ##
a. Public variables and methods can be accessed from every other Java classes.
b. Public variables and methods from SuperClass are all available directly in the SubClass

# What access types of variables can be accessed from a Class in Same Package? ##
Look at the code below to understand what can be accessed and what cannot be.
```java
package com.rithus.membermodifiers.access;
public class TestClassInSamePackage {
public static void main(String[] args) {
ExampleClass example = new ExampleClass();
example.publicVariable = 5;
example.publicMethod();
//privateVariable is not visible
//Below Line, uncommented, would give compiler error
//example.privateVariable=5; //COMPILE ERROR
//example.privateMethod();
example.protectedVariable = 5;
example.protectedMethod();
example.defaultVariable = 5;
example.defaultMethod();
}
}
```
## What access types of variables can be accessed from a Class in Different Package? ##
Look at the code below to understand what can be accessed and what cannot be.
```java
package com.rithus.membermodifiers.access.different;
import com.rithus.membermodifiers.access.ExampleClass;
public class TestClassInDifferentPackage {
public static void main(String[] args) {
ExampleClass example = new ExampleClass();
example.publicVariable = 5;
example.publicMethod();
//privateVariable,privateMethod are not visible
//Below Lines, uncommented, would give compiler error
//example.privateVariable=5; //COMPILE ERROR
//example.privateMethod();//COMPILE ERROR
//protectedVariable,protectedMethod are not visible
//Below Lines, uncommented, would give compiler error
//example.protectedVariable = 5; //COMPILE ERROR
//example.protectedMethod();//COMPILE ERROR
//defaultVariable,defaultMethod are not visible
//Below Lines, uncommented, would give compiler error
//example.defaultVariable = 5;//COMPILE ERROR
//example.defaultMethod();//COMPILE ERROR
}
}
```
## What access types of variables can be accessed from a Sub Class in Same Package? ##
Look at the code below to understand what can be accessed and what cannot be.
```java
package com.rithus.membermodifiers.access;
public class SubClassInSamePackage extends ExampleClass {
void subClassMethod(){
publicVariable = 5;
publicMethod();
//privateVariable is not visible to SubClass
//Below Line, uncommented, would give compiler error
//privateVariable=5; //COMPILE ERROR
//privateMethod();
protectedVariable = 5;
protectedMethod();
defaultVariable = 5;
defaultMethod();
}
}
```
## What access types of variables can be accessed from a Sub Class in Different Package? ##
Look at the code below to understand what can be accessed and what cannot be.
```java
package com.rithus.membermodifiers.access.different;
import com.rithus.membermodifiers.access.ExampleClass;
public class SubClassInDifferentPackage extends ExampleClass {
void subClassMethod(){
publicVariable = 5;
publicMethod();
//privateVariable is not visible to SubClass
//Below Line, uncommented, would give compiler error
//privateVariable=5; //COMPILE ERROR
//privateMethod();
protectedVariable = 5;
protectedMethod();
//privateVariable is not visible to SubClass
//Below Line, uncommented, would give compiler error
//defaultVariable = 5; //COMPILE ERROR
//defaultMethod();
}
}
```
## What is the use of a final modifier on a class? ##
Final class cannot be extended. Example of Final class in Java is the String class. Final is used very
rarely as it prevents re-use of the class.Consider the class below which is declared as final.
Final Class examples : String, Integer, Double and other wrapper classes
```java
final public class FinalClass {
}
Below class will not compile if uncommented. FinalClass cannot be extended.
/*
class ExtendingFinalClass extends FinalClass{ //COMPILER ERROR
}
*/
```
## What is the use of a final modifier on a method? ##
Final methods cannot be overridden. Consider the class FinalMemberModifiersExample with method finalMethod which is declared as final.
public class FinalMemberModifiersExample {
final void finalMethod(){
}
}
Any SubClass extending above class cannot override the finalMethod().
```java
class SubClass extends FinalMemberModifiersExample {
//final method cannot be over-riddent
//Below method, uncommented, causes compilation Error
/*
final void finalMethod(){
}
*/
}
```
## What is a Final variable? ##
Once initialized, the value of a final variable cannot be changed.
```java
final int finalValue = 5;
//finalValue = 10; //COMPILER ERROR
Final Variable example : java.lang.Math.PI
What is a final argument?
Final arguments value cannot be modified. Consider the example below:
void testMethod(final int finalArgument){
//final argument cannot be modified
//Below line, uncommented, causes compilation Error
//finalArgument = 5;//COMPILER ERROR
}
```
## What happens when a variable is marked as volatile? ##
• Volatile can only be applied to instance variables.
• A volatile variable is one whose value is always written to and read from "main memory". Each
thread has its own cache in Java. The volatile variable will not be stored on a Thread cache.
## What is a Static Variable? ##
Static variables and methods are class level variables and methods. There is only one copy of the static variable for the entire Class. Each instance of the Class (object) will NOT have a unique copy of a static variable. Let’s start with a real world example of a Class with static variable and methods.
Static Variable/Method – Example
count variable in Cricketer class is static. The method to get the count value getCount() is also a static method.
```java
public class Cricketer {
private static int count;
public Cricketer() {
count++;
}
static int getCount() {
return count;
}
public static void main(String[] args) {
Cricketer cricketer1 = new Cricketer();
Cricketer cricketer2 = new Cricketer();
Cricketer cricketer3 = new Cricketer();
Cricketer cricketer4 = new Cricketer();
System.out.println(Cricketer.getCount());//4
}
}
```
4 instances of the Cricketer class are created. Variable count is incremented with every instance created in the constructor.

