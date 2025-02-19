# TypeScript Setup

## Setting up a TypeScript Project
To start a TypeScript project, follow these steps:

1. **Install Node.js and npm**
   - Download and install [Node.js](https://nodejs.org/)
   - Verify the installation:
     ```sh
     node -v
     npm -v
     ```

2. **Initialize a New Project**
   - Create a project folder and navigate into it:
     ```sh
     mkdir typescript-project
     cd typescript-project
     ```
   - Initialize a package.json file:
     ```sh
     npm init -y
     ```

3. **Install TypeScript**
   - Run the following command to install TypeScript as a development dependency:
     ```sh
     npm install --save-dev typescript
     ```
   - Verify the installation:
     ```sh
     npx tsc --version
     ```

## Configuring `tsconfig.json`
The `tsconfig.json` file contains the configuration for the TypeScript compiler.

1. **Generate a default `tsconfig.json`**
   ```sh
   npx tsc --init
   ```

2. **Key Configuration Options**
   - `"target"`: Specifies the ECMAScript version output. Example:
     ```json
     "target": "ES6"
     ```
   - `"module"`: Specifies the module system. Example:
     ```json
     "module": "CommonJS"
     ```
   - `"strict"`: Enables strict type-checking options.
   - `"outDir"`: Specifies the output directory for compiled JavaScript files.
   - `"rootDir"`: Specifies the root directory of TypeScript files.

3. **Example `tsconfig.json`**
   ```json
   {
     "compilerOptions": {
       "target": "ES6",
       "module": "CommonJS",
       "strict": true,
       "outDir": "./JavaScript",       //out directory
       "rootDir": "./TypeScript"        
     }
   }
   ```

## Compiling TypeScript
Once TypeScript is installed and configured, you can compile `.ts` files to `.js`.

1. **Create a sample TypeScript file**
   ```sh
   mkdir TypeScript                //create folder 
   touch TypeScript/index.ts       //create file
   ```
   
   Add the following code in `TypeScript/index.ts`:
   ```ts
   const greet = (name: string): string => {
       return `Hello, ${name}!`;
   };
   console.log(greet("TypeScript"));
   ```

2. **Compile TypeScript files**
   ```sh
     tsc index.ts
   ```
   This will generate JavaScript files in the `JavaScript/` directory.

3. **Run the Compiled JavaScript**
   ```sh
   node TypeScript/index.js
   ```

---

**Arrays**, **Tuples**, and **Enums** in TypeScript with simple explanations and examples:

### 1. **Arrays**

In TypeScript, arrays are collections of values of a specific type. You can define an array using the `[]` notation or with the `Array<type>` notation.

#### Example:
```typescript
// Array of strings
let fruits: string[] = ["Apple", "Banana", "Cherry"];

// Array of numbers
let numbers: Array<number> = [1, 2, 3, 4, 5];

// Accessing array elements
console.log(fruits[0]);  // Output: Apple
console.log(numbers[2]); // Output: 3
```

### 2. **Tuples**

Tuples are similar to arrays, but the key difference is that each element in a tuple can have a different type. You specify the types of the elements in the tuple when you declare it.

#### Example:
```typescript
// Tuple with a string, number, and boolean
let person: [string, number, boolean] = ["Vikram", 25, true];

// Accessing tuple elements
console.log(person[0]); // Output: Vikram
console.log(person[1]); // Output: 25
console.log(person[2]); // Output: true
```

### 3. **Enums**

Enums are a way to define named constants. They help make your code more readable by giving a meaningful name to a value instead of using magic numbers or strings.

You can define an enum to represent a set of related values, such as days of the week, states, etc.

#### Example:
```typescript
// Enum for days of the week
enum Days {
  Sunday,
  Monday,
  Tuesday,
  Wednesday,
  Thursday,
  Friday,
  Saturday
}

// Using enum values
let today: Days = Days.Monday;
console.log(today); // Output: 1 (because Monday is the second value, starting from 0)

// You can also assign custom values to enums
enum Status {
  Pending = 1,
  Approved = 2,
  Rejected = 3
}

let applicationStatus: Status = Status.Approved;
console.log(applicationStatus); // Output: 2
```

### Recap:
- **Arrays** store elements of the same type.
- **Tuples** store elements of different types in a specific order.
- **Enums** help group related constants and improve code readability.

**any**, **unknown**, **void**, **null**, **undefined**, and **never** types in TypeScript with examples.

### 1. **any**
The `any` type allows a variable to hold any type of value. This essentially disables TypeScript's type checking for that variable. It's useful when you don't know the type in advance or when you're dealing with dynamic content, but should be used sparingly.

#### Example:
```typescript
let value: any = 42;  // Can hold any type of value
value = "Hello, TypeScript!";  // Now it's a string
value = true;  // Now it's a boolean

// You can also call methods on it without type errors
value.toUpperCase();  // Works fine, even though it's not strictly a string
```

### 2. **unknown**
The `unknown` type is similar to `any`, but it is safer. You cannot perform any operations on an `unknown` type until it is explicitly narrowed to a more specific type.

#### Example:
```typescript
let value: unknown = 42;
value = "Hello, TypeScript!";

// You cannot do this directly with unknown:
console.log(value.toUpperCase());  // Error: Object is of type 'unknown'.

// You need to narrow the type first:
if (typeof value === "string") {
  console.log(value.toUpperCase());  // Works fine because we know it's a string
}
```

### 3. **void**
The `void` type is used to represent the absence of a value. It’s commonly used for functions that do not return anything (e.g., `console.log()`).

#### Example:
```typescript
function logMessage(message: string): void {
  console.log(message);
}

let result: void = logMessage("This is a message"); // The function doesn't return anything
```

### 4. **null**
The `null` type represents a variable that has no value or is intentionally left empty. It can be assigned only to variables of type `null` or `any`.

#### Example:
```typescript
let emptyValue: null = null;

// TypeScript does not allow assigning null to a string type (unless strict null checks are off)
let name: string = null;  // Error in strict mode
```

### 5. **undefined**
The `undefined` type is used when a variable has been declared but not yet assigned a value. In JavaScript, `undefined` is the default value for uninitialized variables.

#### Example:
```typescript
let value: undefined = undefined;

// Also, variables that are declared but not assigned have the type 'undefined'
let uninitialized: number;
console.log(uninitialized);  // undefined (default value)
```

### 6. **never**
The `never` type represents a value that will never occur. This is used for functions that throw an error or have infinite loops (they never return).

#### Example:
```typescript
// Function that throws an error and doesn't return
function throwError(message: string): never {
  throw new Error(message);
}

// Function that has an infinite loop
function infiniteLoop(): never {
  while (true) {}
}
```

### Summary:
- **any**: A variable can hold any type, no type checking.
- **unknown**: A variable can hold any type, but you must narrow the type before using it.
- **void**: Represents a function that doesn't return a value.
- **null**: Represents an intentionally empty or absent value.
- **undefined**: Represents a variable that is declared but not assigned.
- **never**: Represents a value that will never occur (used for functions that don’t return).


## Interface
In TypeScript, an **interface** defines the shape of an object, such as the properties it should have and the types of those properties. The interface itself doesn't provide any implementation but serves as a blueprint for creating objects.

### 1. **Creating an Interface**
An interface defines the structure of an object by specifying the types of its properties. Here's a basic example:

```typescript
// Define an interface
interface Person {
  name: string;
  age: number;
  isActive: boolean;
}

// Using the interface to create an object
let person: Person = {
  name: "Vikram",
  age: 25,
  isActive: true
};

console.log(person);  // Output: { name: 'Vikram', age: 25, isActive: true }
```

### 2. **Interface with Optional Properties**
You can also define optional properties in an interface by using the `?` symbol. These properties may or may not exist in the object.

#### Example:
```typescript
interface Product {
  id: number;
  name: string;
  price?: number;  // Optional property
}

let product1: Product = { id: 1, name: "Laptop" };  // No price
let product2: Product = { id: 2, name: "Phone", price: 500 };  // Price included

console.log(product1);  // Output: { id: 1, name: 'Laptop' }
console.log(product2);  // Output: { id: 2, name: 'Phone', price: 500 }
```

### 3. **Interface with Method Signatures**
You can also include method signatures in an interface. This allows objects to implement functions defined by the interface.

#### Example:
```typescript
interface Employee {
  name: string;
  role: string;
  getDetails: () => string;  // Method signature
}

// Implement the interface with an object
let employee: Employee = {
  name: "Vikram",
  role: "Developer",
  getDetails: function() {
    return `${this.name} is a ${this.role}.`;
  }
};

console.log(employee.getDetails());  // Output: Vikram is a Developer.
```

### 4. **Interface with Index Signatures**
An **index signature** allows you to define the shape of objects when you don’t know all the property names ahead of time, but you know the types of their values.

#### Example:
```typescript
interface Dictionary {
  [key: string]: string;
}

let phonebook: Dictionary = {
  "John": "12345",
  "Jane": "67890"
};

console.log(phonebook["John"]);  // Output: 12345
```

### 5. **Implementing an Interface in a Class**
Classes can implement interfaces, which ensures the class follows the structure defined in the interface.

#### Example:
```typescript
interface Animal {
  name: string;
  sound: string;
  makeSound(): void;
}

class Dog implements Animal {
  name: string;
  sound: string;

  constructor(name: string, sound: string) {
    this.name = name;
    this.sound = sound;
  }

  makeSound(): void {
    console.log(`${this.name} says: ${this.sound}`);
  }
}

let myDog = new Dog("Buddy", "Woof");
myDog.makeSound();  // Output: Buddy says: Woof
```

### Summary:
- **Interface** defines the structure of an object.
- You can define required properties, optional properties (`?`), and methods.
- Interfaces can be implemented by classes to enforce structure.
- **Index signatures** allow you to define objects with dynamic keys but fixed value types.


**Extending Interfaces**, **Type Aliases**, and **Intersection Types** in TypeScript with simple examples:

### 1. **Extending Interfaces**

When you extend an interface, you can create a new interface that includes all the properties of an existing interface, with the option to add more properties.

#### Example:
```typescript
// Base interface
interface Animal {
  name: string;
  sound: string;
}

// Extended interface
interface Dog extends Animal {
  breed: string;
}

let myDog: Dog = {
  name: "Buddy",
  sound: "Woof",
  breed: "Labrador"
};

console.log(myDog);  // Output: { name: 'Buddy', sound: 'Woof', breed: 'Labrador' }
```

- The `Dog` interface extends `Animal`, so it includes `name` and `sound` from `Animal` and adds a `breed` property.
- You can extend multiple interfaces as well.

#### Example of extending multiple interfaces:
```typescript
interface Canine {
  isDomestic: boolean;
}

interface Dog extends Animal, Canine {
  breed: string;
}

let dog: Dog = {
  name: "Max",
  sound: "Bark",
  breed: "Bulldog",
  isDomestic: true
};

console.log(dog);  // Output: { name: 'Max', sound: 'Bark', breed: 'Bulldog', isDomestic: true }
```

### 2. **Type Aliases**

Type aliases allow you to create a new name for a type. They can be used for primitive types, object types, arrays, or even more complex types like function signatures.

#### Example:
```typescript
// Type alias for a simple type
type ID = string;

let userId: ID = "12345";

// Type alias for an object
type Point = {
  x: number;
  y: number;
};

let point: Point = { x: 10, y: 20 };
console.log(point);  // Output: { x: 10, y: 20 }
```

- You can use type aliases for **objects**, **functions**, and **primitives**.

#### Example of a function type alias:
```typescript
type Greet = (name: string) => string;

const greetUser: Greet = (name) => `Hello, ${name}`;

console.log(greetUser("Vikram"));  // Output: Hello, Vikram
```

### 3. **Intersection Types**

Intersection types combine multiple types into one. This means the resulting type has all the properties from each of the combined types. It's useful when you want an object to have properties of multiple types.

#### Example:
```typescript
// Defining two types
type Person = {
  name: string;
  age: number;
};

type Contact = {
  email: string;
  phone: string;
};

// Intersection type combining both types
type Employee = Person & Contact;

let employee: Employee = {
  name: "Vikram",
  age: 25,
  email: "vikram@example.com",
  phone: "123-456-7890"
};

console.log(employee);  // Output: { name: 'Vikram', age: 25, email: 'vikram@example.com', phone: '123-456-7890' }
```

- The `Employee` type has properties from both `Person` and `Contact`. This is an intersection of the two types using the `&` operator.

#### Example with interfaces:
You can also use interfaces with intersection types.

```typescript
interface Product {
  id: number;
  name: string;
}

interface Price {
  price: number;
}

type ProductWithPrice = Product & Price;

let product: ProductWithPrice = {
  id: 1,
  name: "Laptop",
  price: 999
};

console.log(product);  // Output: { id: 1, name: 'Laptop', price: 999 }
```

### Summary:
- **Extending interfaces**: You can create a new interface by inheriting properties from one or more existing interfaces.
- **Type aliases**: Create a new name for a type (can be used for primitives, objects, arrays, or function types).
- **Intersection types**: Combine multiple types into one, meaning the resulting type must have all the properties of the combined types.

### **Classes and Objects in TypeScript**

In TypeScript, **classes** provide a way to create reusable blueprints for objects. A class defines properties (variables) and methods (functions) that an object can have.

---

## **1. Creating a Basic Class**
A class is defined using the `class` keyword, and you can create an object from it using the `new` keyword.

### **Example:**
```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

// Creating an object of the Person class
let person1 = new Person("Vikram", 25);
person1.greet();  
// Output: Hello, my name is Vikram and I am 25 years old.
```

---

## **2. Access Modifiers (public, private, protected)**
TypeScript provides three access modifiers:
- **public**: Can be accessed anywhere (default).
- **private**: Can be accessed only within the class.
- **protected**: Can be accessed within the class and its subclasses.

### **Example of private modifier:**
```typescript
class Employee {
  public name: string;
  private salary: number;

  constructor(name: string, salary: number) {
    this.name = name;
    this.salary = salary;
  }

  getSalary() {
    return `Salary of ${this.name} is ${this.salary}`;
  }
}

let emp = new Employee("Vikram", 50000);
console.log(emp.name);  // Works: Vikram
// console.log(emp.salary); // Error: Property 'salary' is private
console.log(emp.getSalary());  // Works: Salary of Vikram is 50000
```

---

## **3. Readonly Properties**
The `readonly` modifier makes a property immutable after it has been initialized.

### **Example:**
```typescript
class Car {
  readonly brand: string;

  constructor(brand: string) {
    this.brand = brand;
  }
}

let myCar = new Car("Toyota");
console.log(myCar.brand);  // Output: Toyota
// myCar.brand = "Honda";  // Error: Cannot assign to 'brand' because it is a read-only property.
```

---

## **4. Getters and Setters**
Getters (`get`) and setters (`set`) allow controlled access to properties.

### **Example:**
```typescript
class BankAccount {
  private balance: number = 0;

  get getBalance(): number {
    return this.balance;
  }

  set setBalance(amount: number) {
    if (amount < 0) {
      console.log("Invalid amount");
    } else {
      this.balance = amount;
    }
  }
}

let account = new BankAccount();
account.setBalance = 1000;  // Using setter
console.log(account.getBalance);  // Using getter, Output: 1000
```

---

## **5. Static Properties and Methods**
Static members belong to the class itself and not to any object.

### **Example:**
```typescript
class MathUtils {
  static PI: number = 3.14;

  static calculateArea(radius: number): number {
    return this.PI * radius * radius;
  }
}

console.log(MathUtils.PI);  // Output: 3.14
console.log(MathUtils.calculateArea(5));  // Output: 78.5
```

---

## **6. Inheritance (Extending Classes)**
Inheritance allows one class to inherit properties and methods from another class using `extends`.

### **Example:**
```typescript
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound() {
    console.log("Animal makes a sound");
  }
}

class Dog extends Animal {
  breed: string;

  constructor(name: string, breed: string) {
    super(name);  // Calling parent class constructor
    this.breed = breed;
  }

  makeSound() {
    console.log(`${this.name} barks!`);
  }
}

let myDog = new Dog("Buddy", "Labrador");
myDog.makeSound();  // Output: Buddy barks!
```

---

## **7. Abstract Classes**
An **abstract class** cannot be instantiated directly. It is meant to be inherited by other classes.

### **Example:**
```typescript
abstract class Shape {
  abstract getArea(): number;  // Abstract method (must be implemented in child class)
}

class Circle extends Shape {
  radius: number;

  constructor(radius: number) {
    super();
    this.radius = radius;
  }

  getArea(): number {
    return Math.PI * this.radius * this.radius;
  }
}

let circle = new Circle(5);
console.log(circle.getArea());  // Output: 78.53981633974483
```

---

## **Summary**
| Feature | Description |
|---------|-------------|
| **Class** | Defines a blueprint for objects. |
| **Object** | An instance of a class. |
| **Constructor** | Initializes an object when created. |
| **Access Modifiers** | `public`, `private`, `protected` control property access. |
| **Readonly** | Prevents modification after initialization. |
| **Getters & Setters** | Allow controlled access to properties. |
| **Static Members** | Belong to the class, not to instances. |
| **Inheritance** | One class inherits properties/methods from another. |
| **Abstract Class** | Cannot be instantiated, used as a base class. |


### **Constructor in TypeScript**
A **constructor** is a special method inside a class that is automatically called when an object of that class is created. It is used to initialize the object's properties.

---

## **1. Basic Constructor Example**
```typescript
class Person {
  name: string;
  age: number;

  // Constructor
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  display() {
    console.log(`Name: ${this.name}, Age: ${this.age}`);
  }
}

// Creating an object
let person1 = new Person("Vikram", 25);
person1.display();  
// Output: Name: Vikram, Age: 25
```

- The constructor is executed automatically when `new Person("Vikram", 25)` is called.
- It initializes the `name` and `age` properties.

---

## **2. Constructor with Default Values**
You can provide **default values** to parameters inside the constructor.

```typescript
class Car {
  brand: string;
  model: string;

  constructor(brand: string = "Toyota", model: string = "Corolla") {
    this.brand = brand;
    this.model = model;
  }

  showCar() {
    console.log(`Car: ${this.brand} ${this.model}`);
  }
}

// Object with default values
let car1 = new Car();
car1.showCar();  // Output: Car: Toyota Corolla

// Object with custom values
let car2 = new Car("Honda", "Civic");
car2.showCar();  // Output: Car: Honda Civic
```

- If no arguments are passed, the constructor uses the default values.

---

## **3. Using Access Modifiers in Constructor**
TypeScript allows **shorter syntax** for defining properties directly in the constructor using access modifiers (`public`, `private`, `readonly`, `protected`).

### **Example:**
```typescript
class Employee {
  constructor(public name: string, private salary: number) {}

  showDetails() {
    console.log(`Employee: ${this.name}`);
    // console.log(`Salary: ${this.salary}`); // Accessible inside the class
  }
}

let emp = new Employee("Vikram", 50000);
console.log(emp.name);  // Output: Vikram
// console.log(emp.salary); // Error: 'salary' is private
```

- `public name: string` automatically creates and initializes `name`.
- `private salary: number` makes `salary` accessible only inside the class.

---

## **4. Constructor Overloading**
TypeScript does not support true constructor overloading like Java, but we can **simulate** it using optional parameters.

```typescript
class Product {
  name: string;
  price: number;

  constructor(name: string, price?: number) {
    this.name = name;
    this.price = price ?? 0; // If price is undefined, set to 0
  }

  display() {
    console.log(`Product: ${this.name}, Price: $${this.price}`);
  }
}

let p1 = new Product("Laptop", 1000);
let p2 = new Product("Mouse");

p1.display();  // Output: Product: Laptop, Price: $1000
p2.display();  // Output: Product: Mouse, Price: $0
```

- `price?: number` makes `price` optional.
- `this.price = price ?? 0` ensures `price` defaults to `0` if not provided.

---

## **5. Constructor in Inheritance (super keyword)**
When a class **inherits** another class, the child class constructor must call the parent class constructor using `super()`.

```typescript
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  breed: string;

  constructor(name: string, breed: string) {
    super(name); // Calls the parent class constructor
    this.breed = breed;
  }

  showDetails() {
    console.log(`Dog: ${this.name}, Breed: ${this.breed}`);
  }
}

let dog1 = new Dog("Buddy", "Labrador");
dog1.showDetails();  
// Output: Dog: Buddy, Breed: Labrador
```

- `super(name)` calls the `Animal` constructor to initialize `name`.
- The `Dog` class adds an additional property `breed`.

---

## **6. Private Constructor (Singleton Pattern)**
A **private constructor** prevents the creation of multiple instances of a class. This is useful for implementing the **Singleton Pattern**.

```typescript
class Singleton {
  private static instance: Singleton;

  private constructor() {
    console.log("Singleton instance created");
  }

  static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }

  showMessage() {
    console.log("Hello from Singleton");
  }
}

let s1 = Singleton.getInstance();  // Singleton instance created
s1.showMessage();  // Hello from Singleton

let s2 = Singleton.getInstance();  
// No new instance created

console.log(s1 === s2);  // Output: true (Both refer to the same instance)
```

- The constructor is **private**, so no new objects can be created using `new Singleton()`.
- `getInstance()` ensures only **one** instance exists.

---

## **Summary**
| Concept | Description |
|---------|-------------|
| **Basic Constructor** | Initializes object properties when an object is created. |
| **Default Values** | Allows parameters to have default values. |
| **Access Modifiers** | `public`, `private`, `readonly` can be used directly in the constructor. |
| **Constructor Overloading** | Simulated using optional parameters. |
| **super() in Inheritance** | Calls the parent class constructor when extending a class. |
| **Private Constructor** | Prevents object creation, useful for Singleton Pattern. |


### **Abstract Classes and Methods in TypeScript**
In TypeScript, **abstract classes** act as blueprints for other classes. They cannot be instantiated directly and may include **abstract methods**, which must be implemented in derived (child) classes.

---

## **1. What is an Abstract Class?**
An **abstract class**:
- Can **have** methods with implementation.
- Can **have** abstract methods (without implementation).
- Cannot be instantiated directly.
- Must be **extended** by child classes.

### **Example: Basic Abstract Class**
```typescript
abstract class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  // Abstract method (no implementation)
  abstract makeSound(): void;

  // Concrete method (has implementation)
  move(): void {
    console.log(`${this.name} is moving.`);
  }
}

// Error: Cannot create an instance of an abstract class
// let animal = new Animal("Some Animal"); // ❌

class Dog extends Animal {
  constructor(name: string) {
    super(name);
  }

  // Implementing the abstract method
  makeSound(): void {
    console.log(`${this.name} barks!`);
  }
}

let myDog = new Dog("Buddy");
myDog.makeSound();  // Output: Buddy barks!
myDog.move();       // Output: Buddy is moving.
```

### **Key Points:**
✔️ `abstract` keyword is used before class and method names.  
✔️ `makeSound()` has **no body** in the `Animal` class but must be **implemented** in `Dog`.  
✔️ The `move()` method is a **normal method** (not abstract) and can be used directly.

---

## **2. Abstract Methods**
An **abstract method**:
- Has no implementation in the abstract class.
- **Must** be implemented by any child class.
- Enforces consistency across different child classes.

### **Example: Abstract Method in Different Classes**
```typescript
abstract class Vehicle {
  abstract start(): void; // Abstract method (no body)

  stop(): void {
    console.log("Vehicle stopped.");
  }
}

class Car extends Vehicle {
  start(): void {
    console.log("Car engine started.");
  }
}

class Bike extends Vehicle {
  start(): void {
    console.log("Bike engine started.");
  }
}

let car = new Car();
car.start();  // Output: Car engine started.
car.stop();   // Output: Vehicle stopped.

let bike = new Bike();
bike.start(); // Output: Bike engine started.
bike.stop();  // Output: Vehicle stopped.
```

### **Key Points:**
✔️ The `start()` method **must** be implemented in both `Car` and `Bike`.  
✔️ The `stop()` method **is inherited** and can be used directly.

---

## **3. Abstract Classes with Properties**
An abstract class can have both **properties** and **methods**.

```typescript
abstract class Shape {
  constructor(public color: string) {}

  abstract getArea(): number; // Abstract method

  showColor(): void {
    console.log(`Shape color: ${this.color}`);
  }
}

class Circle extends Shape {
  constructor(color: string, public radius: number) {
    super(color);
  }

  getArea(): number {
    return Math.PI * this.radius * this.radius;
  }
}

let circle = new Circle("Red", 5);
circle.showColor(); // Output: Shape color: Red
console.log(circle.getArea()); // Output: 78.53981633974483
```

### **Key Points:**
✔️ `Shape` has an abstract method `getArea()`.  
✔️ `showColor()` is a normal method and can be used directly.  
✔️ `Circle` extends `Shape` and must implement `getArea()`.  

---

## **4. Abstract Class with Multiple Abstract Methods**
If an abstract class has multiple abstract methods, all must be implemented in the subclass.

```typescript
abstract class Employee {
  constructor(public name: string, public id: number) {}

  abstract calculateSalary(): number;
  abstract getRole(): string;
}

class Developer extends Employee {
  constructor(name: string, id: number, private hourlyRate: number, private hoursWorked: number) {
    super(name, id);
  }

  calculateSalary(): number {
    return this.hourlyRate * this.hoursWorked;
  }

  getRole(): string {
    return "Software Developer";
  }
}

let dev = new Developer("Vikram", 101, 50, 160);
console.log(dev.getRole()); // Output: Software Developer
console.log(`Salary: $${dev.calculateSalary()}`); // Output: Salary: $8000
```

✔️ `calculateSalary()` and `getRole()` **must** be implemented in `Developer`.  
✔️ The `Developer` class calculates salary using custom logic.  

---

## **5. Abstract Class with Interface Implementation**
An abstract class can implement an **interface** and provide partial or full implementation.

```typescript
interface Logger {
  log(message: string): void;
}

abstract class Database implements Logger {
  abstract connect(): void;

  log(message: string): void {
    console.log(`Log: ${message}`);
  }
}

class MySQLDatabase extends Database {
  connect(): void {
    console.log("Connected to MySQL Database");
  }
}

let db = new MySQLDatabase();
db.connect();  // Output: Connected to MySQL Database
db.log("Connection successful.");  // Output: Log: Connection successful.
```

✔️ `Database` implements `Logger` and provides a `log()` method.  
✔️ `MySQLDatabase` **must** implement `connect()`.  

---

## **6. Difference Between Abstract Class and Interface**
| Feature | Abstract Class | Interface |
|---------|--------------|------------|
| Can have properties? | ✅ Yes | ❌ No (only declarations) |
| Can have method implementation? | ✅ Yes | ❌ No |
| Can have constructors? | ✅ Yes | ❌ No |
| Can extend multiple? | ❌ No | ✅ Yes (Multiple interfaces) |
| Used for | Code reuse and enforcing structure | Only enforcing structure |

Example:
```typescript
// Abstract class
abstract class A {
  abstract methodA(): void;
  methodB() {
    console.log("Method B");
  }
}

// Interface
interface B {
  methodC(): void;
}

// Class implementing both
class C extends A implements B {
  methodA(): void {
    console.log("Implemented methodA");
  }
  methodC(): void {
    console.log("Implemented methodC");
  }
}

let obj = new C();
obj.methodA(); // Output: Implemented methodA
obj.methodB(); // Output: Method B
obj.methodC(); // Output: Implemented methodC
```

✔️ `A` is an abstract class with one abstract and one normal method.  
✔️ `B` is an interface with only a method declaration.  
✔️ `C` extends `A` and implements `B`, providing required implementations.  

---

## **7. Summary**
| Concept | Description |
|---------|-------------|
| **Abstract Class** | Cannot be instantiated; acts as a blueprint. |
| **Abstract Method** | Declared without implementation; must be implemented in child classes. |
| **Concrete Methods** | Can be defined in abstract classes and used directly. |
| **Extending Abstract Class** | Child class must implement all abstract methods. |
| **Interfaces vs Abstract Classes** | Interfaces define only structure; abstract classes allow partial implementation. |

Try to explore **polymorphism** with abstract classes 😊


### **Inheritance and Its Types in TypeScript**
Inheritance is a core concept in **Object-Oriented Programming (OOP)** that allows a class to **acquire** properties and methods from another class. It helps in **code reusability** and **reducing redundancy**.

---

## **1. What is Inheritance?**
- A **child (derived) class** can **inherit** properties and methods from a **parent (base) class**.
- The `extends` keyword is used to achieve inheritance.
- The child class can **override** or **extend** the parent class's functionality.

### **Basic Example**
```typescript
// Parent class
class Person {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

// Child class inheriting from Person
class Student extends Person {
  studentId: number;

  constructor(name: string, studentId: number) {
    super(name); // Calling the parent constructor
    this.studentId = studentId;
  }

  study(): void {
    console.log(`${this.name} is studying.`);
  }
}

let student = new Student("Vikram", 101);
student.greet();  // Output: Hello, my name is Vikram.
student.study();   // Output: Vikram is studying.
```
✔️ `Student` inherits the `greet()` method from `Person`.  
✔️ The `super()` function calls the parent class constructor.  

---

# **2. Types of Inheritance in TypeScript**
TypeScript supports different types of inheritance:

1. **Single Inheritance** (One parent → One child)
2. **Multilevel Inheritance** (Grandparent → Parent → Child)
3. **Hierarchical Inheritance** (One parent → Multiple children)
4. **Multiple Inheritance** (Not directly supported, but achieved using interfaces)

---

## **1. Single Inheritance**
A **single child class** inherits from a **single parent class**.

```typescript
class Animal {
  makeSound(): void {
    console.log("Animal makes a sound.");
  }
}

class Dog extends Animal {
  bark(): void {
    console.log("Dog barks.");
  }
}

let myDog = new Dog();
myDog.makeSound(); // Output: Animal makes a sound.
myDog.bark();      // Output: Dog barks.
```
✔️ `Dog` class **inherits** `makeSound()` from `Animal`.  
✔️ `bark()` is specific to `Dog`.  

---

## **2. Multilevel Inheritance**
A child class can inherit from another child class, forming a **chain**.

```typescript
class Grandfather {
  constructor(public surname: string) {}

  showSurname(): void {
    console.log(`Family surname: ${this.surname}`);
  }
}

class Father extends Grandfather {
  constructor(surname: string, public profession: string) {
    super(surname);
  }

  showProfession(): void {
    console.log(`Father is a ${this.profession}`);
  }
}

class Child extends Father {
  constructor(surname: string, profession: string, public hobby: string) {
    super(surname, profession);
  }

  showHobby(): void {
    console.log(`Child's hobby is ${this.hobby}`);
  }
}

