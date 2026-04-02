# JavaScript Execution Context & Hoisting -- Complete Interview Guide

------------------------------------------------------------------------

# 1. Execution Context

## What is Execution Context?

Execution Context is the environment in which JavaScript code is
evaluated and executed.

Every time JavaScript runs code, it creates an execution context.

------------------------------------------------------------------------

## Types of Execution Context

1.  Global Execution Context (GEC)
2.  Function Execution Context (FEC)
3.  Eval Execution Context (rarely used)

------------------------------------------------------------------------

## Global Execution Context

Created when the JS file starts running.

It creates: - Global object (window in browser, global in Node) - `this`
binding - Memory space for variables and functions

------------------------------------------------------------------------

## Function Execution Context

Created whenever a function is invoked.

Contains: - Variable environment - Scope chain - `this` binding

Each function call gets its own execution context.

------------------------------------------------------------------------

## Execution Context Phases

Every execution context has 2 phases:

### 1️⃣ Creation Phase

-   Memory allocated for variables and functions
-   Variables initialized as undefined
-   Function declarations stored entirely in memory

### 2️⃣ Execution Phase

-   Code runs line by line
-   Variables assigned actual values
-   Functions executed

------------------------------------------------------------------------

# 2. Hoisting

## What is Hoisting?

Hoisting is JavaScript's default behavior of moving declarations to the
top of their scope during the creation phase.

Important: Only declarations are hoisted, not initializations.

------------------------------------------------------------------------

## Variable Hoisting

### var

-   Hoisted
-   Initialized with undefined

Example:

console.log(a); var a = 5;

Output: undefined

------------------------------------------------------------------------

### let and const

-   Hoisted
-   NOT initialized
-   Stored in Temporal Dead Zone (TDZ)

Example:

console.log(a); let a = 5;

Result: ReferenceError

------------------------------------------------------------------------

## Function Hoisting

### Function Declaration

Fully hoisted.

Example:

sayHi();

function sayHi() { console.log("Hi"); }

Works successfully.

------------------------------------------------------------------------

### Function Expression

Not fully hoisted.

Example:

sayHi();

var sayHi = function() { console.log("Hi"); };

Error: sayHi is not a function

------------------------------------------------------------------------

# 3. Temporal Dead Zone (TDZ)

The time between entering scope and variable initialization for
let/const.

Accessing variable in TDZ causes ReferenceError.

------------------------------------------------------------------------

# 4. Scope Chain & Execution Context Relationship

When JS looks for a variable: - It checks current execution context -
Then outer context - Until global scope

This is called lexical scope.

------------------------------------------------------------------------

# 5. Beginner Interview Questions

### Q1: What is Execution Context?

The environment where JS code is executed.

### Q2: How many execution contexts exist?

Global and Function execution contexts.

### Q3: What is hoisting?

Moving declarations to the top during memory creation phase.

### Q4: Difference between var, let, const in hoisting?

var: - Hoisted - Initialized as undefined

let/const: - Hoisted - Not initialized - In TDZ

------------------------------------------------------------------------

# 6. Intermediate Interview Questions

### Q5: What happens internally before JS executes code?

Creation Phase: - Memory allocation - Hoisting - this binding

Execution Phase: - Code runs - Assignments happen

------------------------------------------------------------------------

### Q6: What is Temporal Dead Zone?

The period where let/const variables exist but cannot be accessed.

------------------------------------------------------------------------

### Q7: Output Prediction

console.log(a); var a = 10;

Output: undefined

------------------------------------------------------------------------

### Q8: Output Prediction

console.log(a); let a = 10;

Output: ReferenceError

------------------------------------------------------------------------

### Q9: Output Prediction

foo();

function foo() { console.log("Hello"); }

Output: Hello

------------------------------------------------------------------------

# 7. Advanced Interview Questions

### Q10: Why does var allow redeclaration but let does not?

var is function-scoped and does not check redeclaration strictly. let is
block-scoped and prevents redeclaration in same scope.

------------------------------------------------------------------------

### Q11: What is the difference between undefined and ReferenceError in hoisting?

undefined: - Variable exists but not assigned (var)

ReferenceError: - Variable exists but in TDZ (let/const)

------------------------------------------------------------------------

### Q12: Explain this code

var x = 1;

function test() { console.log(x); var x = 2; }

test();

Output: undefined

------------------------------------------------------------------------

### Q13: How does execution context relate to call stack?

Each time a function runs: - New execution context is created - Pushed
onto call stack - Removed after completion

------------------------------------------------------------------------

### Q14: What is lexical environment?

Internal data structure that stores: - Identifier-variable mapping -
Reference to outer environment

------------------------------------------------------------------------

### Q15: What is the difference between Execution Context and Scope?

Execution Context: Runtime environment of code.

Scope: Accessibility of variables based on lexical structure.

------------------------------------------------------------------------

# 8. Senior-Level Questions

### Q16: How does JavaScript handle memory during creation phase?

It allocates memory space for: - Variables - Function declarations -
Parameters

------------------------------------------------------------------------

### Q17: Why are function declarations fully hoisted but function expressions are not?

Because function declarations are stored completely during creation
phase. Function expressions behave like variables.

------------------------------------------------------------------------

### Q18: What is the internal structure of Execution Context?

Contains: - Variable Environment - Lexical Environment - this binding

------------------------------------------------------------------------

### Q19: Explain the difference between lexical environment and variable environment.

Variable Environment: Used for var declarations.

Lexical Environment: Used for let, const, and block scope.

------------------------------------------------------------------------

### Q20: Why is understanding execution context important in interviews?

Because it explains: - Hoisting behavior - Scope - Closure behavior -
Memory allocation - Call stack mechanics

------------------------------------------------------------------------

# Final Summary

Execution Context explains how JavaScript runs code internally.

Hoisting happens during creation phase.

Key rules: - var → hoisted and initialized as undefined - let/const →
hoisted but in TDZ - Function declarations → fully hoisted - Function
expressions → partially hoisted

Mastering execution context is essential for understanding closures,
scope chain, and advanced JavaScript behavior.
