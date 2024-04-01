# Elements Code Style Guide

This style guide outlines the coding conventions and guidelines that we follow for Elements. These conventions help ensure that our code is consistent, readable, and maintainable.

<a id='table-of-contents'></a>
## Table of contents
- [Code Conventions](#code-conventions)
    - [Whitespaces](#whitespaces)
    - [Blocks](#blocks)
    - [Arrays](#arrays)
    - [Objects](#objects)
    - [Destructuring](#destructuring)
    - [Interfaces](#interfaces)
    - [Strings](#strings)
    - [Classes & Components](#classes--components)
    - [Comparison operators and equality](#comparison-operators-and-equality)
    - [Naming conventions](#naming-conventions)
    - [Functions](#functions)
    - [Arrow functions](#arrow-functions)
    - [Using observables](#using-observables)
    - [Async pipes](#async-pipes)
    - [Imports](#imports)
    - [Braces](#braces)
    - [Using external libs](#using-external-libs)

## Code Conventions

### Whitespaces
>1.1 Place 1 space before the leading brace. eslint: `space-before-blocks`
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
>1.2 Place 1 space before the opening parenthesis in control statements (if, while etc.). Place no space between the argument list and the function name in function calls and declarations. eslint: `keyword-spacing`
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
>1.4 Avoid spaces before commas and require a space after commas. eslint: `comma-spacing`
```javascript
// bad
const foo = 1,bar = 2;
const arr = [1 , 2];

// good
const foo = 1, bar = 2;
const arr = [1, 2];
```
>1.5 Do not use multiple blank lines to pad your code. eslint: `no-multiple-empty-lines`
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
>1.6 Set off operators with spaces. eslint: `space-infix-ops`
```javascript
// bad
const x=y+5;

// good
const x = y + 5;
```
#### [:arrow_up: Back to top](#table-of-contents)

### Blocks
>2.1 Use braces with all multiline blocks. eslint: `nonblock-statement-body-position`
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
>2.2 If an if block always executes a return statement, the subsequent else block is unnecessary. A return in an else if block following an if block that contains a return can be separated into multiple if blocks. eslint: `no-else-return`
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

>2.3 Use empty line to separate logical blocks.
  ```javascript
// bad
function baz(arg1, arg2) {
    this.a = arg1;
    const foo = arg1;
    this.b = arg2;
    // ...
}

// good
function bar(arg1, arg2) {
    this.a = arg1;
    this.b = arg2;
    
    const foo = arg1;
    // ...
} 
```

> 2.4 If you’re using multiline blocks with `if` and `else`, put `else` on the same line as your `if` block’s closing brace. **brace-style**
```javascript

// bad
if (test) {
  thing1();
  thing2();
} 
else {
  thing3();
}
 
// good 
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}
```

#### [:arrow_up: Back to top](#table-of-contents)

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
#### [:arrow_up: Back to top](#table-of-contents)

### Objects
> 4.1 Use the literal syntax for object creation. eslint: `no-new-object`

```javascript
// bad
const item = new Object();

 // good
const item = {};
```

> 4.2 Use object method shorthand. eslint: `object-shorthand`
```javascript
// bad
const atom = {
  value: 1,

  addValue: function (value) {
      return atom.value + value;
  }
};

// good
const atom = {
  value: 1,
  addValue(value) {
      return atom.value + value;
  }
};
```

> 4.3 Use property value shorthand. eslint: `object-shorthand`
```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad 
const obj = {
    lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
    lukeSkywalker,
};
```

> 4.4 Only quote properties that are invalid identifiers. eslint: `quote-props`

> Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.
```javascript
// bad
const bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5,
};

// good
const good = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
};
```

> 4.5 Prefer the object spread syntax over `Object.assign` to shallow-copy objects. Use the object rest parameter syntax to get a new object with certain properties omitted. eslint: `prefer-object-spread`
```javascript
// very bad
const original = { a: 1, b: 2 }; 
const copy = Object.assign(original, { c: 3 }); // this mutates `original`
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 }; 
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

#### [:arrow_up: Back to top](#table-of-contents)

### Destructuring

> 5.1 Use object destructuring when accessing and using multiple properties of an object. eslint: `prefer-destructuring`

> Why? Destructuring saves you from creating temporary references for those properties, and from repetitive access of the object. Repeating object access creates more repetitive code, requires more reading, and creates more opportunities for mistakes. Destructuring objects also provides a single site of definition of the object structure that is used in the block, rather than requiring reading the entire block to determine what is used.
```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}
 
// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

>5.2 Use array destructuring. eslint: `prefer-destructuring`
```javascript
const arr = [1, 2, 3, 4];

// bad 
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```
>5.3 Use object destructuring for multiple return values, not array destructuring.

> Why? You can add new properties over time or change the order of things without breaking call sites.

```javascript
// bad
function processInput(input) {
  // then a miracle occurs
  return [left, right, top, bottom];
}

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);

// good
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom };
}
 
// the caller selects only the data they need 
const { left, top } = processInput(input);
```

### Interfaces
>6.1 Do not use "I" as a prefix for interface names.
```typescript
//bad
interface ICar {}

//good
interface CarInterface {}
//or
interface Car {}
```
>6.2 Use PascalCase for interface names
```typescript
//bad
interface userProfileInterface {}

//good
interface UserProfileInterface {}
```
>6.3 Use whole words in names when possible
```typescript
//bad
interface DmEditorInterface {}

//good
interface DiagramEditorInterface {}
```
>6.4 Use camelCase for interface members
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
>6.5 Use separate interface instead of explicit describe entity when the interface can be used in several places
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
#### [:arrow_up: Back to top](#table-of-contents)

### Strings
>7.1 When programmatically building up strings, use template strings instead of concatenation
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
>7.2 Use single quotes ' for strings
```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// good
const name = 'Capt. Janeway';
```
#### [:arrow_up: Back to top](#table-of-contents)

### Classes & Components
>8.1 It is unnecessary to provide an empty constructor or one that simply delegates into its parent class because ES2015 provides a default class constructor if one is not specified. However constructors with parameter properties, visibility modifiers or parameter decorators should not be omitted even if the body of the constructor is empty.
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
>8.2 Remove unused lifecycle hooks

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
>8.3 If a class member is not a parameter, initialize it where it's declared, which sometimes lets you drop the constructor entirely.
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
>8.4 Don't use public access modifier for properties because, In TypeScript by default all the members (properties and methods) of a class are public
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
>8.5 Try to find some common methods in our codebase first, if there is one that you need, inject the service or extend a base class in your class

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
>8.6 Consider creating base component if you have common functionality in several components
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
>8.7 Split component members with whitespace if they are different access modifier, decorators etc.
```typescript
//bad
class Component {
    @Input() input1;
    @Input() input2;
    @Output() output1;
    @Output() output2;
    private property1;
    private property2;
    public property3;
    public property4;
    //or
    property5;
    property6;
}

//good
class Component {
  @Input() input1;
  @Input() input2;
  
  @Output() output1;
  @Output() output2;
  
  private property1;
  private property2;
  
  public property3;
  public property4;
  
  //or
  property5;
  property6;
}
```
#### [:arrow_up: Back to top](#table-of-contents)

### Comparison operators and equality
>9.1 Conditional statements such as the if statement evaluate their expression using coercion with the ToBoolean abstract method and always follow these simple rules:

1) ***Objects*** evaluate to ```true```. Empty ***array*** also evaluates to ```true``` because it's object under the hood
2) ***Undefined*** evaluates to ```false```
3) ***Null*** evaluates to ```false```
4) ***Booleans*** evaluate to the value of the boolean
5) ***Numbers*** evaluate to ```false``` if +0, -0, or NaN, otherwise ```true```
6) ***Strings*** evaluate to ```false``` if an empty string '', otherwise ```true```

>9.2 Ternaries should not be nested and generally be single line expressions
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

>9.3 Use Ternaries over if expression when you need to assign some value to variable
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
>9.4 Avoid unneeded ternary statements
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
>9.5 Use shortcuts
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
#### [:arrow_up: Back to top](#table-of-contents)

### Naming conventions
>10.1 Avoid shortcuts for variable, properties or function names. Be descriptive with your naming
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
>10.2 Use camelCase when naming objects, functions, and instances. eslint: `camelcase`
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
>10.3 Use PascalCase only when naming constructors or classes. eslint: `new-cap`
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
>10.4 Use camelCase when you export-default a function. Your filename should be identical to your function’s name
```javascript
function makeStyleGuide() {
  // ...
}

export default makeStyleGuide;
```
>10.5 Use PascalCase when you export a constructor / class / singleton / function library / bare object
```javascript
const Config = {
  es6: {
  },
};

export default Config;
```
>10.6 Acronyms and initialisms should always be all uppercased, or all lowercased. Why? Names are for readability, not to appease a computer algorithm.
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
>10.7 If your file exports a single class, your filename should be exactly the name of the class
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
#### [:arrow_up: Back to top](#table-of-contents)

### Functions
> 11.1 Use descriptive function names

```javascript 
// bad 
function foo() {
  // ...
}

// bad
const foo = function () {
  // ...
};

// good
// lexical name distinguished from the variable-referenced invocation(s)
function longUniqueDescriptiveFunctionName() {
  // ...
};
```
> 11.2 Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

```javascript
// bad
function foo(name, options, arguments) {
  // ...
}

// good
function foo(name, options, args) {
  // ...
}
```

> 11.3 Never use `arguments`, opt to use rest syntax `...` instead. eslint: `prefer-rest-params`

> Why? `...` is explicit about which arguments you want pulled. Plus, rest arguments are a real Array, and not merely Array-like like `arguments`.

```javascript
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
```

> 11.4 Use default parameter syntax rather than mutating function arguments.

```javascript
// really bad
function handleThings(opts) {
  // No! We shouldn’t mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad 
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```
> 11.5 Avoid side effects with default parameters.
```javascript
let b = 1;
// bad
function count(a = b++) {
  console.log(a); 
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

> 11.6 Always put default parameters last. eslint: `default-param-last`

```javascript
// bad
function handleThings(opts = {}, name) {
  // ...
}

// good
function handleThings(name, opts = {}) {
  // ...
} 
```

> 11.7 Never use the Function constructor to create a new function. eslint: `no-new-func`
>Why? Creating a function in this way evaluates a string similarly to `eval()`, which opens vulnerabilities.
```javascript
// bad
const add = new Function('a', 'b', 'return a + b');

// still bad
const subtract = Function('a', 'b', 'return a - b');
```
> 11.8 Spacing in a function signature. eslint: `space-before-function-paren` `space-before-blocks`

> Why? Consistency is good, and you shouldn’t have to add or remove a space when adding or removing a name.
 
```javascript
// bad
const f = function(){};
const g = function (){};
const h = function() {};

// good
const x = function () {};
const y = function a() {};
```

> 11.9 Never reassign parameters. eslint: `no-param-reassign`
   
 > Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.
```javascript
// bad
function f1(a) {
  a = 1;
  // ...
}
 
function f2(a) {
  if (!a) { a = 1; }   
  // ...
}
 
// good 
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```
> 11.10 Prefer the use of the spread syntax `...` to call variadic functions. eslint: `prefer-spread`

> Why? It’s cleaner, you don’t need to supply a context, and you can not easily compose `new` with `apply`.
```javascript
// bad 
const x = [1, 2, 3, 4, 5]; 
console.log.apply(console, x);

// good
const x = [1, 2, 3, 4, 5]; 
console.log(x); 
console.log(...x);

// bad 
new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

// good
new Date(...[2016, 8, 5]);
```
> 11.11 Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item. eslint: `function-paren-newline`

```javascript
// bad
function foo(bar,
             baz,
             quux) {
    // ...
}

// good
function foo(
  bar,
  baz,
  quux
) {
  // ...
}

// bad
console.log(foo,
  bar,
  baz);

// good
console.log(
  foo,
  bar,
  baz
);
```

#### [:arrow_up: Back to top](#table-of-contents)

### Arrow Functions

> 12.1 When you must use an anonymous function (as when passing an inline callback), use arrow function notation. eslint: `prefer-arrow-callback`

> Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

> Why not? If you have a fairly complicated function, you might move that logic out into its own named function expression.

```javascript
// bad 
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```

> 12.2 If the function body consists of a single statement returning an [expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a `return` statement. eslint: `arrow-parens`, `arrow-body-style`

> Why? Syntactic sugar. It reads well when multiple functions are chained together.

```javascript
// bad
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

// good 
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  return `A string containing the ${nextNumber}.`; 
});

// good
[1, 2, 3].map((number, index) => ({
  [index]: number,
}));

// No implicit return with side effects
function foo(callback) {
  const val = callback();
  if (val === true) {
    // Do something if callback returns true
  }
}
```

> 12.3 In case the expression spans over multiple lines, wrap it in parentheses for better readability.

> Why? It shows clearly where the function starts and ends.
```javascript
// bad
['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
  httpMagicObjectWithAVeryLongName,
  httpMethod,
  )
);

// good 
['get', 'post', 'put'].map((httpMethod) => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));
```
> 12.4 Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`). eslint: `no-confusing-arrow`

```javascript
// bad
const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

// good 
const itemHeight = (item) => {
const { height, largeSize, smallSize } = item;
  return height <= 256 ? largeSize : smallSize;
};
```

> 12.5 Enforce the location of arrow function bodies with implicit returns. eslint: `implicit-arrow-linebreak`
```javascript
// bad
(foo) =>
  bar;

(foo) =>
      (bar);

// good
(foo) => bar;
(foo) => (bar);
(foo) => (
 bar
)
```
#### [:arrow_up: Back to top](#table-of-contents)

### Using observables
>13.1 Use camelCase and $ sign for variables that hold observable
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
>13.2 Use the async pipe in templates to subscribe to an Observable and automatically unsubscribe when the component is destroyed.

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
>13.3 Do not use too much logic in subscribe. Consider to create separate method
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
>13.4 Error handling
##### Since the AsyncPipe doesn't directly allow for error handling in the template, handle errors in the observable stream itself, using the catchError operator, and emit a user-friendly error state.
```javascript
data$: Observable<DataType> = this.dataService.getData().pipe(
  catchError(error => {
    // Handle or log the error
    return of([]); // Return a safe value or error indication
  })
);
```

>13.5 Encapsulate Complex Logic in the Service
##### If the observable logic is complex, consider encapsulating it within a service. This keeps your component cleaner and focused on the template and user interactions:
```javascript
    // In your service
    getData(): Observable<DataType> {
    // Complex logic here
    return this.http.get<DataType>(url).pipe(
    // operators here
    );
}
```

#### [:arrow_up: Back to top](#table-of-contents)

### Async pipes

> 14.1 Handle Null and Undefined Gracefully

> Data streams might emit null or undefined at the beginning or during loading states. Ensure your templates can handle this gracefully
```javascript
<div *ngIf="data$ | async as data; else loading">
    {{data}}
</div>
<ng-template #loading>Loading...</ng-template>
```

> 14.2 When you need to conditionally show elements based on the presence of data, combine AsyncPipe with structural directives like *ngIf
```javascript
<div *ngIf="data$ | async as data">
  {{ data }}
</div>
```

#### [:arrow_up: Back to top](#table-of-contents)

### Imports
> 15.1 Always use modules (`import`/`export`) over a non-standard module system. You can always transpile to your preferred module system.

> Why? Modules are the future, let’s start using the future now.

```javascript
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// ok
import AirbnbStyleGuide from './AirbnbStyleGuide';
export default AirbnbStyleGuide.es6;

// best
import { es6 } from './AirbnbStyleGuide';
export default es6;
```
> 15.2 Do not use wildcard imports.
  > Why? This makes sure you have a single default export.
```javascript
// bad
import * as AirbnbStyleGuide from './AirbnbStyleGuide';

// good
import AirbnbStyleGuide from './AirbnbStyleGuide';
```
> 15.3 Only import from a path in one place. eslint: `no-duplicate-imports`

> Why? Having multiple lines that import from the same path can make code harder to maintain.

```javascript
// bad
import foo from 'foo';
// … some other imports … //
import { named1, named2 } from 'foo';

// good
import {
  named1,
  named2,
  named3
} from 'foo';
```
> 15.4 Put all `import`s above non-import statements. eslint: `import/first`

> Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.
```javascript
// bad
import foo from 'foo';
foo.init();
import bar from 'bar';
 
// good
import foo from 'foo';
import bar from 'bar';

foo.init();
```

> 15.5 Multiline imports should be indented just like multiline array and object literals. eslint: `object-curly-newline`

> Why? The curly braces follow the same indentation rules as every other curly brace block in the style guide, as do the trailing commas.

```javascript
// bad
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

// good
import {
  longNameA,
  longNameB,
  longNameC,
  longNameD,
  longNameE,
} from 'path'; 
```

#### [:arrow_up: Back to top](#table-of-contents)

### Braces
> 16.1 Usage of `Single` and `Double` braces
  
```javascript
// bad
<a href='https://example.com' title="Example Site">Visit Example Site</a>
<input type='text' placeholder='John`s Profile'>
  
// good
<a href="https://example.com" title="Example Site">Visit Example Site</a>
<input type="text" placeholder="John's Profile"> 
```
```javascript
// bad 
import {nameA, nameB} from "path";

// good
import {nameA, nameB} from 'path';
```

#### [:arrow_up: Back to top](#table-of-contents)


### Using external libs
> 16.1 Use maintained external libs when it's possible
```javascript
// bad
function baz(array) {
  return array[0];
}
const firstItem = baz(someArray);

// good
import {first} from 'lodash';
    
const firstItem = first(someArray)
```

> 16.2 Don't invent massive code blocks that can be easily replaced by library

```javascript
// bad
function cloneDeep(value) {
  if (value === null || typeof value !== 'object') {
    return value;
  }

  if (Array.isArray(value)) {
    return value.map((item) => cloneDeep(item));
  }

  if (value instanceof Object) {
    const copy = {};
    Object.keys(value).forEach((key) => {
      copy[key] = cloneDeep(value[key]);
    });
    return copy;
  }
  
  if (value instanceof Date) {
    return new Date(value.getTime());
  }

  if (value instanceof RegExp) {
    return new RegExp(value);
  }

  return value;
}

const obj = {a: 2, b: {c: 3}};

const newObj = cloneDeep(obj);

// good
import {cloneDeep} from 'lodash';

const obj = {a: 2, b: {c: 3}};

const newObj = cloneDeep(obj);
```

#### [:arrow_up: Back to top](#table-of-contents)
