# Elements Code Style Guide

This style guide outlines the coding conventions and guidelines that we follow for Elements. These conventions help ensure that our code is consistent, readable, and maintainable.

## Table of Contents

- [Code Conventions](#code-conventions)
    - [Whitespaces](#whitespaces)
    - [Blocks](#blocks)
    - [Arrays](#arrays)
    - [Interfaces](#interfaces)
    - [Strings](#strings)
    - [Classes & Components](#classes--components)
    - [Comparison operators and equality](#comparison-operators-and-equality)
    - [Naming conventions](#naming-conventions)
    - [Using observables](#using-observables)

## Code Conventions

### Whitespaces
>1.1 Place 1 space before the leading brace. eslint: **space-before-blocks**
```javascript
// bad
function test(){
  console.log('test');
}

// good
function test() {
  console.log('test');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog',
});
```
>1.2 Place 1 space before the opening parenthesis in control statements (if, while etc.). Place no space between the argument list and the function name in function calls and declarations. eslint: **keyword-spacing**
```javascript
// bad
if(isJedi) {
  fight ();
}

// good
if (isJedi) {
  fight();
}

// bad
function fight () {
  console.log ('Swooosh!');
}

// good
function fight() {
  console.log('Swooosh!');
}
```
>1.3 Leave a blank line after blocks and before the next statement
```javascript
// bad
if (foo) {
  return bar;
}
return baz;

// good
if (foo) {
  return bar;
}

return baz;

//bad
if (foo) {
    return bar;
}
if (baz) {
    return bar;
}

//good
if (foo) {
  return bar;
}

if (baz) {
  return bar;
}

// bad
const obj = {
  foo() {
  },
  bar() {
  },
};
return obj;

// good
const obj = {
  foo() {
  },
  
  bar() {
  },
};

return obj;

// bad
const arr = [
  function foo() {
  },
  function bar() {
  },
];
return arr;

// good
const arr = [
  function foo() {
  },

  function bar() {
  },
];

return arr;

//bad
const obj = {a:1,a:2,a:3};

//good
const obj = {a:1, a:2, a:3};

//bad
function myFunction() {
    const object1 = {name: 'obj1'};
    const object2 = {name: 'obj1'};
    const object3 = {name: 'obj1'};
    object1.age = 20;
    object2.age = 30;
    object3.age = 40;
    if (object1.age === 20) {
        return object1;
    }
    return {object1, object2, object3};
}

//good
function myFunction() {
  const object1 = {name: 'obj1'};
  const object2 = {name: 'obj1'};
  const object3 = {name: 'obj1'};
  
  object1.age = 20;
  object2.age = 30;
  object3.age = 40;
  
  if (object1.age === 20) {
    return object1;
  }
  
  return {object1, object2, object3};
}
```
>1.4 Avoid spaces before commas and require a space after commas. eslint: **comma-spacing**
```javascript
// bad
const foo = 1,bar = 2;
const arr = [1 , 2];

// good
const foo = 1, bar = 2;
const arr = [1, 2];
```
>1.5 Do not use multiple blank lines to pad your code. eslint: **no-multiple-empty-lines**
```javascript
// bad
class Person {
  constructor(fullName, email, birthday) {
    this.fullName = fullName;


    this.email = email;


    this.setAge(birthday);
  }


  setAge(birthday) {
    const today = new Date();


    const age = this.getAge(today, birthday);


    this.age = age;
  }
}

// good
class Person {
  constructor(fullName, email, birthday) {
    this.fullName = fullName;
    this.email = email;
    this.setAge(birthday);
  }

  setAge(birthday) {
    const today = new Date();
    const age = getAge(today, birthday);
    
    this.age = age;
  }
}
```
>1.6 Set off operators with spaces. eslint: **space-infix-ops**
```javascript
// bad
const x=y+5;

// good
const x = y + 5;
```
#### :arrow_up: Back to top

### Blocks
>2.1 Use braces with all multiline blocks. eslint: **nonblock-statement-body-position**
```javascript
// bad
if (test)
  return false;

// good
if (test) return false;

// good
if (test) {
  return false;
}

// bad
function foo() { return false; }

// good
function bar() {
  return false;
}
```
>2.2 If an if block always executes a return statement, the subsequent else block is unnecessary. A return in an else if block following an if block that contains a return can be separated into multiple if blocks. eslint: **no-else-return**
```javascript
// bad
function foo() {
  if (x) {
    return x;
  } else {
    return y;
  }
}

// bad
function cats() {
  if (x) {
    return x;
  } else if (y) {
    return y;
  }
}

// bad
function dogs() {
  if (x) {
    return x;
  } else {
    if (y) {
      return y;
    }
  }
}

// good
function foo() {
  if (x) {
    return x;
  }

  return y;
}

// good
function cats() {
  if (x) {
    return x;
  }

  if (y) {
    return y;
  }
}

// good
function dogs(x) {
  if (x) {
    if (z) {
      return y;
    }
  } else {
    return z;
  }
}
```

### Arrays

>3.1 Use the literal syntax for array creation.
```javascript
// bad
const items = new Array();

// good
const items = [];
```
>3.2 Use Array.from instead of spread ... for mapping over iterables, because it avoids creating an intermediate array.
```javascript
// bad
const baz = [...foo].map(bar);

// good
const baz = Array.from(foo, bar);
```
>3.3 Use line breaks after open and before close array brackets if an array has multiple lines
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
>3.4 Use an array to hold the values you want to check for validity
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
>3.5 Use an array to hold multiple values after the condition expression completes
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
>4.1 Do not use "I" as a prefix for interface names.
```typescript
//bad
interface ICar {}

//good
interface CarInterface {}
//or
interface Car {}
```
>4.2 Use PascalCase for interface names
```typescript
//bad
interface userProfileInterface {}

//good
interface UserProfileInterface {}
```
>4.3 Use whole words in names when possible
```typescript
//bad
interface DmEditorInterface {}

//good
interface DiagramEditorInterface {}
```
>4.4 Use camelCase for interface members
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
>4.5 Use separate interface instead of explicit describe entity when the interface can be used in several places
```typescript
//bad
const entity1: {property1: string; property2: number};
//bad
subscribe((entity: {property1: string; property2: number}) => entity);


interface EntityInterface {
    property1: string;
    property2: number;
}

//good
const entity2: EntityInterface;

//good
subscribe((entity: EntityInterface) => entity);
```

## Strings
>5.1 When programmatically building up strings, use template strings instead of concatenation
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
>5.2 Use single quotes ' for strings
```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// good
const name = 'Capt. Janeway';
```

## Classes & Components
>6.1 It is unnecessary to provide an empty constructor or one that simply delegates into its parent class because ES2015 provides a default class constructor if one is not specified. However constructors with parameter properties, visibility modifiers or parameter decorators should not be omitted even if the body of the constructor is empty.
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
>6.2 Remove unused lifecycle hooks

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

//good
class Component {
  name: string;

  constructor(private dep1) {}

  getName() {
    return 'name';
  }
}
```
>6.3 If a class member is not a parameter, initialize it where it's declared, which sometimes lets you drop the constructor entirely.
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
>6.4 Don't use public access modifier for properties because, In TypeScript by default all the members (properties and methods) of a class are public
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
>6.5 Try to find some common methods in our codebase first, if there is one that you need, inject the service or extend a base class in your class

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
>6.6 Consider creating base component if you have common functionality in several components
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
>7.1 Conditional statements such as the if statement evaluate their expression using coercion with the ToBoolean abstract method and always follow these simple rules:

1) Objects evaluate to true. Empty array also evaluates to true because it's object under the hood
2) Undefined evaluates to false
3) Null evaluates to false
4) Booleans evaluate to the value of the boolean
5) Numbers evaluate to false if +0, -0, or NaN, otherwise true
6) Strings evaluate to false if an empty string '', otherwise true

>7.2 Ternaries should not be nested and generally be single line expressions
```javascript
// bad
const foo = maybe1 > maybe2
  ? "bar"
  : value1 > value2 ? "baz" : null;

// split into 2 separated ternary expressions
const maybeNull = value1 > value2 ? 'baz' : null;

// better
const foo = maybe1 > maybe2
  ? 'bar'
  : maybeNull;

// best
const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
```

>7.3 Use Ternaries over if expression when you need to assign some value to variable
```javascript
//bad
let age;

if (name === 'John') {
    age = 20;
} else {
    age = 10;
}

//good
const age = name === 'John' ? 20 : 10;
```
>7.4 Avoid unneeded ternary statements
```javascript
// bad
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;
const quux = a != null ? a : b;

// good
const foo = a || b;
const bar = !!c;
const baz = !c;
const quux = a ?? b;
```
>7.5 Use shortcuts
```javascript
// bad
if (name !== '') {
  // ...stuff...
}

// good
if (name) {
  // ...stuff...
}

// bad
if (collection.length > 0) {
  // ...stuff...
}

// good
if (collection.length) {
  // ...stuff...
}
```

## Naming conventions
>9.1 Avoid shortcuts for variable, propertie or function names. Be descriptive with your naming
```javascript
// bad
function rD() {
  // ...
}
const diagramD = 'value1';

// good
function requirementDetails() {
  // ...
}
const diagramDependencies = 'value1';

//bad
var prsn = {
  n: "Joe Schmoe",
  e: "ihrtabbrv8ing@silly.com"
}

//good
var person = {
  name: "Joe Hero",
  email: "jhero@example.com"
}

```
>9.2 Use camelCase when naming objects, functions, and instances. eslint: camelcase
```javascript
// bad
const OBJEcttsssss = {};
const this_is_my_object = {};
function c() {}
function goHome() {}

// good
const thisIsMyObject = {};
function createNewDependency() {}
function goToMainApp() {}
```
>9.3 Use PascalCase only when naming constructors or classes. eslint: new-cap
```javascript
// bad
function user(options) {
  this.name = options.name;
}

const bad = new user({
  name: 'nope',
});

// good
class User {
  constructor(options) {
    this.name = options.name;
  }
}

const good = new User({
  name: 'yup',
});

function User(options) {
    //...stuff
}
```
>9.4 Use camelCase when you export-default a function. Your filename should be identical to your function’s name
```javascript
function makeStyleGuide() {
  // ...
}

export default makeStyleGuide;
```
>9.5 Use PascalCase when you export a constructor / class / singleton / function library / bare object
```javascript
const Config = {
  es6: {
  },
};

export default Config;
```
>9.6 Acronyms and initialisms should always be all uppercased, or all lowercased. Why? Names are for readability, not to appease a computer algorithm.
```javascript
// bad
import SmsContainer from './containers/SmsContainer';

// bad
const HttpRequests = [
  // ...
];

// good
import SMSContainer from './containers/SMSContainer';

// good
const HTTPRequests = [
  // ...
];

// also good
const httpRequests = [
  // ...
];

// best
import TextMessageContainer from './containers/TextMessageContainer';

// best
const requests = [
  // ...
];
```
>9.7 If your file exports a single class, your filename should be exactly the name of the class
```javascript
// file contents
class CheckBox {
// ...
}
export default CheckBox;

// in some other file
// bad
import CheckBox from './checkBox';

// bad
import CheckBox from './check_box';

// good
import CheckBox from './CheckBox';
```

## Using observables
>9.1 Use camelCase and $ sign for variables that hold observable
```typescript
//bad
const myObservable = someSource$.pipe(
        map(data => data.someProperty),
        filter(value => value > 0),
        debounceTime(500)
);

//good
const myObservable$ = someSource$.pipe(
  map(data => data.someProperty),
  filter(value => value > 0),
  debounceTime(500)
);
```
>9.2 Use the async pipe in templates to subscribe to an Observable and automatically unsubscribe when the component is destroyed.
```typescript
//bad
class Component1 implements OnInit {
  data: any;
  readonly myObservable$ = from([]);
  
  ngOnInit() {
      // should also unsubscribe from the observable
      this.myObservable$.subscribe(data => this.data = data)
  }
}
// Component1 template:
// <div *ngIf='data'>{{data}}</div>

//good
class Component1 {
    readonly myObservable$ = from([]);
}
// Component1 template:
// <div *ngIf='myObservable$ | async as data'>{{data}}</div>
```
>9.3 Do not use too much logic in subscribe. Consider to create separate method
```typescript
//bad
this.queryParamsSubscription = this.route.queryParams
        .subscribe((params: any) => {
          this.refModelService.fetchNodePath(this.refModel._id, params.node).subscribe();

          if (this.isMakingNodeRoot) {
            this.isMakingNodeRoot = false;
            this.store.set('rootData', this.selectedNode);
            const selectedNodeAttachments = this.store.selectedNodeAttachments;
            if (this.selectedNode._id !== this.refModel._id && !selectedNodeAttachments.loading
                    && this.selectedNode._id === selectedNodeAttachments.nodeId) {
              this.updateTreeService.set('updateNodeInTree', {
                value: this.attachmentsService.getLinksNumber(selectedNodeAttachments),
                property: 'links',
                nodeId: this.selectedNode._id
              });
            }
          }
        });

//good
this.queryParamsSubscription = this.route.queryParams.subscribe(
    (params: any) => this.processMakeRootNode(params)
);
```

