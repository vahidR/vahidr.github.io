---
layout: post
title: "Introduction to TypeScript, Part 3/4"
date: 2020-11-15 13:09:48 +0100
categories: typescript
---

![Credit: Bernardo Lorena Ponte](https://images.unsplash.com/photo-1605100970536-2046737bc76d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80)

# Classes and Interfaces
In this tutorial, I will discuss the Classes and Interfaces in TypeScript.
As I have mentioned before, I'm mainly a backend developer, and look at the frontend world as such.

Classes in TypeScript are defined very similar to Java and C#. 
Here is a definition of a class in TypeScript:
```typescript
class Human {
  // These are *Fields*
  name: string;
  age: number;

  // Then constructor
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  // Then methods
  sayHi() {
    return "Hi, my name is " + this.name + ", and I am " + this.age + " years old."
  }

}


let john = new Human("John", 30);
console.log(john.sayHi());
```

In the above example, *name* and *age* are class Fields and not properties. If you want to define properties, I will discuss them below. 

But before defining properties, it is worthwhile to mention that there is a shortcut to define class fields in TypeScript. All you need to do is to add the keyword *public* in front of each argument in the constructor. Look below:
```typescript
class Human {
  constructor(public name: string, public age: number);
}
```

This is another way to define fields in a class without writing them, but if you prefer to have everything in order and explicitly written, it is better to stick to the first example. 


### Defining Properties
Everything is TS is public, so if you want to have encapsulation of properties, like what we have in Java, you should make them private and have getter and setter methods for them.
```typescript
class Human {
  // These are properties.
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  // Getter
  get getName(): string {
      return this.name;
  }

  // Setter
  set setName(value: string) {
      if(value == undefined) throw 'Please provide a name!'
      this.name = value;
  }


  sayHi() {
    return "Hi, my name is " + this.getName;
  }

}
  
let vahid = new Human("vahid"); 
console.log(vahid.sayHi());
```

### Object Composition or defining Complex Types
If you are familiar with the Object-Oriented Design (OOD), you know about the Object Composition and its merits over the Inheritance. Long story short, it makes your code more modular and easier to test.
Here is an example of Object Composition in TypeScript:
```typescript
class PaymentDAO {
  ...
}

class PaymentService {
  // Compose PaymentDAO with PaymentService
  private dao: PaymentDAO;

  constructor(dao: PaymentDAO) {
    this.dao = dao;
  }

  ...
}
```

### Casting Types
Like Java, we can cast calling an object. We surround the casted type in the `< >` sign.
Here is an example:
```typescript
var table : HTMLTableElement = <HTMLTableElement> document.createElement("table");
```
Here the `<HTMLTableElement>` is mandatory. If we don't mention the casted type, the compiler will raise an error.  


### Object Inheritance
So similar to Java, we should use the keyword *extends* in the class definition and *super* in the constructor.
```typescript
class Car {
  private model: number;
  private wheels: number;

  constructor(model: number, wheels: number) {
    this.model = model;
    this.wheels = wheels;
  }

  // Setter and Getter
  ...
}


class SUV extends Car {
  private fourWheelDrive: boolean;

  constructor(model: number, wheels: number, fourWheelDrive: boolean) {
    // Call the constructor in the super class
    super(model, wheels);
    this.fourWheelDrive = fourWheelDrive;
  }
}
```


### Interfaces
Interfaces are contracts for objects. They define how objects should behave and how to coordinate with each other. The syntax, again, should be very similar to Java/C# with the same keyword of *implements*.
```typescript
interface PaymentService {
  depsit(): boolean;
  withdraw(): boolean;
} 

class PaymentServiceImpl implements PaymentService {

  depsit(): boolean {
    ...
  }

  withdraw(): boolean {
    ....
  }
}
```

### Readonly modifier
TypeScript has a very interesting feature to protect the cohesion of a class, which Java lacks! 
You can define a *readonly* property. No setter involved, which is a good practice. If you want to initialize such properties, you have to do that either in the property definition or within the constructor of the class:
```typescript
class Robot {
  readonly legs: number = 2;
  readonly name: string;

  constructor(name: string) {
    this.name = name;
  }
}

let yoogi = new Robot("Yoogi");
yoogi.name = "somethings!!"; // ERROR! Cannot assign to 'name' because it is a read-only property.
```

### Static fields and static methods
We can make the fields and method static, and make them independent from the object instantiation. This is mostly considered harmful in OOD and it's better to avoid it.
Here is an example:
```typescript
class Circle {
    static pi: number = 3.14;
    
    static calculateArea(radius:number) {
        return this.pi * radius * radius;
    }
}
Circle.pi; // returns 3.14
Circle.calculateArea(5); // returns 78.5
```


### Abstract classes
We can also make a class abstract (as a template) and then implement the real one based on that blueprint. 
```typescript
abstract class Human {
  speak(): void {};
}

class Man extends Human {
  // Implement the abstract method.
  speak(): void {
    console.log("Hi, this is a Man!");
  }
}

class Woman extends Human {
  // Implement the abstract method.
  speak(): void {
    console.log("Hi, this is a Woman!");
  }
}
```


ُُThis should be enough to get you going. Don't forget the TypeScript official [documentation](https://www.typescriptlang.org/docs/handbook/intro.html) which is a great source of knowledge. 
In the next tutorial (which is the last one by the way), I will discuss the modules and all the good things that they facilitate for the large scale projects. 




  
