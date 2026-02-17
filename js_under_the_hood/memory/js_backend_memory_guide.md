# JavaScript & Node.js Memory & Performance Guide

---

# 🟢 Level 1 – Basics (Easy)

## Stack vs Heap
| Feature | Stack | Heap |
|---------|-------|------|
| Stores | Execution context, primitives | Objects, arrays, closures |
| Size | Small | Large, dynamic |
| Cleaning | Auto when function returns | Managed by GC |
| Risk | Stack Overflow | Memory Leak |

## Garbage Collection
- Automatic removal of unreachable objects
- Objects **not reachable from root** → deleted
- **Mark-and-Sweep** algorithm
- Young objects → fast cleanup (Minor GC)
- Old objects → major GC

---

# 🟡 Level 2 – Event Loop & Async (Intermediate)

## Tick
- One full iteration of Event Loop
- Steps:
  1. Run Call Stack
  2. Microtasks (Promises)
  3. process.nextTick callbacks
  4. setImmediate callbacks

## process.nextTick vs setImmediate
| Feature | nextTick | setImmediate |
|---------|---------|-------------|
| Timing | Before I/O | After I/O, next tick |
| Use Case | Immediate, critical | Heavy, post-I/O tasks |
| Risk | Can starve Event Loop | Safe |

---

# 🟠 Level 3 – Backend Performance Patterns (Advanced)

## 1. Worker Threads
- Solve CPU-intensive tasks without blocking Event Loop
- Each thread has its own Event Loop
- Example: image processing, encryption

```js
const { Worker } = require("worker_threads");
```

## 2. Streams
- Read/write files in chunks
- Avoid loading entire data into memory
- Scalable for large files (GBs)

```js
const fs = require("fs");
fs.createReadStream("bigfile.txt").pipe(res);
```

---

# 🔴 Level 4 – Memory Optimization (Senior)

## Generational GC
- **New Space** → Minor GC → Scavenge (Copying)
- **Old Space** → Major GC → Mark-Sweep/Mark-Compact
- Objects surviving multiple Minor GC → promotion to Old Space

## WeakMap / WeakRef
- WeakMap keys weak → GC can collect
- WeakRef → weak reference, safe caching

```js
const cache = new WeakMap();
cache.set(userObject, Date.now());
```

---

# 🟣 Level 5 – Practical Backend Insights

## Memory Leak
- Heap objects not released
- Causes:
  - Closures holding big data
  - Event listeners not removed
  - setInterval without clear
- Result: slow performance, eventual Out of Memory

## Stack Overflow
- Stack small → uncontrolled recursion
- Immediate crash

## Performance & Scalability
- Understanding Engine → better API performance
- Reduce GC overhead
- Non-blocking, scalable servers

---

# 🟣 Level 6 – Senior-Level Insights

- Event Loop internals → Ticks, microtasks, macrotasks
- Worker Threads → parallel CPU tasks
- Streams → memory-efficient file/data handling
- WeakMap / WeakRef → safe caching
- GC behavior → optimize heap usage
- Node.js optimization patterns → responsive, scalable

---

# ✅ Summary Diagram (Mental Flow)
```
[Frontend/Backend Code]
        |
        v
   [Call Stack] <- recursion -> Stack Overflow
        |
        v
   [Heap] <- objects/closures -> GC cleans -> Memory Leak if referenced
        |
        v
[Event Loop Ticks] -> process.nextTick -> microtasks -> setImmediate -> I/O
        |
        v
[Worker Threads] (CPU-intensive) -> keep main loop responsive
        |
        v
[Streams] -> memory-efficient file/data handling
        |
        v
[WeakMap / WeakRef] -> safe caching without leaks
```

---

# 💬 Interview Questions & Answers

### Basics
**1. Explain the difference between Stack and Heap in JavaScript.**
- Stack stores execution contexts and primitives, is fast, small, and LIFO. Heap stores objects, arrays, closures, is dynamic, and managed by GC.

**2. What is Garbage Collection? How does Mark-and-Sweep work?**
- Garbage Collection automatically removes unreachable memory. Mark-and-Sweep marks all reachable objects and sweeps unmarked objects as garbage.

**3. What is the difference between Memory Leak and Stack Overflow?**
- Memory Leak: memory grows gradually because unreachable objects are still referenced. Stack Overflow: immediate crash due to call stack exceeding its size (usually from uncontrolled recursion).

### Event Loop
**4. Explain what a Tick is in Node.js.**
- A tick is one full iteration of the Event Loop, processing one macrotask and all associated microtasks.

**5. Compare `process.nextTick()` and `setImmediate()`.**
- `nextTick`: runs before I/O, within current tick, used for critical immediate code. `setImmediate`: runs after current I/O, in the next tick, used for heavy tasks without blocking.

**6. How does the Event Loop handle microtasks vs macrotasks?**
- Microtasks (Promises, process.nextTick) run after the current stack but before the next macrotask. Macrotasks (setTimeout, setImmediate, I/O) run in the next tick.

### Performance & Optimization
**7. How do Worker Threads help with CPU-intensive tasks?**
- They run tasks in parallel threads with separate Event Loops, keeping the main thread responsive.

**8. How would you use Streams to handle large files efficiently?**
- Streams read/write data in chunks without loading the entire file into memory, reducing heap usage and improving performance.

**9. Explain the difference between Minor GC (Scavenge) and Major GC (Mark-Sweep/Mark-Compact).**
- Minor GC cleans the New Space using Scavenge (copying live objects). Major GC cleans Old Space using Mark-Sweep or Mark-Compact.

**10. How can WeakMap and WeakRef help prevent memory leaks?**
- WeakMap keys are weak references; GC can collect them when no other references exist. WeakRef allows weak references to objects for memory-sensitive caching.

**11. What strategies would you use to avoid memory leaks in a Node.js backend?**
- Remove event listeners, clear intervals, avoid large closures holding unnecessary data, use WeakMap/WeakRef for caches, monitor heap usage.

**12. How does understanding V8 engine internals help in writing scalable backend code?**
- Understanding heap, stack, GC, and Event Loop allows writing memory-efficient, non-blocking, and high-performance backend code that scales under load.

---

# 🔹 Notes
- Practice reading heap snapshots in Chrome DevTools or Node.js --inspect.  
- Experiment with Worker Threads and Streams for large-scale backend tasks.  
- Understand how closures and references affect memory retention.

