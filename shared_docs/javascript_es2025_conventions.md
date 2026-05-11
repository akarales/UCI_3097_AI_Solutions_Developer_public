# JavaScript ES2025 — Conventions & Style Reference

> Based on the **ECMAScript 2025 (ES2025)** specification — the 16th edition, approved by the 129th ECMA General Assembly on **June 25, 2025**.

---

## Table of Contents

1. [Naming Conventions](#1-naming-conventions)
2. [Variable Declarations — `const`, `let`, `var`](#2-variable-declarations--const-let-var)
3. [Indentation, Line Length & Formatting](#3-indentation-line-length--formatting)
4. [Blank Lines & Whitespace](#4-blank-lines--whitespace)
5. [Comments & JSDoc](#5-comments--jsdoc)
6. [Functions — Declarations, Expressions & Arrows](#6-functions--declarations-expressions--arrows)
7. [Classes & OOP Patterns](#7-classes--oop-patterns)
8. [Modules — Import & Export](#8-modules--import--export)
9. [ES2025 — Import Attributes (JSON Modules)](#9-es2025--import-attributes-json-modules)
10. [ES2025 — Iterator Helpers](#10-es2025--iterator-helpers)
11. [ES2025 — Set Methods](#11-es2025--set-methods)
12. [ES2025 — `Promise.try()`](#12-es2025--promisetry)
13. [ES2025 — `RegExp.escape()` & Pattern Modifiers](#13-es2025--regexpescape--pattern-modifiers)
14. [ES2025 — Duplicate Named Capture Groups](#14-es2025--duplicate-named-capture-groups)
15. [ES2025 — `Float16Array`](#15-es2025--float16array)
16. [Async / Await & Promises](#16-async--await--promises)
17. [Destructuring & Spread](#17-destructuring--spread)
18. [Error Handling](#18-error-handling)
19. [Expressions & Operators](#19-expressions--operators)
20. [Tooling](#20-tooling)
21. [Quick Reference Cheat Sheet](#21-quick-reference-cheat-sheet)

---

## 1. Naming Conventions

JavaScript uses **camelCase** for most identifiers — the opposite of Python's snake_case. This is one of the most important things to internalize when switching between the two languages.

### 1.1 Variables & Functions — `camelCase`

```js
// CORRECT
const userName = 'Alex';
const totalCount = 42;
const isAuthenticated = true;
let retryAttempts = 0;

function calculateTotalPrice(basePrice, taxRate) {
  return basePrice * (1 + taxRate);
}

const getUserById = (userId) => fetch(`/api/users/${userId}`);

// WRONG — snake_case is not JavaScript convention
const user_name = 'Alex';
function calculate_total_price() {}
```

### 1.2 Classes & Constructors — `PascalCase`

```js
// CORRECT
class UserAccount {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
}

class HttpRequestHandler {}
class SmartContractClient {}
class AIEmbeddingModel {}

// WRONG
class userAccount {}      // camelCase — wrong for classes
class user_account {}     // snake_case — wrong for classes
```

### 1.3 Constants — `UPPER_SNAKE_CASE`

Only for true compile-time / module-level constants. Regular `const` bindings that are not conceptually constant still use `camelCase`.

```js
// CORRECT — true constants
const MAX_CONNECTIONS = 100;
const DEFAULT_TIMEOUT_MS = 30_000;
const API_BASE_URL = 'https://api.example.com';
const GAS_LIMIT_WEI = 21_000n;

// Regular const — still camelCase (not truly "constant" in nature)
const userConfig = loadConfig();   // camelCase — this is a runtime value
const results = [];                // camelCase — mutable contents, const binding
```

### 1.4 Private Class Fields — `#camelCase`

```js
class SecureVault {
  #masterKey;        // Private field — # prefix is enforced by the language
  #connectionPool;

  constructor(key) {
    this.#masterKey = key;
  }

  #deriveSubKey(salt) {   // Private method
    return crypto.subtle.deriveBits({ name: 'HKDF', salt }, this.#masterKey, 256);
  }
}
```

### 1.5 Acronyms in Names

```js
// Treat acronyms like regular words in camelCase / PascalCase
const userId = 42;           // NOT: userID
const apiUrl = '...';        // NOT: APIUrl or apiURL
const htmlParser = {};       // NOT: HTMLParser
class XmlBuilder {}          // NOT: XMLBuilder

// At the start of a name — still lowercase for camelCase
const jsonPayload = {};      // NOT: JSONPayload
const httpClient = {};       // NOT: HTTPClient
```

### 1.6 Boolean Variables — Prefix with `is`, `has`, `can`, `should`

```js
// CORRECT — boolean naming that reads naturally
const isLoading = true;
const hasPermission = false;
const canRetry = attempts < MAX_RETRIES;
const shouldRefresh = tokenAge > TOKEN_TTL;

// WRONG — ambiguous
const loading = true;
const permission = false;
```

### 1.7 Event Handlers — Prefix with `on` or `handle`

```js
// CORRECT
function onSubmit(event) {}
function handleClick(event) {}
const onMessageReceived = (msg) => {};

// Common React / UI convention
<button onClick={handleClick}>Submit</button>
```

### 1.8 Avoid

```js
// Never use reserved words or ambiguous single letters outside loops
let l = 10;    // BAD — ambiguous
let O = {};    // BAD — looks like zero

// Acceptable single-letter names
for (let i = 0; i < 10; i++) {}      // i, j, k — loop counters
array.forEach((x) => process(x));    // x, y — math or trivial transforms
const add = (a, b) => a + b;         // a, b — short pure functions
```

---

## 2. Variable Declarations — `const`, `let`, `var`

### 2.1 Prefer `const` by Default

```js
// CORRECT — use const for anything that won't be reassigned
const API_URL = 'https://api.example.com';
const user = { name: 'Alex', role: 'admin' };  // object ref is const, contents mutable
const items = [];                               // array ref is const

// CORRECT — use let only when reassignment is needed
let retryCount = 0;
let currentPage = 1;

while (hasMore) {
  retryCount++;
  currentPage = fetchNextPage();
}

// NEVER use var — it is function-scoped, hoisted, and causes subtle bugs
var x = 10;   // BAD — avoid in all modern JavaScript
```

### 2.2 One Declaration Per Line

```js
// CORRECT
const firstName = 'Alex';
const lastName = 'Smith';
const age = 30;

// WRONG
const firstName = 'Alex', lastName = 'Smith', age = 30;
```

### 2.3 Declare Close to First Use

```js
// CORRECT — declare where the variable is first needed
function processUsers(users) {
  const active = users.filter((u) => u.isActive);

  for (const user of active) {
    const displayName = `${user.first} ${user.last}`;
    console.log(displayName);
  }
}
```

---

## 3. Indentation, Line Length & Formatting

### 3.1 Indentation — 2 Spaces (JavaScript Ecosystem Convention)

```js
// CORRECT — 2 spaces (standard across most JS style guides and tooling)
function greet(name) {
  if (name) {
    return `Hello, ${name}!`;
  }
  return 'Hello, stranger!';
}

// Some teams use 4 spaces — pick one and stay consistent within a project
```

### 3.2 Semicolons — Always (recommended) or Never (ASI-reliant)

```js
// STYLE A — always use semicolons (most common, safer)
const x = 10;
const y = 20;
const sum = x + y;

// STYLE B — omit semicolons (relies on Automatic Semicolon Insertion)
const x = 10
const y = 20
const sum = x + y

// ASI GOTCHA — always use semicolons if unsure
const a = 1
const b = 2
[a, b].forEach(console.log)   // Parsed as: const b = 2[a, b].forEach(...)  — BUG
```

### 3.3 Quotes — Single or Double (pick one and be consistent)

```js
// Single quotes — default in most JS style guides (Airbnb, Google)
const name = 'Alex';
const url = 'https://api.example.com';

// Double quotes — common in JSON-heavy codebases and JSX
const message = "Hello, World!";

// Template literals — always for interpolation and multi-line strings
const greeting = `Hello, ${name}!`;
const multiLine = `
  This is a
  multi-line string.
`;

// WRONG — mixing quote styles without reason
const bad = 'hello";
```

### 3.4 Line Length

```js
// Target: 80–100 characters per line
// Break long chains with one method per line
const result = largeArray
  .filter((item) => item.isActive)
  .map((item) => item.value * 2)
  .reduce((acc, val) => acc + val, 0);

// Break long function signatures
function createUserAccount(
  username,
  email,
  passwordHash,
  role = 'user',
  metadata = {},
) {
  // ...
}

// Break long ternaries
const label = isAuthenticated
  ? 'Welcome back!'
  : 'Please log in';
```

### 3.5 Trailing Commas

```js
// CORRECT — trailing commas make diffs cleaner
const config = {
  host: 'localhost',
  port: 3000,
  debug: true,   // trailing comma — valid in ES5+
};

const names = [
  'Alice',
  'Bob',
  'Carol',   // trailing comma
];

function register(
  name,
  email,
  role,   // trailing comma in params — valid in ES2017+
) {}
```

---

## 4. Blank Lines & Whitespace

```js
// Two blank lines between top-level declarations (optional but common)
import { readFile } from 'fs/promises';


const MAX_RETRIES = 3;


async function fetchData(url) {
  // One blank line between logical sections inside a function
  const response = await fetch(url);
  const data = await response.json();

  if (!data.success) {
    throw new Error(data.message);
  }

  return data.result;
}


class DataService {
  constructor(config) {
    this.config = config;
  }

  // One blank line between class methods
  async getData(id) {
    return fetch(`${this.config.baseUrl}/${id}`);
  }

  async postData(payload) {
    return fetch(this.config.baseUrl, {
      method: 'POST',
      body: JSON.stringify(payload),
    });
  }
}
```

```js
// Spaces around operators
const total = price + tax;
const isValid = count > 0 && count < MAX;

// No spaces before function call parentheses
doSomething();    // CORRECT
doSomething ();   // WRONG

// Space after keywords
if (condition) {}     // CORRECT
if(condition) {}      // WRONG

while (running) {}    // CORRECT
for (const item of items) {}   // CORRECT
```

---

## 5. Comments & JSDoc

### 5.1 Single-Line Comments

```js
// Retrieve the user's JWT from local storage
const token = localStorage.getItem('auth_token');

// WRONG — stating the obvious
const x = x + 1;  // add 1 to x
```

### 5.2 Block Comments

```js
/*
 * This module handles wallet connection and signing.
 * It supports EIP-1193 provider injection and WalletConnect v2.
 */
```

### 5.3 JSDoc — Document Public APIs

```js
/**
 * Verifies an ECDSA signature against a message and public key.
 *
 * @param {Uint8Array} message - The original message bytes.
 * @param {Uint8Array} signature - The DER-encoded signature.
 * @param {CryptoKey} publicKey - The signer's public key.
 * @returns {Promise<boolean>} True if the signature is valid.
 * @throws {TypeError} If any argument has an incorrect type.
 *
 * @example
 * const isValid = await verifySignature(msgBytes, sigBytes, key);
 */
async function verifySignature(message, signature, publicKey) {
  return crypto.subtle.verify('ECDSA', publicKey, signature, message);
}

/**
 * @typedef {Object} UserRecord
 * @property {number} id - Unique user identifier.
 * @property {string} username - The user's handle.
 * @property {string} email - The user's email address.
 * @property {boolean} isActive - Whether the account is active.
 */

/**
 * Fetches a user record by ID.
 *
 * @param {number} userId
 * @returns {Promise<UserRecord>}
 */
async function getUserById(userId) {
  const res = await fetch(`/api/users/${userId}`);
  return res.json();
}
```

---

## 6. Functions — Declarations, Expressions & Arrows

### 6.1 When to Use Each Form

```js
// Function declarations — use for named, top-level, hoistable functions
function processPayment(amount, currency) {
  return { amount, currency, timestamp: Date.now() };
}

// Arrow functions — use for callbacks, short helpers, lexical `this`
const double = (n) => n * 2;
const add = (a, b) => a + b;

const users = rawData.map((u) => ({
  id: u.user_id,
  name: `${u.first} ${u.last}`,
}));

// Regular function expressions — use when you need `arguments` or dynamic `this`
const handler = function namedFn(event) {
  console.log(event.type);
};
```

### 6.2 Arrow Function Syntax

```js
// Single param — parentheses optional (many style guides require them for consistency)
const double = (n) => n * 2;   // PREFERRED — consistent
const double = n => n * 2;     // also valid

// No params — empty parens required
const getRandom = () => Math.random();

// Multi-line — use braces and explicit return
const formatUser = (user) => {
  const full = `${user.first} ${user.last}`;
  return { ...user, displayName: full };
};

// Returning an object literal — wrap in parens to avoid parse ambiguity
const toPoint = (x, y) => ({ x, y });   // CORRECT
const toPoint = (x, y) => { x, y };     // WRONG — parsed as block body
```

### 6.3 Default Parameters

```js
// CORRECT — use default parameters, not || inside the body
function createConfig(host = 'localhost', port = 3000, debug = false) {
  return { host, port, debug };
}

// WRONG — fragile (treats falsy values as missing)
function createConfig(host, port, debug) {
  host = host || 'localhost';   // BAD — '' would be replaced too
  port = port || 3000;          // BAD — 0 would be replaced too
}
```

### 6.4 Rest & Spread in Functions

```js
// Rest parameters — always last
function logAll(prefix, ...messages) {
  messages.forEach((msg) => console.log(`[${prefix}] ${msg}`));
}

logAll('INFO', 'Server started', 'Listening on port 3000');

// Spread — pass array elements as individual arguments
const numbers = [1, 5, 3, 9, 2];
const max = Math.max(...numbers);   // 9
```

---

## 7. Classes & OOP Patterns

```js
class Animal {
  // Public field declarations (ES2022+)
  name;
  sound;

  // Private fields (enforced by the runtime)
  #heartRate = 60;

  constructor(name, sound) {
    this.name = name;
    this.sound = sound;
  }

  speak() {
    return `${this.name} says ${this.sound}`;
  }

  get heartRate() {
    return this.#heartRate;
  }

  set heartRate(bpm) {
    if (bpm < 20 || bpm > 300) throw new RangeError('Invalid heart rate');
    this.#heartRate = bpm;
  }

  // Static factory method
  static fromJSON({ name, sound }) {
    return new Animal(name, sound);
  }
}


class Dog extends Animal {
  #tricks = [];

  constructor(name) {
    super(name, 'woof');
  }

  learn(trick) {
    this.#tricks.push(trick);
    return this;   // fluent / builder pattern
  }

  perform() {
    return this.#tricks.map((t) => `${this.name} performs: ${t}`);
  }
}

const rex = new Dog('Rex');
rex.learn('sit').learn('shake').learn('roll over');
console.log(rex.perform());
// ['Rex performs: sit', 'Rex performs: shake', 'Rex performs: roll over']
```

---

## 8. Modules — Import & Export

### 8.1 Named Exports (preferred for most cases)

```js
// math.js
export const PI = 3.14159;

export function add(a, b) {
  return a + b;
}

export class Calculator {
  // ...
}

// Consuming
import { PI, add, Calculator } from './math.js';
```

### 8.2 Default Exports (one per file, for the primary export)

```js
// UserService.js
export default class UserService {
  async getUser(id) { /* ... */ }
}

// Consuming — any name works
import UserService from './UserService.js';
import Users from './UserService.js';   // also valid but inconsistent
```

### 8.3 Re-exports & Barrels

```js
// index.js — barrel file aggregates exports from a module folder
export { default as UserService } from './UserService.js';
export { add, multiply } from './math.js';
export * from './validators.js';

// Consuming the barrel
import { UserService, add } from './services/index.js';
```

### 8.4 Dynamic Imports

```js
// Lazy-load a heavy module only when needed
async function loadChart() {
  const { Chart } = await import('./chart.js');
  return new Chart();
}

// Conditional loading
if (featureFlags.enableAnalytics) {
  const analytics = await import('./analytics.js');
  analytics.init();
}
```

---

## 9. ES2025 — Import Attributes (JSON Modules)

Import attributes provide the syntax foundation for importing non-JavaScript files. The first artifact officially supported is **JSON modules**.

```js
// Static JSON import — no fetch, no fs.readFile, no build step needed
import appConfig from './config.json' with { type: 'json' };

console.log(appConfig.version);    // Direct property access
console.log(appConfig.apiUrl);

// Dynamic JSON import with attributes
const locale = await import(`./locales/${lang}.json`, {
  with: { type: 'json' },
});

console.log(locale.default.greeting);

// Practical use — environment-specific config
const env = process.env.NODE_ENV ?? 'development';
const config = await import(`./config.${env}.json`, {
  with: { type: 'json' },
});
```

> The `with` keyword is designed to be extensible — future editions may add other module attribute types beyond `json`.

---

## 10. ES2025 — Iterator Helpers

ES2025 adds chainable lazy helper methods directly to iterators, similar to array methods but without materializing intermediate arrays. Ideal for large data sets and generator pipelines.

### 10.1 Available Methods

| Method | Description |
|--------|------------|
| `.map(fn)` | Transform each value |
| `.filter(fn)` | Keep values that pass the predicate |
| `.reduce(fn, init)` | Fold into a single value |
| `.flatMap(fn)` | Map and flatten one level |
| `.take(n)` | Take only the first n values |
| `.drop(n)` | Skip the first n values |
| `.find(fn)` | Return first matching value |
| `.some(fn)` | True if any value passes |
| `.every(fn)` | True if all values pass |
| `.forEach(fn)` | Side-effect iteration |
| `.toArray()` | Materialize to a standard array |

### 10.2 Examples

```js
// Generator — produces an infinite sequence
function* naturals(start = 1) {
  let n = start;
  while (true) yield n++;
}

// Chain helpers lazily — nothing is computed until .toArray() or .forEach()
const firstFiveEvenSquares = naturals()
  .filter((n) => n % 2 === 0)    // keep evens
  .map((n) => n * n)             // square each
  .take(5)                       // stop after 5 values
  .toArray();

console.log(firstFiveEvenSquares);  // [4, 16, 36, 64, 100]

// Working with existing iterables
const sentence = 'ECMAScript 2025 is great';

const longWords = sentence
  .split(' ')
  .values()              // convert array to iterator
  .filter((w) => w.length > 4)
  .map((w) => w.toUpperCase())
  .toArray();

console.log(longWords);  // ['ECMASCRIPT', '2025', 'GREAT']

// Pipeline that doesn't materialize an array until needed
function* readLines(text) {
  yield* text.split('\n');
}

const errorCount = readLines(logOutput)
  .filter((line) => line.startsWith('ERROR'))
  .reduce((count) => count + 1, 0);

console.log(`Total errors: ${errorCount}`);

// Drop and take — useful for pagination over generators
const page2 = naturals()
  .drop(20)   // skip first 20
  .take(10)   // take next 10
  .toArray(); // [21, 22, 23, ..., 30]
```

---

## 11. ES2025 — Set Methods

ES2025 adds mathematical set operations natively to `Set`, eliminating the need for manual loops or libraries like lodash.

```js
const frontend = new Set(['Alice', 'Bob', 'Carol']);
const backend = new Set(['Bob', 'Dave', 'Eve']);
const devops = new Set(['Carol', 'Frank']);

// union — all members across both sets
const allEngineers = frontend.union(backend);
// Set { 'Alice', 'Bob', 'Carol', 'Dave', 'Eve' }

// intersection — members in both sets
const fullStack = frontend.intersection(backend);
// Set { 'Bob' }

// difference — in this set but NOT in the argument set
const frontendOnly = frontend.difference(backend);
// Set { 'Alice', 'Carol' }

// symmetricDifference — in either set but NOT in both
const unique = frontend.symmetricDifference(backend);
// Set { 'Alice', 'Carol', 'Dave', 'Eve' }

// isSubsetOf — is every element of this set in the other?
const small = new Set(['Bob', 'Carol']);
small.isSubsetOf(frontend);    // true

// isSupersetOf — does this set contain all elements of the other?
frontend.isSupersetOf(small);  // true

// isDisjointFrom — do the two sets share NO elements?
frontend.isDisjointFrom(devops);  // false — Carol is in both
backend.isDisjointFrom(devops);   // true — no overlap

// Practical example — permission system
const userRoles = new Set(['editor', 'viewer']);
const requiredRoles = new Set(['admin', 'editor']);

const hasAccess = !userRoles.isDisjointFrom(requiredRoles);  // true
```

---

## 12. ES2025 — `Promise.try()`

`Promise.try()` wraps a function in a promise safely — whether the function is synchronous or asynchronous, throws synchronously or rejects. Eliminates the common pattern of wrapping sync code in `new Promise()` or `async` wrappers.

```js
// Before ES2025 — verbose and error-prone
function safeRun(fn) {
  try {
    return Promise.resolve(fn());
  } catch (err) {
    return Promise.reject(err);
  }
}

// ES2025 — Promise.try() handles both sync throws and async rejections
const result = await Promise.try(() => {
  return JSON.parse(rawInput);   // If this throws, Promise.try() catches it
});

// Async function — also works
const data = await Promise.try(async () => {
  const res = await fetch('/api/data');
  return res.json();
});

// Practical — consistent error handling regardless of sync/async
function processInput(input) {
  return Promise.try(() => validateAndTransform(input))   // might throw sync
    .then(storeToDatabase)                                // async step
    .catch((err) => logError(err));                       // single catch handles all
}

// Route handler pattern
app.get('/data', (req, res) => {
  Promise.try(() => requireAuth(req))            // sync auth check
    .then(() => fetchUserData(req.user.id))      // async data fetch
    .then((data) => res.json(data))
    .catch((err) => res.status(500).json({ error: err.message }));
});
```

---

## 13. ES2025 — `RegExp.escape()` & Pattern Modifiers

### 13.1 `RegExp.escape()`

Safely escapes any string for use as a literal match inside a regex. Prevents regex injection — the regex equivalent of SQL injection.

```js
// Before ES2025 — error-prone manual escaping
function escapeRegex(str) {
  return str.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');   // easy to miss characters
}

// ES2025 — built-in, complete, reliable
const userQuery = 'price: $10.00 (sale)';
const safe = RegExp.escape(userQuery);
// 'price:\\ \\$10\\.00\\ \\(sale\\)'

const regex = new RegExp(safe, 'i');
const found = catalogText.match(regex);

// Security use case — prevent injection in dynamic regex construction
function searchInContent(rawUserInput, content) {
  const safePattern = RegExp.escape(rawUserInput);
  return new RegExp(safePattern, 'gi').test(content);
}
```

### 13.2 Pattern Modifiers — `(?flags:pattern)`

Change regex flags mid-pattern without applying them to the entire expression.

```js
// Make just part of a regex case-insensitive
const pattern = /Hello (?i:world)/;
pattern.test('Hello WORLD');   // true
pattern.test('HELLO world');   // false — 'Hello' part is still case-sensitive

// Disable a flag for part of the pattern
const strictPattern = /(?-i:EXACT) match/i;  // 'EXACT' must be uppercase, rest is case-insensitive
strictPattern.test('EXACT Match');   // true
strictPattern.test('exact Match');   // false

// Practical — parse log lines where timestamps are case-sensitive but labels are not
const logPattern = /\d{4}-\d{2}-\d{2} (?i:error|warn|info): (.+)/;
```

---

## 14. ES2025 — Duplicate Named Capture Groups

ES2025 allows the same capture group name to appear in different alternatives of a regex (separated by `|`). Previously this caused a `SyntaxError`.

```js
// Before ES2025 — forced to use different names (awkward)
const datePattern = /(?<y4>\d{4})-(?<m>\d{2})|(?<y2>\d{2})\/(?<m2>\d{2})/;

// ES2025 — reuse the same name in each alternative
const datePattern = /(?<year>\d{4})-(?<month>\d{2})|(?<year>\d{2})\/(?<month>\d{2})/;

const full = '2025-06'.match(datePattern);
console.log(full.groups.year);    // '2025'
console.log(full.groups.month);   // '06'

const short = '25/06'.match(datePattern);
console.log(short.groups.year);   // '25'
console.log(short.groups.month);  // '06'

// Practical — version string matching
const versionPattern = /ECMAScript(?<version>\d{4})|ES(?<version>\d{2})/;
'ECMAScript2025'.match(versionPattern).groups.version;  // '2025'
'ES25'.match(versionPattern).groups.version;            // '25'
```

---

## 15. ES2025 — `Float16Array`

A new TypedArray for **16-bit half-precision floating-point** numbers. Useful for WebGPU, WebGL, and ML workloads where memory is the bottleneck.

```js
// Create a Float16Array — 16-bit values use half the memory of Float32Array
const weights = new Float16Array(1024);   // 2KB instead of 4KB (Float32) or 8KB (Float64)

// DataView methods for reading/writing individual Float16 values
const buffer = new ArrayBuffer(2);
const view = new DataView(buffer);

view.setFloat16(0, 3.14);
console.log(view.getFloat16(0));   // ~3.14 (reduced precision)

// ML / GPU use case — loading model weights from a .bin file
async function loadWeights(url) {
  const response = await fetch(url);
  const buffer = await response.arrayBuffer();
  return new Float16Array(buffer);   // interpret bytes directly as fp16
}

// WebGPU upload pattern
const gpuBuffer = device.createBuffer({
  size: weights.byteLength,
  usage: GPUBufferUsage.STORAGE,
  mappedAtCreation: true,
});
new Float16Array(gpuBuffer.getMappedRange()).set(weights);
gpuBuffer.unmap();
```

---

## 16. Async / Await & Promises

### 16.1 Always `await` in `async` Functions

```js
// CORRECT
async function loadUser(id) {
  const res = await fetch(`/api/users/${id}`);

  if (!res.ok) {
    throw new Error(`HTTP ${res.status}: ${res.statusText}`);
  }

  return res.json();
}

// CORRECT — parallel fetches with Promise.all
async function loadDashboard(userId) {
  const [user, posts, notifications] = await Promise.all([
    fetchUser(userId),
    fetchPosts(userId),
    fetchNotifications(userId),
  ]);

  return { user, posts, notifications };
}

// WRONG — sequential when parallel is possible
async function loadDashboardSlow(userId) {
  const user = await fetchUser(userId);            // waits
  const posts = await fetchPosts(userId);          // waits again (unnecessary)
  const notifications = await fetchNotifications(userId);  // waits again
  return { user, posts, notifications };
}
```

### 16.2 Top-Level Await (ES2022+, stable in ES2025)

```js
// In ES modules — await is allowed at the top level
const config = await import('./config.json', { with: { type: 'json' } });
const db = await connectDatabase(config.default.dbUrl);

export { db };   // other modules importing this will wait for the connection
```

### 16.3 Error Handling in Async Code

```js
// CORRECT — try/catch in async functions
async function saveRecord(data) {
  try {
    const validated = schema.parse(data);
    await db.insert(validated);
  } catch (err) {
    if (err instanceof ValidationError) {
      throw new UserFacingError('Invalid data format', { cause: err });
    }
    throw err;   // re-throw unknown errors
  }
}

// Promise.try() for mixed sync/async pipelines (ES2025)
const result = await Promise.try(() => validateSync(input))
  .then(saveAsync)
  .catch(handleError);
```

---

## 17. Destructuring & Spread

### 17.1 Object Destructuring

```js
// Basic
const { name, email, role = 'user' } = userData;

// Rename on destructure
const { user_id: userId, created_at: createdAt } = apiResponse;

// Nested
const { address: { city, country } } = profile;

// Function parameters
function renderUser({ name, email, isActive = true }) {
  return `${name} <${email}> — ${isActive ? 'active' : 'inactive'}`;
}
```

### 17.2 Array Destructuring

```js
const [first, second, ...rest] = items;
const [, middle] = ['a', 'b', 'c'];   // skip first element

// Swap variables cleanly
let a = 1, b = 2;
[a, b] = [b, a];

// From function return
const [data, error] = await safeAsync(fetchUser(id));
```

### 17.3 Spread Operator

```js
// Merge objects (later keys win)
const merged = { ...defaults, ...overrides };

// Clone and modify
const updatedUser = { ...user, lastLogin: new Date() };

// Merge arrays
const all = [...list1, ...list2, extraItem];

// Pass array as arguments
const max = Math.max(...numbers);
```

---

## 18. Error Handling

```js
// Always extend Error for custom exceptions
class AppError extends Error {
  constructor(message, options = {}) {
    super(message, options);   // options.cause supported since ES2022
    this.name = this.constructor.name;
  }
}

class ValidationError extends AppError {
  constructor(message, field) {
    super(message);
    this.field = field;
  }
}

class NetworkError extends AppError {}

// Use cause to chain errors without losing context
try {
  const data = await fetchUserData(id);
} catch (err) {
  throw new NetworkError('Failed to load user', { cause: err });
}

// Check error type
function handleError(err) {
  if (err instanceof ValidationError) {
    return res.status(400).json({ error: err.message, field: err.field });
  }
  if (err instanceof NetworkError) {
    return res.status(502).json({ error: 'Upstream error' });
  }
  throw err;   // unknown — re-throw
}
```

---

## 19. Expressions & Operators

### 19.1 Equality — Always `===`

```js
// CORRECT — strict equality (no type coercion)
if (count === 0) {}
if (name === 'Alex') {}
if (value === null) {}

// WRONG — loose equality causes unexpected coercions
if (count == 0) {}     // '' == 0 is true
if (value == null) {}  // null == undefined is true (sometimes intentional but risky)
```

### 19.2 Null-Safe Operators

```js
// Optional chaining — safe property traversal
const city = user?.address?.city;
const len = arr?.length;
const first = getUsers()?.[0];
const result = obj?.method?.();

// Nullish coalescing — only fallback on null/undefined (not 0, '', false)
const port = config.port ?? 3000;
const name = user.displayName ?? user.username ?? 'Anonymous';

// Nullish assignment — only assign if currently null/undefined
config.timeout ??= 5000;
user.role ??= 'viewer';

// Logical assignment
user.name ||= 'Guest';     // assign if falsy
user.score &&= user.score * 2;  // assign only if currently truthy
```

### 19.3 Numeric Separators & BigInt

```js
// Numeric separators — readability for large numbers
const ONE_MILLION = 1_000_000;
const MAX_SAFE = 9_007_199_254_740_991;
const HEX_COLOR = 0xFF_EC_D8;
const BLOCK_REWARD = 6.25e0;

// BigInt — for values beyond Number.MAX_SAFE_INTEGER
const tokenSupply = 21_000_000n;
const totalWei = 1_000_000_000_000_000_000n;   // 1 ETH in Wei

// WRONG — cannot mix BigInt and Number
const bad = tokenSupply + 100;   // TypeError
const good = tokenSupply + 100n; // CORRECT
```

---

## 20. Tooling

| Tool | Purpose | Command |
|------|---------|---------|
| **ESLint** | Linting — find style and logic errors | `eslint . --fix` |
| **Prettier** | Opinionated code formatter | `prettier --write .` |
| **TypeScript** | Static type checking | `tsc --noEmit` |
| **Biome** | Fast all-in-one linter + formatter | `biome check --apply .` |
| **Vitest** | Unit testing (Vite-native) | `vitest run` |
| **Bun** | Runtime + package manager + bundler | `bun run` / `bun test` |
| **Vite** | Build tool and dev server | `vite build` |

### Recommended `eslint.config.js` (Flat Config — ESLint 9+)

```js
// eslint.config.js
import js from '@eslint/js';
import globals from 'globals';

export default [
  js.configs.recommended,
  {
    languageOptions: {
      ecmaVersion: 2025,
      sourceType: 'module',
      globals: {
        ...globals.browser,
        ...globals.node,
      },
    },
    rules: {
      'no-var': 'error',
      'prefer-const': 'error',
      'eqeqeq': ['error', 'always'],
      'no-console': 'warn',
      'no-unused-vars': ['error', { argsIgnorePattern: '^_' }],
      'prefer-arrow-callback': 'error',
      'object-shorthand': 'error',
      'no-param-reassign': 'error',
    },
  },
];
```

### Recommended `prettier.config.js`

```js
// prettier.config.js
export default {
  semi: true,
  singleQuote: true,
  trailingComma: 'all',
  printWidth: 100,
  tabWidth: 2,
  arrowParens: 'always',
};
```

---

## 21. Quick Reference Cheat Sheet

### Naming Rules

| Identifier Type | Convention | Example |
|----------------|-----------|---------|
| Variable | `camelCase` | `userName`, `totalCount` |
| Function | `camelCase` | `getUser()`, `calculateTax()` |
| Class / Constructor | `PascalCase` | `UserAccount`, `HttpClient` |
| Constant (module-level) | `UPPER_SNAKE_CASE` | `MAX_RETRIES`, `API_KEY` |
| Private class field | `#camelCase` | `#masterKey`, `#cache` |
| Boolean variable | `is/has/can/should` prefix | `isLoading`, `hasPermission` |
| Event handler | `on/handle` prefix | `onSubmit`, `handleClick` |
| Enum-like object | `UPPER_SNAKE_CASE` or `PascalCase` | `Direction.UP`, `STATUS.ACTIVE` |

### ES2025 Highlights

| Feature | What it Adds |
|---------|-------------|
| Import Attributes | `import data from './f.json' with { type: 'json' }` |
| Iterator Helpers | `.map()`, `.filter()`, `.take()`, `.drop()`, `.toArray()` on any iterator |
| Set Methods | `.union()`, `.intersection()`, `.difference()`, `.isSubsetOf()`, etc. |
| `Promise.try()` | Unified sync + async error handling in a promise chain |
| `RegExp.escape()` | Safely escape user strings for use in dynamic regex |
| Regex Pattern Modifiers | `(?i:pattern)` — change flags mid-expression |
| Duplicate Named Groups | Reuse capture group names across `|` alternatives |
| `Float16Array` | 16-bit floating-point TypedArray for GPU/ML workloads |

### `const` vs `let` vs `var`

| Keyword | Scope | Hoisting | Reassign | Use |
|---------|-------|---------|---------|-----|
| `const` | Block | No (TDZ) | No | Default for everything |
| `let` | Block | No (TDZ) | Yes | When reassignment is needed |
| `var` | Function | Yes | Yes | Never — legacy only |

---

*Reference: [ECMAScript 2025 Specification](https://tc39.es/ecma262/2025/) | [TC39 Finished Proposals](https://github.com/tc39/proposals/blob/main/finished-proposals.md) | [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript) | Approved June 25, 2025*
