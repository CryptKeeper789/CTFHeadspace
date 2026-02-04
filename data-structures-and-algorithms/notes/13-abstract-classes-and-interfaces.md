## 13.1 Intro
A super class defines common behaviors for related subclasses. 
An **interface** can be used to define common behavior for classes (including unrelated classes).
- example: writing code to sort an array of geometric objects. 
- **interface**: 
	- Cannot create an instance/object of.
	- Can have data and methods
		- data: must be constants
		- methods: can have only declarations w/o implementation
	- Eased single inheritance:
		- Single inheritance: Restriction where a class can inherit from a single super class
## 13.2 Abstract Classes
classes become more specific and concrete with each new subclass. 
classes become more general and less specific as you move up the hierarchy. 
**Abstract class:** A class for abstract and non-specific that it cannot be used to create any instances. 
- no instances can be made using the `new` operator.
**Abstract Methods**: A method signature without implementation (body) Implementation is provided by its subclasses. 
- denoted with `abstract` modifier
- contained in the abstract class.
- in an abstract classes' subclasses all abstract methods must be implemented at the lowest subclass level (given a subclass is also abstract)
### UML notation for abstract classes
![[13-abstract-UML.png]]
Reminder: `protected` means can be accessed in the same package. 
- constructors are protected because they are only used by its subclasses. 
![[13-subclass-to-abstract-class.png]]

## 13.2.1 Abstract Methods
The JVM, due to dynamic binding, determines which overridden method to invoke at **run time**. This depends on the **actual type** of object that invokes the method. (The **declared type*** of a polymorphic object is the abstract class in this case)

**For Example**: you could not define `equalsArea()` method for comparing whether two geometric objects, with the declared type of  `GeometricObject`, have the same area if `getArea()` were not defined in `GeometricObject` 