let child = new Child("Vishwakarma", "Engineer", "Painting");
child.showSurname();   // Output: Family surname: Vishwakarma
child.showProfession();// Output: Father is an Engineer
child.showHobby();     // Output: Child's hobby is Painting
```
✔️ `Child` inherits properties and methods from both `Father` and `Grandfather`.  

---

## **3. Hierarchical Inheritance**
Multiple child classes inherit from a single parent.

```typescript
class Vehicle {
  move(): void {
    console.log("Vehicle is moving.");
  }
}

class Car extends Vehicle {
  speed(): void {
    console.log("Car moves at 100 km/h.");
  }
}

class Bike extends Vehicle {
  balance(): void {
    console.log("Bike requires balance.");
  }
}

let car = new Car();
car.move();   // Output: Vehicle is moving.
car.speed();  // Output: Car moves at 100 km/h.

let bike = new Bike();
bike.move();   // Output: Vehicle is moving.
bike.balance();// Output: Bike requires balance.
```
✔️ Both `Car` and `Bike` **inherit** `move()` from `Vehicle`.  
✔️ Each child class has its **own** additional method (`speed()`, `balance()`).  

---

## **4. Multiple Inheritance (Using Interfaces)**
TypeScript **does not support** multiple inheritance directly but allows **multiple interface implementation**.

```typescript
interface Flyable {
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

// Class implementing multiple interfaces
class Duck implements Flyable, Swimmable {
  fly(): void {
    console.log("Duck can fly.");
  }

