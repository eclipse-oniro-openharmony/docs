# ArkTS1.2迁移语法规范

ArkTS1.2在引入了静态类型系统、增强的并发能力的同时，也引入了与ArkTS1.1在语法和语义上的一部分差异。本文罗列了所有在ArkTS1.2中被限制的ArkTS1.1特性，并提供了重构代码的建议。

## 限定关键字

**规则：** `arkts-invalid-identifier`

**级别：** error

ArkTS1.2中对关键字和保留字做了严格定义。代码中不能使用这些关键字作为变量名称。

**ArkTS1.1**
```typescript
let as: number = 1;
const abstract: string = "abstract";
```

**ArkTS1.2**
```typescript
let a = 1;
const abstract1: string = "abstract";
```

## 数值类型语义变化

**规则：** `arkts-numeric-semantic`

**级别：** error

在ArkTS1.2中，为了获得更好的执行效率，整型数字字面量默认是int类型。

**ArkTS1.1**
```typescript
let n = 1;
console.log(n / 2)  // output: 0.5

let arr = [1, 2, 3];

function multiply(x = 2, y = 3) { // 需要明确类型
  return x * y;
}

function divide(x: number, y: number) {
  return x / y;
} // 函数返回值

let num = Math.floor(4.8); // num 可能是 int
let value = parseInt("42"); // value 可能是 int

function identity<T>(value: T): T {
  return value;
}
identity(42); // 42 可能推导为 int
```

**ArkTS1.2**
```typescript
let n: number = 1;
console.log(n / 2)  // output: 0.5

let m = 1;
console.log(m / 2)  // output: 0

let arr: number[] = [1, 2, 3];

function multiply(x: number = 2, y: number = 3): number {
  return x * y;
}

function divide(x: number, y: number): number {
  return x / y;
}

let num: number = Math.floor(4.8);
let value: number = parseInt("42");

function identity<T>(value: T): T {
  return value;
}
identity(42 as number);
```

## void类型只能用在返回类型的场景

**规则：** `arkts-limited-void-type`

**级别：** error

在ArkTS1.2中，void仅作为类型使用。void类型没有实体。

**ArkTS1.1**
```typescript
let s: void = foo();
let t: void | number = foo();

function process<T>(input: T): T {
  return input;
}
let result = process<void>(foo()); 

type VoidAlias = void; 

let { x }: { x: void } = { x: foo() };

function execute(callback: void) {
  callback();
}

let x = fun() as void;
```

**ArkTS1.2**
```typescript
function foo(): void {}
foo();

function bar(): void {}

function execute(callback: () => void) {
  callback();
}
fun();
```

## 不支持void操作符

**规则：** `arkts-no-void-operator`

**级别：** error

在ArkTS1.2中，undefined作为关键字不能作为变量名称，因此不需要通过void操作符获取undefined。

**ArkTS1.1**
```typescript
let s = void 'hello';
console.log(s);  // output: undefined

let a = 5;
let b = void (a + 1);

function logValue(value: any) {
    console.log(value);
}
logValue(void 'data');

let fn = () => void 0;
```

**ArkTS1.2**
```typescript
(() => {
    'hello'
    return undefined;
})()

let a = 5;
let b = (() => {
    a + 1;
    return undefined;
})();  // 替换为 IIFE

logValue((() => {
    'data';
    return undefined;
})());  // 替换为 IIFE

let fn = () => undefined;  // 直接返回 `undefined`
```

## 限定使用字面量类型

**规则：** `arkts-limited-literal-types`

**级别：** error

ArkTS1.2不支持数字字面量类型，布尔字面量类型。

ArkTS1.2提供了更多细化的数值类型供开发者选择，更关注数值的范围而非某个特定的数字值，同时，为了更好的代码简洁性和避免引入歧义，不引入复杂的数值字面量类型语法。

**ArkTS1.1**
```typescript
let n1: 1 = 1;
let n2: 0.1 = 0.1;
let f: true = true;

function getOne(): 1 {
  return 1; 
}
function isAvailable(): true {
  return true;
}

function setFlag(flag: true) {
  console.log(flag);
}
function setPrecision(precision: 0.1) {
  console.log(precision);
}

interface Config {
  readonly enable: true;
  readonly threshold: 100;
}
```

**ArkTS1.2**
```typescript
let n1: int = 1;
let n2: number = 0.1;
let f: boolean = true;

function getOne(): int {
  return 1;
}
function isAvailable(): boolean {
  return true;
}

function setFlag(flag: boolean) {
  console.log(flag);
}
function setPrecision(precision: number) {
  console.log(precision);
}

interface Config {
  readonly enable: boolean;
  readonly threshold: int;
}
```

## 不支持arguments对象

**规则：** `arkts-no-arguments-obj`

**级别：** error

ArkTS1.2对函数调用进行严格的参数检查，参数个数不符时编译报错，因此不需要在函数体内通过arguments机制获取参数。

**ArkTS1.1**
```typescript
function foo(u: string) {
  console.log(arguments[0]);
}

function bar(a: number, b?: number) {
  if (arguments.length === 1) {
    console.log("Only one argument passed");
  }
}

function sum() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

function test() {
  console.log(arguments.callee);
}
```

**ArkTS1.2**
```typescript
function foo(u: string) {
  console.log(u);
}

function bar(a: number, b?: number) {
  if (b === undefined) {
    console.log("Only one argument passed");
  }
}

function sum(...args: number[]) {  
  // 使用 `...rest` 替代 `arguments`
  return args.reduce((acc, num) => acc + num, 0);
}

function test() {
  console.log(test);  // 直接使用函数名
}
```

## 数组索引必须是整型数据

**规则：**`arkts-array-index-expr-type`

**级别：error**

ArkTS1.2支持数值类型的细化，为了实现数组更快的访问，数组索引表达式必须是整数类型。

**ArkTS1.1**

```typescript
function foo (index: number) {
  let array = [1, 2, 3] 
  let element = array[index]
}

function getIndex(): number {
  return Math.random() * 10; // 可能返回小数
}

let array = [1, 2, 3];
for (let i: number = 0; i < array.length; i++) { // 违反规则
  console.log(array[i]);
}
```

**ArkTS1.2**

```typescript
function foo (index: int) {
  let array = [1, 2, 3] 
  let element = array[index]
}

function getIndex(): int {
  return Math.floor(Math.random() * 10);  // 转换为 `int`
}

let array = [1, 2, 3];
for (let i: int = 0; i < array.length; i++) { // 改为 `int`
  console.log(array[i]);
}
```

## 不支持通过负数访问数组

**规则：**`arkts-array-index-negative`

**级别：error**

ArkTS1.2不支持使用负整数访问数组元素。

**ArkTS1.1**

```typescript
let an_array = [1, 2, 3];
let element = an_array [-1];
console.log(getElement(an_array, -1)); // 违反规则
for (let i: int = -1; i < an_array.length; i++) { // 违反规则
  console.log(an_array[i]);
}

function getElement(arr: number[], index: int) {
  return arr[index]; // 可能接收负数索引
}
```

**ArkTS1.2**

```typescript
let an_array = [1, 2, 3];
let element = an_array [1];
console.log(getElement(an_array, 1)); // 传递非负索引
for (let i: int = 0; i < an_array.length; i++) { // 仅允许非负索引
  console.log(an_array[i]);
}

function getElement(arr: number[], index: int) {
  if (index < 0) throw new Error("Index must be a non-negative integer");
  return arr[index]; // 仅允许非负整数
}
```

