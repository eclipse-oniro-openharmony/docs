# @ohos.util.json (JSON解析与生成)

本模块提供了将JSON文本转换为JSON对应对象或值，以及将对象转换为JSON字符串等功能。

>**说明：**
>
>本模块首批接口从API version 12开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```
import JSON from '@ohos.util.json';
```

## Transformer

用于转换结果函数的类型。

**系统能力：** SystemCapability.Utils.Lang

| 类型 | 说明 |
| -------- | -------- |
| (this: Object, key: string, value: Object) => Object \| undefined \| null | 转换结果函数。|

## JSON.parse

parse(text: string, reviver?: Transformer): Object | null

用于解析JSON字符串生成对应ArkTS对象或null。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型   | 必填 | 说明            |
| ------ | ------ | ---- | --------------- |
| text   | string | 是 | 有效的JSON字符串。|
| reviver  | [Transformer](#transformer) | 否 | 转换函数，传入该参数，可以用来修改解析生成的原始值。默认值是undefined。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Object \| null | 返回ArkTS对象或null。当入参是null时，返回null。|

**示例：**

```ts
import JSON from '@ohos.util.json';

let jsonText = '{"name": "John", "age": 30, "city": "ChongQing"}';
let obj = JSON.parse(jsonText);
```


## JSON.stringify

stringify(value: Object, replacer?: (number | string)[] | null, space?: string | number): string

该方法将一个ArkTS对象或数组转换为JSON字符串。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | ArkTS对象或数组。|
| replacer | number[] \| string[] \| null | 否 | 当参数是数组时，只有包含在这个数组中的属性名才会被序列化到最终的JSON字符串中；当参数为null或者未提供时，则对象所有的属性都会被序列化。默认值是undefined。|
| space | string \| number | 否 | 指定缩进用的空格或字符串或空字符串，用于美化输出。当参数是数字时表示有多少个空格；当参数是字符串时，该字符串被当作空格；当参数没有提供或者是null时，将没有空格。默认值是空字符串。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 转换后的JSON字符串。|

**示例：**

```ts
interface Person {
  name: string;
  age: number;
  city: string;
}
let obj = {"name": "John", "age": 30, "city": "ChongQing"} as Person;
let str1 = JSON.stringify(obj, ["name"]);
```


## JSON.stringify

stringify(value: Object, replacer?: Transformer, space?: string | number): string

该方法将一个ArkTS对象或数组转换为JSON字符串。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| value | Object | 是 | ArkTS对象或数组。|
| replacer | [Transformer](#transformer) | 否 | 在序列化过程中，被序列化的值的每个属性都会经过该函数的转换和处理。默认值是undefined。|
| space | string \| number | 否 | 指定缩进用的空格或字符串或空字符串，用于美化输出。当参数是数字时表示有多少个空格；当参数是字符串时，该字符串被当作空格；当参数没有提供或者是null时，将没有空格。默认值是空字符串。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| string | 转换后的JSON字符串。|

**示例：**

```ts
function replacer(key: string, value: Object): Object {
  if (typeof value === "string") {
    return value.toUpperCase();
  }
  return value;
}
interface Person {
  name: string;
  age: number;
  city: string;
}

let obj = {"name": "John", "age": 30, "city": "ChongQing"} as Person;
let str2 = JSON.stringify(obj, replacer);
```


## JSON.has

has(obj: object, property: string): boolean

检查ArkTS对象或数组是否包含某种属性，可用于[JSON.parse](#jsonparse)解析JSON字符串之后的相关操作。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| obj | object | 是 | ArkTS对象或数组。|
| property | string | 是 | 属性名。|

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| boolean | 返回ArkTS对象是否包含某种属性结果，true表示包含，false表示不包含。|

**示例：**

```ts

const jsonText = '{"name": "John", "age": 30, "city": "ChongQing"}';
let obj = JSON.parse(jsonText);
let rst = JSON.has(obj, "name");
```


## JSON.remove

remove(obj: object, property: string): void

从ArkTS对象或数组中删除某种属性，可用于[JSON.parse](#jsonparse)解析JSON字符串之后的相关操作。

**系统能力：** SystemCapability.Utils.Lang

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| obj | object | 是 | ArkTS对象或数组。|
| property | string | 是 | 属性名。|

**示例：**

```ts

const jsonText = '{"name": "John", "age": 30, "city": "ChongQing"}';
let obj = JSON.parse(jsonText);
let rst = JSON.remove(obj, "name");
```