  swim(): void {
    console.log("Duck can swim.");
  }
}

let duck = new Duck();
duck.fly();  // Output: Duck can fly.
duck.swim(); // Output: Duck can swim.
```
✔️ `Duck` implements both `Flyable` and `Swimmable` interfaces.  
✔️ This is how TypeScript **achieves multiple inheritance**.  

---

# **3. Method Overriding in Inheritance**
A child class can **override** a parent method to provide its own implementation.

```typescript
class Employee {
  work(): void {
    console.log("Employee is working.");
  }
}

class Manager extends Employee {
  work(): void {
    console.log("Manager is handling the team.");
  }
}

let emp1 = new Employee();
emp1.work(); // Output: Employee is working.

let emp2 = new Manager();
emp2.work(); // Output: Manager is handling the team.
```
✔️ `Manager` overrides the `work()` method from `Employee`.  
✔️ When calling `work()` on `Manager`, it executes the overridden method.  

---

# **4. Access Modifiers in Inheritance**
| Modifier | Description | Accessible in Parent? | Accessible in Child? | Accessible Outside? |
|----------|------------|---------------------|-------------------|----------------|
| `public` | Accessible anywhere | ✅ Yes | ✅ Yes | ✅ Yes |
| `protected` | Accessible in parent & child | ✅ Yes | ✅ Yes | ❌ No |
| `private` | Accessible only in parent | ✅ Yes | ❌ No | ❌ No |

### **Example: Using Access Modifiers**
```typescript
class BankAccount {
  public accountHolder: string;
  protected balance: number;
  private pin: number;