## 增加数组越界运行时检查

**规则：**`arkts-runtime-array-check`

**级别：error**

为了保证类型安全，在访问数组元素时，ArkTS1.2会对索引的合法性进行校验。

**ArkTS1.1**

```typescript
let a: number[] = []
a[100] = 5; // 可能越界
```

**ArkTS1.2**

```typescript
let a: number[] = []
if (100 < a.length) {
  a[100] = 5  // a[100]的值为5
}
```

## arkts-no-tuples-arrays

**规则：**`arkts-no-tuples-arrays`

**级别：error**

ArkTS1.2中数组和元组是不同的类型，运行时使用元组类型可以获得更好的性能。

**ArkTS1.1**

```typescript
const tuple: [number, number, boolean] = [1, 3.14, true];
const array: (number|boolean) [] = tuple;

const tuple: Array<number | boolean> = [1, 3.14, true];  // 违反规则

function getTuple(): (number | boolean)[] {  // 违反规则
  return [1, 3.14, true];
}
getTuple([1, 3.14, true]);  // 传入元组

type Point = (number | boolean)[];  // 违反规则
const p: Point = [3, 5, true];
```

**ArkTS1.2**

```typescript
const tuple: [number, number, boolean] = [1, 3.14, true];
const array:  [number, number, boolean] = tuple;

const tuple: [number, number, boolean] = [1, 3.14, true];  // 正确使用元组

function getTuple(): [number, number, boolean] {  // 正确使用元组
  return [1, 3.14, true];
}
getTuple([1, 3.14, true]);

type Point = [number, number, boolean];  // 使用元组
const p: Point = [3, 5, true];
```

## 函数类型

**规则：**`arkts-incompatible-function-types`

**级别：error**

TypeScript允许对函数类型的变量进行更宽松的赋值，而在ArkTS1.2中，将对函数类型的赋值进行更严格的检查。函数类型转换时，参数遵循逆变(Contravariance)规则，返回类型遵循协变(Covariance)规则。

**ArkTS1.1**

```typescript
type FuncType = (p: string) => void;
let f1: FuncType =
    (p: string): number => {
        return 0
    }
let f2: FuncType = (p: any): void => {};

class Animal {}
class Dog extends Animal {}
type FuncType = () => Animal;
let f: FuncType = (): Dog => new Dog(); // 在 TypeScript 允许，但在 ArkTS 可能不允许

type FuncType2 = (dog: Dog) => void;
let f: FuncType2 = (animal: Animal) => {}; // 违反规则
```

**ArkTS1.2**

```typescript
type FuncType = (p: string) => void
let f1: FuncType =
  	(p: string) => {
        ((p: string): number => {
            return 0
        })(p) 
    }
let f2: FuncType = (p: string): void => {};

class Animal {}
class Dog extends Animal {}
type FuncType = () => Animal;
let f: FuncType = (): Animal => new Animal();// 返回 `Animal`

type FuncType2 = (dog: Dog) => void;
let f: FuncType = (dog: Dog) => {}; // 参数类型严格匹配
```

## 不支持指数操作符

**规则：**`arkts-no-exponent-op`

**级别：error**

ArkTS1.2不支持指数运算符（`**`和`**=`），采用语言基础库。

**ArkTS1.1**

```typescript
let x = 2 ** 5;

let y = 3;
y **= 4; // 违反规则

let result = (1 + 2) ** (3 * 2); // 违反规则

function power(base: number, exponent: number) {
  return base ** exponent; // 违反规则
}

let values = [1, 2, 3];
let squared = values.map(v => v ** 2); // 违反规则
```

**ArkTS1.2**

```typescript
let x = Math.pow(2, 5);

let y = 3;
y = Math.pow(y, 4); // 直接使用 `Math.pow()`

let result = Math.pow(1 + 2, 3 * 2); // 直接使用 `Math.pow()`

function power(base: number, exponent: number) {
  return Math.pow(base, exponent); // 使用 `Math.pow()`
}

let values = [1, 2, 3];
let squared = values.map(v => Math.pow(v, 2)); // 使用 `Math.pow()`
```

## 不支持正则表达式

**规则：**`arkts-no-regexp-literals`

**级别：error**

ArkTS1.2不支持正则表达式字面量。

**ArkTS1.1**

```typescript
let regex: RegExp = /bc*d/;
let regex = /\d{2,4}-\w+/g; // 违反规则
function matchPattern(str: string) {
  return str.match(/hello\s+world/i); // 违反规则
}

let text = "Hello world!";
let result = text.replace(/world/, "ArkTS"); // 违反规则

let items = "apple,banana, cherry".split(/\s*,\s*/); // 违反规则
```

**ArkTS1.2**

```typescript
let regex: RegExp =  new RegExp('bc*d');
let regex = new RegExp('\\d{2,4}-\\w+', 'g'); // 使用 `RegExp` 类
function matchPattern(str: string) {
  let regex = new RegExp('hello\\s+world', 'i'); // 使用 `RegExp`
  return str.match(regex);
}

let text = "Hello world!";
let regex = new RegExp('world'); // 使用 `RegExp` 类
let result = text.replace(regex, "ArkTS");

let regex = new RegExp('\\s*,\\s*'); // 使用 `RegExp`
let items = "apple,banana, cherry".split(regex);
```

## enum中不支持成员为不同类型数据

**规则：**`arkts-no-enum-mixed-types`

**级别：error**

enum用来表示一组离散的数据，使用浮点数据不符合enum的设计理念。使用浮点数据可能造成精度损失的问题。因此，ArkTS1.2中enum的值必须为整型数据。

**ArkTS1.1**

```typescript
enum Size {
  UP = 1.5,
  MIDDLE = 1,
  DOWN = 0.75
}
```

**ArkTS1.2**

```typescript
enum Size{ 
  UP = 1,
  MIDDLE = 2,
  DOWN = 3
}
```

## 不支持为函数增加属性

**规则：**`arkts-no-func-props`

**级别：error**

ArkTS1.2上不支持在函数上动态添加属性。

**ArkTS1.1**

```typescript
function foo(path: string): void {
  console.log(path)
}
foo.baz = 1

const obj = {
  foo(path: string): void {
    console.log(path);
  }
};
obj.foo.baz = 2; // 违反规则

function createLogger() {
  function log(message: string) {
    console.log(message);
  }
  log.level = "debug"; // 违反规则
  return log;
}

const logger = createLogger();
console.log(logger.level);

function counter() {
  counter.count = (counter.count || 0) + 1; // 违反规则
  return counter.count;
}
console.log(counter());
```

**ArkTS1.2**

```typescript
class T {
  static foo(path: string): void {
    console.log(path)
  }
  static bar: number = 1
}

class T {
  static foo(path: string): void {
    console.log(path);
  }

  static baz: number = 2;
}
T.foo("example");
console.log(T.baz);

class Logger {
  static level = "debug";

  static log(message: string) {
    console.log(message);
  }
}
Logger.log("test");
console.log(Logger.level);

class Counter {
  static count = 0;

  static increment() {
    this.count += 1;
    return this.count;
  }
}
console.log(Counter.increment());
```

## 不支持TS装饰器

**规则：**`arkts-no-ts-decorators`

**级别：error**

ArkTS1.2中不支持将类作为对象，不能通过装饰器中对类做动态改变。

**ArkTS1.1**

