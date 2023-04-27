# Elements Code Style Guide

This style guide outlines the coding conventions and guidelines that we follow for Elements. These conventions help ensure that our code is consistent, readable, and maintainable.

## Table of Contents

- [Code Conventions](#code-conventions)
    - [Whitespaces](#whitespaces)
    - [Arrays](#arrays)
    - [Interfaces](#interfaces)
    - [Strings](#strings)
    - [Classes & Components](#classes--components)
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
>3.1 Do not use "I" as a prefix for interface names.
```typescript
//bad
interface ICar {}

//good
interface CarInterface {}
//or
interface Car {}
```
>3.2 Use PascalCase for interface names
```typescript
//bad
interface userProfileInterface {}

//good
interface UserProfileInterface {}
```
>3.3 Use whole words in names when possible
```typescript
//bad
interface DmEditorInterface {}

//good
interface DiagramEditorInterface {}
```
>3.4 Use camelCase for interface members
```typescript
//bad
interface CarInterface {
    last_service: '20.05.2020';
    first_owner: 'John';
}

//good
interface CarInterface {
    lastService: '20.05.2020';
    firstOwner: 'John';
}
```
>3.5 Use separate interface instead of explicit describe entity when the interface can be used in several places
```typescript
//bad
const entity: {property1: string; property2: number};
//bad
subscribe((entity: {property1: string; property2: number}) => entity);


interface EntityInterface {
    property1: string;
    property2: number;
}

//good
const entity: EntityInterface;

//good
subscribe((entity: EntityInterface) => entity);
```

## Strings
>4.1 When programmatically building up strings, use template strings instead of concatenation
```javascript
//bad
const myUrl = endPoint + '/create';

//bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

//good
const myUrl = `${endPoint}/create`;

//good
function sayHi(name) {
  return `How are you ${name}?`;
}
```
>4.2 Use single quotes ' for strings
```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// good
const name = 'Capt. Janeway';
```

## Classes & Components
>5.1 It is unnecessary to provide an empty constructor or one that simply delegates into its parent class because ES2015 provides a default class constructor if one is not specified. However constructors with parameter properties, visibility modifiers or parameter decorators should not be omitted even if the body of the constructor is empty.
```typescript
//bad
class Car {
    constructor() {}
  
    getInfo() {
        return this.info;
    }
}

//good
class Car {
  getInfo() {
    return this.info;
  }
}

//good
class DefaultConstructor {}

//good
class ParameterProperties {
  constructor(private myService) {}
}

//good
class ParameterDecorators {
  constructor(@SideEffectDecorator myService) {}
}

//good
class NoInstantiation {
  private constructor() {}
}
```
>5.2 Remove unused lifecycle hooks

```typescript
//bad
class Component implements OnInit {
  name: string;

  constructor(private dep1) {}
  //This method is unused and you should remove it
  ngOnInit() {}
  
  getName() {
      return 'name';
  }
}

//good 
class Component implements OnInit {
  name: string;

  constructor(private dep1) {}
  
  ngOnInit() {
      this.initData();
  }

  getName() {
    return 'name';
  }
}
```
>5.3 If a class member is not a parameter, initialize it where it's declared, which sometimes lets you drop the constructor entirely.
```typescript
//bad
class Foo {
  private readonly userList: string[];
  
  constructor() {
    this.userList = [];
  }
}

//good
class Foo {
  private readonly userList: string[] = [];
}
```
>5.4 Don't use public access modifier for properties because, In TypeScript by default all the members (properties and methods) of a class are public
```typescript
//bad
class Student {
  //Name is public by deafult
  public name: string;
}

//good
class Student {
  name: string;
}
```
>5.5 Try to find some common methods in our codebase first, if there is one that you need, inject the service or extend a base class in your class

```typescript
//bad
class SomeComponent {
  // The method can exist in some service or base class
  calculateDistance() {
    return 44;
  }
}

//good
class CalculationService {
  calculateDistance() {
    return 44;
  }
}

class SomeComponent {
  constructor(private calculationService: CalculationService) {}
  
  getDistanceResult() {
      this.calculationService.calculateDistance();
  }
}

//or
class BaseCalculate {
  calculateDistance() {
    return 44;
  }
}

class SomeComponent extends BaseCalculate {
  getDistanceResult() {
    this.calculateDistance();
  }
}
```
>5.6 Consider creating base component if you have common functionality in several components
```typescript
//bad
//Component1 template:
//<button (click)='getInfo()'></button>

class Component1 {
  name: string;
  type: string;

  getInfo() {
    return `${this.name} ${this.type}`
  }
}
//Component2 template:
//<button (click)='getInfo()'></button>
class Component2 {
  name: string;
  type: string;

  getInfo() {
    return `${this.name} ${this.type}`
  }
}

//good
class BaseComponent {
  protected abstract name: string;
  protected abstract type: string;

  getInfo() {
    return `${this.name} ${this.type}`
  }
}

//Component1 template:
//<button (click)='getInfo()'></button>
class Component1 extends BaseComponent {
  readonly name = 'name1';
  readonly type = 'type1';
}

//Component2 template:
//<button (click)='getInfo()'></button>
class Component2 extends BaseComponent {
  readonly name = 'name2';
  readonly type = 'type2';
}
```

## Comparison operators and equality

[Insert your information about Comparison operators and equality]

## Naming conventions

[Insert information about Naming conventions]

## Using observables with new practise

[Insert information about Using observables with new practise. Can be removed]

## Creating Modules with standalone logic

[Insert information about Creating Modules with standalone logic]