  constructor(accountHolder: string, balance: number, pin: number) {
    this.accountHolder = accountHolder;
    this.balance = balance;
    this.pin = pin;
  }

  showBalance(): void {
    console.log(`Balance: $${this.balance}`);
  }
}

class SavingsAccount extends BankAccount {
  constructor(accountHolder: string, balance: number, pin: number) {
    super(accountHolder, balance, pin);
  }

  withdraw(amount: number): void {
    if (amount <= this.balance) {
      this.balance -= amount;
      console.log(`Withdrawal successful. New balance: $${this.balance}`);
    } else {
      console.log("Insufficient balance.");
    }
  }
}

let account = new SavingsAccount("Vikram", 5000, 1234);
console.log(account.accountHolder); // ✅ Accessible (public)
account.showBalance();  // ✅ Accessible (public)
// account.balance;  // ❌ Error (protected)
// account.pin;      // ❌ Error (private)
account.withdraw(1000); // ✅ Withdrawal successful.
```
✔️ `accountHolder` is **public**, accessible anywhere.  
✔️ `balance` is **protected**, accessible in the child class (`withdraw`).  
✔️ `pin` is **private**, **not accessible** outside the parent class.  

---

# **5. Summary**
| Inheritance Type | Description |
|------------------|-------------|
| **Single** | One class inherits from another. |
| **Multilevel** | A chain of inheritance (Grandparent → Parent → Child). |
| **Hierarchical** | One parent has multiple child classes. |
| **Multiple** | Not supported directly, but achieved with interfaces. |

Try to explore **Polymorphism and Method Overloading** 🚀

## **Method Overloading and Method Overriding in TypeScript**
Both **Method Overloading** and **Method Overriding** are important concepts in **Object-Oriented Programming (OOP)** that help in code reusability and flexibility.

---

# **1. Method Overloading**
### **Definition:**
Method overloading allows a **single function** to have **multiple method signatures** with different **parameters**.

### **Key Points:**
✔️ Overloading allows **same method name** but with different **parameter types or count**.  
✔️ TypeScript does **not** support **true** method overloading like Java/C++, but we can **simulate it** using **function signatures**.  
✔️ Only **one** implementation of the method is allowed.

---

### **Example 1: Function Overloading**
```typescript
class MathOperations {
  // Function signatures (overloads)
  add(a: number, b: number): number;
  add(a: string, b: string): string;
  add(a: number, b: number, c: number): number;