```typescript
function decorateKlass(target: Object) {
  console.log("decorateKlass")
}

@decorateKlass // 违反规则
class Person {
    age: number = 12
}
```

**ArkTS1.2**

```typescript
class Person {
    age: number = 12
}

class PersonHelper {
  static createPerson(): Person {
     console.log("decorateKlass")
     return new Person()
  }
}
```

## 类实现接口时，不能用类方法替代对应interface属性

**规则：**`arkts-no-method-overriding-field`

**级别：error**

ArkTS1.2不支持structural type，属性和方法不能互相转换。

**ArkTS1.1**

```typescript
interface Person {
  cb: () => void
}

class student implements Person{
  cb() {}
} 

interface Transformer<T> {
  transform: (value: T) => T; // 违反规则
}

class StringTransformer implements Transformer<string> {
  transform(value: string) { return value.toUpperCase(); }  // 违反规则
}
```

**ArkTS1.2**

```typescript
interface Person {
  cb(): void
}

class student implements Person{
  cb() {}
}

interface Transformer<T> {
  transform(value: T): T;  // 变成方法
}

class StringTransformer implements Transformer<string> {
  transform(value: string) { return value.toUpperCase(); }  // 正确
}
```

## 限定switch语句中case语句类型

**规则：**`arkts-switch-expr`

**级别：error**

ArkTS1.2的switch表达式类型只能为number，string，enum。

**ArkTS1.1**

```typescript
const isTrue = true;
switch (isTrue) {
    case true: // 违反规则
        console.log('It\'s true'); break;
    case false:  // 违反规则
        console.log('It\'s false'); break;
}

const obj = { value: 1 };
switch (obj) {  // 违反规则
    case { value: 1 }:
        console.log('Matched'); break;
}

const arr = [1, 2, 3];
switch (arr) {  // 违反规则
    case [1, 2, 3]: 
        console.log('Matched'); break;
}
```

**ArkTS1.2**

```typescript
const isTrue = 'true';
switch (isTrue) {
    case 'true': 
        console.log('It\'s true'); break;
    case 'false': 
        console.log('It\'s false'); break;
}

const objValue = 1;  // 仅存储值
switch (objValue) {
    case 1:
        console.log('Matched'); break;
}

const arrValue = '1,2,3';  // 变成字符串
switch (arrValue) {
    case '1,2,3':
        console.log('Matched'); break;
}
```

## 不支持重复case语句

**规则：**`arkts-case-expr`

**级别：error**

ArkTS1.2不支持Switch语句的中case重复，便于提高代码可读性。

**ArkTS1.1**

```typescript
const num = 1;
switch (num) {
    case 1:
        console.log('First match');
    case 1:
        console.log('Second match');
        break;
    default:
        console.log('No match');
}

enum Status {
    Active,
    Inactive
}

const state = Status.Active;
switch (state) {
    case Status.Active:
        console.log('User is active');
        break;
    case Status.Active: // 违反规则
        console.log('Already active');
        break;
}
```

**ArkTS1.2**

```typescript
const num = 1;
switch (num) {
    case 1:
        console.log('First match');
        console.log('Second match');
        break;
    default:
        console.log('No match');
}

switch (state) {
    case Status.Active:
        console.log('User is active');
        console.log('Already active'); // 代码合并
        break;
}
```

## 不支持lazy关键字

**规则：**`arkts-no-lazy-import`

**级别：error**

ArkTS1.2支持默认懒加载，无需lazy关键字。

**ArkTS1.1**

```typescript
import lazy { m } from 'module'
import lazy { a, b } from 'module1'; // 违反规则
import { c } from 'module2';
```

**ArkTS1.2**

```typescript
import { m } from 'module'
import { a, b } from 'module1'; // 移除 lazy
import { c } from 'module2';
```

## 不支持动态import

**规则：**`arkts-no-dynamic-import`

**级别：error**

ArkTS1.2中模块加载默认支持懒加载。

**ArkTS1.1**

```typescript
function main(): void {
  import('./file').then((m) => {
    console.log(m.Data.name)
  })
}

document.getElementById("btn")?.addEventListener("click", async () => {
  const module = await import('./utils');  // 错误: 在ArkTS中动态`import()`是不支持的.
  module.doSomething();
});

function getModule() {
  return import('./heavyModule')  // 错误: 在ArkTS中动态`import()`是不支持的.
    .then((m) => m.default);
}
```

**ArkTS1.2**

```typescript
import { Data } from './file'
import { doSomething } from './utils';  // 静态import是可以的.
import heavyModule from './heavyModule';  // 静态import是可以的.

function main(): void {
  console.log(Data.name)
}

document.getElementById("btn")?.addEventListener("click", () => {
  doSomething();
});

function getModule() {
  return heavyModule;
}
```

## 不支持副作用导入

**规则：**`arkts-no-side-effect-import`

**级别：error**

ArkTS1.2中模块加载默认支持懒加载，无法实现导入副作用的功能。

**ArkTS1.1**

```typescript
// logger.ets
console.log("Logger initialized!");

// main.ets
import "./logger";
console.log("Main program running...");
```

**ArkTS1.2**

```typescript
// main.ets
console.log("Logger initialized!");
console.log("Main program running...");
```

## 不支持globalThis

**规则：**`arkts-no-globalthis`

**级别：error**

由于ArkTS1.2不支持动态更改对象的布局，因此不支持全局作用域和globalThis。

**ArkTS1.1**

```typescript
// 全局文件中
var abc = 100;

// 从上面引用'abc'
let x = globalThis.abc;
```

**ArkTS1.2**

```typescript
// file1
export let abc: number = 100;

// file2
import * as M from 'file1'

let x = M.abc;
```

## 不支持Funcion.bind方法

**规则：**`arkts-no-func-bind`

**级别：error**

ArkTS不允许使用标准库函数Function.bind。标准库使用这些函数来显式设置被调用函数的this参数。

**ArkTS1.1**

```typescript
class MyClass {
  constructor(public name: string) {}

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const instance = new MyClass("Alice");
const boundGreet = instance.greet.bind(instance); // 违反规则，不允许使用 Function.bind
boundGreet();
```

**ArkTS1.2**

```typescript
class MyClass {
  constructor(public name: string) {}

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const instance = new MyClass("Alice");
const boundGreet = () => instance.greet(); // 使用箭头函数
boundGreet(); // Hello, my name is Alice
```

## 不支持将类作为对象

**规则：**`arkts-no-classes-as-obj`

**级别：error**

在ArkTS中，class声明的是一个新的类型，不是一个值。因此，不支持将class用作对象（例如将class赋值给一个变量）。

**ArkTS1.1**

```typescript
class MyClass {
  constructor(public name: string) {}
}

let obj = MyClass; // 违反规则
```

**ArkTS1.2**

```typescript
class MyClass {
  constructor(name: string) {}
}

// 需要通过反射来实现
let className = "path.to.MyClass";
let linker = Class.ofCaller()!.getLinker();
let classType: ClassType | undefined = linker.getType(className) as ClassType;
```

## arkts-limited-stdlib

**规则：**`arkts-limited-stdlib`

**级别：error**

由于TypeScript或JavaScript标准库中的大部分接口与动态特性有关，所以在ArkTS中禁止使用以下接口：

Object: getPrototypeOf

## 不支持structural typing

**规则：**`arkts-no-structural-typing`

**级别：error**

ArkTS1.2不支持structural typing，编译器无法比较两种类型的publicAPI并决定它们是否相同。使用其他机制，例如继承、接口或类型别名。

