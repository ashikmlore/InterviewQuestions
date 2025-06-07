
#### 1. What is the event loop in Node.js? How does it work?
Answer:
The event loop allows Node.js to perform non-blocking I/O operations despite being single-threaded. It offloads operations to the system kernel whenever possible.

Phases:
Timers
Pending callbacks
Idle/prepare
Poll
Check
Close callbacks

Example:
```bash
setTimeout(() => console.log('timeout'), 0);
setImmediate(() => console.log('immediate'));
```
Output:
```bash
immediate
timeout
```

#### 2. What are microtasks and macrotasks in Node.js?
Answer:
Microtasks: Processed after the current operation completes and before returning control to the event loop.
Macrotasks: Scheduled in various phases of the event loop.

Microtasks: process.nextTick(), Promise.then()
Macrotasks: setTimeout(), setImmediate()

Example:

```bash 
setTimeout(() => console.log('timeout'));
Promise.resolve().then(() => console.log('promise'));
process.nextTick(() => console.log('nextTick'));
```
Output:
```bash
nextTick
promise
timeout
```

#### 3. Why is Node.js single-threaded, and how does it handle concurrency?
Answer:
Node.js uses a single thread for JavaScript execution but leverages libuv’s thread pool for I/O operations. This allows it to handle many connections simultaneously.

#### 4. What is libuv?
Answer:
Libuv is a C library that abstracts asynchronous I/O operations using the event loop, thread pool, and handles filesystem, TCP, UDP, etc.

#### 5. How does Node.js handle child processes?
Answer:
Using child_process module: spawn, exec, fork.

``` bash
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh', '/usr']);
ls.stdout.on('data', data => console.log(`Output: ${data}`));
🧵 Asynchronous Programming
```

#### 6. Difference between process.nextTick() and setImmediate()?
Answer:

nextTick(): Runs before any I/O.

setImmediate(): Runs after I/O.

#### 7. How to handle errors in async/await?
Answer:
``` bash
try {
  const result = await someAsyncFunc();
} catch (error) {
  console.error('Error:', error);
}
```

#### 8. What is the difference between callback, promise, and async/await?
Answer:

Callback: Traditional async pattern, prone to callback hell.

Promise: Cleaner, chainable.

Async/Await: Looks synchronous, easier to read.

#### 9. How does util.promisify work?
Answer:
Converts a callback-based function to return a Promise.
```bash
const fs = require('fs');
const util = require('util');
const readFile = util.promisify(fs.readFile);

readFile('file.txt', 'utf-8').then(console.log);
```

### 10. What is a race condition? How do you prevent it in Node.js?
Answer:
Occurs when two or more operations run concurrently and lead to unexpected results. Prevent using locks, mutexes, or queues (e.g., async library).


🧠 Advanced Concepts
#### 11. What is a memory leak? How to detect it in Node.js?
Answer:
Unreleased memory due to forgotten references.

Tools: heapdump, clinic, Chrome DevTools.

```bash
const heapdump = require('heapdump');
heapdump.writeSnapshot('./snapshot.heapsnapshot');
```

#### 12. What is the use of cluster module?
Answer:
It allows you to create child processes that share the same server port.

``` bash
const cluster = require('cluster');
if (cluster.isMaster) {
  cluster.fork();
} else {
  require('http').createServer((req, res) => res.end('Worker')).listen(3000);
}
```

#### 13. Explain stream backpressure and how to handle it.
Answer:
When writable stream cannot process incoming data fast enough, it's called backpressure.

Handle using: drain event.
```bash
const fs = require('fs');
const stream = fs.createReadStream('input.txt');
const out = fs.createWriteStream('output.txt');
stream.pipe(out);
```

#### 14. What are different types of streams in Node.js?
Answer:
Readable
Writable
Duplex
Transform

#### 15. Explain middleware in Express.
Answer:
Middleware functions are functions with access to req, res, and next.

```bash
app.use((req, res, next) => {
  console.log('Logging...');
  next();
});
```

⚙️ Performance & Optimization
#### 16. How do you improve performance in Node.js apps?
Answer:

Use async APIs

Use clustering

Reduce synchronous code

Stream large files

Cache results (e.g., Redis)

#### 17. How do you profile Node.js applications?
Answer:
Using:

--inspect

Chrome DevTools

clinic.js

v8-profiler

#### 18. How to manage large numbers of concurrent requests?
Answer:

Use clustering

Use load balancers

Optimize DB queries

Use message queues

#### 19. Difference between synchronous and asynchronous code in Node.js?
Answer:
Synchronous blocks the thread. Asynchronous uses callbacks/promises and is non-blocking.

