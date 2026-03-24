# Node.js Internals Interview Questions

## 🔹 Basics

### 1. What is Node.js?
- Explain that Node.js is a runtime built on V8
- Runs JavaScript outside the browser

### 2. Is Node.js single-threaded or multi-threaded?
- JS execution is single-threaded
- Internally uses multi-threading (libuv, worker threads)

---

## 🔹 Event Loop

### 3. What is the Event Loop?
- Mechanism that handles async callbacks
- Moves tasks from queue to call stack

### 4. How does the Event Loop work?
- Call stack executes sync code
- Async tasks go to APIs/libuv
- Callback queue processed by event loop

### 5. What are the phases of the Event Loop?
- Timers
- I/O callbacks
- Idle/prepare
- Poll
- Check
- Close callbacks

### 6. Difference between microtasks and macrotasks?
- Microtasks: Promise.then, queueMicrotask
- Macrotasks: setTimeout, setImmediate

---

## 🔹 libuv

### 7. What is libuv?
- C library used by Node.js
- Handles async I/O and event loop

### 8. What problems does libuv solve?
- Non-blocking I/O
- Cross-platform async behavior

### 9. What operations does libuv handle?
- File system
- DNS
- Networking

---

## 🔹 Thread Pool

### 10. What is the thread pool in Node.js?
- Pool of worker threads (default 4)

### 11. Which operations use the thread pool?
- fs
- crypto
- zlib
- dns.lookup

### 12. Can thread pool size be changed?
- Yes using UV_THREADPOOL_SIZE

### 13. What happens if thread pool is overloaded?
- Tasks queue up
- Performance degrades

---

## 🔹 Blocking vs Non-Blocking

### 14. What is blocking code?
- Code that stops the event loop

### 15. Give example of blocking operation
- Large loops
- CPU-heavy calculations

### 16. Why does CPU-heavy code block Node.js?
- Runs on main thread
- No offloading to libuv

---

## 🔹 Worker Threads

### 17. What are Worker Threads?
- Enable parallel JS execution

### 18. When should you use Worker Threads?
- CPU-intensive tasks

### 19. How do Worker Threads communicate?
- parentPort.postMessage

### 20. Is memory shared between workers?
- No (by default)

### 21. How can memory be shared?
- SharedArrayBuffer + Atomics

### 22. What is workerData?
- Data passed from main thread to worker

### 23. Are Worker Threads expensive?
- Yes (new V8 instance, memory cost)

---

## 🔹 Worker Threads vs Thread Pool

### 24. Difference between Worker Threads and Thread Pool?

| Feature | Worker Threads | Thread Pool |
|--------|---------------|------------|
| Runs JS | Yes | No |
| Use case | CPU tasks | I/O tasks |
| Control | Manual | Automatic |

---

## 🔹 Practical Scenario

### 25. Why did the blocking route freeze the server?
- CPU loop blocked main thread

### 26. How did Worker Threads fix it?
- Moved computation off main thread

### 27. Why did multiple workers improve performance?
- Parallel execution across CPU cores

### 28. What is Promise.all used for in workers?
- Wait for all workers to finish

---

## 🔹 Advanced

### 29. What is a Worker Pool?
- Reusing workers instead of creating new ones

### 30. Difference between Worker Threads and Clustering?
- Workers: threads
- Clustering: multiple processes

### 31. When would you use clustering?
- Scaling server across CPU cores

### 32. What are common mistakes with Worker Threads?
- Creating too many workers
- Using for I/O tasks

---

## 🔹 Bonus (Tricky Questions)

### 33. Can libuv thread pool execute JavaScript?
- No

### 34. Why is Node.js still fast if single-threaded?
- Non-blocking I/O

### 35. What happens if main thread is blocked?
- Entire app becomes unresponsive

---

## ✅ Quick Summary

- Event Loop handles execution
- libuv handles async I/O
- Thread pool handles blocking I/O tasks
- Worker Threads handle CPU-heavy tasks
- Use the right tool for the right problem