**ArkTS1.1**

```typescript
// case1
class A {
  v: number = 0
}

class B {
  v: number = 0
}

let a = new B() as A

// case2
class C<T> {
  u: T
}

let b: C<B> = new C<A>()

// case3
class A {
  u: number = 0
}

class B {
  u: number = 0
}

(): A => { return new B() }

class A {
  v: number = 0
}

class B {
  v: number = 0
}
class C<T> {
  u: T;
}

let b: C<B> = new C<A>(); // 违反规则
```

**ArkTS1.2**

```typescript
// case1
class A {
  v: number = 0
}

class B {
  v: number = 0
}

let a = new B()

// case2
class C<T> {
  u: T
}

let b: C<A> = new C<A>()

// case3
class A {
  u: number = 0
}

class B {
  u: number = 0
}

(): B => { return new B() }

class A {
  v: number = 0
}

class B {
  v: number = 0
}
let b: C<A> = new C<A>(); // 使用相同的泛型类型

```

## 禁止extends/implements表达式

**规则：**`arkts-no-extends-expression`

**级别：error**

ArkTS1.2中规范了类的继承，类不能作为对象来继承一个表达式。

**ArkTS1.1**

```typescript
class A {
  v: number = 0
}

let a = A;

class B extends a { // 违反规则
  u: number = 0
}

function getBase() {
  return class {
    w: number = 0;
  };
}

class B extends getBase() { // 违反规则
  u: number = 0;
}

interface I {
  w: number;
}

let i = I;

class B implements i { // 违反规则
  w: number = 0;
}

class A {
  v: number = 0;
}

class B extends new A() { // 违反规则
  u: number = 0;
}
```

**ArkTS1.2**

```typescript
class A {
  v: number = 0
}

class B extends A { // 直接继承类
  u: number = 0
}

class Base {
  w: number = 0;
}

class B extends Base { // 直接继承类
  u: number = 0;
}

interface I {
  w: number;
}

class B implements I { // 直接使用接口
  w: number = 0;
}

class A {
  v: number = 0;
}

class B extends A { // 直接继承类
  u: number = 0;
}
```

## 不支持类TS重载

**规则：**`arkts-no-ts-overload`

**级别：error**

ArkTS1.2不支持TS-like的重载，使用不同的函数体可以提高执行效率。

**ArkTS1.1**

```typescript
function foo(): void
function foo(x: string): void
function foo(x?: string): void { // 违反规则
  /*body*/
}

function sum(x: number, y: number): number;
function sum(x: number, y: number, z: number): number;
function sum(x: number, y: number, z?: number): number {  // 违反规则
  return z ? x + y + z : x + y;
}

function foo(): string;
function foo(x: number): number;
function foo(x?: number): string | number {  // 违反规则
  return x !== undefined ? x * 2 : "default";
}
```

**ArkTS1.2**

```typescript
function foo(x?: string): void {
  /*body*/
}

function sumTwo(x: number, y: number): number {  // 独立实现
  return x + y;
}

function sumThree(x: number, y: number, z: number): number {  // 独立实现
  return x + y + z;
}

function fooString(): string {  // 独立实现
  return "default";
}

function fooNumber(x: number): number {  // 独立实现
  return x * 2;
}
```

## enum的key不能是字符串

**规则：**`arkts-identifiers-as-prop-names`

**级别：error**

ArkTS1.2不支持将字符串作为class、interface、enum等属性或元素的名称，需要使用标识符来表示。

**ArkTS1.1**

```typescript
enum A{
 'red' = '1'
}
```

**ArkTS1.2**

```typescript
enum A{
  red = '1'
}
```

## 创建泛型实例需要类型实参

**规则：**`arkts-no-inferred-generic-params`

**级别：error**

ArkTS1.2中，创建泛型实例时需要类型实参。

**ArkTS1.1**

```typescript
new Array() // 违反规则

new Map(); // 违反规则

class Box<T> {
  value: T;
  constructor(value: T) {
    this.value = value;
  }
}

let box = new Box(42); // 违反规则
```

**ArkTS1.2**

```typescript
new Array<SomeType>() // 指定类型

new Map<string, number>(); // 显式指定键值类型

let box = new Box<number>(42); // 明确指定类型
```

## 不支持[]访问对象属性

**规则：**`arkts-no-props-by-index`

**级别：error**

在ArkTS1.2中，对象结构在编译时已确定。为避免运行时出现错误和更好地提升性能，在ArkTS1.2中不能使用[]的方式动态访问object类型对象的属性。

**ArkTS1.1**

```typescript
function foo(u: object) {
  u['key'] // 违反规则
}

const person = { name: "Alice", age: 30 };
console.log(person['name']); // 违反规则

const data = JSON.parse('{ "name": "Alice" }');
console.log(data['name']); // 违反规则
```

**ArkTS1.2**

```typescript
function foo(m: Map<string, Object>) {
  m.get('key') // 使用 `Map`
}

console.log(person.name); // 直接使用 `.` 访问

interface UserData {
  name: string;
}
const data: UserData = JSON.parse('{ "name": "Alice" }');
console.log(data.name); // 直接使用点访问符
```

## 对象字面量只包含属性不包含方法

**规则：**`arkts-obj-literal-props`

**级别：error**

ArkTS1.2中不支持在对象字面量中定义方法。因为静态语言中类的方法被所有实例所共享，无法通过对象字面量重新定义方法。

**ArkTS1.1**

```typescript
class A {
  foo: () => void = () => {}
}

let a: A = {
  foo() { // 违反规则
    console.log('hello')
  }
}

interface Person {
  sayHello: () => void;
}

let p: Person = {
  sayHello() {  // 违反规则，方法定义方式错误
    console.log('Hi');
  }
};

type Handler = {
  foo(): void; 
};

let handler: Handler = {
  foo() {  // 违反规则
    console.log("Executing handler");
  }
};
```

**ArkTS1.2**

```typescript
class A {
  foo : () => void = () => {}
}

let a: A = {
  foo: () => {
    console.log('hello')
  }
}

let p: Person = {
  sayHello: () => {  // 使用属性赋值方式
    console.log('Hi');
  }
};

type Handler = {
  foo: () => void;  
};

let handler: Handler = {
  foo: () => {  // 修正方法定义方式
    console.log("Executing handler");
  }
};
```

## 对象字面量生成类的实例

**规则：**`arkts-obj-literal-generate-class-instance`

**级别：error**

ArkTS1.2中对象字面量会生成类的实例。

**ArkTS1.1**

```typescript
class A {
  v: number = 0
}

let a: A = { v: 123 }
console.log(a instanceof A)  // false

class A {
  v: number = 0;
  hello() {
    return "Hello";
  }
}

let a: A = { v: 123 };
console.log(a.hello()); // 报错，a 没有 hello() 方法

class A {
  v: number = 0;
}

let a: A = { v: 123 };
console.log(Object.getPrototypeOf(a) === A.prototype); // false

```

**ArkTS1.2**

```typescript
class A {
  v: number = 0
}

let a: A = { v: 123 }
console.log(a instanceof A)  //  true

class A {
  v: number = 0;
  hello() {
    return "Hello";
  }
}

let a: A = { v: 123 };
console.log(a.hello()); // 正常执行 "Hello"

class A {
  v: number = 0;
}

let a: A = { v: 123 };
console.log(Object.getPrototypeOf(a) === A.prototype); // true

```