#### 20. How to debug memory usage in Node.js?
Answer:
Use:

process.memoryUsage()

Chrome DevTools

heapdump

🧰 Modules & Tools

#### 21. Difference between require and import in Node.js?
Answer:

require: CommonJS

import: ES Module

ES Modules require .mjs or "type": "module" in package.json.

#### 22. What is the role of exports and module.exports?
Answer:
exports is a shorthand to module.exports. Assigning directly to exports can break linkage.

#### 23. What are global objects in Node.js?
Answer:
global, process, Buffer, __dirname, __filename

#### 24. What is the purpose of package-lock.json?
Answer:
Locks exact version of installed dependencies for consistency across environments.

#### 25. What is the difference between dependencies and devDependencies?
Answer:

dependencies: Required for runtime.

devDependencies: Only for development (e.g., test libraries).

🔐 Security
#### 26. How do you prevent SQL Injection in Node.js?
Answer:
Use parameterized queries or ORM/ODM (like Sequelize or Mongoose).

#### 27. How to handle user input securely in Express?
Answer:

Validate inputs

Sanitize data

Use helmet for HTTP headers

#### 28. What is CSRF and how to prevent it?
Answer:
CSRF forces authenticated users to submit a request.
Prevent via:

CSRF tokens

SameSite cookies

#### 29. What is XSS and how to prevent it?
Answer:
Cross-Site Scripting.
Prevent by:

Escaping HTML

Using helmet

Validating inputs

#### 30. How to store passwords securely in Node.js?
Answer:
Use bcrypt or argon2 to hash passwords before saving.
```bash
const bcrypt = require('bcrypt');
const hash = await bcrypt.hash(password, 10);
```

🧪 Testing

#### 31. How to test asynchronous code in Node.js?
Answer:
Use async/await in test functions or pass done().

```bash
it('should return data', async () => {
  const data = await fetchData();
  assert(data);
});
```

#### 32. What are mocking and stubbing?
Answer:

Mock: Fake object/function

Stub: Replaces real implementation

Use libraries like sinon, jest.

#### 33. How to use supertest with Express?

```bash
const request = require('supertest');
const app = require('./app');

request(app)
  .get('/route')
  .expect(200)
  .then(response => console.log(response.body));
```

#### 34. What is the difference between unit and integration tests?
Answer:

Unit: Test single function/component

Integration: Test multiple units working together

#### 35. How to achieve 100% test coverage?
Answer:

Use nyc, jest, or mocha

Write tests for all branches and edge cases

📡 Networking & APIs
#### 36. How to implement rate limiting in Express?
```bash
const rateLimit = require('express-rate-limit');
app.use(rateLimit({ windowMs: 15 * 60 * 1000, max: 100 }));
```

#### 37. How to implement file uploads in Node.js?
Answer:
Use multer middleware.

#### 38. Difference between REST and GraphQL?
Answer:

REST: Fixed endpoints

GraphQL: Flexible queries and types

#### 39. How do you secure an API in Node.js?
Answer:

Use JWTs

HTTPS

API keys

Rate limiting

Input validation

#### 40. How to stream data to clients?
Answer:
Using response stream:

```bash
res.write('data chunk');
res.end();
```

🧬 Misc & Internals
#### 41. What is process.env?
Answer:
Accesses environment variables.

#### 42. What is the purpose of process.exit()?
Answer:
Ends the Node.js process.

#### 43. How do you handle uncaught exceptions?
Answer:
```bash
process.on('uncaughtException', err => {
  console.error(err);
  process.exit(1);
});
```

#### 44. How to log performance in Node.js?
Answer:
Use console.time(), performance.now(), or perf_hooks.

#### 45. How to share state between modules?
Answer:
Use singletons, global variables, or dependency injection.

🧾 Design Patterns
#### 46. What is middleware chaining in Express?
Answer:
Sequential execution of functions using next().

#### 47. Explain the factory pattern in Node.js.
Answer:
Encapsulates object creation logic.
```bash
function userFactory(name) {
  return { name, role: 'user' };
}
```

#### 48. What is the singleton pattern in Node.js?
Answer:
Same instance shared across modules.

```bash
module.exports = new Config();
```

#### 49. How to implement caching in Node.js?
Answer:

In-memory: node-cache

External: Redis

#### 50. How to build scalable architecture in Node.js?
Answer:

Use microservices

Employ message brokers (e.g., RabbitMQ)

Horizontal scaling via clustering/load balancer

Containerize with Docker

