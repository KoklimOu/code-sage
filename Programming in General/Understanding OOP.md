Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects," which can contain data and methods. Java is a widely used programming language that follows the OOP principles. Let's explore the core concepts of OOP in the context of Java:

### 1. Classes and Objects
- **Class**: A blueprint for creating objects. It defines a datatype by bundling data (fields) and methods (functions) that operate on the data into one single unit.
- **Object**: An instance of a class. When a class is defined, no memory is allocated until an object of that class is created.

**Example:**
```java
class Car {
    // Fields (or instance variables)
    String color;
    String model;
    int year;

    // Method
    void displayDetails() {
        System.out.println("Model: " + model);
        System.out.println("Color: " + color);
        System.out.println("Year: " + year);
    }
}

public class Main {
    public static void main(String[] args) {
        // Creating an object of Car class
        Car myCar = new Car();
        myCar.color = "Red";
        myCar.model = "Tesla Model S";
        myCar.year = 2021;
        myCar.displayDetails();
    }
}
```

### 2. Inheritance
Inheritance is a mechanism where one class inherits the fields and methods of another class. The class that inherits is called the subclass, and the class from which it inherits is called the superclass.

**Example:**
```java
class Vehicle {
    String brand;

    void honk() {
        System.out.println("Honk! Honk!");
    }
}

class Car extends Vehicle {
    String model;

    void displayDetails() {
        System.out.println("Brand: " + brand);
        System.out.println("Model: " + model);
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.brand = "Tesla";
        myCar.model = "Model S";
        myCar.honk();
        myCar.displayDetails();
    }
}
```

### 3. Polymorphism
Polymorphism allows methods to do different things based on the object it is acting upon. It is mainly achieved through method overriding (runtime polymorphism) and method overloading (compile-time polymorphism).

**Example: Method Overriding:**
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();  // Outputs "Dog barks"
    }
}
```

### 4. Encapsulation
Encapsulation is the technique of making the fields in a class private and providing access to the fields via public methods (getters and setters). This helps in protecting the data from unauthorized access and modification.

**Example:**
```java
class Person {
    private String name;
    private int age;

    // Getter method for name
    public String getName() {
        return name;
    }

    // Setter method for name
    public void setName(String newName) {
        name = newName;
    }

    // Getter method for age
    public int getAge() {
        return age;
    }

    // Setter method for age
    public void setAge(int newAge) {
        age = newAge;
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("John");
        person.setAge(30);
        System.out.println("Name: " + person.getName());
        System.out.println("Age: " + person.getAge());
    }
}
```

### 5. Abstraction
Abstraction is the concept of hiding the complex implementation details and showing only the essential features of the object. It can be achieved using abstract classes and interfaces.

**Example: Abstract Class:**
```java
abstract class Animal {
    abstract void sound();

    void sleep() {
        System.out.println("Animal is sleeping");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}

public class Main {
    public static void main(String[] args) {
        Cat myCat = new Cat();
        myCat.sound();  // Outputs "Cat meows"
        myCat.sleep();  // Outputs "Animal is sleeping"
    }
}
```

**Example: Interface:**
```java
interface Animal {
    void sound();
    void sleep();
}

class Cow implements Animal {
    @Override
    public void sound() {
        System.out.println("Cow moos");
    }

    @Override
    public void sleep() {
        System.out.println("Cow is sleeping");
    }
}

public class Main {
    public static void main(String[] args) {
        Cow myCow = new Cow();
        myCow.sound();  // Outputs "Cow moos"
        myCow.sleep();  // Outputs "Cow is sleeping"
    }
}
```