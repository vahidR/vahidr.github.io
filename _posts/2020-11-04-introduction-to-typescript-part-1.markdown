---
layout: post
title: "Introduction to TypeScript, Part 1"
date: 2020-11-04 10:46:48 +0100
categories: general
---

![Credit: Jan Huber](https://images.unsplash.com/photo-1604238375869-8fa40deb74a5?ixlib=rb-1.2.1&auto=format&fit=crop&w=1534&q=80)

This weekend, I decided to teach myself TypeScript. As it is my learning style, I always take notes and put them in the Anki spaced repetition system when I learn a new subject in any field.

So let’s dive into a series of tutorials that target learning TypeScript. I am basically a Java Backend Developer and this is my perspective of learning TypeScript, so I might use terms that a front-end developer might not use, but it’s just fine, you get the idea…

## Introduction

TypeScript is a language which is built by Microsoft **on top of** JavaScript. The technical terms for that, as it is mentioned on the official website, is:

> Typescript is a **superset** of JavaScript which compiles to plain JavaScript.

Being superset of JavaScript means that you can combine the TypeScript (TS) and JavaScript (JS) even in the same TS script file!

There is also a TS compiler (called **tsc**) which compiles TS to JS directly. You can minify that JS file and include it into your HTML page like a good human being who likes to save some energy for this screwed planet!

TS has an excellent supporting tool system, like Compilers, Linters, Cloud support, IDE support, and many more. When you are developing apps that need to be scaled, these tools become a breeze. They give you a lot of flexibility and prevent you from having late-night headaches.

But the most important aspect of this language is that it has a **static typing** system. Coming from the Java backend world, this actually encouraged me to try the front-end world after almost a decade of hate and bashing it. The undisciplined nature of JS before ECMAScript 5 (ES5), drove me crazy and made me hate the JS world altogether. JS has improved a lot, especially after ES6, but it still lacks the goodies that I would like to see, like static typing.

When you are developing in languages with Dynamic nature (like JS, Python, Ruby, etc.), your best bet to keep your sanity and not seeing weird errors in production is having a lot of unit tests and most of them check the type system of the inputs to functions/methods/classes/etc. This need can be eliminated by having a static type system like what Java or C# has.

The type system in TS is interesting. you declare an entity and then the type comes after the (**:**) sign:

```typescript
class Car {
  engine: string;
  constructor(enging: string) {
    this.engine = engine;
  }
  show() {
    alert("Car has the engine: " + this.engine);
  }
}
```

As you can see from the code example, TS also provides a great encapsulation for you. Having Modules/Interfaces/Classes are a must for any large scale application. Reading a TS application should be quite easy for any backend developer, I must say.

We can define Interfaces (like what we do in Java/C#), so it becomes a **contract** for types and classes, and if we break a rule, then compilers and toolings can catch that for us.

TS also supports the anonymous functions/lambdas/arrow functions which are defined in ECMAScript 6. So technically you are open to the functional world as well.

Finally, for this short tutorial, I must say that by using TS, you have a semantic way of structuring the data in your application. You have Modules and Namespaces, you have Interfaces, Classes, Properties, and Methods, like any other sane Object-Oriented language.

In the following tutorial, I will discuss the Types, Variables, and Functions.