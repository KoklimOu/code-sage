Got it! You’re referring to the **three common ways** of defining functions in JavaScript:

1. **Function Declaration (Function Declaration Notation)**
2. **Function Expression (Function as a Value)**
3. **Arrow Function**

Let's go over these three types in detail:

### 1. **Function Declaration (Function Declaration Notation)**
A **function declaration** defines a named function and is hoisted (i.e., you can call the function before it is defined in the code).

#### Syntax:
```javascript
function functionName(parameters) {
  // Function body
  return value;
}
```

#### Example:
```javascript
function greet(name) {
  return `Hello, ${name}`;
}

console.log(greet('John')); // Output: Hello, John
```

**Characteristics**:
- **Hoisting**: Function declarations are hoisted, meaning you can call the function before it is defined in the code.
- It must have a function name.
- Best used when you want to define a reusable function that can be called anywhere in the scope.

#### Hoisting Example:
```javascript
console.log(greet('John')); // Output: Hello, John

function greet(name) {
  return `Hello, ${name}`;
}
```

---

### 2. **Function Expression (Function as a Value)**
A **function expression** defines a function as a value and is assigned to a variable. Function expressions are not hoisted, so they cannot be used before their definition.

#### Syntax:
```javascript
const variableName = function(parameters) {
  // Function body
  return value;
};
```

#### Example:
```javascript
const greet = function(name) {
  return `Hello, ${name}`;
};

console.log(greet('John')); // Output: Hello, John
```

**Characteristics**:
- **No hoisting**: Function expressions are not hoisted, so you can only call them after they are defined.
- Can be anonymous (does not require a function name).
- Can be used as a value (passed as arguments or returned from other functions).

#### No Hoisting Example:
```javascript
console.log(greet('John')); // Error: greet is not defined

const greet = function(name) {
  return `Hello, ${name}`;
};
```

---

### 3. **Arrow Function**
An **arrow function** is a more concise syntax for writing function expressions. It does not have its own `this` context, making it different from regular functions. Arrow functions are not hoisted.

#### Syntax:
```javascript
const variableName = (parameters) => {
  // Function body
  return value;
};
```

#### Example:
```javascript
const greet = (name) => `Hello, ${name}`;

console.log(greet('John')); // Output: Hello, John
```

**Characteristics**:
- **No `this` context**: Arrow functions inherit `this` from their surrounding scope, making them useful for scenarios where `this` needs to remain consistent.
- Concise syntax: If the function body contains just a single expression, the `return` keyword can be omitted.
- No hoisting: Like function expressions, arrow functions are not hoisted.

#### Example with `this` context:
```javascript
function Person() {
  this.name = 'John';
  setTimeout(() => {
    console.log(this.name); // Arrow function inherits `this` from Person
  }, 1000);
}

const person = new Person(); // Output: John after 1 second
```

---

### Key Differences:

| Feature                        | **Function Declaration**             | **Function Expression**              | **Arrow Function**                    |
|---------------------------------|--------------------------------------|--------------------------------------|---------------------------------------|
| **Hoisting**                    | Yes                                 | No                                   | No                                    |
| **Syntax**                      | `function functionName()`            | `const variableName = function()`    | `const variableName = () => {}`       |
| **Requires Function Name**      | Yes                                 | No                                   | No                                    |
| **`this` Binding**              | Dynamic (`this` is based on caller)  | Dynamic (`this` is based on caller)  | Lexical (`this` is inherited from parent scope) |
| **Use Case**                    | Reusable, hoisted functions          | Anonymous functions, first-class     | Concise functions, no own `this`      |

Each type of function has its own use case, and depending on the situation (e.g., the need for `this`, hoisting, or concise syntax), you can choose the best approach for defining a function.