  // Single implementation handling all overloads
  add(a: any, b: any, c?: any): any {
    if (typeof a === "string" && typeof b === "string") {
      return a + b; // Concatenation for strings
    }
    return c !== undefined ? a + b + c : a + b; // Addition for numbers
  }
}

let math = new MathOperations();

console.log(math.add(5, 10));         // Output: 15
console.log(math.add("Hello, ", "Vikram")); // Output: Hello, Vikram
console.log(math.add(2, 3, 4));       // Output: 9
```
✔️ Multiple function signatures exist, but only **one** implementation (`add()`).  
✔️ It handles **both numbers and strings** differently.  

---

### **Example 2: Overloading in a Class**
```typescript
class Printer {
  print(message: string): void;
  print(message: number): void;

  print(message: any): void {
    console.log(`Printing: ${message}`);
  }
}

let printer = new Printer();
printer.print("Hello, TypeScript!"); // Output: Printing: Hello, TypeScript!
printer.print(1234);                 // Output: Printing: 1234
```
✔️ `print()` method is overloaded to accept both `string` and `number`.  
✔️ The implementation is **flexible** based on the argument type.  

---

# **2. Method Overriding**
### **Definition:**
Method overriding allows a **child class** to **redefine** a method of the **parent class**.

### **Key Points:**
✔️ Overriding occurs in **inheritance** when the child class **modifies** the parent’s method.  
✔️ The method **name, parameters, and return type** should be **the same**.  
✔️ The `super` keyword is used to call the **parent’s method** inside the child class.  

---

### **Example 1: Overriding a Method**
```typescript
class Animal {
  makeSound(): void {
    console.log("Animal makes a sound.");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Dog barks."); // Overriding the parent method
  }
}

let myDog = new Dog();
myDog.makeSound(); // Output: Dog barks.
```
✔️ The `Dog` class **overrides** `makeSound()` of `Animal`.  
✔️ Instead of "Animal makes a sound", it prints "Dog barks".  

---

### **Example 2: Overriding + Using `super`**
```typescript
class Employee {
  work(): void {
    console.log("Employee is working.");
  }
}

class Manager extends Employee {
  work(): void {
    super.work(); // Calls the parent class's method
    console.log("Manager is managing the team.");
  }
}

let emp = new Manager();
emp.work(); 
// Output:
// Employee is working.
// Manager is managing the team.
```
✔️ `super.work()` calls the **parent’s** method before executing the **child’s method**.  
✔️ This maintains **both behaviors** (parent + child).  

---

# **3. Key Differences Between Overloading & Overriding**
| Feature            | **Method Overloading** | **Method Overriding** |
|--------------------|----------------------|----------------------|
| **Definition**     | Same method name but different parameters in the same class | Same method name and parameters in **parent-child relationship** |
| **Where it Occurs?** | **Same class** | **Different classes (Inheritance required)** |
| **Return Type**    | Can be different | Must be the same |
| **Parameters**     | Must be different | Must be the same |
| **Implementation** | **One** function implementation handles all cases | Separate implementations in parent and child |
| **Keyword Used**   | Not required | `super` (to call parent method) |

---

# **4. Summary**
✔️ **Overloading** is used when **methods have the same name but different parameters**.  
✔️ **Overriding** is used when **a child class modifies a method from the parent class**.  
✔️ **Overriding works with inheritance**, whereas **overloading does not require inheritance**.  

---

# **5. Real-World Analogy**
| Concept  | Example |
|----------|---------|
| **Method Overloading** | **Bank ATM machine**: You can **withdraw money** using **card**, **UPI**, or **mobile banking** (same function, different inputs). |
| **Method Overriding** | **Car Horns**: All cars **have horns**, but **each model has a different sound** (same method, different implementation). |

# **Generics in TypeScript**
### 🚀 **Introduction**
**Generics** in TypeScript allow us to **write flexible and reusable code** by working with **multiple data types** while maintaining **type safety**.

### 🔹 **Why Use Generics?**
✔️ Avoids **code duplication**  
✔️ Provides **type safety**  
✔️ Works with **any data type**  
✔️ Used in **functions, interfaces, and classes**  

---

# **1. Generic Functions**
A **generic function** works with **different data types** while keeping **type safety**.

### **Example 1: Basic Generic Function**
```typescript
function identity<T>(value: T): T {
  return value;
}

// Using the generic function with different data types
console.log(identity<number>(10));      // Output: 10
console.log(identity<string>("Hello")); // Output: Hello
console.log(identity<boolean>(true));   // Output: true
```
✔️ `<T>` represents a **generic type**  
✔️ The function **returns** the same type as input  
✔️ We **explicitly** define `<number>`, `<string>`, etc.  

---

### **Example 2: Generic Function with Arrays**
```typescript
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}