## 增强对联合类型属性访问的编译时检查

**规则：**`arkts-common-union-member-access`

**级别：error**

在ArkTS1.2中，对象的结构在编译时就确定了。为了避免访问联合类型后出现运行时错误，ArkTS1.2在编译时会对联合类型的同名属性进行编译检查，要求同名属性具有相同的类型。

**ArkTS1.1**

```typescript
class A {
  v: number = 1
}

class B {
  u: string = ''
}

function foo(a: A | B) {
  console.log(a.v) // 违反规则
  console.log(a.u) // 违反规则
}
```

**ArkTS1.2**

```typescript
class A {
  v: number = 1
}

class B {
  u: string = ''
}

function foo(a: A) {
  console.log(a.v)
}

function foo(a: B) {
  console.log(a.u)
}
```

## 类的静态属性需要有初始值

**规则：**`arkts-class-static-initialization`

**级别：error**

ArkTS1.2遵循null-safety，需要为属性赋上初始值。

**ArkTS1.1**

```typescript
class B {}

class A {
  static b: B
}

class A {
  static count: number; // 违反规则，必须初始化
}

class A {
  static config: { theme: string }; // 违反规则，必须初始化
}

class A {
  static name: string;

  constructor() {
    A.name = "default"; // 违反规则，静态属性必须在定义时初始化
  }
}
```

**ArkTS1.2**

```typescript
class B {}

class A {
  static b? : B
  static b: B | undefined = undefined
}

class A {
  static count: number = 0; // 提供初始值
}

class A {
  static config: { theme: string } = { theme: "light" }; // 提供初始值
}

class A {
  static name: string = "default"; // 在定义时初始化
}

```

## 不支持TS-like `Function`类型的调用方式

**规则：**`arkts-no-ts-like-function-call`

**级别：error**

ArkTS1.2会对函数类型进行更严格的编译器检查。函数返回类型需要严格定义来保证类型安全，因此不支持TS-like`Function`类型。

**ArkTS1.1**

```typescript
let f: Function = () => {} // 违反规则

function run(fn: Function) {  // 违反规则
  fn();
}

let fn: Function = (x: number) => x + 1; // 违反规则

class A {
  func: Function = () => {}; // 违反规则
}

function getFunction(): Function { // 违反规则
  return () => {};
}
```

**ArkTS1.2**

```typescript
type F<R> = () => R;
type F1<P, R> = (p:  P) => R

let f: F<void> = () => {}

function run(fn: () => void) {  // 指定返回类型
  fn();
}

let fn: (x: number) => number = (x) => x + 1; // 明确参数类型

class A {
  func: () => void = () => {}; // 明确类型
}

function getFunction(): () => void { // 明确返回类型
  return () => {};
}
```

## 不支持可选方法

**规则：**`arkts-optional-methods`

**级别：error**

ArkTS1.2中类的方法被所有类的实例所共享，增加可选方法的支持会增加开发者判断空值的成本，影响性能。

**ArkTS1.1**

```typescript
interface InterfaceA {
  aboutToDisappear?(): void
}
class ClassA {
  aboutToDisappear?(): void {}
}
```

**ArkTS1.2**

```typescript
interface InterfaceA {
  aboutToDisappear?: () => void
}
class ClassA {
  aboutToDisappear?: () => void = () => {}
}
```

## 实例方法当作对象时会绑定this

**规则：**`arkts-instance-method-bind-this`

**级别：error**

ArkTS1.2中实例方法被当作lambda对象传递时，会捕获上下文的this，避免类型不安全的行为。

**ArkTS1.1**

```typescript
class A {
  n: string = 'a'
  foo() { console.log (this.n) }
}
let a = new A()
const method = a.foo
method()   // 无法读取未定义的属性'n'.
```

**ArkTS1.2**

```typescript
class A {
  n: string = 'a'
  foo() { console.log (this.n) }
}
let a = new A()
const method = a.foo
method()   // 输出a
```

## namespace内方法不能重名

**规则：**`arkts-no-duplicate-function-name`

**级别：error**

由于ArkTS1.2中会将多个名称相同的namespace合并成一个namespace，所以namespace内方法不能重名，否则会导致冲突。

**ArkTS1.1**

```typescript
namespace A {
  export function foo() {  // 错误：命名空间 'A' 中重复导出函数 'foo'.
    console.log('test1');
  }
}

namespace A {
  export function foo() {  // 错误：命名空间 'A' 中重复导出函数 'foo'.
    console.log('test2');
  }
}

```

**ArkTS1.2**

```typescript
namespace A {
  export function foo1() {  // 重命名导出函数
    console.log('test1');
  }
}

namespace A {
  export function foo2() {
    console.log('test2');
  }
}
```

## arkts-no-ctor-prop-decls

**规则：**`arkts-no-ctor-prop-decls`

**级别：error**

ArkTS1.2不支持在constructor中声明类字段。在class中声明这些字段。

**ArkTS1.1**

```typescript
class A {
  constructor(readonly a: string) {
  }
}

class Base {
  readonly b: string = "base";
}

class A extends Base {
  constructor(override readonly b: string) {  // 违反规则
    super();
  }
}
```

**ArkTS1.2**

```typescript
class A {
  readonly a: string
  constructor(a: string) {
    this.a = a
  }
}

class Base {
  readonly b: string = "base";
}

class A extends Base {
  override readonly b: string;  // 显式声明字段
  constructor(b: string) {
    super();
    this.b = b;
  }
}

```

## 不支持tagged templates

**规则：**`arkts-no-tagged-templates`

**级别：error**

ArkTS1.2规范函数调用方式，支持字符串相加的用法，不支持Tagged templates（标签模板字符串）。

**ArkTS1.1**

```typescript
function myTag(strings: TemplateStringsArray, value: string): string {
    return strings[0] + value.toUpperCase() + strings[1];
}

const name = 'john';
const result = myTag`Hello, ${name}!`;
console.log(result);

function formatTag(strings: TemplateStringsArray, first: string, last: string): string {  
    return `${strings[0]}${first.toUpperCase()} ${last.toUpperCase()}${strings[1]}`;
}

const firstName = 'john';
const lastName = 'doe';
const result = formatTag`Hello, ${firstName} ${lastName}!`;  // 违反规则
console.log(result);
```

**ArkTS1.2**

```typescript
function myTagWithoutTemplate(strings: string, value: string): string {
    return strings + value.toUpperCase();
}

const name = 'john';

const part1 = 'Hello, ';
const part2 = '!';
const result = myTagWithoutTemplate(part1, name) + part2;
console.log(result);

function formatWithoutTemplate(greeting: string, first: string, last: string, end: string): string {  
    return greeting + first.toUpperCase() + ' ' + last.toUpperCase() + end;
}

const firstName = 'john';
const lastName = 'doe';
const result = formatWithoutTemplate('Hello, ', firstName, lastName, '!');  // 直接使用函数参数
console.log(result);
```

## 不支持确定赋值断言

**规则：**`arkts-no-definite-assignment`

**级别：error**

ArkTS1.2不支持确定赋值断言。改为在声明变量的同时为变量赋值。

**ArkTS1.1**

```typescript
let x!: number // 提示：在使用前将x初始化

initialize();

function initialize() {
  x = 10;
}

console.log('x = ' + x);
```

**ArkTS1.2**

```typescript
function initialize(): number {
  return 10;
}

let x: number = initialize();

console.log('x = ' + x);
```

## Record增加运行时类型

