# Elements Code Style Guide

This style guide outlines the coding conventions and guidelines that we follow for Elements. These conventions help ensure that our code is consistent, readable, and maintainable.

## Table of Contents

- [Code Conventions](#code-conventions)
    - [Whitespaces](#whitespaces)
    - [Arrays](#arrays)
    - [Interfaces](#interfaces)
    - [Strings](#strings)
    - [Classes & Constructors (extend shared)](#classes--constructors-extend-shared)
    - [Comparison operators and equality](#comparison-operators-and-equality)
    - [Naming conventions](#naming-conventions)
    - [Using observables with new practise](#using-observables-with-new-practise)
    - [Creating Modules with standalone logic](#creating-modules-with-standalone-logic)

## Code Conventions

### Whitespaces

Which style for whitespaces we should follow?

### Option 1:
![ray-so-export (1).png](./images/ray-so-export%20(1).png)
![ray-so-export (6).png](./images/ray-so-export%20(6).png)
![ray-so-export (12).png](./images/ray-so-export%20(12).png)
![ray-so-export (4).png](./images/ray-so-export%20(4).png)
![ray-so-export (8).png](./images/ray-so-export%20(8).png)


### Option 2: 
![ray-so-export (2).png](./images/ray-so-export%20(2).png)
![ray-so-export (7).png](./images/ray-so-export%20(7).png)
![ray-so-export (11).png](./images/ray-so-export%20(11).png)
![ray-so-export (5).png](./images/ray-so-export%20(5).png)
![ray-so-export (10).png](./images/ray-so-export%20(10).png)

### Arrays

>2.1 Use the literal syntax for array creation.
```javascript
// bad
const items = new Array();

// good
const items = [];
```
>2.2 Use Array.from instead of spread ... for mapping over iterables, because it avoids creating an intermediate array.
```javascript
// bad
const baz = [...foo].map(bar);

// good
const baz = Array.from(foo, bar);
```
>2.3 Use line breaks after open and before close array brackets if an array has multiple lines
```javascript
// bad
const arr = [
  [0, 1], [2, 3], [4, 5],
];

const objectInArray = [{
  id: 1,
}, {
  id: 2,
}];

const numberInArray = [
  1, 2,
];

// good
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [
  {
    id: 1,
  },
  {
    id: 2,
  },
];

const numberInArray = [
  1,
  2,
];
```
>2.4 Use an array to hold the values you want to check for validity
```javascript
//bad
const value1 = 'value1';
const value2 = 'value2';

if (value1 === 'someValue' || value2 === 'someValue') {
    // perform some logic
}

//good
const validValues = ['value1', 'value2'];

if (validValues.includes('someValue')) {
  // perform some logic
}
```
>2.5 Use an array to hold multiple values after the condition expression completes
```javascript
//bad
const value1 = 'foo' === 'baz' ? '1' : '2';
const value2 = 'bar' === 'baz' ? '2' : '1';

//good
const [value1, value2] = 'foo' === 'baz' 
        ? ['1', '2'] 
        : ['2', '1']
```


### Interfaces

[Insert your information about Interfaces]

## Strings

[Insert your information about Strings]

## Classes & Constructors (extend shared)

[Insert your information about Classes & Constructors (extend shared)]

## Comparison operators and equality

[Insert your information about Comparison operators and equality]

## Naming conventions

[Insert information about Naming conventions]

## Using observables with new practise

[Insert information about Using observables with new practise. Can be removed]

## Creating Modules with standalone logic

[Insert information about Creating Modules with standalone logic]