console.log(getFirstElement<number>([1, 2, 3])); // Output: 1
console.log(getFirstElement<string>(["A", "B", "C"])); // Output: "A"
```
✔️ Works with **any array type**  
✔️ **Returns** the first element with the correct type  

---

### **Example 3: Generic Function with Multiple Types**
```typescript
function combine<T, U>(a: T, b: U): string {
  return `First: ${a}, Second: ${b}`;
}

console.log(combine<number, string>(10, "TypeScript")); 
// Output: First: 10, Second: TypeScript
```
✔️ Uses **two generic types** `<T, U>`  
✔️ **Accepts different types** for `a` and `b`  

---

# **2. Generic Interfaces**
A **generic interface** allows us to define a structure that works with **different types**.

### **Example 1: Generic Interface with Objects**
```typescript
interface Box<T> {
  value: T;
}

// Using the interface with different types
let numberBox: Box<number> = { value: 100 };
let stringBox: Box<string> = { value: "Hello" };

console.log(numberBox.value); // Output: 100
console.log(stringBox.value); // Output: Hello
```
✔️ `<T>` makes the interface **flexible**  
✔️ `Box<number>` and `Box<string>` are **different instances**  

---

### **Example 2: Generic Interface for Functions**
```typescript
interface MathOperation<T> {
  (a: T, b: T): T;
}