**规则：**`arkts-record-add-runtime-type`

**级别：error**

ArkTS1.2中对象字面量会生成类的实例。

**ArkTS1.1**

```typescript
let a: Record<string, number> = { 'v': 123 };  // Record是编译时类型，运行时仍是动态对象
a.v;  // 需要使用[]方式访问
```

**ArkTS1.2**

```typescript
let a: Record<string, number> = { 'v': 123 };  // Record是编译时类型，运行时仍是动态对象
console.info(a instanceof Record) // true
a['v'];  
```

## as具有运行时语义

**规则：**`arkts-no-ts-like-as`

**级别：error**

ArkTS1.1中的`as`只在编译时提供类型信息，如果类型断言失败，报错时机取决于后续的代码操作。

ArkTS1.2中的`as`会在运行时进行类型检查和可能的类型转换，如果类型断言失败，会立即抛出错误。

**ArkTS1.1**

```typescript
// ArkTS1.1
interface I {}
class A implements I {
  m: number = 0;
}

class B implements I {
  n: string = 'a';
}

let a: A = new A();
let i: I = a;
let t: B = i as B; // ArkTS1.1：正常编译运行，ArkTS1.2:运行时异常
t.n.toString();     // ArkTS1.1：运行时崩溃
```

**ArkTS1.2**

```typescript
// ArkTS1.2
interface I {}
class A implements I {
  m: number = 0;
}

class B implements I {
  n: string = 'a';
}

let a: A = new A();
let i: I = a;
if (i instanceof B) {
  let t: B = i as B;  // ArkTS1.2：运行时正常
  t.n.toString();     // ArkTS1.2：运行时正常
}
```

## catch语句中是error类型

**规则：**`arkts-no-ts-like-catch-type`

**级别：error**

在ArkTS1.1上catch语句中的e是any类型。因此，编译器不会对catch语句中的异常进行编译时类型检查。当ArkTS1.1上限制throw时，只能抛出Error类型。

在ArkTS1.2的静态模式中，类型必须明确，同时需考虑与ArkTS1.1的兼容性。对于catch(e)的语法，默认e为Error类型。

**ArkTS1.1**

```typescript
try {
  throw new Error();
} catch(e) {  // e是any类型
  e.message; // ArkTS1.1编译通过，运行正常
  e.prop;     // ArkTS1.1编译通过，输出undefined
}
```

**ArkTS1.2**

```typescript
try {
  throw new Error();
} catch(e:Error) {  // e是Error类型
  e.message;   // ArkTS1.2编译通过，运行正常
  e.prop;      // ArkTS1.2编译错误，需要将e转换成需要处理的异常类型，例如：(e as SomeError).prop
}
```

## 不支持逻辑赋值运算

**规则：**`arkts-unsupport-operator`

**级别：error**

1. 当前暂不支持&&=, ||=, ??=逻辑赋值运算符，通过迁移工具提示开发者修改源码，不提供自动修复能力。

**ArkTS1.1**

```typescript
let a = 1;
a &&= 2;    // 结果: 2，ArkTS1.2暂不支持
a ||= 3;   // 结果: 2，ArkTS1.2暂不支持
a ??= 4;  // 结果: 2，ArkTS1.2暂不支持
```

**ArkTS1.2**

```typescript
let a = 1;
a = a && 2;   // 结果: 2
a = a || 3;   // 结果: 2
a = a ?? 4;   // 结果: 2
```

## 非十进制bigint字面量

**规则：**`arkts-only-support-decimal-bigint-literal`

**级别：error**

 当前暂不支持非十进制bigint字面量，通过迁移工具提示开发者修改源码，不提供自动修复能力。

**ArkTS1.1**

```typescript
let a1: bigint = 0xBAD3n;  // 十六进制字面量，ArkTS1.2暂不支持
let a2: bigint = 0o777n;   // 八进制字面量，ArkTS1.2暂不支持
let a3: bigint = 0b101n;  // 二进制字面量，ArkTS1.2暂不支持
```

**ArkTS1.2**

```typescript
let a1: bigint = BigInt(0xBAD3);
let a2: bigint = BigInt(0o777);
let a3: bigint = BigInt(0b101);
```

## 数值类型和bigint类型的比较

**规则：**`arkts-numeric-bigint-compare`

**级别：error**

 当前暂不支持数值类型和bigint类型的比较，迁移工具将提示开发者修改源码，不提供自动修复能力。

**ArkTS1.1**

```typescript
let n1: number = 123;
let n2: bigint = 456n;

n1 <= n2;   // 编译通过
n1 == n2;   // 编译失败
n1 >= n2;   // 编译通过
```

**ArkTS1.2**

```typescript
let n1: number = 123;
let n2: bigint = 456n;

BigInt(n1) <= n2;
BigInt(n1) == n2;
BigInt(n1) >= n2;
```

## new Number/Boolean/String不再是"object"类型

**规则：**`arkts-primitive-type-normalization`

**级别：error**

1. 在ArkTS1.2中primitive type和boxed type是相同的类型，这样可以提高语言一致性和性能。
   比较Number/Boolean/String时比较的是值而不是对象。

2. 在ArkTS1.1上，boxed类型通过new创建。在获取其类型、比较boxed类型对象时会产生意外行为，这是因为对象比较时是通过引用进行比较，而不是值。通常直接使用primitive 
   type性能更高效，内存占用更少（相比之下对象会占用更多内存）。

**ArkTS1.1**

```typescript
typeof new Number(1) // 结果: "object"
new Number(1) == new Number(1);  //结果: false
if (new Boolean(false)) {} // 在if语句中new Boolean(false)为true
```

**ArkTS1.2**

```typescript
typeof new Number(1)// 结果: "number"
new Number(1) == new Number(1);  //结果: true
if (new Boolean(false)) {}      // 在if语句中new Boolean(false)为false
```

## enum的元素不能作为类型

**规则：**`arkts-no-enum-prop-as-type`

**级别：error**

ArkTS1.1上的枚举是编译时概念，在运行时仍是普通对象。ArkTS1.2遵循静态类型，需要在运行时为enum提供类型。因此，ArkTS1.2上枚举的每个元素是枚举类的实例（在运行时才确定），无法成为编译时的静态类型信息。这与ArkTS1.2整体类型设计上不支持实例类型相违背。

**ArkTS1.1**

```typescript
enum A { E = 'A' }
function foo(a: A.E) {}
```

**ArkTS1.2**

```typescript
enum A { E = 'A' }
function foo(a: 'A') {}

// ...
enum A { E = 'A' }
function foo(a: A) {}
```

## 不支持debugger 

**规则：**`arkts-no-debugger`

**级别：error**

1. 静态类型语言具备编译时检查和强类型约束，调试通常由IDE完成，已具备较强大的调试机制。

2. debugger会侵入式修改源码。

3. debugger语句会被优化，造成行为不一致。

**ArkTS1.1**

```typescript
// ArkTS1.1 
// ...
debugger;
// ...
```

**ArkTS1.2**

```typescript
// ArkTS1.2   移除debugger语句
// ...
```

## 不支持空数组/稀疏数组 

**规则：**`arkts-no-sparse-array`

**级别：error**

1. ArkTS1.2遵循静态类型，空数组需要能根据上下文推导出数组元素的类型，否则会有编译错误。

2. ArkTS1.2的数组是连续存储的，空位（如 [1, , , 2]）会浪费内存。‌

3. ArkTS1.2遵循空值安全，无法使用默认undefined表示空缺。

