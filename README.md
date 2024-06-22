### 1. Introduction to TypeScript

#### What is TypeScript?
TypeScript is a superset of JavaScript that adds static types. It enables catching errors early through a type system and makes development more efficient by providing powerful tooling.

#### Why Use TypeScript?
- **Type Safety**: Catch type-related errors during development.
- **Enhanced IDE Support**: Better code completion and refactoring.
- **Object-Oriented Programming**: Supports features like classes and interfaces.
- **Interoperability**: Seamlessly integrates with existing JavaScript code.

#### Setting Up TypeScript
To set up TypeScript, follow these steps:
1. **Install Node.js and npm**: Download and install from the [official Node.js website](https://nodejs.org/).
2. **Install TypeScript**: Open your terminal and run:
   ```bash
   npm install -g typescript
   ```
3. **Initialize a TypeScript Project**: Create a new directory for your project and run:
   ```bash
   tsc --init
   ```
4. **Write TypeScript Code**: Create a `.ts` file and start coding:
   ```typescript
   const greeting: string = 'Hello, TypeScript!';
   console.log(greeting);
   ```
5. **Compile TypeScript Code**: Run the TypeScript compiler:
   ```bash
   tsc
   ```
   This will compile your `.ts` files into `.js` files.

Node.js and npm are essential tools for modern JavaScript development, particularly for server-side and full-stack development.

#### Node.js

**Node.js** is an open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside of a web browser. It allows developers to use JavaScript to write server-side scripts, enabling dynamic web page content before the page is sent to the user's web browser. This makes it possible to use JavaScript for both client-side and server-side code.

#### npm

**npm** (Node Package Manager) is the default package manager for Node.js. It is a critical tool for managing JavaScript packages and dependencies.

### 2. Basic Types

#### Number
TypeScript supports all numeric values as `number`.
```typescript
let age: number = 25;
```

#### String
String values are represented with the `string` type.
```typescript
let name: string = 'John Doe';
```

#### Boolean
Boolean values are represented with the `boolean` type.
```typescript
let isStudent: boolean = true;
```

#### Array
Arrays can be defined in two ways: using the type followed by `[]` or using the generic `Array<type>`.
```typescript
let numbers: number[] = [1, 2, 3];
let fruits: Array<string> = ['Apple', 'Banana', 'Cherry'];
```

#### Tuple
Tuples allow you to express an array with a fixed number of elements whose types are known.
```typescript
let person: [string, number] = ['Alice', 30];
```

#### Enum
Enums allow you to define a set of named constants.
```typescript
enum Color {
  Red,
  Green,
  Blue
}
let c: Color = Color.Green;
```

#### Any
The `any` type allows you to opt-out of type checking.
```typescript
let randomValue: any = 10;
randomValue = 'Hello';
randomValue = true;
```

#### Void
The `void` type is used for functions that do not return a value. It can implicitly return undefined.
```typescript
function logMessage(message: string): void {
  console.log(message);
}
```

#### Null and Undefined
In TypeScript, `null` and `undefined` are distinct types that represent the absence of a value. They are part of the basic type system and have specific uses and behaviors.

**TypeScript Configuration**

By default, TypeScript treats `null` and `undefined` in a special way. However, you can configure TypeScript to enforce stricter rules with the `--strictNullChecks` compiler option.

**Without `--strictNullChecks`**

When `--strictNullChecks` is not enabled, `null` and `undefined` are considered valid values for every type. This means you can assign `null` and `undefined` to any variable.

```typescript
let value: number;
value = null;        // OK
value = undefined;   // OK
```

**With `--strictNullChecks`**

When `--strictNullChecks` is enabled, `null` and `undefined` are only assignable to their respective types or to `any` type. This stricter checking helps catch errors where `null` or `undefined` might be assigned inadvertently.

```typescript
let value: number;
value = null;        // Error
value = undefined;   // Error

let nullableValue: number | null;
nullableValue = null;  // OK
nullableValue = undefined;  // Error

let undefinableValue: number | undefined;
undefinableValue = undefined;  // OK
undefinableValue = null;  // Error

let maybe: number | null | undefined;
maybe = null;        // OK
maybe = undefined;   // OK
```

#### Never
The `never` type represents the type of values that never occur.  It doesn't even return undefined like void. it is used for throwing exceptions since the value never occurs, example throwing an exception is default case in switch statement.
```typescript
function error(message: string): never {
  throw new Error(message);
}
```

### 3. Advanced Types

#### Type Assertions
Type assertions are used when you know more about the type than TypeScript does.
```typescript
let someValue: any = 'this is a string';
let strLength: number = (someValue as string).length;
```

#### Type Inference
TypeScript can infer types when they are not explicitly provided.
```typescript
let x = 3; // inferred as number
```

#### Union Types
Union types allow a value to be one of several types.
```typescript
let value: number | string;
value = 42;
value = 'Hello';
```

#### Intersection Types
Intersection types combine multiple types into one.
```typescript
interface A {
  a: string;
}
interface B {
  b: number;
}
type AB = A & B;
let ab: AB = { a: 'foo', b: 42 };
```

#### Literal Types
Literal types allow specifying exact values a variable can hold.
```typescript
let direction: 'north' | 'south' | 'east' | 'west';
direction = 'north';
```

#### Type Aliases
Type aliases create new names for types.
```typescript
type ID = string | number;
let userId: ID;
userId = 123;
userId = 'abc';
```

#### Interface
Interfaces define the shape of an object.
```typescript
interface User {
  name: string;
  age: number;
}
let user: User = { name: 'John', age: 30 };
```

#### Function Types
Interfaces can also describe function types.
```typescript
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
  return source.search(subString) > -1;
}
```

### 4. Object-Oriented Programming

#### Class Basics
TypeScript supports object-oriented programming features like classes.
```typescript
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

let john = new Person('John Doe');
john.greet(); // Output: Hello, my name is John Doe
```

#### Inheritance
Classes can inherit from other classes.
```typescript
class Employee extends Person {
  employeeId: number;
  constructor(name: string, employeeId: number) {
    super(name);
    this.employeeId = employeeId;
  }
  displayEmployeeInfo() {
    console.log(`Name: ${this.name}, Employee ID: ${this.employeeId}`);
  }
}

let jane = new Employee('Jane Doe', 123);
jane.displayEmployeeInfo(); // Output: Name: Jane Doe, Employee ID: 123
```

#### Polymorphism
Polymorphism allows objects of different classes to be treated as objects of a common superclass. It is a core concept that allows for methods to do different things based on the object it is acting upon. Polymorphism is typically achieved through method overriding and interfaces.

**Method Overriding** allows a subclass to provide a specific implementation of a method that is already defined in its superclass. This is a form of runtime polymorphism.

```typescript
class Animal {
    move(): void {
        console.log("Animal is moving");
    }
}

class Dog extends Animal {
    move(): void {
        console.log("Dog is running");
    }
}

class Bird extends Animal {
    move(): void {
        console.log("Bird is flying");
    }
}

function moveAnimal(animal: Animal): void {
    animal.move();
}

const myDog = new Dog();
const myBird = new Bird();

moveAnimal(myDog);  // Output: Dog is running
moveAnimal(myBird); // Output: Bird is flying
```

**Interfaces** can also be used to achieve polymorphism. By defining a common interface that different classes implement, you can write code that works with any class that implements the interface.

```typescript
interface Shape {
    getArea(): number;
}

class Circle implements Shape {
    constructor(public radius: number) {}

    getArea(): number {
        return Math.PI * this.radius ** 2;
    }
}

class Rectangle implements Shape {
    constructor(public width: number, public height: number) {}

    getArea(): number {
        return this.width * this.height;
    }
}

function printArea(shape: Shape): void {
    console.log(`The area is ${shape.getArea()}`);
}

const myCircle = new Circle(5);
const myRectangle = new Rectangle(4, 6);

printArea(myCircle);    // Output: The area is 78.53981633974483
printArea(myRectangle); // Output: The area is 24
```

#### Encapsulation
Encapsulation restricts direct access to some of an object's components, which can be achieved using access modifiers such as private, protected, and public.

Public, Private, Protected Modifiers
Access modifiers control the accessibility of class members.
- `public` (default) members are accessible everywhere.
- `private` members are only accessible within the class.
- `protected` members are accessible within the class and subclasses.

```typescript
class Animal {
  private name: string;
  protected species: string;
  public age: number;

  constructor(name: string, species: string, age: number) {
    this.name = name;
    this.species = species;
    this.age = age;
  }

  getName(): string {
    return this.name;
  }
}

class Dog extends Animal {
  constructor(name: string, age: number) {
    super(name, 'Dog', age);
  }

  getSpecies(): string {
    return this.species;
  }
}

let myDog = new Dog('Buddy', 5);
console.log(myDog.age); // 5
console.log(myDog.getName()); // Buddy
console.log(myDog.getSpecies()); // Dog
```
#### Abstraction

Abstraction means hiding the complex implementation details and showing only the essential features of an object. Abstract classes and interfaces are used to achieve abstraction.

**Abstract Classes**
Abstract classes cannot be instantiated and must be extended by other classes. Abstract methods can be used only inside abstract class. it makes subclasses to mandate the implementation of abstract method.
```typescript
abstract class Animal {
  abstract makeSound(): void;
  move(): void {
    console.log('Moving...');
  }
}

class Cat extends Animal {
  makeSound(): void {
    console.log('Meow');
  }
}

let myCat = new Cat();
myCat.makeSound(); // Meow
myCat.move(); // Moving...
```


#### Readonly Modifier
The `readonly` modifier ensures a property can only be assigned once.
```typescript
class Vehicle {
  readonly make: string;
  constructor(make: string) {
    this.make = make;
  }
}

let myCar = new Vehicle('Toyota');
console.log(myCar.make); // Toyota
// myCar.make = 'Honda'; // Error: Cannot assign to 'make' because it is a read-only property.
```
#### Constant Variable
The `Constant` is similar to that of readonly but it need to be initialize at declaration.
```typescript
const PI = 3.14;
const GREETING = "Hello, World!";
GREETING = "Bye"; // Error: Cannot assign to 'GREETING' because it is a constant

const user = { name: "Alice", age: 30 };
user.age = 31; // This is allowed
user = { name: "Ten", age: 32 }; // This is not allowed

const numbers = [1, 2, 3];
numbers.push(4); // This is allowed
numbers = [7, 9, 10, 11]; //This is not allowed
```

#### Static Properties
Static properties are shared among all instances of a class.
```typescript
class Circle {
  static pi: number = 3.14;
  radius: number;

  constructor(radius: number) {
    this.radius = radius;
  }

  calculateArea(): number {
    return Circle.pi * this.radius * this.radius;
  }
}

// Accessing the static property
console.log(Circle.pi); // 3.14

// Creating an instance of Circle and using an instance method
const circle = new Circle(10);
console.log(circle.getArea()); // 314

// Trying to access the static property through an instance
// console.log(circle.pi); // Error: Property 'pi' does not exist on type 'Circle'

```

#### Interfaces
Interfaces define contracts for classes.
```typescript
interface Shape {
  area(): number;
}

class Rectangle implements Shape {
  width: number;
  height: number;

  constructor(width: number, height: number) {
    this.width = width;
    this.height = height;
  }

  area(): number {
    return this.width * this.height;
  }
}

let rect = new Rectangle(10, 20);
console.log(rect.area()); // 200
```

### 5. Generics

Generics in TypeScript provide a way to create reusable and flexible components that can work with a variety of data types. By using generics, you can write functions, classes, and interfaces that can operate on different types without sacrificing type safety. This makes your code more robust and maintainable.

#### Generic Functions

A generic function is defined using a type parameter, which acts as a placeholder for the actual type that will be provided when the function is called.

```typescript
function identity<T>(arg: T): T {
    return arg;
}

const numberIdentity = identity<number>(42);
const stringIdentity = identity<string>("Hello");

console.log(numberIdentity); // Output: 42
console.log(stringIdentity); // Output: Hello
```

In this example, the `identity` function takes a type parameter `T` and an argument of type `T`. It returns a value of type `T`. When calling the function, you can specify the type (`number` and `string` in this case).

#### Generic Classes

Generic classes allow you to define classes that can operate on different types.

```typescript
class GenericBox<T> {
    contents: T;

    constructor(value: T) {
        this.contents = value;
    }

    getContents(): T {
        return this.contents;
    }
}

const numberBox = new GenericBox<number>(123);
const stringBox = new GenericBox<string>("TypeScript");

console.log(numberBox.getContents()); // Output: 123
console.log(stringBox.getContents()); // Output: TypeScript
```

In this example, `GenericBox` is a generic class that works with any type `T`. The type is specified when creating an instance of the class.

#### Generic Interfaces

Generic interfaces allow you to define a contract for functions, classes, or objects that work with various types.

```typescript
interface Pair<T, U> {
    first: T;
    second: U;
}

const pair: Pair<number, string> = {
    first: 42,
    second: "Hello"
};

console.log(pair.first);  // Output: 42
console.log(pair.second); // Output: Hello
```

In this example, `Pair` is a generic interface with two type parameters `T` and `U`, representing the types of its properties.

#### Generic Constraints

Generic constraints are used to restrict the types that can be passed to a generic function, class, or interface. This means you can specify that a generic type must have certain properties or methods.

```typescript
interface Lengthwise {
    length: number;
}

function logLength<T extends Lengthwise>(arg: T): void {
    console.log(arg.length);
}

logLength({ length: 10, value: "Hello" }); // Output: 10
// logLength(3); // Error: Argument of type 'number' is not assignable to parameter of type 'Lengthwise'.
```

In this example, the `logLength` function only accepts arguments that have a `length` property(here propery means ex: for a string type implicitly we can use int1.length or { length: 10, value: "Hello" } here we have inserted explicitly length propery as an object form). This constraint is enforced by `T extends Lengthwise`.

#### Difference b/w Any Type and Generic type

**Any Type**
- **No Type Checking**: Allows any type of value without compile-time checks.
- **Maximum Flexibility**: Can hold any type of value and perform any operation.
- **Loss of Type Safety**: Increases risk of runtime errors due to lack of type constraints.
- **No Type Inference**: TypeScript does not infer types, leading to potential issues.
- **Reduced Readability**: Makes code harder to understand and maintain.
- **Use Sparingly**: Best for cases where the type is truly unknown or for quick prototyping.

**Generic Type**
- **Type Safety**: Ensures type consistency and correctness at compile-time.
- **Flexibility with Constraints**: Can work with various types while enforcing type constraints.
- **Type Inference**: TypeScript can infer types, enhancing safety and reducing errors.
- **Improved Readability**: Explicitly defines type relationships, making code clearer.
- **Reusable Components**: Ideal for creating functions, classes, and interfaces that work with multiple types.
- **Preferred Choice**: Use generics for writing flexible and type-safe code. 

### 6. Advanced Topics

#### Type Guards and Differentiating Types
Type guards are used to narrow down the type within a conditional block.
```typescript
function isNumber(x: any): x is number {
  return typeof x === 'number';
}

function padLeft(value: string, padding: number | string) {
  if (isNumber(padding)) {
    return Array(padding + 1).join(' ') + value;
  }
  if (typeof padding === 'string') {
    return padding + value;
  }
  throw new Error(`Expected string or number, got '${typeof padding}'.`);
}

console.log(padLeft('Hello', 4)); // "    Hello"
console.log(padLeft('Hello', '>>')); // ">>Hello"
```

#### Type Compatibility
TypeScript's type compatibility is based on structural subtyping.
```typescript
interface Named {
  name: string;
}

class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

let p: Named;
p = new Person('John');
console.log(p.name); // John
```

#### Module Augmentation
Module augmentation allows you to add new members to existing modules.
```typescript
import * as moment from 'moment';

declare module 'moment' {
  export interface Moment {
    toCustomFormat(): string;
  }
}

moment.fn.toCustomFormat = function () {
  return this.format('YYYY-MM-DD');
};

console.log(moment().toCustomFormat()); // current date in 'YYYY-MM-DD' format
```

#### Declaration Merging
TypeScript allows multiple declarations to be merged.
```typescript
interface Box {
  height: number;
  width: number;
}

interface Box {
  scale: number;
}

let box: Box = { height: 5, width: 6, scale: 10 };
console.log(box);
```

#### Utility Types
Utility types help with common type transformations.
- `Partial<Type>`: Makes all properties optional.
- `Readonly<Type>`: Makes all properties readonly.
- `Record<Keys, Type>`: Constructs an object type with a set of properties.
- `Pick<Type, Keys>`: Creates a type by picking properties from another type.
- `Omit<Type, Keys>`: Creates a type by omitting properties from another type.

```typescript
interface Todo {
  title: string;
  description: string;
}

type PartialTodo = Partial<Todo>;
type ReadonlyTodo = Readonly<Todo>;
type RecordTodo = Record<'title' | 'description', string>;
type PickTodo = Pick<Todo, 'title'>;
type OmitTodo = Omit<Todo, 'description'>;
```

### 7. Decorators

#### Introduction to Decorators
Decorators are a special kind of declaration in TypeScript that can be attached to a class, method, accessor, property, or parameter. They allow you to modify the behavior of the decorated entity at runtime. By using decorators, you can enhance or change the predefined behavior of that entity, providing a powerful tool for meta-programming and adding reusable functionality.

To enable experimental decorators, add `"experimentalDecorators": true` to your `tsconfig.json`.

#### Class Decorators
Class decorators are applied to the constructor of a class.
```typescript
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@sealed
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return `Hello, ${this.greeting}`;
  }
}
```

#### Method Decorators
Method decorators are applied to the methods of a class.
```typescript
function enumerable(value: boolean) {
  return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.enumerable = value;
  };
}

class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }

  @enumerable(false)
  greet() {
    return `Hello, ${this.greeting}`;
  }
}
```

#### Accessor Decorators
Accessor decorators are applied to the accessors of a class.
```typescript
function configurable(value: boolean) {
  return function(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.configurable = value;
  };
}

class Point {
  private _x: number;
  private _y: number;

  constructor(x: number, y: number) {
    this._x = x;
    this._y = y;
  }

  @configurable(false)
  get x() {
    return this._x;
  }

  @configurable(false)
  get y() {
    return this._y;
  }
}
```

#### Property Decorators
Property decorators are applied to properties of a class.
```typescript
function format(formatString: string) {
  return function(target: any, propertyKey: string) {
    let value: string;

    const getter = function() {
      return value;
    };

    const setter = function(newVal: string) {
      value = formatString.replace('{value}', newVal);
    };

    Object.defineProperty(target, propertyKey, {
      get: getter,
      set: setter,
      enumerable: true,
      configurable: true
    });
  };
}

class Person {
  @format('Mr./Ms. {value}')
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}

let p = new Person('John');
console.log(p.name); // Mr./Ms. John
```

#### Parameter Decorators
Parameter decorators are applied to the parameters of a class constructor or method.
```typescript
function required(target: any, propertyKey: string, parameterIndex: number) {
  console.log(`Parameter at index ${parameterIndex} is required for method ${propertyKey}`);
}

class BugReport {
  type = 'report';

  constructor(@required title: string) {}
}

let report = new BugReport('Need bug report');
```

### 8. Modules and Namespaces

#### Introduction to Modules
Modules are executed within their own scope, not in the global scope. They can export declarations to be used in other modules.

#### Export and Import
Modules can export declarations using `export` and import them using `import`.
```typescript
// math.ts
export function add(x: number, y: number): number {
  return x + y;
}

// app.ts
import { add } from './math';

console.log(add(5, 3)); // 8
```

#### Default Exports
Modules can have a default export.
```typescript
// math.ts
export default function subtract(x: number, y: number): number {
  return x - y;
}

// app.ts
import subtract from './math';

console.log(subtract(10, 3)); // 7
```

#### Namespaces
Namespaces are a way to group related code together.
```typescript
namespace Geometry {
  export class Square {
    constructor(public sideLength: number) {}
    area() {
      return this.sideLength * this.sideLength;
    }
  }
}

let square = new Geometry.Square(5);
console.log(square.area()); // 25
```

#### Module Resolution
Module resolution is the process TypeScript uses to find what an import refers to.
```typescript
// Example with module resolution
// math.ts
export function multiply(x: number, y: number): number {
  return x * y;
}

// app.ts
import { multiply } from './math';

console.log(multiply(4, 5)); // 20
```

### 9. Asynchronous Programming

#### Promises
Promises are used to handle asynchronous operations.
```typescript
let promise = new Promise((resolve, reject) => {
  let success = true;
  if (success) {
    resolve('Operation was successful');
  } else {
    reject('Operation failed');
  }
});

promise
  .then((message) => {
    console.log(message);
  })
  .catch((error) => {
    console.error(error);
  });
```

#### Async/Await
`async` and `await` make asynchronous code look like synchronous code.
```typescript
function delay(ms: number) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function asyncFunction() {
  console.log('Start');
  await delay(2000);
  console.log('End after 2 seconds');
}

asyncFunction();
```

#### Working with APIs
Using async/await to fetch data from an API.
```typescript
async function fetchData(url: string) {
  try {
    let response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchData('https://api.example.com/data');
```

### 10. Interview Preparation Programs

#### Common Algorithms

##### 1. **Binary Search**
```typescript
function binarySearch(arr: number[], target: number): number {
  let left = 0, right = arr.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (arr[mid] === target) return mid;
    else if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}

console.log(binarySearch([1, 2, 3, 4, 5], 3)); // 2
```

##### 2. **Quick Sort**
```typescript
function quickSort(arr: number[]): number[] {
  if (arr.length <= 1) return arr;
  const pivot = arr[Math.floor(arr.length / 2)];
  const left = arr.filter(x => x < pivot);
  const middle = arr.filter(x => x === pivot);
  const right = arr.filter(x => x > pivot);
  return [...quickSort(left), ...middle, ...quickSort(right)];
}

console.log(quickSort([3, 6, 8, 10, 1, 2, 1])); // [1, 1, 2, 3, 6, 8, 10]
```

##### 3. **Merge Sort**
```typescript
function mergeSort(arr: number[]): number[] {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left: number[], right: number[]): number[] {
  const result = [];
  while (left.length && right.length) {
    if (left[0] < right[0]) {
      result.push(left.shift()!);
    } else {
      result.push(right.shift()!);
    }
  }
  return result.concat(left, right);
}

console.log(mergeSort([10, 24, 76, 73, 72, 1, 9])); // [1, 9, 10, 24, 72, 73, 76]
```

#### Data Structures

##### 1. **Stack**
```typescript
class Stack<T> {
  private items: T[] = [];

  push(item: T) {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }

  peek(): T | undefined {
    return this.items[this.items.length - 1];
  }

  isEmpty(): boolean {
    return this.items.length === 0;
  }

  size(): number {
    return this.items.length;
  }
}

const stack = new Stack<number>();
stack.push(1);
stack.push(2);
console.log(stack.peek()); // 2
console.log(stack.pop()); // 2
console.log(stack.pop()); // 1
```

##### 2. **Queue**
```typescript
class Queue<T> {
  private items: T[] = [];

  enqueue(item: T) {
    this.items.push(item);
  }

  dequeue(): T | undefined {
    return this.items.shift();
  }

  front(): T | undefined {
    return this.items[0];
  }

  isEmpty(): boolean {
    return this.items.length === 0;
  }

  size(): number {
    return this.items.length;
  }
}

const queue = new Queue<number>();
queue.enqueue(1);
queue

.enqueue(2);
console.log(queue.front()); // 1
console.log(queue.dequeue()); // 1
console.log(queue.dequeue()); // 2
```

##### 3. **Linked List**
```typescript
class Node<T> {
  value: T;
  next: Node<T> | null = null;

  constructor(value: T) {
    this.value = value;
  }
}

class LinkedList<T> {
  head: Node<T> | null = null;

  append(value: T) {
    const newNode = new Node(value);
    if (this.head === null) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next !== null) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  prepend(value: T) {
    const newNode = new Node(value);
    newNode.next = this.head;
    this.head = newNode;
  }

  delete(value: T) {
    if (this.head === null) return;

    if (this.head.value === value) {
      this.head = this.head.next;
      return;
    }

    let current = this.head;
    while (current.next !== null && current.next.value !== value) {
      current = current.next;
    }

    if (current.next !== null) {
      current.next = current.next.next;
    }
  }

  find(value: T): Node<T> | null {
    let current = this.head;
    while (current !== null && current.value !== value) {
      current = current.next;
    }
    return current;
  }

  display() {
    let current = this.head;
    while (current !== null) {
      console.log(current.value);
      current = current.next;
    }
  }
}

const list = new LinkedList<number>();
list.append(1);
list.append(2);
list.prepend(0);
list.display(); // 0, 1, 2
list.delete(1);
list.display(); // 0, 2
console.log(list.find(2)); // Node { value: 2, next: null }
```

##### 4. **Hash Table**
```typescript
class HashTable<T> {
  private table: { [key: string]: T } = {};

  set(key: string, value: T) {
    this.table[key] = value;
  }

  get(key: string): T | undefined {
    return this.table[key];
  }

  remove(key: string) {
    delete this.table[key];
  }

  has(key: string): boolean {
    return this.table.hasOwnProperty(key);
  }

  keys(): string[] {
    return Object.keys(this.table);
  }
}

const hashTable = new HashTable<number>();
hashTable.set('a', 1);
hashTable.set('b', 2);
console.log(hashTable.get('a')); // 1
console.log(hashTable.has('b')); // true
hashTable.remove('a');
console.log(hashTable.keys()); // ['b']
```

##### 5. **Binary Tree**
```typescript
class TreeNode<T> {
  value: T;
  left: TreeNode<T> | null = null;
  right: TreeNode<T> | null = null;

  constructor(value: T) {
    this.value = value;
  }
}

class BinaryTree<T> {
  root: TreeNode<T> | null = null;

  insert(value: T) {
    const newNode = new TreeNode(value);
    if (this.root === null) {
      this.root = newNode;
    } else {
      this.insertNode(this.root, newNode);
    }
  }

  private insertNode(node: TreeNode<T>, newNode: TreeNode<T>) {
    if (newNode.value < node.value) {
      if (node.left === null) {
        node.left = newNode;
      } else {
        this.insertNode(node.left, newNode);
      }
    } else {
      if (node.right === null) {
        node.right = newNode;
      } else {
        this.insertNode(node.right, newNode);
      }
    }
  }

  inOrderTraversal(node: TreeNode<T> | null = this.root) {
    if (node !== null) {
      this.inOrderTraversal(node.left);
      console.log(node.value);
      this.inOrderTraversal(node.right);
    }
  }

  preOrderTraversal(node: TreeNode<T> | null = this.root) {
    if (node !== null) {
      console.log(node.value);
      this.preOrderTraversal(node.left);
      this.preOrderTraversal(node.right);
    }
  }

  postOrderTraversal(node: TreeNode<T> | null = this.root) {
    if (node !== null) {
      this.postOrderTraversal(node.left);
      this.postOrderTraversal(node.right);
      console.log(node.value);
    }
  }

  find(value: T, node: TreeNode<T> | null = this.root): TreeNode<T> | null {
    if (node === null) return null;
    if (value < node.value) return this.find(value, node.left);
    if (value > node.value) return this.find(value, node.right);
    return node;
  }
}

const tree = new BinaryTree<number>();
tree.insert(10);
tree.insert(5);
tree.insert(15);
tree.insert(3);
tree.insert(7);
tree.inOrderTraversal(); // 3, 5, 7, 10, 15
console.log(tree.find(7)); // TreeNode { value: 7, left: null, right: null }
```

#### Sample Coding Interview Problems

##### 1. **Two Sum**
```typescript
function twoSum(nums: number[], target: number): number[] {
  const map = new Map<number, number>();
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement)!, i];
    }
    map.set(nums[i], i);
  }
  return [];
}

console.log(twoSum([2, 7, 11, 15], 9)); // [0, 1]
```

##### 2. **Longest Substring Without Repeating Characters**
```typescript
function lengthOfLongestSubstring(s: string): number {
  let maxLength = 0;
  let start = 0;
  const map = new Map<string, number>();

  for (let end = 0; end < s.length; end++) {
    if (map.has(s[end])) {
      start = Math.max(map.get(s[end])! + 1, start);
    }
    map.set(s[end], end);
    maxLength = Math.max(maxLength, end - start + 1);
  }

  return maxLength;
}

console.log(lengthOfLongestSubstring('abcabcbb')); // 3
```

##### 3. **Valid Parentheses**
```typescript
function isValid(s: string): boolean {
  const stack: string[] = [];
  const map: { [key: string]: string } = {
    '(': ')',
    '{': '}',
    '[': ']'
  };

  for (const char of s) {
    if (char in map) {
      stack.push(map[char]);
    } else {
      if (stack.pop() !== char) {
        return false;
      }
    }
  }

  return stack.length === 0;
}

console.log(isValid('()[]{}')); // true
console.log(isValid('([)]')); // false
```

##### 4. **Merge Two Sorted Lists**
```typescript
class ListNode {
  val: number;
  next: ListNode | null = null;

  constructor(val: number) {
    this.val = val;
  }
}

function mergeTwoLists(l1: ListNode | null, l2: ListNode | null): ListNode | null {
  const dummy = new ListNode(0);
  let current = dummy;

  while (l1 !== null && l2 !== null) {
    if (l1.val < l2.val) {
      current.next = l1;
      l1 = l1.next;
    } else {
      current.next = l2;
      l2 = l2.next;
    }
    current = current.next;
  }

  current.next = l1 !== null ? l1 : l2;
  return dummy.next;
}

const l1 = new ListNode(1);
l1.next = new ListNode(2);
l1.next.next = new ListNode(4);

const l2 = new ListNode(1);
l2.next = new ListNode(3);
l2.next.next = new ListNode(4);

let mergedList = mergeTwoLists(l1, l2);
while (mergedList !== null) {
  console.log(mergedList.val);
  mergedList = mergedList.next;
}
// Output: 1, 1, 2, 3, 4, 4
```

##### 5. **Maximum Subarray**
```typescript
function maxSubArray(nums: number[]): number {
  let maxCurrent = nums[0];
  let maxGlobal = nums[0];

  for (let i = 1; i < nums.length; i++) {
    maxCurrent = Math.max(nums[i], maxCurrent + nums[i]);
    if (maxCurrent > maxGlobal) {
      maxGlobal = maxCurrent;
    }
  }

  return maxGlobal;
}

console.log(maxSubArray([-2, 1, -3, 4, -1, 2, 1, -5, 4])); // 6
```

### Conclusion
This comprehensive guide covers essential TypeScript topics and provides practical examples and coding interview problems to help you prepare for your interviews. By practicing these concepts and implementing the provided programs, you'll build a solid foundation in TypeScript and

 improve your coding skills.

Good luck with your learning and interview preparation!