// Function using the generic interface
const add: MathOperation<number> = (x, y) => x + y;
const concatenate: MathOperation<string> = (x, y) => x + y;

console.log(add(10, 5)); // Output: 15
console.log(concatenate("Hello, ", "Vikram!")); // Output: Hello, Vikram!
```
✔️ The function must **match** the interface structure  
✔️ Works for **both numbers and strings**  

---

# **3. Generic Classes**
A **generic class** allows defining a **class template** that works with **different data types**.

### **Example 1: Basic Generic Class**
```typescript
class Storage<T> {
  private data: T[] = [];

  add(item: T): void {
    this.data.push(item);
  }

  getAll(): T[] {
    return this.data;
  }
}

// Creating instances with different types
let numberStorage = new Storage<number>();
numberStorage.add(10);
numberStorage.add(20);
console.log(numberStorage.getAll()); // Output: [10, 20]

let stringStorage = new Storage<string>();
stringStorage.add("Hello");
stringStorage.add("TypeScript");
console.log(stringStorage.getAll()); // Output: ["Hello", "TypeScript"]
```
✔️ `Storage<T>` can **store any type** (`number`, `string`, etc.)  
✔️ The class maintains **type safety**  

---

### **Example 2: Generic Class with Constraints**
We can **restrict** generic types using `extends`.

```typescript
class Car {
  constructor(public brand: string) {}
}