**ArkTS1.1**

```typescript
let a = []; // ArkTS1.2，编译错误，需要从上下文中推导数组类型
let b = [1, , , 2]; // 不支持数组中的空位
b[1];  // undefined 
```

**ArkTS1.2**

```typescript
let a: number[] = [];  // 支持，ArkTS1.2上可以从上下文推导出类型
let b = [1, undefined, undefined, 2];
```

## 智能类型差异

**规则：**`arkts-no-ts-like-smart-type`

**级别：error**

在ArkTS1.1中，由于对象不是线程间共享的，编译器在做类型推导和分析时无需考虑并发场景。

在ArkTS1.2中，由于对象是多线程共享的，编译器在做类型推导和分析时需要考虑并发场景下变量类型/值的变化。

**智能转换：** 编译器会在某些场景下（如instanceof、null检查、上下文推导等）识别出对象的具体类型，自动将变量转换为相应类型，而无需手动转换。

**ArkTS1.1**

```typescript
class AA {
  public static instance?: number;
  getInstance(): number {
    if (!AA.instance) {
      return 0;
    }
    return AA.instance;       // ArkTS1.2编译错误，返回值和返回类型不匹配
  }
}
```

**ArkTS1.2**

```typescript
class AA {
  public static instance?: number;
  getInstance(): number {
    let a = AA.instance       // ArkTS1.2上，需要通过局部变量做智能转换
    if (!a) {
      return 0;
    }
    return a;
  }
}
```

## 数组/元组类型在继承关系中遵循不变性原则

**规则：**`arkts-array-type-immutable`

**级别：error**

ArkTS1.2上数组在继承关系中遵循不变性原则，可以通过编译时检查保证类型安全，将潜在的运行时错误提前到编译期，避免运行时失败，从而提高执行性能。

**ArkTS1.1**

```typescript
class A {
  a: number = 0;
}

class B {
  b: number = 0;
}

// ArkTS1.1 
let arr1: A[] = [new A()];
let arr2: (A | B)[] = arr1;      // ArkTS1.2编译错误
```

**ArkTS1.2**

```typescript
class A {
  a: number = 0;
}

class B {
  b: number = 0;
}

// ArkTS1.2 
let arr1: [ A | B ] = [new A()];
let arr2: [ A | B ] = arr1;       // 需要相同类型的元组
```

## 默认参数必须放在必选参数之后

**规则：**`arkts-default-args-behind-required-args`

**级别：error**

默认参数放在必选参数之前没有意义，ArkTS1.1上调用该接口时仍须传递每个默认参数。

**ArkTS1.1**

```typescript
function add(left: number = 0, right: number) { 
  return left + right;
}
```

**ArkTS1.2**

```typescript
function add(left: number, right: number) {
  return left + right;
}
```

## class的懒加载

**规则：**`arkts-class-lazy-import`

**级别：error**

ArkTS1.2的类在使用时进行加载或初始化，以提升启动性能，减少内存占用。

**ArkTS1.1**

```typescript
class C {
  static {
    console.info('init');  // ArkTS1.2上不会立即执行
  }
}
```

**ArkTS1.2**

```typescript
// ArkTS1.2  如果依赖没有被使用的class执行逻辑，那么将该段逻辑移出class
class C {
  static {}
}
console.info('init');
```

## 方法继承/实现参数遵循逆变原则，返回类型遵循协变原则

**规则：**`arkts-method-inherit-rule`

**级别：error**

ArkTS1.2子类方法覆写父类方法，参数类型须遵循逆变原则，可以通过编译时检查保证类型安全，将潜在的运行时错误提前到编译期，避免运行时失败，无需运行时检查，从而提高执行性能。

**逆变/协变：** 用来描述类型转换后的继承关系，如果A、B表示类型，f()表示类型转换，≤表示继承关系（A≤B表示A是由B派生出来的子类），则有：

- f()为逆变时，当A≤B时有f(B)≤f(A)成立。

- f()为协变时，当A≤B时有f(A)≤f(B)成立。

**ArkTS1.1**

```typescript
// ArkTS1.1  
class A {
  a: number = 0;
}
class B {
  b: number = 0;
}

class Base {
  foo(obj: A | B): void {}
}
class Derived extends Base {
  override foo(obj: A): void {      // 可以覆写父类方法，ArkTS1.2编译错误
    console.info(obj.a.toString());
  }
}
```

**ArkTS1.2**

```typescript
// ArkTS1.2
class A {
  a: number = 0;
}
class B {
  b: number = 0;
}

class Base {
  foo(obj: A | B): void {}
}
class Derived extends Base {
  override foo(obj: A | B): void {
    if (obj instanceof A) {
      console.info(obj.a.toString());
    }
  }
}
```

## Enum不可以通过索引访问成员

**规则：**`arkts-enum-no-props-by-index`

**级别：error**

