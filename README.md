# JavaScript_Working


First of all, JavaScript is a High - Level Programming language. created for interaction with web pages

There are some steps which js follow for run its code

The first step is we , write the code of JS in a file

uske baad vo code parsing phase mein jata hai , jha prr 2 tarah ki parsing hoti hai one is Lexical parsing and second is Syntax parsing

after that hume AST Abstract Syntax Tree milta hai

av execution mein aata hai compilation phase, jisme pehle to AST Bytecode mein convert hota hai , interpreter code execute krta hai and JIT compiler Jo code ko optimize tarike se compile krta hai

after that execution phase jisme code execute hota hai , call stack ki help se issi phase mein Global execution context execute hota hai and after that output milta hai


# Execution Context

## What is Execution Context?

Execution context - It is an enviroment where js code will run , it has two parts:

1. Memory creation phase
2. Execution phase

---

## Types of Execution Context

### Global Execution Context

Global Execution context - It is the first execution context which will created and it represent the whole code of a file in execution context.

---

### Function Execution Context

Function execution context - Every function has its own Execution context.

---

## Execution Context mein hota kya hai?

sabse pehle pura code scan hota hai then jitne bhi memory allocation chahiye code ko vo saari memory milti hai, after that line by line code execute hota hai.

That's why hoisting is performed.

---

## Example

```js
console.log(a)
var a = 2;
```

iss code mein sabse pehle jitne bhe memory decalreation hai vo saare Memory creation wale context mein declare ho jayenge after that code execute hoga, to memroy to allocate ho gyi aur default value undefined hoti hai to console.log mein a ki value undefined hogi.

# Parsing

## Let's talk about Parsing --

### Lexical Parsing

Lexical parsing - Isme JS ka code jo hai uske tokens bnaye jaate hai.

### Example

```js
const total = 5 + 10;
```

Tokens:

```json
[
  { "type": "Keyword",    "value": "const" },
  { "type": "Identifier", "value": "total" },
  { "type": "Punctuator", "value": "=" },
  { "type": "Numeric",    "value": "5" },
  { "type": "Punctuator", "value": "+" },
  { "type": "Numeric",    "value": "10" },
  { "type": "Punctuator", "value": ";" }
]
```

---

### Syntax Parsing

after that second parsing jo hai vo hai Syntax parsing jo ki syntax check krti hai aur tokens se AST tree create krke deta hai.

---

## AST

fir parsing ke baad hume AST Abstract Syntax Tree milta hai jisme code ki related saari cheeze hoti hai.

# Compilation and JIT Compiler

Av AST milne ke baad humara ye AST code ko Bytecode mein convert kiya jaata hai.

---

## Compilation ke time pe kya hota hai?

js ka engine use krta hai JIT compilation (Just in time compilation).
Sabse pehle interpreter bytecode ko execute krega aur hot code ko JIT observe krke machine code mein convert krr dega

---

## JIT Compiler

ye kya krta hai ki ye hot code ko compile krke machine code mein convert krr deta hai.

### Hot Code

Hot code - esa piece of code jo bhot baar run kre.

---

## JIT ka Working

JIT code ko observe krke uss mein se hot code ko compile krta hai and baki code ko interpreter ke through run krwata hai.

# Asynchronous Operations in JavaScript

Hum jaante hain ki JavaScript code ko execute karne ke liye **Call Stack** use karti hai.

Lekin problem tab aati hai jab koi aisa kaam aa jaye jiska execution time hume pehle se pata nahi hota, jaise:

- API call karna
- User ki location access karna
- Timer lagana (`setTimeout`)
- File read karna

Agar JavaScript khud in tasks ko execute karne lage, to poora code tab tak ruk jayega jab tak ye task complete na ho jaye.

## Web APIs

Browser JavaScript ko kuch extra functionalities provide karta hai jinhe **Web APIs** kaha jaata hai.

Web APIs JavaScript ko advanced features use karne ki capability deti hain, jaise:

- Location access karna
- API requests bhejna
- Timers chalana
- DOM events handle karna

## Kaise Kaam Karta Hai?

Jab Call Stack mein koi asynchronous task aata hai, to JavaScript us task ko execute karne ke liye **Web API** ko de deti hai.

Web API us task ko background mein handle karti rehti hai, aur tab tak JavaScript apna baaki synchronous code execute karti rehti hai.

### Flow

1. Asynchronous task Call Stack mein aata hai.
2. Task Web API ko handover kar diya jaata hai.
3. Call Stack apna baaki code execute karta rehta hai.
4. Jab Web API apna kaam complete kar leti hai, to result ko Queue mein daal diya jaata hai.
5. **Event Loop** continuously check karta rehta hai:
   - Kya Call Stack empty hai?
   - Kya Queue mein koi task pending hai?
6. Agar Call Stack empty ho aur Queue mein task ho, to Event Loop us task ko Queue se utha kar Call Stack mein push kar deta hai.
7. Phir woh task execute ho jaata hai.

## Types of Queues

JavaScript mein mainly do tarah ki queues hoti hain:

### 1. Microtask Queue

Is queue mein generally:

- Promise callbacks (`.then()`, `.catch()`, `.finally()`)
- `queueMicrotask()`
- Mutation Observer callbacks

store hote hain.

### 2. Macrotask Queue (Callback Queue)

Is queue mein generally:

- `setTimeout`
- `setInterval`
- DOM Events
- Location APIs
- Other Web API callbacks

store hote hain.

## Priority

**Microtask Queue ki priority Macrotask Queue se zyada hoti hai.**

Jab bhi Call Stack empty hota hai:

1. Pehle saare Microtasks execute kiye jaate hain.
2. Uske baad Macrotask Queue ke tasks execute hote hain.

Isliye Promise callbacks aksar `setTimeout` se pehle execute hote hain, chahe timeout `0ms` hi kyu na ho.

## Summary

- JavaScript single-threaded hai.
- Code execute karne ke liye Call Stack use hota hai.
- Time-consuming tasks Web APIs handle karti hain.
- Completed tasks Queue mein jaate hain.
- Event Loop Queue aur Call Stack ko manage karta hai.
- Microtask Queue ki priority Macrotask Queue se zyada hoti hai.
