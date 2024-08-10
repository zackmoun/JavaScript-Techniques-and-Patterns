# JavaScript Techniques and Patterns

Welcome to the **JavaScript Techniques and Patterns** repository! This document covers various programming techniques and design patterns that can help you write cleaner, more maintainable, and efficient JavaScript code.

## Table of Contents

1. [Guard Clauses](#guard-clauses)
2. [Modularization](#modularization)
3. [DRY (Don't Repeat Yourself)](#dry-dont-repeat-yourself)
4. [KISS (Keep It Simple, Stupid)](#kiss-keep-it-simple-stupid)
5. [YAGNI (You Ain’t Gonna Need It)](#yagni-you-aint-gonna-need-it)
6. [Separation of Concerns](#separation-of-concerns)
7. [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
8. [Immutability](#immutability)
9. [Chaining](#chaining)
10. [Error Handling with Try/Catch](#error-handling-with-trycatch)
11. [Higher-Order Functions](#higher-order-functions)
12. [Debouncing and Throttling](#debouncing-and-throttling)
13. [Currying](#currying)

## Guard Clauses

Guard clauses are a technique used to simplify complex functions by handling edge cases and special conditions early in the function. This reduces the need for deeply nested `if` statements and keeps the main logic of the function clean and readable.

### Example:

```javascript
function processOrder(order) {
    if (!order) return;
    if (order.status !== 'pending') return;
    if (!order.items || order.items.length === 0) return;

    // Main logic
    order.items.forEach(item => console.log(`Processing item: ${item.name}`));
    order.status = 'processed';
}
```

## Modularization

Modularization involves breaking down large codebases into smaller, self-contained modules or functions, each with a single responsibility. This approach promotes code reusability and easier maintenance.

### Example:

```javascript
// moduleA.js
export function add(a, b) {
    return a + b;
}

// moduleB.js
import { add } from './moduleA';
console.log(add(2, 3)); // 5
```

## DRY (Don't Repeat Yourself)

The DRY principle emphasizes reducing code duplication by abstracting repeated logic into reusable functions or modules. This minimizes maintenance overhead and potential bugs.

### Example:

```javascript
function calculateDiscount(price, discount) {
    return price * (1 - discount);
}

const priceA = calculateDiscount(100, 0.1);
const priceB = calculateDiscount(200, 0.1);
```

## KISS (Keep It Simple, Stupid)

The KISS principle encourages writing code in the simplest way possible. Avoid unnecessary complexity to improve readability and maintainability.

### Example:

```javascript
// Complex and unnecessary
const result = isAvailable ? true : false;

// Simple and clear
const result = isAvailable;
```

## YAGNI (You Ain’t Gonna Need It)

YAGNI suggests that you should not add functionality until it is necessary. Avoid writing code for features that might be needed in the future, focusing instead on the current requirements.

### Example:

```javascript
function processData(data) {
    // Regular processing code
}
```

## Separation of Concerns

Separation of Concerns involves dividing your code into distinct sections, each handling a specific aspect of the application (e.g., data management, UI rendering, business logic).

### Example:

```javascript
// Data layer
function fetchData() {
    return fetch('/api/data').then(response => response.json());
}

// Business logic
function processData(data) {
    return data.map(item => item.value * 2);
}

// UI layer
function renderData(data) {
    const element = document.getElementById('output');
    element.textContent = JSON.stringify(data);
}
```

## Single Responsibility Principle (SRP)

SRP states that a function or module should have only one reason to change, meaning it should be responsible for only one task.

### Example:

```javascript
function validateOrder(order) {
    // Validation logic
}

function applyDiscount(order) {
    // Discount logic
}

function finalizeOrder(order) {
    // Finalization logic
}
```

## Immutability

Immutability means avoiding direct modification of objects or arrays. Instead, create new objects or arrays with the updated values to prevent unintended side effects.

### Example:

```javascript
// Mutating an array
const array = [1, 2, 3];
array.push(4); // Mutates the original array

// Immutable approach
const newArray = [...array, 4]; // Creates a new array
```

## Chaining

Chaining allows you to call multiple methods on an object in a single statement, making your code more concise and readable.

### Example:

```javascript
const numbers = [1, 2, 3, 4, 5];
const result = numbers
    .filter(num => num % 2 === 0)
    .map(num => num * 2)
    .reduce((sum, num) => sum + num, 0);

console.log(result); // 12
```

## Error Handling with Try/Catch

Use `try/catch` blocks to handle errors gracefully, especially when dealing with asynchronous code or external API calls.

### Example:

```javascript
async function fetchData() {
    try {
        const response = await fetch('/api/data');
        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Fetch error:', error);
    }
}
```

## Higher-Order Functions

Higher-Order Functions are functions that take other functions as arguments or return functions as results. They are useful for creating reusable logic.

### Example:

```javascript
function withLogging(fn) {
    return function(...args) {
        console.log('Arguments:', args);
        const result = fn(...args);
        console.log('Result:', result);
        return result;
    };
}

const addWithLogging = withLogging((a, b) => a + b);
addWithLogging(2, 3); // Logs arguments and result
```

## Debouncing and Throttling

Debouncing and throttling are techniques to limit the rate at which a function is executed, especially in scenarios like user input or window resizing.

### Example:

```javascript
function debounce(fn, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => fn(...args), delay);
    };
}

const handleResize = debounce(() => {
    console.log('Window resized');
}, 300);

window.addEventListener('resize', handleResize);
```

## Currying

Currying is the process of transforming a function that takes multiple arguments into a sequence of functions that each take a single argument. This is useful for creating more flexible and reusable functions.

### Example:

```javascript
function add(a) {
    return function(b) {
        return a + b;
    };
}

const addFive = add(5);
console.log(addFive(3)); // 8
```