1. ArkTS1.1上已对索引访问元素的语法做了限制，ArkTS1.2对枚举场景增强约束。具体内容请参考[不支持通过索引访问字段](typescript-to-arkts-migration-guide.md#不支持通过索引访问字段)。

2. ArkTS1.1上枚举是动态对象，ArkTS1.2是静态类型，枚举具有运行时类型。为获得更高的性能，对[]访问做了限制。

**ArkTS1.1**

```typescript
enum TEST {
  A,
  B,
  C
}

TEST['A'];       // ArkTS1.2上不支持这种语法
TEST[0];    // ArkTS1.2上不支持这种语法
```

**ArkTS1.2**

```typescript
enum TEST {
  A,
  B,
  C
}

TEST.A;          // 使用.操作符或者enum的值
TEST.A.getName();  // 使用enum对应的方法获取enum的key
```

## 对象没有constructor

**规则：**`arkts-obj-no-constructor`

**级别：error**

ArkTS1.2支持天然共享的能力，运行时需要确定类型信息。实现上不再基于原型的语言，而是基于class的语言。

**ArkTS1.1**

```typescript
class A {}
let a = new A().constructor;   // ArkTS1.2上编译错误
```

**ArkTS1.2**

```typescript
class A {}
let a = new A();
let cls = Type.of(a); 
```

## 子类有参构造函数需要显式定义，且必须调用父类的构造函数

**规则：**`arkts-subclass-must-call-super-constructor-with-args`

**级别：error**

1. ArkTS1.1在运行时没有对函数调用的检查，同时利用arguments机制获取所有参数（ArkTS1.2上不支持这个特性）并传入父类构造函数。ArkTS1.2对函数参数的个数和类型会进行编译时检查，确保程序的安全和正确性，因此ArkTS1.2上不支持这种写法。

2. ArkTS1.2支持方法重载，构造函数可能有多个实现体，在ArkTS1.2上支持这个特性会造成子类继承父类时的二义性。

**ArkTS1.1**

```typescript
class A {
  constructor(a: number) {}
}
class B extends A {}                // ArkTS1.2上编译报错
let b = new B(123);
```

**ArkTS1.2**

```typescript
class A {
  constructor(a: number) {}
}
class B extends A {
  constructor(a: number) {
    super(a)
  }
}
let b = new B(123);
```

## 不支持可选元组类型

**规则：**`arkts-no-optional-tuple`

**级别：error**

ArkTS1.2不支持可选元组类型。通过编译时检查保证类型安全，将潜在的运行时错误提前到编译期，避免运行时失败，从而提高执行性能。

**ArkTS1.1**

```typescript
let t: [number] = [1];
let t1: [number, boolean?] = t;   // ArkTS1.2编译错误
```

**ArkTS1.2**

```typescript
let t: [number] = [1];
let t1: [number, boolean] | [number] = t;
```

## 不支持超大数字字面量

**规则：**`arkts-no-big-numeric-literal`

**级别：error**

1. ArkTS1.2支持更多数值类型细化，可以获得更好的性能。超出int/long/double范围的数字字面量会有编译错误。

2. 支持隐式转换会造成额外的性能损耗。

3. 浮点数据的隐式转换可能带来精度的损失，违反开发者预期。清晰的数值边界可以提升代码准确性和可读性。

**ArkTS1.1**

```typescript
let s = 1000000000000000000000000000000000000; // ArkTS1.1会转换成浮点形式数据，ArkTS1.2编译错误
let t = 1E+309;                               // ArkTS1.1会转换为Infinity，ArkTS1.2编译错误
```

**ArkTS1.2**

```typescript
let s = 1000000000000000000000000000000000000.0; // ok，浮点形式数据
let t = Infinity;                                // ok，值为Infinity
```

## class/interface的变量名称需要是合法标识符

**规则：**`arkts-identifier-as-prop-names`

**级别：error**

1. ArkTS1.1上已经进行约束，ArkTS1.2对边界场景增强约束。详细内容请参考[对象的属性名必须是合法的标识符](typescript-to-arkts-migration-guide.md#对象的属性名必须是合法的标识符)。

2. 静态类型中对属性的访问是静态的，可以获得更好的执行性能。

3. 使用字符串作为属性名称可能带来二义性。

**ArkTS1.1**

```typescript
class A {
  's' = 1;
}
```

**ArkTS1.2**

```typescript
class A {
  s = 1;
}
```

## 子类不可以声明和父类的方法同名的lamada类型的属性

**规则：**`arkts-no-subclass-lamada-prop-name-same-as-superclass-method`

**级别：error**

不同于ArkTS1.1上的动态对象（属性和方法一致），ArkTS1.2上的属性与方法有本质区别。属性用以保存类实例的状态，是可变的。方法定义类对象的行为或功能，被类的所有实例所共有，不能被改变。

同时，ArkTS1.1和ArkTS1.2不支持属性和实例方法同名。因此在ArkTS1.2上，类的继承关系中不能将同名属性和方法相互覆写。

**ArkTS1.1**

```typescript
class A {
  foo() {
    console.info('A');
  }
}

class B extends A {
  foo: () => void = () => {
    console.info('B');
  }
}
```

**ArkTS1.2**

```typescript
class A {
  foo() {
    console.info('A');
  }
}

class B extends A {
  foo() {
    console.info('B');
  }
}
```

## 子类不能在static context中调用super

**规则：**`arkts-no-super-call-in-static-context`

**级别：error**

1. ArkTS1.2不再基于原型实现继承。没有原型/构造函数的概念，无法实现动态替换原型，因此无需通过super动态访问父类。

2. super定义在子类的静态上下文中，容易混淆super的指向，与在实例方法中super指向父类实例相冲突，造成开发者的混用。使用类名的方式访问静态成员更清晰、可维护，易于开发者理解。

**ArkTS1.1**

```typescript
class A {
  static foo() {
    return 123;
  }
}

class B extends A {
  static foo() {
    return super.foo() + 456;
  }
}
```

**ArkTS1.2**

```typescript
class A {
  static foo() {
    return 123;
  }
}

class B extends A {
  static foo() {
    return A.foo() + 456;
  }
}
```

## 类继承含属性的接口时，需要实现属性的get/set方法

**规则：**`arkts-class-implement-interface-prop-getter-setter`

**级别：error**

ArkTS1.2遵循严格的类型检查，可以通过编译时检查保证类型安全，将潜在的运行时错误提前到编译期，避免运行时失败，从而提高执行性能。

**ArkTS1.1**

```typescript
interface I {
  v: number
}

class A implements I {
  get v(): number {
    return 1;
  }
}
```

**ArkTS1.2**

```typescript
interface I {
  readonly v: number
}

class A implements I {
  get v(): number {
    return 1;
  }
}
```

## 不能将超出枚举范围的值赋值给枚举类型的变量

**规则：**`arkts-out-of-enum-index`

**级别：error**

ArkTS1.2上枚举类型是类型安全的，编译器会进行严格检查，避免应用中的非预期行为或错误。同时，枚举的值是编译时确定的，如果在运行时赋值超出范围的值，会对开发者造成困惑，降低易用性（TS在新版本上也增强了枚举场景的编译检查）。

**ArkTS1.1**

```typescript
enum T {
  A = 0,
  B = 1,
  C = 2
}

let num: number = 123;

let t1: T = 0;
let t2: T = -1;
let t3: T = num;
```

**ArkTS1.2**

运行时赋值枚举类型在ArkTS1.2上没有直接的替代写法。如果想超出枚举范围赋值，建议使用类/容器等其他数据结构实现。

## 不支持不定长的元组类型

**规则：**`arkts-no-unfixed-len-tuple`

**级别：error**

ArkTS1.2上不支持可变元组，可以通过编译时检查保证类型安全，将潜在的运行时错误提前到编译期，避免运行时失败，从而提高执行性能。

**ArkTS1.1**

```typescript
const s: [string, ...boolean[]]=['', true];
```

**ArkTS1.2**

```typescript
const s: (string | boolean)[] =['', true];
```

## 类实例不支持关系表达式

**规则：**`arkts-no-class-instance-relational-expression`

**级别：error**

1. ArkTS1.2中遵循类型安全，为避免隐式转化行为，关系表达式的操作符必须是数值类型、字符串类型、布尔类型、枚举类型。同时，支持隐式转化可能引发非预期的异常。

2. 对象的比较缺乏默认语义，为了语言的一致性和明确性，不支持不同对象的比较。

**ArkTS1.1**

```typescript
class A {
  valueOf () {
    return 3;
  }
}

class B {
  valueOf () {
    return 4;
  }
}

let a = new A();
let b = new B();
console.info('a<b:', a < b);
```

**ArkTS1.2**

```typescript
class A {
  valueOf () {
    return 3;
  }
}

class B {
  valueOf () {
    return 4;
  }
}

let a = new A();
let b = new B();
console.info(a.valueOf() < b.valueOf());
```

## instanceof的目标类型不能是函数

**规则：**`arkts-no-instanceof-func`

**级别：error**

ArkTS1.2上不再基于原型实现继承，没有原型/构造函数的概念，不能通过任意函数创建对象。因此instanceof的目标类型不能是函数。

**ArkTS1.1**

```typescript
function foo() {}
function bar(obj: Object) {
  console.info('obj instanceof foo :' ,obj instanceof foo);
}
```

**ArkTS1.2**
```typescript
function bar(obj: Object) {
console.info('obj instanceof foo :', obj instanceof string);
}
```

## 静态加载包内模块某一文件时ohmurl路径变更

**规则：**`arkts-ohmurl-path-change`

**级别：error**

ArkTS1.2中在静态加载包内模块某一文件时ohmurl路径必须写全，不可省略路径中的"src/main"。

**ArkTS1.1**

```typescript
// library/ets/components/Index.ets
import { MainPage } from 'library/ets/components/MainPage'
```

**ArkTS1.2**

```typescript
// library/ets/components/Index.ets
import { MainPage } from 'library/src/main/ets/components/MainPage'
```