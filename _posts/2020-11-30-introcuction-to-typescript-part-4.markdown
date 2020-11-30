---
layout: post
title: "Introduction to TypeScript, Part 4/4"
date: 2020-11-30 12:59:48 +0100
categories: typescript
---

![Credit: Marek Piwnicki](https://images.unsplash.com/photo-1605904266472-c5be8939cdb6?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&auto=format&fit=crop&w=1401&q=80)

This is the last part of the 4-part series on my learning notes about TypeScript. 
In this part, I am going to share my understanding of the TypeScript **modules**.


## Why Modules?
When you are dealing with large-scale projects, and have to split the domain among different people and teams, you have to have a way to structure the code in a sustainable manner. 
This is vital, as developing software, nowadays, is more like a sports team where everyone focuses on one or a few particular domains. 
To be more specific, we should use modules, because for three reasons at least:
#### Encapsulation
There is no need to emphasize the importance of encapsulation for developing large-scale projects. 
#### Resusability
No one wants to re-invent the wheels. When a piece of code has been developed by someone else and is useful for another developer, he/she should use it and speed up the development. Modules in TypeScript help to achieve this goal.
#### Higher level abstraction
When you use modules, you split the code and abstractions in a better fashion as well. If you follow the Domain-Driven Design practice, it is even more vital for you.

## Exporting from modules
Now lets the code speaks for itself and cut the words. 
From what I have understood, it is better to gather relevant classes/functions/etc. in separate files and consider each file as a module. 
For example, if you want to have a payment module, it is better to create a file and put the classes/functions/etc. there and consider it as a module.
```typescript
// payment.ts file
interface PaymentProvider {..}

function sendEmail() : void {..}

class Deposit() {..}

class Withdraw() {..} // Not accessible outside of the module, as we don't export it

export {PaymentProvider as Provider, sendEmail, Deposit};
```
In the above code, exporting all the entities at the end of the file is considered to be a good practice in the real-world. 
I also used an alias export above to make the name shorter. 

## Importing from other modules
Let's say all the TS files (modules) are in the same folder. We can import a single entity from a module.
```typescript
// main.ts
import Deposit from './payment';

let bankDeposit: Deposit = new Deposit();
```
Please notice that there is no need to add the suffix to the name of the module. TypeScript compiler will comprehend that for you.
It is also worthwhile to mention that we have used the **relative import** in the above code. That is why we have to add a **./** before the name of the module.
I will talk about the relative modules later on. 

We can also import multiple entities from a module. 
```typescript
// main.ts file

import {Deposit, sendEmail } from './payment';

let bankDeposit: Deposit = new Deposit();
```

We can use **aliases** while importing from a module
```typescript
import {Deposit as PaypalDepsit} from './payment';

let dep: PaypalDeposit = new PaypalDeposit();
```

Or we can import **everything** from a module which is *exportable*
```typescript
import * as Payment from './payment';

Payment.sendEmail();
```

## Relative vs Non-Relative imports.
As I mentioned before, I used relative imports above (**'./payment'**). We also have **Non-Relative** import where we don't identify the location of the modules and leave it to the compiler to comprehend. 
An example of the relative import can be the following
```typescript
import {Deposit} from './payment';
import {Login} from './auth';
import {Casino} from './game/casino';
```
For the non-relative import, the syntax is simpler
```typescript
import * as $ from 'jquery';
import { Component } from "@angular/core";
```
### When to use which? 
Based on researching the large-scale projects, I came to the conclusion that it is better to use relative imports for your own development project and use non-relative imports for integrating the third-party libraries. 

## Module Resolution Strategies
We have two types of Module Resolution Strategies: **Classic** & **Node**.
ُThe difference is that Classic is used when emitting AMD, System, or ES2015 modules. 
It is simple and needs less configuration.
On the other hand, Node is the default method when emitting CommonJS or UMD modules. It closely mirrors the Node module resolution and needs more configuration.

You can decide which one to use in the compile-time
```bash
$ tsc --moduleResolution Classic | Node
```


## Resolving Classic Relative Imports
Imagine that you have a file called *payment.ts* as follow
```typescript
// File: /source/core/payment.ts
import {Login} from './auth';
```

Now, how the compiler finds the *auth.ts* file? It searches in the same folder to find any of these two files:
```bash
/source/core/auth.ts
/source/core/auth.d.ts
```
If any of them is found, then we are okay, otherwise, the compiler raises a compile error. 


## Resolving Node Relative Imports
The Node method is more complex, as it searches for more comprehensively and has more checks.
Just like above, imagine that you have a file called *payment.ts* file. 
```typescript
// File: /source/core/payment.ts
import {Login} from './auth';
```
The following are the the paths that compiler looks for it. 
```
/source/core/auth.ts
/source/core/auth.tsx
/source/core/auth.d.ts
/source/core/auth/package.json (with "typings" property)
/source/core/index.ts
/source/core/index.tsx
/source/core/index.d.ts
```
As you can see it is more complex, but it tries to mimic the way that Node searches for the modules. 

## Resolving Classic Non-relative Imports
When dealing with the non-relative imports, the searching is more complex for the compiler. But at the end of the day, for we programmers, the import should be kind of automatic. 
Again imagine that we have a module called *payment.ts*.
```typescript
// File: /source/core/payment.ts
import {Login} from 'auth';
```
Please attention that there is no **./** at the beginning of the *auth* name. 
Now the following is how the compiler looks for the *auth.ts* module
```
/source/core/auth.ts
/source/core/auth.d.ts
/source/auth.ts
/source/auth.d.ts
(continue searching up the directory tree)
```

## Resolving Node Non-relative Imports
Again anything Node style is more complex.
 Imagine that we have a module called *payment.ts*.
```typescript
// File: /source/core/payment.ts
import {Login} from 'auth';
```
Here are the paths that the Node method would search 
```
/source/core/node_modules/auth.ts (or auth.tsx or auth.d.ts)
/source/core/node_modules/auth/package.json (with "typings" property)
/source/core/node_modules/index.ts (or index.tsx or index.d.ts)

/source/node_modules/auth.ts (or auth.tsx or auth.d.ts)
/source/node_modules/auth/package.json (with "typings" property)
/source/node_modules/index.ts (or index.tsx or index.d.ts)

(continue searching up the directory tree)
```


This was all I wanted to share with you, dear reader, about TypeScript. I hope you have enjoyed reading this series and it has been helpful for you. 
Happy Hacking...
