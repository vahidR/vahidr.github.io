---
layout: post
title: "Introduction to TypeScript, Part 2/4"
date: 2020-11-04 11:38:48 +0100
categories: typescript
comments: true
---

![Credit: Alessandro Rossi](https://images.unsplash.com/photo-1604142056225-1feabdac3af1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1490&q=80)

### Table of Contents
Part I - [Introduction](https://vahid-r.com/introduction-to-typescript-part-1)  
Part II - [Types, Variables, and Functions](https://vahid-r.com/introduction-to-typescript-part-2)  
Part III - [Classes and Interfaces](https://vahid-r.com/introduction-to-typescript-part-3)  
Part IV - [Modules](https://vahid-r.com/introduction-to-typescript-part-4)


In Part II, I’m going to discuss the **Types**, **Variables**, and **Functions**.
You can find Part I of the tutorial [here](https://vahid-r.com/introduction-to-typescript-part-1).

## Type Inference

First of all, in TypeScript, we have a beautiful concept called _Type Inference_. Technically it means that when you define an entity, the compiler tries to infer or understand the type that you talking about.
For instance when the TypeScript compiler seems something like this:

```typescript
let num = 3;
```

It infers that the variable “num” must be a **number**! So these two lines should be equal:

```typescript
let num = 3;
let num: number = 3; // They are the same
```

This is amazing because you have to type less, but be careful! It is like a double-edged sword. For people like me that prefer static typing and prefer to get help from the compiler on types, the main reason for considering TypeScript was to have specific types bundled with entities in the first place! So If you are like me, try to mention the type yourself. It will save you later in the large scale projects.

## Ambient declaration

Sometimes you don’t know the type of a variable or entity in advance. For example, you are going to use a third party library and want to refer to that as a variable. In this case, you can use the keyword **declare**. This keyword allows you to infer the type of it as you go along with the code further.

For example, let’s say declare a variable for a document

```typescript
declare var document;
```

What is the type of document here? We don’t know yet. But if do something like to one line below:

```typescript
document.title = "This is a title";
```

Then the compiler says AHA!. The document should be of type “string”.
In the real-world, the usage can be using third-party libraries like jQuery or any other library.

For jQuery, we can do something like this:

```typescript
/// <reference path=”jquery.d.ts” />
declare var $;
var hello = "Hello World";
$("div").text(hello);
```

## Basic Types

In TypeScript, we have all the types that are supported in JavaScript plus an extra enumeration type. You can find the list of basic types in the [official documentation](https://www.typescriptlang.org/docs/handbook/basic-types.html), but I summarise them with a minimal explanation here for future references.

### Number

We can have the number type is a default type for numerical values, except for big integers that you have a separate type for that. Here are some examples of the type number:

```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```

### Boolean

Like booleans in any other programming language:

```typescript
var isActive: boolean = true;
```

### String

The most well-known type on planet earth!

```typescript
let name: string = "Ryan";
```

### Array

Arrays in TypeScript are very interesting. If you are a Java developer, you will be amazed that Arrays in TypeScript, just like in Java, can be Generic and accept the type that they are supposed to work with! So if you want to have an Array of numbers you can declare it as the following:

```typescript
let list: Array<number> = [1, 2, 3, 4, 5];
```

### Tuple

Tuples are Arrays with a fixed number of elements!

```typescript
let x: [string, number] = ["hi", 20];
```

### Enum

Enums are types that can help you to hold an entity with a limited number of values. If you know any C-based language, the concept is not foreign to you.

```typescript
enum Direction {
  RIGHT,
  LEFT,
  UP,
  DOWN,
}

let dir: Direction = Direction.RIGHT;
```

### Unknown

In TypeScript, we have a default type called “any”. So this code is of type “any”:

```typescript
var someVariable;
```

we can cast types together if we don’t define the type of a variable. So it should work:

```typescript
var message = 100 + " Hi, there"; // → OK!
```

But if we define the type of the variable message above, it gives an error:

```typescript
var message: number = 100 + " Hi, there"; // → FAIL
```

### Void

Mostly used for functions that return nothing. In a more technical sense, they are mostly deal with **side-effects**, like directing to the outside world of the application (console, file, DB, network, etc.)

```typescript
function sendMessage(message: string): void {
  console.log(message);
}
```

### Null

Like nulls in other languages, it is something that you can assign to any primitive types like string, number, boolean, etc.
Null is a sub-type of all primitives, except for “void” and “undefined”.

```typescript
var name: string = null;
var age: number = null;
var obj: {} = null; // Noticed the object literal type? Amazing!
```

### Undefined

Just like what we have in the JavaScript world. When you define a variable and it has no value yet. So the following two lines are the same:

```typescript
var name: string;

var name: string = undefined;
```

### Never

This type is used in cases that you never expect a result to be seen.
For instance, if a function throws an exception! You never expect a result from that function:

```typescript
function error(message: string): never {
  throw new Error(messag);
}
```

Another example is when you are dealing with infinite loops (who said writing games are not fun?)

```typescript
function infiniteLoop(): never {
  while(true) {
    …
  }
}
```

### Objects

In TypeScript, as it is built on top of JavaScript, we have the concept of objects to the same extent that we have and understand in JavaScript.
For instance, objects, functions, modules, interfaces, and literal types are all objects.

```typescript
var person = {
   name:"Ryan"
   age:2
};
alert(person.name);
alert(person.age);
```

### Functions

The concept of functions is not alien to you if you are an experienced programmer.
In TypeScript, there are multiple ways to define a function. We can define them with the keyword “function” (please attention to the type declaration):

```typescript
function addTwoParams(x: number, y: number): number {
  return x + y;
}
```

or we can use the Anonymous functions:

```typescript
var addTwoParams = function (x: number, y: number): number {
  return x + y;
};
```

For the Anonymous functions (lambdas), we also have a syntactic sugar version called the “Arrow Functions”:

```typescript
var addTwoParams = (x: number, y: number): number => x * y;
```

One more thing about functions. There are times when the return type of a function is void, just like in C based languages.
We have this notion in TypeScript as well:

```typescript
var sayHi: (message: string) => void;
sayHi = function (message) {
  alert(message);
};
```

## Optional Parameters

Sometimes you want to have a function that has arbitrary arguments. In this case, you can mark those arguments with a (**?**) sign and within the body of the function decide if they are provided or not. Take a look at the example:

```typescript
function sayHi(firtName: string, lastName?: string): string {
  if (lastName) {
    return "Hi " + firstName + " " + lastName;
  }
  return "Hi " + firstName;
}
```

## Default Parameters

Sometimes you might want to have a default value for arguments, in cases that they are not provided by the caller. Default parameters come in handy in these cases:

```typescript
function discount(value: number, amount = 0.2): number {
  return value * amount;
}
```

## Rest Parameters

Sometimes you don’t know the number of arguments that are supposed to be sent to a function. In these scenarios, the function can accept the rest parameters with the notion of three dots “**…**”.

A rest parameter has **three** rules:

1. A function has **only one** rest parameter.
2. The rest parameter appears **last** in the parameter list.
3. The type of the rest parameter is an **array type**.

```typescript
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}
// employeeName will be "Joseph Samuel Lucas MacKinzie"
let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie"); 
```

## Functions and Interfaces
Did you know that the functions can follow a contract? In Java, C#, etc. we call these contracts the interface. In TypeScript, they also share the same concept. Functions are all objects so it should not be surprising that a function can follow an interface.
```typescript
interface Square {
  (x: number) : number;
}
var squareMe: Square = (num) => num * num;
```

That is all for now. In the next tutorial, we will see the **Classes** and **Interfaces** and all the goods that they provide for a large scale application.