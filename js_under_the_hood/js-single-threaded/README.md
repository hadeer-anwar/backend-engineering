# JavaScript Single Thread -- Complete Interview Guide

------------------------------------------------------------------------

## 1. Core Concept

### What Does "Single-Threaded" Mean?

JavaScript executes one task at a time using a single Call Stack. It
does not run multiple pieces of JavaScript code simultaneously on the
main thread.

Important: - One Call Stack - One main execution thread - Concurrency
handled via Event Loop

------------------------------------------------------------------------

## 2. Architecture Overview

### Components

1.  Call Stack
2.  Web APIs / Node APIs
3.  Callback (Macrotask) Queue
4.  Microtask Queue
5.  Event Loop

Execution Priority Order:

1.  Run all synchronous code
2.  Execute all microtasks
3.  Execute one macrotask
4.  Repeat

Microtasks always run before macrotasks.

------------------------------------------------------------------------

## 3. Beginner Interview Questions

### Q1: What does single-threaded mean in JavaScript?

JavaScript can execute only one task at a time using one call stack.

### Q2: What is the Call Stack?

A LIFO data structure that tracks function execution.

### Q3: What happens if the call stack is busy?

The browser freezes. No async callbacks execute until stack is empty.

### Q4: Is setTimeout synchronous?

No. It is asynchronous and handled by the environment (browser or Node).

------------------------------------------------------------------------

## 4. Intermediate Interview Questions

### Q5: What is the Event Loop?

A mechanism that continuously checks if the call stack is empty and
moves tasks from queues to the stack.

### Q6: Difference between Microtask and Macrotask?

Microtasks: - Promise.then - async/await continuation - queueMicrotask -
Higher priority

Macrotasks: - setTimeout - setInterval - setImmediate (Node) - DOM
events

Microtasks run before macrotasks.

------------------------------------------------------------------------

### Q7: What is the output?

console.log(1); setTimeout(() =\> console.log(2), 0);
Promise.resolve().then(() =\> console.log(3)); console.log(4);

Answer: 1 4 3 2

------------------------------------------------------------------------

### Q8: Why do Promises execute before setTimeout?

Because Promise callbacks go to the microtask queue, which has higher
priority.

------------------------------------------------------------------------

## 5. Advanced Interview Questions

### Q9: If JavaScript is single-threaded, how does Node.js handle concurrency?

Node uses: - Event Loop - libuv thread pool (default 4 threads) -
Offloads I/O operations to background threads

JavaScript code itself still runs on a single main thread.

------------------------------------------------------------------------

### Q10: What is Event Loop Starvation?

When microtasks keep scheduling new microtasks, preventing macrotasks
from executing.

Example:

function loop() { Promise.resolve().then(loop); } loop();

setTimeout(() =\> console.log("Hello"), 0);

"Hello" never executes.

------------------------------------------------------------------------

### Q11: What causes Call Stack Overflow?

Infinite recursion without a base condition.

------------------------------------------------------------------------

### Q12: How does async/await work internally?

It is syntactic sugar over Promises. When await is encountered: -
Function pauses - Returns a Promise - Continuation is added to microtask
queue

------------------------------------------------------------------------

## 6. Node.js Event Loop Phases (Senior Level)

1.  Timers
2.  Pending Callbacks
3.  Idle / Prepare
4.  Poll
5.  Check
6.  Close Callbacks

Important difference: process.nextTick runs before Promise microtasks in
Node.js.

------------------------------------------------------------------------

## 7. JavaScript vs Multithreaded Languages (e.g., Java)

JavaScript: - Single-threaded - No race conditions on main thread - Uses
event-driven concurrency

Java: - Multi-threaded - True parallel execution - Requires
synchronization

------------------------------------------------------------------------

## 8. Common Tricky Output Question

console.log("A"); setTimeout(() =\> console.log("B"), 0);

(async () =\> { console.log("C"); await Promise.resolve();
console.log("D"); })();

console.log("E");

Answer: A C E D B

------------------------------------------------------------------------

## 9. Performance & Best Practices

To avoid blocking:

-   Use Web Workers (Browser)
-   Use Worker Threads (Node)
-   Break heavy loops into chunks
-   Use streaming for large data
-   Avoid long synchronous loops

------------------------------------------------------------------------

## Final Summary

JavaScript is:

-   Single-threaded (one call stack)
-   Non-blocking (via Event Loop)
-   Concurrent (via async delegation)
-   Not parallel by default
-   Can achieve parallelism using Workers

Mastering the Event Loop and task prioritization is critical for
interviews.