class Garage<T extends Car> {
  private cars: T[] = [];

  addCar(car: T): void {
    this.cars.push(car);
  }

  getCars(): T[] {
    return this.cars;
  }
}

let myGarage = new Garage<Car>();
myGarage.addCar(new Car("Toyota"));
myGarage.addCar(new Car("Honda"));

console.log(myGarage.getCars()); 
// Output: [Car { brand: "Toyota" }, Car { brand: "Honda" }]
```
✔️ `T extends Car` ensures **only Car objects** can be added  
✔️ **Prevents invalid types** from being used  

---

# **4. Generics with Type Aliases**
```typescript
type KeyValuePair<K, V> = {
  key: K;
  value: V;
};

let user: KeyValuePair<number, string> = { key: 1, value: "Vikram" };
console.log(user); // Output: { key: 1, value: "Vikram" }
```
✔️ Works **similarly to interfaces**  
✔️ Allows **different types** for `key` and `value`  

---

# **5. Summary**
| Feature  | Generic Functions | Generic Interfaces | Generic Classes |
|----------|-----------------|------------------|----------------|
| **Use Case** | Reusable functions for multiple types | Define structures with flexible types | Create flexible class templates |
| **Syntax** | `<T>` in function signature | `<T>` in interface | `<T>` in class declaration |
| **Example** | `function identity<T>(value: T): T {}` | `interface Box<T> { value: T; }` | `class Storage<T> { private data: T[] = []; }` |
| **Flexibility** | ✅ High | ✅ Medium | ✅ Medium |

---

# **6. Real-World Analogy**
| Concept | Example |
|---------|---------|
| **Generic Function** | **A universal charger** that works with any phone (type) |
| **Generic Interface** | **A template resume** that can be used by different people (types) |
| **Generic Class** | **A storage box** that can hold different types of objects |

---

## 🚀 **What's Next?**
Explore **Generic Constraints, Utility Types, or Advanced TypeScript Concepts** 😊