## 13.2.2 Interesting Points
- An abstract method cannot be contained in a non-abstract class. 
- If a subclass of an abstract super class doesn't implement all abstract methods it must be defined as abstract and have sub classes that implement it. 
- Abstract methods are **non-static.**
- Abstract classes cannot be instantiated. However you can still define its constructors. 
- An abstract class doesn't HAVE to contain abstract methods. This type of class is called a **base** class. 
- A subclass can override a method from its superclass to define it as abstract. 
**Example:**
<pre> 
		class abstract SubClass extends SuperClass {
			@override
			public void abstract method();`
		}  
</pre>

- A subclass can be abstract even if its super class is concrete. 
	- Ex: Object class is concrete (The God of all object classes including abstract ones)
- An abstract class can be used as a data type. 
<pre> 
AbstractObjectClass[] objects = new AbstractObjectClass[10];
</pre>
You can then create an instance of `AbstractObjectClass` and assign its reference to the array like this:
<pre> 
objects[0] = new SubClassObjec();
</pre>
## Calendar Class
![[13-abstract-class-calender.png]]
![[13-abstract-class-calendar-constants.png]]
## 13.5 Interfaces

**Interfaces**: A class-like construct for defining common operations for objects.
- Contains only
	- Abstract Methods
	- Constants
- Interface Inheritance
- Defines how a class should *behave*
- Does NOT define implementation.
**Example:** 
```java
public interface Edible {
	public abstract String howToEat();
}

public class TestEdible {
	Objects[] objects = {new Tiger(), new Chicken(), new Apple()}
	for (int i = 0; i < objects.length; i++) {
		if (objects[i] instanceof Edible) {
			System.out.println((Edible)object[i].howToEat());
		}
	}
}

class Animal{
}

class Chicken extends Animal implements Edible {
	public String howToEat() {
		return "Chicken: Fry it";
	}
}

class Tiger extends Animal {
}

abstract class Fruit implements Edible {
}

class Apple extends Fruit {
	public String howToEat() {
		return "Apple: Make apple cider";
	}
}
```
- `extends` forces an is-a **relationship**.
- `implements` forces the class to implement the methods in the interface class. 
- The `Fruit` class doesn't HAVE to implement the specified methods in the `Edible` class as long its sub classes do. It is therefore an abstract class.
- The `Apple` class must implement `howToEat()`
	- Doesn't have to use keyword `implements` b/c its super class did.
- Tiger is not an `instanceof` Edible so it would be be `False` in the if-statement test.
- `Edible` is a **super type** for `Chicken` and `Fruit`. `Animal` is a **super type** for `Chicken` and `Tiger`. `Fruit` is a **super type** for `Orange` and `Apple`
![[13-interfaces-diagram.png]]

> **Note:** The modifiers `public static final` on data fields and the modifiers `public abstract` methods can be omitted in an interface. 
> **However**: The method must be have the `public` modifier when implemented in its subclass.

![[13-interface-note1.png]] ![[13-interface-note2.png]]

#### Default Method in an Interface
Provides a default implementation for the method in the interface. A class that implements the interface can use the default implementation for the method OR override the method with new implementation. 
- Enables adding a new method to an existing interface w/o having to rewrite the code for the existing classes that implement the interface. 
#### Public Static Methods
Can be used in an interface just like it is in a class

## 13.6 The Comparable Interface
![[13-compareTo-interface.png]]
Determines the order of object `E` with object `o` and returns `-` integer, `0`, or a `+` integer if object `e` is less than equal to, or greater than `o`

#### Example:
![[13-interface-compareto-example.png]]
#### Classes that Implement Comparable Interface:
- Byte, Short, Integer, Long, Float, Double, Character
- BigInteger, BigDecimal
- Calandar, Date
- String
![[13-instanceof-comparable.png]]
Since all `Comparable` objects have the `compareTo` method, `java.util.Arrays.sort(Object[])` in Java API uses the `compareTo` method to compare and sort the objects in the array. The objects must be an `instanceof` the Comparable interface. 

You can create classes that implement the `Comparable` interface and then override its `compareTo` method. 

Example:
![[13-compareto-override-code-example.png]]
![[13-compareto-custom-example.png]]
Now an Array of `ComparableRectangles` can be sorted. 

## 13.7 The Cloneable Interface
`Cloneable` Interface specifies that an object can be cloned. 

```java
package java.lang;

public interface Clonable {
}
```
 **marker interface**: An empty interface that is used to signify that all the classes implementing the interface share certain properties. 
 - classes that implement this interface can be cloned uising the clone() method defined in the objects class. 
	 - classes `Date` `Calandar` and `ArrayList` implement this interface. 
**Example
![[13-cloned-interface-example.png]]

You can also clone an array using the `clone()` method
**Example**
```Java
int[] list1 = [1,2];
int[] list2 = list1.clone(); //list2 is a clone of list1
```

> Cloning objects essentially creates new objects with the same attributes. (not duplicating the pointer to a memory address)

To define a custom class that implements the `Clonable` interface, the class must override the clone() method in the `Object` class. 
**Custom Clone Example:**
![[13-custom-clone-example.png]]

The header for the clone method in the `Object` class is:
```java
protected native Object clone() throws CloneNotSupportedException
```
- `native` - this method is not written in Java but is implementewd in the JVM native platform,
- `protected` restricts access to be in the same package or subclass. 
	- House` class myst `@override` the method and change the visability
- The `clone()` in the `House` class invokes `super.clone()` to have object perform the cloning task. 
- If an object is not cloneable the object class with throw `CloneNotSupportedException` so the house catches the exception in the `clone()` method body.
- If an attribute is an object the reference to the object attribute will be shallow copied (not the object's own data fields)
	- **Shallow Copy**: All fields are copied
	- **Deep Copy**: All fields are copied recursively
- For a deep copy its more complicated:
  ```java
  public class House implements Cloneable, Comparable<House> {
  private int id;
  private double area;
  private java.util.Date whenBuilt;
  
  public House(int id, double area) {
    this.id = id;
    this.area = area;
    whenBuilt = new java.util.Date();
  }
  
  public int getId() {
    return id;
  }
  
  public double getArea() {
    return area;
  }

  public java.util.Date getWhenBuilt() {
    return whenBuilt;
  }

  @Override /** Override the protected clone method defined in 
    the Object class, and strengthen its accessibility */
  public Object clone() throws CloneNotSupportedException {
    // Perform a shallow copy
    House houseClone = (House)super.clone(); 
    // Deep copy on whenBuilt
    houseClone.whenBuilt = (java.util.Date)(whenBuilt.clone()); 
    return houseClone;
  }
  
  @Override // Implement the compareTo method defined in Comparable
  public int compareTo(House o) {
    if (area > o.area)
      return 1;
    else if (area < o.area)
      return -1;
    else
      return 0;
  }  
}
  ```

## 13.8 Interfaces v. Abstract Classes
![[13-interfaces-v-abstract-classes.png]]

You can implement multiple interfaces:
```java
public class NewClass extends BaseClass implements Interface1, Interface2,...,InterfaceN {
//code
}
```

**Subinterface**: one interface inherit other interfaces:

```java
public interface NewInterface extends Interface1,...,InterfaceN {
//constant and abstract methods
}
```

A class implementing `NewInterface` must implement the abstract methods defined in the `NewInterface` as well as all the interfaces it inherits. 

Like a class an interface is a type that can be type-casted. In this way an interface acts very much like a super class. You can use an interface as a data type and cast a variable of an interface type to its subclass and vice versa. 

**For Example**: let `z` be an `instanceof` `Class2` Thighs means that its also an `instanceof` everything `Class2` is either an `instanceof` or `implements`. 
![[13-instanceof-example.png]]

> **Note:** Class names are nouns and interface names can be nouns or adjectives (tall, beautiful, comparable happy)

#### When to use Which
- Classes: When there is a strong is-a parent/child relationship
- Interfaces: When there is a weak is-a relationship a.k.a *is-kind-of-relationship*
	- object possess certain properties
	- Example: all `Strings` are `Comparable`.

## 13.10 Class Design Guideline

## 13.11 Records
 
 